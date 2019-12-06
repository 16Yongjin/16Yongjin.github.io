---
id: 779
title: 'Factory 패턴: 객체의 생성과 구현을 분리한다.'
date: 2018-07-13T16:55:41+09:00
author: yongjinsite

guid: https://yongjinsite.wordpress.com/?p=779
permalink: '/2018/07/13/factory-pattern/'
timeline_notification:
  - "1531468546"
categories:
  - Development
tags:
  - Node.js
  - Design Pattern
  - Factory Pattern
---

## 객체의 생성과 구현을 분리하는 팩토리 패턴


처음에는 팩토리 패턴이 클래스들 여러개를 클래스 하나에 몰아넣고 옵션 인자에 따라 선택적으로 객체를 생성하는 것이라 생각했다.

Node.js Design Patterns 챕터 6을 읽으면서 객체의 생성과 구현을 분리해서 수정하기 쉬운 코드를 만드는데 도움이 된다는 것을 알았다.


JS는 객체 생성 시 `new` 연산자와 `Object.create()` 사용한다.

new 사용 시 코드에 객체 타입 하나만 결합할 수 있다.

```javascript
function createImage(name) {
    return new Image(name);
}
const image = createImage('photo.jpeg');
```
위는 Image를 생성하는 팩토리 함수다.

```javascript
const image = new Image(name);
```

이렇게 그냥 new로 Image 클래스 를 바로 사용할 수 있으므로 createImage() 팩토리는 쓸모 없어 보인다.

하지만 Image 클래스를 작은 클래스 단위로 나눠서 리팩토링할 때

코드에서 image 생성을 팩토리를 통해서만 했다면

기존의 코드를 변경할 필요 없이 팩토리만 수정하면 된다.


```javascript
function createImage(name) {
    if(name.match(/\.jpeg$/)) {
        return new JpegImage(name);
    } else if(name.match(/\.gif$/)) {
        return new GifImage(name);
    } else if(name.match(/\.png$/)) {
        return new PngImage(name);
    } else {
        throw new Exception('Unsupported format');
    }
}
```

이 외에도 팩토리는 내부 클래스를 노출시키지 않는다.

덕분에 클래스가 확장되거나 변경되는 것을 막을 수 있다.
