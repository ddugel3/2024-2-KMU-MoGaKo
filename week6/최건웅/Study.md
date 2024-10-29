### 트리(tree)
- 계층적인 구조 표현
    - 조직도
    - 디렉토리와 서브 디렉토리 구조
    - 가계도 등등
    
![image](https://user-images.githubusercontent.com/50076031/124688720-40881e80-df12-11eb-89cf-5d7f46bdd6cc.png)
https://towardsdatascience.com/8-useful-tree-data-structures-worth-knowing-8532c7231e8c

- 트리는 노드(node)들과 노드들을 연결하는 링크(link)들로 구성됨
- 맨위의 노드를 "루트(Root)" 라고 부름
- 노드들을 연결하는 선을 "link", "edge", "branch" 등으로 부름
- 루트노드를 제외한 트리의 모든 노드들은 유일한 부모 노드를 가짐
- 부모가 동일한 노드 -> 형제(sibling) 관계라고 부름
- 리프(leaf) 노드: 자식이 없는 노드
- 트리의 높이(height) => 5

#### 트리의 기본적인 성질
- 노드가 N개인 트리는 항상 N-1개의 링크(link)를 가진다.
- 루트에서 어떤 노드로 가는 경로는 유일하다.
- 또한 임의의 두 노드간의 경로도 유일하다.

### 이진 트리(binary tree)
- 이진 트리에서 각 노드는 최대 2개의 자식을 가진다.
- 각각의 자식 노드는 자신이 부모의 왼쪽 자식인지, 오른쪽 자식인지 지정된다.

![image](https://user-images.githubusercontent.com/50076031/124689386-6cf06a80-df13-11eb-9a7e-af46341ff6e7.png)
https://en.wikipedia.org/wiki/Binary_tree

#### 이진 트리의 표현

![image](https://user-images.githubusercontent.com/50076031/124690446-2d2a8280-df15-11eb-9341-611f8f3081b7.png)

- 각 노드에 하나의 데이터 필드와 왼쪽 자식(left), 오른쪽 자식(right), 부모 노드(p)의 주소를 저장
- 부모 노드의 주소는 반드시 필요한 경우가 아니면 보통 생략

#### 이진 트리의 순회(traversal)
- 순회: 이진 트리의 모든 노드를 방문하는 일
- 전위 순위(preorder) 순회
  - 루트 노드를 먼저 순회한 후 '왼쪽 하위 -> 오른쪽 하위' 순으로 순회
- 중위 순위(inorder) 순회
  - 왼쪽 최 하위 노드를 먼저 순회한 후 '상위 노드 -> 오른쪽 하위' 순으로 순회
- 후위 순위(postorder) 순회
  - 왼쪽 최 하위 노드를 먼저 순회한 후 '오른쪽 하위 노드 -> 상위 노드' 순으로 순회

![image](https://user-images.githubusercontent.com/50076031/124915301-5853c580-e02c-11eb-8942-465ddb0e6fd6.png)

- 전위 순회: 1 -> 2 -> 4 -> 5 -> 3 -> 6 -> 7
- 중위 순회: 4 -> 2 -> 5 -> 1 -> 6 -> 3 -> 7
- 후위 순회: 4 -> 5 -> 2 -> 6 -> 7 -> 3 -> 1

### 이진검색트리(BST, Binary Search Tree)
- 이진 트리
- 각 노드에 하나의 키를 저장
- 각 노드 v에 대해 왼쪽 트리에 있는 키들은 key[v]보다 작거나 같고, 오른쪽 트리에 있는 값은 크거나 같다.

![image](https://user-images.githubusercontent.com/50076031/124694414-2c491f00-df1c-11eb-81b7-ce4136a8c2e6.png)


#### 검색

![image](https://user-images.githubusercontent.com/50076031/124694706-c5783580-df1c-11eb-86ce-ca6d14e7b03e.png)

- 이진검색트리에서 13을 검색
- 15보다 작기 때문에 왼쪽 노드
- 6보다 크기 때문에 오른쪽 노드
- 7보다 크기 때문에 오른쪽 노드
- 찾는값인 13
- 수도코드

```java
// x: 루트노드, k: 찾는 값
TREE-SEARCH(x, k)
1. if x == NIL or k == key[x]
2.     then return x
3. if k < key[x]
4.     then return TREE-SEARCH(left[x], k)
5.     else return TREE-SEARCH(right[x], k)

시간 복잡도: O(h), h = 트리의 높이
```
