# TESTING.md

A reproducible workflow for dependency updates, validation scaffolds, and clean configs

> This repo uses **CommonJS (CJS)** module resolution
> Config files are `.cjs` for compatibility
> See section 06 for notes on harmonizing with ESM repos

## 01. Dependency Update Workflow

Install **npm-check-updates**:

- **Globally** (quick, not version‑pinned):
  ```sh
  npm install -g npm-check-updates
  ncu        # list outdated deps
  ncu -u     # update package.json
  npm install

# TESTING.md

A reproducible workflow for dependency updates, validation scaffolds, and clean configs

> This repo uses **CommonJS (CJS)** module resolution
> Config files are `.cjs` for compatibility
> See section 06 for notes on harmonizing with ESM repos

## 01. Dependency Update Workflow

Install **npm-check-updates**:

- **Globally** (quick, not version‑pinned):
  ```sh
  npm install -g npm-check-updates
  ncu        # list outdated deps
  ncu -u     # update package.json
  npm install

- **Locally** (per repo, reproducible)
```
npm install --save-dev npm-check-updates
npx npm-check-updates
npx npm-check-updates -u
npm install
```

Update with ncu

- Review available updates:
  - `npx npm-check-updates`
  - `npm install --save-dev npm-check-updates`

Apply updates:

- `npx npm-check-updates -u`
- `npm install`

## 02. Post-Update Checklist - confirming operational

- Run tests (if present)
  - `npm test`
- All tests pass — no regressions

Update Docs & Changelog

- Note version bumps in CHANGELOG.md
- Mention any new minimum Node/ESLint requirements

Commit the new baseline

- `git add package.json package-lock.json`
- `git commit -m "chore: deps updated via ncu; all checks passed"`

Optional: One‑Shot Validation Script to package.json

  - `"scripts": {
"validate": "eslint . --ext .js,.cjs,.mjs && prettier --check . && npm test"
}`
- Run after ncu:
  - npm run validate

## 03. Cleanup Tasks

- Remove and reinstall dependencies:
  - `rm -rf node_modules package-lock.json`
  - `npm install`
  - Guarantees node_modules matches what's in package.json and lockfile.

- Prune extraneous packages
  - `npm prune`
  - Removes anything unlisted in package.json

- Clear npm cache
  - `npm cache clean --force`
  - Affects local cache to speed up installs, doesn't touch /node_modules

## 04. Lint Validation - ESLint config and error checks

- `npx eslint . --ext .js,.cjs,.mjs`
- `npx prettier --check .`
- No new errors/warnings
- Prettier output matches ESLint expectations

Check Peer Dependencies

- `npm ls eslint prettier`
- Confirm versions satisfy updated package peer ranges

## 05. Prettier Validation - formatting consistency and config resolution

Create test file
`touch ./test.js`

Verify which config file is being used
`npx prettier --find-config-path ./test.js`

Run Prettier with a specific config file on a specific file
`npx prettier --config ./.prettier.config.cjs --write ./test.js`

Check if a single file passes the Prettier configuration
`npx prettier --check ./test.js`

Check if entire repo passes the Prettier configuration
`npx prettier --check .`

```sh
npm run prettier:testfile     # Format test.js using repo config
npm run prettier:force        # Overwrite all files with current config
npm run prettier:checkfile    # Check formatting of test.js
npm run prettier:checkall     # Check formatting across entire repo

```

Warning! Overwrite all files in repo with current Prettier config
`npx prettier --write .`

## 06. Config Drift - Notes

- This repo (CJS) vs. fse-learning (ESM):
  - .eslintrc.cjs and .prettierrc.cjs pinned here for CJS compatibility
  - Adjust extensions (.mjs, .js) when porting configs to ESM repos
- Quote/comma rules harmonized across repos for consistency

## 07. Debugging Node.js in VS Code

### Option 1: JS Debug Terminal (Quick & Dirty)
- Open `Terminal > New JavaScript Debug Terminal`
- Run your script manually: `node app.js`
- VS Code auto-attaches debugger

### Option 2: launch.json (Reproducible & Configurable)
- Create `.vscode/launch.json`
- Define entry point, env vars, console type, etc.
- Ideal for team projects and onboarding clarity

## 08. Preflight Setup

- Requires Node.js
- Uses CommonJS module resolution
- Install dependencies before running validation
```sh
npm install
```
All scripts and config paths are version-pinned for future maintainers.
Before running layout tests or validating formatting, install dependencies:

```sh
npm install
```


Update with ncu

- Review available updates:
  - `npx npm-check-updates`
  - `npm install --save-dev npm-check-updates`

Apply updates:

- `npx npm-check-updates -u`
- `npm install`

## 02. Post-Update Checklist - confirming operational

- Run tests (if present)
  - `npm test`
- All tests pass — no regressions

Update Docs & Changelog

- Note version bumps in CHANGELOG.md
- Mention any new minimum Node/ESLint requirements

Commit the new baseline

- `git add package.json package-lock.json`
- `git commit -m "chore: deps updated via ncu; all checks passed"`

Optional: One‑Shot Validation Script to package.json

  - `"scripts": {
"validate": "eslint . --ext .js,.cjs,.mjs && prettier --check . && npm test"
}`
- Run after ncu:
  - npm run validate

## 03. Cleanup Tasks

- Remove and reinstall dependencies:
  - `rm -rf node_modules package-lock.json`
  - `npm install`
  - Guarantees node_modules matches what's in package.json and lockfile.

- Prune extraneous packages
  - `npm prune`
  - Removes anything unlisted in package.json

- Clear npm cache
  - `npm cache clean --force`
  - Affects local cache to speed up installs, doesn't touch /node_modules

## 04. Lint Validation - ESLint config and error checks

- `npx eslint . --ext .js,.cjs,.mjs`
- `npx prettier --check .`
- No new errors/warnings
- Prettier output matches ESLint expectations

Check Peer Dependencies

- `npm ls eslint prettier`
- Confirm versions satisfy updated package peer ranges

## 05. Prettier Validation - formatting consistency and config resolution

Create test file
`touch ./test.js`

Verify which config file is being used
`npx prettier --find-config-path ./test.js`

Run Prettier with a specific config file on a specific file
`npx prettier --config ./.prettier.config.cjs --write ./test.js`

Check if a single file passes the Prettier configuration
`npx prettier --check ./test.js`

Check if entire repo passes the Prettier configuration
`npx prettier --check .`

```sh
npm run prettier:testfile     # Format test.js using repo config
npm run prettier:force        # Overwrite all files with current config
npm run prettier:checkfile    # Check formatting of test.js
npm run prettier:checkall     # Check formatting across entire repo

```

Warning! Overwrite all files in repo with current Prettier config
`npx prettier --write .`

## 06. Config Drift - Notes

- This repo (CJS) vs. fse-learning (ESM):
  - .eslintrc.cjs and .prettierrc.cjs pinned here for CJS compatibility
  - Adjust extensions (.mjs, .js) when porting configs to ESM repos
- Quote/comma rules harmonized across repos for consistency

## 07. Debugging Node.js in VS Code

### Option 1: JS Debug Terminal (Quick & Dirty)
- Open `Terminal > New JavaScript Debug Terminal`
- Run your script manually: `node app.js`
- VS Code auto-attaches debugger

### Option 2: launch.json (Reproducible & Configurable)
- Create `.vscode/launch.json`
- Define entry point, env vars, console type, etc.
- Ideal for team projects and onboarding clarity

## 08. Preflight Setup

- Requires Node.js
- Uses CommonJS module resolution
- Install dependencies before running validation
```sh
npm install
```
All scripts and config paths are version-pinned for future maintainers.
Before running layout tests or validating formatting, install dependencies:
