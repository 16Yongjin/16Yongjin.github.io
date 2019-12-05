---
id: 840
title: Redis로 MongoDB 캐싱하기
date: 2019-04-21T15:11:56+09:00
author: yongjin0802
layout: revision
guid: https://yongj.in/2019/04/21/703-revision-v1/
permalink: /2019/04/21/703-revision-v1/
---
Mongoose가 MongoDB로 보내는 쿼리를 가로채는 방식으로 캐시를 적용할 수 있다.

가로챈 쿼리는 캐시의 해시 키가 된다.

레디스는 문자열만 저장할 수 있어서 JSON의 메서드가 많이 사용된다.

https://gist.github.com/16Yongjin/4239ae656efb91469fb238f86fa2a39a