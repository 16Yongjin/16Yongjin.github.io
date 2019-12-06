---
id: 847
title: VS Code에서 Phoenix 프레임워크의 eex 템플릿에 Emmet 사용하기
date: 2019-04-21T15:13:41+09:00
author: yongjin0802
layout: revision
guid: https://yongj.in/2019/04/21/665-revision-v1/
permalink: /2019/04/21/665-revision-v1/
---
<div>
  cmd + , 로 사용자 설정 파일을 열고
</div>

<pre>"files.associations": {
        "*.eex": "ejs"
    },
</pre>

<pre>"emmet.includeLanguages": {
        "ejs": "html"
    }</pre>

<div>
   이 두 줄을 추가해준다.
</div>

<div>
  <img class="alignnone size-full wp-image-666" src="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/01/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-01-12-e1848be185a9e18492e185ae-5-32-58.png" alt="스크린샷 2018-01-12 오후 5.32.58" width="1432" height="332" srcset="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/01/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-01-12-e1848be185a9e18492e185ae-5-32-58.png 1432w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/01/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-01-12-e1848be185a9e18492e185ae-5-32-58-300x70.png 300w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/01/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-01-12-e1848be185a9e18492e185ae-5-32-58-768x178.png 768w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/01/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-01-12-e1848be185a9e18492e185ae-5-32-58-1024x237.png 1024w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/01/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-01-12-e1848be185a9e18492e185ae-5-32-58-1000x232.png 1000w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/01/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-01-12-e1848be185a9e18492e185ae-5-32-58-800x185.png 800w" sizes="(max-width: 1432px) 100vw, 1432px" /><img class="alignnone size-full wp-image-667" src="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/01/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-01-12-e1848be185a9e18492e185ae-5-33-14.png" alt="스크린샷 2018-01-12 오후 5.33.14" width="1370" height="398" srcset="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/01/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-01-12-e1848be185a9e18492e185ae-5-33-14.png 1370w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/01/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-01-12-e1848be185a9e18492e185ae-5-33-14-300x87.png 300w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/01/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-01-12-e1848be185a9e18492e185ae-5-33-14-768x223.png 768w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/01/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-01-12-e1848be185a9e18492e185ae-5-33-14-1024x297.png 1024w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/01/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-01-12-e1848be185a9e18492e185ae-5-33-14-1000x291.png 1000w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/01/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-01-12-e1848be185a9e18492e185ae-5-33-14-800x232.png 800w" sizes="(max-width: 1370px) 100vw, 1370px" />
</div>

<div>
  emmet 이 잘 작동한다.
</div>

&nbsp;