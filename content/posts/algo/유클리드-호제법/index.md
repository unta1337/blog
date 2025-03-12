---
title: "유클리드 호제법"
date: 2024-07-23T22:16:00+09:00
draft: false
summary: "유클리드 호제법과 시간복잡도"
toc: true 
katex: true
---
## 개요
유클리드 호제법은 두 수 $a$와 $b$에 대한 최대공약수를 빠르게 구하는 알고리즘이다.  

일반적으로는 아래와 같이 쓸 수 있다.  
$$
gcd(a, b) = gcd(b, a\ mod\ b)
$$

보통은 $a$와 $b$의 관계를 몫과 나머지에 대해서 나타내어 귀류법으로 증명한다.  
그러나 여기서는 $a$와 $b$ 그리고 $a\ mod\ b$에 대한 공약수가 동일함을 보여 증명한다.  

## 증명
### 공약수의 성질
시작하기에 앞서 공약수에 대한 간단한 성질을 짚고 넘어가자.
$$
\begin{align*}
&d(a, b)를\ a와\ b의\ 공약수라고\ 하자. \newline
&그러면\ d(a, b) = d(b, a)이다.\ ...\ (a)
\end{align*}
$$

이는 어떤 수 $a$와 $b$의 공약수는 $b$와 $a$의 공약수와 같다는 의미로 공약수 집합에 대해 일종의 교환법칙이 성립함을 보여준다.  

### 공약수가 동일함을 보이기
우리가 보여야 할 것은 $gcd(a, b) = gcd(b, a\ mod\ b)$이다.  
이를 위해 $a$, $b$의 공약수와 $b$, $a\ mod\ b$의 공약수가 동일함을 보일 것이다.  

먼저 $c$를 아래와 같이 정의하자.  
$$
c = a\ mod\ b
$$

이렇게 하면 $c$에 대해 $b | a - c$, 즉 $b$가 $a - c$를 나누어 떨어지게 할 수 있다.  
따라서 $a - c$를 $b$에 대한 정수배로 표현할 수 있다.  
$$
a - c = by\ (단,\ y는\ 임의의\ 정수.)\ ...\ (b)
$$

$(b)$에서 $c = a - by$임을 유도할 수 있다.  
이때 어떤 수 $d$가 $a$와 $b$의 공약수라면 전체 식 $a - by$를 나눌 수 있음을 의미하므로 $a$와 $b$의 공약수는 $c$를 나누어 떨어지게 할 수 있다.  

이를 다시 정리하면 $a$와 $b$의 공약수는 $b$와 $c$의 공약수이기도 하다.  
$$
d \in d(a, b) \rightarrow d \in d(b, c)
$$

같은 방법으로 $(b)$에서 $a = c + by$임을 유도할 수 있다.  
이때 어떤 수 $d$가 $c$와 $b$의 공약수라면 전체 식 $c + by$를 나눌 수 있음을 의미하므로 $c$와 $b$의 공약수는 $a$를 나누어 떨어지게 할 수 있다.  

이를 다시 정리하면 $c$와 $b$의 공약수는 $b$와 $a$의 공약수이기도 하다.  
$$
d \in d(c, b) \rightarrow d \in d(b, a)
$$

이때 $(a)$를 이용해 $d(a, b)$등의 순서를 적절히 바꿔주면,
$$
\begin{align*}
d \in d(a, b) \rightarrow d \in d(b, c) \newline
d \in d(b, c) \rightarrow d \in d(a, b) \newline
\end{align*}
$$

이를 종합하면,
$$
d \in d(a, b) \leftrightarrow d \in d(b, c)
$$
즉, $a$와 $b$의 공약수는 $b$와 $c$의 공약수와 같다.  

### $gcd(a, b) = gcd(b, a\ mod\ b)$
$a$와 $b$의 공약수와 $b$와 $c$의 공약수가 같으므로 공약수 중 가장 큰 수인 최대공약수 또한 동일하다.  

따라서,
$$
gcd(a, b) = gcd(b, c)
$$

$c = a\ mod\ b$이므로,  
$$
gcd(a, b) = gcd(b, a\ mod\ b)
$$

## 시간복잡도
수식의 형태에서 볼 수 있듯이 유클리드 호제법은 $a$와 $b$를 $b$와 $a\ mod\ c$로 줄이며 진행된다.  
이때 $a\ mod\ c$가 $0$이 될 때까지 반복하므로 부등식을 세워 시간복잡도를 계산할 수 있다.  

일반화를 위해 $a \ge b$라고 두자.  
$a$와 $b$의 관계를 $a = bq + r$로 표현하면 아래와 같은 부등식을 유도할 수 있다.  
$$
\begin{align*}
&1 \le q \newline
\rightarrow\ &2 \le q + 1 \newline
\rightarrow\ &2r \le rq + r \newline
\end{align*}
$$

이때 $r \le b$에서 $rq + r \le bq + r$이다.  
그러므로,  
$$
\begin{align*}
2r \le bq + r
\end{align*}
$$

이상을 통해 $r$은 적어도 $a$의 절반임을 할 수 있다.  
즉, 그 수가 매 반복마다 적어도 반으로 줄어들므로 구하고자 하는 시간복잡도는,  
$$
O(log(a))
$$

그런데 실제 입력에서는 $a \ge b$임이 보장되지 않으므로,
$$
O(log(max(a, b)))
$$

한편 위에서 구한 시간복잡도는 보다 엄밀한 복잡도는 아니며 다만 상한으로서 설정하기에 적절하다.  
따라서 정확한 시간복잡도가 $O(log(max(a, b)))$라고 생각하기보단 로그의 시간복잡도를 갖는다고 기억하면 된다.  

## 구현
`a`와 `b`에 대한 최대공약수를 구하기 위해 `b`와 `a % b`의 최대공약수를 구하므로 재귀를 이용해 구현할 수 있다.  

```python
def get_gcd(a, b):
    if b == 0:
        return a

    return get_gcd(b, a % b)
```

`b`가 `0`이 되면 더 이상 나머지를 구할 수 없으므로 재귀 호출을 종료한다.  

이때 각 단계별로 `a`와 `b`를 출력해보면 각 단계에서 두 수의 공약수가 항상 같음을 볼 수 있다.  

## 외부 링크
[The Euclidean Algorithm | Whitman College](https://www.whitman.edu/mathematics/higher_math_online/section03.03.html)  
[유클리드 호제법 시간복잡도 증명 | Dandalf's Life Log](https://dandalf.tistory.com/123)  
