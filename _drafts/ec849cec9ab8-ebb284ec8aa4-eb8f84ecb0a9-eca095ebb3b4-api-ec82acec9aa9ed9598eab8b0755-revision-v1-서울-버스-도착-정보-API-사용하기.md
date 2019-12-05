---
id: 834
title: 서울 버스 도착 정보 API 사용하기
date: 2019-04-21T15:10:03+09:00
author: yongjin0802
layout: revision
guid: https://yongj.in/2019/04/21/755-revision-v1/
permalink: /2019/04/21/755-revision-v1/
---
**사전 준비**

  1. 공공데이터포털에 회원가입과 로그인 하기(https://www.data.go.kr)
  2. 버스도착정보조회 서비스 활용신청 (https://www.data.go.kr/dataset/15000314/openapi.do) &#8211; 상세기능정보는 모두 체크

<img class="alignnone size-full wp-image-758" src="https://yongj.in/wp-content/uploads/2018/06/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-06-07-e1848be185a9e1848ce185a5e186ab-12-26-54.png" alt="스크린샷 2018-06-07 오전 12.26.54.png" width="1548" height="574" srcset="https://yongj.in/wp-content/uploads/2018/06/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-06-07-e1848be185a9e1848ce185a5e186ab-12-26-54.png 1548w, https://yongj.in/wp-content/uploads/2018/06/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-06-07-e1848be185a9e1848ce185a5e186ab-12-26-54-300x111.png 300w, https://yongj.in/wp-content/uploads/2018/06/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-06-07-e1848be185a9e1848ce185a5e186ab-12-26-54-768x285.png 768w, https://yongj.in/wp-content/uploads/2018/06/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-06-07-e1848be185a9e1848ce185a5e186ab-12-26-54-1024x380.png 1024w, https://yongj.in/wp-content/uploads/2018/06/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-06-07-e1848be185a9e1848ce185a5e186ab-12-26-54-1000x371.png 1000w, https://yongj.in/wp-content/uploads/2018/06/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-06-07-e1848be185a9e1848ce185a5e186ab-12-26-54-800x297.png 800w" sizes="(max-width: 1548px) 100vw, 1548px" /> 4개의 API 중 2번, 정류소 노선별 도착예정 정보 목록 조회 API를 사용한다.

정류장 ID 와 버스 노선 ID로 버스 하나의 도착 예정 시간을 알 수 있다.

정류장의 모든 버스 도착 정보를 한번에 보면 좋겠지만 서버 부하를 막기 위함인지 그런 API가 없다. <del>경기도는 있던데</del>

2번 API의 명세표는 이러하다.

<img class="alignnone size-full wp-image-759" src="https://yongj.in/wp-content/uploads/2018/06/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-06-07-e1848be185a9e1848ce185a5e186ab-12-49-39.png" alt="스크린샷 2018-06-07 오전 12.49.39.png" width="1048" height="814" srcset="https://yongj.in/wp-content/uploads/2018/06/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-06-07-e1848be185a9e1848ce185a5e186ab-12-49-39.png 1048w, https://yongj.in/wp-content/uploads/2018/06/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-06-07-e1848be185a9e1848ce185a5e186ab-12-49-39-300x233.png 300w, https://yongj.in/wp-content/uploads/2018/06/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-06-07-e1848be185a9e1848ce185a5e186ab-12-49-39-768x597.png 768w, https://yongj.in/wp-content/uploads/2018/06/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-06-07-e1848be185a9e1848ce185a5e186ab-12-49-39-1024x795.png 1024w, https://yongj.in/wp-content/uploads/2018/06/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-06-07-e1848be185a9e1848ce185a5e186ab-12-49-39-1000x777.png 1000w, https://yongj.in/wp-content/uploads/2018/06/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-06-07-e1848be185a9e1848ce185a5e186ab-12-49-39-386x300.png 386w" sizes="(max-width: 1048px) 100vw, 1048px" /> 

API 호출은

`http://ws.bus.go.kr/api/rest/arrive/getArrInfoByRoute`에 `serviceKey, stId, busRouteId, ord` 인자를 실어서 GET 요청을 보내면 된다.

`http://ws.bus.go.kr/api/rest/arrive/getArrInfoByRoute?serviceKey=${serviceKey}&stId=${stId}&busRouteId=${busRouteId}&ord=${ord}`

이렇게 말이다.

serviceKey는 마이페이지에서 볼 수 있다.

⭐️나머지 정보는 <a href="http://topis.seoul.go.kr/excel/stationlist.xlsx" target="_blank" rel="noopener noreferrer">http://topis.seoul.go.kr/excel/stationlist.xlsx</a> 이 엑셀 파일에서 알 수 있다.⭐️

`busRouteId`는 노선ID

`stId`는 정류소ID

`ord`는 순번(정류소가 노선의 몇 번째에 있는지에 관한 정보, 왜 필요한지 모르겠다.) 이므로

필요한 버스의 정보를 찾아서 API URL에 집어 넣으면 된다.

**Node.js에서 API 사용하기**

`npm init && npm i request request-promise xml2js` 터미널 명령어 실행 후

https://gist.github.com/16Yongjin/4de52b75f4175d69fdad3ea80c129c13

자주 타는 150번 버스의대방역1번출구앞 정류소 정보를 예제로 사용하였다.

<a href="http://topis.seoul.go.kr/excel/stationlist.xlsx" target="_blank" rel="noopener noreferrer">이 엑셀 파일</a>을 보면

<img class="alignnone size-full wp-image-795" src="https://yongj.in/wp-content/uploads/2018/10/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-10-11-e1848be185a9e1848ce185a5e186ab-1-22-31.png" alt="스크린샷 2018-10-11 오전 1.22.31.png" width="2414" height="470" srcset="https://yongj.in/wp-content/uploads/2018/10/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-10-11-e1848be185a9e1848ce185a5e186ab-1-22-31.png 2414w, https://yongj.in/wp-content/uploads/2018/10/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-10-11-e1848be185a9e1848ce185a5e186ab-1-22-31-300x58.png 300w, https://yongj.in/wp-content/uploads/2018/10/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-10-11-e1848be185a9e1848ce185a5e186ab-1-22-31-768x150.png 768w, https://yongj.in/wp-content/uploads/2018/10/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-10-11-e1848be185a9e1848ce185a5e186ab-1-22-31-1024x199.png 1024w, https://yongj.in/wp-content/uploads/2018/10/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-10-11-e1848be185a9e1848ce185a5e186ab-1-22-31-1000x195.png 1000w, https://yongj.in/wp-content/uploads/2018/10/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-10-11-e1848be185a9e1848ce185a5e186ab-1-22-31-800x156.png 800w" sizes="(max-width: 2414px) 100vw, 2414px" /> 

버스의 고유 식별자인 노선ID가 119000295

우리가 사용하는 노선번호가 150

150번 버스의 대방역1번출구앞 정류소의 순번은 48

대방역1번출구앞 정류소의 정류소ID는 119000295임을 알 수 있다.

http://ws.bus.go.kr/api/rest/arrive/getArrInfoByRoute?serviceKey=서비스키&stId=119000295&busRouteId=119000295&ord=48

위 URL에 발급받은 서비스키 넣고 HTTP GET 요청을 보내면 버스도착정보를 담은 XML 응답을 받을 수 있다.

XML 형식을 xml2js.parseString() 함수로 파싱한 뒤 원하는 정보를 가진 속성에 접근해서 사용하면 된다.

프라미스를 사용해서 아름다운 코드를 짜기 위해 parseString 함수를 promisify 유틸함수에 감싸서 사용했다.

다음에는 동네 예보 API 사용법을 소개하겠다.