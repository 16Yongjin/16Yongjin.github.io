---
id: 836
title: PT POPDIC 크롬 익스텐션
date: 2019-04-21T15:10:57+09:00
author: yongjin0802
layout: revision
guid: https://yongj.in/2019/04/21/732-revision-v1/
permalink: /2019/04/21/732-revision-v1/
---
<img class="alignnone size-full wp-image-733" src="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-05-e1848be185a9e18492e185ae-11-11-30.png" alt="스크린샷 2018-05-05 오후 11.11.30.png" width="1960" height="1229" srcset="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-05-e1848be185a9e18492e185ae-11-11-30.png 1960w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-05-e1848be185a9e18492e185ae-11-11-30-300x188.png 300w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-05-e1848be185a9e18492e185ae-11-11-30-768x482.png 768w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-05-e1848be185a9e18492e185ae-11-11-30-1024x642.png 1024w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-05-e1848be185a9e18492e185ae-11-11-30-1000x627.png 1000w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-05-e1848be185a9e18492e185ae-11-11-30-478x300.png 478w" sizes="(max-width: 1960px) 100vw, 1960px" />

단어 서버 성능이 좋아진 기념으로 크롬 익스텐션을 만들었다.

https://goo.gl/tbmQ65

**고민한 점**

단어에 마우스를 올리면 아래에 뜻을 tooltip으로 보여주면 편하겠지만

매일 포어 단어 찾는 것도 아니고

안 쓸 때는 끄기 옵션을 선택하는 게 상당히 귀찮다.

그래서 알림을 사용했다.

단어 뜻이 팝업 되는 게 앱 이름값을 하는 것 같아 마음에 든다.

&nbsp;

**메모할 점**

팝업을 만들 때 vue.js 를 사용했는데

Content Security _Policy_를 지키기 위해

manifest.json에

<pre>"sandbox": {
    "pages": ["index.html"]
 }</pre>

를 추가해야 한다.

vue.js 가 내부의 eval 함수 사용이 CSP를 위반하기에

sandbox 옵션을 넣어주면 eval 함수를 안전하게 사용할 수 있고 vue도 정상적으로 작동한다.

&nbsp;

<img class="  wp-image-734 aligncenter" src="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-05-e1848be185a9e18492e185ae-11-22-07.png" alt="스크린샷 2018-05-05 오후 11.22.07" width="414" height="367" srcset="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-05-e1848be185a9e18492e185ae-11-22-07.png 884w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-05-e1848be185a9e18492e185ae-11-22-07-300x266.png 300w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-05-e1848be185a9e18492e185ae-11-22-07-768x681.png 768w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-05-e1848be185a9e18492e185ae-11-22-07-338x300.png 338w" sizes="(max-width: 414px) 100vw, 414px" /> 

<p style="text-align:center;">
  완성된 팝업
</p>