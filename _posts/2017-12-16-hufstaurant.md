---
id: 657
title: Hufstaurant
date: 2017-12-16T19:33:33+09:00
author: yongjinsite

guid: https://yongjinsite.wordpress.com/?p=657
permalink: /2017/12/16/hufstaurant/
categories:
  - Development
tags:
  - Portuguese
---
&nbsp;

외대 주변 식당 추천앱, 훕스토랑

Vuetify와 Firebase를 사용했다.

말은 학회 프로젝트지 혼자 다 만들었다.

서버 만들 시간이 없어서 Firebase에 많이 의존했는데 DB조작을 다 앞단에서 하기에 보안 문제가 많다. 그래서 다시 다 갈아엎어야 한다.

UI도 마음에 안 든다. 제일 어려운 문제다.

Element 라이브러리를 써서 다시 만들고 싶다.

**특이사항**

1. 음식 사진이나 리뷰 사진 썸네일 만드는 것은 Cloud function을 사용했다.

스토리지에 리스너가 있어서 파일이 들어오면 썸네일을 만들고 저장한 뒤 데이터베이스에 다운로드 주소를 추가한다.

2. 로그인 & 회원가입 기능

3. Vue.js용 구글맵스 라이브러리 &#8211; 진작 쓸 걸!

4. 반응형으로 만들어서 브라우저를 어떻게 찌그려 뜨리든 보일 건 다 보인다.

&nbsp;

&nbsp;

&nbsp;