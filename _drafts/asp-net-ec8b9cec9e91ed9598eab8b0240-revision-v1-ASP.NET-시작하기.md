---
id: 825
title: ASP.NET 시작하기
date: 2019-04-21T15:03:41+09:00
author: yongjin0802
layout: revision
guid: https://yongj.in/2019/04/21/240-revision-v1/
permalink: /2019/04/21/240-revision-v1/
---
<div>
  https://docs.microsoft.com/en-us/aspnet/core/tutorials/first-mvc-app/start-mvc
</div>

<div>
</div>

<div>
  .Net Core를 설치하고
</div>

<div>
</div>

<div>
  firstapp이라는 디렉토리를 만들고
</div>

<div>
</div>

<div>
  터미널에서 dotnet new mvc를 치면 프로젝트가 하나 생성된다.
</div>

<div>
</div>

<div>
  생성된 파일을 살펴보면 이러하다.
</div>

<div>
</div>

<div>
  <strong>Startup.cs</strong> : Startup Class를 포함하고 있으며, 이 앱으로 오는 모든 요청을 처리하는 Request pipeline을 설정할 수 있다.
</div>

<div>
</div>

<div>
  <strong>Program.cs</strong> : Program Class를 포함하고 있으며, 앱의 Main 함수 시작하는 지점임
</div>

<div>
</div>

<div>
  <strong>firstapp.csproj</strong> : <a href="http://ASP.NET">ASP.NET</a> 프로젝트 포멧을 담고있고, 패키지 추가같은 프로젝트 설정을 할 수 있음
</div>

<div>
</div>

<div>
  <strong>appsettings.json / appsettings.Development.json</strong> : 앱의 환경 설정을 할 수 있음. 로그남기는 정도 등등
</div>

<div>
</div>

<div>
  <strong>bower.json</strong> : Bower(소프트웨어 시스템 매니저) 패키지의 의존성 표시
</div>

<div>
</div>

<div>
  <strong>.bowerrc</strong> : Bower 설정 파일인데, 패키지 다운로드 받으면 어디에 설치할 건지 설정함
</div>

<div>
</div>

<div>
  <strong>bundleconfig.json</strong> : 프론트 엔드인 자바스크립트나 CSS 묶는 설정 파일임
</div>

<div>
</div>

<div>
  <strong>Views</strong> : 앱의 UI단이 들어있는 폴더임
</div>

<div>
</div>

<div>
  <strong>Controller</strong> : MVC 컨트롤러가 들어있는 폴더. 안에 있는 HomeController.cs가 브라우저의 요청을 처리함
</div>

<div>
</div>

<div>
  <strong>wwwroot</strong> : 웹 앱의 루트 폴더임
</div>

<div>
</div>

<div>
</div>

<div>
  터미널에서 dotnet run 하면 바로 실행되서 로컬호스트로 가면 실행된 앱을 볼 수 있음
</div>

<div>
</div>