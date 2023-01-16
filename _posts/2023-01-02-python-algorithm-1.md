---
date: 2023-01-02 22:10:00
layout: post
title: Python 공부하기 1일차
subtitle: 2023-01-02
description: 프로그래머스 Lv.0
image: 
optimized_image: /assets/img/posts/python_image.png
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

***

<h2>몫 구하기</h2> 
##### 문제<br>
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
operation.__floordiv__(a,b) 라는 python 연산 내장함수는 a//b 의 결과를 보여준다.
a//b 의 결과 값을 보여주는 값이다.

<h2>나머지 구하기</h2>
##### 문제<br>
정수 num1, num2가 매개변수로 주어질 때, num1를 num2로 나눈 나머지를 return 하도록 solution 함수를 완성해주세요.
0 < num1 ≤ 100
0 < num2 ≤ 100
```python
def solution(num1, num2):
    return num1 % num2
```
나머지를 구하는 연산자를 이용했다.

다른 사람의 풀이
```python
def solution(num1, num2):
    return divmod(num1, num2)[1]
```
divmod(x, y)는 두 숫자를 인자로 전달 받아 첫번째 인자를 두번째 인자로 나눈 몫과 나머지를 tuple 형식으로 반환하는 함수이다.

<h2>숫자 비교하기</h2>
##### 문제<br>
정수 num1과 num2가 매개변수로 주어집니다. 두 수가 같으면 1 다르면 -1을 retrun하도록 solution 함수를 완성해주세요.
0 ≤ num1 ≤ 10,000
0 ≤ num2 ≤ 10,000
```python
def solution(num1: int, num2: int)->int:
    return 1 if num1 == num2 else -1
```
one-line if else문을 이용했다.

<h2>각도기</h2>
##### 문제<br>
각에서 0도 초과 90도 미만은 예각, 90도는 직각, 90도 초과 180도 미만은 둔각 180도는 평각으로 분류합니다. 
각 angle이 매개변수로 주어질 때 예각일 때 1, 직각일 때 2, 둔각일 때 3, 평각일 때 4를 return하도록 solution 함수를 완성해주세요.
예각 : 0 < angle < 90
직각 : angle = 90
둔각 : 90 < angle < 180
평각 : angle = 180
0 < angle ≤ 180
angle은 정수입니다.
```python
def solution(angle):
    return 1 if angle > 0 and angle < 90 else 2 if angle == 90 else 3 if angle > 90 and angle < 180 else 4
```
one-line if else문을 이용해서 예각, 직각, 둔각, 평각의 범위를 나누었다.

다른 사람의 풀이
```python
def solution(angle):
    answer = (angle // 90) * 2 + (angle % 90 > 0) * 1
    return answer
```
각도를 90도로 나눈 몫에 2를 곱한 값과 각을 90도로 나눈 나머지가 있는지(1) 없는지(0)를 판별한 값을 더해주는 식으로 풀었다.
예를 들어 170도라고 하면 2 + 1 로 둔각인 3이 나올 수 있게 된다.
(angle % 90 > 0) 를 통해 1, 0 값을 활용한 것이 참신했다.