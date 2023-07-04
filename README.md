# Coverage Badge
> Works with private repos!

[![Build][test-shield]][test-url] ![Coverage][coverage_badge]

## Why?

I had to work on a few private repos and really wanted an automated coverage badge solution. However, a lot of the options available used third-party services. Thus, coverage-badge can create badges with nobody having access

## Guide

There are a few steps to set up the workflow to auto update a `README.md` or similar file

1. Add the following two sequential comment anywhere in your file. Preferably, push it to the bottom

    <code>\<!--&nbsp;Coverage&nbsp;Comment:Begin&nbsp;-->
    \<!--&nbsp;Coverage&nbsp;Comment:End&nbsp;--></code>
1. Add the following wherever you want to see the badge: `![Coverage][coverage_badge]`
1. Update your testing workflow as needed, make sure the `actions/checkout` can write in to your repo
    ```yaml
    ---
    on:
      push:
    jobs:
      test:
        name: Test the github action
        runs-on: ubuntu-latest
        permissions:
        contents: write
        steps:
        - uses: actions/checkout@v3
        - uses: kevinfjiang/coverage-badge@v1
        with:
          coverage: 100
          change_file: ./README.md
    ```

## Supported Parameters

| Parameter               | Description                                                | Default           |
| ----------------------- | ---------------------------------------------------------- | ----------------- |
| `coverage`\*\*          | Code coverage as a percentage in range [0, 100]            | `Required`        |
| `color`                 | Color of badge. {0-59: red, 60-89: yellow, 80-100: green}  | `""`              |
| `change_file`           | Files to be changed, default only outputs badge            | `""`              |
| `style`                 | [shield.io](https://shields.io/) styling of badge          | `"for-the-badge"`   |
## Outputs

The following output values can be accessed via `${{ steps.<step-id>.outputs.<output-name> }}`:

| Name                     | Description                                            | Type   |
| ------------------------ | ------------------------------------------------------ | ------ |
| `badge`                  | [shield.io](https://shields.io/) badge url             | string |

### Notes:

- Parameters denoted with `**` are required.
- The `change_file` parameter supports multi-line [glob](https://github.com/isaacs/node-glob) patterns, see repository examples.

[test-url]: https://github.com/kevinfjiang/coverage-badge/actions/workflows/test.yml
[test-shield]: https://img.shields.io/github/actions/workflow/status/kevinfjiang/coverage-badge/test.yml?style=for-the-badge

<!-- Coverage Comment:Begin -->
[coverage_badge]: https://img.shields.io/badge/Coverage-100%25-green.svg?style=for-the-badge
<!-- Coverage Comment:End -->
