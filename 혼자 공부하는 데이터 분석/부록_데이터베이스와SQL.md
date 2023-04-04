# 데이터베이스와 SQL

## 데이터베이스

- 컴퓨터를 사용하여 저장하고 관리하는 데이터의 집합
  - 이를 보려면 데이터베이스 관리 시스템(DBMS)라는 별도의 프로그램이 필요
- 레코드(행)와 필드(열) 구성된 여러 개의 테이블
- DBMS에 전달하는 메시지는 SQL9Structured Query Language)



## SQL

- SQL문으로 DBMS에 데이터를 요청하는 것을 **쿼리(query)**라고 부른다.
  - DBMS가 이 쿼리를 이해하고 DB에서 데이터를 찾아 반환(딕셔너리 or 리스트)

- 데이터 읽기

  ```sql
  SELECT * FROM 테이블이름 WHERE 조건;
  ```

- 데이터 저장

  ```sql
  INSERT INTO 테이블이름 (열) VALUES (내용);
  ```



## SQLite

- 파이썬에 내장되어 있는 DBMS
- 데이터베이스 연결
  - connect() 함수
    - 데이터베이스와 파이썬을 처음 연결할 때 해당 이름의 데이터베이스가 없다면 자동 생성

- 테이블 생성

  - 데이터 타입을 지정해야 한다

  ```sqlite
  CREATE TABLE 테이블이름 (열이름 데이터 타입, ... )
  ```

- SQL 문 실행

  - 코랩 환경에서
  - DB 커넷견 객체인 conn으로 커서 객체 생성 -> 이 커서 객체의 execute() 메서드에 SQL 문 전달

  ```python
  c = conn.cursor()
  c.execute("CREATE TABLE nslib_book \
            (name TEXT, author TEXT, borrow_count INTEGER)")
            
  # 데이터베이스 사용을 마칠 때 커서와 커넥션 객체를 명시적으로 닫아주는 것이 좋다
  # c.close()
  # conn.close()
  ```

  - 기존 테이블이 있다면 오류
    - IF NOT EXISTS 구문을 추가하면 기존 테이블이 없는 경우에만 생성

- 테이블 삭제

  ```python
  c.execute("DROP TABLE nslib_book")
  ```

- 데이터 추가

  - 작은 따옴표안에 작은 따옴표 같은 것을 해결하는 일이 번거롭다
    - 이를 신경쓰지 않기 위해 execute 메서드 사용

  ```python
  c.execute("INSERT INTO nslib_book (name,author,borrow_count) VALUES (?,?,?)", (row['도서명'], row['저자'], row['대출건수']))
  ```

- 데이터 읽기

  - SELECT 문으로 가져오는 테이블의 첫번째 행 출력

    - 튜플 형태로 반환
    - 한 번 더 실행 시 그 다음 행 가져옴

    ``` python
    c.fetchone()
    ```

  - 여러개 출력

    ```python
    c.fetchmany(n)
    ```

  - 모든행 출력

    ```python
    c.fetchall()
    ```

    

<hr>

- df.iterrows() 메서드
  - df 한 행씩 순환
  - index와 행 객체 반환



- df.to_sql(사용할 db 이름, db 커넥션 객체, if_exists=) 메서드
  - df의 내용을 db로 바로 저장
  - 열이름이 같다고 가정
  - if_exists 매개변수
    - 'fail' : 기본값, 지정된 테이블이 이미 있으면 오류
    - 'replace' : 테이블을 지우고 새로 만든 다음 데이터 추가
    - 'append' : 기존의 테이블에 데이터 추가
  - index 매개변수
    - False : df의 인덱스는 저장하지 않는다.



- pd.read_sql_query(쿼리, db 커넥션 객체)
  - 데이터베이스를 읽어 데이터프레임으로 만들기



## 데이터베이스에서 제공하는 함수로 통계량 구하기

```sql
# 행의 개수 세기
SELECT count(*) FROM nslib_book

# 행의 합
SELECT sum(borrow_count) FROM nslib_book

# 행의 평균
SELECT avg(borrow_count) FROM nslib_book

# 대출건수를 내림차순으로 10건
SELECT * FROM nslib_book ORDER BY borrow_count DESC LIMIT 10
```



<hr>

- 데이터베이스 정규화
  - 데이터가 가능한 한 중복되지 않도록 여러 테이블에 나누는 과정
    - 중복된 값을 바꿀 때 편하기 위해서
  - 정규화를 지원하는 데이터베이스 : 관계형데이터베이스(RDBMS)



- NoSQL
  - 비관계형 데이터베이스
  - 정규화가 어려운 비구조적인 데이터를 저장하는데 최적화되어 있으며 대용량 데이터를 다루는데 뛰어난 성능
  - 대표적으로 Redis, MongoDB, Cassandra

