---
id: 675
title: '[Codewars] Moves in squared strings (II)'
date: 2018-01-25T14:46:15+09:00
author: yongjinsite

guid: https://yongjinsite.wordpress.com/?p=675
permalink: /2018/01/25/codewars-moves-in-squared-strings-ii/
timeline_notification:
  - "1516859178"
categories:
  - 기타
tags:
  - Codewars
---
n 라인의 문자열을 180도, 360도 회전시키는 문제

예시:

[code language=&#8221;javascript&#8221;]

|rotation |selfie\_and\_rot  
|abcd &#8211;> ponm |abcd &#8211;> abcd&#8230;.  
|efgh lkji |efgh efgh&#8230;.  
|ijkl hgfe |ijkl ijkl&#8230;.  
|mnop dcba |mnop mnop&#8230;.  
&#8230;.ponm  
&#8230;.lkji  
&#8230;.hgfe  
&#8230;.dcba"  
[/code]

<div>
   답안 1등
</div>

[code language=&#8221;javascript&#8221;]

function rot(s) {  
return s.split("").reverse().join("");  
}

function selfieAndRot(s) {  
return (s = s.replace(/.+/g, t => t + t.replace(/./g, "."))) + "\n" + rot(s);  
}

[/code]

<div>
  replace 메서드에 함수 적용
</div>

<div>
   /.+/ 는 \n 등을 제외함
</div>

<div>
  매개변수를 변수로 재사용함
</div>

<div>
  대입문을 표현식으로 사용함
</div>