---
id: 833
title: 동네 예보 API 사용하기
date: 2019-04-21T15:09:47+09:00
author: yongjin0802
layout: revision
guid: https://yongj.in/2019/04/21/769-revision-v1/
permalink: /2019/04/21/769-revision-v1/
---
  1. (신)동네예보정보조회서비스 활용 신청 (https://www.data.go.kr/dataset/15000099/openapi.do)
  2. API 미리보기를 실행해서 API URL 얻기

<img class="alignnone size-full wp-image-770" src="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/06/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-06-07-e1848be185a9e18492e185ae-1-02-11.png" alt="스크린샷 2018-06-07 오후 1.02.11.png" width="789" height="621" srcset="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/06/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-06-07-e1848be185a9e18492e185ae-1-02-11.png 789w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/06/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-06-07-e1848be185a9e18492e185ae-1-02-11-300x236.png 300w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/06/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-06-07-e1848be185a9e18492e185ae-1-02-11-768x604.png 768w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/06/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-06-07-e1848be185a9e18492e185ae-1-02-11-381x300.png 381w" sizes="(max-width: 789px) 100vw, 789px" /> 

base_date에는 YYYYMMDD 형식의 오늘 날짜를 넣는다.

base_time에는 0200을 넣는다. 0500으로 넣으면 새벽 6시 예보가 안 나온다.

numOfRows에는 50을 넣는게 좋다.

_type은 json을 넣으면 Node.js에서 사용하기 편하다

<img class="alignnone size-full wp-image-771" src="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/06/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-06-07-e1848be185a9e18492e185ae-1-04-49.png" alt="스크린샷 2018-06-07 오후 1.04.49.png" width="339" height="663" srcset="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/06/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-06-07-e1848be185a9e18492e185ae-1-04-49.png 339w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/06/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-06-07-e1848be185a9e18492e185ae-1-04-49-153x300.png 153w" sizes="(max-width: 339px) 100vw, 339px" /> 

그러면 사진처럼 JSON 응답이 오는데

6, 9, 12, 15, 18, 21시