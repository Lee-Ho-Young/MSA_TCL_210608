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
  
  
1-5. Vue 프로젝트를 SpringBoot 웹프로젝트의 화면으로 사용하고자 한다면 어떻게 해야할까?









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
