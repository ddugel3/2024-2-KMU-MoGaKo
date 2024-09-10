# [[BOJ]1068](https://www.acmicpc.net/problem/1068)

## 풀이
첫째 줄에 트리의 노드의 개수 N이 주어진다. N은 50보다 작거나 같은 자연수이다. 둘째 줄에는 0번 노드부터 N-1번 노드까지, 각 노드의 부모가 주어진다. 만약 부모가 없다면 (루트) -1이 주어진다. 셋째 줄에는 지울 노드의 번호가 주어진다.

## 전체 코드
```C
#include <iostream>
#include <vector>

using namespace std;
int n,k,leaf=0,root;
vector<int> tree[51];


int dfs(int node) {
	if (node == k) return -1;
	if (!tree[node].size()) {
		leaf++;
		return 0 ;
	}
	for (int i = 0; i < tree[node].size(); i++) {
		int tmp = dfs(tree[node][i]);
		if (tmp == -1 && tree[node].size() == 1)
			leaf++;
	}
	return 0;
}

void solve() {
	dfs(root);
	cout << leaf;
}



int main() {
	cin >> n;
	for (int i = 0; i < n; i++) {
		int t1;
		cin >> t1;
		if (t1 == -1)
			root = i;
		else
			tree[t1].push_back(i);
	}
	cin >> k;
	solve();
	
	return 0;
}
```

# [[BOJ]1260](https://www.acmicpc.net/problem/1260)

## 풀이

첫째 줄에 정점의 개수 N(1 ≤ N ≤ 1,000), 간선의 개수 M(1 ≤ M ≤ 10,000), 탐색을 시작할 정점의 번호 V가 주어진다. 다음 M개의 줄에는 간선이 연결하는 두 정점의 번호가 주어진다. 어떤 두 정점 사이에 여러 개의 간선이 있을 수 있다. 입력으로 주어지는 간선은 양방향이다.

graph라는 2차원 배열을 통해 각 정점끼리 연결된 것을 표현하고 각 정점을 방문하면 visited라는 배열의 해당 index 값을 1로 바꿔주었다
그리고 BFS 한정으로 큐(Queue)를 사용했는데 front와 rear라는 변수를 통해 enqueue, dequeue할 때의 위치를 나타내었다

## 전체 코드
```C
#include <iostream>
#include <vector>
#include <string.h>
#include <queue>
#include <algorithm>
using namespace std;
 
vector<int> vec[10002];
vector<int> result_bfs;
vector<int> result_dfs;
bool visit[1002];
 
void bfs(int temp){
    queue<int> q;
    q.push(temp);
    visit[temp] = true;
    while(!q.empty()){
        int x = q.front();
        q.pop();
        result_bfs.push_back(x);
 
        for (int i = 0; i < vec[x].size(); i++){
            if(!visit[vec[x][i]]){ //방문하지 않은 곳만 탐색
                q.push(vec[x][i]); 
                visit[vec[x][i]] = true;
            }
        }
    }
}
 
void dfs(int x){
    visit[x] = true;
    result_dfs.push_back(x);
 
    for (int i = 0; i < vec[x].size(); i++){
        if(!visit[vec[x][i]]){ //방문하지 않은 곳만 탐색
            dfs(vec[x][i]);
        }
    }
}
 
int main(){
    int n, m, v, a, b;
    cin >> n >> m >> v;
 
    for (int i = 1; i <= m;i++){
        cin >> a >> b;
        vec[a].push_back(b); //양방향 간선처리
        vec[b].push_back(a); //양방향 간선처리
    }
    for (int i = 1; i <= n;i++){
        sort(vec[i].begin(), vec[i].end()); // 낮은 숫자부터 탐색.
    }
    bfs(v);
    memset(visit, false, sizeof(visit));
    dfs(v);
    for (int i = 0; i < result_dfs.size() ;i++){
        cout << result_dfs[i] << " ";
    }
    cout << '\n';
    for (int i = 0; i < result_bfs.size() ;i++){
        cout << result_bfs[i] << " ";
    }
    
    return 0;
}
```
