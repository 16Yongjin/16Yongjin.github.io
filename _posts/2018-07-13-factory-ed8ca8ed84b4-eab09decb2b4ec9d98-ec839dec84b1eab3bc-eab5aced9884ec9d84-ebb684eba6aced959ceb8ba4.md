---
id: 779
title: 'Factory 패턴: 객체의 생성과 구현을 분리한다.'
date: 2018-07-13T16:55:41+09:00
author: yongjinsite

guid: https://yongjinsite.wordpress.com/?p=779
permalink: '/2018/07/13/factory-%ed%8c%a8%ed%84%b4-%ea%b0%9d%ec%b2%b4%ec%9d%98-%ec%83%9d%ec%84%b1%ea%b3%bc-%ea%b5%ac%ed%98%84%ec%9d%84-%eb%b6%84%eb%a6%ac%ed%95%9c%eb%8b%a4/'
timeline_notification:
  - "1531468546"
categories:
  - Development
tags:
  - Node.js
  - 디자인 패턴
---
처음에는 팩토리 패턴이 클래스들 여러개를 클래스 하나에 몰아넣고 옵션 인자에 따라 선택적으로 객체를 생성하는 것이라 생각했다.

Node.js Design Patterns 챕터 6을 읽으면서 객체의 생성과 구현을 분리해서 수정하기 쉬운 코드를 만드는데 도움이 된다는 것을 알았다.

<div>
</div>

<div>
  JS는 객체 생성 시 new 연산자와 Object.create() 사용한다.
</div>

<div>
</div>

<div>
  new 사용 시 코드에 객체 타입 하나만 결합할 수 있다.
</div>

<div>
</div>

<div>
</div>

<div style="background:#f0f0f0;overflow:auto;width:auto;border:solid gray;border-width:.1em .1em .1em .8em;padding:.2em .6em;">
  <pre style="margin:0;line-height:125%;"><span style="color:#007020;font-weight:bold;">function</span> createImage(name) {
    <span style="color:#007020;font-weight:bold;">return</span> <span style="color:#007020;font-weight:bold;">new</span> Image(name);
}
<span style="color:#007020;font-weight:bold;">const</span> image <span style="color:#666666;">=</span> createImage(<span style="color:#4070a0;">'photo.jpeg'</span>);</pre>
</div>

<div>
</div>

<div>
  위는 Image를 생성하는 팩토리 함수다.
</div>

<div>
</div>

<div>
</div>

<div>
  <div style="background:#f0f0f0;overflow:auto;width:auto;border:solid gray;border-width:.1em .1em .1em .8em;padding:.2em .6em;">
    <pre style="margin:0;line-height:125%;"><span style="color:#007020;font-weight:bold;">const</span> image <span style="color:#666666;">=</span> <span style="color:#007020;font-weight:bold;">new</span> Image(name);
</pre>
  </div>
</div>

<div>
  <div>
    이렇게 그냥 new로 Image 클래스 를 바로 사용할 수 있으므로 createImage() 팩토리는 쓸모 없어 보인다.
  </div>
</div>

<div>
</div>

<div>
  하지만 Image 클래스를 작은 클래스 단위로 나눠서 리팩토링할 때
</div>

<div>
</div>

<div>
  코드에서 image 생성을 팩토리를 통해서만 했다면
</div>

<div>
</div>

<div>
  기존의 코드를 변경할 필요 없이 팩토리만 수정하면 된다.
</div>

<div>
</div>

<div>
  <div>
    <div style="background:#f0f0f0;overflow:auto;width:auto;border:solid gray;border-width:.1em .1em .1em .8em;padding:.2em .6em;">
      <pre style="margin:0;line-height:125%;"><span style="color:#007020;font-weight:bold;">function</span> createImage(name) {
    <span style="color:#007020;font-weight:bold;">if</span>(name.match(<span style="color:#235388;">/\.jpeg$/</span>)) {
        <span style="color:#007020;font-weight:bold;">return</span> <span style="color:#007020;font-weight:bold;">new</span> JpegImage(name);
    } <span style="color:#007020;font-weight:bold;">else</span> <span style="color:#007020;font-weight:bold;">if</span>(name.match(<span style="color:#235388;">/\.gif$/</span>)) {
        <span style="color:#007020;font-weight:bold;">return</span> <span style="color:#007020;font-weight:bold;">new</span> GifImage(name);
    } <span style="color:#007020;font-weight:bold;">else</span> <span style="color:#007020;font-weight:bold;">if</span>(name.match(<span style="color:#235388;">/\.png$/</span>)) {
        <span style="color:#007020;font-weight:bold;">return</span> <span style="color:#007020;font-weight:bold;">new</span> PngImage(name);
    } <span style="color:#007020;font-weight:bold;">else</span> {
        <span style="color:#007020;font-weight:bold;">throw</span> <span style="color:#007020;font-weight:bold;">new</span> Exception(<span style="color:#4070a0;">'Unsupported format'</span>);
    }
}
</pre>
    </div>
    
    <p>
      &nbsp;
    </p>
  </div>
  
  <div>
  </div>
  
  <div>
    이 외에도 팩토리는 내부 클래스를 노출시키지 않는다.
  </div>
  
  <div>
  </div>
  
  <div>
    덕분에 클래스가 확장되거나 변경되는 것을 막을 수 있다.
  </div>
</div>