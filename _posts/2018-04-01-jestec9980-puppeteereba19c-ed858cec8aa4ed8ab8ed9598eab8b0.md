---
id: 707
title: Jest와 Puppeteer로 테스트하기
date: 2018-04-01T18:35:51+09:00
author: yongjinsite

guid: https://yongjinsite.wordpress.com/?p=707
permalink: '/2018/04/01/jest%ec%99%80-puppeteer%eb%a1%9c-%ed%85%8c%ec%8a%a4%ed%8a%b8%ed%95%98%ea%b8%b0/'
timeline_notification:
  - "1522575353"
categories:
  - Development
tags:
  - Jest
  - Node.js
  - Puppeteer
---
Puppeter를 사용하기 쉽게 해주는 Helper Class.

ES6 Proxy를 통해  Puppeter의 기능과 커스텀 기능을 객체 하나로 사용할 수 있다.

https://gist.github.com/16Yongjin/73b123b6c198fa77aac5ce798069bd8d

describe 블럭 아래에 describe 블럭을 넣어서 테스트 트리 구조를 만든다.

HTML 요소에 원하는 텍스트가 나오길 기대하며 테스트를 진행한다.

https://gist.github.com/16Yongjin/41b9bec89044eebad0bd7fd1fb5c3339