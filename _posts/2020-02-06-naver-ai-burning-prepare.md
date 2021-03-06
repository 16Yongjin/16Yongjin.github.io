---
title: 네이버 AI 버닝데이 준비기
date: 2020-02-6T21:00:00+09:00
author: yongjin0802
categories:
  - Development
---

### 해커톤을 준비하기 위해 아키텍처, 시퀀스 다이어그램 구성, 랜딩페이지, 로고 디자인, 풀스택 개발, 코어 기능 구현한 이야기

2월 5일 오늘, 해커톤에 불합격 통보를 받았다.

본선에 진출하지 못한 점은 아쉽지만 준비하면서 배운 게 많아서 만족한다.

## 만들려고 했던 서비스

이력서를 OCR API로 분석해서 이력서 내 정보를 채용플랫폼(사람인, 잡코리아 등)에 입력해주는 서비스다.

이력서를 하나만 작성하면 여러 플랫폼에 정보를 입력하는 수고를 덜어준다.

## 서비스 아키텍처

프런트엔드와 Node.js 이력서 자동입력 서버는 내가 만들고

나머지 인증, 유저 데이터 저장 등의 기능을 팀원들에게 맡길 생각이었다.

각 기능을 독립적으로 개발해서 분업하기 위해, 기능 간 통신 시 HTTP를 통해 JSON으로 데이터를 주고받도록 기획했다.

![ctrl-cv-Page-2(2)](https://user-images.githubusercontent.com/22253556/73840227-0c12bd80-485b-11ea-9a56-9dd3a673e0eb.png)

## 서비스 시퀀스 다이어그램

내 머리속에 있는 구현 방식을 팀원들에게 설명하기 위해 시퀀스 다이어그램을 만들었다.

![ctrl-cv(3)](https://user-images.githubusercontent.com/22253556/73840076-bb02c980-485a-11ea-8a0d-38dfddbe896a.png)

## 랜딩 페이지 ([https://ctrl-cv.surge.sh/](https://ctrl-cv.surge.sh/))

![73840560-c9051a00-485b-11ea-8b83-37a8e2d9b85a](https://user-images.githubusercontent.com/22253556/73840656-f9e54f00-485b-11ea-80a7-6b3fc74bc63f.png)


서비스를 유저에게 소개하는 페이지

트렌디하게 웨이브 배경과 콘셉트 그래픽을 넣었다.

레이아웃은 dribbble에서 자주 보이는 랜딩페이지 레이아웃이다.

3시간 만에 만들었는데 조금 잘 만든 듯


## 로고 디자인

![image](https://user-images.githubusercontent.com/22253556/73927840-7b4ce800-4915-11ea-89eb-f5f0f5e3ec15.png)


서비스 이름이 이력서(CV)를 다룬다는 뜻의 `ctrl cv`로 결정됐다.

거기에 맞는 로고를 만들기 위해 로고 생성기 샘플도 둘러보고 구글에서 이력서 관련 이미지도 많이 찾아봤다.

이력서나 종이처럼 보이는 한쪽 모서리가 접힌 박스에 CV를 넣었다.

이력서 관련 서비스라는 것을 알 수 있으면서 세련한 느낌을 준다.

HTML과 CSS로 만들어서 페이지 방문 시 로고가 늦게 뜰 걱정이 없다.


&nbsp;

## Vue.js 클라이언트

Buefy로 클라이언트 데모를 7시간 만에 만들었다.

Vue.js를 3달 만에 사용하는 것을 감안해도 빠르게 만들었다. (모바일 지원은 기본)

UI Flowchart를 만들어놓으니 보면서 그대로 구현하기 쉬웠다.

모든 구간을 애니메이션으로 연결해서 UI 흐름이 부드럽다.

### 클라이언트 데모

<iframe width="560" height="315" src="https://www.youtube.com/embed/5GhKvJTgbi0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

&nbsp;

## 이력서 자동입력 Puppeteer 스크립트

[깃허브 링크](https://github.com/16Yongjin/ctrl-cv-resume-write-automation)

Puppeteer와 타입스크립트로 채용플랫폼에 이력서를 자동으로 입력하는 기능을 구현했다.

## 이력서 자동입력 데모

### 사람인

<iframe width="560" height="315" src="https://www.youtube.com/embed/rsWg3vgPqM4" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


### 잡코리아

<iframe width="560" height="315" src="https://www.youtube.com/embed/Yo3t2ijzwhk" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### 원티드

<iframe width="560" height="315" src="https://www.youtube.com/embed/yM91WkJMxdU" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### 잡플래닛 (구현 중에 탈락해서 학력사항까지만)

<iframe width="560" height="315" src="https://www.youtube.com/embed/-hGCeNDxmhQ" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


## Puppeteer를 사용한 이유

### 1. 유저 사용성

크롬 확장 기능을 사용해서 클라이언트에서 입력을 다 실행할 수도 있지만 그럴 경우 브라우저가 데스크톱용 크롬에만 한정되어 사용성이 떨어진다.

유저의 로그인 정보를 받아야 하는게 마음에 걸리더라도 서버에서 데이터를 입력하는 게 더 낫다고 생각했다.
(토스 사용자들은 토스에 은행 계정를 넘기는데도 거부감을 안 느낀다. 보안에 신경쓰고 유저만 편하면 되는 게 아닌가)

### 2. 비동기 이벤트 대처

사람인과 잡코리아는 JQuery로 구현되어 있어서 괜찮지만

원티드와 잡플래닛은 React로 구현되어 있고 폼 입력 시 비동기 임시저장 이벤트가 일어나서 스크립트 실행 조절을 관리하기 힘들다.

그래서 Puppeteer를 사용했다.

## Puppeteer를 사용하면서 배운 점

### 1. XPath

`$x` 유틸 함수와 XPath를 사용하면 `id`나 `class` 대신 내부 텍스트를 기반으로 요소를 탐색할 수 있다.

힘들게 알맞은 선택자를 찾아 `click('.area_school_minor')`같이 함수를 호출하는 대신에

`click('기준학점선택')` 같이 실제로 눈에 보이는 텍스트를 기반으로 요소를 선택할 수 있어서 코드 작성과 파악이 쉬워졌다.

### 2. 복잡한 CSS 선택자

`major`로 시작하는 인풋 태그를 선택하는 `input[id^=major]`나

부모 요소에서 n번째 요소를 선택하는 `:nth-of-type(n)` 같은 선택자 쿼리를 작성할 수 있게 됐다.

덕분에 채용사이트 개발자들이 만들어 놓은 돔 정글 속에서 원하는 요소만 가져올 수 있었다.

### 3. 복잡한 비동기 처리

요소가 렌더링 되길 기다리는 `waitFor(selector)`나

api 요청 중일 때 대기하는 `page.waitForNavigation({waitUntil: "networkidle0"});`를 사용해서

비동기 상황에서도 폼 입력을 할 수 있는 코드를 작성했다.

&nbsp;

## `FastAPI` 발견


[FastAPI](fastapi.tiangolo.com/)는 코드를 작성해서 API 만들면 문서가 자동으로 생성된다.

문서를 작성해서 내가 필요한 API을 팀원에게 만들어 달라고 할 생각이었다.

문서를 만들기 위해 `FastAPI`로 코드를 작성하다 보니 필요한 기능을 내가 구현해버리고 말았다..


## `FastAPI`의 장점

1. 타입 힌트 사용으로 개발 시 편하다.
2. API 정의에 따라 스웨거와 리독 문서가 자동으로 생성된다.
3. 튜토리얼 문서가 잘 되어 있어서 필요한 기능 개발에 많은 도움을 받을 수 있다.

## `Sqlalchemy`(ORM)와 `Pydantic`(Data Validation)

속성에 타입이 있는 클래스만 정의하면

- `Sqlalchemy`으로 쉽게 [DB 모델링](https://github.com/16Yongjin/ctrl-cv-fastapi/blob/master/sql_app/models.py)을 할 수 있다.
- `Pydantic`으로 쉽게 [폼 검증 기능](https://github.com/16Yongjin/ctrl-cv-fastapi/blob/master/sql_app/schemas.py)을 구현할 수 있다.

&nbsp;

## 마치며

심리학 책 **굿라이프**에 따르면 개인 프로젝트는 좋은 삶을 위한 의미에 중요한 역할을 한다.

심리학자 브라이언 리틀은 개인 프로젝트를 5가지 차원으로 평가할 수 있다고 했다.

1. 자신에게 도움이 되는 정도(self benefit)
2. 성공 가능성(efficacy)
3. 재미(fun)
4. 타인의 지지(support)
5. 통합(integrity, 자신의 정체성과의 부합 정도)

프로젝트 준비를 하면서

1. 아키텍처 구성, 서비스 다이어그램, 브랜드 디자인, 풀스택, 코어 기능 구현 등을 했고 실력이 전보다 늘었다.
2. 본선 진출엔 실패했지만 구현 계획 실현에 성공했다.
3. 부드럽게 UI가 진행되는 프런트엔드와 이력서를 빠르게 입력하는 Puppeteer 스크립트를 보며 재미를 느꼈다.
4. 기능을 구현해서 팀원에게 보여줄 때마다 좋은 반응을 얻을 수 있었고 그 덕분에 힘이 나고 자신감이 생겼다.
5. 프로그래밍하길 잘했다는 생각이 들었다.

다음 목표가 생길 때까지 하고 싶은 공부를 계속하면서 다음에 목표가 생기면 다시 열심히 해야겠다.
