---
title: Git으로 실행취소(Undo)하는 거의 모든 방법
date: 2019-12-26T20:30:00+09:00
author: yongjin0802
categories:
  - Git
tags:
  - Git
---

[How to undo (almost) anything with Git](https://github.blog/2015-06-08-how-to-undo-almost-anything-with-git/) 번역

버전 제어 시스템에서 가장 유용한 기능 중 하나는 실수를 "실행취소"할 수 있다는 것입니다. Git에서 "실행취소"는 많은 의미가 있습니다.

커밋을 할 때마다 Git은 특정 시점에 저장소의 스냅샷을 저장합니다. Git을 사용하여 나중에도 이전 버전의 프로젝트로 돌아갈 수 있습니다.

이 글에서는 변경한 내용을 "실행취소"하는 몇 가지 일반적인 시나리오와 Git으로 실행취소하는 가장 좋은 방법을 알아봅니다.

## "공개(Public)" 변경사항 실행취소하기

**시나리오:** `git push` 실행하여 변경사항을 GitHub에 전송했는데, 커밋 중 하나에 문제가 있음을 알게 되었습니다. 그 커밋을 실행취소하고 싶습니다.

**실행취소:** `git revert <SHA>`

**일어나는 일:** `git revert`는 주어진 SHA의 정반대인 새로운 커밋을 만듭니다. 이전 커밋이 "물질"이라면 새 커밋은 "반물질"입니다. 이전 커밋에서 제거된 항목은 새 커밋에 추가되고 이전 커밋에 추가된 항목은 새 커밋에서 제거됩니다.

이것이 바로 Git의 안전하고, 가장 기본적인 "실행취소" 시나리오입니다. 왜나하면 히스토리를 바꾸지 않으니까요. 이제, 새로운 "역" 커밋을 `git push`하여 실수한 커밋을 실행취소할 수 있습니다.

## 마지막 커밋 메시지 수정하기

**시나리오:** 마지막 커밋 메시지를 입력했습니다. `git commit -m "Fxies bug #42"`라고 입력했지만, `git push`하기 전에 실제로는 "Fixes bug #42"라고 입력해야 한다는 것을 깨달았습니다.

**실행취소:** `git commit --amend` 또는 `git commit --amend -m "Fixes bug #42"`

**일어나는 일:** `git commit --amend`는 가장 최근의 커밋을, Staged 상태의 변경사항을 이전 커밋 내용과 합친 새로운 커밋으로 업데이트하고 대체합니다. 현재 상태가 Staged 상태가 아니라면, 이전 커밋 메시지만 재작성합니다.

## "로컬" 변경사항 실행취소하기

**시나리오:** 고양이가 키보드 위를 걸어 다니다가 어떻게 했는지 변경사항을 저장하고 에디터를 먹통으로 만들어 버렸습니다. 이 변경사항을 아직 커밋 하지 않은 상태인데, 파일 안의 모든 것을 마지막으로 커밋 했던 상태로 돌리고 싶습니다.

**실행취소:** `git checkout -- <잘못 저장된 파일 이름>`

**일어나는 일:** `git checkout`은 작업 디렉터리의 파일을 예전에 Git이 알고 있던 상태로 변경합니다. 가고 싶은 브랜치 이름이나 특정 SHA를 제공할 수도 있습니다. 기본적으로 Git은 당신이 현재 체크아웃된 브랜치의 마지막 커밋인, `HEAD`로 체크아웃 하고 싶어 한다고 가정합니다.

## "로컬" 변경사항 리셋하기

**시나리오:** 로컬에서 커밋 여러 개를 했는데(아직 push하지 않음), 코드가 엉망이라 최근 커밋 세 개를 실행취소하려고 합니다. 그 커밋들이 없었던 것처럼요.

**실행취소:** `git reset <마지막으로 잘한 SHA>` 또는 `git reset --hard <마지막으로 잘한 SHA>`

**일어나는 일:** `git reset`은 저장소의 히스토리를 지정된 SHA로 되돌립니다. 마치 커밋이 발생한 적이 없는 것처럼 보입니다. 기본적으로 `git reset`은 작업 디렉터리를 보존합니다. 커밋은 사라졌지만 내용은 여전히 ​​디스크에 있습니다. 이것이 가장 안전한 옵션이지만, 커밋과 변경사항을 한 번에 "실행취소"하고 싶을 때가 있습니다. 이럴 때는 `--hard` 옵션을 사용합니다.

## "로컬" 실행취소 뒤 다시 실행

**시나리오:** 커밋을 하고 `git reset --hard`를 실행해서 변경 사항을 "실행취소"한 뒤(위의 시나리오) 깨달았습니다. 그 변경사항들을 되돌리고 싶다!

**실행취소:** `git reflog` 및 `git reset` 또는 `git checkout`

**일어나는 일:** `git reflog` 는 프로젝트 히스토리를 복구하는 놀라운 명령어입니다. `reflog`를 통해 커밋한 적 있는 거의 모든 것을 복구할 수 있습니다.

커밋 목록을 보여주는 `git log` 명령어에 익숙하실 겁니다. `git reflog`는 비슷하지만, 대신에 `HEAD`가 변경된 시간 목록을 보여줍니다.

몇 가지 주의 사항:

- `HEAD`만 변경됩니다. 브랜치를 변경하고 `git commit`으로 커밋을 만들고 `git reset`으로 un-make 커밋을 하면 `HEAD`가 변경됩니다. 하지만, 이전 시나리오처럼 `git checkout -- <잘못 저장된 파일 이름>`을 실행했다면 `HEAD`가 변경되지 않습니다. 그 변경사항이 커밋된 적이 없었기 때문에 `reflog`를 통해 복구할 수 없습니다.
- `git reflog`는 영원히 지속되지 않습니다. Git은 "도달할 수없는" 오브젝트를 정기적으로 청소합니다.
- 자신의 `reflog`은 자신만의 것입니다. `git reflog`를 사용하여 다른 개발자가 푸시하지 않은 커밋을 복원할 수 없습니다.

![reflog](https://github.blog/wp-content/uploads/2015/06/f6b9f054-d891-11e4-8c53-838eff9f40ae.png?resize=1429%2C644)

그렇다면… reflog를 사용하여 어떻게 이전에 "취소된" 커밋을 "재실행"해야 할까요? 정확히 달성하려는 목적에 따라 다릅니다.

- 그 당시의 프로젝트 기록을 복원하려면 `git reset --hard <SHA>`
- 히스토리를 변경하지 않고 그 당시의 작업 디렉터리에서 하나 이상의 파일을 다시 작성하려면 `git checkout <SHA> -- <filename>`
- 저장소에 커밋을 정확히 재생하려면 `git cherry-pick <SHA>`

## 브랜치에 할 커밋을 마스터에 했을 때

**시나리오:** 커밋을 한 다음 `master`에 체크아웃했음을 깨달았습니다. `feature` 브랜치에 커밋을 수행하고 싶습니다.

**실행취소:** `git branch feature`, `git reset --hard origin/master` 및 `git checkout feature`

**일어나는 일:** 새 브랜치를 만들고 그 브랜치로 바로 체크아웃하는 `git checkout -b <name>` 명령어로 새 브랜치를 만들어 봤을 겁니다. 브랜치를 만들고 바로 전환하고 싶지 않을 때가 있습니다. `git branch feature` 명령어를 사용하면 `feature`라는 새로운 브랜치를 생성하고 가장 최근의 커밋을 가리키게 하지만, `master`에 체크아웃한 상태로 둡니다.

다음으로, `git reset --hard`는 새로 커밋하기 전에 `master`를 `origin/master`로 되돌립니다. 커밋들은 `feature`에 유지되니 걱정하지 않아도 됩니다.

마지막으로, `git checkout`은 최근의 모든 작업을 그대로 유지하면서 새로운 `feature` 브랜치로 전환합니다.

## 첫 브랜치부터 잘 만들자. 리베이스

**시나리오:** `master`를 기반으로 새 브랜치인 `feature`를 만들었을 때, `master`는 `origin/master`보다 훨씬 뒤처져있었습니다. 이제 `master` 브랜치가 `origin/master`와 동기화되었으므로, `feature`에 대한 커밋이 뒤처지지 않았으면 좋겠습니다.

**실행취소:** `git checkout feature` 및 `git rebase master`

**일어나는 일:** `git reset`을 (디스크에 변경 사항을 보존하는 `--hard` 옵션 없이) 실행하고 `git checkout -b <new branch name>` 실행한 뒤 변경사항을 다시 커밋할 수 있지만, 그렇게 하면 커밋 히스토리가 날아갑니다. `rebase`라는 좋은 방법이 있습니다.

`git rebase master`는 몇 가지 일을 합니다.

- 먼저, 현재 체크아웃된 브랜치와 `master` 사이의 공통 조상을 찾습니다.
- 그런 다음, 현재 체크아웃된 브랜치를 해당 조상으로 재설정하여 모든 나중의 커밋을 임시 보류 영역에 놓습니다.
- 그런 다음, 현재 체크아웃된 브랜치를 `master`의 끝으로 진행시키고 `master`의 마지막 커밋 이후 보류 영역에 있는 커밋을 재실행합니다.

![rebase](https://miro.medium.com/max/1466/1*i8LUeJZhpp80Ed77U1D9_Q.jpeg)

## 대규모 실행취소 / 다시 실행

**시나리오:** feature 브랜치를 한 방향으로 진행하고 있었지만, 중간에 다른 해결책이 더 낫다는 것을 깨달았습니다. 커밋이 수십 개 정도 있지만 그중 일부만 원하고 다른 나머지는 사라지기를 바랍니다.

**실행취소:** `git rebase -i <앞의 SHA>`

**일어나는 일:** `-i` 옵션은 `rebase`를 "대화식 모드"로 설정합니다. 위에서 설명한 `rebase`처럼 시작하지만, 커밋을 재생하기 전에 일시 중지되어 재생될 때마다 각 커밋을 부드럽게 수정할 수 있습니다.

`rebase -i`는 기본 텍스트 에디터에서 적용할 커밋 목록과 함께 열립니다. 이렇게요:

![rebase-interactive1](https://github.blog/wp-content/uploads/2015/06/f6b1ab88-d891-11e4-97c1-e0630ac74e74.png?resize=1459%2C495)

처음 두 열이 핵심입니다. 첫 번째 열은, 두 번째 열의 SHA로 식별되는 커밋에 대해 실행할 명령입니다. 기본적으로 `rebase -i`는 각 커밋에 `pick` 명령을 적용한다고 가정합니다.

커밋을 삭제하려면 에디터에서 해당 줄을 삭제하면 됩니다. 프로젝트에서 잘못된 커밋을 없애고 싶다면, 위의 1 행과 3-4 행을 삭제할 수 있습니다.

커밋 내용을 보존하고 커밋 메시지를 편집하려면 `reword` 명령을 사용합니다. 첫 번째 열의 단어 `pick`을 `reword`(또는 `r`)로 바꾸면 됩니다. 지금 커밋 메시지를 다시 작성하고 싶어도 못합니다. `rebase -i`는 SHA 열 뒤의 모든 것을 무시하기 때문입니다. 그 후의 텍스트는 단지 `0835fe2`가 무엇인지 기억하는 데 도움을 주기 위한 것입니다. `rebase -i`를 마치면 작성해야 할 새로운 커밋 메시지를 묻는 메시지가 나타납니다.

두 커밋을 합치려면 `squash` 또는 `fixup` 명령을 사용할 수 있습니다. 이렇게요:

![rebase-interactive2](https://github.blog/wp-content/uploads/2015/06/f6b605ca-d891-11e4-98cf-d567ca9f4edc.png?resize=1449%2C339)

`squash`와 `fixup`은 "위로" 합칩니다. 이 두 개의 "합치는" 명령이 있는 커밋은 바로 위에 있는 커밋과 합쳐집니다. 이 시나리오에서 `0835fe2` 와 `6943e85`는 하나의 커밋으로 합쳐지고 `0835fe2` 와 `6943e85`도 하나의 커밋으로 합쳐집니다.

`squash`를 선택하면 Git은 새로 합쳐진 커밋에 새로운 커밋 메시지를 제공하기를 요구합니다. `fixup`은 새 커밋에 목록의 첫 번째 커밋 메시지를 사용하게 합니다. "ooops"라는 메시지를 가진 `af67f82`에는 `38f5e4e`의 커밋 메시지를 사용하지만, `0835fe2`와 `6943e85`를 합친 새 커밋에는 새 메시지를 작성하게 됩니다.

에디터를 저장하고 종료하면 Git은 커밋을 위에서 아래로 적용합니다. 저장하기 전에 커밋 순서를 변경하여 커밋이 적용되는 순서를 변경할 수 있습니다. 원한다면 다음과 같이 정렬하여 `af67f82`와 `0835fe2`를 합칠 수 있습니다.

![rebase-interactive3](https://github.blog/wp-content/uploads/2015/06/f6b4a9d2-d891-11e4-9ac9-10039c031d06.png?resize=1445%2C326)

<center><sub><code>af67f82</code>를 마지막 줄에서 두 번째 줄로 옮김</sub></center>

## 예전 커밋 수정하기

**시나리오:** 예전에 파일 하나를 빼고 커밋을 했습니다. 빼먹은 파일을 어떻게든 예전 커밋에 넣을 수 있다면 좋을 텐데요. 아직 푸시하지 않았지만 가장 최근 커밋이 아니기 때문에 `commit --amend`를 사용할 수 없습니다.

**실행취소:** `git commit --squash <SHA of the earlier commit>` 및 `git rebase --autosquash -i <even earlier SHA>`

**일어나는 일:** `git commit --squash`는 `squash! Earlier commit`와 같은 커밋 메시지를 가진 새로운 커밋을 생성합니다. (커밋 메시지를 직접 입력할 수 있지만, `commit --squash`를 사용하면 입력하는 수고를 덜 수 있습니다.)

합쳐진 커밋에 새로운 커밋 메시지를 작성하고 싶지 않다면, `git commit --fixup`을 사용할 수도 있습니다. 이 경우에는 이전 커밋의 커밋 메시지를 사용합니다.

`rebase --autosquash -i`는 대화식 `rebase` 에디터를 실행시키지만, 에디터에는 커밋 목록에서 커밋 대상과 짝지어진 `squash!`와 `fixup!` 커밋만 보입니다. 이렇게요:

![rebase-auto-squash](https://github.blog/wp-content/uploads/2015/06/f6a7a1d8-d891-11e4-8784-c32262ff54da.png?resize=1446%2C294)

`--squash`과 `--fixup` 옵션을 사용할 때는 수정할 커밋의 SHA가 기억나지 않을 겁니다. 그게 1분 전에 한 커밋이 아니라면요^^. Git의 `^`나 `~` 연산자를 사용하면 편리합니다. `HEAD^`는 `HEAD`에서 커밋 하나 전입니다. `HEAD~4`는 `HEAD`에서 커밋 4개 전입니다.

## 트랙킹되는 파일 지우기

**시나리오:** 실수로 `application.log`를 저장소에 추가했습니다. 그랬더니 애플리케이션을 실행할 때마다 Git이 `application.log`에 Unstaged 상태의 변경사항이 있다고 보고합니다. `.gitignore` 파일에 `*.log`를 넣었지만 여전합니다. Git에게 파일의 변경사항 추적을 그만하도록 하려면 어떻게 해야 할까요?

**실행취소:** `git rm --cached application.log`

**일어나는 일:** `.gitignore`는 Git이 파일의 변경사항을 추적하거나 추적된 적 없는 파일의 존재를 알아차리는 것을 못 하게 합니다. 하지만 일단 파일이 추가되고 커밋됐다면 Git은 해당 파일의 변경사항을 계속 알아차립니다. 마찬가지로, `git add -f`로 강제로 파일을 추가하거나 `.gitignore`를 재정의해도 Git이 변경사항을 추적합니다. 나중에 추가하기 위해 `-f`를 사용할 필요는 없습니다.

Git의 추적을 피해야 하는 파일을 제거하고 싶습니다. `git rm --cached`는 추적에서 파일을 제거하지만 디스크에서 파일을 삭제하지 않습니다. `git status`에서 무시된 파일이 보이거나 실수로 해당 파일의 변경 사항을 커밋할 일은 없을 것입니다.

---

이상으로 **Git으로 실행취소하는 거의 모든 방법**을 마칩니다. 이 글에서 사용된 Git 명령에 자세히 알고 싶다면 관련 문서를 확인하시길 바랍니다.

- [checkout](http://git-scm.com/docs/git-checkout)
- [commit](http://git-scm.com/docs/git-commit)
- [rebase](http://git-scm.com/docs/git-rebase)
- [reflog](http://git-scm.com/docs/git-reflog)
- [reset](http://git-scm.com/docs/git-reset)
- [revert](http://git-scm.com/docs/git-revert)
- [rm](http://git-scm.com/docs/git-rm)

## 출처

[깃허브 블로그](https://github.blog/2015-06-08-how-to-undo-almost-anything-with-git/)
