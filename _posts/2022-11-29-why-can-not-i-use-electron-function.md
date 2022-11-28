---
layout: article-view
categories: post
title: "Electron 기능을 왜 활용을 못하니"
summary: "React + Electron 환경 프로젝트에서 사용자가 이미지를 첨부 했을 때 용량 및 가로, 세로 크기가 특정 값을 초과한 경우 유효성 검사를 처리하는 작업을 진행했으며, Electron의 기본 기능을 활용하지 못해 추가 패키지를 설치하는 실수를 했다. 내가 사용하고 있는 라이브러리, 프레임워크의 공식 문서는 완벽하지 않더라도 훑어보고 어떤 기능들이 있는지 파악해 같은 실수를 되풀이 하지 말자 🥲🥲"
date: 2022-11-29
---

`React` + `Electron` 환경 프로젝트에서 사용자가 이미지를 첨부 했을 때 용량 및 가로, 세로 크기가 특정 값을 초과한 경우 유효성 검사를 처리하는 작업을 진행했다. 이미지 용량은 `fs.statSync` 로 체크할 수 있었지만 크기에 대한 정보는 없었다. `fs`로 확인하는 방법은 없었고 구글링 하다 `image-size` 패키지의 존재를 알게되고 다운로드 수도 괜찮아서 설치 및 적용 한 뒤 작업을 마무리 했다.

```typescript
import { sizeOf } from "image-size";

ipcMain.on(
  SYSTEM_IPC_CHANNEL.EXPECT_OVER_DIMENSIONS_FILES,
  (event, config: ExpectOverDimensionsFilesConfig) => {
    const { width, height } = sizeOf("images/...png");
    event.returnValue = width <= MAX_WIDTH && height <= MAX_HEIGHT;
  }
);
```

그러다 코드 리뷰에서 크기 확인은 `Electron`에 `nativeImage`를 활용한다면 된다는 코멘트가 달렸는데, 이 때 `Electron`을 활용하고 있으면서 왜 관련 내용을 찾아볼 생각을 못했는지 허탈감으로 몇 분을 보냈다.

```typescript
import { nativeImage } from "electron";

ipcMain.on(
  SYSTEM_IPC_CHANNEL.EXPECT_OVER_DIMENSIONS_FILES,
  (event, config: ExpectOverDimensionsFilesConfig) => {
    const { width, height } = nativeImage.createFromPath("images/...png");
    event.returnValue = image.width <= MAX_WIDTH && image.height <= MAX_HEIGHT;
  }
);
```

내가 사용하고 있는 라이브러리, 프레임워크의 공식 문서는 완벽하지 않더라도 훑어보고 어떤 기능들이 있는지 파악해 같은 실수를 되풀이 하지 말자 🥲🥲

## 참고 문서

- [https://nodejs.org/api/fs.html](https://nodejs.org/api/fs.html){:target="\_blank"}
- [https://github.com/image-size/image-size#readme](https://github.com/image-size/image-size#readme){:target="\_blank"}
- [https://www.electronjs.org/docs/latest/api/native-image](https://www.electronjs.org/docs/latest/api/native-image){:target="\_blank"}
