---
title: 깃헙처럼 안전하고 쓰기 편한 API 타입 정의하기
date: 2024-04-16T16:00:00+09:00
author: yongjin0802
categories:
  - Development
---

깃헙 Octokit 수준의 API 클라이언트 타입을 정의하고 생산적으로 사용하는 방법

---

깃헙 [octokit.js](https://github.com/octokit/octokit.js)는 최고의 API 사용경험을 제공합니다.

`request()` 함수를 사용하면 API 경로 뿐만 아니라 경로변수, 쿼리파라미터, 응답 타입까지 모두 타입이 완성됩니다.

![githuboctokit](https://github.com/16Yongjin/16Yongjin.github.io/assets/22253556/c212dd8e-9e57-4992-af20-15e7ae73df33)

Octokit은 깃헙의 OpenAPI 문서를 기반으로 별도의 [스크립트](https://github.com/octokit/openapi-types.ts/blob/main/scripts/generate-types.js) 작성해서 타입을 생성하고 있습니다.

스크립트 없이 순수 타입스크립트만 써서 API 타입을 만드는 방법을 소개합니다.

## 강력한 타입을 가지면서 쓰기 편한 API 클라이언트 만들기

아래처럼 메서드, 경로, 인자, 응답 타입 모두 추론되는 API 클라이언트를 만들 수 있습니다.

![apitypes](https://github.com/16Yongjin/16Yongjin.github.io/assets/22253556/2b6fd654-e5e6-4435-a255-c4e645eb0817)

### 1. API 엔티티 정의하기

예시로 사용할 간단한 `User` 엔티티를 정의합니다.

```ts
type User = {
  id: string;
  name: string;
};
```

### 2. API 인터페이스 정의하기

`User`를 만들고 가져오는 HTTP API 인터페이스를 정의합니다.

OpenAPI 형식을 간소화해서 경로 > 메서드 > 인자 + 출력으로 타입을 구성합니다.

```ts
type API = {
  '/users': {
    // 사용자를 생성함
    post: {
      body: Pick<User, 'name'>;
      response: User;
    };

    // 사용자 목록을 페이지네이션으로 가져옴
    get: {
      query: {
        page: number;
        size: number;
      };
      response: User[];
    };
  };

  '/users/:id': {
    // 특정 사용자를 가져옴
    get: {
      path: {
        id: string;
      };
      response: User;
    };
  };
};
```

### 3. API 인터페이스에서 API 호출 타입 만들기

코드가 길어서 [타입스크립트 플레이그라운드](https://www.typescriptlang.org/play?#code/MYewdgzgLgBAhgBwJYwLw2AJwKZytgQQAUBJAHgBURiSAlEAV3wjJoD42AKASgG4AofgHohaVOImTxMIgBs4ATxgB3JFAAWMAAaIkWmCABGAK2zBY4GADMQs2SFVgA5jAhmoSS1O8TBoSLC6AMrunmBo8BAKYMAwPGhsMADe-DAwImmZWdk5uVmAyYQwALLYGiAAJvBglfRM2PA4MEhgVtiYOOUAhKkY4NAwDG6YEXDKcGrwyAB0OACODNjQnADkAOIAohTpg20QQgBcSOXLADTJPWkIeOr75zlHt8sAjABMAMyn6aKACYQwVxowABucGGSAgTRabQ63SyAF8Tj1YXxBGkMplCrRFgg+vUoAoEPUwRDWu1sF0ejtMFMjgI0pSpmA4ABbbACHpovKcrlpDGMfBNcHNEnQnr+fqU8HoUbjQLTJylFZCCWfFJZDKFACKC0wSiIIOZ4JBhMhpPJWXmbQUt1V2Su8tuTwROQgSAAXtgHQAGC5pWEwRHI9miHIYrE4mB4gkC4lQskwgZDCAAbU9AF1qeVaQndin04yWQJYWyMj5vDJ5EpVACtJgEMB9EZTOYDOEbHYHM0XG5zGExKXUH4+rBa8AQj2vJForF4qhEjaOdzF1zCgAhCpKSOEwUmkVpMWwSkjMYTEdTelYXD4ThJGCGdfWmD5j0wZbGEDqMBTcogbDLGCwpE2VRYN0RgTEIGxSBcXxLcY1NeN6RpCkhgZZlWRRL4lywzlNW1XV9SZCMYOjIVYzNXoAmzTBJXgY9hzrM8UNkMEoGvGALR1B87WfR1XDdHjPX-QCMIXUDwMgtwiKjIlSPg5CczTDMswlXNUILfhYUEEt+wkGB1jADw8RgAARbArGaNRex0yRBE3GAAFUhgiG0HlcKBME7LMn1uaAPOcQs2TsogQH6dAXPKHz3M8npDNkZ9fOitI73KK03L8pwAq00RrOkGgTLMiyPC8HKB34Oy8rCnpliVRNlmtH15Sgeqcg41KbRybjbjABgmUMNos2dfiup6vrMAGzIix9NIcAgnFbkctok1TcbJqybFoGa7JktSogkGAABrMgFswM5lifZY2HG6awyg+ahhWrNJqqmrdgOI46ruTJGs2tbrh+7JXIS-ypv-K6YBmiTn2Oh7ESAl8hHWqAIA+9qYG+z7zTw-7fvtR8Rv6kG0hdd1ht6gmclW7IIbmmQQqgJaYbWunsdve8ZD2w7gugU7Yt-GAAB8X22i6wep27aegRnQYw6rEb2Q5jn+9HUcuP6MYBiK0sS7JKayMW3FuLmoCly4mBZ-4bnVrJAai4GKbB7bDY5sgjZ5tQ4r-QXlmFy6Qf158jZNmBymwOL8HNtWVcyG30rB3XMn9w26alyanu06yYAoYiAAlQ4Jai+2swdKJHZz5Mwf6LzwZ9dCmKxMBAJkViIAB5IIthe6jlm4J1MmYjbJiQOuG6btZNm2Wqe4a0pblr+vG5WDYO4lN7jin30ER6RHK5wavZ+mefR9b9v0jl7ve7SfumsH4eF7Hjuz-Xr6Z5vw-F-HhG6fl96n7pBByj3q-Eezd7IPy-qvc+PoQ5hxrgfYByxjLrAADKbHWKfcBCtIEbw0sWbKOVM45zzrsQuOlbLEQANLYAUC3KwlBEjoHWAAD3cnAcwZB9pUJAFYTOZwgZOF9mVYiBAEAEmqJQhQZByEwGwMw7A1RwREAbvnPE4izgUHoZ9JMRAIQwHETQuhkRtAABIkj2REW0YAcA3AuzYH6ExTDgCyAYCHSRvCFC9VsLYrQqZbgUC0ctHBZCoxFEQAANTgE4xYlBpGyPkQYEw7gNE2iTFI5oMAOEKC4ZnHxMBhGiPKOI1xmcUmpl9k9Oy4TIkQH0eoiIfiMlZIoAEwRUZ7JgDCFQEgBldihHAEdDRnB7IxPwHEuAYAlAAH44j7XmtwBIQIQBHBgF1bAgI2hzJkSM8o4JOA9BmXBGAJB+BzNnAso4PQplHLSCstZY0gn1CoDQWozBWCkBXFY+omy5HbPiU2KAGi2kdJAF0-A1FelgDID0SpCxqm0JCQgaFUSaDvLcBwfgAi7LiIgAAdTUOoLOBJKBnFCUknoKSdENO4U03xJThnfPBKEmAUypE3IJrCJMlLsmBWIpiJkIA1kADlVltAAGJIFDuUAx6AW5MjUES3RVCcV4oJdgeVYBhWYA4NyqMzzsCmXMu0oq4RKppHULgEO1EJmz3GVmC2VqqgKCzK1e1YzHU9G2i6m1PR-aerdeUnl2ALTQBbggI1LBdV0ribq-VhUwgaN5fy7AQrbliolWQG0Zq4AWogLcJhLC2G6qTMsTN2blipjOI2RJtq1Z5swKwqAZBC3LAtmWitCTzC+zSK1XNzC60Fr5NgItrVW2-Kre6tmtb62NoHUW4W5bR0dsLBi4iJQyg-PQPfT2L5j4UC3csIgoC92IJQRQdYe6iAEAoAAYWzssbV9RV3qAqLqlgj6KiRp+W+7ZajSVpHJWkzlWwrG6I-eCLQJiv12KSHw2E+hmXLMfBqnJfjyEBP9VGGgeoNDTrqKBrWzh6E9AjV8uJ4GkhfogFB2SMgCKwaZTRuthFWV3JafUdYTJQ3UPbbAdAmJQCYElXws46rbm+zspieYSAOgtzALICRtSTUwH-eEQDhiUOpjwxJhgUmyR0NpfB5jyGSmZTsiGo1ES9SMalWBQN2npOyfk4kEjPz2OcZbtxi5SmmkCyU6mHotwkxNPvbk0gL6UX1EU0mBudRIrpRydGgqhqwiZWEHgjOeUVzadkBakh-ZBBWAYDEI1GBd74BoK8ugA7wTOfBE8qr4WuBzJtPucGtnFg8ZgJCrIxHYk-L0bQurdQIBsAvjAMzYRqu9fBFp9r42+gVZfUmXVpTRviXDDVkLlWhtLYHamIt-sy09C4D6aL4cwIDtG1MK7SYQChomzkubjJZCWeZGQR7w2ejcENiPMEqq1tQXoXOH0GgG7KEQ2D9Y7QQCYBWAKkAsAkAcbiiybpa9Hpwxa41CIXXMg9a2eCfrZAv0vrIJus4g3mAcFG1hzQG3MPXBw-gEbPp3uaba8Gu782KeLCTFoJeMATE09gytn0-3JJ09C1V3n-PBfXGF-tm6bhDtpGO79DQhtriXeu7dsND3OdPZe0yN7+uPtpC+zIH71ixfYEB+rEHDhwd6ShzD5YcOEdI+wCj-AaPYYYRa4jbHouB14cJ8TqrpOd2fG58N5nWQad4fp9h3VsfMis42zNjnYaFtS60DugXSQhfeJT2ka3CfJfbdz23LYsuNDy+WAdvzKvdlq8tjTrXUwbsm71+Z57BFjdhrYJ977jdfuNsVzb+ZqN7dg-VRD53sP4dNA917sk3d0d+6HH8JggfuvB426H0oT7ygk-3Ye8n5fKfF5owCCXJAaeM5t6NtPU2bNBqgO97PFeD3V4L3Lovq3x8y8ttmBedv989C89t69x9lcYBVdMgLYNcNB29O9ddbhHsLM+93tB8zdh9ZUrdx9bcp91BQdHdIcG4Xc3cl8EBkc5Fvc19fdRRN9oFShsARVjVOsg9cN98qF9Ew8htSdj1UEo8L9FgqcfR49b979k8n8Tc2c38P9o9edBDT1wC-8RdutADb9FstBlC0Ea91A68G8jtm94C1Y28fQrsO8dd7s0D9cMCrMsCh8LcR98DZoAdJ9gdiCHdZ8ndyCF93dqDPdaDV9kRfQMdN9-hgBNB0AccS898X8D810T8L1r1b1z9gDRCr8JCX9E91AH8r9n98dX8YV38TdP8QDc9L0b1VDa9-9RdNCciRDkxKjUiaiDDvEFc3CldG9YCTDVZ1dr91BkDrC+hu8wh7DXtHCcDnC8C-sCCPCshp9SD59XdF9EdAiV8fcwiN9KJD4d9cd4iijCdo8CjZD092dSis9FDlsr9S8tCpdltOjIYYCuBTtnxdVzdOBLCUCbCxs7De8HCTc2ATlEhFEXC5iuiJ9TkiCSCfCyDod-CqCaDUd6DtjvVSgGBMBwgbw5gSizhGozhEZCSmAzhmCzsyTWCwBCS8Aoizg9jU4BAgA)에 전체 코드를 실어놓았습니다.

API 인터페이스에서 API 호출 함수의 인자, 반환 타입을 추출합니다.

`createAPI()`에 API 인터페이스를 넣어주면 안전하게 API를 호출할 수 있는 함수가 완성됩니다.

```ts
const api = createAPI<ToAPIRoutes<API>>();

//                               ↓ 메서드와 경로가 자동완성됨
const user = await api.request('GET /users/:id', {
  path: {
    id: '123', // ← 경로변수 :id의 타입이 추론됨
  },
});

//    ↓ 반환 타입이 모두 추론됨
user.id;
user.name;
```

&nbsp;

## 왜 이렇게 써야할까?

### 자주 봤던 API 호출 코드 작성방식

아래 같은 API 호출 코드를 많이 보셨을 거 같습니다.

```ts
import axios from 'axios'; // ← API 클라이언트 import하기
import type { User } from '@/types'; // ← 응답 타입 import하기

//                               ↓ 응답 타입 직접 적어주기
const { data } = await axios.get<User>('/users/123');
//                                       ↑ 경로 직접 적어주기
```

코드를 작성하기는 간단하지만, 앱이 커질수록 문제가 발생합니다.

1. 인자 타입이 추론되지 않습니다.
   - 인자 하나 빼먹고 에러 처리 안 해서 장애가 나는 경우도 있습니다.
2. 경로와 응답 타입을 개발자가 직접 지정해줘야 합니다.
   - 나중에 BE 개발자의 API 변경 요청에 대응하기 힘듭니다. 문자열 검색해서 하나하나 바꿔줘야 해요.
3. 타입 `import` 문이 많이 늘어납니다.
   - 코드 베이스가 커지면 무시 못할 수준입니다

### 해결방안 1. 함수화

API 호출 코드를 함수로 만드는 방법이 있습니다.

이러면 인자 타입이 추론되고, API 인터페이스 변경에 빠른 대응이 가능해집니다.

```ts
export const getUser = (id: string): Promise<User> => {
  const { data } = await axios.get<User>(`/users/${id}`);

  return data;
};

export const getUsers = ({ page, size }: Pagination): Promise<User[]> => {
  const { data } = await axios.get<User>(`/users`, {
    params: { page, size },
  });

  return data;
};

export const createUser = ({ name }: Pick<User, 'name'>): Promise<User> => {
  const { data } = await axios.post<User>(`/users`, { name });

  return data;
};
```

다만, 모든 API에 대해 함수를 정의해줘야 하고

> API 하나당 코드 5~6줄 씩, 하나의 서비스를 정의하는데 코드가 500줄씩 되기도 합니다.

비슷하지만 조금씩 다른 인자 타입이 계속해서 늘어납니다.

> 딱 한번에 못 쓰는 인자 타입이 코드베이스에 불어나서 처지곤란해집니다.

또한, API 함수를 import 하는 코드도 상당히 많아 집니다.

> 이게 너무 스트레스인게, 어떤 걸 import 해야하는지 함수명을 떠올려서 입력해야 돼요.

```ts
import {
  getUser,
  getUsers,
  createUser,
  deleteUser,
  updateUser,
  getPosts,
  createPost,
} from '@/api';
```

또한, API가 1차원적으로 늘어나므로, API 간의 관계를 파악하기 어려워집니다.

### 해결방안 2. 객체로 묶기

API 함수의 import 문이 늘어나는 것을 막고 관계를 명확하게 만드는 간단한 방법이 있습니다.

바로 객체로 API 함수를 묶는 것입니다.

```ts
const createUser = () => { ... };
const getUsers = () => { ... };
const getUser = () => { ... };
...

export const rpc = {
  user: {
    create: createUser,
    list: getUsers,
    get: getUser,
  },

  post: {
    create: createPost,
    list: listPosts,
    get: getPost,
    update: updatePost,
  },
};
```

그럼 `import` 문 하나로 모든 API를 편하게 쓸 수 있습니다.

```ts
import { rpc } from '@/rpc';
```

또한, API를 호출하는 코드를 사용하기도, 읽기도 편합니다.

```ts
const createdUser = await rpc.user.create({ name: 'john.doe' });

const user = await rpc.user.get('123');

const users = await rpc.user.list({ page: 1, size: 10 });
```

`rpc.user.` 만 입력해도, `User`를 다룰 수 있는 모든 연산을 확인할 수 있어요.

### 해결방안 3. API 함수 자동생성하기

경로를 받아서 API 함수를 반환하는 고차함수 `from()`을 사용하면

별도 함수 정의 없이 API 함수를 정의할 수 있어요.

> `from()` 함수는 `request()` 함수의 커링된 버전입니다. 인자 2개를 한번에 받는 대신 따로 따로 받습니다.
>
> 위 타입스크립트 플레이그라운드 링크에 코드가 모두 나와있습니다.

```ts
const rpc = {
  user: {
    create: api.from('POST /users'),
    list: api.from('GET /users'),
    get: api.from('GET /users/:id'),
  },

  post: {
    create: api.from('POST /posts'),
    list: api.from('GET /posts'),
    get: api.from('GET /posts/:id'),
    update: api.from('PUT /posts/:id'),
    delete: api.from('DELETE /posts/:id'),
  },
};
```

이런식으로 API 호출에 필요한 1) 인자 타입도 2) 함수도 3) 긴 `import` 문도 모두 없앨 수 있습니다.

### 더 나아가기

서버의 API 타입을 그대로 써서 FE 앱을 작성하면,

서버 스펙 변경에 따라 FE에서도 API 타입, 그 데이터를 입력받는 컴포넌트의 프롭 타입까지 바꿔줘야 하고

가끔 `userno` 같이 자바스크립트 변수명 컨벤션에 맞지도 않고, 직관적이지 않은 필드명을 억지도 써야 하는 경우도 있습니다.

또한, 테스트 코드 작성 시 컴포넌트에서 쓰는 정말 필요한 데이터는 2~3개인데, 서버 필드 20개를 목업해줘야 하기도 합니다.

그래서 가능하다면, FE앱에서 쓰는 자체 도메인 모델 타입과 그에 대한 연산을 인터페이스로 정의하고

그 인터페이스에 맞게 서버 API 호출하는 코드를 작성하는 걸 추천합니다.

그러면, 정말 필요한 데이터만 서버에서 가져오므로 코드가 작고 가벼워집니다.

또한, 인터페이스의 목업 구현체를 만들어서 쓰면(코파일럿이 잘 만들어줍니다), 서버 연결 없이도 개발을 진행할 수 있고

마지막에 서버 구현체만 하나 만들어주면 서버 연동을 위한 작업이 빠르게 완료되기도 합니다.

## 참고

- [깃헙 Octokit.js](https://github.com/octokit/octokit.js)
- [openapi-typescript](https://www.npmjs.com/package/openapi-typescript): OpenAPI 문서에서 타입 추출하기
- [OpenApi 스펙을 활용해서 type-safe하게 ReactQuery 사용하기](https://gist.github.com/seonghyeonkimm/977b58387f9f4e11afeee8c7685c2e89)
