---
id: 685
title: 파이프 함수를 사용한 신경망 쌓기
date: 2018-02-16T02:14:52+09:00
author: yongjinsite

guid: https://yongjinsite.wordpress.com/?p=685
permalink: '/2018/02/16/%ed%8c%8c%ec%9d%b4%ed%94%84-%ed%95%a8%ec%88%98%eb%a5%bc-%ec%82%ac%ec%9a%a9%ed%95%9c-%ec%8b%a0%ea%b2%bd%eb%a7%9d-%ec%8c%93%ea%b8%b0/'
timeline_notification:
  - "1518714895"
categories:
  - Development
  - 기타
tags:
  - Functional Programming
---
<img class="alignnone size-full wp-image-684" src="https://yongj.in/wp-content/uploads/2018/02/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-02-15-e1848be185a9e18492e185ae-8-55-54.png" alt="스크린샷 2018-02-15 오후 8.55.54" width="1118" height="276" srcset="https://yongj.in/wp-content/uploads/2018/02/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-02-15-e1848be185a9e18492e185ae-8-55-54.png 1118w, https://yongj.in/wp-content/uploads/2018/02/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-02-15-e1848be185a9e18492e185ae-8-55-54-300x74.png 300w, https://yongj.in/wp-content/uploads/2018/02/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-02-15-e1848be185a9e18492e185ae-8-55-54-768x190.png 768w, https://yongj.in/wp-content/uploads/2018/02/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-02-15-e1848be185a9e18492e185ae-8-55-54-1024x253.png 1024w, https://yongj.in/wp-content/uploads/2018/02/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-02-15-e1848be185a9e18492e185ae-8-55-54-1000x247.png 1000w, https://yongj.in/wp-content/uploads/2018/02/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-02-15-e1848be185a9e18492e185ae-8-55-54-800x197.png 800w" sizes="(max-width: 1118px) 100vw, 1118px" />

함수를 가변인자로 받아서 reduce함

<img class="alignnone size-full wp-image-683" src="https://yongj.in/wp-content/uploads/2018/02/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-02-15-e1848be185a9e18492e185ae-8-55-16-e1518714628410.png" alt="스크린샷 2018-02-15 오후 8.55.16" width="1730" height="933" srcset="https://yongj.in/wp-content/uploads/2018/02/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-02-15-e1848be185a9e18492e185ae-8-55-16-e1518714628410.png 1730w, https://yongj.in/wp-content/uploads/2018/02/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-02-15-e1848be185a9e18492e185ae-8-55-16-e1518714628410-300x162.png 300w, https://yongj.in/wp-content/uploads/2018/02/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-02-15-e1848be185a9e18492e185ae-8-55-16-e1518714628410-768x414.png 768w, https://yongj.in/wp-content/uploads/2018/02/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-02-15-e1848be185a9e18492e185ae-8-55-16-e1518714628410-1024x552.png 1024w, https://yongj.in/wp-content/uploads/2018/02/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-02-15-e1848be185a9e18492e185ae-8-55-16-e1518714628410-1000x539.png 1000w, https://yongj.in/wp-content/uploads/2018/02/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-02-15-e1848be185a9e18492e185ae-8-55-16-e1518714628410-556x300.png 556w" sizes="(max-width: 1730px) 100vw, 1730px" /> 

블록처럼 쌓기