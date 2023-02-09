---
date: 2023-02-08 13:12:01
layout: post
title: node.js 엑셀(excel) 파일 다운로드 스트림, 비동기 처리
subtitle: excel file create stream, csv to xlsx, asynchronous
description: 엑셀 파일 다운로드 속도 개선
image: /assets/img/posts/2023-02-08-daily-error/excel.png
optimized_image: /assets/img/posts/2023-02-08-daily-error/excel.png
category: dev
tags:
 - node.js
author: wgmin0416
paginate: false
---

<h3>문제 발생</h3>
&nbsp;&nbsp;엑셀 파일 다운로드 시 스피너가 계속 돌면서 도중에 다른 작업을 하지 못하는 문제가 있었다.
약 1만 건부터 50만 건 정도의 데이터였고 더 많을 수록 행이 더 오래 걸렸다.  
&nbsp;&nbsp;사용자가 다운로드 버튼을 누르고 다른 작업을 할 수 있도록 비동기 처리가 필요했다.
또한 파일 처리 속도를 개선하고 메모리 부하를 줄여 다른 작업 시 블락되지 않도록 해야했다.
엑셀 파일을 다운로드 하는 페이지가 두 곳이 있었는데 로직이 조금 달라서 따로 확인하여 수정했다.  


<hr/>

<h3>원인 파악</h3>
- 첫 번째 페이지의 전체 로직  
1) csv → xlsx 변환  
2) xlsx 파일 암호화(xlsx-populate)  
3) 메일(첨부파일), 문자(비밀번호) 발송

속도를 저하시키는, 메모리를 과도하게 사용하는 부분 2가지를 수정했다.  
1) csv → xlsx 변환 시 stream 처리  
2) xlsx 파일 암호화 시 느림 → zip 압축 후 zip 파일 암호화(minizip-asm.js)  

- 두 번째 페이지의 전체 로직  
1) AWS Athena query를 통해 데이터 조회  
2) xlsx 파일 생성  
3) 메일(첨부파일), 문자(비밀번호) 발송  

두 번째 페이지에서 Athena query는 약 4~5초정도 걸렸는데 xlsx 파일 생성이 느렸다.  
1) xlsx 파일 생성 시 stream 처리

<hr/>

<h3>문제 해결</h3>

```javascript
// source(csv file path), destination(xlsx file path), callback 함수
const csvToExcel = async (source, destination, callback) => {
    if (typeof source !== "string" || typeof destination !== "string") {
        throw new Error(
            `"source" and "destination" arguments must be of type string.`
        );
    }
    // source exists
    if (!fs.existsSync(source)) {
        throw new Error(`source "${source}" doesn't exist.`);
    }
    // read stream
    const reader = fs.createReadStream(source);
    // write stream
    const xlsxWriter = new xlsxWriteStream(destination);
    const writeStream = xlsxWriter
        .getReadStream()
        .pipe(fs.createWriteStream(destination));
    // read line by line
    const lineReader = readline.createInterface({
        input: reader,
        crlfDelay: Infinity,
    });
    lineReader.on("line", (line) => {
        const lineData = line.toString();
        if (lineData) {
            xlsxWriter.addRow({ column_name: lineData });
        }
    });
    lineReader.on("close", () => {
        xlsxWriter.finalize();
    });
    lineReader.on("error", (error) => {
        xlsxWriter.finalize();
    });
    writeStream.on("finish", () => {
        if (fs.existsSync(destination)) {
            callback(destination);
        }
    });
};
```

```javascript
// 비밀번호 8자리 생성
const excelPassword = Math.random().toString(36).slice(-8);
// 메일 발송 양식
const mail = { ... }
// excel 다운 폴더 생성
const excelDir = 경로
if (!fs.existsSync(excelDir)) {
    fs.mkdirSync(excelDir, { recursive: true, mode: 0o755 });
}
// excel 파일 경로
const excelFilePath = excelDir + "파일명" + ".xlsx";
// csv 파일을 excel 파일로 변환
await csvToExcel(csvFilePath, excelFilePath);
// excel file 암호화
const workbook = await XlsxPopulate.fromFileAsync(excelFilePath);
await workbook.toFileAsync(excelFilePath, {
    password: excelPassword,
});
// 첨부파일 메일 전송
// 메일 발송 성공했을 때 문자로 엑셀 파일 비밀번호 발송
res.status(200).json({
    result: {
        code: 2000,
        message: "success",
    },
});
```

<hr/>

<h3>문제를 해결하며 배운 것</h3>

<h1>(작성중..)</h1>