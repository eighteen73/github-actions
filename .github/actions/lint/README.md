# Lint Suite

Composite action that provisions PHP and Node toolchains, installs dependencies, and runs `phpcs`, `eslint`, and `stylelint` with WordPress-friendly defaults.

## Features
- Uses `shivammathur/setup-php` to install PHP 8.3 plus optional extensions and INI overrides.
- Installs Composer packages (with caching) before invoking `phpcs`.
- Installs Node dependencies (default `npm ci`) and runs ESLint/Stylelint with configurable paths.
- All commands execute relative to an optional `working-directory` input to support monorepos.

## Key Inputs
- `php-version` (default `8.3`): PHP runtime for `phpcs`.
- `composer-install` / `composer-args`: control Composer bootstrap behaviour (dev dependencies are installed by default).
- `node-version` (default `24`) and `npm-install-command`: manage Node toolchain setup.
- `run-phpcs`, `run-eslint`, `run-stylelint`: toggle individual lint tasks (all enabled by default).
- `phpcs-standard` (leave empty to use local `phpcs.xml`), `eslint-paths`, `stylelint-paths`: override lint targets and rules without editing the action.

A full list lives in `action.yml`.

## Outputs
This action does not expose outputs; failures bubble up through command exit codes.

## Usage

```yaml
jobs:
  lint:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: eighteen73/github-actions/.github/actions/lint@v1
        with:
          working-directory: wp-content/plugins/example-plugin
          phpcs-standard: WordPressVIPMinimum
          eslint-paths: assets/js src
          stylelint-paths: assets/css/**/*.scss
```

Adjust the `uses` reference (`@v1`) to match your chosen tag or commit.
