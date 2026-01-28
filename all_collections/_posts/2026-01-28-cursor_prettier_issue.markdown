---
layout: post
title: "cursor 업데이트 후 prettier 동작 이슈 관련 해결법"
date: 2026-01-28 09:50:00 +0100
categories: ["tips", "cursor", "prettier"]
published: true
---

cursor의 특정 버전 업데이트 이후 갑자기 멀쩡히 사용하던 prettier 가 동작하지 않음을 확인했다.(v2.3.41)

이에 관련 커뮤니티를 좀 찾아본 결과, 현재 cursor에서 12버전 이상의 prettier 플러그인을 정상적으로 인식하지 못하고 있다고 한다.

[관련 cursor forum](https://forum.cursor.com/t/after-last-update-prettier-stopped-working/149213/25)

이에 해결 방법을 찾아보니, prettier 버전을 11.0.2 버전으로 낮추는 것이 제시되고 있었다.

---

prettier 버전 변경 이후, cmd + shift + p -> format document / format document(forced)는 정상적으로 동작했지만 format on save는 여전히 동작하지 않았다.

이에 설정에서 default formatter / format on save 옵션을 다시 확인했지만 모두 정상적으로 prettier를 통한 자동 formatting 이 적용되어 있었다.

---

결국 settings.json을 동료 직원(thx to Leo)과 비교해 본 결과, 기존의 setting.json은

```json
{
  "editor.formatOnSave": true,
  "typescript.preferences.autoImportFileExcludePatterns": ["@rsbuild/core"],
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "editor.codeActionsOnSave": {
    "source.organizeImports": "explicit",
    "source.fixAll.eslint": "explicit",
    "source.fixAll.eslint.format": "explicit"
  }
}
```

위처럼 기본 설정만 되어 있었는데, 레오의 setting.json에는

```json
{
  "[typescriptreact]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  }
}
```

각 파일 형식에 따른 default formatter가 별도 적용되어 있었다. 이를 적용하니 .tsx 확장자에서는 format on save 가 정상 적용되었고, .ts확장자의 formatting을 위해 최종적으로 다음과 같이 수정하였다.

```json
{
  "editor.formatOnSave": true,
  "typescript.preferences.autoImportFileExcludePatterns": ["@rsbuild/core"],
  "editor.defaultFormatter": "esbenp.prettier-vscode",

  "editor.codeActionsOnSave": {
    "source.organizeImports": "explicit",
    "source.fixAll.eslint": "explicit",
    "source.fixAll.eslint.format": "explicit"
  },

  "eslint.run": "onType",

  "[typescript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[typescriptreact]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },

  "files.autoSave": "afterDelay",
  "eslint.runtime": "node",
  "cursor.general.disableHttp2": true
}
```

이게 최종적으로 맞는 방법인지는 모르겠으나 나의 경우/현재 프로젝트에서는 정상적으로 prettier / format on save가 동작한다.
