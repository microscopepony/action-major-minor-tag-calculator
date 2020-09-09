# major-minor-tag-calculator GitHub Action

[![build-test](https://github.com/manics/action-major-minor-tag-calculator/workflows/build-test/badge.svg)](https://github.com/manics/action-major-minor-tag-calculator/actions)

Calculate major and minor semver tags, e.g. for tagging containers.

This will calculate major and minor prefix tags for when you want to provide users with a way to obtain the latest `major` or `major.minor` version.

Pre-releases are ignored.

## Examples

Current and latest tag: `1.2.3`, returned tags: `[1.2.3, 1.2.0, 1.0.0, latest]`.

Current tag `1.2.3` but the repository already contains a more recent tag `2.0.0`: return only `[1.2.3]`.

## Required input parameters

- `githubToken`: The GitHub token, required so this action can comment on pull requests.

## Optional input parameters

- `binderUrl`: Optionally specify an alternative BinderHub instead of mybinder.org.
  The URL `<binderUrl>/badge_logo.svg` must exist, and will be used as the badge for linking.

## Example

```yaml
name: binder-badge
on:
  pull_request_target:

jobs:
  badge:
    runs-on: ubuntu-latest
    steps:
      - uses: manics/action-binderbadge@main
        with:
          githubToken: ${{ secrets.GITHUB_TOKEN }}
```

## Developer notes

Install the dependencies:

```bash
$ npm install
```

Build the typescript, run the formatter and linter:

```bash
$ npm run build && npm run format && npm run lint
```

Package the code for distribution (uses [ncc](https://github.com/zeit/ncc)):

```bash
$ npm run package
```

Run the tests :heavy_check_mark:

```bash
$ npm test
```

The tests use [nock](https://github.com/nock/nock) to mock GitHub API responses, no real requests are made so manual testing is still required.

Shortcut:

```bash
$ npm run all
```

Actions are run from GitHub repos so you must checkin the packed `dist` folder:

```bash
$ npm run all
$ git add dist
$ git commit
$ git push origin main
```
