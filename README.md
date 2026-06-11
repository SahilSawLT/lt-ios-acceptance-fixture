# LambdaTest iOS Acceptance Kit — Fixture

This is the exact HTML fixture from
`Playwright real-iOS acceptance kit / Part 2 / locator-acceptance-test.js`
hosted as a static page so it can be loaded via a real `http://` URL.

**Live URL**: <https://sahilsawlt.github.io/lt-ios-acceptance-fixture/>

## Why this exists

The acceptance kit's Part 2 loads its fixture via a `data:text/html,...` URL
for hermeticity. On iOS Safari driven through Apple's Web Inspector protocol,
`Page.navigate(data:URL)` deadlocks the page-target's debug connection
(WebKit-level limitation, independent of any test logic).

Hosting the same fixture at a real URL bypasses that platform limitation
entirely. Locator engine results are identical to the data: URL case once
the navigation completes — which proves the kit's gating questions
(`getByTestId`, `getByRole`, `getByLabel`) are answered correctly by the
LambdaTest iOS real-device fork.

## How to use

In `locator-acceptance-test.js`, replace the FIXTURE-loading goto:

```js
// before
await page.goto('data:text/html,' + encodeURIComponent(FIXTURE), { waitUntil: 'commit', timeout: 30_000 });
// after
await page.goto('https://sahilsawlt.github.io/lt-ios-acceptance-fixture/', { waitUntil: 'commit', timeout: 30_000 });
```
