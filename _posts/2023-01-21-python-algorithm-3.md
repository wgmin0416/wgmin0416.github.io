---
date: 2023-01-21 01:46:52
layout: post
title: 알고리즘 문제 풀기(3)
subtitle: algorithm python
description: 프로그래머스 Lv.0
image: /assets/img/posts/algorithm.jpg
optimized_image: /assets/img/posts/algorithm.jpg
category: algorithm
tags:
  - python
  - algorithm
author: wgmin0416
---
<h2>아이스 아메리카노</h2>
##### 문제<br>
머쓱이는 추운 날에도 아이스 아메리카노만 마십니다. 아이스 아메리카노는 한잔에 5,500원입니다. 
머쓱이가 가지고 있는 돈 money가 매개변수로 주어질 때, 머쓱이가 최대로 마실 수 있는 아메리카노의 잔 수와 
남는 돈을 순서대로 담은 배열을 return 하도록 solution 함수를 완성해보세요.
0 < money ≤ 1,000,000
```python
def solution(money):
    return [money//5500, money%5500]
```
몫과 나머지를 통해 구했다.

다른 사람의 풀이
```python
def solution(money):
    return divmod(money, 5500)
```
divmod함수는 몫과 나머지를 배열로 return한다.

<h2>피자 나눠 먹기(1)</h2>
##### 문제<br>
머쓱이네 피자가게는 피자를 일곱 조각으로 잘라 줍니다. 피자를 나눠먹을 사람의 수 n이 주어질 때,
모든 사람이 피자를 한 조각 이상 먹기 위해 필요한 피자의 수를 return 하는 solution 함수를 완성해보세요.
1 ≤ n ≤ 100
```python
def solution(n):
    if n%7 == 0:
        answer = n//7
    else:
        answer = n//7 + 1
    return answer
```

다른 사람의 풀이
```python
def solution(n):
    return (n - 1) // 7 + 1
```
인원수 n에서 1을 뺀 값이 7을 넘지 않을 때는 1, 7이 넘을 때 몫 만큼 추가하는 계산으로 풀었다.
if 분기처리가 아닌 몫을 이용해 수학적으로 접근하는 방법도 생각해봐야겠다.

<h2>문자열 뒤집기</h2>
##### 문제<br>
문자열 my_string이 매개변수로 주어집니다. my_string을 거꾸로 뒤집은 문자열을 return하도록 solution 함수를 완성해주세요.
1 ≤ my_string의 길이 ≤ 1,000
```python
def solution(my_string):
    return my_string[::-1]
```
지난 알고리즘 풀이를 통해 학습한 array[::] extended slices를 활용하였다.

> arr = range(10) # [0,1,2,3,4,5,6,7,8,9] <br/>
> arr[::2] # 처음 ~ 끝 두 칸 간격 [0,2,4,6,8] <br/>
> arr[1::2] # index 1 ~ 끝까지 두 칸 간격 [1,3,5,7,9] <br/>
> arr[::-1] # 처음 ~ 끝 -1칸 간격(=역순) [9,8,7,6,5,4,3,2,1,0] <br/>
> arr[::-2] # 처음 ~ 끝 -2칸 간격(=역순, 두 칸 간격) [9,7,5,3,1] <br/>
> arr[3::-1] # index 3 ~ 끝까지 -1칸 간격(=역순) [3,2,1,0] <br/>
> arr[1:6:2] # index 1 ~ index 6 까지 두 칸 간격 [1,3,5] <br/>

<h2>점의 위치 구하기</h2>
##### 문제<br>
사분면은 한 평면을 x축과 y축을 기준으로 나눈 네 부분입니다. 사분면은 아래와 같이 1부터 4까지 번호를매깁니다.
x 좌표와 y 좌표가 모두 양수이면 제1사분면에 속합니다.
x 좌표가 음수, y 좌표가 양수이면 제2사분면에 속합니다.
x 좌표와 y 좌표가 모두 음수이면 제3사분면에 속합니다.
x 좌표가 양수, y 좌표가 음수이면 제4사분면에 속합니다.
x 좌표 (x, y)를 차례대로 담은 정수 배열 dot이 매개변수로 주어집니다.
좌표 dot이 사분면 중 어디에 속하는지 1, 2, 3, 4 중 하나를 return 하도록 solution 함수를 완성해주세요.
dot의 길이 = 2
dot[0]은 x좌표를, dot[1]은 y좌표를 나타냅니다
-500 ≤ dot의 원소 ≤ 500
dot의 원소는 0이 아닙니다.
```python
def solution(dot):
    answer = 0
    if dot[0]*dot[1] > 0:
        answer = 1 if dot[0]+dot[1] > 0 else 3
    else:
        answer = 2 if dot[0] < 0 else 4
    return answer
```
x좌표와 y좌표 곱으로 양,음수를 판단하고 곱이 양수일 경우(1,3사분면) 합의 양,음수를 판단하여 분기처리했다. 

다른 사람의 풀이
```python
def solution(dot):
    a, b = 1, 0
    if dot[0]*dot[1] > 0:
        b = 1
    if dot[1] < 0:
        a = 2
    return 2*a-b
```
x좌표와 y좌표 곱이 양수(1,3사분면)일 경우와 y좌표가 음수일 경우에 값을 설정하여 계산했다.