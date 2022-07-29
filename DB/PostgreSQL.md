# PostgreSQL

## PostgreSQL 옵션
psql -U postgres 로그인

* USER 검색 
    *SELECT * FROM PG_SHADOW; 혹은 \du

ROLE	                     기능
SUPERUSER		USER들을 생성하고 권한을 부여해 주는 USER
CREATE ROLE		USER가 새로운 ROLE을 정의하는 기능을 생성
CREATE DB		USER가 DB를 생성하는 권한을 부여하는 기능
REPLICATION		USER가 DB를 실시간으로 복사하는 기능

======================================================
## postgreSQL 도커 설치 및 유저생성 + 테이블 생성

* docker run -p 5432:5432 --name postgres -e POSTGRES_PASSWORD=1q2w3e4r -d -v ~/data남겨놓을 경로:/var/lib/postgresql/data postgres

* docker exec -it postgres /bin/bash 

* CREATE USER [user_id] PASSWORD '[password]' [roleOption];	
  * ex) CREATE USER will PASSWORD '1q2w3e4r' SUPERUSER;
  
* CREATE DATABASE [database_name] OWNER [user_id];
  * ex) CREATE DATABASE willDataBase OWNER will;
  
* \c [database_name] [user_id]
  * ex) \c willDataBase will; 하면 will이라는 user로 willDataBase를 사용하겠다는 뜻 
  
* \dt : 현재 database 테이블 목록 보는 명령어

======================================================
## PostgreSQL 오라클과 차이

* 오라클에서 사용하는 LOGGING, PCTFREE, INITRANS, MAXTRANS, STORAGE(…), MONITORING는 사용하지 않음
* VARCHAR2 (Oracle) => varchar(PostgreSQL) VARCHAR타입으로 지정해도 내부적으로는 Character Varying으로 인식
* NUMBER(Oracle) => integer,bigint,NUMERIC(PostgreSQL) 
* BLOB(Oracle) => bytea(PostgreSQL)
* Date(Oracle) => timestamp(PostgreSQL) postgreSQL의 Date는 날짜만 저장 시간과 같이 저장하기위해 timestamp(숫자)사용 (숫자)는 초의 소수점자리수

======================================================
## UUID 자동생성하는 Insert문
* insert into [table_name] (id) values ((SELECT uuid_in(md5(random()::text || now()::text)::cstring)));