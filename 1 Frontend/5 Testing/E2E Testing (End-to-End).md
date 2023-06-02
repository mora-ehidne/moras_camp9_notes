In E2E testing a user flow is tested - a complete flow of an application.

E2E Testing tools:

1. Selenium
2. Pupeteer
3. Playwright

# Playwright

A Node.js library that automates Firefox, Chromium and other browsers.

## Setup

Package installation command:
`pnpm dlx create-playwright`

Script to run playwight test: 
`"e2e": "playwright test"`

## Playwright Config

When Playwright is installed, it creates a `playwright.config.ts`.
Inside of `playwright.config.ts`, the `projects` array contains the browser it will use for testing.

## Running tests

the `playwright test` command has to specify the test file from which tests will be run.
eg: `playwright test example` for running tests from the file `Example.spec.ts`

In order to specify which worker (browser) to use, the flag `--project=` can be used, eg:
`pnpm playwright test --project=chromium`.

Each test in the file will be run in a separate worker (browser).

## Writing tests

It makes sense to write at least 1 happy path and 1 unhappy path.

## Debugging

Before running a test, the command `PWDEBUG=1` enables debug mode for the test run.
In the debug mode, the Playwright inspector will open. 
In the Inspector, we used the `Pick locator` button to select a locator from the page.