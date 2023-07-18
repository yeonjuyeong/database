# database

## oracle sql developer를 이용하여 사용자 추가
<br>classmanager 라는 유저를 생성하고 비밀번호는 classmanager로 만들고 기본 기본 테이블스페이스는 'users' 임시 테이블스페이스는 'temp'로 만듦
``` sql
CREATE USER classmanager
IDENTIFIED by classmanager
DEFAULT TABLESPACE users
TEMPORARY TABLESPACE temp;
```

<br>classmanager라는 사용자에 권한 부여하기
``` sql
GRANT CONNECT to classmanager;//이 권한은 데이터베이스에 접속할 수 있는 권한
GRANT RESOURCE to classmanager;//이 권한은 CREATE, ALTER, DROP, 등의 데이터베이스 객체를 조작할 수 있는 권한
GRANT dba to classmanager;//데이터베이스의 모든 작업을 수행할 수 있는 최고 권한을 제공
```

## classmanager로 성적DB라는 이름의 데이터베이스 접속 후 테이블 생성
![image](https://github.com/yeonjuyeong/database/assets/123055714/b26abcc1-3278-4a3c-9903-b194c50068b7)
<br> 테이블 생성
```sql
CREATE TABLE admin_table(
    idx NUMBER(4) not NULL,
    admin_id VARCHAR2(50) not NULL,
    admin_pw VARCHAR2(50) not NULL
    );
```
<br> 테이블에 idx에 primary key를 주는 admin_idx_pk 라는 이름의 제약조건을 추가
```sql
ALTER TABLE admin_table ADD( CONSTRAINT admin_idx_pk PRIMARY KEY(idx));
```

```sql
CREATE SEQUENCE admin_idx_pk START WITH 1;
```

```sql
INSERT INTO admin_table (idx, admin_id, admin_pw) VALUES ( admin_idx_pk.nextval, 'moon', 'soyun');
```
