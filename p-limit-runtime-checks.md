# Checking the public paths behind the map

The [caller-map example](p-limit-dependency-example.md) pointed to two creation paths and, after source inspection, a setter path. On September 11, 2026, Kevin's AI assistant checked those paths locally against the same pinned [p-limit revision](https://github.com/sindresorhus/p-limit/commit/783068bb9e967fd7bea8642e1bf5a3627fe38bdf).

**The runtime checks passed. The combined upstream test command did not pass.** These results extend the original source-review demonstration; they do not change what its earlier saved session recorded.

| Check | Result | What it establishes |
|---|---|---|
| Upstream `npm test` (`xo && ava && tsd`) | Exit 1 during `xo` | The full command failed in this environment. Its runtime and type stages did not run through this command. |
| Upstream AVA, invoked separately | Exit 0; **23 tests passed** | Existing runtime tests passed against the unchanged pinned source in this local run. |
| Upstream `tsd`, invoked separately | Exit 0 | Existing type tests passed in this environment. |
| Supplemental public-path script below | Exit 0; **47 assertions passed** | The selected invalid and valid values behaved as described below through the three public paths. |

Environment: Windows, Node.js 22.23.1, npm 10.9.8. Installed direct packages included AVA 6.4.1, tsd 0.33.0, XO 1.2.3, and yocto-queue 1.2.2. Dependencies were installed with `--ignore-scripts --no-audit --no-fund`. The upstream revision has no committed dependency lockfile; future installs can resolve differently. The sample's tracked files were unchanged after the checks.

The lint failure reported that `index.d.ts` and `index.test-d.ts` were not found by the TypeScript project service. It also emitted one TODO-comment warning. This report does not attribute the cause to an upstream defect, and no lint configuration was changed to make the command pass.

## What the additional check covered

Before a proposed validator edit, state the assumption: **creating a limiter and changing an existing limiter should enforce the same valid-concurrency rules.** Then inspect the public paths where callers rely on it.

The upstream runtime suite checks invalid values through `pLimit` creation, valid concurrency increases and decreases through the setter, and `limitFunction` execution. Source review did not find a setter test that supplies invalid concurrency values in this revision. That is a specific coverage observation, not a claim that the library behaves incorrectly.

The supplemental script checks eight invalid values—zero, negative one, a fraction, undefined, true, an object, NaN, and negative infinity—through `pLimit`, `limitFunction`, and the setter. All three paths throw `TypeError` for these inputs. A rejected setter assignment preserves the previous concurrency value. It also checks 1, 2, and positive infinity through those paths and confirms that a submitted task returns its result.

The 47 assertions are 8 invalid inputs × 4 checks plus 3 valid inputs × 5 checks. They do not exhaust JavaScript values, scheduling interleavings, or concurrency behavior. The graph itself was not regenerated or changed. These are local checks of an open-source sample, not Brain Scanner product tests, a customer result, or a performance benchmark.

## Repeat the check

In an isolated folder, clone the sample and select the exact revision:

```powershell
git clone https://github.com/sindresorhus/p-limit.git p-limit-validation
git -C p-limit-validation checkout --detach 783068bb9e967fd7bea8642e1bf5a3627fe38bdf
cd p-limit-validation
npm install --ignore-scripts --no-audit --no-fund
npm test
.\node_modules\.bin\ava.cmd
.\node_modules\.bin\tsd.cmd
cd ..
```

Save the following script as `p-limit-public-path-check.mjs` beside the `p-limit-validation` folder, then run `node p-limit-public-path-check.mjs`. The code imports that local sample; it does not contact Brain Scanner.

```javascript
import assert from 'node:assert/strict';
import pLimit, {limitFunction} from './p-limit-validation/index.js';

const invalid = [0, -1, 1.2, undefined, true, {}, NaN, -Infinity];
const valid = [1, 2, Infinity];
let assertions = 0;
for (const value of invalid) {
  assert.throws(() => pLimit(value), TypeError);
  assert.throws(() => limitFunction(() => 'ok', {concurrency: value}), TypeError);
  const existing = pLimit(2);
  assert.throws(() => { existing.concurrency = value; }, TypeError);
  assert.equal(existing.concurrency, 2, 'Rejected assignment preserves previous concurrency');
  assertions += 4;
}
for (const value of valid) {
  const fresh = pLimit(value);
  assert.equal(fresh.concurrency, value);
  assert.equal(await fresh(() => 'ok'), 'ok');
  const wrapped = limitFunction(() => 'ok', {concurrency: value});
  assert.equal(await wrapped(), 'ok');
  const existing = pLimit(2);
  existing.concurrency = value;
  assert.equal(existing.concurrency, value);
  assert.equal(await existing(() => 'ok'), 'ok');
  assertions += 5;
}
console.log(JSON.stringify({
  sourceRevision: '783068bb9e967fd7bea8642e1bf5a3627fe38bdf',
  checks: assertions,
  invalidValues: 8,
  validValues: 3,
  paths: ['pLimit initialization', 'limitFunction initialization', 'existing limiter concurrency setter'],
  result: 'passed',
  scope: 'Supplemental local public-API assertions; not upstream tests, a Brain Scanner test, a benchmark, or comprehensive concurrency testing.'
}, null, 2));

```

## Try the mapping step

To explore the same review workflow, [create a free Brain Scanner beta account](https://brainscanner.dev/signup), [connect your coding agent](https://brainscanner.dev/connect), and follow the [first-map steps](README.md#map-a-small-project-of-your-own). Start with one public helper. Ask for its callers and source references before changing code, then identify which public-path tests address the assumption you want to preserve.

The demonstrated mapping client was Codex. A saved graph can miss relationships, as the setter example shows. Use the source and tests to check the proposed review boundary.
