# Package Zip

Composite action that builds a WordPress/WooCommerce-ready zip from a cleaned release branch checkout, optionally uploads it as a workflow artifact, and can attach it to an existing GitHub Release.

## Features
- Stages files under `{slug}/` and produces `{slug}.zip` (correct layout for plugin installs and WooCommerce.com uploads).
- Excludes `.git` only — expects the source tree to already be cleaned (e.g. `.gitattributes` `export-ignore` paths removed by `build-to-branch`).
- Optionally uploads the zip as a workflow artifact.
- Optionally attaches the zip to a GitHub Release by tag (updates an existing release if present).

## Prerequisites
Run this against the **release branch** working tree after `build-to-branch` (or equivalent) has:
- committed built assets
- removed `export-ignore` paths
- included `vendor/` when Composer is used

Do **not** package from `main` unless that tree is already export-clean.

## Key Inputs
- `slug` (required): Folder and zip basename (e.g. `my-plugin-name`).
- `source_directory` (default `.`): Root directory to package.
- `upload_artifact` (default `true`): Upload the zip as a workflow artifact.
- `artifact_name` (optional): Artifact name; defaults to `slug`.
- `release_tag` (optional): If set, attach the zip to this GitHub release tag.
- `github_token` (default `${{ github.token }}`): Token used when attaching to a release.

## Outputs
- `zip_path`: Absolute path to the generated zip.
- `zip_name`: Zip filename (`{slug}.zip`).

## Usage

Standalone (after checking out the release branch):

```yaml
jobs:
  package:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
        with:
          ref: release
      - uses: eighteen73/github-actions/.github/actions/package-zip@main
        with:
          slug: example-plugin
          release_tag: v1.2.3
          github_token: ${{ secrets.GITHUB_TOKEN }}
```

Prefer the reusable workflow when possible — `build-and-release-node.yml` runs this automatically after tagging.
