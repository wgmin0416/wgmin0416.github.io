---
date: 2023-01-25 00:33:09
layout: post
title: 알고리즘 문제 풀기(4)
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
<h2>배열 자르기</h2>
##### 문제<br>
정수 배열 numbers와 정수 num1, num2가 매개변수로 주어질 때, numbers의 num1번 째 인덱스부터 num2번째 인덱스까지 자른 정수 배열을 return 하도록 solution 함수를 완성해보세요.
2 ≤ numbers의 길이 ≤ 30
0 ≤ numbers의 원소 ≤ 1,000
0 ≤num1 < num2 < numbers의 길이
```python
def solution(numbers, num1, num2):
    return numbers[num1:num2+1]
```
지난 알고리즘 풀이를 통해 학습한 array[::] extended slices를 활용하였다.

> arr = range(10) # [0,1,2,3,4,5,6,7,8,9] <br/>
> arr[::2] # 처음 ~ 끝 두 칸 간격 [0,2,4,6,8] <br/>
> arr[1::2] # index 1 ~ 끝까지 두 칸 간격 [1,3,5,7,9] <br/>
> arr[::-1] # 처음 ~ 끝 -1칸 간격(=역순) [9,8,7,6,5,4,3,2,1,0] <br/>
> arr[::-2] # 처음 ~ 끝 -2칸 간격(=역순, 두 칸 간격) [9,7,5,3,1] <br/>
> arr[3::-1] # index 3 ~ 끝까지 -1칸 간격(=역순) [3,2,1,0] <br/>
> arr[1:6:2] # index 1 ~ index 6 까지 두 칸 간격 [1,3,5] <br/>

<h2>배열 자르기</h2>
##### 문제<br>
정수 배열 numbers와 정수 num1, num2가 매개변수로 주어질 때, numbers의 num1번 째 인덱스부터 num2번째 인덱스까지 자른 정수 배열을 return 하도록 solution 함수를 완성해보세요.
2 ≤ numbers의 길이 ≤ 30
0 ≤ numbers의 원소 ≤ 1,000
0 ≤num1 < num2 < numbers의 길이
```python
def solution(numbers, num1, num2):
    return numbers[num1:num2+1]
```
지난 알고리즘 풀이를 통해 학습한 array[::] extended slices를 활용하였다.

> arr = range(10) # [0,1,2,3,4,5,6,7,8,9] <br/>
> arr[::2] # 처음 ~ 끝 두 칸 간격 [0,2,4,6,8] <br/>
> arr[1::2] # index 1 ~ 끝까지 두 칸 간격 [1,3,5,7,9] <br/>
> arr[::-1] # 처음 ~ 끝 -1칸 간격(=역순) [9,8,7,6,5,4,3,2,1,0] <br/>
> arr[::-2] # 처음 ~ 끝 -2칸 간격(=역순, 두 칸 간격) [9,7,5,3,1] <br/>
> arr[3::-1] # index 3 ~ 끝까지 -1칸 간격(=역순) [3,2,1,0] <br/>
> arr[1:6:2] # index 1 ~ index 6 까지 두 칸 간격 [1,3,5] <br/>

다른 사람의 풀이
```python
def solution(num_list):
    answer = [0,0]
    for n in num_list:
        answer[n%2]+=1
    return answer
```
같은 방식이지만 몫이 0과 1이므로 배열의 index로 잘 활용했다.

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