
# [[BOJ]11966](https://www.acmicpc.net/problem/11966)

## 풀이
1 ≤ N ≤ 2^30 이므로 2^30보다 작은 2의 제곱수 squareNum을 생성하여 일치하면 1, 일치하는 것이 없으면 0 return.

 
## 전체 코드
```C++
#include <iostream>
using namespace std;
 
int main() {
    int N;
    cin >> N;
 
    if (N == 1) {
        cout << 1 << endl;
        return 0;
    }
 
    int squareNum = 1;
    for (int i = 0; i < 30; i++) {
        squareNum *= 2;
        
        if (N == squareNum) {
            cout << 1 << endl;
            return 0;
        }
    }
 
    cout << 0 << endl;
 
    return 0;
}
```



# [[BOJ]2667][https://www.acmicpc.net/problem/11404](https://www.acmicpc.net/problem/2667))

## 풀이

그림 1>과 같이 정사각형 모양의 지도가 있다. 1은 집이 있는 곳을, 0은 집이 없는 곳을 나타낸다. 철수는 이 지도를 가지고 연결된 집의 모임인 단지를 정의하고, 단지에 번호를 붙이려 한다. 여기서 연결되었다는 것은 어떤 집이 좌우, 혹은 아래위로 다른 집이 있는 경우를 말한다. 대각선상에 집이 있는 경우는 연결된 것이 아니다. <그림 2>는 <그림 1>을 단지별로 번호를 붙인 것이다. 지도를 입력하여 단지수를 출력하고, 각 단지에 속하는 집의 수를 오름차순으로 정렬하여 출력하는 프로그램을 작성하시오.

단지를 먼저 찾고 그다음에 dfs 알고리즘 이용해서 해결
## 전체 코드
```C++
#include <stdio.h>
#include<vector>
#include<queue>
#include<algorithm>

int graph[26][26] = {0};
int apart[26*26] = {0};
int n, count, sum = 0;
int dx[4] = {-1, 1, 0, 0};
int dy[4] = {0, 0, -1, 1};

int dfs(int x, int y){
    if(x < 0 || y < 0 || x >= n || y >= n) {
        return 0;
    }
    
    if(graph[x][y] == 1) {
        graph[x][y] = 0;
        count++;
        
        for(int i = 0; i < 4; i++) {
            dfs(x + dx[i], y + dy[i]);
        }
        return 1;
        
    }
    return 0;
    
}

int main()
{
    scanf("%d", &n);
    for(int i = 0; i < n; i++){
        for(int j = 0; j < n; j++){
            scanf("%1d", graph[i] + j);
        }
    }
    
    for(int i = 0; i < n; i++) {
        for(int j = 0; j < n; j++) {
            if(dfs(i, j) == 1) {
                apart[count]++;
                count = 0;
                sum++;
            }
        }
    }
    
    printf("%d\n", sum);
    for(int i = 0; i < 26*26; i++) {
        if(apart[i] != 0){
            int k = apart[i];
            for(int j = 0; j < k; j++) {
                printf("%d\n", i);
            }
        }
    }
    
    return 0;
}

```
