# page-ide-assets

Internal asset repository for [PAGE IDE](https://github.com/monkshark/page-ide).
Stores prebuilt LSP and toolchain bundles that PAGE IDE's built-in installers
download automatically.

**This repository is not intended for direct user download.** Files here are
fetched by PAGE IDE's installer code at runtime. Use PAGE IDE itself — the
in-app LSP install flow handles everything.

Browse the current asset catalog at
**[monkshark.github.io/page-ide-assets](https://monkshark.github.io/page-ide-assets/)**.

## What's here

| Asset family | Tag                  | Content                                                                  |
|--------------|----------------------|--------------------------------------------------------------------------|
| Ruby         | `ruby-bundle`        | RubyInstaller-devkit + MSYS2 UCRT64 + solargraph + rbs (per Ruby version) |
| Java         | `jdtls-bundle`       | Eclipse JDT Language Server milestones (noarch JAR)                       |
| Dart         | `dart-sdk-bundle`    | Dart SDK stable releases (per OS / arch / version)                        |
| Flutter      | `flutter-sdk-bundle` | Flutter SDK stable releases (per OS / arch / version)                     |
| Go           | `gopls-bundle`       | Go SDK + prebuilt gopls (planned)                                        |

### Naming convention

All bundle filenames follow a single rule so installer / CI parsing stays
deterministic:

```
page-{language}-{tool}-{os}-{arch}-{version}.{ext}
```

- `language` — upstream language id (`ruby`, `go`, `java`, `dart`, `flutter`, …)
- `tool` — the bundled LSP / toolchain (`solargraph`, `gopls`, `jdtls`, `sdk`, …)
- `os` — `windows`, `macos`, `linux`, or `noarch`
- `arch` — `x86_64`, `aarch64`, or `noarch`
- `version` — upstream tool / runtime version
- `ext` — `zip` (Windows) or `tar.gz` (Unix-like / noarch)

The `noarch` value covers bundles whose payload is platform-independent
(currently only JDT-LS, which ships as JAR + launcher scripts that run
unmodified on every supported OS). PAGE IDE's installer falls back to a
`noarch` slot when no OS/arch-specific bundle is published.

Each release tag groups assets per OS / architecture / upstream version, e.g.:

```
ruby-bundle        / page-ruby-solargraph-windows-x86_64-3.4.6.zip
ruby-bundle        / page-ruby-solargraph-windows-x86_64-3.5.0.zip
jdtls-bundle       / page-java-jdtls-noarch-noarch-1.58.0.tar.gz
dart-sdk-bundle    / page-dart-sdk-linux-x86_64-3.5.0.tar.gz
dart-sdk-bundle    / page-dart-sdk-macos-aarch64-3.5.0.tar.gz
flutter-sdk-bundle / page-flutter-sdk-windows-x86_64-3.24.0.zip
```

## Upstream licenses

This repo redistributes prebuilt binaries of third-party software. **Each
bundle retains its upstream license** — there is no single LICENSE file
covering the assets. Representative components:

- Ruby — Ruby License / BSD 2-clause
- MSYS2 / MinGW-w64 / GCC — GPL / LGPL / various
- solargraph — MIT
- rbs — BSD 2-clause
- Go SDK — BSD 3-clause
- gopls — BSD 3-clause
- Eclipse JDT-LS — EPL 2.0

Refer to each upstream project for full license text.

The workflow YAML files in `.github/workflows/` are configuration scripts with
no creative content claim; treat them as public domain.

## Build pipelines

Bundles are produced by GitHub Actions in this repository
(`workflow_dispatch` only — no scheduled builds). Each pipeline is
self-contained and uploads its result as a release asset on the appropriate
bundle tag.

Run history is visible under the
[Actions tab](https://github.com/monkshark/page-ide-assets/actions).

## Override for offline / corporate mirrors

PAGE IDE honors `PAGE_*_OVERRIDE` environment variables that point installers
at an alternative bundle URL or local file path — useful when this repo is
unreachable. See the PAGE IDE LSP installer documentation for current variable
names.

## Contributing

This repository is automation-managed. **Pull requests and issues are not
accepted here.** File feedback on the
[PAGE IDE repository](https://github.com/monkshark/page-ide) instead.

---

# page-ide-assets (한국어)

[PAGE IDE](https://github.com/monkshark/page-ide) 내부용 에셋 저장소입니다.
PAGE IDE 의 내장 인스톨러가 런타임에 자동으로 받아가는 LSP·툴체인 프리빌트
번들을 보관합니다.

**이 저장소는 사용자가 직접 다운로드하는 용도가 아닙니다.** 파일들은 PAGE IDE
인스톨러 코드가 알아서 가져옵니다. PAGE IDE 의 LSP 설치 흐름을 그대로
사용하세요.

현재 보관 중인 에셋은
**[monkshark.github.io/page-ide-assets](https://monkshark.github.io/page-ide-assets/)**
에서 한눈에 확인할 수 있습니다.

## 보관 항목

| 에셋 종류 | 태그                 | 내용                                                                |
|-----------|----------------------|---------------------------------------------------------------------|
| Ruby      | `ruby-bundle`        | RubyInstaller-devkit + MSYS2 UCRT64 + solargraph + rbs (Ruby 버전별) |
| Java      | `jdtls-bundle`       | Eclipse JDT Language Server 마일스톤 (noarch JAR)                    |
| Dart      | `dart-sdk-bundle`    | Dart SDK stable 릴리스 (OS / arch / 버전별)                          |
| Flutter   | `flutter-sdk-bundle` | Flutter SDK stable 릴리스 (OS / arch / 버전별)                       |
| Go        | `gopls-bundle`       | Go SDK + 프리빌트 gopls (예정)                                       |

### 네이밍 규칙

번들 파일명은 단일 규칙을 따라 인스톨러·CI 파싱이 일관됩니다:

```
page-{language}-{tool}-{os}-{arch}-{version}.{ext}
```

`os` / `arch` 자리는 일반적으로 `windows` / `macos` / `linux` × `x86_64` /
`aarch64` 조합입니다. 페이로드 자체가 플랫폼 독립인 번들 (현재 JDT-LS) 은
두 자리 모두 `noarch` 입니다 — PAGE IDE 인스톨러가 OS/arch 일치 번들을 못
찾으면 `noarch` 자리로 폴백합니다.

예시:

```
ruby-bundle        / page-ruby-solargraph-windows-x86_64-3.4.6.zip
jdtls-bundle       / page-java-jdtls-noarch-noarch-1.58.0.tar.gz
dart-sdk-bundle    / page-dart-sdk-linux-x86_64-3.5.0.tar.gz
dart-sdk-bundle    / page-dart-sdk-macos-aarch64-3.5.0.tar.gz
flutter-sdk-bundle / page-flutter-sdk-windows-x86_64-3.24.0.zip
```

각 릴리즈 태그는 OS / 아키텍처 / 업스트림 버전별로 묶입니다.

## 업스트림 라이선스

프리빌트 바이너리를 재배포하는 저장소이므로 **각 번들은 업스트림 라이선스를
그대로 유지**합니다. 전체를 덮는 단일 LICENSE 파일은 두지 않습니다. 주요
구성요소 라이선스는 영문 섹션의 목록과 동일합니다.

`.github/workflows/` 의 워크플로 YAML 은 단순 설정 스크립트로 창작물 청구가
없습니다 — public domain 로 취급하세요.

## 빌드 파이프라인

번들은 이 저장소의 GitHub Actions 에서 생성됩니다 (`workflow_dispatch` 전용,
스케줄 빌드 없음). 각 파이프라인은 자체 완결형이며 해당 번들 태그에 결과를
릴리즈 에셋으로 업로드합니다.

실행 기록은 [Actions 탭](https://github.com/monkshark/page-ide-assets/actions)
에서 볼 수 있습니다.

## 오프라인 / 사내 미러 우회

PAGE IDE 는 `PAGE_*_OVERRIDE` 환경변수를 인식해 인스톨러가 대체 번들 URL 또는
로컬 파일 경로를 사용하도록 할 수 있습니다 — 이 저장소가 막혀 있는 환경에서
유용합니다. 현재 변수명은 PAGE IDE LSP 인스톨러 문서를 참고하세요.

## 기여

이 저장소는 자동화로 관리됩니다. **PR / 이슈를 받지 않습니다.** 피드백은
[PAGE IDE 저장소](https://github.com/monkshark/page-ide)에 남겨주세요.
