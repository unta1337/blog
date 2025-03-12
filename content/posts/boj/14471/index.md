---
title: "14471 포인트 카드"
date: 2024-05-01T15:19:00+09:00
draft: false
summary: "14471 포인트 카드"
toc: true 
katex: true
---
## 접근 방법
당첨 도장이 가장 많은 $m - 1$개의 카드를 이용해 경품과 교환하는 것이 가장 적은 당첨 도장을 구매하게 된다.  

따라서 카드를 당첨 도장에 대해 내림차순으로 정렬하여 첫 $m - 1$개의 카드에 대해 필요한 당첨 도장의 개수를 구해주면 된다.  

## 구현
```c
#include <stdio.h>
#include <stdlib.h>

typedef struct {
    size_t win;
    size_t lose;
} card_t;

int card_comp_desc(const void* p, const void* q) {
    size_t i = ((card_t*)p)->win;
    size_t j = ((card_t*)q)->win;

    return (i < j) - (i > j);
}

int main(void) {
    size_t n = 0;
    size_t m = 0;
    scanf("%zu %zu", &n, &m);

    card_t cards[1000] = { 0, };
    for (size_t i = 0; i < m; i++) {
        scanf("%zu %zu", &cards[i].win, &cards[i].lose);
    }

    qsort(cards, m, sizeof(*cards), card_comp_desc);

    size_t answer = 0;
    for (size_t i = 0; i < m - 1; i++) {
        if (cards[i].win >= n) {
            continue;
        } else {
            answer += n - cards[i].win;
        }
    }

    printf("%zu\n", answer);

    return 0;
}
```

`m`개의 카드를 입력받은 후 이를 `win`에 대해 내림차순 정렬한다.  
이때 `win`은 그 카드에 찍힌 당첨 도장의 개수이다.  

한편 모든 카드는 동일한 도장 개수를 가지므로 `win`이 같으면 반대로 꽝 도장 `lose`의 개수도 동일하다.  
즉, `win`이 같은 상황이어도 `lose`는 고려하지 않아도 된다.  

정렬한 `cards`의 첫 `m - 1`개를 순회하며 필요한 당첨 도장의 개수를 계산한다.  
당첨 도장의 개수가 이미 `n`개 이상으로 당첨 도장이 더 필요하지 않은 경우는 무시한다.  

## 외부 링크
[포인트 카드 | BOJ](https://www.acmicpc.net/problem/14471)  
[채점 결과 | BOJ](https://www.acmicpc.net/source/share/cd83a28d6e394b63ab2f92949bb79a48)  
