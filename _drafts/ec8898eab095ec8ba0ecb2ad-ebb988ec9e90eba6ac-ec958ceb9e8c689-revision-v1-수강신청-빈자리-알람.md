---
id: 842
title: 수강신청 빈자리 알람
date: 2019-04-21T15:12:33+09:00
author: yongjin0802
layout: revision
guid: https://yongj.in/2019/04/21/689-revision-v1/
permalink: /2019/04/21/689-revision-v1/
---
<img class="  wp-image-690 aligncenter" src="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/03/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-03-04-e1848be185a9e18492e185ae-10-38-33.png" alt="스크린샷 2018-03-04 오후 10.38.33" width="307" height="559" srcset="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/03/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-03-04-e1848be185a9e18492e185ae-10-38-33.png 548w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/03/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-03-04-e1848be185a9e18492e185ae-10-38-33-165x300.png 165w" sizes="(max-width: 307px) 100vw, 307px" />



&nbsp;

<span class="re_green">이틀 만에</span> 만든 빈자리 알람

잘한 점은 전보다 서버 코드가 짧아졌지만 성능은 더 강력해지고 재사용이 가능해졌다.

자리가 비었나 확인할 때는 강의 html을 모두 <span class="re_green">파싱해서</span> 등록된 강의인지 <span class="re_green">필터링하지 않고</span>

클라이언트가 보낸 강의 인덱스로 td 태그에 바로 접근해서 필요한 정보(수강인원)만 가져온다.

빈자리가 났으면 데이터베이스에서 강의를 지워서 <span class="re_green">필요 없는</span> html 요청을 없앴다.

강의 인원이 &#8217;10 / 30&#8242; 이렇게 나오는데

if (eval(&#8217;10/30&#8242;) < 1에 try catch를 붙여서 강의가 비었는지 확인했다.

이렇게 필요한 것만 <span class="re_green">파싱하니</span> 30ms <span class="re_green">걸리던 게</span>  8ms 정도만 걸렸다.

아쉬웠던 점은

푸시 알람을 받아주는 서비스 워커를 등록하는데 4시간이나 걸렸다.

기본이 부족한 탓이다.