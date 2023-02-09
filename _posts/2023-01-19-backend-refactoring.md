---
date: 2023-01-19 07:01:13
layout: post
title: "node.js 백엔드 리팩토링"
subtitle: node.js backend refactoring
description: node.js study
image: /assets/img/posts/maze.jpg
optimized_image: 
category: dev
tags:
- node.js
author: wgmin0416
paginate: false
---
&nbsp;&nbsp;node.js, react로 구성 된 마케팅과 관련된 프로젝트를 담당하고 있다.
2021년 초 개발 시작 단계부터 지금까지 여러 개발자의 손을 거쳐오고, 다양한 기능이 추가/변경 되면서 점점 개발 속도가 더뎌지게 되었다. <br/>
&nbsp;&nbsp;그래서 2023년 node.js 공부 계획을 이 프로젝트를 리팩토링 하는 것으로 목표를 세웠다.
지금도 새로운 기능들이 추가되고 있지만 이번 요건이 마무리 되는대로 잠시 틈을 타 정리하려고 한다.<br/>

<b>리팩토링 하는 이유</b><br/>
1) 불필요한 폴더나 폴더 카테고리에 맞지 않는 위치에 존재하는 파일이 많다.
2) 여러 개발자를 거쳐와 코드 스타일이 매우 다르다.
3) 비슷한 기능의 함수들이 여러 개, 예상할 수 없는 위치에 존재하여 다음에 활용하기 힘들다.
4) 기능이 확장되면서 기존에 하드코딩 되어있던 부분들로 추가 요건에 대한 개발 속도가 더뎌졌다.
5) 성능 개선이 필요한 부분들이 있다.

<b>리팩토링의 목적</b><br/>
1순위. 개발/디버깅 속도 향상<br/>
2순위. 누가 봐도 쉬운 코드 이해<br/>
3순위. 성능 개선<br/>
<br/>

<b>계획</b>

| 기간 | 내용 |
| -- | ------ |
| 23.01.19 ~ 23.01.31 | 기능 파악 |
| 23.02.01 ~ 23.02.28 | 리팩토링 작업 |
| 23.03.01 ~ 23.03.10 | 통합 테스트 |

도중에 다른 업무를 진행할 확률이 높아 조금은 현실성있게 기간을 설정했다.<br/>
이 포스트에 리팩토링 진행 상황을 좀 더 자세히 꾸준히 덧붙이려고 한다.

<hr/>

23.02.09 리팩토링 일지
역시나 우선적으로 해결해야하는 업무들이 생겨 리팩토링을 미룰 수 밖에 없었다.
```
+-- src
    +-- scheduler
        +-- scheduleJob1.js
        +-- scheduleJob2.js
        +-- scheduleJob3.js
        +-- ...
    +-- service
        +-- scheduleJob1Service.js
        +-- scheduleJob2Service.js
        +-- scheduleJob3Service.js
```
현재 디렉토리 구조는 위와 같이 Schedule Job에 따라 나뉘어 있고, 각 Job 별로 비즈니스 로직이 있는 jobService이 존재한다.
비즈니스 로직이 service에만 있지 않고 중구난방으로 있는 상태이며 
Job별로 service가 나뉘어 있지만 같은 로직을 쓰는 경우가 존재해서
service를 어떤 식으로 나눌지 고민했다. 
(예를 들어 scheduleJob1Service.js와 scheduleJob2Service.js에 같은 비즈니스 로직이 생기는 경우가 있다.)

&nbsp;&nbsp;일단 함수는 공통 기능부터 시작하여 작은 단위부터 빼려고 한다. Sequelize ORM을 사용하고 있기 때문에 DB CRUD는
최대한 model 내에 정의하려고 한다. (Select 같은 경우는 로직 상 테이블 join이 많아 model에 정의하는게 더 비효율적이라 생각이 들었다.)
AWS S3 upload, delete나 file 입출력, log 및 외부 API 요청을 위해 필요한 함수들은 utils에 정리하려고 한다.  
사실 구조가 매우 중요하기 때문에 한 번에 확정짓지 않고 한 주 정도 더 고민해보면서 같은 팀 시니어 분께 조언을 구할 예정이다.