---
title: LV.3 정수 삼각형 (동적계획법(Dynamic Programming))
date: 2026-11-10 00:41:00 +0900
categories: [Coding, Programmers]
tags: [DP, Dynamic-Programming]
---

# 문제
```text
            [7]
         [3]   [8]
      [8]   [1]   [0]
   [2]   [7]   [4]   [4]
[4]   [5]   [2]   [6]   [5]
```
위와 같은 삼각형의 꼭대기에서 바닥까지 이어지는 경로 중, 거쳐간 숫자의 합이 가장 큰 경우를 찾아보려고 합니다. 아래 칸으로 이동할 때는 대각선 방향으로 한 칸 오른쪽 또는 왼쪽으로만 이동 가능합니다. 예를 들어 3에서는 그 아래칸의 8 또는 1로만 이동이 가능합니다.

삼각형의 정보가 담긴 배열 triangle이 매개변수로 주어질 때, 거쳐간 숫자의 최댓값을 return 하도록 solution 함수를 완성하세요.

> ### 제한사항
> 삼각형의 높이는 1 이상 500 이하입니다.
> 삼각형을 이루고 있는 숫자는 0 이상 9,999 이하의 정수입니다.

[프로그래머스 문제 페이지](https://school.programmers.co.kr/learn/courses/30/lessons/43105)

<br>

# code
```cpp
#include <string>
#include <vector>

using namespace std;

int solution(vector<vector<int>> triangle) {
    int answer = 0;
    
    for (int i = triangle.size() - 2; i >= 0; i--){ //n-1번째 ~ 1번째
        for (int j = 0; j < triangle[i].size(); j++){ //줄 순회
            triangle[i][j] += ((triangle[i + 1][j] > triangle[i + 1][j+1]) ? (triangle[i + 1][j]) : (triangle[i + 1][j+1])); //밑 줄에서 더 큰 정수 더하기
        }
    }
    
    answer = triangle[0][0];
    
    return answer;
}
```
<br>

# 해설
1. n개의 줄이 존재할 때 n-1번째(마지막에서 두 번째 줄)에서 n번째(마지막) 줄의 정수를 선택할 때의 선택지는 두 가지이다.
   <br>이때, 둘 중 무조건 큰 수를 고르는 것이 조건을 만족한다.
2. 그러므로 n-1번째 줄이 가지는 선택지들 중 더 큰 쪽을 선택해 해당 정수에 더하면 n-1번째 줄이 마지막 줄이 된다.
3. 이를 첫 번째 줄까지 반복하면 가장 큰 합의 경우만 남게된다.

<br>

**전체 문제를 n-1, n번째 사이의 문제로 나누어 아래에서 위로 해결하는 bottom-up 동적 계획법 풀이입니다.**
