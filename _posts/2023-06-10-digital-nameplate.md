---
title: ESP32와 LED 매트릭스로 디지털 명패 만들기
date: 2023-02-19T21:00:00+09:00
author: yongjin0802
categories:
  - Development
---

사무실의 시대가 돌아왔다. 회사에 내 자리가 생기면 가장 갖고 싶었던 게 이름표다. 테크 감성 오지는 디지털 명패 만드는 법을 알아보자.

![데스크 셋업](https://github.com/16Yongjin/16Yongjin.github.io/assets/22253556/76625900-9c14-44dd-b43d-4c46fdcdf134)

## 데모

<video width="100%" controls="controls">
  <source src="https://github.com/16Yongjin/16Yongjin.github.io/assets/22253556/6d730f21-6473-40a3-b467-1a0bd0a0c7f2" type="video/mp4">
</video>

회의 등으로 자리를 비웠을 때, 내 상태를 표시할 수 있다.

- ⚫️ - 출근 안 함 / 재택 중 (화면 꺼짐)
- ⚪️ - 근무 중 (이름 표시)
- 🔴 - 바쁨 / 방해금지
- 🟢 - 티타임 중
- 🔵 - 회의 중

## 필요한 부품

![디지털 명패 부품](https://github.com/16Yongjin/16Yongjin.github.io/assets/22253556/8ca688aa-af3a-472f-b2b1-d14066e37f5a)

### 부품 가격

- 배송비 포함 약 41,000원 (23. 6. 10 기준)

| 부품명            | 가격     | 구매 링크                                                                         |
| ----------------- | -------- | --------------------------------------------------------------------------------- |
| LED 매트릭스      | 20,000원 | [알리익스프레스](https://ko.aliexpress.com/item/4000002686894.html)               |
| ESP32 + 어댑터    | 6,700원  | [알리익스프레스](https://ko.aliexpress.com/item/1005004268911484.html)            |
| 점퍼 와이어 120개 | 2,200원  | [알리익스프레스](https://ko.aliexpress.com/item/4000203371860.html)               |
| 빵판              | 2,000원  | [알리익스프레스](https://ko.aliexpress.com/item/1005004373602861.html)            |
| 버튼 25개         | 3,000원  | [알리익스프레스](https://ko.aliexpress.com/item/32834276752.html)                 |
| 막대저항          | 3,000원  | [네이버 쇼핑](https://smartstore.naver.com/mechasolution_com/products/2955124756) |
| U자 점퍼 와이어   | 4,000원  | [알리익스프레스](https://ko.aliexpress.com/item/1005004181586889.html)            |

## 조립 방법

### 디스플레이 조립

아래 영상을 보고 LED Matrix와 ESP32를 조립한다.

<iframe width="560" height="315" src="https://www.youtube.com/embed/hmmGhepMbSs" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

이때! 영상 나오는 전원 어댑터는 따로 필요가 없다.

ESP32의 5V핀(VIN)을 LED 매트릭스의 POWER +5V에 꽂아도 작동한다.

LED 매트릭스 전원 핀에 일반 점퍼 와이어를 힘줘서 잘 끼우면 겨우겨우 들어간다.

![전원연결](https://github.com/16Yongjin/16Yongjin.github.io/assets/22253556/dec577db-6a87-4a5e-9fdd-d734c38f960c)

### 컨트롤러 조립

아래 영상을 보고 컨트롤러를 조립한다.

버튼마다 핀을 하나씩 배정하면 ESP32 - 컨트롤러 간 케이블이 7개 필요하지만,

영상의 방식대로 하면 케이블이 3개만 있으면 돼서, 선정리가 편하다.

<iframe width="560" height="315" src="https://www.youtube.com/embed/Y23vMfynUJ0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

납작한 U자 점퍼 와이어를 쓰면 깔끔한 컨트롤러를 만들 수 있다.

![컨트롤러](https://github.com/16Yongjin/16Yongjin.github.io/assets/22253556/821440cd-03e3-4f51-9e37-f9945d155175)

3.3v, 접지를 연결하고 빵판 J1번 소켓을 ESP32 33번핀과 연결한다.

### 실제 연결된 모습

ESP32 어댑터를 써서 선 연결도 쉽고, LED 매트릭스에 결합하기도 쉬웠다.

![선연결](https://github.com/16Yongjin/16Yongjin.github.io/assets/22253556/07af4efb-9cd1-4812-8b7a-889c59555cf8)

## 코드 짜기

### 아두이노 환경 설정

1. [아두이노 IDE](https://www.arduino.cc/en/software)를 설치한다.

2. 설정에서 아래 ESP32 펌웨어 설정을 추가한다.

   - https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_index.json

   ![아두이노 IDE 설정](https://github.com/16Yongjin/16Yongjin.github.io/assets/22253556/6b85e112-48b9-48a9-bb9f-1c1b377c84b4)

3. 아래 깃헙에서 zip 파일 다운로드 후, 아두이노 IDE 라이브러리에 zip 파일을 추가한다.

   - [ESP32-HUB75-MatrixPanel-DMA](https://github.com/mrfaptastic/ESP32-HUB75-MatrixPanel-DMA)
   - [Adafruit-GFX-Library](https://github.com/adafruit/Adafruit-GFX-Library)
   - [Adafruit_BusIO](https://github.com/adafruit/Adafruit_BusIO)

4. 포트 USB 어쩌구저쩌구로 설정
5. 보드는 ESP32 Dev Module 설정
6. 업로드 속도는 115200

### 테스트 해보기

예제 파일을 열어서 ESP32에 업로드 해본다.

![예제 파일 열기](https://github.com/16Yongjin/16Yongjin.github.io/assets/22253556/dad76c63-fbd4-4934-b465-6e2797806a38)

아래 사진 뜨면 정상이다.

![예제 파일 작동 사진](https://github.com/16Yongjin/16Yongjin.github.io/assets/22253556/f8b1bb89-dca1-4958-8ef0-c21d063ee431)

### 소스 코드

눌린 버튼 색상에 따라 텍스트를 그리는 코드이다. (너무 자세한 로직은 생략했음)

```c
#include <ESP32-HUB75-MatrixPanel-I2S-DMA.h>

// 버튼 설정
#define BUTTON_PIN 33

const int None = 0;
const int BlackButton = 1 << 0;
const int WhiteButton = 1 << 1;
const int RedButton = 1 << 2;
const int GreenButton = 1 << 3;
const int BlueButton = 1 << 4;

int currentButtonColor = WhiteButton;

// LED 매트릭스 설정
MatrixPanel_I2S_DMA *dma_display = nullptr;

uint16_t myBLACK = dma_display->color565(0, 0, 0);
uint16_t myWHITE = dma_display->color565(128, 128, 128);
uint16_t myRED = dma_display->color565(128, 0, 0);
uint16_t myGREEN = dma_display->color565(0, 128, 0);
uint16_t myBLUE = dma_display->color565(0, 0, 128);

#define R1_PIN 25
#define G1_PIN 27
#define B1_PIN 26
#define R2_PIN 14
#define G2_PIN 13
#define B2_PIN 12
#define A_PIN 23
#define B_PIN 19
#define C_PIN 5
#define D_PIN 17
#define E_PIN -1
#define LAT_PIN 4
#define OE_PIN 15
#define CLK_PIN 16

HUB75_I2S_CFG::i2s_pins _pins={R1_PIN, G1_PIN, B1_PIN, R2_PIN, G2_PIN, B2_PIN, A_PIN, B_PIN, C_PIN, D_PIN, E_PIN, LAT_PIN, OE_PIN, CLK_PIN};

void setup() {
  Serial.begin(115200);

  HUB75_I2S_CFG mxconfig(64, 32, 1, _pins);

  // Display 설정
  dma_display = new MatrixPanel_I2S_DMA(mxconfig);
  dma_display->begin();
  dma_display->setBrightness8(120);
  dma_display->clearScreen();

  updateButton(BlackButton);
}

void loop() {
  int buttonValue = analogRead(BUTTON_PIN);
  int buttonColor = getButtonColor(buttonValue);
  updateButton(buttonColor);

  delay(100);
}

// 눌려진 버튼 색깔 가져오기
int getButtonColor(int value) {
  if (value < 200) {
    return None;
  } else if (value < 300) {
    Serial.println("Black Button Clicked");
    return BlackButton;
  } else if (value < 700) {
    Serial.println("White Button Clicked");
    return WhiteButton;
  } else if (value < 1100) {
    Serial.println("Red Button Clicked");
    return RedButton;
  } else if (value < 1800) {
    Serial.println("Green Button Clicked");
    return GreenButton;
  } else {
    Serial.println("Blue Button Clicked");
    return BlueButton;
  }
}

// 버튼 색깔에 따라 화면 업데이트하기
void updateButton(int buttonColor) {
  if (buttonColor == 0) return;
  if (buttonColor == currentButtonColor) return;

  currentButtonColor = buttonColor;

  updateScreen(currentButtonColor);
}

// 화면에 텍스트 작성하기
void updateScreen(int buttonColor) {
  dma_display->setCursor(0, 0);
  dma_display->setTextSize(2);
  dma_display->setTextWrap(true);
  dma_display->fillScreen(myBLACK);

  if (BlackButton & buttonColor) {
    dma_display->fillScreen(myBLACK);
  }

  if (WhiteButton & buttonColor) {
    dma_display->setTextColor(myWHITE);
    dma_display->println("Name");
  }

  if (RedButton & buttonColor) {
    dma_display->setTextColor(myRED);
    dma_display->println("BUSY");
  }

  if (GreenButton & buttonColor) {
    dma_display->setTextColor(myGREEN);
    dma_display->println("TEA TIME");
  }

  if (BlueButton & buttonColor) {
    dma_display->setTextColor(myBLUE);
    dma_display->println("MEETING");
  }
}
```

## 기타

- 그냥 부품 사서 코드만 짜면 될 줄 알았는데, 시행착오가 많아서 완성에 한 달 넘게 걸렸다.
  - 5v 4a 어댑터를 연결해도 화면은 안 나오고 발열만 생겨서 고생했다.
  - 우연히 5v 선이 LED 파워 핀에 닿았는데, 화면이 제대로 나와서 겨우 완성함
- 소량 생산해서 팔아볼까 생각해봤다.
  - 근데 `원가 < 가격 < 가치`의 부등식을 통과하기 힘들 것 같아서 패스
  - 원가 5만 원에 판매가격 7만 원으로 잡았는데, 과연 이게 구매자에게 7만 원 이상의 가치를 주는가?
  - 기술혁신을 해서 원가를 3만 원 아래로 내리고 5만 원에 판매할 수도 있지만
  - 시장이 너무 작고, 그 시간에 다른 일 하는 게 나을 듯...
- GIF 재생도 가능하다.
  - 32 x 16 크기의 GIF 중 괜찮은 걸 못 찾았고
  - GIF 프레임 렌더링 중에 버튼을 눌러서 인터럽트 하는 코드를 못 짜겠어서 패스
