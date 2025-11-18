# Build Node.js Project to Target Branch

This workflow automates installing dependencies, building a Node.js project, committing built assets to a release branch, and creating a versioned GitHub release based on a WordPress plugin file.

## Features
- Checks out the repository and sets up Node.js with caching.
- Runs the `Lint Suite` action to enforce PHP, JavaScript, and CSS standards.
- Merges a source branch into a release branch and builds project assets.
- Force-adds built assets to the release branch, overriding `.gitignore`.
- Extracts the plugin version and creates a Git tag and GitHub release.

## Key Inputs
- `source_branch` (required): Branch to merge from.
- `release_branch` (required): Branch to merge into and update with built assets.
- `built_asset_paths` (required): Paths to generated assets to forcibly include in the release commit.
- `build_script` (optional, default: `npm ci; npm run build`): Command to build project assets.
- `commit_user_name` (optional, default: `"eighteen73"`): Author name for commits.
- `commit_user_email` (optional, default: `"<>"`): Author email for commits.
- `node_version` (optional, default: `22`): Node.js version to use for the workflow.
- `plugin_file` (required): Path to the main WordPress plugin file used for tagging and releasing.

## Outputs
This workflow does not expose outputs; success is determined by command exit codes of the individual actions.

## Usage

```yaml
jobs:
  build-and-release:
    uses: eighteen73/github-actions/.github/workflows/build-node-to-branch.yml@main
    with:
      source_branch: "main"
      release_branch: "release"
      built_asset_paths: "dist/**"
      build_script: |
        npm ci
        npm run build
      commit_user_name: "Build Bot"
      commit_user_email: "bot@example.com"
      node_version: 22
      plugin_file: "wp-content/plugins/example-plugin/example-plugin.php"
```
