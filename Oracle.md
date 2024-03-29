## 🚀 관계형 데이터베이스 DBMS



#### 관계형 데이터베이스(relational database)란?

관계형 데이터베이스는 현재 가장 많이 사용되고 있는 데이터베이스의 한 종류입니다.

관계형 데이터베이스란 테이블(table)로 이루어져 있으며, 이 테이블은 키(key)와 값(value)의 관계를 나타냅니다.

이처럼 데이터의 종속성을 관계(relationship)로 표현하는 것이 관계형 데이터베이스의 특징입니다.



#### 관계형 데이터베이스의 특징

관계형 데이터베이스의 특징은 다음과 같습니다.

 

1. 데이터의 분류, 정렬, 탐색 속도가 빠릅니다.

2. 오랫동안 사용된 만큼 신뢰성이 높고, 어떤 상황에서도 데이터의 무결성을 보장해 줍니다.

3. 기존에 작성된 스키마를 수정하기가 어렵습니다.

4. 데이터베이스의 부하를 분석하는 것이 어렵습니다.

​     [출처 :  TCP School 링크](https://www.tcpschool.com/mysql/mysql_intro_relationalDB)







## 💻 트랜잭션(transaction)이란

 트랜잭션은 데이터베이스 관리시스템(DBMS)에서 하나의 작업의 단위이다.

데이터베이스는 여러 사람들이 데이터를 공유하고 사용할 목적으로 사용된다. 그렇기 때문에 다수의 사람들이 동시에 사용하더라도 데이터에 문제가 없어야한다. 트랜잭션은 모든 명령문을 완벽하게 처리하거나, 하나의 명령문이라도 문제가 발생하면 모든 명령문을 수행하지 않고 데이터를 보존하는 기능을 하고 해야한다.

트랜잭션의 예시에 가장 적합한게 은행이라고 볼 수 있다. 예를들어 A계좌에 1000원이 있다고 하자. 이때 서로 다른 2대의 ATM 기기에서 동시에 A계좌의 1000원을 인출하려고 한다. 정말 거의 동시에 인출을 시도했을 때 트랜잭션이 제대로 기능하지 않아 두명 다 각각 1000원씩 인출해 간다면 은행은 아마 파산할 것이다. 그래서 은행은 두 트랜잭션을 모두 수행하지 않거나, 0.000001 초라도 빠른 사람의 요청을 수행하고 나머지 사람에게는 지급부족으로 요청을 거절해야 한다.

이러한 트랜잭션의 기능을 제대로 수행하기 위해서는 네 가지 특성을 만족해야하는데 ACID 특성이라고 부른다.

 
- **원자성 (Atomicity)** : 원자성이란 트랜잭션이 수행하는 연산들을 모두 정상적으로 처리하거나 모두 처리하지 않아야 한다는 all-or-nothing 방식을 의미한다. 

  

- **일관성 (Consistency)** : 일관성은 트랜잭션이 성공적으로 수행된 이후에도 데이터베이스의 데이터는 일관된 상태를 유지해야 한다는 의미이다.

  

- **격리성 (Isolation)** : 격리성은 하나의 트랜잭션이 완료될 때까지 다른 트랜잭션이 간섭하지 못하도록 하여 각각의 트랜잭션이 독립적으로 수행되어야 한다는 의미이다.

  

- **지속성 (Durability)** : 지속성은 트랜잭션이 성공적으로 완료된 이후에 데이터베이스의 데이터들이 영구적으로 보존되어야 한다는 의미이다. 

***

### :star: 트랜잭션 의 개념

select 조회는 데이터의 값이 수정되거나 추가되거나 삭제되지않기때문에 트랜잭션이 일어나지않는다고 본다

조작이 이뤄질때 ! 정확히 말하면 테이블에서  insert , update , delete 를 할때를 트랜잭션의 범위에 해당된다.

조작을 시작하는 시점부터 조작을 마무리하는 끝점 마지막점까지가 `트랜잭션의 범위` 다.

트랜잭션을 완료하면 `commit` 을 해서 마무리한다.

트랜잭션을 관리하는 `commit` 과 `rollback` 이 있는데

rollback 은 현재까지의 트랜잭션을 무효화 시키는 개념이다.

`rollback` 은 마지막 `commit` 시점으로 돌아갈수 있는데, 만약 트랜잭션을 정상적으로 `commit`을한후 이어서 update 로 데이터를 수정하는데 잘못하여 모든 name 의 값을 '만득이' 로 바꾸게 되었다고 생각해보자 원하는 결과가 아니라서 다시 일일이 그많은 데이터들을 다시 값을 바꾸게된다면 엄청 힘들것이다. 이때 몇번의 트랜잭션이 일어났다고 하더라도 `rollback`; 를 입력하면 마지막 `commit` 시점으로 즉 update 쿼리문을 입력하기 전 내용의 데이터로 되돌아갈수 있다.!





### :star: SQL 

* `Create` 
  * 테이블 생성
    * **`create table "info" ("num" number primary key,"name" varchar2(100),"birth" date,"phone" varchar2(15));`**

* `Read`
  * 테이블 조회
    * 선택조회 : num과 name 만 보고싶다면 **`select "num","name" from "info";`**
    * 조건조회: **`select "name" from "info" where "num"=1;`** 
    * 전체조회: **`select * from "info";`**

* Update
  * 데이터 수정
    * **`update "info" set "name"='박꺽정' where "num"=1;`**

* Delete
  * 데이터 삭제 ( :heavy_exclamation_mark: where 을 안쓰면 데이터가모두 삭제될수있다.)
    * delete from "info" where "name"='박꺽정';


:heart_decoration: tip

* 현재 계정의 테이블 목록 확인하기
  * select * from tab;
* 현재 계정의 테이블 개수 확인하기
  * select count(*) from tabs;

:heavy_check_mark: SQL 문법은 더 다양하지만  CRUD 의 기본명령어 구문만 알아도 데이터베이스를 활용할 기본 준비는 된거다. 
