
# [[BOJ]1339](https://www.acmicpc.net/problem/1339)

## 풀이
2
GCF
ACDEB
에서
A = 10000 * 9
C = 1010 * 8
D = 100 * 7
G = 100 * 6
E = 10 * 5
F = 1 * 4
B = 1 * 3
ACDEB + GCF는 99437이 된다.
 
## 전체 코드
```C++
#include <iostream>
#include <string>
#include <algorithm>

using namespace std;
int graph[26];

//내림차순
bool cmp(int &a, int &b) {
	return a > b;
}
int main() {
	ios::sync_with_stdio(false);
	cin.tie(0);
	cout.tie(0);
	
	int n;
	cin >> n;
	for (int i = 0; i < n; i++) {
		string input;
		cin >> input;
		int pow = 1;
		for (int j = input.length()-1; j >= 0; j--) {
			graph[input[j]-'A'] += pow;
			pow *= 10;
		}
	}

	sort(graph, graph+26,cmp);

	int num = 9;
	int answer = 0;
	for (int i = 0; i < 26;i++) {
		if (graph[i] == 0) 
			break;
		answer += graph[i] * num--;
	}
	cout << answer << '\n';

	
	return 0;
}
```



# [[BOJ]17836][https://www.acmicpc.net/problem/17836))

## 풀이

코드 첨부

## 전체 코드
```C++
#include<iostream>
#include<queue>
#include<cstring>
using namespace std;
int n, m, t;
// 성의 정보
int castle[100][100];
// cache[y][x][검을 가졌는지] = 검을 갖고(or갖지 않고) (y,x)를 처음 방문했을때 시간
int cache[100][100][2];
// 한 칸씩 이동
int dy[4] = { 0,0,1,-1 };
int dx[4] = { 1,-1,0,0 };
// queue에 담을 구조체
struct Data {
	int x, y;
	int time;
	bool hasGram;
};
int rescue() {
	// 처음엔 0초
	cache[0][0][false] = 0;
	// bfs를 위한 queue
	queue<Data> q;
	// 용사의 처음 상태 push
	q.push({ 0,0,0,false });
	while (!q.empty()) {
		// 현재 상태 저장
		int curY = q.front().y; int curX = q.front().x;
		int curTime = q.front().time; bool curHas = q.front().hasGram;
		q.pop();
		// 각각 4가지 방향으로 이동할 경우
		for (int i = 0; i < 4; i++) {
			// 다음 상태 계산
			int nextY = curY + dy[i]; 
			int nextX = curX + dx[i];
			int nextTime = curTime + 1;
			// 현재 검을 갖고 있거나 검이 있는 칸을 가거나
			bool nextHas = (curHas || castle[nextY][nextX] == 2);
			// 공주를 구할 수 있으면 해당 시간을 return
			if (nextY == n && nextX == m)return nextTime;
			// castle을 안벗어나고
			if ((nextY >= 0 && nextY <= n && nextX >= 0 && nextX <= m)) 
				// 검을 갖고 있거나 벽에 안부딪히게
				if (curHas || castle[nextY][nextX] != 1) {
					// 이미 지나온 길은 되돌아갈 필요없음
					if (cache[nextY][nextX][nextHas] == -1) {
						q.push({ nextX, nextY, nextTime, nextHas });
						cache[nextY][nextX][nextHas] = nextTime;
					}
				}
		}
	}
	// 공주를 못구하는 경우
	return -1;
}
int main() {
	cin >> n >> m >> t;
	for (int i = 0; i < n; i++)
		for (int j = 0; j < m; j++)
			cin >> castle[i][j];
	n--; m--;
	memset(cache, -1, sizeof(cache));
	int result = rescue();
	// 공주를 제한시간내에 못구하는 경우
	if (result == -1 || result > t)
		cout << "Fail" << endl;
	else
		cout << result << endl;
}

```
