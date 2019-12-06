---
id: 310
title: '파이썬 illegal UTF-16 surrogate  에러'
date: 2017-06-17T00:24:44+09:00
author: yongjinsite

guid: https://yongjinsite.wordpress.com/?p=310
permalink: '/2017/06/17/%ed%8c%8c%ec%9d%b4%ec%8d%ac-illegal-utf-16-surrogate-%ec%97%90%eb%9f%ac/'
categories:
  - Development
tags:
  - Python
---

파이썬 illegal UTF-16 surrogate 해결법

과제 수행 중

코드를 완벽하게 작성했다 생각했지만

text_preprocess(open(path, encoding=&#8217;utf-16-le&#8217;).read())

이 부분에서

UnicodeDecodeError: &#8216;utf-16-le&#8217; codec can&#8217;t decode bytes in position 374-375: illegal UTF-16 surrogate

오류가 계속 생겼다.

&nbsp;

구글링을 아무리해도 해결하지 못했지만

해결책은 엄청 간단했다.

&nbsp;

맥os 에서 파인더를 이쁘게 보여줄려고 자동으로 생성되는 .DS.store 파일이 원인이였고

이를 삭제하니까 path변수에 txt 파일위치만 잘 들어가서 과제를 잘 해결했다.

그냥 except UnicodeDecodeError: print(&#8220;error&#8221;)만 넣어도 되겠다.

&nbsp;

&nbsp;

&nbsp;

&nbsp;