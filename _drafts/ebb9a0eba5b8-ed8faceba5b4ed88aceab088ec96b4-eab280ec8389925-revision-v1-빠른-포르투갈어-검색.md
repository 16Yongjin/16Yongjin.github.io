---
id: 932
title: 빠른 포르투갈어 검색
date: 2019-07-02T20:32:31+09:00
author: yongjin0802
layout: revision
guid: https://yongj.in/2019/07/02/925-revision-v1/
permalink: /2019/07/02/925-revision-v1/
---
<figure class="wp-block-image"><img src="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2019/07/포어검색플레이스토어캡쳐.png?fit=840%2C810&ssl=1" alt="" class="wp-image-926" srcset="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2019/07/포어검색플레이스토어캡쳐.png 1437w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2019/07/포어검색플레이스토어캡쳐-300x289.png 300w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2019/07/포어검색플레이스토어캡쳐-768x741.png 768w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2019/07/포어검색플레이스토어캡쳐-1024x988.png 1024w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2019/07/포어검색플레이스토어캡쳐-1000x965.png 1000w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2019/07/포어검색플레이스토어캡쳐-311x300.png 311w" sizes="(max-width: 1437px) 100vw, 1437px" /><figcaption> <https://play.google.com/store/apps/details?id=com.yongj.in.pt_popdic> </figcaption></figure> 

터치 세 번만에 포르투갈어 단어를 찾을 수 있는 앱

사전을 켜지 않아도 단어를 앱에 공유하면 그 자리에서 바로 단어사전이 나타난다.

## 프론트엔드

과거에 만든 PT POPDIC을 Flutter로 재구현했다.

메서드 채널로 안드로이드 특수 기능을 사용했다.

Provider로 상태관리를 했다.

### 구현하기 어려웠던 부분

  1. 안드로이드 인텐트 사용 (플랫폼 특정 기능 사용)
  2. 사전 카드 이외 부분 터치 시 앱 종료

#### 1. 안드로이드 인텐트 사용

[Writing custom plaform-specific code](https://flutter.dev/docs/development/platform-integration/platform-channels)를 보고 따라하니 텍스트 메뉴와 공유에 앱을 연결하는 건 쉬웠다.

자바 액티비티 속 메서드 채널로 공유된 문자열을 플러터 위젯에서 받으면 끝났다.

하지만 액티비티는 달라도 실행되는 플러터 인스턴스는 같고

플러터 인스턴스에서 자신이 실행 중인 액티비티를 알 방법을 찾을 수 없었다.

그래서 &#8216;그냥 앱 실행 시&#8217;와 &#8216;다른 앱 위에서 실행 시&#8217;를 구분하는 게 조금 까다로웠다.

메서드 채널에서 문자열을 받으면 &#8216;다른 앱 위에서 실행 중&#8217;

문자을 받는 걸 실패하면 &#8216;그냥 앱 실행 중&#8217; 으로 구분하고

문자열을 받기 직전, 이도저도 아닌 상태에서는 로딩바를 띄웠다.

#### 2. 사전카드 이외 부분 터치 시 앱 종료 

옛날 PT POPDIC에서는 터치 이벤트의 X, Y축이 사전카드 밖이면 앱을 종료했다.

플러터에서는 위젯에 글로벌키를 연결해야 위젯 위치 정보를 얻을 수 있는다. 

부모 위젯에서 자식 위젯 여러 개의 글로벌키를 연결해서 위치정보를 얻다보면 스파게티 코드가 되어 보기 싫은 코드가 작성된다.

그래서 좌표값으로 터치 영억을 알아내는 것을 포기했다.

대신 전체화면에 터치 시 앱이 종료되는 제스처 탐지 위젯을 씌우고

그 위에 사전카드에 제스처 탐지 위젯을 다시 씌워서 전체화면으로 터치 이벤트가 전파되는 걸 막았다.

엄청 간단하게 문제를 해결했다.

과거 방식에 집착하지 말고 다르게 생각하는 게 중요함을 느꼈다. 

### 기타

Provider 패턴은 Vuex랑 비슷해서 사용하기 정말 편했다.

Provider에 빌드 컨텍스트랑 사용할 모델 타입만 건내주면 데이터 저장소에 접근할 수 있다.

차이점이라면 플러터에서는 내가 직접 _notifyListeners_()를 호출해서 UI를 다시 그리도록 하는 거 같다.

## 백엔드

네이버 포어 사전에서 데이터를 가져오는 기능을 네번째 구현 중이다.

첫번째는 Callback 두번째는 Promise 세번째는 Async/Await를 사용했고

이번에는 함수만을 사용했다.

함수를 정말 작은 단위로 쪼개고 이름을 붙여서 파이프라이닝했다.

[코어 모듈 코드](https://github.com/16Yongjin/ptdic/blob/master/searchDict.js)

옛날코드보다 보기 좋고 짧다.

#### Memoizing If 함수 &#8211; mif

<pre class="wp-block-code"><code>const v = f()
if (v) g(v)</code></pre>

이런 코드를 로직 상 많이 작성했다.

이 코드를 _.if 함수를 사용해서 표현하려면

<pre class="wp-block-code"><code>_.if(f())(g(f())</code></pre>

이렇게 f()를 두 번 호출해야 구색을 맞출 수 있다.

f()가 연산 비용이 크다면 문제가 되므로

술어에 들어온 값이 truthy하면 그 값을 그대로 g()에 적용하는 mif 함수를 만들었다.

<pre class="wp-block-code"><code>mif(f())(g)</code></pre>

이런 식으로 사용할 수 있다.

덕분에 

<pre class="wp-block-code"><code>const extractEntryIds = getExtractEntryIds(query)
if (extractEntryIds) return searchDictsByEntry(searchDictsByEntry)

const rootsFromWiki = getRootsFromWiki(entry)
if (rootsFromWiki) return searchWords(rootsFromWiki)

const verbRoots = getVerbRoots(query)
if (verbRoots) return searchWords(verbRoots)

const postprocessed = needsToPostprocess(query)
if (postprocessed) return searchWords(postprocessed)

return []</code></pre>

이런 코드를

<pre class="wp-block-code"><code>mif(extractEntryIds(query))(searchDictsByEntry)
  .elseIf(rootsFromWiki)(searchWords)
  .elseIf(_.c(getVerbRoots(query)))(searchWords)
  .elseIf(_.c(needsToPostprocess(query)))(searchWord)
  .else(_.c([]))</code></pre>

더 짧게, 동사 위주라 더 읽기 쉬운 코드로 작성할 수 있었다.

## 마치며

앱은 독창적으로 잘 만들었다고 생각하는데 다운로드 수는 3 밖에 되지 않는다. 

원인은 1. 홍보 채널이 부족하다. 2 포르투갈어가 수요가 적다.

1은 극복할 수 있지만 2는 극복하기 힘들 것 같다.

그래서 다음부터는 독창성과 대중성을 모두 갖춘 앱을 만들어서 다운로드 수 100을 기록해봐야겠다.