
# [[BOJ]9905](https://www.acmicpc.net/problem/11047)

## 풀이
​정수 4를 1, 2, 3의 합으로 나타내는 방법은 총 7가지가 있다. 합을 나타낼 때는 수를 1개 이상 사용해야 한다.
1+1+1+1
1+1+2
1+2+1
2+1+1
2+2
1+3
3+1

정수 n이 주어졌을 때, n을 1, 2, 3의 합으로 나타내는 방법의 수를 구하는 프로그램을 작성하시오.


dp[n] = dp[n-3] + dp[n-2] + dp[n-1] 이라는 점화식을 만들어 냅니다


## 전체 코드
```C

#include <stdio.h>
int dp[11];
int main(void) {
	int T;
	scanf("%d", &T);
	
	int i, j;
	int n;
	dp[0] = 1;
	dp[1] = 2;
	dp[2] = 4;
	
	for(i = 0; i < T; i++){
		scanf("%d", &n);
		for(j = 3; j < n; j++){
			dp[j] = dp[j-3] + dp[j-2] + dp[j-1];
		}
		printf("%d\n", dp[n-1]);
	}
	
	return 0;
}
```
