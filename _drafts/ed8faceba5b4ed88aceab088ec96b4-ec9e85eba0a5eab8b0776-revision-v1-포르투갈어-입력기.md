---
id: 831
title: 포르투갈어 입력기
date: 2019-04-21T15:09:02+09:00
author: yongjin0802
layout: revision
guid: https://yongj.in/2019/04/21/776-revision-v1/
permalink: /2019/04/21/776-revision-v1/
---
<img class="  wp-image-777 aligncenter" src="https://yongj.in/wp-content/uploads/2018/06/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-06-11-e1848be185a9e18492e185ae-3-15-49.png" alt="스크린샷 2018-06-11 오후 3.15.49.png" width="540" height="374" srcset="https://yongj.in/wp-content/uploads/2018/06/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-06-11-e1848be185a9e18492e185ae-3-15-49.png 1436w, https://yongj.in/wp-content/uploads/2018/06/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-06-11-e1848be185a9e18492e185ae-3-15-49-300x208.png 300w, https://yongj.in/wp-content/uploads/2018/06/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-06-11-e1848be185a9e18492e185ae-3-15-49-768x532.png 768w, https://yongj.in/wp-content/uploads/2018/06/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-06-11-e1848be185a9e18492e185ae-3-15-49-1024x709.png 1024w, https://yongj.in/wp-content/uploads/2018/06/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-06-11-e1848be185a9e18492e185ae-3-15-49-1000x692.png 1000w, https://yongj.in/wp-content/uploads/2018/06/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-06-11-e1848be185a9e18492e185ae-3-15-49-433x300.png 433w" sizes="(max-width: 540px) 100vw, 540px" />

http://pt-key.surge.sh/

윈도우에서도 편하게 포어를 입력하기 위해 웹상에 구현한 포르투갈어 입력기

keymage 라이브러리를 사용해 키 입력 이벤트를 가로채서 포어를 textarea에 집어넣는 방식으로 구현했다.

&nbsp;

RxJS로 구현하기 위해 멀티키 입력을 인식하는 스트림도 만들었지만

https://jsfiddle.net/op2derk7/3/

이걸 사용하려면 모든 키에 대한 스트림도 만들어야 해서 그냥 기존의 키입력을 가로채는 방식으로 만들었다.