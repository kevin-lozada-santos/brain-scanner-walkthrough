# The unit tests passed. The requested check still failed.

> Verified on September 11, 2026 using the live MCP connection and the signed-in production Reports interface in Chrome. This is a synthetic owner demonstration.

A coding agent can report passing tests while a required check is still failing. The useful question is whether the evidence satisfies the specific thing you asked for.

Here is a small, real Brain Scanner example. We created synthetic owner test reports using previously recorded results from the public `p-limit` project. The outcome was deliberately simple: the repository's configured `npm test` command must pass.

The [underlying test record](https://github.com/kevin-lozada-santos/brain-scanner-walkthrough/blob/c79a85c4693b34d2cf7cd35b569215c313a70392/p-limit-runtime-checks.md) contains a failing full command caused by lint configuration errors, a passing AVA run with 23 tests, and passing type checks. These observations refer to `p-limit` source revision `783068bb9e967fd7bea8642e1bf5a3627fe38bdf`. No upstream source was changed for this demonstration.

We attached the results to separate criteria in a Brain Scanner report, saved it, and read it back through the live MCP connection:

| Criterion | Recorded result | Brain Scanner's saved review |
|---|---|---|
| The configured `npm test` command passes | Failed | Failure recorded |
| The AVA runtime test suite passes | Passed | Matching pass recorded |
| The `tsd` type checks pass | Passed | Matching pass recorded |

The passing components did not turn the full-command criterion into a pass. Saving a review baseline also left that failure visible.

## What stayed visible for the next session

The returned continuation brief included the requested outcome, selected source revision, each criterion and its evidence reference. It preserved these two distinct lines:

> The configured npm test command passes.: Failure recorded.
>
> The AVA runtime test suite passes.: Matching pass recorded.

Those are excerpts from the actual MCP response, with the following action text omitted. The production browser download preserved both review states, the selected source revision, and the warning that recorded evidence is not independently verified by Brain Scanner.

We also exercised three boundary cases with separate reads after saving:

- With no evidence supplied, the criteria remained missing.
- A clearly labeled synthetic passing result for a different revision produced a revision mismatch.
- Canceling that synthetic outcome persisted the cancellation and a do-not-resume instruction. A subsequent request to queue it was refused, and the queue stayed empty.

Cancellation blocks new queue admission. It does not stop work that was already queued or running.

## Try the same distinction on one project

[Connect Brain Scanner](https://brainscanner.dev/connect), then choose an existing project in your connected coding agent. Start with one requested outcome and two or three concrete criteria. Keep the evidence for each criterion separate.

For example:

> Create a clearly labeled review report for this project. Record the requested outcome and separate criteria for the full configured test command, runtime tests, and type checks. Attach only results I provide, each with its actual source revision and evidence reference. Keep missing or mismatched evidence unresolved. Read the saved report back and show the continuation brief. Do not run tests, edit source, or queue work as part of this recording step.

Inspect the evidence yourself before accepting the outcome. A matching recorded pass means that an observation was associated with the criterion and revision; it does not establish that the observation is true or that the chosen check covers the requirement.

## What this demonstration proves

This was an owner-controlled test of the deployed MCP report workflow: persistence, criterion-specific review states, continuation text, saved baseline behavior, and refusal to queue a canceled outcome. We also opened the saved reports in the signed-in production website, downloaded the continuation text, and confirmed that the canceled report showed a do-not-resume notice and no queue action. It used two synthetic reports and created no customer account. It is not a customer testimonial or evidence of market demand.

Brain Scanner did not execute the underlying tests, inspect arbitrary logs, discover a Git diff, or independently verify the supplied revision and path claims. The recorded outcomes help organize a review; they do not establish software correctness. Manual browser verification covered these existing report views and the download in Chrome; it did not cover report editing, other browsers, or the complete onboarding flow.

Demonstration run by Kevin Lozada Santos's AI assistant for Brain Scanner on September 11, 2026. Brain Scanner's implementation is private; this repository contains public walkthroughs and evidence.
