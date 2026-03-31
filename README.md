<div align="center" markdown>

![Copier TypeScript](https://socialify.git.ci/liblaf/copier-typescript/image?custom_language=TypeScript&description=1&forks=1&issues=1&language=1&logo=https%3A%2F%2Fraw.githubusercontent.com%2Fcopier-org%2Fcopier%2Frefs%2Fheads%2Fmaster%2Fimg%2Flogo.svg&name=1&owner=1&pattern=Transparent&pulls=1&stargazers=1&theme=Auto)

[![Made with Copier](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/copier-org/copier/master/img/badge/badge-black.json)](https://github.com/copier-org/copier)
[![Bun](https://img.shields.io/badge/Bun-000000?logo=bun)](https://bun.sh)
[![Checked with Biome](https://img.shields.io/badge/Checked_with-Biome-60a5fa?style=flat&logo=biome)](https://biomejs.dev)
[![Release / PR](https://github.com/liblaf/copier-typescript/actions/workflows/release-pr.yaml/badge.svg)](https://github.com/liblaf/copier-typescript/actions/workflows/release-pr.yaml)
[![Shared / MegaLinter](https://github.com/liblaf/copier-typescript/actions/workflows/shared-mega-linter.yaml/badge.svg)](https://github.com/liblaf/copier-typescript/actions/workflows/shared-mega-linter.yaml)

[Changelog](https://github.com/liblaf/copier-typescript/blob/main/CHANGELOG.md) · [Report Bug](https://github.com/liblaf/copier-typescript/issues) · [Request Feature](https://github.com/liblaf/copier-typescript/issues)

![Rule](https://cdn.jsdelivr.net/gh/andreasbm/readme/assets/lines/rainbow.png)

</div>

Copier template for TypeScript packages that layers on top of `gh:liblaf/copier-shared` and `gh:liblaf/copier-release`, generating a Bun-first library setup with Biome, GitHub Actions, and npm publishing via OIDC.

## ✨ Features

- 🧱 **Composable template stack:** Designed to be applied after `gh:liblaf/copier-shared` and `gh:liblaf/copier-release`, reusing shared answers and release automation instead of rebuilding them from scratch.
- ⚡ **Bun-first package workflow:** Generates `package.json` scripts for `build`, `lint`, `test`, and `type-check`, uses `bunup` for builds, and adds a `mise` enter hook that runs `bun install`.
- 🧼 **Opinionated library defaults:** Ships `biome.jsonc` and `tsconfig.json` that extend `@liblaf/config`, marks the package as ESM, and publishes only `dist/` with npm provenance enabled.
- 🧪 **CI that matches real projects:** The generated `typescript-test.yaml` packs the package on pushes and pull requests, runs tests only when `*.test.ts` files exist, uploads coverage and test results to Codecov, and runs `tsc --noEmit`.
- 🚀 **Release automation for npm:** Conventional commits feed the release PR flow from `copier-release`, while the generated `typescript-release.yaml` builds release artifacts, publishes to npm with OIDC, and uploads release assets.
- 🛡️ **Safer template application:** Skips overwriting existing `package.json`, `tsconfig.json`, `biome.jsonc`, `.gitignore`, and VS Code settings when those files are already present.

## 📦 Installation

> [!IMPORTANT]
> This template is meant to layer on top of `gh:liblaf/copier-shared` and `gh:liblaf/copier-release`.

```bash
copier copy --trust gh:liblaf/copier-shared my-package
copier copy --trust gh:liblaf/copier-release my-package
copier copy --trust gh:liblaf/copier-typescript my-package
```

When prompted, `package_name` defaults to `@<github_user>/<project_name_slug>`.

## 🚀 Quick Start

```bash
cd my-package
bun install
bun run lint
bun run test
bun run type-check
bun run build
```

Generated projects are ESM-first with `"type": "module"`. If you use `mise`, entering the project also adds `node_modules/.bin` to `PATH` and runs `bun install` automatically.

## 🔄 Release Flow

1. Write conventional commits on `main`.
2. `release-pr.yaml` computes the next version, updates `CHANGELOG.md`, and opens a release PR.
3. Merging that PR triggers `release-draft.yaml`, which tags the release and creates the GitHub release. If immutable releases are enabled, it creates a draft first.
4. Published releases trigger `typescript-release.yaml`, which packs the project, publishes to npm with OIDC and provenance, and uploads the built tarball as a release asset.
5. `release-publish.yaml` runs hourly and publishes drafts older than 6 hours when immutable releases are enabled.

> [!TIP]
> After scaffolding a new repository, use `setup-npm-trusted-publish` so the `npm` environment and trusted publisher are ready for OIDC-based publishing.

## ⌨️ Local Development

```bash
git clone https://github.com/liblaf/copier-typescript.git
cd copier-typescript
copier copy --trust gh:liblaf/copier-shared ../copier-typescript-sandbox
copier copy --trust gh:liblaf/copier-release ../copier-typescript-sandbox
copier copy --trust . ../copier-typescript-sandbox
```

Most day-to-day changes live in `copier.yaml` and `template/`. Recopying into a scratch repository is the quickest way to verify the generated package layout and workflows.

## 🤝 Contributing

Issues and pull requests are welcome, especially when they tighten the generated package surface, improve the release flow, or keep the Bun and Biome defaults sharp.

[![PR WELCOME](https://img.shields.io/badge/%F0%9F%A4%AF%20PR%20WELCOME-%E2%86%92-ffcb47?labelColor=black&style=for-the-badge)](https://github.com/liblaf/copier-typescript/pulls)

[![Contributors](https://contrib.nn.ci/api?repo=liblaf/copier-typescript)](https://github.com/liblaf/copier-typescript/graphs/contributors)

## 🔗 More Copier Templates

- **[Shared](https://github.com/liblaf/copier-shared)** - Base repository hygiene, shared automation, MegaLinter, and recurring maintenance workflows.
- **[Release](https://github.com/liblaf/copier-release)** - Conventional-commit release PRs, changelog generation, draft releases, and scheduled publish automation.
- **[Python](https://github.com/liblaf/copier-python)** - A modern Python project template with `mise`, Ruff, pytest, docs, and GitHub Actions.
- **[Rust](https://github.com/liblaf/copier-rust)** - A Rust project template with cross-compilation, CI, and release automation.

---

#### 📝 License

Copyright © 2024 [liblaf](https://github.com/liblaf). <br />
This project is [MIT](https://github.com/liblaf/copier-typescript/blob/main/LICENSE) licensed.
