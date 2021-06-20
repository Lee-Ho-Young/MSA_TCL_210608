<MSA Advanced TCL 목표>

1. Vue.js[DevExtreme] - Github - Nginx - SpringBoot - MariaDB를 활용한 웹 대시보드 구축

https://amanokaze.github.io/blog/SB-VJ-PS-Setting/
https://github.com/jonashackt/spring-boot-vuejs [Vue / SpringBoot 분리]
https://mr-spock.tistory.com/3 [Vue를 SpringBoot 프로젝트 안으로]

<2021-06-13>
* vue3 버전으로 DevExtreme vue-dashborad 프로젝트를 C:\Develop 디렉토리에 생성
* 


1-1. vue.js 설치하기
   -- 기본적으로는 JQuery와 유사하게 <script></script> 구문 추가로 사용 가능
   -- npm을 활용한 설치 지원
     -- node package manger : node.js에서 활용하는 모듈들을 패키지로 만들어 관리
     -- npm의 경우 node.js를 설치하면 포함되어 있음
     -- node.js 공식 웹사이트에서 Windows 10 64bit 전용 설치파일을 깔자 [node-v14.17.0-x64.msi]
     -- 설치가 완료된 후 powerShell 화면에서 npm -v 명령어로 설치된 npm 버전을 확인할 수 있다.
     -- npm을 사용하여 vue.js 설치
        $ npm install -g vue-cli
     -- 환경변수 등을 모두 확인해 보아도, vue 명령어가 실행이 안 된다.
     -- 환경변수 설정 후 powershell이 아닌 cmd에서는 잘 실행됨 [이상하네..]
       
1-2. vue 프로젝트 생성 [Vue3 활용할 계획]
  -- webpack 패키지를 활용하여 my-project를 생성한다.
  -- $ vue init webpack my-project
  -- 이상한 팅을 오지게 물어보고 설치해줌
  -- 설치 마지막에 안내문구 :
     To get started: 
      cd my-project
      npm run dev
  -- 2개의 명령어를 실행하면 "Your application is running here: http://localhost:8080" 이라고 뜬다.
  -- 웹화면을 확인할 수 있다.

 
1-3. DevExtreme 활용해 보기
  -- Installing DevExtreme CLI
     $ npm i -g devextreme-cli
  -- Create a new DevExtreme Vue application that uses the DevExtreme layout template:
     [vue-dashboard 이름을 갖는 vue-app을 생성, 현재 디렉토리에 생성되는 것 같으니 주의필요]
     $ devextreme new vue-app vue-dashboard
  -- 프로젝트 렉토리에 들어가서 'npm run serve' 실행
     $ C:\Users\rich>cd vue-dashboard
     $ npm run serve
  -- 병신같은 경로에 만들어진 프로젝트를 다른 곳에 사용하자.
  -- DevExtreme을 활용하여 프로젝트를 만들었다면, DevExtreme에서 제공하는 샘플UI를 담은 Vue프로젝트일 뿐이다.


1-4. vue 개발환경 [Visual Studio Code 설치]
  -- javascript framework인데, 별도의 개발환경이 필요한 것일까?
  -- 온라인에서는 보통 VScode 프로그램을 사용하여 화면을 개발하고 있다.
     -- 화면개발 내용에 대한 즉각적인 확인 및 코드에 대한 tip 확인이 가능하다.

  -- https://code.visualstudio.com/ 접속
  -- 설치버전으로 할 경우 다양한 가이드에서 처럼 cmd창에서 code 명령어로 프로젝트 오픈이 가능할 것
  -- zip버전으로 사용해도 vue-dashboard 프로젝트 폴더를 오픈할 경우 동일하게 사용이 가능하다.
  -- VSCode에서 Vetur Extention을 설치해 준다. [아직 뭔지는 모름]
  -- VSCode에서 제공하는 cmd터미널을 통해 Vue프로젝트가 로컬에 뜨는 것을 확인하였다.
  
  
1-5. MariaDB 세팅
  -- 간단하게 Docker 환경에 올리자
  -- 테스트 환경인 Windows Docker에서 실행하기 위해서는 아래와 같이 진행한다.
  -- cmd창에서
     -- $ docker pull mariadb
     -- $ docker run --name mariadb -d -p 3306:3306 -e MYSQL_ROOT_PASSWORD=mariadb mariadb
     -- $ docker ps [Maridb 컨테이너 확인가능]
       -- $ mysql -u root -p [Maridb를 CMD창에서 바로 접속 가능]
       -- $ docker exec -it mariadb /bin/bash
          $ mysql -u root -p [Mariadb를 컨테이너 내부에서 접속 가능]
          
     -- 컨테이너에 설치한 Mariadb 설정
        -- 컨테이너 환경에서는 VI에디터가 깔려있지 않다. 먼저 깔아주자
           -- $ apt-get update && apt-get install nano vim
        -- Mariadb 설정파일을 수정해 주자
           -- $ vi /etc/mysql/my.cnf
           -----------------------------------------
            [client]
            default-character-set = utf8mb4

            [mysql]
            default-character-set = utf8mb4

            [mysqld]
            character-set-client-handshake = FALSE
            character-set-server = utf8mb4
            collation-server = utf8mb4_unicode_ci
           -----------------------------------------
        -- Mariadb 컨테이너 재시작
        $ docker restart mariadb
        -- DBeaver 툴을 활용해 연결상태 확인
           -- Server Host : localhost [3306]
           -- username, password 입력 후 연결 확인
        -- 테스트로 database를 생성 [https://jdm.kr/blog/132]
            $ create database test;
            $ create user 'test'@'%' identified by 'test';
            $ grant all privileges on test.* to 'test'@'%';
            $ flush privileges;
        -- DBeaver 툴에서 test 데이터 베이스에 대해 id/pass(test/test) 값으로 접속되는지 확인
           $ show databases; 
           $ use test;
           $ show tables; [아직 아무런 테입블이 없다.]
           $ create table user_info (user_id varchar(10), user_name varchar(20), hand_phone varchar(20));
           $ select * from user_info [아직 테이블에 데이터가 1건도 없다.]
           $ insert into user_info(user_id, user_name, hand_phone) values('09340', '이호영', '010-0000-0000');
           $ insert into user_info(user_id, user_name, hand_phone) values('09275', '박정수', '010-0000-0000');
           $ insert into user_info(user_id, user_name, hand_phone) values('09341', '누구쇼', '010-0000-0000');
        -- 지금까지 vue.js -> api -> db를 통해 확인할 테스트 데이터를 생성해 보았다.

------------------------------------------------------------------------------------------
PS C:\Users\rich> npm -v
6.14.13
PS C:\Users\rich> npm install vue
npm WARN saveError ENOENT: no such file or directory, open 'C:\Users\rich\package.json'
npm notice created a lockfile as package-lock.json. You should commit this file.
npm WARN enoent ENOENT: no such file or directory, open 'C:\Users\rich\package.json'
npm WARN rich No description
npm WARN rich No repository field.
npm WARN rich No README data
npm WARN rich No license field.

+ vue@2.6.14
added 1 package from 1 contributor and audited 1 package in 1.225s
found 0 vulnerabilities
------------------------------------------------------------------------------------------

------------------------------------------------------------------------------------------
C:\WINDOWS\system32>vue init webpack my-project

? Project name my-project
? Project description A Vue.js project
? Author lee
? Vue build standalone
? Install vue-router? Yes
? Use ESLint to lint your code? Yes
? Pick an ESLint preset Standard
? Set up unit tests Yes
? Pick a test runner jest
? Setup e2e tests with Nightwatch? Yes
? Should we run `npm install` for you after the project has been created? (recommended) npm

   vue-cli · Generated "my-project".


# Installing project dependencies ...
# ========================
------------------------------------------------------------------------------------------


2. 웹 대시보드 App.에 대한 MSA 패턴 전환

3. MSA App. / MariaDB를 AWS 상에 구축
