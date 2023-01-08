---
date: 2023-01-02 22:10:00
layout: post
title: Python 공부하기 1일차
subtitle: 2023-01-02
description: 프로그래머스 Lv.0
image: /assets/img/posts/2023-01-02-python-algorithm-1/thumbnail.png
optimized_image: /assets/img/posts/2023-01-02-python-algorithm-1/thumbnail.png
category: python
tags:
  - python
  - algorithm
author: wgmin0416
---
Python 기초부터 공부하기
===
회사에서 Python과 Django 프레임워크를 만들어진 서비스를 담당하고 있지만, 쓰는 문법만 사용하게 되고 외워서 쓰지 못하는 문제점이 있어서
기초부터 다시 학습하기로 다짐했다. 프로그래머스 Lv.0 알고리즘부터 차근차근 풀어나가며 다른 사람들의 풀이에서 많이 배울 생각이다.

> 몫 구하기

#### 문제<br>
정수 num1, num2가 매개변수로 주어질 때, num1을 num2로 나눈 몫을 return 하도록 solution 함수를 완성해주세요.
0 < num1 ≤ 100
0 < num2 ≤ 100
```python
def solution(num1, num2):
    return int(num1/num2)
```
나눈 뒤 int()를 통해 정수를 return 하였다.


다른 사람의 풀이
```python
solution = int.__floordiv__
```
operatior.__floordiv__(a,b) 라는 python 연산 내장함수가 있다.
a//b 의 결과 값을 보여주는 값이다.