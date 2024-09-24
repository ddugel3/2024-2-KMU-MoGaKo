# [[BOJ]11047](https://www.acmicpc.net/problem/11047)

## 풀이
첫째 줄에 N과 K가 주어진다. (1 ≤ N ≤ 10, 1 ≤ K ≤ 100,000,000)
둘째 줄부터 N개의 줄에 동전의 가치 Ai가 오름차순으로 주어진다. (1 ≤ Ai ≤ 1,000,000, A1 = 1, i ≥ 2인 경우에 Ai는 Ai-1의 배수)

목표 금액  k  이상인 동전을 반복해서 빼며, 해당 동전이 사용될 때마다 카운트를 증가시키고, 금액이 모자라면 더 작은 동전을 선택해 계속해서 금액을 맞춰나간다.

## 전체 코드
```C
#include<stdio.h>

int main()
{
    int n,k,arr[12];    scanf("%d %d",&n,&k);
    for(int i=0;i<n;i++)    scanf("%d",&arr[i]);
    int sum=k,m=n-1,cnt=0;
    while(sum>0){
        if(sum>=arr[m]){
            sum-=arr[m];
            cnt++;
        }
        else    m--;
    }
    printf("%d",cnt);
}

```

# [[BOJ]11401](https://www.acmicpc.net/problem/11401)

## 풀이

첫째 줄에 N과 K가 주어진다.

이항계수를 1,000,000,007로 나눈 나머지를 구하는 프로그램을 작성해야 한다 .

모듈로 연산을 통해서 문제를 해결할 수 있다.

## 전체 코드
```C
#include <iostream>
#define DIV		1000000007
using namespace std;

long long temp;

long long power(long long a, long long m) {
	if (m == 0) return 1;

	temp = power(a, m / 2) % DIV;
	if (m % 2 == 1) return temp * temp % DIV * a % DIV;
	return temp * temp % DIV;
}

void solve(int n, int k) {
	if (k == 1) { cout << n; return; }
	if (k == 0 || n == k) { cout << 1; return; }
	if (n - k == 1) { cout << n; return; }

	long long A = 1, B = 1, ans;
	for (int i = n; i >= n - k + 1; i--) A = (A * i) % DIV;
	for (int i = 1; i <= k; i++) B = (B * i) % DIV;
	ans = ((A % DIV) * power(B, DIV - 2) % DIV) % DIV;
	cout << ans;
}

int main(void) {
	int n, k;

	cin >> n >> k;
	solve(n, k);

	return 0;
}
```
