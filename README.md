# shared-workflows

[![License](https://img.shields.io/github/license/kevnm67/shared-workflows)](LICENSE)

Reusable GitHub Actions workflows for iOS/Swift projects.

<details>
<summary>Table of Contents</summary>

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

- [Workflows](#workflows)
  - [📖 Documentation](#-documentation)
  - [🧹 SwiftLint](#-swiftlint)
  - [🏷️ PR Labeler](#-pr-labeler)
  - [📏 PR Size](#-pr-size)
  - [🕰️ Stale](#-stale)
  - [📦 Release Drafter](#-release-drafter)
- [Quick Start](#quick-start)
- [Templates](#templates)
- [License](#license)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

</details>

## Workflows

### 📖 Documentation

[`.github/workflows/docs.yml`](.github/workflows/docs.yml)

Generates TOC with doctoc, lints markdown, checks links, and optionally syncs to GitHub Wiki. Auto-commits any fixes.

| Input | Type | Default | Description |
|-------|------|---------|-------------|
| `readme_path` | string | `README.md` | Path to README for TOC generation |
| `wiki_sync` | boolean | `false` | Sync docs/ to GitHub Wiki |
| `lint_strict` | boolean | `false` | Fail on markdownlint warnings |

**Usage:**

```yaml
jobs:
  docs:
    uses: kevnm67/shared-workflows/.github/workflows/docs.yml@main
    with:
      readme_path: README.md
      lint_strict: true
```

---

### 🧹 SwiftLint

[`.github/workflows/swift-lint.yml`](.github/workflows/swift-lint.yml)

Runs SwiftLint with inline PR annotations.

| Input | Type | Default | Description |
|-------|------|---------|-------------|
| `swiftlint_config` | string | `.swiftlint.yml` | Path to SwiftLint config |
| `strict` | boolean | `false` | Fail on warnings |
| `reporter` | string | `github-actions-logging` | Reporter format |

**Usage:**

```yaml
jobs:
  lint:
    uses: kevnm67/shared-workflows/.github/workflows/swift-lint.yml@main
    with:
      strict: true
```

---

### 🏷️ PR Labeler

[`.github/workflows/pr-labeler.yml`](.github/workflows/pr-labeler.yml)

Auto-labels PRs based on changed file paths. Requires a `.github/labeler.yml` in your repo. See [`.github/labeler.yml`](.github/labeler.yml) for a starter config.

**Default labels:** `ci`, `fastlane`, `docs`, `tests`, `ui`, `dependencies`, `config`

**Usage:**

```yaml
jobs:
  labeler:
    uses: kevnm67/shared-workflows/.github/workflows/pr-labeler.yml@main
```

> **Note:** Copy [`.github/labeler.yml`](.github/labeler.yml) to your repo's `.github/labeler.yml` and customize as needed.

---

### 📏 PR Size

[`.github/workflows/pr-size.yml`](.github/workflows/pr-size.yml)

Labels PRs by diff size: `size/XS` (<10), `size/S` (<50), `size/M` (<200), `size/L` (<500), `size/XL` (500+).

**Usage:**

```yaml
jobs:
  pr-size:
    uses: kevnm67/shared-workflows/.github/workflows/pr-size.yml@main
```

---

### 🕰️ Stale

[`.github/workflows/stale.yml`](.github/workflows/stale.yml)

Marks stale issues and PRs, then closes them after a grace period.

| Input | Type | Default | Description |
|-------|------|---------|-------------|
| `days_before_stale` | number | `30` | Days of inactivity before marking stale |
| `days_before_close` | number | `7` | Days after stale label before closing |
| `stale_label` | string | `stale` | Label to apply |

**Usage:**

```yaml
jobs:
  stale:
    uses: kevnm67/shared-workflows/.github/workflows/stale.yml@main
    with:
      days_before_stale: 60
```

---

### 📦 Release Drafter

[`.github/workflows/release-drafter.yml`](.github/workflows/release-drafter.yml)

Auto-drafts GitHub releases from merged PRs. Categorizes changes into Features, Bug Fixes, CI/CD, Documentation, and Dependencies. Requires [`.github/release-drafter.yml`](.github/release-drafter.yml) in your repo.

**Usage:**

```yaml
jobs:
  release:
    uses: kevnm67/shared-workflows/.github/workflows/release-drafter.yml@main
```

> **Note:** Copy [`.github/release-drafter.yml`](.github/release-drafter.yml) to your repo and customize categories/labels.

---

## Quick Start

Copy [`workflow-starter.yml`](workflow-starter.yml) to `.github/workflows/shared.yml` in your repo. That's it.

## Templates

- **[`workflow-starter.yml`](workflow-starter.yml)** — All-in-one workflow that calls every shared workflow
- **[`.github/README-TEMPLATE.md`](.github/README-TEMPLATE.md)** — Starter README with badges, doctoc TOC, and standard sections
- **[`.github/labeler.yml`](.github/labeler.yml)** — PR labeler config for iOS/Swift projects
- **[`.github/release-drafter.yml`](.github/release-drafter.yml)** — Release drafter categories and autolabeler

## License

MIT
