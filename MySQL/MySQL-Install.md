MySQL
==========

## AWS에 MySQL 세팅하기 (yum)

1. yum 으로 mysql-server 설치

 ```bash
 sudo yum install mysql-server
 ```

2. mysqld 실행

 ```bash
 sudo service mysqld start
 ```

3. root 패스워드 변경

 ```bash
 /usr/bin/mysqladmin -u root password '패스워드'
 ```

4. 접속확인

 ```bash
 mysql -u root -p
 ```

5. 설정파일 복사

 ```bash
 sudo cp /usr/share/mysql/my-huge.cnf /etc/my.cnf
 ```

6. UTF8 인코딩 셋을 사용하기 위해 파일 내용 변경

 ```bash
 sudo vi /etc/my.cnf
 ```

 ```cnf
 [client]
 default-character-set = utf8

 [mysqld]
 init_connect = SET collation_connection = utf8_general_ci

 init_connect = SET NAMES utf8
 character-set-server = utf8
 collation-server = utf8_general_ci

 [mysqldump]
 default-character-set=utf8

 [mysql]
 default-character-set=utf8
 ```

7. 설정 변경 후 MySQL 재시작

 ```bash
 sudo service mysqld restart
 ```

8. 부팅시 자동시작 설정

 ```bash
 sudo chkconfig mysqld on
 chkconfig --list mysqld
 ```

9. 새로운 계정 만들기

 ```mysql
 mysql> grant all privileges on 데이터베이스이름.* to 사용자이름@localhost identified by '비밀번호' with grant  option;
 ```

 - 데이터베이스이름에 사용자이름을 prefix로 사용하고 싶을때!
  ```mysql
  mysql> GRANT ALL PRIVILEGES ON  `jaap\_%` . * TO  'jaap'@'localhost';
  ```

10. 새로운 유저로 접속하기

 ```bash
 mysql -u 사용자이름 -p
 ```
