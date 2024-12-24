---
title: 맥용 외장 Touch Id 버튼 만들기
date: 2024-12-24T21:00:00+09:00
author: yongjin0802
categories:
  - Development
---

외장 터치 아이디 버튼 제작기

![IMG_5994](https://github.com/user-attachments/assets/75dc018f-fe38-479e-9d4f-c718a2636cd7)

## 만들게 된 이유

맥북 화면을 닫고 모니터만 사용해서 일하고 있다.

지문인식으로 빠르게 로그인하기 위해 맥북을 여는 순간 화면 배치가 다 틀어져서 불편하다.

기계식 키보드가 좋아서 매직 키보드는 쓰고 싶지 않다.

터치 아이디만 똑 떼서 쓸 방법은 없을까?

<img width="500px" src="https://github.com/user-attachments/assets/ae430aa3-48aa-46a7-9464-0365240d6c9e" />

아쉽게도 이런 제품은 없다. [사진출처](https://basicappleguy.com/basicappleblog/themagicbutton)

## 나와 비슷한 고민을 한 사람들

책상 아래에 매직 키보드를 붙여서 터치 아이디만 사용하는 사람도 있고

매직 키보드에서 터치 아이디 분리해서 버튼으로 만든 사람도 있다.

<iframe width="560" height="315" src="https://www.youtube.com/embed/hz9Ek6fxX48?si=gUc-4JXVAev27KGn" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

터치 아이디를 트랙패드나 키보드에 붙여서 쓰는 사례도 있다.

<iframe width="560" height="315" src="https://www.youtube.com/embed/nl-3-w-riQ8?si=nRkoA6drQRGUHyoU" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/lyCmdgZI6WU?si=mGeJpy6sPCneW-Ts" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

책상 위에 거대한 매직 키보드 올려두고 싶진 않아서 단일 버튼을 만들어 보기로 결정했다.

## 만드는 방법

[Make your own Touch ID Button](https://gist.github.com/KhaosT/1406a6b6bea38f59e059c2afcb39d545) 문서에 잘 정리되어 있다.

### 1. 준비하기

#### 매직키보드

중고 매직키보드를 구매했다.

수십 개의 키 중에서 터치 아이디 1개만 동작하면 되므로

상태 상관없이 가장 저렴한 거 구매했다. (중고나라 8만 원)

![IMG_5979](https://github.com/user-attachments/assets/707e72bc-8000-4241-8fdc-2ca4798aee76)

![IMG_5981](https://github.com/user-attachments/assets/a2ca7248-58fd-4a45-ae57-f49661c70f5c)

#### 별 드라이버

키보드를 분해하는 데 필요한 드라이버도 구매했다.

별 드라이버 검색하면 나오는 단품 드라이버 살 필요 없이

비트가 여러 종류 들어있는 드라이버 세트를 사면 된다.

![IMG_5982](https://github.com/user-attachments/assets/75d73ee5-9a2f-4283-9a60-94361ff74f04)

7,000원에 구매

#### 3D 프린트된 케이스

크몽에서 도안만 주면 다 출력해 준다.

<img width="1000" alt="스크린샷 2024-12-25 오전 12 49 24" src="https://github.com/user-attachments/assets/cec0ffbf-fe97-4f62-9e10-43386c11e6f9" />

프린터블에서 가장 맘에 드는 모델을 골라서 대행업자에게 출력을 요청했다.

<img width="1000" alt="스크린샷 2024-12-25 오전 1 09 09" src="https://github.com/user-attachments/assets/00e23b91-c550-4f78-bde3-e210ab52a75f" />

> 출처: [Printable - Wired Touch ID case](https://www.printables.com/model/899849-wired-touch-id-case)

![IMG_5977](https://github.com/user-attachments/assets/c7caeea6-7c42-408c-b8e0-bca8bdd06ffa)
![IMG_5978](https://github.com/user-attachments/assets/68637b98-cb63-4cd6-9009-0c4a8532bf31)

생각보다 가격이 비쌌는데 (30,000원에 배송비 별도)

직접 3D 프린터를 구매해서 출력물 퀄리티를 위해 신경 쓰고, 출력 끝나고 관리하는 거 등등 생각하면 비싼 건 아닌 거 같다.

장비를 좋은 걸 쓰는지 실제 출력물을 보면 적층면이 안 느껴질 정도로 옆면이 매끈하게 잘 나와서 대만족이다.

## 분리하기

일자 드라이버를 빠루처럼 사용해서 뒷면 플라스틱을 분리했다.

![IMG_5983](https://github.com/user-attachments/assets/41107617-7076-4a95-a945-360eed23ef55)
![IMG_5984](https://github.com/user-attachments/assets/20f6ad87-0cad-4398-8a21-cd7ce37b48b4)

케이블들은 끊어지기 쉬우므로 라이브로 분리하는 영상을 따라 하면서 조심스럽게 떼냈다.

<iframe width="560" height="315" src="https://www.youtube.com/embed/5h-i6v3eVqM?si=zkXVKf5u49L5LRLq" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

분리한 터치 아이디 센서로 지문 인식을 해봤는데 맥북 잠금이 잘 풀린다. 성공적으로 분리했다.

![IMG_5985](https://github.com/user-attachments/assets/6e7254fb-8d5d-4f98-b155-28dea71a7c04)

### 조립하기

터치 아이디 센서와 라이트닝 단자를 끼우고 로직보드까지 결합한다.

![IMG_5987](https://github.com/user-attachments/assets/9fb9a6a0-6218-46b5-b347-95d553073953)

![IMG_5988](https://github.com/user-attachments/assets/8086c9a6-1687-4082-b7a6-c24b78f50745)

조립이 완료된 모습

![IMG_5989](https://github.com/user-attachments/assets/c4a9cfb3-341c-47d7-b8f4-4f293a4a9dd6)

---

지문인식 잘 된다.

<video width="100%" controls="controls">
  <source src="https://github.com/user-attachments/assets/856a0080-1493-4da7-a03c-e5eac941d17b" type="video/mp4">
</video>

## 앞으로 쓰면서 기대되는 것

- 맥북 잠금 해제할 때 비밀번호 입력 안 해도 된다.
- 업무망 로그인 할 때 Okta FastPass 써서 손가락만 올리고 있으면 된다.
