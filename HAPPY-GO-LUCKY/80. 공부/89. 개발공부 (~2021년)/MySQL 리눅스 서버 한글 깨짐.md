---
tags:
  - Mysql
Created: Invalid date
Updated: Invalid date
---
linux mysql 한글 깨짐 해결

[http://home.zany.kr:9003/board/bView.asp?bCode=18&aCode=2693](http://home.zany.kr:9003/board/bView.asp?bCode=18&aCode=2693)

데이터 베이스 생성시 인코딩 설정

CREATE DATABASE ‘share job’ /*!40100 DEFAULT CHARACTER SET utf8 COLLATE utf8_bin*/

인코딩 변경

ALTER DATABASE **sharejob** CHARACTER SET utf8 COLLATE utf8mb4_unicode_ci;

3mysql> `**charset utf8**`

인코딩 조회

`mysql> show variables like``'c%'``;`

해당 테이블 인코딩 확인

show full columns from em_smt_client;

각 테이블 인코딩 변경 방법

ALTER TABLE table_name convert to charset utf8;

---

**MySQL의 Procedure나 Function의 한글 깨짐 방지**

MySQL 에서 Stored procedure나 function 을 작성하는 경우,

가끔 Procedure나 Function body 부분에 한글이나 일본어와 같은 문자를 사용해야 하는 경우가 있다.

하지만, 가끔 이러한 Procedure나 Function을 실행 해보면 글자가 깨어지는 경우를 자주 볼 수 있다.

이러한 부분의 원인은 Procedure나 Function이 만들어 질 때부터 글자가 깨어져서 만들어 지는 경우가 상당히 많다.

가끔 그냥 놓치는 경우가 많지만,

MySQL client에서 Procedure나 Function 을 만들기 전에 여러가지 character set을 설정한 후

생성하면 이러한 문제점을 해결할 수 있다.

일반적으로 MySQL client를 실행하고, character set들을 확인해보면 아래와 같이 Latin1으로 설정된 경우가 상당히 많다.

root@localhost:test>show variables like '%char%';

+--------------------------+---------+

| Variable_name | Value |

+--------------------------+---------+

| character_set_client | latin1 |

| character_set_connection | latin1 |

| character_set_database | utf8 |

| character_set_filesystem | binary |

| character_set_results | latin1 |

| character_set_server | utf8 |

| character_set_system | utf8 |

+--------------------------+---------+

지금과 같은 상태에서 Procedure나 Function을 생성하면 Body내의 한글이나 일본어가 깨어져서 생성되게 된다.

이런 경우에는 **SET NAMES utf8;** 명령으로 character_set_connection, _client, _results 을 변경하고 Procedure나 Function 을 생성해 주면 된다.

그리고, 가끔 이렇게 정상적으로 생성되어도 글자가 깨어지는 경우에는 아래와 같이 리턴값의 Character set을 지정해주는 것도 방법이다.

create function getString() returns varchar(20) **CHARACTER SET UTF8**

---

5.5 이하

character_set_server=utf8

collation_server=utf8_general_ci

init_connect=set collation_connection=utf8_general_ci

init_connect=set names utf8

character-set-server=utf8

character-set-client-handshake = TRUE

mysql> show variables like 'c%';

+--------------------------+----------------------------+

| Variable_name | | Value |

+--------------------------+----------------------------+

| character_set_client | latin1 |

| character_set_connection | latin1 |

| character_set_database | latin1 |

| character_set_filesystem | binary |

| character_set_results | latin1 |

| character_set_server | latin1 |

| character_set_system | utf8 |

| character_sets_dir | /usr/share/mysql/charsets/ |

| collation_connection | latin1_swedish_ci |

| collation_database | latin1_swedish_ci |

| collation_server | latin1_swedish_ci |

| completion_type | 0 |

| concurrent_insert | 1 |

| connect_timeout | 10 |

+--------------------------+----------------------------+

14 rows in set (0.02 sec)

역시 latin1으로 되어있다.

명령어를 통해서도 mysql을 사용할때 변경 할 수 있지만, 이렇게 되면 데몬이 재실행 될때마다 다시 latin1으로 돌아간다. 따라서 고정적으로 바꿔주자.

**기본 케릭터 셋들을 원하는 값으로 변경 ( UTF-8 로 변경하였다 )**

**$ vi /etc/my.cnf**

[mysql]

default-character-set = utf8

[mysqld]

character-set-client-handshake=FALSE

init_connect="SET collation_connection = utf8_general_ci"

init_connect="SET NAMES utf8"

default-character-set = utf8

character-set-server = utf8

collation-server = utf8_general_ci

datadir=/var/lib/mysql

socket=/var/lib/mysql/mysql.sock

user=mysql

# Disabling symbolic-links is recommended to prevent assorted security risks

symbolic-links=0

[client]

default-character-set = utf8

[mysqldump]

default-character-set = utf8

[mysqld_safe]

log-error=/var/log/mysqld.log

pid-file=/var/run/mysqld/mysqld.pid

**그리고 재시작**

$ service mysqld restart

Stopping MySQL: [ OK ]

Starting MySQL: [ OK ]