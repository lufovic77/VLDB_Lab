\# 본 mysql은 8.0버젼이 아닌 5.7 버젼 입니다.  

\# 5.7 stable 버전 다운 위해서 깃허브에서 클론해오깅 .. mysql 사이트 이런데서 말구 ..

\# clone 해오면 브랜치는 기본적으로 8.0으로 되어 있을 것이기 때문에 git checkout으로 5.7로 옮겨가자.  

<참고 사이트>

[<http://bluexmas.tistory.com/631](http://bluexmas.tistory.com/631)>  : 요게 우리 상황이랑 가장 적합함.   (걍 이거 따라하고 아래는 참고 용)

**<소스 코드를 통해 MySQL 설치하기>**

1. **다운로드 받고, 압축 풀기**

​     `cd [wanted directory] # 보통 home 하위 디렉토리에 지정`

​     wget [download link]

​     tar -xvf [name]

​     `cd [extracted directory]` 

​     \#현재 디렉토리는 압축이 풀려진 mysql 코드. 예를 들어 /mysql-5.7.24/

2. **필요한 라이브러리 설치하기**

​      `apt-get install build-essential cmake libreadline6-dev libncurses5-dev`

​     \+ 추가적으로 'boost' 를 반드시 설치해야한다.  

​     본인이 알아서 설치하면 됨.  

​     인터넷에서 boost_1_67_0 받아서 압축 풀고 설치하기 (mysql 5.7은 boost 67버젼이 적합하다)

​     (나는 원래 그   -DDOWNLOAD_BOOST=1  -DWITH_BOOST=/usr/local/src/boost_1_59_0 이 두 옵션 주고 하려했는데

​     걍 미리 다운 받아두는게 정신건강에 좋음)

​     그리고 다운 받아놔도 권한 때문에 실패할 수도 있어서

​     미리미리 sudo chmod 777 boost 로 바꿔두자 ................이거때매 빌드를 세번을 했다.  

​     \+ bison도 설치하자. (sudo apt install bision)

3\. **CMAKE 하기**

​     이게 제일 까다롭고 에러가 많이 나는 부분이다.

​     옵션으로 주는 부분에서 경로 지정을 많이 해야하기 때문.  

​     다만, CMAKE는 실패하면 바로 뭐가 틀렸는지 뜨고 실패하기 때문에 바로 고치면 되긴 한다.  

​     configuration file인 my.cnf의 경우 home 아래로 지정하자.   (해당 cnf 파일은 mysql이 사이트에서 제공하는 파일을 사용해도 문제는 없다)

​     아래는 내가 사용한 CMAKE 옵션들이고, 각자 뭔 역할을 하는지 살펴보자.  

`cmake \`

`DCMAKE_INSTALL_PREFIX=/home/kyungmin/MySQL/workspace \     #실제 설치가 되는 부분`

`DMYSQL_DATADIR=/home/kyungmin/MySQL/data \     #데이터 및 로그가 기록되는 부분`

`DENABLED_LOCAL_INFILE=1 \`

`DDEFAULT_CHARSET=utf8 \`

`DDEFAULT_COLLATION=utf8_general_ci \`

`DMYSQL_UNIX_ADDR=/tmp/mysql.sock \     #소켓 저장 위치`

`DMYSQL_TCP_PORT=3306 \     #포트번호`

`DSYSCONFDIR=/home/kyungmin/MySQL/config \     #본인의 my.cnf를 어디다 저장할 것인지`

`DWITH_EXTRA_CHARSETS=all \`

`DWITH_INNOBASE_STORAGE_ENGINE=1 \`

`DWITH_ARCHIVE_STORAGE_ENGINE=1 \`

`DDOWNLOAD_BOOST=1 \`

`DWITH_BOOST=../boost_1_59_0     #반드시 필요한 boost의 압축 푼 파일`

1. DCMAKE_INSTALL_PREFIX: compile result directory
2. DMYSQL_DATADIR: data loading directory
3. DSYSCONFDIR: your own mysql.cnf or my.cnf
4. DWITH_BOOST: boost source directory

4\. make

​     `make`

​     make test

​     sudo make install

​     을 차례로 하면 되는데, 참고할 사항 두개

​     \- make 할때 nproc를 통해 cpu개수를 미리 알아두자

​     만약에 결과 값이 8이면 make -j8로 하면 훨씬 빠름

​     \- make install할 때 반드시 sudo를 붙이자.  

5\. my.cnf

​     : 원래는 my.cnf가 위에서 지정한 DSYCONFIDIR 위치에 자동적으로 만들어져야 하는데,  

​     내가 했을 때는 안그랬음 .. . .

​     그래서 한 방법은 종혁이 형이 주신(혹은 인터넷에 돌아다니는 표준 cnf 파일들) my.cnf를 가져와서 config에 넣은 다음에 내 상황에 맞게 고친거!

6\. mysql.server 고치기  

​      블로그를 보면  

`sudo cp /usr/local/mysql/support-files/mysql.server /etc/init.d/mysqld`

이렇게 옮기고 나서 고치는 부분이 있는데,  

우리가 고쳐야 할 것은 중간에  

basedir / datadir밖에 없다.  

얘도 cmake할 때 지정해둔 path로 동일하게 하면 됨.

7\. 실행 및 확인하기

​     mysql이 빌드 된 폴더에 들어가면 /bin 폴더가 있을 것.  거기 들어가서  

`./mysqld_safe --defaults-file=/path/to/my.cnf --skip-grant-tables &`

(뒤에 반드시 & 붙여서 백그라운드에서 실행되고 있도록 만들기)

한 터미널 창에서 저렇게 실행했을 때 바로 안꺼지고 버티는 상태에서

다른 터미널 창 열어서  

ps -al | grep mysql

했을 때 있으면 된거.  

그 터미널 창에서  

`./mysqladmin shutdown`

했을 때 꺼진 것처럼 문구가 ended 하고 나오면 성공.  

\-----

troubleshooting

1\. my.cnf가 안생긴다 ?

: mysql에서 제공하는 기본 innodb cnf파일 이용 / 종혁이 형이 주신 파일 이용

2\. innodb log 폴더가 안만들어진다 ?

: 미리 만들어 두기

3\. 로그를 열심히 보자.

: data안에 본인컴퓨터.err 파일이 만들어 질텐데, 여기에 상세히 [ERROR]라고 나와있다.  

가끔 가다 보면 폴더나 파일을 못 만들거나 못 열겠다는 경우가 있는데,

이건 퍼미션 문제기 때문에 나는 걍 sudo chown 777 ? 로 해결했다.  