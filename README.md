# database

## oracle sql developer를 이용하여 사용자 추가
<br>classmanager 라는 유저를 생성하고 비밀번호는 classmanager로 만들고 기본 테이블스페이스는 'users' 임시 테이블스페이스는 'temp'로 만듦
``` sql
CREATE USER classmanager
IDENTIFIED by classmanager
DEFAULT TABLESPACE users
TEMPORARY TABLESPACE temp;
```

<br>classmanager라는 사용자에 권한 부여하기
<br>CONNECT라는 권한은 데이터베이스에 접속할 수 있는 권한
<br>RESOURCE라는 권한은 CREATE, ALTER, DROP, 등의 데이터베이스 객체를 조작할 수 있는 권한
<br>dba라는 권한은 데이터베이스의 모든 작업을 수행할 수 있는 최고 권한을 제공
``` sql
GRANT CONNECT to classmanager;
GRANT RESOURCE to classmanager;
GRANT dba to classmanager;
```

## classmanager로 성적DB라는 이름의 데이터베이스 접속 후 테이블 생성
![image](https://github.com/yeonjuyeong/database/assets/123055714/b26abcc1-3278-4a3c-9903-b194c50068b7)
<br>
<br>
<br> admin_table 테이블 생성
``` sql
CREATE TABLE admin_table(
    idx NUMBER(4) not NULL,
    admin_id VARCHAR2(50) not NULL,
    admin_pw VARCHAR2(50) not NULL
    );
```
<br>admin_table 테이블에 idx에 primary key를 주는 admin_idx_pk 라는 이름의 제약조건을 추가
``` sql
ALTER TABLE admin_table ADD( CONSTRAINT admin_idx_pk PRIMARY KEY(idx));
```

<br>  1부터 시작하여 값이 자동으로 증가하는 admin_idx_pk라는 시퀀스를 만들고 
``` sql
CREATE SEQUENCE admin_idx_pk START WITH 1;
```

<br> admin_table 테이블에 idx(값이 자동으로 생성), admin_id, admin_pw 열에 해당하는 값을 삽입하는 작업을 수행합니다.
``` sql
INSERT INTO admin_table (idx, admin_id, admin_pw) VALUES ( admin_idx_pk.nextval, 'moon', 'soyun');
```

<br>grade_table 테이블 생성
``` sql
CREATE TABLE grade_table(
    idx NUMBER(4) not NULL,
    num NUMBER(5) not NULL,
    name VARCHAR2(20) not NULL,
    sub1 VARCHAR2(20) not NULL,
    score1 NUMBER(3) not NULL,
    sub2 VARCHAR2(20) not NULL,
    score2 NUMBER(3) not NULL,
    sub3 VARCHAR2(20) not NULL,
    score3 NUMBER(3) not NULL,
    total NUMBER(3) not NULL,
    avg NUMBER(3) not NULL
    );
```

<br>grade_table 테이블에 idx에 primary key를 주는 user_idx_pk 라는 이름의 제약조건을 추가
``` sql
ALTER TABLE grade_table ADD( CONSTRAINT user_idx_pk PRIMARY KEY(idx));
```

<br>grade_table 테이블에 idx(값이 자동으로 생성), num, name, sub1, score1, sub2, score2, sub3, score3, total, avg 열에 해당하는 값을 삽입하는 작업을 수행합니다.
``` sql
INSERT INTO grade_table (idx, num, name, sub1, score1, sub2, score2, sub3, score3, total, avg)
 VALUES ( admin_idx_pk.nextval, 21110, 'yeonjuyeong', '국어', 88, '영어', 50, '한국사', 12, 150,50);
```
