---
layout: base
title:  "[기성이의 개발지] 애플 clion 컴파일러 애러 해결"
date:   2026-09-17
categories: [기성이의 개발지]
---

## Too Long; Didn't Read

CLion에서 멀쩡히 돌아가던 C 프로젝트가 갑자기 링크 에러를 뱉기 시작했다. 원인을 역으로 추적해보니 **"이틀 전 출시된 macOS 27 + 라이선스 미동의"**라는 두 가지 원인이 겹친 문제였다. 아래는 그걸 찾아낸 과정.

## 문제 발생

평소처럼 CLion에서 빌드했는데 이런 에러가 떴다.

```
ld: tapi error: malformed file
/Library/Developer/CommandLineTools/SDKs/MacOSX27.0.sdk/usr/lib/libSystem.B.tbd:4:20: error: unknown architecture
                   arm64e.x1-macos, arm64e.x1-maccatalyst ]
                   ^~~~~~~~~~~~~~~
 in '/Library/Developer/CommandLineTools/SDKs/MacOSX.sdk/usr/lib/libSystem.tbd'
clang: error: linker command failed with exit code 1 (use -v to see invocation)
ninja: build stopped: subcommand failed.
```

코드는 건드린 적도 없는데 빌드가 깨지니까 당황스러웠다. `.c` 파일 문제가 아니라 **툴체인 레벨**에서 나는 에러라는 걸 로그만 보고도 짐작할 수 있었다 — `libSystem.tbd`, `ld`, `tapi error` 같은 키워드는 전부 링커/SDK 쪽 이야기니까.

## 첫 번째 가설: "베타 SDK겠지" — 틀림

`MacOSX27.0.sdk`라는 이름을 보고 반사적으로 "아, 이거 아직 정식 출시 안 된 베타 macOS 버전 SDK구나" 라고 판단했다. 그래서 처음엔:

- 구버전 CommandLineTools를 지우고 정식(stable) 버전으로 재설치하면 해결될 거라 생각함

근데 찾아보니 **macOS 27은 이미 이틀 전(9/14)에 정식 출시된 버전**이었다. 베타가 아니라 그냥 최신 OS였던 것. 가설 하나 폐기.

수정된 가설: SDK는 최신인데, 그걸 읽는 **링커(ld) 쪽이 구버전이라 새 SDK 포맷을 못 읽는 것** 아닐까 → macOS 업데이트를 했다고 Xcode/Command Line Tools까지 자동으로 같이 업데이트되는 게 아니니까 앞뒤가 맞다.

## 두 번째 가설: "Xcode 자체를 업데이트하면 끝" — 부분적으로만 맞음

`xcode-select -p` 로 확인해보니 standalone CommandLineTools가 아니라 **Xcode.app**을 쓰고 있었다.

```
/Applications/Xcode.app/Contents/Developer
```

그래서 Xcode.app을 최신 버전으로 업데이트했다. 업데이트 후 확인:

```
$ cc -v
Apple clang version 21.0.0 (clang-2100.1.1.101)
Target: arm64-apple-darwin27.0.0
InstalledDir: /Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin
```

`darwin27.0.0`으로 잘 뜨길래 "이제 됐겠지" 하고 CLion에서 다시 빌드했는데 — **여전히 똑같은 에러**가 났다. 컴파일러 버전은 최신인데 왜 안 되지?

## 세 번째 시도: 진짜 원인 발견

여기서 다시 원점으로 돌아가 에러 로그를 자세히 봤다. 에러가 참조하는 경로가 여전히:

```
/Library/Developer/CommandLineTools/SDKs/MacOSX27.0.sdk/...
```

즉 `xcode-select`는 Xcode.app을 가리키는데, **실제 컴파일 시점의 SDK는 옛날 CommandLineTools 쪽**을 보고 있었다. 뭔가가 폴백을 시키고 있다는 뜻.

터미널에서 직접 컴파일을 시도하니 이런 메시지가 나왔다.

```
You have not agreed to the Xcode and Apple SDKs license.
You must agree to the license below in order to use Xcode.
```

**여기가 진짜 원인이었다.** Xcode를 업데이트했지만 라이선스 동의를 안 해서, macOS가 새 Xcode의 SDK 사용을 막고 있었던 것. 그래서 컴파일러가 조용히 예전 CommandLineTools SDK로 폴백했고, 그 폴백된 SDK는 애초에 macOS 27을 지원하지 않아서 똑같은 tapi 에러가 반복됐던 거다.

## 해결

```bash
sudo xcodebuild -license accept
```

동의 후 SDK 경로 재확인:

```bash
$ xcrun --show-sdk-path
/Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX.sdk
```

드디어 Xcode.app 안의 정식 macOS 27 SDK를 가리키는 걸 확인했다. CLion에서 `Tools → CMake → Reset Cache and Reload Project` 로 캐시를 지우고 재빌드하니 정상적으로 빌드 성공.

## 디버깅 흐름 요약

| 단계 | 가설 | 결과 |
|---|---|---|
| 1 | SDK 이름이 27이라 베타 버전일 것 | ❌ macOS 27은 이미 정식 출시됨 |
| 2 | 구버전 링커가 새 SDK 포맷을 못 읽는 것 | ⭕ 방향은 맞음, 근본 원인은 아님 |
| 3 | Xcode.app만 업데이트하면 해결될 것 | ❌ 업데이트해도 에러 재현 |
| 4 | 라이선스 미동의로 인한 SDK 폴백 | ✅ 최종 원인 |

## 오늘의 교훈

- **에러 메시지에 나오는 경로를 끝까지 의심하자.** `xcode-select -p`가 정상이어도, 실제 컴파일 로그에 찍히는 SDK 경로가 다르면 그게 진짜 단서다.
- macOS 업데이트 ≠ Xcode/툴체인 업데이트. 별개로 챙겨야 한다.
- Xcode를 새로 깔거나 업데이트한 직후 정체불명의 SDK/링크 에러가 난다면, 가장 먼저 `sudo xcodebuild -license accept` 부터 의심해볼 것. 은근히 잘 잊는 단계다.
