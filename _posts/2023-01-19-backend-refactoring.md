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
- backend
- refactoring 
author: wgmin0416
paginate: false
---
&nbsp;&nbsp;node.js, react로 구성 된 마케팅과 관련된 프로젝트를 담당하고 있다.
2021년 초 개발 시작 단계부터 지금까지 여러 개발자의 손을 거쳐오고, 다양한 기능이 추가/변경 되면서 점점 개발 속도가 더뎌지게 되었다. <br/>
&nbsp;&nbsp;그래서 2023년 node.js 공부 계획을 이 프로젝트를 리팩토링 하는 것으로 목표를 세웠다.
지금도 새로운 기능들이 추가되고 있지만 이번 요건이 마무리 되는대로 잠시 틈을 타 정리하려고 한다.<br/>
&nbsp;&nbsp;*(효과적인 리팩토링을 위해 먼저 '클린코드'라는 책을 빠르게 읽고 시작하려고 한다.)* 

<b>리팩토링의 목적</b><br/>
1순위. 개발 속도 향상<br/>
2순위. 쉬운 코드 이해<br/>
3순위. 성능 개선<br/>
<br/>
<b>리팩토링 작업 순서</b><br/>
1)&nbsp;모든 기능 파악하기<br/>
2)&nbsp;테스트 환경 만들기<br/>
3)&nbsp;리팩토링 필요한 부분 정리하기<br/>
4)&nbsp;리팩토링 작업

<b>계획</b>

| 기간 | 내용 |
| -- | ------ |
| 23.01.19 ~ 23.01.31 | 클린코드 읽기 |
| 23.02.01 ~ 23.02.10 | 기능 파악 |
| 23.02.10 ~ 23.02.28 | 리팩토링 작업 |
| 23.03.01 ~ 23.03.10 | 통합 테스트 |

도중에 다른 업무를 진행할 확률이 높아 조금은 현실성있게 기간을 설정했다.<br/>
이 포스트에 리팩토링 진행 상황을 좀 더 자세히 꾸준히 덧붙이려고 한다.