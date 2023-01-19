---
date: 2023-01-19 12:16:13
layout: post
title: 알고리즘 프로그래머스 Lv.0 풀이 (2)
subtitle: algorithm python
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

<h2>짝수의 합</h2>
##### 문제<br>
정수 n이 주어질 때, n이하의 짝수를 모두 더한 값을 return 하도록 solution 함수를 작성해주세요.
0 < n ≤ 1000
```python
def solution(n):
    answer = 0
    for i in range(0, n+1, 2):
        answer += i
    return answer
```
0부터 정수 n까지 step 2 만큼 증가하는 배열을 만들어 모두 더하는 식으로 풀이했다.
합이므로 0이 아닌 2부터 시작해도 될 것 같다.

다른 사람의 풀이
```python
def solution(n):
    return sum([i for i in range(2, n + 1, 2)])
```
비슷한 원리이지만 sum 함수를 통해 간결하게 작성하였다.

<h2>배열의 평균값</h2>
##### 문제<br>
정수 배열 numbers가 매개변수로 주어집니다. numbers의 원소의 평균값을 return하도록 solution 함수를 완성해주세요.
0 ≤ numbers의 원소 ≤ 1,000
1 ≤ numbers의 길이 ≤ 100
정답의 소수 부분이 .0 또는 .5인 경우만 입력으로 주어집니다.
```python
def solution(numbers):
    answer = 0
    for number in numbers:
        answer += number
    return answer/len(numbers)
```
정수 배열의 값을 모두 더한 뒤 개수로 나누어 평균값을 구했다.

다른 사람의 풀이
```python
import numpy as np
def solution(numbers):
    return np.mean(numbers)
```
numpy라는 라이브러리를 사용해서 풀이했다.<br/>
*Numpy: 선형대수 라이브러리*

<h2>양꼬치</h2>
##### 문제<br>
머쓱이네 양꼬치 가게는 10인분을 먹으면 음료수 하나를 서비스로 줍니다. 양꼬치는 1인분에 12,000원, 음료수는 2,000원입니다. 정수 n과 k가 매개변수로 주어졌을 때, 양꼬치 n인분과 음료수 k개를 먹었다면 총얼마를 지불해야 하는지 return 하도록 solution 함수를 완성해보세요.
0 < n < 1,000
n / 10 ≤ k < 1,000
서비스로 받은 음료수는 모두 마십니다.
```python
def solution(n, k):
    return 12000*n+2000*k if n<10 else 12000*n+2000*(k-(n//10))
```
10인분 미만으로 시켜 서비스가 없을 때와 서비스가 생겼을 때를 나누어 풀이했다.

다른 사람의 풀이
```python
def solution(n, k):
    return 12000 * n + 2000 * (k - n // 10)
```
다른 사람의 풀이를 보니 굳이 나눌 필요없이 10인분 당 서비스 음료수 1개를 빼서 계산하면 됐다..<br/>


<h2>머쓱이보다 키 큰 사람</h2>
##### 문제<br>
머쓱이는 학교에서 키 순으로 줄을 설 때 몇 번째로 서야 하는지 궁금해졌습니다. 머쓱이네 반 친구들의 키가 담긴 정수 배열 array와 머쓱이의 키 height가 매개변수로 주어질 때, 머쓱이보다 키 큰 사람 수를 return 하도록 solution 함수를 완성해보세요.
1 ≤ array의 길이 ≤ 100
1 ≤ height ≤ 200
1 ≤ array의 원소 ≤ 200
```python
def solution(array, height):
    answer = 0
    for i in array:
        if i > height:
            answer += 1
    return answer
```
머쓱이의 키와 배열 내 값을 비교해서 큰 사람 수를 구했다.

다른 사람의 풀이
```python
def solution(array, height):
    return sum(1 for a in array if a > height)
```
같은 방식으로 sum함수를 사용해 간결하게 풀이했다.

<h2>머쓱이보다 키 큰 사람</h2>
##### 문제<br>
정수가 들어 있는 배열 num_list가 매개변수로 주어집니다. num_list의 원소의 순서를 거꾸로 뒤집은 배열을 return하도록 solution 함수를 완성해주세요.
1 ≤ num_list의 길이 ≤ 1,000
0 ≤ num_list의 원소 ≤ 1,000
```python
def solution(num_list):
    answer = []
    for num in num_list:
        answer.insert(0, num)
    return answer
```
num_list를 꺼내 insert()를 통해 배열의 0번째에 넣었다.

다른 사람의 풀이
```python
def solution(num_list):
    return num_list[::-1]
```
array[::] extended slices를 활용하여 간단하게 뒤집었다.<br/>

> arr = range(10) # [0,1,2,3,4,5,6,7,8,9] <br/>
> arr[::2] # 처음 ~ 끝 두 칸 간격 [0,2,4,6,8] <br/>
> arr[1::2] # index 1 ~ 끝까지 두 칸 간격 [1,3,5,7,9] <br/>
> arr[::-1] # 처음 ~ 끝 -1칸 간격(=역순) [9,8,7,6,5,4,3,2,1,0] <br/>
> arr[::-2] # 처음 ~ 끝까-2칸 간격(=역순, 두 칸 간격) [9,7,5,3,1] <br/>
> arr[3::-1] # index 3 ~ 끝까지 -1칸 간격(=역순) [3,2,1,0] <br/>
> arr[1:6:2] # index 1 ~ index 6 까지 두 칸 간격 [1,3,5] <br/>

앞으로 배열에 대한 여러가지 활용을 잘 익혀둬야겠다는 생각이 들었다.<br/>