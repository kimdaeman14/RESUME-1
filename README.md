# Chapter 40: Depth-First Search

이 장에서는 그래프를 탐색하거나 검색하기위한 또 다른 알고리즘 인 DFS (Depth-First Search)를 살펴 봅니다.

지금부터 깊이 우선 탐색(DFS)를 진행해볼거고 아래의 그래프를 전체 다 탐색할때까지 진행한다.

![image](https://user-images.githubusercontent.com/34432988/77828221-7c540600-715d-11ea-89dd-1bfc125850ff.png)

깊이우선탐색은 말그대로 제일 깊은곳까지 탐색을했다가 다시 뒤로 돌아나오면서 아직 탐색하지 않은 갈림길?이 있다면 다시 제일 깊게 탐색하고, 다시 돌아나오고, 다시 탐색하고,,, 그러는 알고리즘이다.

## 주요 사항은 아래와 같다.

- 스택을 활용하므로 나중에 들어온게 먼저나가는 후입선출(LIFO) 구조로 진행된다.
- 현재 점(vertex)이 더 갈 수 있는지를 찾는다.
- 방문한 점을 기억한다.
- 다음 점이 있어서 더 갈 수 있다면 들어가고, 없다면 그대로 되돌아나온다.
- 현재 점(vertex)의 인접한 정점(갈림길)이 있는지 확인한다.
- 방문하지 않은 점이 있다면 들어가서 끝까지 탐색하고, 되돌아 나온다.
- 스택이 비워질때까지 작업을 계속한다.

## 시작.

![image](https://user-images.githubusercontent.com/34432988/77828206-65adaf00-715d-11ea-9a2d-be2f252799d9.png)

A를 스택에 push한다.
현재 몇번 작업했는지 알 수 있다.

![image](https://user-images.githubusercontent.com/34432988/77828240-9392f380-715d-11ea-903f-a73b953e1f41.png)

갈림길도 없고 아무것도 없고하니 B를 push 한다.
A에서 처음 인접한 B, D, C에서는 가장 최근에 추가된 점인 B부터 탐색한다.
점을 추가하는 순서에 따라 엄청 돌아갈 수도 있기때문에 검색 결과에 영향을 미칠 수 있다.

![image](https://user-images.githubusercontent.com/34432988/77828245-97bf1100-715d-11ea-92fc-2f597eae1744.png)

위와 같은 이유로 E, F를 push한다.

![image](https://user-images.githubusercontent.com/34432988/77828248-9b529800-715d-11ea-8d83-e608f710ce27.png)

위와 같은 이유로 G, C를 push한다.
그런데 더 이상 들어갈 데가 없다. 막 다른 길에 도달했으므로 이제 스택에서 C를 빼내서 역추적을 시작한다.

![image](https://user-images.githubusercontent.com/34432988/77828251-9db4f200-715d-11ea-95c4-1fb16d2344a5.png)

C 를 pop해서 일단 G 로 왔다. 인접한 점이 있는지 확인한다. 없다. 다시 팝한다.
F이다. 인접한 점인 C가 있으나 이미 방문한 곳이다. 다시 팝한다.

![image](https://user-images.githubusercontent.com/34432988/77828277-be7d4780-715d-11ea-8543-3bc626f5ae26.png)

이제 E로 돌아왔다. 인접한 곳이 있고 아직 방문하지 않은 H 가 남아있다. 푸쉬한다.
또 다시 막다른 골목에 다다랐다. 위와 똑같이 다시 스택에서 팝을 하면서 백트래킹한다.

![image](https://user-images.githubusercontent.com/34432988/77828280-c2a96500-715d-11ea-92f6-860c5a419ca6.png)

인접한 점이 있고 아직 방문할 점이 남아있는 A 까지 간다.

![image](https://user-images.githubusercontent.com/34432988/77828282-c5a45580-715d-11ea-936e-3b43a4391847.png)


A 에 왔다. 인접한 점인 D 가 있고, 아직 방문하지 않았으므로 푸쉬한다.
또 다시 막다른 길에 도달했다.

![image](https://user-images.githubusercontent.com/34432988/77828285-c89f4600-715d-11ea-98bc-17740c13ac0b.png)


막다른 길에 도달했으므로 다시 팝한다.
A 로 돌아왔다.
인접한 점이 있지만 전부다 방문했던 곳이므로 A를 팝한다.
스택이 비었으므로 탐색을 종료한다.


## Implement

![image](https://user-images.githubusercontent.com/34432988/77828344-2f246400-715e-11ea-8b28-17dbdce2201b.png)




## Key points
점(vertex), 간선(edge)

- 시간복잡도

일단 모든 점을 1번씩 방문하므로 O (V) 이다.

그리고 모든 간선을 1번씩 push하고 다시 pop하므로 O (2E) 이다.

전체적으로는 O(V+2E)인데 의미없는 상수를 제외하면

DFS의 시간복잡도는 O(V+E)로 표현할 수 있다.

- 공간복잡도

DFS의 공간 복잡도는 여기서는 스택을 사용해서 구현했고, 점을 3 개의 별도 데이터 구조(아래)에 저장했기 때문에 O (V)이다.

var stack: Stack<Vertex<Element>> = [] //그래프를 통해 경로를 저장하는데 사용한다.
  
var pushed: Set<Vertex<Element>> = [] //동일한 점을 두번 방문하지 않도록 기억한다.
  
var visited: [Vertex<Element>] = [] //점을 방문한 순서를 저장한다.
  
## 출처 :
이 글은 아래 링크의 챕터 40장을 공부하여 작성한 글입니다.

https://store.raywenderlich.com/products/data-structures-and-algorithms-in-swift

참고링크 :

Set insert vs update

https://zeddios.tistory.com/206
