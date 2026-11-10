---
title: LV.2 올바른 괄호 (스택/큐)
date: 2026-11-11 06:05:00 +0900
categories: [Coding, Programmers]
tags: [Stack, Queue]
---

# 문제 설명
괄호가 바르게 짝지어졌다는 것은 '(' 문자로 열렸으면 반드시 짝지어서 ')' 문자로 닫혀야 한다는 뜻입니다. 예를 들어

"()()" 또는 "(())()" 는 올바른 괄호입니다.
")()(" 또는 "(()(" 는 올바르지 않은 괄호입니다.
'(' 또는 ')' 로만 이루어진 문자열 s가 주어졌을 때, 문자열 s가 올바른 괄호이면 true를 return 하고, 올바르지 않은 괄호이면 false를 return 하는 solution 함수를 완성해 주세요.

> ### 제한사항
> 문자열 s의 길이 : 100,000 이하의 자연수
> 문자열 s는 '(' 또는 ')' 로만 이루어져 있습니다.
<br>

# code
```cpp
#include <string>
#include <iostream>
#include <list>

using namespace std;

bool solution(string s) {
    bool answer = true;

    list<char> l;
    for (int i = 0; i < s.length(); i++){
        if (l.empty()) { //스택이 비었을 때
            if (s[i] == ')') return false; //')'가 들어오면 잘못됨
            l.push_back(s[i]);
            continue;
        }
        
        if (l.back() != s[i]){ //괄호가 맞으면 ')' 하나씩 빼기
            l.pop_back();
        }
        else{
            if (s[i] == ')') return false;file://xn--')'%20%20-do27ao66cm6b693ar2az71jhqb20l/
            l.push_back(s[i]);
        }
    }
    
    answer = l.empty(); //전부 처리한 후 스택이 비어있으면 올바른 괄호
    
    return answer;
}
```
<br>

# 해설
기초적인 스택 관련 문제입니다.

1. '('가 입력되면 스택에 저장합니다.
2. ')'가 입력되면 스택의 '('를 하나 삭제합니다.<br>
(이때 삭제할 '('가 없다면 잘못된 괄호입니다.)
3. 모든 입력이 끝났을 때에 스택이 비어있다면 올바른 괄호입니다.

*여러 종류의 괄호에서도 똑같이 적용할 수 있음*

*본 풀이에서는 list 라이브러리를 사용해 스택을 구현했으나 stack 라이브러리를 사용하는 것이 적절할 수 있습니다.
