
# [[BOJ]1753](https://www.acmicpc.net/problem/1753)

## 풀이
방향그래프가 주어지면 주어진 시작점에서 다른 모든 정점으로의 최단 경로를 구하는 프로그램을 작성하시오. 단, 모든 간선의 가중치는 10 이하의 자연수이다.

첫째 줄에 정점의 개수 V와 간선의 개수 E가 주어진다. (1 ≤ V ≤ 20,000, 1 ≤ E ≤ 300,000) 모든 정점에는 1부터 V까지 번호가 매겨져 있다고 가정한다. 둘째 줄에는 시작 정점의 번호 K(1 ≤ K ≤ V)가 주어진다. 셋째 줄부터 E개의 줄에 걸쳐 각 간선을 나타내는 세 개의 정수 (u, v, w)가 순서대로 주어진다. 이는 u에서 v로 가는 가중치 w인 간선이 존재한다는 뜻이다. u와 v는 서로 다르며 w는 10 이하의 자연수이다. 서로 다른 두 정점 사이에 여러 개의 간선이 존재할 수도 있음에 유의한다.

## 전체 코드
```C++
#include <iostream>
#include <algorithm>
#include <vector>
#include <queue>
#define INF 987654321

using namespace std;
int v,e,k;
int dis[20001];
vector < pair<int,int> > adj[20001];

void solve(){
    dis[k] = 0;
    priority_queue < pair<int, int> > pq;
    pq.push(make_pair(0,k));
    while(!pq.empty()){
        int cur = pq.top().second;
        int curdis = -pq.top().first;
        pq.pop();
        if(curdis > dis[cur])
            continue;
        for(int i = 0; i < adj[cur].size(); i++){
            int next = adj[cur][i].second;
            int nextdis = curdis + adj[cur][i].first;
            if(dis[next] > nextdis){
                dis[next] = nextdis;
                pq.push(make_pair(-nextdis, next));
            }
        }
    }
}

int main (){
    int a, b, c;
    cin >> v >> e >> k;   
    for(int i = 1; i<= v; i++)
        dis[i] = INF;
    for(int i = 0 ; i < e ; i++){
        cin >> a >> b >> c;
        auto it = find_if(adj[a].begin(), adj[a].end(),
        [&b](const pair<int,int>& elem){return elem.second == b;});
        if(it == adj[a].end())
            adj[a].push_back(make_pair(c,b));
        else{
            if(it->first > c)
                it->first = c;
        }
    }
    solve();
    for(int i = 1; i <= v; i++){
        if(dis[i] != INF)
            cout << dis[i] << "\n";
        else
            cout << "INF\n";
    }
    
}
```



# [[BOJ]11404](https://www.acmicpc.net/problem/11404)

## 풀이
n(2 ≤ n ≤ 100)개의 도시가 있다. 그리고 한 도시에서 출발하여 다른 도시에 도착하는 m(1 ≤ m ≤ 100,000)개의 버스가 있다. 각 버스는 한 번 사용할 때 필요한 비용이 있다.
모든 도시의 쌍 (A, B)에 대해서 도시 A에서 B로 가는데 필요한 비용의 최솟값을 구하는 프로그램을 작성하시오.

최단거리 알고리즘 중 모든정점에서 모든정점으로 가는 최단거리를 구하는 플로이드 워셜 알고리즘을 사용해야한다.
이 알고리즘은 O(n^3)이라는 시간복잡도가 걸린다.

## 전체 코드
```C++
#include <stdio.h>

int arr[105][105];

int main(){
    int n,m;
    int a,b,c;

    scanf("%d",&n);
    scanf("%d",&m);

    for(int i=1;i<=n;i++)
        for(int j=1;j<=n;j++)
            arr[i][j] = INF;

    for(int i=1;i<=n;i++)
        arr[i][i] = 0;

    for(int i=0;i<m;i++){
        scanf("%d %d %d",&a,&b,&c);

        if(arr[a][b]>c)
            arr[a][b] = c;
    }

    for(int k=1;k<=n;k++)
        for(int i=1;i<=n;i++)
            for(int j=1;j<=n;j++)
                if(arr[i][j]>arr[i][k]+arr[k][j])
                    arr[i][j] = arr[i][k]+arr[k][j];

    for(int i=1;i<=n;i++){
        for(int j=1;j<=n;j++)
            if(arr[i][j]==INF) printf("0 ");
            else printf("%d ",arr[i][j]);
        printf("\n");
    }


    return 0;
}

```
