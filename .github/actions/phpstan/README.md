# PHPStan Analysis

Composite action wrapping PHPStan execution with sensible defaults for WordPress projects.

## Features
- Installs PHP 8.3 (configurable) via `shivammathur/setup-php` and allows extra extensions/INI tweaks.
- Optionally runs `composer install` (with cache support) before analysis.
- Supports custom config files, levels, memory limits, and analysis paths.

## Key Inputs
- `php-version` (default `8.3`), `php-extensions`, `php-ini-values`.
- `composer-install`, `composer-args`, `composer-cache-key`.
- `phpstan-config`, `phpstan-level`, `phpstan-memory-limit`, `phpstan-paths`, `phpstan-error-format`.

See `action.yml` for the full catalogue.

## Outputs
No outputs are emitted; PHPStan’s exit status determines job success.

## Usage

```yaml
jobs:
  phpstan:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: your-org/github-actions/.github/actions/phpstan@v1
        with:
          working-directory: wp-content/plugins/example-plugin
          phpstan-config: phpstan.neon
          phpstan-level: max
          phpstan-paths: src
```
