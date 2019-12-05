---
id: 246
title: 아두이노 레오나르도로 마우스 시뮬레이션하기
date: 2017-04-22T23:12:38+09:00
author: yongjinsite
layout: post
guid: https://yongjinsite.wordpress.com/?p=246
permalink: '/2017/04/22/%ec%95%84%eb%91%90%ec%9d%b4%eb%85%b8-%eb%a0%88%ec%98%a4%eb%82%98%eb%a5%b4%eb%8f%84%eb%a1%9c-%eb%a7%88%ec%9a%b0%ec%8a%a4-%ec%8b%9c%eb%ae%ac%eb%a0%88%ec%9d%b4%ec%85%98%ed%95%98%ea%b8%b0/'
categories:
  - 기타
tags:
  - Arduino
---
 



여기를 참고 했다.

<img src="https://yongj.in/wp-content/uploads/2017/04/kakaotalk_20170421_212141455-e1492870559437.jpg" alt="KakaoTalk_20170421_212141455.jpg" width="540" height="747" class="aligncenter size-full wp-image-252" srcset="https://yongj.in/wp-content/uploads/2017/04/kakaotalk_20170421_212141455-e1492870559437.jpg 540w, https://yongj.in/wp-content/uploads/2017/04/kakaotalk_20170421_212141455-e1492870559437-217x300.jpg 217w" sizes="(max-width: 540px) 100vw, 540px" /> 



 

 

   
[code language=&#8221;cpp&#8221;]  
// Define Pins  
#include <Mouse.h>  
const int mouseLeftButton = 2; // input pin for the mouse left Button  
const int joystickX = A1; // joystick X axis  
const int joystickY = A0; // joystick Y axis

// parameters for reading the joystick:  
int cursorSpeed = 10; // output speed of X or Y movement  
int responseDelay = 5; // response delay of the mouse, in ms  
int threshold = cursorSpeed/4; // resting threshold  
int center = cursorSpeed/2; // resting position value

boolean mouseIsActive = true; // whether or not to control the mouse  
int lastSwitchState = HIGH; // previous switch state

void setup() {  
pinMode(mouseLeftButton, INPUT_PULLUP); // the left mouse button pin  
Mouse.begin(); // take control of the mouse  
}

void loop() {  
// read the switch:  
int switchState = 1;

// if it&#8217;s changed and it&#8217;s high, toggle the mouse state:  
if (switchState != lastSwitchState) {  
if (switchState == LOW) {  
mouseIsActive = !mouseIsActive;  
}  
}

// save switch state for next loop:  
lastSwitchState = switchState;

// read and scale the two axes:  
int xReading = readAxis(A1);  
int yReading = readAxis(A0);

// if the mouse control state is active, move the mouse:  
if (mouseIsActive) {  
Mouse.move(xReading, -yReading, 0); // (x, y, scroll mouse wheel)  
}

// read the mouse button and click or not click:  
// if the mouse button is pressed:  
if (digitalRead(mouseLeftButton) != HIGH) {  
// if the mouse is not pressed, press it:  
if (!Mouse.isPressed(MOUSE_LEFT)) {  
Mouse.press(MOUSE_LEFT);  
delay(100); // delay to enable single and double-click

}  
}

// else the mouse button is not pressed:  
else {  
// if the mouse is pressed, release it:  
if (Mouse.isPressed(MOUSE_LEFT)) {  
Mouse.release(MOUSE_LEFT);  
}  
}

delay(responseDelay);  
}

/*  
reads an axis (0 or 1 for x or y) and scales the  
analog input range to a range from 0 to  
*/

int readAxis(int thisAxis) {  
// read the analog input:  
int reading = analogRead(thisAxis);

// map the reading from the analog input range to the output range:  
reading = map(reading, 0, 1023, 0, cursorSpeed);

// if the output reading is outside from the  
// rest position threshold, use it:  
int distance = reading &#8211; center;

if (abs(distance) < threshold) {  
distance = 0;  
}

// return the distance for this axis:  
return distance;  
}  
[/code]