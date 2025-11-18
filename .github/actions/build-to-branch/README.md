# Build to Branch

Composite action that merges a source branch into a release branch, builds project assets, and force-commits generated files while preserving branch history.

## Features
- Configures Git user for automated commits.
- Merges a source branch into a release branch, simulating a “theirs” strategy for automatic conflict resolution of built files.
- Runs a customizable build script (default: `npm ci; npm run build`).
- Force-adds built assets to the release branch, overriding `.gitignore`.
- Cleans up files marked with `export-ignore` in `.gitattributes` before committing.
- Pushes the updated release branch back to the remote repository.

## Key Inputs
- `source_branch` (default `main`): Branch to merge from.
- `release_branch` (default `release`): Branch to merge into and update with built assets.
- `built_asset_paths` (required): Paths to generated assets to forcibly include in the commit.
- `build_script` (default `npm ci; npm run build`): Command to run to build assets.
- `commit_user_name` (default `"Your friendly neighborhood GH Actions Bot"`): Author name for commits.
- `commit_user_email` (default `"<>"`): Author email for commits.

## Outputs
This action does not expose outputs; success is determined by command exit codes.

## Usage

```yaml
jobs:
  build-release:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: eighteen73/github-actions/.github/actions/build-to-branch@v1
        with:
          source_branch: main
          release_branch: release
          built_asset_paths: "dist/**"
          build_script: |
            npm ci
            npm run build
          commit_user_name: "Build Bot"
          commit_user_email: "bot@example.com"
```

Adjust the `uses` reference (`@v1`) to match your chosen tag or commit.
