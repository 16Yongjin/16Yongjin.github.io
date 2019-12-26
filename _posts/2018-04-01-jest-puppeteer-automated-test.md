---
id: 707
title: Jest와 Puppeteer로 자동화 테스트하기
date: 2018-04-01T18:35:51+09:00
author: yongjinsite
categories:
  - Node.js
tags:
  - Jest
  - Puppeteer
  - Testing
---

Jest와 Puppeteer로 자동화 테스트를 하는 방법

Puppeter를 사용하기 쉽게 해주는 Helper Class.

ES6 Proxy를 통해  Puppeter의 기능과 커스텀 기능을 객체 하나로 사용할 수 있다.

<script src="https://gist.github.com/16Yongjin/73b123b6c198fa77aac5ce798069bd8d.js"></script>

describe 블럭 아래에 describe 블럭을 넣어서 테스트 트리 구조를 만든다.

HTML 요소에 원하는 텍스트가 나오길 기대하며 테스트를 진행한다.

<script src="https://gist.github.com/16Yongjin/41b9bec89044eebad0bd7fd1fb5c3339.js"></script>