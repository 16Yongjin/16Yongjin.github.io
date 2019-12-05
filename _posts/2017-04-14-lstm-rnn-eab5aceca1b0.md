---
id: 101
title: LSTM RNN 구조
date: 2017-04-14T13:31:30+09:00
author: yongjinsite

guid: https://yongjinsite.wordpress.com/?p=101
permalink: '/2017/04/14/lstm-rnn-%ea%b5%ac%ec%a1%b0/'
categories:
  - Deep Learning
tags:
  - LSTM
---
<div>
  <h2>
    Understanding LSTM Networks
  </h2>
</div>

<div>
  http://colah.github.io/posts/2015-08-Understanding-LSTMs/
</div>

<div>
  여기 나와 있는 것을 보고 천천히 살펴보았다.
</div>

<div>
</div>

<div>
  우선 입력, 상태, 출력 으로 구성됨
</div>

<div>
</div>

<div>
  <img src="http://colah.github.io/posts/2015-08-Understanding-LSTMs/img/LSTM3-chain.png" />
</div>

<div>
</div>

<div>
</div>

<div>
</div>

<div>
  각 셀마다 공통적으로 흐르는 줄기가 있음
</div>

![](http://colah.github.io/posts/2015-08-Understanding-LSTMs/img/LSTM3-C-line.png) 

<div>
</div>

<div>
  새 입력의 시그모이드 적용한 값이 그 줄기에 곱해져서
</div>

<div>
  줄기에 있던 값이 필요한지 아닌지 결정해줌
</div>

<div>
  1이면 다 받기, 0이면 안받기
</div>

<div>
</div>

<div>
</div>

<div>
</div>

<div>
  <b>LSTM이 처음으로 하는 일 : 망각 게이트 층. 어떤 정보를 버릴지 결정</b>
</div>

<div>
</div>

![](http://colah.github.io/posts/2015-08-Understanding-LSTMs/img/LSTM3-focus-f.png) 

<div>
  전 셀의 상태 Ct-1를 버릴지 말지 결정하는 값:
</div>

<div>
  ft = σ(가중치Wf * [전 층의 출력ht-1,  현재 입력값xt ] + 바이어스bf)
</div>

<div>
         입력값 한 층 더 업데이트한 벡터에 시그모이드 함수 적용하고 편향값 더한거.
</div>

<div>
</div>

<div>
</div>

<div>
</div>

<div>
  <b>다음으로 하는 일: 셀 상태 저장</b>
</div>

![](http://colah.github.io/posts/2015-08-Understanding-LSTMs/img/LSTM3-focus-i.png) 

<div>
  [전 층의 출력ht-1,  현재 입력값xt ]이게 여러번 쓰임, 여기에 곱하는 가중치, 편향, 활성 함수만 다 다름
</div>

<div>
</div>

<div>
</div>

<div>
  현재 셀 상태 Ct 저장할 때 쓰이는 값
</div>

<div>
  it = σ(Wi[전 층의 출력ht-1,  현재 입력값xt ] + bi) 인풋 값
</div>

<div>
  Çt = tanh(Wc * [전 층의 출력ht-1,  현재 입력값xt ] + bC) 현재 상태가 될 예정
</div>

<div>
</div>

![](http://colah.github.io/posts/2015-08-Understanding-LSTMs/img/LSTM3-focus-C.png) 

<div>
  Ct = ft * Ct-1 + it * Çt 그냥 이게 현재 상태임, 다음 셀 참고용
</div>

<div>
</div>

<div>
</div>

<div>
  이제 출력값을 뽑아냄
</div>

![](http://colah.github.io/posts/2015-08-Understanding-LSTMs/img/LSTM3-focus-o.png) 

<div>
</div>

<div>
  ot = σ(Wo * [전 층의 출력ht-1,  현재 입력값xt ] + bo)
</div>

<div>
  ht = ot * tanh(Ct) 이게 출력이고, tanh 함수는 -1에서 1사이 값 반환
</div>

<div>
</div>

<div>
</div>

<div>
  이렇게 나온 ht는 출력값으로 사용하고 Ct는 다음 셀에서 장기종속성을 해결하기 위해 다시 사용됨
</div>

<div>
</div>

<div>
</div>

<div>
</div>

<div>
</div>

<div>
</div>

<div>
</div>

<div>
</div>

<div>
</div>

<div>
</div>

<div>
</div>

<div>
</div>

<div>
</div>

<div>
</div>