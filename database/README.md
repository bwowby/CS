Database
-------

- - -
```Index```
* [PK/FK/UK](#PK-FK-UK)

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
