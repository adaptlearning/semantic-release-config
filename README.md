# Adapt semantic-release-config

Shared [semantic-release](https://github.com/semantic-release/semantic-release) configuration and reusable GitHub Actions workflow for adapt-authoring modules.

## What's included

- **Shared config** (`index.js`) — commit analyzer and release notes using the [ESLint preset](https://github.com/conventional-changelog/conventional-changelog/tree/master/packages/conventional-changelog-eslint), plus npm, GitHub, and git plugins
- **Reusable workflow** (`.github/workflows/release.yml`) — a GitHub Actions workflow that runs semantic-release on push to the default branch

## Setup

### 1. Install the config package

```bash
npm install --save-dev @adaptlearning/semantic-release-config
```

### 2. Add release config to `package.json`

Replace any inline `release` config with:

```json
{
  "release": {
    "extends": "@adaptlearning/semantic-release-config"
  }
}
```

### 3. Use the reusable workflow

Replace your `.github/workflows/releases.yml` with:

```yaml
name: Release

on:
  push:
    branches:
      - master

jobs:
  release:
    uses: adaptlearning/semantic-release-config/.github/workflows/release.yml@master
    secrets:
      NPM_TOKEN: ${{ secrets.NPM_TOKEN }}
```

### 4. Remove redundant devDependencies

The following are now provided by this package and can be removed from your `devDependencies`:

- `semantic-release`
- `@semantic-release/git`
- `conventional-changelog-eslint`
