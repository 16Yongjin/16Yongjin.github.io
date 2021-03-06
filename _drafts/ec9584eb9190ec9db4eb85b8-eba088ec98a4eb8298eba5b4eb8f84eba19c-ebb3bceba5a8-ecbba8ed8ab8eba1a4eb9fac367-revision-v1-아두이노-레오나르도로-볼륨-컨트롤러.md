---
id: 856
title: 아두이노 레오나르도로 볼륨 컨트롤러
date: 2019-04-21T15:15:35+09:00
author: yongjin0802
layout: revision
guid: https://yongj.in/2019/04/21/367-revision-v1/
permalink: /2019/04/21/367-revision-v1/
---
아두이노 레오나르도로 PC나 Mac의 볼륨 컨트롤러를 만들었다.

  1. https://github.com/NicoHood/HID 여기서 라이브러리 zip 파일 다운 받기
  2. 아두이노 IDE 메뉴 -> Sketch  -> Include Library -> Add .zip file 해서 라이브러리 추가
  3.  코드 작성

[code language=&#8221;cpp&#8221;]  
#include "HID-Project.h"

#define outputA 6  
#define outputB 7  
#define button 8  
int counter = 0;  
int aState;  
int aLastState;  
void setup() {  
pinMode (outputA,INPUT);  
pinMode (outputB,INPUT);  
pinMode (button, INPUT_PULLUP);  
Consumer.begin();

//Serial.begin (9600);

// Reads the initial state of the outputA  
aLastState = digitalRead(outputA);  
}  
void loop() {  
aState = digitalRead(outputA); // Reads the "current" state of the outputA  
// If the previous and the current state of the outputA are different, that means a Pulse has occured  
if (aState != aLastState){  
// If the outputB state is different to the outputA state, that means the encoder is rotating clockwise  
if (digitalRead(outputB) != aState) {  
counter ++;  
Consumer.write(MEDIA\_VOLUME\_UP);  
} else {  
counter &#8211;;  
Consumer.write(MEDIA\_VOLUME\_DOWN);  
}  
//Serial.print("Position: ");  
//Serial.println(counter);  
}  
aLastState = aState; // Updates the previous state of the outputA with the current state

if (!digitalRead(button)) {  
//Serial.println("Button Pressed");  
Consumer.write(MEDIA\_VOLUME\_MUTE);  
delay(500);  
}  
}  
[/code]  
로터리 인코더 사용법은

[youtube https://www.youtube.com/watch?v=v4BbSzJ-hz4&w=560&h=315]

여기서 확인했고볼륨 컨트롤은

http://www.loiph.in/2014/09/arduino-leonardo-atmega32u4-based-usb.html

여기를 참고했다.

작동 영상  
[youtube https://www.youtube.com/watch?v=McfWUW4JflE&w=560&h=315]  
Windows10

[youtube https://www.youtube.com/watch?v=oUGgiOFYr_g&w=560&h=315]  
Mac