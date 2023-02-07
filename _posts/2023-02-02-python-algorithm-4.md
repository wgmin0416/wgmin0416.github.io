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
  - algorithm
author: wgmin0416
---
<h2>배열 자르기</h2>
##### 문제<br>
정수 배열 numbers와 정수 num1, num2가 매개변수로 주어질 때, 
numbers의 num1번 째 인덱스부터 num2번째 인덱스까지 자른 정수 배열을 return 하도록 solution 함수를 완성해보세요.<br/>
2 ≤ numbers의 길이 ≤ 30<br/>
0 ≤ numbers의 원소 ≤ 1,000<br/>
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

<h2>짝수는 싫어요</h2>
##### 문제<br>
정수 n이 매개변수로 주어질 때, n 이하의 홀수가 오름차순으로 담긴 배열을 return하도록 solution 함수를 완성해주세요.<br/>
1 ≤ n ≤ 100
```python
def solution(n):
    return list(range(1, n+1, 2))
```
range함수를 통해 1부터 2씩 n까지 증가하는 숫자 객체를 만들어 리스트에 담았다.

다른 사람의 풀이
```python
def solution(n):
    return [i for i in range(1, n+1, 2)]
```
같은 방식으로 배열에 담았다. array와 list는 다르므로 정확하게는 배열에 담는 것이 맞을 것 같다.

> Array와 List <br/>
* 공통점 : 아이템들의 컬렉션, 순서 존재<br/>
* 차이점 : <br/>
&nbsp;&nbsp;&nbsp;&nbsp;- Array : 인덱스 존재, 위치에 직접 접근 가능, 할당된 공간이 연속적(조회가 빠름), 미리 배열의 크기를 지정(추가 삭제가 불편)  
&nbsp;&nbsp;&nbsp;&nbsp;- List : 인덱스를 갖지만 몇 번째인지만 의미, 메모리 주소가 연속적이지 않을 수 있음, 동적이므로 크기가 정해져 있지 않음, 검색 성능이 안 좋음

<h2>최댓값 만들기(1)</h2>
##### 문제<br>
정수 배열 numbers가 매개변수로 주어집니다. numbers의 원소 중 두 개를 곱해 만들 수 있는 최댓값을 return하도록 solution 함수를 완성해주세요.    
0 ≤ numbers의 원소 ≤ 10,000  
2 ≤ numbers의 길이 ≤ 100
```python
def solution(numbers):
    max_number = max(numbers)
    del numbers[numbers.index(max(numbers))]
    max_number2 = max(numbers)
    return max_number * max_number2
```
배열의 최댓값을 구하고 배열에서 제거한 뒤 다음 최댓값을 구해서 곱했다.

다른 사람의 풀이
```python
def solution(numbers):
    numbers.sort()
    return numbers[-2] * numbers[-1]
```
정렬하여 가장 큰 값과 다음 큰 값을 곱했다.

<h2>피자 나눠 먹기 (3)</h2>
##### 문제<br>
머쓱이네 피자가게는 피자를 두 조각에서 열 조각까지 원하는 조각 수로 잘라줍니다. 피자 조각 수 slice와 피자를 먹는 사람의 수 n이 매개변수로 주어질 때, n명의 사람이 최소 한 조각 이상 피자를 먹으려면 최소 몇 판의 피자를 시켜야 하는지를 return 하도록 solution 함수를 완성해보세요.  
2 ≤ slice ≤ 10  
1 ≤ n ≤ 100
```python
def solution(slice, n):
    return (n // slice) + (1 if n % slice > 0 else 0)
```
전체 인원 수를 조각 수로 나눈 몫과 나머지가 있으면 1판을 추가 하는 방식으로 풀었다.

다른 사람의 풀이
```python
def solution(slice, n):
    return ((n - 1) // slice) + 1
```
전체 인원 수에서 1을 빼고 를 조각 수로 나눈 몫에 1을 더하는 방식이다. 
이전 피자 나눠먹기 문제에서도 봤던 풀이법인데 또 떠올리지 못했다.