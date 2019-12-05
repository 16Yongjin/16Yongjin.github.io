---
id: 515
title: 한국외대 수강신청 빈자리 알리미
date: 2017-08-22T03:42:59+09:00
author: yongjinsite
layout: post
guid: https://yongjinsite.wordpress.com/?p=515
permalink: '/2017/08/22/%ed%95%9c%ea%b5%ad%ec%99%b8%eb%8c%80-%ec%88%98%ea%b0%95%ec%8b%a0%ec%b2%ad-%eb%b9%88%ec%9e%90%eb%a6%ac-%ec%95%8c%eb%a6%ac%eb%af%b8/'
categories:
  - Development
tags:
  - HUFS
---
&nbsp;

강의 빈자리가 나면 알람 울리는 앱을 혼자 쓸려고 만들었다가

파이어베이스로 크롬에 universial하게 알람 메시지를 보낼 수 있다는 것을 알고

앞단과 뒷단을 부랴부랴 만들었다.

앞단은 vue.js로 만들었는데 코드 짠 거 보면 남에게 보여주기엔 너무 민망하다.

기능을 컴포넌트 파일 별로 나눠서 만들어야 됐는데 부모-자식 간 데이터 교환을 신경쓰는게 너무 귀찮아서 html 파일 하나 js 파일 하나에 다 몰아넣었다.

뒷단은 속도를 탓하며 es6 class로 유저 데이터를 저장하고 있는데 사실 db를 사용할 줄 몰라서 그런다.

그래도 학교 서버에서 강의 데이터를 뽑아오는 함수는 강건하게 작성했고

서버엔 https와 클라이언트엔 bootstrap-select도 잘 적용했다.

&nbsp;

http 접속을 https로 돌려야되는데 계속 미루고 있다.

https://hufs-lecture-alert.yjdev.com

&nbsp;

&nbsp;