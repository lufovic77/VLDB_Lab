# https://github.com/Percona-Lab/tpcc-mysql 

#TPC-C 설치는 생각보다 순조로웠다.  

#그냥 tpcc-mysql 깃허브 readme대로 따라하면 됨. 



## 1. /etc/profile 수정하기 

​    지금까지 설치한 mysql을 전역에서 사용하기 위해선 해당 파일을 수정해야 한다.  

​    vim /etc/profile 한 후 아래 네개를 추가하면 됨 

```bash
export MYSQL_HOME=/home/kyungmin/MySQL/workspace #사람마다 다를거 
export C_INLUDE_PATH=$MYSQL_HOME/include      
export LD_LIBRARY_PATH=$MYSQL_HOME/lib 
export PATH=MYSQL_HOME/bin:$PATH 
```

짬을 내서 쉘 스크립트 개념에 대해 설명하면  

$PATH 이런거는 변수를 의미한다.  

근데 이게 선언을 할때는 $를 붙이지 않고 사용하다가  

그 변수를 가져다 사용할 떄는 $를 붙여서 쓴다.  



예를 들어 첫 번째 줄에서 MYSQL_HOME을 선언할 때는 $를 붙이지 않는다. 

근데 두번째 줄에서 가져다 쓸때는 $MYSQL_HOME이라고 붙이는데,  

이는 결국 /home/kyungmin/MySQL/workspace/include를 의미한다! 



## 2. 다운받고 압축 풀기 

(얘는 걍 git clone만 하면 끝) 



## 3. source /etc/profile하기    

​    저렇게 치면 커맨드 라인의 색이 바뀔 것이다.  

​    저걸 쳐야만 4번이 진행됨. 안치고 하면 에러 뿜으면서 실행이 안됨. 



## 4. src 폴더로 들어가서 make하기  

​    리드미에 나와 있듯이 mysql_config가 $PATH에 들어 있어야 한다고 하는데,  

​    1번에서 정리한 개념을 적용하면 $PATH는 결국 

​    workspace안의 bin 폴더일 것이다. 그 안에 mysql_config가 있는지를 살펴보면 됨! 

​     

## 5. 그 다음부터는 걍 리드미가 하란대로 따라하면 됨. 



------------------------



## 주의 할 점 

tpcc_load -h127.0.0.1 -d tpcc1000 -u root -p "" -w 1000 

나는 이거 똑같이 따라했는데, warehouse를 너무 높게 잡았다.  

warehouse 1이 약 100MB이기 때문에, 1000이면 130GB..? 

그래서 막판 가서 아예 컴터가 멈췄음. 



./tpcc_start -h127.0.0.1 -P3306 -dtpcc1000 -uroot -w1000 -c32 -r10 -l10800 

얘도 같은데, 일단 -dtpcc1000 -w1000뒤의 숫자는 같이 맞춰줘야함.  

그리고 -c32도 클라이언트 수인데, 데모 할 때는 줄여서 하자 