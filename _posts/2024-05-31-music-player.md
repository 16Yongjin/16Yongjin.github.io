---
title: 나를 위한 음악앱 만들기
date: 2024-05-31T16:00:00+09:00
author: yongjin0802
categories:
  - Development
---

유튜브 프리미엄에서 독립하기

---

유튜브 프리미엄 가격이 올랐다.

1년으로 치면 거의 20만 원 돈

담배값 2,500원에서 4,500원으로 오를 때 아부지가 금연하신 것처럼

나도 이참에 유튭을 끊어보려고 했다.

근데 음악은 못 끊겠다.

유튭 프리미엄 한 달에 15,000원 아끼려다가

앱 디자인 영감을 얻는다고 비싼 카페에 가고

잘못 짠 코드 때문에 데이터 100기가 쓰고 통신비 2만 원 더 나와서

돈은 더 쓰게 됐지만

매일매일 잘 쓰고 있는 음악앱 개발기를 써본다.

![아이패드](https://github.com/16Yongjin/16Yongjin.github.io/assets/22253556/3fefc2b2-bc06-4485-a071-4b76b3e7d195)

(아이패드에 띄웠을 때 가장 예쁘다)

![유니버셜앱](https://github.com/16Yongjin/16Yongjin.github.io/assets/22253556/abe24137-e869-4675-b853-1ce56ea91ab2)

(모바일 폰, 패드 화면을 모두 지원한다)

## 음악이 너무 듣고 싶다

5월 1일 유튜브 프리미엄 구독이 끊겼다.

출근길 지하철에서 매일 듣던 음악이 모두 사라졌다.

참다 참다 제일 듣고 싶은 음악 1곡을 힘들게 다운로드 받아서 들었는데

3일 만에 귀에 드럼, 기타 소리가 터져나오니까 살 것 같았다.

음악을 들을 방법은 여러 가지 있었지만 (회사에서 지원하는 멜론, 내장 아이폰 음악 앱 등등)

음악을 선택하고 재생하고 앨범 사진까지 바라보는 경험을 내가 원하는 방식으로 즐기고 싶었다.

애플 뮤직의 둥글한 디자인과 따스한 느낌을 주는 그러데이션 배경도 갖고 싶었다.

![ipad-music-app](https://github.com/16Yongjin/16Yongjin.github.io/assets/22253556/979ceca7-10e4-42a0-ae88-dbadd1ed0430)

(아이패드의 애플 뮤직과 유튜브 뮤직)

그래서 홀린 듯이 노트에 앱 레이아웃만 그려놓고 언젠가 만들어야겠다고 다짐만 했다.

## 불편한 상황으로 나를 몰아넣기

음악앱 없이 다운로드 받은 2곡만 노래만 계속 들으니까 너무 물렸다.

아이폰 파일 앱으로 음악 듣는 것도 매우 불편했다. 한 곡이 끝나면 다시 음악 파일을 선택해 줘야 한다.

그렇다고 음악앱을 만드는 건 시간이 오래 걸리니까 계속 미루다가

일단 너무 듣고 싶은 노래 10곡을 모았다. 앨범 사진도 한땀한땀 구하고 노래명과 가수명을 잘 정리해 뒀다.

이 노래들을 내가 만든 음악앱에서 들을 때까지 음악은 안 듣기로 했다.

즉, 음악을 들으려면 음악앱을 만들 수밖에 없는 상황을 만들었다.

## 디자인과 마크업 만들기

![figma](https://github.com/16Yongjin/16Yongjin.github.io/assets/22253556/f490317d-3361-4128-839f-f0890990886e)

애플 뮤직을 레퍼런스 삼아서 디자인하고

![마크업](https://github.com/16Yongjin/16Yongjin.github.io/assets/22253556/4b08f7c0-3751-43a4-8928-edaa7db46a41)

마크업을 구현했다.

Vue, Svelte만 쓰다가 React도 공부할 겸 React와 Tailwind를 사용했는데

탑-다운으로 마크업을 나누고 조합하는 방식은 React에서도 먹히는 것 같다.

스타일드 컴포넌트를 쓰면 자연스럽게 되는 방식인데 테일윈드와도 잘 어울린다.

## 음악 재생 로직 구현하기

브라우저에서 음악 재생하는 코드는 매우 간단하다.

```ts
const audio = new Audio(src);

audio.play();
```

여기에 정지/다음/이전 기능을 구현하고

노래가 끝났을 때 `ended` 이벤트에 맞춰서 다음 곡으로 넘어가게 하면

음악을 듣기에 충분하다.

## 그레디언트 배경

음악은 듣기도 하지만 보기도 한다.

앨범 사진과 노래명, 가수의 이름이 주는 설렘이 있다.

[grade](https://benhowdle89.github.io/grade/) 라이브러리를 쓰면 사진에서 예쁜 그래디언트 배경을 만들어준다.

다만 돔 요소에 직접 CSS를 삽입하는 방식이라 리액트와 어울리지도 않고 콜백 방식의 인터페이스가 불편하다.

다행히 코드가 200줄도 안 되는 파일 하나짜리 라이브러리라서

소스코드 가져다가, 실행하면 그래디언트 문자열을 프라미스로 반환하는 간단한 함수를 만들었다.

### 그래디언트 배경 트랜지션

![gradient](https://github.com/16Yongjin/16Yongjin.github.io/assets/22253556/ea366e0e-2ca6-4134-81c7-d751dd1fc3ec)

다음 곡으로 넘어갈 때 배경 색상이 자연스럽게 스르륵 바뀌었으면 좋겠는데

그래디언트 배경을 적용할 때 `background-image` CSS 속성은 트랜지션이 적용되지 않아서

배경 색상이 뚝뚝 끊겨서 바뀐다.

대신에, 이전 배경 색상을 보여주고 있다가,

다음에 바뀔 배경 색상의 `opacity`를 0에서 1로 천천히 바꿔서 보여주면

색상 트랜지션이 일어나는 것처럼 보인다.

<details>
<summary>배경 전환 코드</summary>

```tsx
const useGradient = (imageSrc: string) => {
  const [gradient, setGradient] = useState(DEFAULT_GRADIENT);

  useEffect(() => {
    const updateGradient = async () =>
      setGradient(await createGradient(imageSrc));

    updateGradient();
  }, [imageSrc]);

  return gradient;
};

const useGradientTransition = (gradient: string) => {
  const [previousGradient, setPreviousGradient] = useState(gradient);
  const isTransitioning = gradient !== previousGradient;

  useEffect(() => {
    const timeout = setTimeout(() => setPreviousGradient(gradient), 1000);

    return () => clearTimeout(timeout);
  }, [gradient]);

  return { previousGradient, isTransitioning };
};

const ImageGradientBackground: React.FC<Props> = ({ src }) => {
  const gradient = useGradient(src);
  const { previousGradient, isTransitioning } = useGradientTransition(gradient);

  return (
    <div
      className={`
				before:bg-[image:var(--previous-gradient)]
				after:bg-[image:var(--gradient)] after:duration-1000 
				${isTransitioning ? "after:opacity-1" : "after:opacity-0"}
			`}
      style={{
        "--gradient": gradient,
        "--previous-gradient": previousGradient,
      }}
    ></div>
  );
};
```

</details>

## 음악을 재생하면 뜨거워지는 아이폰

![데이터 사용](https://github.com/16Yongjin/16Yongjin.github.io/assets/22253556/5f4ea53b-ebbe-4ffa-84db-cbcdd3e750f4)

(200기가 쓴 사파리)

음악앱을 완성해서 쓰기 시작한 지 얼마 안 돼서 이상한 일이 많이 생겼다.

Netlify에 배포했는데 5일만에 무료 대역폭 100기가를 넘었다고 경고 메일이 왔고

음악을 듣기만 하면 아이폰 사과 윗부분이 엄청나게 뜨거워지고 배터리가 엄청 빠르게 닳았다.

아이폰을 맥과 연결해서 사파리 디버거를 켜보니

음악을 재생할 때마다 네트워크 요청이 미친 듯이 가고 있었는데

문제의 원인은 아래 `useRef` 코드 한 줄 때문이었다.

```ts
export const useMusicPlayer = () => {
  ...

  const audio = useRef(new Audio(src));

  ...
}
```

음악 재생시간을 업데이트하기 위해 1초에 2번 리렌더링이 일어나는데

그때마다 오디오 객체가 생성되고 사파리 브라우저(맥/ios 둘다)에서는 음악 파일이 새로 로딩됐다.

개발할 때 크롬만 써서 몰랐는데 아이폰용 웹앱을 만들 때는 사파리에서 테스트를 꼭 해봐야겠다..

글고 리액트 공부한다고 나름 책도 읽었지만, 결국 만들어서 직접 경험해보는 게 최고인 거 같다.

### Audio 객체 재생성 해결

렌더링될 때마다 `Audio` 객체가 새로 생성되는 것만 막으면 된다.

`Audio` 객체는 한번 만들어서 앱 전체에서 계속 쓰니까 싱글턴으로 만들어서 해결했다.

```ts
const audio = new Audio();

export const useMusicPlayer = () => {
  ...
}
```

`useEffect()`에서 한번 `ref.current` 값을 넣어주는 방법도 있지만 `.current` 코드를 안 쓰고 싶기도 하고

`useState()`나 `useMemo()`를 쓰는 방법은 `useEffect` 의존성 배열에 넣어줘야할 코드가 많이 늘어나서 피했다.

## 드래그 앤 드롭으로 네이티브 앱 같은 사용 경험 만들기

노래 순서를 바꿀 때는 [dnd kit](https://dndkit.com/)를

![dnd](https://github.com/16Yongjin/16Yongjin.github.io/assets/22253556/dcce1501-a00d-40ce-87d3-10327ca1a90b)

플레이어를 열고 닫을 때는 [react-modal-sheet](https://github.com/Temzasse/react-modal-sheet)를 (내부적으로 framer motion을 쓴다.)

![album open](https://github.com/16Yongjin/16Yongjin.github.io/assets/22253556/cd45c105-2319-4e1f-b205-70c0c7b47dcb)

앨범 사진을 슬라이드해서 둘러볼 때는 [framer-motion](framer.com/motion/)를 사용했다.

![album slide](https://github.com/16Yongjin/16Yongjin.github.io/assets/22253556/5ad8bdba-6655-4778-a15c-4d0e3186ca26)

하나의 드래그 앤 드롭에서 발생하는 버그를 잡는 것뿐만 아니라

여러 라이브러리가 한 번에 사용됐을 때 발생하는 충돌을 해결해야 하느라 신경 쓸 게 많았다.

### 1. 스크롤이 있는 목록에서 항목 드래그하기

터치 기기에서는 드래그와 스크롤 이벤트가 구분 없이 동시에 일어난다고 한다.

항목을 집어서 드래그하고 있으면, 뒤에 있는 목록 요소에 스크롤이 발생해서 화면이 울렁거린다.

드래그 손잡이 요소에 `touch-action: none;` (테일윈드 `touch-none` 클래스)을 붙이면 해결된다.

### 2. 모달 시트 드래그 이벤트 막기

모달 시트가 드래그를 다 먹어버려서 재생시간 슬라이더가 먹통이 됐다.

아래 코드를 추가하면 모달 시트로 가는 스크롤 이벤트가 막히면서 재생시간 슬라이드가 가능해진다.

`onPointerDownCapture={(e) => e.stopPropagation()}`

### 3. 노래 드래그 중엔 모달 시트 드래그 비활성화하기

`onPointerDownCapture`로 이벤트 전파를 막으면 모달 시트뿐만 아니라 dndkit의 드래그까지 막힌다.

`DndContext`에 `onDragStart`, `onDragEnd`로 현재 노래 드래그 중임 상태를 알아내서

노래를 드래그 중일 땐 모달 시트를 비활성화해서 해결했다.

### 돔 이벤트 발생 절차

1. 윈도우에서 이벤트가 캡쳐돼서 아래로 내려감
2. 타겟 요소에서 이벤트가 발생
3. 이벤트가 버블링돼서 위로 올라감

### 드래그 관련 디버깅을 잘하려면 어떻게 해야할까

소스코드를 분석하든가, 직접 실험해서 동작을 파악하든가 해서

라이브러리가 이벤트를 어떻게 처리하는지에 대한 최소한의 멘탈모델을 들고 있어야

빠른 버그 수정이 가능해지는 것 같다.

## 성능이 좋은 라이브러리가 최고일까?

노래 순서 정렬 기능을 구현하기 위해

처음엔 아틀라시안에서 새로 나온 [Pragmatic Drag and Drop](https://github.com/atlassian/pragmatic-drag-and-drop)을 쓰려고 했다.

이 라이브러리엔 장점이 많다.

- 모든 프레임워크에서 사용할 수 있고
- 라이브러리 제작자는 드래그앤드롭에만 몇 년씩 문제를 해결해 왔고
- 요소 이미지 캡쳐를 통해 저성능 기기에서도 높은 FPS를 유지하는 성능이 나오고
- 핵심 기능만 트리셰이킹으로 번들에 포함해서 앱 초기 로딩속도도 높일 수 있다.

그런데 유튜브 뮤직처럼 부드러운 드래그 경험을 만들려면 내가 작성해야 할 코드가 많다.

프로토타이핑 조금 해보다가 힘들어서 [dnd kit](https://dndkit.com/)을 채택했는데 매우매우 만족한다.

이미 라이브러리에서 제공하는 기능을 잘만 조합하니까 원하는 기능을 바로 만들어 낼 수 있었다.

작성할 코드도 적고 명시적이라 나중에 관리하기 편해 보인다.

현재까지 성능 이슈도 아직 못 느꼈고 내가 바라는 대로 예쁘게 잘 작동해서 맘에 든다.

성능이 사용자에게 정말 가치를 주는지와

성능을 위해 개발자의 시간이 희생되는 건 아닌지를 잘 따져서 적절한 라이브러리를 채택하는 게 중요해 보인다.

## 앱 전체 리렌더링 막기

음악 플레이어의 상태와 로직을 가진 훅을 정의하고

최상단 컴포넌트에서 컨텍스트로 넣어준 훅을 앱 전체에서 사용하는 구조를 사용했다.

그러니까 상태가 하나만 바뀌어도 앱 전체가 리렌더링됐다.

이건 좀 아닌거 같아서

[Making React Context FAST!](https://youtu.be/ZKlXqrcBx88) 영상을 보고 상태 변경 시 컴포넌트 렌더링을 최소화하는 방법을 알았는데

1. `useState()`가 아닌 `useRef()`로 상태를 들고 있는다.
2. 상태를 사용하는 컴포넌트는 `useEffect`로 상태의 변화를 감지할 수 있는 콜백을 등록한다.
3. 상태 변경 시, 콜백을 실행한다.

근데 요게 `useSyncExternalStore()`가 하는 일이고

관련 코드를 직접 작성하는 것보단, 그런 코드가 이미 작성된 Zustand를 쓰는 게 나아 보였다.

### Zustand `useShallow` 미들웨어 사용하기

Zustand를 썼는데도 select하지 않은 상태의 변경에도 컴포넌트 리렌더링이 발생했다.

자동으로 `useShallow`를 적용해 주는 미들웨어를 정의해서

selector 작성 코드도 줄이고, 얕은 객체 비교로 진짜로 상태가 변경됐을 때만 렌더링을 발생시키게 했다.

<details>
  <summary>useShallow 미들웨어</summary>

```ts
import { StoreApi, UseBoundStore } from "zustand";
import { useShallow } from "zustand/react/shallow";

type GenericState = Record<string, unknown>;

export const createStoreWithSelectors = <T extends GenericState>(
  store: UseBoundStore<StoreApi<T>>
): (<K extends keyof T>(keys: K[]) => Pick<T, K>) => {
  const useStore: <K extends keyof T>(keys: K[]) => Pick<T, K> = <
    K extends keyof T
  >(
    keys: K[]
  ) => {
    return store(
      useShallow((state) =>
        keys.reduce((acc, key) => {
          acc[key] = state[key];
          return acc;
        }, {} as Pick<T, K>)
      )
    );
  };

  return useStore;
};
```

```ts
const { currentTrack, playlist } = useMusicPlayerStore([
  "currentTrack",
  "playlist",
]);
```

</details>

## 플레이리스트 자동생성 스크립트

유튜브에서 오디오를 하나씩 다운로드 받고, 구글 이미지에서 앨범 커버를 하나씩 찾아서 음악을 모으고 있었는데

너무 오래 걸리고 힘들어서 조금씩 자동화하기 시작했다.

지금은 음악 제목과 유튜브 링크 배열만 넣어주면

1. [yt-dlp](https://github.com/yt-dlp/yt-dlp)로 유튜브에서 음악 파일 다운로드
2. 스포티파이 API에서 음악 정보와 앨범 사진 다운로드
3. Sharp.js로 썸네일 이미지 생성
4. 플레이리스트 JSON 파일 생성이 자동으로 된다.

## 마무리

- 돈이 없으면 좋아하는 음악을 못 듣게 되는 슬픈 일은 이제 발생하지 않는다.
- 회사를 위해 개발을 하다가 오로지 나만을 위한 제품을 만드니까 정말 즐겁다.
- 버그 고치러..
