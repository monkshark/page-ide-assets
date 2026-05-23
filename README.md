# page-ide-assets

Internal asset repository for [PAGE IDE](https://github.com/monkshark/page-ide).
Stores prebuilt LSP and toolchain bundles that PAGE IDE's built-in installers
download automatically.

**This repository is not intended for direct user download.** Files here are
fetched by PAGE IDE's installer code at runtime. Use PAGE IDE itself — the
in-app LSP install flow handles everything.

## What's here

| Asset family | Tag                | Content                                                                  |
|--------------|--------------------|--------------------------------------------------------------------------|
| Ruby         | `ruby-bundle`      | RubyInstaller-devkit + MSYS2 UCRT64 + solargraph + rbs (per Ruby version) |
| Go           | `gopls-bundle`     | Go SDK + prebuilt gopls (planned)                                        |
| Java         | `jdtls-bundle`     | Eclipse JDT Language Server tar (planned)                                |

Each release tag groups assets per OS / architecture / upstream version, e.g.:

```
ruby-bundle / page-ruby-solargraph-windows-x86_64-3.4.6.zip
ruby-bundle / page-ruby-solargraph-windows-x86_64-3.5.0.zip
gopls-bundle / page-gopls-windows-x86_64-0.16.0.zip
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
