<div>

<div># 본 mysql은 8.0버젼이 아닌 5.7 버젼 입니다.  </div>

<div># 5.7 stable 버전 다운 위해서 깃허브에서 클론해오깅 .. mysql 사이트 이런데서 말구 ..</div>

<div># clone 해오면 브랜치는 기본저긍로 8.0으로 되어 있을 것이기 때문에 git checkout으로 5.7로 옮겨가자.  </div>

<div><참고 사이트></div>

<div>[http://bluexmas.tistory.com/631](http://bluexmas.tistory.com/631)  : 요게 우리 상황이랑 가장 적합함.   (걍 이거 따라하고 아래는 참고 용)</div>

<div><소스 코드를 통해 MySQL 설치하기></div>

<div>1\. 다운로드 받고, 압축 풀기</div>

<div>     cd [wanted directory] # 보통 home 하위 디렉토리에 지정</div>

<div>     wget [download link]</div>

<div>     tar -xvf [name]</div>

<div>     cd [extracted directory]</div>

<div>     #현재 디렉토리는 압축이 풀려진 mysql 코드. 예를 들어 /mysql-5.7.24/</div>

<div>2\. 필요한 라이브러리 설치하기</div>

<div>      apt-get install build-essential cmake libreadline6-dev libncurses5-dev</div>

<div>     + 추가적으로 'boost' 를 반드시 설치해야한다.  </div>

<div>     본인이 알아서 설치하면 됨.  </div>

<div>     인터넷에서 boost_1_67_0 받아서 압축 풀고 설치하기 (mysql 5.7은 boost 67임)</div>

<div>     (나는 원래 그   <span style="box-sizing: border-box; font-size: 14px; letter-spacing: normal; orphans: 2; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; background-color: rgb(255, 255, 255); color: rgb(255, 221, 221); font-family: Monaco; font-stretch: normal; font-variant: no-common-ligatures; line-height: normal;">-DDOWNLOAD_BOOST</span><span style="box-sizing: border-box; font-size: 14px; letter-spacing: normal; orphans: 2; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; background-color: rgb(255, 255, 255); color: rgb(236, 236, 21); font-family: Monaco; font-stretch: normal; font-variant: no-common-ligatures; line-height: normal;">=</span><span style="box-sizing: border-box; font-size: 14px; letter-spacing: normal; orphans: 2; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; background-color: rgb(255, 255, 255); color: rgb(255, 60, 255); font-family: Monaco; font-stretch: normal; font-variant: no-common-ligatures; line-height: normal;">1</span><span style="font-size: 14px; letter-spacing: normal; orphans: 2; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; color: rgb(51, 51, 51); font-family: -apple-system, BlinkMacSystemFont, &quot;Segoe UI&quot;, Roboto, Oxygen, Ubuntu, Cantarell, &quot;Fira Sans&quot;, &quot;Droid Sans&quot;, &quot;Helvetica Neue&quot;, sans-serif; font-variant-caps: normal; font-variant-ligatures: normal;">  </span><span style="box-sizing: border-box; font-size: 14px; letter-spacing: normal; orphans: 2; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; color: rgb(255, 221, 221); font-family: Monaco; font-variant-caps: normal; font-variant-ligatures: no-common-ligatures;">-DWITH_BOOST</span><span style="box-sizing: border-box; font-size: 14px; letter-spacing: normal; orphans: 2; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; color: rgb(236, 236, 21); font-family: Monaco; font-variant-caps: normal; font-variant-ligatures: no-common-ligatures;">=</span><span style="box-sizing: border-box; font-size: 14px; letter-spacing: normal; orphans: 2; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; color: rgb(0, 0, 0); font-family: Monaco; font-variant-caps: normal; font-variant-ligatures: no-common-ligatures;">/usr/</span><span style="box-sizing: border-box; font-size: 14px; letter-spacing: normal; orphans: 2; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; background-color: rgb(255, 255, 255); color: rgb(236, 236, 21); font-family: Monaco; font-stretch: normal; font-variant: no-common-ligatures; line-height: normal;">local</span><span style="box-sizing: border-box; font-size: 14px; letter-spacing: normal; orphans: 2; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; color: rgb(0, 0, 0); font-family: Monaco; font-variant-caps: normal; font-variant-ligatures: no-common-ligatures;">/src/boost_1_59_0 이 두 옵션 주고 하려했는데</span></div>

<div><span style="box-sizing: border-box; font-size: 14px; letter-spacing: normal; orphans: 2; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; color: rgb(0, 0, 0); font-family: Monaco; font-variant-caps: normal; font-variant-ligatures: no-common-ligatures;">     걍 미리 다운 받아두는게 정신건강에 좋음)</span></div>

<div><span style="box-sizing: border-box; font-size: 14px; letter-spacing: normal; orphans: 2; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; color: rgb(0, 0, 0); font-family: Monaco; font-variant-caps: normal; font-variant-ligatures: no-common-ligatures;">     그리고 다운 받아놔도 권한 때문에 실패할 수도 있어서</span></div>

<div><span style="box-sizing: border-box; font-size: 14px; letter-spacing: normal; orphans: 2; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; color: rgb(0, 0, 0); font-family: Monaco; font-variant-caps: normal; font-variant-ligatures: no-common-ligatures;">     미리미리 sudo chmod 777 boost 로 바꿔두자 ................이거때매 빌드를 세번을 했다.  </span></div>

<div>     + bison도 설치하자. (sudo apt install bision)</div>

<div>3\. CMAKE 하기</div>

<div>     이게 제일 까다롭고 에러가 많이 나는 부분이다.</div>

<div>     옵션으로 주는 부분에서 경로 지정을 많이 해야하기 때문.  </div>

<div>     다만, CMAKE는 실패하면 바로 뭐가 틀렸는지 뜨고 실패하기 때문에 바로 고치면 되긴 한다.  </div>

<div>     configuration file인 my.cnf의 경우 home 아래로 지정하자.  </div>

<div>     아래는 내가 사용한 CMAKE 옵션들이고, 각자 뭔 역할을 하는지 살펴보자.  </div>

<div style="box-sizing: border-box; padding: 8px; font-family: Monaco, Menlo, Consolas, &quot;Courier New&quot;, monospace; font-size: 12px; color: rgb(51, 51, 51); border-radius: 4px; background-color: rgb(251, 250, 248); border: 1px solid rgba(0, 0, 0, 0.15);-en-codeblock:true;">

<div>cmake \</div>

<div>DCMAKE_INSTALL_PREFIX=/home/kyungmin/MySQL/workspace \     #실제 설치가 되는 부분</div>

<div>DMYSQL_DATADIR=/home/kyungmin/MySQL/data \     #데이터 및 로그가 기록되는 부분</div>

<div>DENABLED_LOCAL_INFILE=1 \</div>

<div>DDEFAULT_CHARSET=utf8 \</div>

<div>DDEFAULT_COLLATION=utf8_general_ci \</div>

<div>DMYSQL_UNIX_ADDR=/tmp/mysql.sock \     #소켓 저장 위치</div>

<div>DMYSQL_TCP_PORT=3306 \     #포트번호</div>

<div>DSYSCONFDIR=/home/kyungmin/MySQL/config \     #본인의 my.cnf를 어디다 저장할 것인지</div>

<div>DWITH_EXTRA_CHARSETS=all \</div>

<div>DWITH_INNOBASE_STORAGE_ENGINE=1 \</div>

<div>DWITH_ARCHIVE_STORAGE_ENGINE=1 \</div>

<div>DDOWNLOAD_BOOST=1 \</div>

<div>DWITH_BOOST=../boost_1_59_0     #반드시 필요한 boost의 압축 푼 파일</div>

</div>

1.  <div style="margin-top: 0pt; margin-bottom: 8pt;">

    <div><span style="font-size: 11pt; color: rgb(1, 1, 1);">DCMAKE_INSTALL_PREFIX: compile result directory</span></div>

    </div>

2.  <div style="margin-top: 0pt; margin-bottom: 8pt;">

    <div><span style="font-size: 11pt; color: rgb(1, 1, 1);">DMYSQL_DATADIR: data loading directory</span></div>

    </div>

3.  <div style="margin-top: 0pt; margin-bottom: 8pt;">

    <div><span style="font-size: 11pt; color: rgb(1, 1, 1);">DSYSCONFDIR: your own mysql.cnf or my.cnf</span></div>

    </div>

4.  <div><span style="font-size: 11pt; text-align: justify; text-indent: 0pt; color: rgb(1, 1, 1);-en-paragraph:true;">DWITH_BOOST: boost source director</span><span style="font-size: 11pt; text-align: justify; text-indent: 0pt; color: rgb(1, 1, 1); font-family: Cambria; line-height: 108%;-en-paragraph:true;">y</span></div>

<div>4\. make</div>

<div>     make</div>

<div>     make test</div>

<div>     sudo make install</div>

<div>     을 차례로 하면 되는데, 참고할 사항 두개</div>

<div>     - make 할때 nproc를 통해 cpu개수를 미리 알아두자</div>

<div>     만약에 결과 값이 8이면 make -j8로 하면 훨씬 빠름</div>

<div>     - make install할 때 반드시 sudo를 붙이자.  </div>

<div>5\. my.cnf</div>

<div>     : 원래는 my.cnf가 위에서 지정한 DSYCONFIDIR 위치에 자동적으로 저장이 되어야 하는데,  </div>

<div>     내가 했을 때는 안그랬음 .. . .</div>

<div>     그래서 한 방법은 종혁이 형이 주신 my.cnf를 가져와서 config에 넣은 다음에 내 상황에 맞게 고친거!</div>

<div>![](MySQL%205.7.24%20%EC%84%A4%EC%B9%98%20%EC%9D%BC%EA%B8%B0.html.resources/F0E20377-2023-42F4-9BB0-70695D64E71C.png)</div>

<div>  이 세가지 였는데,  </div>

<div>위에 두개는 처음에 cmake할 때랑 같은 애고,  </div>

<div>마지막에는 새로 지정해 줬다.  </div>

<div>근데 문제는 InnoDB는 자기가 알아서 폴더를 못만들기 때문에 만들어 주고 실행해야함 !</div>

<div>6\. mysql.server 고치기  </div>

<div>      블로그를 보면  </div>

<div style="box-sizing: border-box; padding: 8px; font-family: Monaco, Menlo, Consolas, &quot;Courier New&quot;, monospace; font-size: 12px; color: rgb(51, 51, 51); border-radius: 4px; background-color: rgb(251, 250, 248); border: 1px solid rgba(0, 0, 0, 0.15);-en-codeblock:true;">

<div>sudo cp /usr/local/mysql/support-files/mysql.server /etc/init.d/mysqld</div>

</div>

<div>이렇게 옮기고 나서 고치는 부분이 있는데,  </div>

<div>우리가 고쳐야 할 것은 중간에  </div>

<div>basedir / datadir밖에 없다.  </div>

<div>얘도 cmake할 때 지정해둔 path로 동일하게 하면 됨.</div>

<div>7\. 실행 및 확인하기</div>

<div>     mysql이 빌드 된 폴더에 들어가면 /bin 폴더가 있을 것.  거기 들어가서  </div>

<div style="box-sizing: border-box; padding: 8px; font-family: Monaco, Menlo, Consolas, &quot;Courier New&quot;, monospace; font-size: 12px; color: rgb(51, 51, 51); border-radius: 4px; background-color: rgb(251, 250, 248); border: 1px solid rgba(0, 0, 0, 0.15);-en-codeblock:true;">

<div>./mysqld_safe --defaults-file=/path/to/my.cnf --skip-grant-tables &</div>

</div>

<div>(뒤에 반드시 & 붙여서 백그라운드에서 실행되고 있도록 만들기)</div>

<div>한 터미널 창에서 저렇게 실행했을 때 바로 안꺼지고 버티는 상태에서</div>

<div>다른 터미널 창 열어서  </div>

<div style="box-sizing: border-box; padding: 8px; font-family: Monaco, Menlo, Consolas, &quot;Courier New&quot;, monospace; font-size: 12px; color: rgb(51, 51, 51); border-radius: 4px; background-color: rgb(251, 250, 248); border: 1px solid rgba(0, 0, 0, 0.15);-en-codeblock:true;">

<div>ps -al | grep mysql</div>

</div>

<div>했을 때 있으면 된거.  </div>

<div>그 터미널 창에서  </div>

<div style="box-sizing: border-box; padding: 8px; font-family: Monaco, Menlo, Consolas, &quot;Courier New&quot;, monospace; font-size: 12px; color: rgb(51, 51, 51); border-radius: 4px; background-color: rgb(251, 250, 248); border: 1px solid rgba(0, 0, 0, 0.15);-en-codeblock:true;">

<div>./mysqladmin shutdown</div>

</div>

<div>했을 때 꺼진 것처럼 문구가 ended 하고 나오면 성공.  </div>

<div>-----</div>

<div>troubleshooting</div>

<div>1\. my.cnf가 안생긴다 ?</div>

<div>: mysql에서 제공하는 기본 innodb cnf파일 이용 / 종혁이 형이 주신 파일 이용</div>

<div>2\. innodb log 폴더가 안만들어진다 ?</div>

</div>

<div>: 미리 만들어 두기</div>

<div>3\. 로그를 열심히 보자.</div>

<div>: data안에 본인컴퓨터.err 파일이 만들어 질텐데, 여기에 상세히 [ERROR]라고 나와있다.  </div>

<div>가끔 가다 보면 폴더나 파일을 못 만들거나 못 열겠다는 경우가 있는데,</div>

<div>이건 퍼미션 문제기 때문에 나는 걍 sudo chown 777 ? 로 해결했다.  </div>