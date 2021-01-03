Database
-------

- - -
```Index```
* [PK/FK/UK](#PK-FK-UK)
* [Index](#Index)

- - - 

## PK/FK/UK 
### 1. PK
  * 각 해을 고유하게 식별하는 역할을 담당.
  * 테이블 당 하나만 정의 가능.   
  * NOT NULL + UNIQUE Constraint.   
  * Unique index 자동 생성.    
  
### 2. FK
  * 다른 부모 테이블의 참조되는 키는 PK 혹은 UK 여야 함.
  * 부모 테이블 삭제 시 자식 테이블 먼저 삭제해야 가능.
  * ON DELETE CASCADE/ON DELETE NULL.

### 3. UK
  * Unique Key 조합의 칼럼 값은 항상 유일해야 함. 중복 방지.
  * PK와 다르게 NULL 값을 허용함(NULL 값은 중복 가능).
  * 여러 개의 Unique Key 설정 가능.
  * Unique index 자동 생성
   
- - -       
   
## Index
### 1. index?
테이블의 색인을 빠르게 하기 위해 풀스캔 하지 않고, 칼럼의 값과 해당 레코드의 주소를 키밸류 쌍으로 만든 자료구조

### 2. index 자료구조
 * B+ Tree : 일반적으로 사용하는 인덱스 알고리즘. 칼럼값 변형하지 않고, 원래의 값을 이용해 인덱싱.
 * Hash : 칼럼 값으로 해시값을 계산하여 인덱싱. 매우 빠른 검색 지원. 값을 변형하여 인덱싱하므로 값의 일부를 이용한 검색 시에는 사용할 수 없다. 메모리 기반 db에서 많이 사용
 * Hash table에 대한 접근 시 복잡도가 O(1) 이지만 등호(=) 연산에 특화된 Hash table은 부등호 연산 질의에는 적합하지 않다. 
 
 ### 3. 고려할 점
 * SELECT 시에는 빠르지만, CUD 시에는 인덱스 또한 변경해 주어야 하므로 성능에 영향이 있을 수 있음.
 * 저장 성능을 희생하고 읽기 속도를 높이는 것이라 index 설정 시 많이 설정한다고 좋은 것이 아님.
 
 ### 4. DML 수행 시 index 동작
 * ```INSERT``` : 데이터와 함께 index에 대한 데이터도 추가해야 함 -> 성능 손실
 * ```DELETE``` : index에 존재하는 값은 삭제되지 않고 표시만 해둠 -> 삭제되었지만 데이터는 여전히 남아있다
 * ```UPDATE``` : index에는 update 개념이 없어 DELETE->INSERT 작업이 발생. 다른 DML보다 더 큰 부하를 주게 된다.
