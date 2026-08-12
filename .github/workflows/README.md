# Build Node.js Project to Target Branch

This workflow automates installing dependencies, building a Node.js project, committing built assets to a release branch, creating a versioned GitHub release based on a WordPress plugin file, and attaching a WooCommerce-ready zip to that release.

## Features
- Checks out the repository and sets up Node.js with caching.
- Runs the `Lint Suite` action to enforce PHP, JavaScript, and CSS standards.
- Merges a source branch into a release branch and builds project assets.
- Force-adds built assets to the release branch, overriding `.gitignore`.
- Extracts the plugin version and creates a Git tag and GitHub release.
- Packages `{plugin_slug}.zip` from the cleaned release branch and attaches it to the GitHub Release (also uploads a workflow artifact).

## Key Inputs
- `source_branch` (required): Branch to merge from.
- `release_branch` (required): Branch to merge into and update with built assets.
- `built_asset_paths` (required): Paths to generated assets to forcibly include in the release commit.
- `build_script` (optional, default: `npm ci --ignore-scripts; npm run build`): Command to build project assets.
- `commit_user_name` (optional, default: `"eighteen73"`): Author name for commits.
- `commit_user_email` (optional, default: `"<>"`): Author email for commits.
- `node_version` (optional, default: `22`): Node.js version to use for the workflow.
- `plugin_file` (required): Path to the main WordPress plugin file used for tagging and releasing.
- `plugin_slug` (optional): Plugin folder/zip basename. Defaults to the repository name.
- `php_version`, `php_extensions`, `php_ini_values`, `run_composer_install`, `composer_script`: optional PHP/Composer controls for the build step.

## Outputs
This workflow does not expose outputs; success is determined by command exit codes of the individual actions.

## Usage

```yaml
jobs:
  release:
    name: "Update release branch"
    uses: eighteen73/github-actions/.github/workflows/build-and-release-node.yml@main
    with:
      source_branch: main
      release_branch: release
      built_asset_paths: build
      run_composer_install: true
      node_version: 22
      plugin_file: example-plugin.php
      plugin_slug: example-plugin # optional if the repo name already matches the slug
```

The resulting GitHub Release includes `{plugin_slug}.zip`, ready to download and upload to WooCommerce.com.
