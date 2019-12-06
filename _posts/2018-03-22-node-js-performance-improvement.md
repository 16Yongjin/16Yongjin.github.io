---
id: 698
title: 'Node.js  성능 올리기'
date: 2018-03-22T20:15:48+09:00
author: yongjinsite

guid: https://yongjinsite.wordpress.com/?p=698
permalink: '/2018/03/22/node-js-performance-improvement/'
timeline_notification:
  - "1521717351"
categories:
  - Development
tags:
  - Node.js
---
노드 인스턴스를 여러개 띄워 노드 앱의 성능을 향상시킬 수 있다.

  1. cluster로 직접 자식 프로세스를 만들기
  2. 편하게 pm2의 클러스터 모드 사용하기
  3. webworker-threads 모듈 사용하기

https://gist.github.com/16Yongjin/3f52d2b37e2f6ea8bc3f416d292a4ddb