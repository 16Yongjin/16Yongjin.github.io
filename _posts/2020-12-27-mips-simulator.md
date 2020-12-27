---
title: MIPS 시뮬레이터
date: 2020-12-27T21:00:00+09:00
author: yongjin0802
categories:
  - Development
---

Vue.js로 구현한 온라인 MIPS 시뮬레이터

![image](https://user-images.githubusercontent.com/22253556/103166802-fb02de80-4868-11eb-9e25-625a87ea49a2.png)

GUI 앱 링크: [https://mips.surge.sh](https://mips.surge.sh)

GUI 깃헙: [https://github.com/16Yongjin/mips-simulator-in-vue](https://github.com/16Yongjin/mips-simulator-in-vue)

CLI 링크: [https://repl.it/@yongjin0802/mips-simulator-team-0x03](https://repl.it/@yongjin0802/mips-simulator-team-0x03)

## 제작 이유

컴퓨터 구조 수업 과제로, 원래는 C언어로 MIPS 시뮬레이터 CLI만 만들면 됐다.

하지만, 과제 설명에 쓰여있는 _(Option) GUI 구현_ 이 FE 개발자의 도전 정신을 불러일으켰다.

![image](https://user-images.githubusercontent.com/22253556/103166924-2e923880-486a-11eb-8ae2-a8bb08196614.png)

# 파트 1. C언어로 CLI 구현하기

## 프로그램 실행 과정

명령어 실행 시, PC가 가리키는 메모리 주소에서 명령어 바이너리를 읽고 PC를 4 증가시킨다.

명령어를 파싱 해서 명령어마다 구현된 별도의 함수를 실행한다. (ex, `sll(rd, rt, sh)`, `add(rd, rs, rt)`, ...)

해당 함수에서 레지스터, 메모리, ALU를 조작하면서 명령어의 기능을 수행한다.

## 환경 조성

팀원과 협업을 위해 Repl.it 온라인 IDE를 사용했다.

ALU, 레지스터, 메모리 등의 구성요소를 파일별로 나누고

유저 입력 처리, 바이너리 파일 파싱, 디버깅·에러 로거 등 어렵거나 귀찮은 부분을 구현했다.

그리고 나머지 부분은 팀원들이 할 수 있게 환경을 조성했다.

## 외과 수술 팀

멘 먼스 미신이란 책에서 효율적인 팀 구조로 **"외과 수술 팀"** 을 언급했다.

> 소수의 그룹에서 리더 한 사람이 목표를 정하면, 나머지 팀원은 리더가 정한 방향에 맞게 리더를 도와 생산성과 효율성을 증대시킨다.
>
> 이때 리더는 목표를 달성하기 위해 팀원들의 역할을 적절히 분배하고 이것을 다시 합치는 역할을 한다.

팀장으로서 프로그램의 구조와 인터페이스를 정하고

각 인터페이스마다 구현 담당자를 배정하고 구현 방법을 기술했다.

![image](https://user-images.githubusercontent.com/22253556/103167574-79627f00-486f-11eb-903e-5019e7cae432.png)

팀원은 단순히 할당된 함수를 명세에 따라 구현하기만 하면 돼서 편하고

팀장인 나는 반복적이고 양이 많은 구현 부분을 팀원에게 맡길 수 있어서 편했다.

## 구현과 인터페이스의 분리

구현이 하나도 안 되어 있어도,

인터페이스만 있으면 이를 합쳐서 또 다른 인터페이스를 만들 수 있고 프로그램도 완성시킬 수 있다.

### 예시

`stepProgram` 함수는 명령어 하나를 실행한다.

`stepProgram` 함수와 내부에서 사용된 함수들(`sll`, `and`, ...)은 실행에 성공하면 0, 실패하거나 프로그램 완료 시 1을 반환하는 인터페이스를 갖는다.

![image](https://user-images.githubusercontent.com/22253556/103167947-d1e74b80-4872-11eb-8727-280889702db0.png)

내부 함수들(`sll`, `and`, ...)은 구현이 완료되지도 않았는데 `stepProgram` 함수는 완성됐다.

`goProgram` 함수는 명령어 전체를 실행한다.

`goProgram` 함수는 무한 루프 속 `stepProgram`이 1을 반환하면 실행을 멈춘다.

![image](https://user-images.githubusercontent.com/22253556/103167924-a49a9d80-4872-11eb-86b2-e974fec63d2c.png)

`goProgram` 함수 또한, `stepProgram` 함수가 내부 구현이 완료되지 않아 실제 실행 시 정상적으로 작동하지 않더라도 완성됐다.

### 그래서 드는 생각

프로그램 전체의 개발 기간은 측정하기 힘들지만, 내부 함수 구현 하나하나의 개발 기간은 측정하기 쉽다.

인터페이스로 프로그램을 완성하고 작은 함수 각각의 개발 기간만 합치면 프로그램 개발 기간을 정확하게 측정할 수 있지 않을까 싶다. (작은 프로그램에서만 가능하겠지만)

&nbsp;

# 파트 2. 프로그램 포팅하기

C로 프로그램 구현을 마치고 어떻게 GUI를 구현할까 고민을 했다.

1. 기존 프로그램에 C나 C++ GUI 라이브러리 연동하기

2. 기존 프로그램을 웹 어셈블리로 컴파일해서 브라우저에 올리고 UI 붙이기

3. 기존 프로그램을 TypeScript로 포팅하고 Vue.js 붙이기

## C++ GUI 라이브러리 연동 시도

C++ 라이브러리로 스타 2.6만 개를 받은 [ImGui](https://github.com/ocornut/imgui) 도입을 고려했다.

API가 직관적이고 버튼 이벤트 핸들러 등록 방식이 특이하게 if 문에 UI 컴포넌트를 넣는 방식이다.

```cpp
if (ImGui::Button("Save"))
    MySaveFunction();
```

하지만 도입에 다음과 같은 난관이 있어서 포기했다.

1. 개발 환경을 Repl.it에서 Visual Studio로 옮겨야 함
2. C와 C++이 다른 점이 생각보다 많고, 엄격한 코드 규칙으로 인해 코드를 거의 다 재작성해야 함
3. C++로 복잡한 UI 구현과 상태 관리를 할 자신이 없음

## 웹 어셈블리 사용하기

[Compile C Language Into WebAssembly](https://youtu.be/_pHgILVlx3c) 강의를 보고 C 언어 함수를 JS 상에서 쉽게 호출할 수 있었다.

그런데, WASM은 프로그램 통째를 올리거나, 작은 FFI 함수 단위로 불러와서 사용하기 용이한 것 같은데

프로그램을 전부 올리기 위해서는 WASM과 호환되지 않는 라이브러리는 제거해야 한다.

또한, 시뮬레이터와 UI 간 연동을 위한 함수도 모두 정의해야 하고, 언어 데이터 변환도 해야 하는 등 적용하기 까다로운 점이 많다.

이럴 바엔 그냥 TypeScript로 시뮬레이터를 다시 구현하는 게 낫겠다고 생각이 들었다.

## 타입스크립트로 포팅하기

시뮬레이터 구현에 사용이 편리한 Python을 사용할 수 있었지만, 로우 레벨 프로그래밍의 용이함을 위해 굳이 C언어를 사용했다.

그래서 과연 JS 환경에서 로우 레벨 프로그래밍을 할 수 있을까 의심이 됐지만, 하다 보니 됐다.

### `unsigned int`, `signed int` 형변환

`>>> 0` 연산을 하면 `int`가 `unsigned int`가 되고, `>> 0` 연산을 하면 그 반대가 된다.

```js
;-1 >>> 0 // 4294967295

4294967295 >> 0 // -1
```

### 바이너리 파일 읽기

1. `<input type="file" />` 태그에서 파일 입력을 받는다.

2. 파일을 `ArrayBuffer`로 읽는다.

```js
const file = e.target.files[0]
const arrayBuffer = await file.arrayBuffer()
```

3. `ArrayBuffer`를 `Uint8Array`에 넣어서 `buffer`로 만든다.

```js
const buffer = new Uint8Array(arrayBuffer).buffer
```

4. `buffer`를 `DataView`에 넣어서 `view`를 만든다.

```js
const view = new DataView(buffer)
```

5. `view`에 `.getUint32()` 메서드를 호출해서 바이너리를 읽는다.

```js
for (let i = 0; i < wordCount; i++) {
  const word = view.getUint32(4 * i)
}
```

&nbsp;

# 파트 3. GUI 구현하기

![image](https://user-images.githubusercontent.com/22253556/103166802-fb02de80-4868-11eb-9e25-625a87ea49a2.png)

## UI 컨셉

단지 동작하는 것을 넘어서 심미적으로 만족감을 주는 디자인과 유저가 원하는 기능을 바로 찾아 쓸 수 있는 UI 구성을 고민했다.

디자인이 진부하고 UI가 사용하기 불편하다면 CLI와 다름이 없기 때문이다.

힙한 Big Sur 배경에 트렌디한 Glassmorphism을 적용했다.

테두리는 둥글게, 각 요소 간 간격은 넓게, 배경은 화려하고 살짝 불투명하게 한 것뿐이지만, 기존의 머티리얼 디자인처럼 질리지 않아서 만족한다.

## CTA

![image](https://user-images.githubusercontent.com/22253556/103170469-d0744e00-4887-11eb-8608-b3362e02d71e.png)

우상단의 명령어를 한 단계 씩 실행하는 버튼과 프로그램 전체를 실행하는 버튼이 있다.

## 명령어 패널

![image](https://user-images.githubusercontent.com/22253556/103170474-dcf8a680-4887-11eb-916c-fbeedf29a225.png)

### 중단점

왼쪽 빨간 버튼을 누르면 중단점이 설정된다.

### 바이너리 파일 불러오기

_리스트 버튼_ 을 누르면 이미 작성된 바이너리 파일을 불러올 수 있다.

직접 작성한 파일을 불러오려면 옆에 _파일 추가 버튼_ 을 누르면 된다.

\* 바이너리 형식은 빅 엔디안에 `명령어 개수`, `데이터 개수`, `명령어`, `데이터`로 구성되어 있다.

![image](https://user-images.githubusercontent.com/22253556/103170482-ebdf5900-4887-11eb-9352-1841df3f3818.png)

### 명령어 작성

MIPS 명령어 직접 입력해서 프로그램을 실행할 수 있다.

테스트 프로그램을 작성하기 위해 바이너리를 다루는 게 귀찮아서 MIPS 명령어 파서를 구현했다.

명령어에 따라 12 종류의 정규식을 작성해서 간단히 구현했고, Syntax 에러도 막는다.

![image](https://user-images.githubusercontent.com/22253556/103170477-e5e97800-4887-11eb-98dc-b6faa8f44a19.png)

## 레지스터 패널

### 레지스터 변경 감지

명령어 실행 전후로 레지스터의 스냅샷을 찍어서 비교한 뒤 변경된 레지스터를 파악한다.

![image](https://user-images.githubusercontent.com/22253556/103170632-0534d500-4889-11eb-9e3a-c84e60431da5.png)

### 레지스터 수정

레지스터를 선택하면 레지스터를 수정할 수 있다.

PC를 수정하면 프로그램 실행 위치도 변경할 수 있다.

![image](https://user-images.githubusercontent.com/22253556/103170636-10880080-4889-11eb-9798-510e29b78c0e.png)

## 데이터 패널

![image](https://user-images.githubusercontent.com/22253556/103170639-15e54b00-4889-11eb-860e-728f20d96d30.png)

### 가상 스크롤러 사용

데이터가 100만 개 이상의 Uint8 배열로 이루어져 있다.

이를 다 보여주려면 25만 개 이상의 div 요소가 필요한데,

메모리 낭비를 막기 위해 Vuetify가 제공하는 가상 스크롤러를 사용했다.

### 데이터 메모리 변경 감지

Uint8 배열 요소 100만 개에 Vue Observable을 붙여서 데이터 변경을 감지하는 것은 리소스 소모가 크다.

대신에, 메모리 수정 시 `Vue.$forceUpdate()`를 호출하고 데이터 패널에 `:key="Math.random()"`를 붙여서

UI가 업데이트될 때마다 강제로 데이터 패널이 업데이트되도록 했다.

Vue는 변경이 있을 때만 UI를 업데이트하므로 이런 방식이 생각보다 비효율적이지 않다.

## 스택 패널

스택이라는 컨셉에 맞게 데이터가 아래에서 위로 쌓이는 모습을 보여준다.

![image](https://user-images.githubusercontent.com/22253556/103170647-24cbfd80-4889-11eb-8f2b-3bb7c9872853.png)

## 콘솔 패널

CLI에서 쓰는 명령어를 GUI에서도 사용할 수 있게 했다.

디버그 로그도 콘솔에 나타나서 프로그램 실행을 더 잘 파악할 수 있다.

![image](https://user-images.githubusercontent.com/22253556/103170652-2eedfc00-4889-11eb-98a9-f73cad80409a.png)

&nbsp;

# 마무리 느낀 점

## 웹이 미래다.

- C언어 구현도 웹 IDE를, GUI 구현도 웹 기술을 (심지어 VS Code도 웹 기반), 발표자료 만들 때도 온라인 구글 프레젠테이션을 사용했다.
- 기존 프로그램들이 모두 웹으로 옮겨지고 있다. 이런 상황에서 웹에서 로우 레벨을 다루는 기술은 더욱 중요해질 것이라고 생각한다.

## 아키텍처와 프로젝트 관리의 재미

- 프로그램을 여러 구성요소로 나누고 합쳐서 아키텍처를 구성하는 것도 재밌고
- 각 구성요소를 작은 함수로 나눈 뒤 실행 가능한 업무로 만들어서 팀원들에게 분배하는 것도 생각보다 재밌다.
- 개발자로 오래 일하려면 프로그래머로 남으라는데, 그래도 프로그래머, 아키텍트, PM 역할을 다 잘하고 싶다.
