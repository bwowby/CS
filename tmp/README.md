CS 복합 (_분류 및 순서는 나중에 정리..._)
-------

- - -
```Index```
* OS : [페이지 교체 알고리즘](#페이지-교체-알고리즘)
  * FIFO
  * Optimal
  * LRU
  * LRU 근사
  * NUR

* 보안 : [대칭 비대칭키 암호화](#대칭-비대칭키-암호화) 
  * RSA 알고리즘
  
* 알고리즘 : [정렬 알고리즘](#정렬-알고리즘)
  * Quick Sort   
  * Merge Sort
 
* 자료구조 : [그래프](#그래프)
  * 인접 행렬
  * 인접 리스트
  * DFS/BFS
  * AVL 트리
  * 레드블랙 
  * 최소신장 트리   
  
* OS : [프로세스와 스레드](#프로세스와-스레드)
  + 프로세스
  + 스레드
 
* 네트워크 : [IP와 IP주소](#IP-IP주소)
  + IP
  + IP 주소
 
* 네트워크 : [DNS](#DNS)
  + DNS 
  + DNS 서버
  + 도메인 질의 과정
  
- - - 
   
## 페이지 교체 알고리즘
### 1. FIFO (First In First Out)
메모리에 ```먼저 올라온``` 페이지를 먼저 내보내는 가장 간단한 알고리즘.   
victim page는 가장 먼저 메모리에 올라온 페이지로 초기화 코드에 대해서 적절한 방법.   
페이지 수 적을 수록 계속 교체해 주어야해 페이지 부재는 더 많이 일어나게 된다.
프레임 수가 많으면 페이지 부재 수가 줄어드는 것이 일반적이지만, 프레임 수 증가 시켰는데도 페이지 부재가 더 많이 일어나는 벨레이디의 모순이 많이 발생.   

### 2. OPT (Optiaml) 
현재 메모리에 올라와 있는 페이지 중 ```앞으로 가장 사용되지 않을``` 페이지를 우선적으로 교체하는 알고리즘.   
최적 교체 알고리즘 으로 가장 페이지 교체수가 적은 알고리즘.   
프로세스가 미래에 사용할 페이지를 미리 알아야한 다는 것이 전제조건이므로 알 방법이 없기에 최적으로 구현이 불가능한 알고리즘. 연구목적으로 주로 사용됨.   

### 3. LRU (Least Recently Used)
```최근에 가장 사용하지 않은``` 페이지를 교체하는 알고리즘.  
최근에 사용하지 않으면 나중에도 사용하지 않을 것이라는 아이디어에서 나온 최적 알고리즘과 비슷한 효과를 낼 수 있는 알고리즘이다.  
각 페이지마다 카운터나 스택을 두어 과거의 데이터를 바탕으로 페이지가 사용될 시간을 예측함으로써 많은 운영체제가 채택하는 알고리즘.

### 4. LRU 근사 (LRU Approximation Page Replacement)
#### 부가 참조 비트 알고리즘 
각 페이지에 8비트를 할당하여 일정 주기마다 페이지 참조 비트들을 쉬프트 연산하여 가장 오랫동안 쓰이지 않는 (가장 작은 획수를 갖는) 페이지 교체

#### 이차 기회 알고리즘
기본은 FIFO 교체로 페이지 선택 시 마다 참조 비트 확인. 비트 == 0이면 페이지 교체 1이면 한번 기회를 주고 다음 FIFO 페이지로 넘어간다.
한번 기회를 얻은 페이지는 참조 비트가 해제되고 도착 시간이 현재로 갱신 -> 다른 페이지들 교체될 때 까지 교체되지 않는다. 모든 페이지의 
비트가 1이면 모든 참조 비트를 0으로 만들어 2차 기회를 준다
순환 큐 이용

#### 개선된 이차기회 알고리즘
변경 비트를 두어 쓰기 작업을 한 페이지만 보조 메모리에 다시 작성하여, 변경된 페이지에 대해 우선순위를 줘 입/출력 횟수를 줄이기 위함.

### 5. NUR (Not Used Recently)
LRU와 비슷한 방식으로 최근에 사용하지 않은 페이지 교체. 
LRU의 단점인 시간 오버헤드를 적게하고 참조비트,변형비트를 두어 사용
   
      
      
- - -
   
## 대칭 비대칭키 암호화

| 비교 | 대칭 | 비대칭 |
----|----|---|
| 키 개수 | 한개 | 두개 |
| 키 보관 | 개인이 비밀리에 | 개인키는 비밀리에,공개키는 어디든 배포 가능 |
| 키 교환 | 교환이 어려우며 위험 | 공개키 교환 매우 쉬움 |
| 키 길이 | 56 bit,128 bit | 512,1024,2048 bit |
| 암호화/복호화 속도 | 빠름 | 느림 |
| 암호화 가능 평문 길이 | 제한 없음 | 제한 있음 |
   

### 1. 대칭키 암호화
```암호화/복호화키가 같은``` 암호화 방식.   
비대칭형 알고리즘 보다 빠르다 -> 통신에 유리하므로 주로 데이터 통신의 암호화에 사용.   
암호문의 크기가 크지 않아 암호화 시 데이터 증가가 없다 -> 네트워크 대역폭이 추가로 필요하지 않아 통신에 적합. 
>A와 B가 동일한 비밀키를 가지게 하는 방법? (네트워크를 통해 A-(비밀키)->B는 중간에 가로챌 수 있기 때문에 안됨)
>1. 비밀키를 비대칭형 알고리즘을 이용해 암호화 후 전송.
>2. Key를 전송하지 않고도 동일한 Key를 생성할 수 있도록 하는 알고리즘 사용(Diffie-Hellman...)

SEED,DES,DES3,AES 등의 알고리즘이 있다.

### 2. 비대칭키 암호화
```암호화와 복호화에 사용되는 키가 서로 다른``` 암호화 방식. 공개키 알고리즘.
대칭형 알고리즘의 Key를 암호화하거나 인증에 주로 사용.   
A는 공개키(Public Key)와 개인키(Private Key)를 생성하며 A의 공개키를 이용하여 암호화한 데이터는 A의 개인키로만 복호화 할 수 있고, A의 개인키로 암호화한 데이터는 A의 공개키로만 복호화 가능하다는 특징이 있다.   
>A - (A 공개키) -> B   
A <- (A 공개키로 암호화한 데이터) - B : 암호화된 데이터는 A의 개인키로만 복호화 가능 (중간에 공개키/문서 가로채도 안전)   

C가 A인척 자신의 공개키를 넘기고 B가 속아서 C에게 데이터를 전송하면 전송에 사용할 비밀키를 획득할 수 있으므로 ```인증서```를 사용한다.
인증서에는 인증받는 자(target)의 정보, 공개키, 유효기간, 인증 기관 정보 등이 기록되어 있음.
#### RSA 알고리즘
대표적인 비대칭키 암호 알고리즘.   
```키 생성 방식```
1. 소수 p,q 준비
2. p * q = N 계산
3. (p-1) * (q-1)과 서로소이고 1<e<(p-1) * (q-1) 인 공개키 e 생성
4. (d * e) mod% (p-1) * (q-1) =1 이고 0<=d<=N인 d 구하기
N,e는 공개키 d는 비밀키로 사용    
N을 소인수 분해하면 p,q 값 구할 수 있고 공개키 e와 p,q를 이용해 개인키 d를 얻을 수 있으므로 안전성 보장을 위해 적어도 1024 bit 길이의 키값 사용하고 현대에는 2048 bit를 권장.
   
암호화 : 보내려는 평문 a 를 x = a^e mod N 으로 암호화 -> 암호화된 평문 x   
복호화 : 암호문 x 를 a = x^d mod N 하여 다시 a로 복호화


- - -
   
## 정렬 알고리즘
| Name | Best | Avg | Worst | Space complexity |
| --- | --- | --- | --- | --- |
| 삽입정렬 | n | n^2 | n^2 | n |
| 선택정렬 | n^2 | n^2 | n^2 | n | 
| 버블정렬 | n^2 | n^2 | n^2 | n |
| 셀정렬 | n | n^1.5 | n^2 |  |
| 퀵정렬 | nlogn | nlogn | n^2 | n |
| 힙정렬 | nlogn | nlogn | nlogn | | 
| 합병정렬 | nlogn | nlogn | nlogn | 2n |

### Quick Sort
분할 정복으로 정렬.   
기저 조건은 n=0,1일 때, pivot을 기준으로 왼쪽에 작은 원소, 오른쪽에 큰 원소들이 오도록 정렬.   
피벗의 선정 방법에 따라 속도가 달라진다. 다른 nlogn 정렬보다 빠름.   
최악의 경우 pivot이 항상 가장 작은 수로 선택 될 때로 n^2의 시간이 소요된다.   
* Worst
~~~
T(n) = T(n/2) + T(n/2) + O(n) = T(0) + T(n-1) + O(n)
     = T(n-1/2) + T(n-1/2) + O(n-1) + O(n)  =  T(0) + T(n-2) + O(n-1) + O(n)
     = ...
     = T(n-k) + O(n) + O(n-1) + ... + O(n-k)
     = T(n-k) + kn-k(k-1)/2
기저조건인 n-k가 1일 때 : T(n) = T(1) + (n-1)n-(n-1)(n-2)/2 = O(n^2)
~~~
   
* Code
~~~python
def quickSort(array):
    if (len(array) == 0)  | (len(array) == 1) : return array
    
    pivot = array[0]
    left = getLeftArray(array[1:], pivot)
    right = getRigthArray(array[1:], pivot)

    return quickSort(left) + [pivot] + quickSort(right) 
    
def getLeftArray(array, pivot):
    left = []
    
    for num in array :
        if num <= pivot : left.append(num)
    return left
    
def getRigthArray(array, pivot):
    right = []
    
    for num in array :
        if num > pivot : right.append(num)
    return right

~~~

### Merge Sort
분할 정복으로 정렬.   
기저 조건은 n=1일 때. 중간 기준으로 왼쪽 오른쪽으로 쪼개서 각각 재귀 후 리턴 받고, 리턴 한 왼쪽 오른쪽 배열을 비교하여 합병한다. 이때 정렬 결과가 임시배열에 저장됨. 
* Code
~~~python
def mergeSort(data) :
    if len(data) == 1 : 
        return data
    mid = len(data)//2
    
    left = mergeSort(data[:mid])
    right =  mergeSort(data[mid:])
    
    result = []
    
    leftPtr = 0
    rightPtr = 0
    
    while(leftPtr < len(left) or rightPtr < len(right)) : 
        lValue = left[leftPtr] if leftPtr < len(left) else math.inf
        rValue = right[rightPtr] if rightPtr < len(right) else math.inf
        
        if lValue  < rValue: 
            result.append(lValue)
            leftPtr += 1
        else : 
            result.append(rValue)
            rightPtr += 1
    
    return result
~~~
#### 퀵 소트 vs 머지 소트
https://medium.com/pocs/locality%EC%9D%98-%EA%B4%80%EC%A0%90%EC%97%90%EC%84%9C-quick-sort%EA%B0%80-merge-sort%EB%B3%B4%EB%8B%A4-%EB%B9%A0%EB%A5%B8-%EC%9D%B4%EC%9C%A0-824798181693   
Locality 측면에서 보자면 Merge Sort < Quick Sort. 머지소트는 쪼개어진 반쪽짜리를 각각 소팅하고 x n 하기 때문에 끝과 끝을 왔다갔다하며 데이터를 탐색하게 되고 데이터가 좌우로 계속 움직이며 정렬된다. 또 내부적으로 정렬된 데이터를 복사해야하기 때문에 더 많은 시간 소요됨.   
반면 Quick Sort는 피봇 기준으로 쪼개어진 앞쪽 부분부터 정렬이 되기 때문에 데이터들이 넓은 범위에서 움직이지 않으며 pivot 주변에서 데이터 이동이 일어나기 때문에 자주 캐쉬에 있는 페이지들을 교체할 필요가 없으므로 HW적으로 더 효율적.
>TIM SORT?!   
https://d2.naver.com/helloworld/0315536
Merge Sort + Insertion Sort
- - -
   
## 그래프
### 인접 행렬
그래프의 연결관계를 2차원 배열로 나타내는 방식.   
인접 행렬 i에서 j로 가는 간선이 존재한다면 adj[i][j] = 1, 아니면 0. 가중치가 있다면 1 대신 가중치.   

### 인접 리스트
그래프의 연결관계를 vector의 배열(vector<int>adj[])로 나타내는 방식.   
adj[i] 는 노드 i에 연결된 노드들을 원소로 갖는 vector. 가중치가 있다면 pair<int,int>로 노드 번호, 가중치 저장하면 됨. vector에 들어간 노드의 순서는 의미없음.
 
 ### DFS/BFS 
 #### DFS
 깊이 우선 탐색. 재귀,스택으로 구현 가능. 하나의 노드에 대하여 leaf까지 끝까지 들어가서 탐색하는 방식. 단순 검색 속도는 BFS에 비해서 느리지만 traverse 할때 백트래킹에 많이 쓰인다. 

* Code
~~~python
 def dfs(node) :
   if node == leaf : 
    doSometing() 
    return
   dfs(node.left)
   dfs(node.right)
~~~

 #### DFS
 너비 우선 탐색. 큐로 구현 가능. 무한한 길이를 가지는 경로가 있을 경우 dfs는 무한한 경로에서 종료하지 못하지만, 모든 경로를 동시에 진행하기 때문에 탐색 가능. 그래프에서 최단경로 알아내기에 많이 사용.
* Code
~~~python
 def bfs(root) :
   q = queue.Queue()
   q = put(root)
     while q.qsize() > 0 : 
        node = q.get()
        if node : 
           doSometing()
        q.put(node.left)
        q.put(node.right)
~~~
### AVL 트리
이진 검색 트리이면서 balanced 트리. n개의 원소가 있을 때 O(logn) 의 복잡도로 삽입,검색,삭제 가능(레드블랙 트리보다 삽입/삭제 성능이 안좋다 -> 이유?)   
* 규칙1. 이진 트리이면서 균형 트리
* 규칙2. 모든 노드의 왼쪽/오른쪽 서브트리의 높이 차이는 1이하여야 함 -> 유지하려면 별짓을 다해야함...   
LL / : 우회전  RR \ : 좌회전  RL < : 중간 노드 좌회전-> 전체 우회전  LR > : 중간 노드 우회전 -> 전체 좌회전   
[별짓의 detail] :https://www.zerocho.com/category/Algorithm/post/583cacb648a7340018ac73f1
* 삽입 연산 : 이진 탐색 트리처럼 왼쪽 작은 원소, 오른쪽 큰 원소로 두면서 불균형이 일어날 때 마다 회전을 시키며 균형 유지

### 최소 신장 트리
* 신장 트리(Spanning Tree)   
그래프내의 정점을 모두 포함하는 트리.   
n개의 정점을 가지는 그래프를 최소 간선 수인 n-1개로 연결하여 만든 트리. 하나의 그래프에는 많은 신장 트리 존재하며 사이클을 포함해서는 안된다. 
* 최소 신장 트리(MST)   
신장 트리 중 사용된 간선들의 가중치의 합이 최소인 트리.   
가중치가 있는 그래프의 모든 정점을 가장 적은 수의 간선과 비용으로 연결한 것.   
MST의 구현 방법은 크게 두개. Kruskal,Prim   

  + Kruskal [detail] : https://gmlwjd9405.github.io/2018/08/29/algorithm-kruskal-mst.html   
O(n^2). ```greedy 하게 모든 정점을 최소비용으로``` 선택하여 연결하는 답을 구하는 것. 간선 선택 기반.   
간선의 가중치를 오름차순으로 정렬해 작은 것 부터 선택해 나가는 알고리즘.   
이때 다음에 선택할 간선이 사이클을 만드는지의 여부를 검사할 때 union-find 사용   
  + Prim [detail] : https://gmlwjd9405.github.io/2018/08/30/algorithm-prim-mst.html   
O(eloge). 시작 정점을 기준으로 가장 낮은 가중치와 연결된 정점을 먼저 선택하며 확장해 나가는 것. 정점 선택 기반.   
트리를 확장하면서 n-1개 간선을 가질 때 까지 반복.

그래프 내에서 적은 숫자의 간선 가지는 희소 그래프의 경우 크루스칼 적합. 간선이 많은 밀집 그래프의 경우 프림이 적합.



- - -
   
## 프로세스와 스레드 
https://shoark7.github.io/programming/knowledge/difference-between-process-and-thread
### 프로세스
```메모리에 적재되어 실행되고 있는 프로그램.``` 동적. 프로그램의 인스턴스.   
운영체제가 관리하며 시간,자원을 할당받아 실행됨. 메모리 공간 상에서 ```Code(Method,Class,Static),PC Register,Heap,Stack``` 영역으로 나뉜다. 각각의 프로세스는 독립적으로 관리되며 서로 자원을 공유하는 일도 없다(대신 같은 프로그램의 프로세스는 Code 영역 공유)   

### 스레드
프로세스 내에서 실행되는 흐름. 모든 하나의 프로세스는 메인 스레드에서 시작되며 실행된다. 한 프로세스 안의 스레드들은 ```스택 공간을 제외한 나머지 영역과 자원을 공유.```   


- - -
   
## IP와 IP 주소
### IP 
* 물데네전세표응 중 네트워크 계층에서 사용하는 네트워크 프로토콜. 비신뢰성,비연결성.   
* 상위 계층인 전송 계층(TCP/UDP)에서의 ```세그먼트``` 를 받아 IP 헤더(목적지, 전송지의 주소/host 주소...) 를 붙여 ```패킷```으로 다른 호스트까지 전송.   

```ip header```   
<img src="https://user-images.githubusercontent.com/18088806/104322096-d45ecc00-5527-11eb-8224-661c5efb04bc.png" width="50%"></img>   

* 네트워크 상에서 이 주소를 바탕으로 패킷이 전송
* 게이트웨이인 라우터의 라우팅 프로토콜(RIP,IGRP/OSPF..)을 기반으로 패킷이 목적지까지 도달
   
### IP 주소   
* IPv4. 32비트로 구성된 네트워크상 컴퓨터를 식별하기 위한 논리적 주소. 물리적 주소인 MAC과 구별됨.    
* 네트워크 주소(-.-.-)와 호스트 주소(.-) 로 조합되어 구성.   
* 패킷의 IP 헤더에는 반드시 보내는 곳, 받는 곳의 IP 주소가 추가됨.
* -.-.-.0 : 네트워크 주소와  -.-.-.255 : 브로드캐스팅 주소는 사용 불가.   


- - -
   
## DNS  
### DNS   
 * Domain Name System 도메인 이름의 수직적 체계
 * 도메인 구입 시 각 체계별 도메인을 지정하여 등록하며 3->2->1 단계 순으로 표기
 * 인터넷 도메인 체계는 최상위 루트 도메인 서버로 시작
 * 1단계 도메인(TLD): 국가최상위 도메인/일반 최상위 도메인으로 구분(kr,jp,us../com,net,org...)
 * 2단계 도메인(SLD): 도메인을 등록한 조직 나타냄(ac,co..)
 * 3단계 도메인(Domain Name): 임의로 지정 가능한 자율적 이름(naver,google...)
 ><img src = "https://xn--3e0bx5euxnjje69i70af08bea817g.xn--3e0b707e/images/domain/imgDomainSys02.gif"/>   
 
### DNS 서버   
* Domain Name Server   
* 네트워크 상 고유 식별자인 ip 주소를 기본 체계로 하나, 이 주소를 인간이 기억하기 편한 언어체계로 변환하는 작업을 해줌.   
* 도메인 이름으로 요청한 클라이언트는 돌려받은 IP 주소로 라우터를 통해 목적지에 접속. 
### 도메인 질의 과정
1. ```abcd.com``` 도메인 입력 시 /etc/resolve.conf 에 지정된 네임 서버(resolver)로 도메인 주소에 대한 요청 전달
2. resolver에 있는 루트 네임 서버의 IP 기록한 hint 파일을 참조해 루트 네임 서버로 요청 전달.
3. 루트 네임 서버가 가진 TLD 네임 서버명과 IP 주소(glue record)를 참조하여 .com 네임서버를 참조하라고 응답.
4. .com 네임 서버가 가진 글루레코드를 참조하여 ```abcd.com``` 네임서버 참조하라고 응답.
5. ```abcd.com``` 네임 서버는 도메인에 대한 zone 파일을 참조하여 ```abcd.com```의 IP 주소를 최초요청한 1번의 네임서버로 돌려준다.
6. 최초 요청을 받은 네임서버는 클라이언트에게 IP 주소 전송.
* DNS 서버는 한번 검색할 결과를 메모리의 캐쉬에 기록하여 사용하며, TTL이 정해져 있어 유효기간 지난 정보는 삭제함.   
><img src ="https://d1.awsstatic.com/Route53/how-route-53-routes-traffic.8d313c7da075c3c7303aaef32e89b5d0b7885e7c.png"/>
