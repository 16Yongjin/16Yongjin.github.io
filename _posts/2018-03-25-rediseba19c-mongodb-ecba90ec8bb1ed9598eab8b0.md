---
id: 703
title: Redis로 MongoDB 캐싱하기
date: 2018-03-25T18:53:00+09:00
author: yongjinsite

guid: https://yongjinsite.wordpress.com/?p=703
permalink: '/2018/03/25/redis%eb%a1%9c-mongodb-%ec%ba%90%ec%8b%b1%ed%95%98%ea%b8%b0/'
timeline_notification:
  - "1521971582"
categories:
  - Development
tags:
  - MongoDB
  - Node.js
  - Redis
---
Mongoose가 MongoDB로 보내는 쿼리를 가로채는 방식으로 캐시를 적용할 수 있다.

가로챈 쿼리는 캐시의 해시 키가 된다.

레디스는 문자열만 저장할 수 있어서 JSON의 메서드가 많이 사용된다.

https://gist.github.com/16Yongjin/4239ae656efb91469fb238f86fa2a39a