# Tag and Release

Composite action that creates a Git tag and a GitHub release based on the version specified in a WordPress plugin header.

## Features
- Reads the `Version` header from a WordPress plugin file.
- Creates a `vX.Y.Z` git tag based on the extracted version.
- Checks if the tag already exists and aborts if it does.
- Pushes the tag to the remote repository.
- Creates a GitHub release with the tag, using an automated release body.

## Key Inputs
- `plugin_file` (required): Path to the main WordPress plugin file containing the `Version` header.
- `target_branch` (required): Branch to tag (e.g., `release`).
- `github_token` (required): GitHub token used to create tags and releases.

## Outputs
- `version`: Extracted version from the plugin file.
- `tag`: Generated git tag (prefixed with `v`).
- `tag_exists`: Boolean indicating whether the tag already exists.

## Usage

```yaml
jobs:
  release:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: eighteen73/github-actions/.github/actions/tag-and-release@v1
        with:
          plugin_file: "wp-content/plugins/example-plugin/example-plugin.php"
          target_branch: "release"
          github_token: ${{ secrets.GITHUB_TOKEN }}
```

Adjust the `uses` reference (`@v1`) to match your chosen tag or commit.
