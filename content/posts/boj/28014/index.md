---
title: "28014 첨탑 밀어서 부수기"
date: 2024-04-28T17:46:00+09:00
draft: false
summary: "28014 첨탑 밀어서 부수기"
toc: true 
katex: true
---
## 접근 방법
신지니는 반드시 앞으로만 움직이므로 가능한 선택지는 현재 첨탑을 미는 경우와 밀지 않는 경우 두 개밖에 없다.  
이때 첨탑을 밀지 않는 경우는 앞선 첨탑에 의해 이미 첨탑이 넘어진 경우로 어떤 첨탑을 밀지만 정하면 된다.  

현재 첨탑의 높이가 다음 첨탑보다 높으면 다음 첨탑도 밀려나므로 이를 반대로 생각해보자.  

현재 첨탑은 이전 첨탑의 높이보다 낮아야 밀려난다.  
 현재 첨탑이 이전 첨탑보다 높거나 같은 경우에 그 첨탑을 밀어주면 된다.  

## 구현
```c
#include <stdio.h>

int main(void) {
    size_t n = 0;
    scanf("%zu", &n);

    size_t prev = 0;
    size_t answer = 0;

    for (size_t i = 0; i < n; i++) {
        size_t curr = 0;
        scanf("%zu", &curr);

        if (curr >= prev) {
            answer++;
        }

        prev = curr;
    }

    printf("%zu\n", answer);

    return 0;
}
```

주어진 첨탐을 입력받으며 이전 첨탑보다 높이가 높거나 같은 경우에 첨탐을 밀어주어 `answer`를 1씩 증가시켰다.  

이때 `prev`는 이전 첨탑의 높이를 유지하는 변수로 첫 첨탑은 항상 밀어야 하므로 가능한 최소 높이인 1보다 작은 0을 초깃값으로 두었다.  

## 외부 링크
[28014 첨탑 밀어서 부수기 | BOJ](https://www.acmicpc.net/problem/28014)  
[채점 결과 | BOJ](https://www.acmicpc.net/source/share/9f4d0f0b693c4085b4324cb0b3569904)  
