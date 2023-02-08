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

&nbsp;&nbsp;2개의 페이지에서 엑셀 파일 다운로드 시 스피너가 계속 돌면서 도중에 다른 작업을 하지 못하는 문제가 있다고 연락이 왔다.
첫 번째 페이지는 csv파일을 xlsx로 변환하여 메일 첨부 발송, 파일 비밀번호는 문자 발송 해주는 방식,
두 번째 페이지는 AWS Athena query를 통해 조회한 데이터를 xlsx 파일로 생성하여 메일 첨부 발송, 파일 비밀번호는 문자 발송해주는 방식이다.
약 1만 건부터 50만 건 사이의 데이터인데 당연하게도 데이터가 많을 수록 행이 오래 걸렸다.

먼저 첫 번째 페이지의 문제를 파악해보니,  
1. csv 파일을 xlsx로 변환할 때 stream 처리가 되어있지 않았다.
2. 비동기 처리가 되어있지 않았다.

기존 코드
1) csv → xlsx 변환
2) xlsx 파일 암호화
3) 
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
if (fs.existsSync(excelFilePath)) {
    // excel file 암호화
    const workbook = await XlsxPopulate.fromFileAsync(excelFilePath);
    await workbook.toFileAsync(excelFilePath, {
        password: excelPassword,
    });
    // 첨부파일 메일 전송
    mail.attachments[0].content = fs.readFileSync(excelFilePath);
    // mail.attachments[0].content = fs.createReadStream(excelFilePath);
    mail.attachments[0].filename = `${getKoreanFilename(
        path.basename(excelFilePath)
    )}`;
    const sendMailResultId = await sendMail(mail);
    if (sendMailResultId) {
        // 메일 발송 성공했을 때 문자로 엑셀 파일 비밀번호 발송
        const sendInfo = {
            msgType: "LMS",
            title: "Biz Campaign Manager",
            receivers: user.mobile.replace(/\-/g, ""),
            message: `Biz Campaign Manager 다운로드 파일 첨부 메일이 발송 되었습니다.\n\nExcel 파일 비밀번호: ${excelPassword}`,
        };
        const result = await campaignService.sendSmsLms(sendInfo);
        console.log(result.config.params);
        console.log(result.data);
    }
} else {
    console.log("Excel 파일 생성 오류입니다.");
    throw new NotFoundError("Excel 파일이 존재하지 않습니다.");
}

res.status(200).json({
    result: {
        code: 2000,
        message: "success",
    },
});
```