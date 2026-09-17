# Your first scan should end with one checked connection

Turn a map into a review decision: pick one helper, follow one caller, and check that relationship against your actual source. This kit adds a completion receipt and troubleshooting path to the [existing setup walkthrough](https://github.com/kevin-lozada-santos/brain-scanner-walkthrough#map-a-small-project-of-your-own).

**[SCAN YOUR PROJECT](https://brainscanner.dev/connect?utm_source=github&utm_medium=owned&utm_campaign=first_scan_20260917)**

## Connect, then start small

1. Create a Brain Scanner account and verify your email. Website sign-in and agent authorization are separate.
2. Follow the [connection instructions](https://brainscanner.dev/connect) in a compatible agent. Add `https://brainscanner.dev/mcp/v2` as remote Streamable HTTP MCP and complete the client's OAuth flow. Review the displayed consent; keep authorization codes and redirect addresses out of chat. If your agent session predates authorization, start a new session after the client confirms completion.
3. Open a repository you are allowed to inspect. Pick one function or file and use the prompt below.
4. Open the saved map, inspect one relation against source, and fill in the receipt. Compare the mapped source revision with the current checkout before relying on it.

The public demonstration used Codex with an existing authorization. It establishes neither a fresh setup time nor compatibility with every agent. [Setup source](https://brainscanner.dev/connect) · [Demonstration boundary](https://github.com/kevin-lozada-santos/brain-scanner-walkthrough/blob/main/p-limit-dependency-example.md)

## Copyable first-scan prompt

> Map this project in Brain Scanner, starting with [one function or file]. Keep the scope small and leave source code unchanged. Save project metadata only: exclude source-file contents, raw diffs, logs, secrets, credentials, and private prompt text. Identify the source revision and saved graph version. Open the saved map and show one caller relationship with a source reference. Compare that relationship with the actual source at that revision. Identify a relevant test without claiming it has run. List missing, uncertain, or omitted relationships explicitly. Return a first-scan receipt with the fields below. If a required capability is unavailable, name the step that stopped instead of claiming a saved map.

This is a natural-language request, not a tool API. Actual results depend on the client's available tools and project access. The hosted authorization manages metadata; local source access remains subject to the permissions already granted to your agent. [Access boundary](https://brainscanner.dev/connect)

## Keep this receipt privately

[Download the blank receipt](https://raw.githubusercontent.com/kevin-lozada-santos/brain-scanner-walkthrough/main/first-scan-receipt.txt) or copy the template below. Fill it locally; it is not automatically sent anywhere.

```text
First-scan receipt
Date:
Agent/client:
Repository or project label (private):
Requested scope (one function/file):
Actual mapped scope:
Current source revision:
Mapped source revision (or unknown):
Saved graph version:
Saved map URL (private; do not post publicly):
One relation: [caller] -> [callee]
Source reference inspected:
Independent source check: confirmed / contradicted / not checked
Relevant test reference (not an execution claim):
Missing, omitted, or uncertain relationships:
Next file or test to inspect:
Status: connected only / map saved / relation checked / blocked
Blocked step, if any:
```

A first result means a saved map plus one relationship you checked against the matching source revision. A connection alone does not establish this result. An unknown revision or uninspected relationship stays unresolved. Do not publish a private map URL, path, or project label to ask for help.

## If you get stuck

| Where you stopped | Next step | What to report safely |
|---|---|---|
| Account or sign-in | Finish email verification, then return to the client's authorization flow. | Client name and “email verification” or “website sign-in.” |
| Signed in, connector unavailable | Check that your client supports the remote MCP/OAuth requirements on the connect page. | Client/version and “connector setup.” |
| Consent approved, agent still unauthorized | Confirm the initiating client finished authorization. Start a new agent session. If an interrupted attempt left an empty credential, follow the connect page's reconnect instructions. | “Client authorization did not finish,” without codes or redirect URLs. |
| Connected, no saved map | Ask the agent which mapping step stopped and whether it can inspect the selected local scope and save metadata. Do not count a connection or an empty dashboard as a scan. | “Connected; mapping stopped at [step],” with no project content. |
| Map saved, relation absent or revision unknown | Record the gap. Inspect the source and ask for a scoped refresh or correction before relying on the relationship. | “Map saved; relation/revision check unresolved.” |

The authorization recovery steps come from the [connect page](https://brainscanner.dev/connect). The map/revision checks are acceptance criteria for this exercise, not a guarantee that a particular mapping tool will succeed.

## A concrete result to compare with

In the public p-limit example, the saved map led from `limitFunction` through `pLimit` to `validateConcurrency`. Source inspection also found the validator in a concurrency setter that lacked a separate map node. That missing detail changed the review checklist. [Read the example and pinned source](https://github.com/kevin-lozada-santos/brain-scanner-walkthrough/blob/main/p-limit-dependency-example.md).

The later local checks separately recorded successful runtime/type checks and a failed combined `npm test` command. A map did not run those tests or make the full command pass. [Read the runtime evidence](https://github.com/kevin-lozada-santos/brain-scanner-walkthrough/blob/main/p-limit-runtime-checks.md).

Maps can omit relationships. This workflow does not automatically capture every source change, provide prompt-to-diff attribution, or replace Git review and tests. Keep those records separately and inspect current source before accepting an edit.

Need help? Email support@brainscanner.dev with your client and the step reached. Prepared by Kevin Lozada Santos's AI assistant for Brain Scanner; the example is an owner demonstration, not a customer result.
