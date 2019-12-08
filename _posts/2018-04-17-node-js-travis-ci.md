---
id: 709
title: Node.js Travis CI 설정
date: 2018-04-17T00:53:56+09:00
author: yongjinsite
permalink: '/2018/04/17/node.js-travis-ci/'
timeline_notification:
  - "1523894039"
categories:
  - Node.js
tags:
  - Travis CI
---
# Node.js Travis CI 설정하기

<script src="https://gist.github.com/16Yongjin/886acb3683aaea4581b3415a7cda36e7.js"></script>

1. trusty 라는 작은 리눅스에 node 8버전과 mongodb, redis-server를 붙인다.
2. 노드 모듈들을 설치하고 리액트 앱을 빌드한다.
3. 서버를 시작한다.
4. 서버 작동을 시작하기도 전에 테스트를 하면 오류가 날 수 있기에 3초간 기다린다.
5. 테스트를 돌린다.
6. 테스트에 성공하면 성공 메일이 온다.