# The agent said “tests passed.” Which check passed?

Before accepting an agent's next edit, ask for a review you can follow: the behavior at risk, the paths that reach it, and the evidence for each check.

That request has recognizable roots. A [Codex issue](https://github.com/openai/codex/issues/31424) describes difficulty tracing task changes back to files and prompts. A [Claude Code feature request](https://github.com/anthropics/claude-code/issues/44787) asks for finer-grained review with feedback context. These are individual reports, not proof that every current client has the same problem. They do suggest a useful discipline: make the next decision inspectable.

Brain Scanner's public p-limit exercise gives that discipline a small, concrete example. At the pinned source revision, the saved map showed `limitFunction → pLimit → validateConcurrency`. Inspecting source added another place to review: changing an existing limiter through its concurrency setter. The map had not exposed that setter as a separate node. That is a reason to compare a map with source before trusting the review boundary. [Caller evidence and source links](https://github.com/kevin-lozada-santos/brain-scanner-walkthrough/blob/main/p-limit-dependency-example.md)

The follow-up runtime check made the lesson sharper. The configured `npm test` command failed during lint. Separately invoked AVA tests and type checks passed, along with a small supplemental check of the selected public paths. Calling the whole result “tests passed” would erase a failed criterion. The record includes the environment, unchanged revision, exact scope, and reproduction script; these were local sample checks, not Brain Scanner product tests. [Complete runtime evidence](https://github.com/kevin-lozada-santos/brain-scanner-walkthrough/blob/main/p-limit-runtime-checks.md)

Use that distinction on your own next task. Write the outcome before asking for a change. Name what must stay true, identify where callers depend on it, and keep each check's result attached to the criterion it actually addresses. If the full configured test command is required, a successful component suite cannot substitute for it.

Start smaller than the entire repository. Choose one validator or shared helper. Connect your agent, ask for a focused map, and check one relationship against the current source revision. Record the scope, saved graph version, source reference, missing relationships, and the next file or test to inspect. That receipt makes it clear whether you merely connected or obtained a useful first result. [Connection instructions](https://brainscanner.dev/connect)

Brain Scanner does not automatically capture every source change or establish which prompt produced every diff. Keep Git review and actual test evidence. A saved map can miss relationships, and a recorded test result still needs inspection. The demonstrated mapping used an existing owner account in Codex; it is not a customer testimonial or a fresh onboarding timing claim.

Try one small scope and leave with one checked connection. Use the [first-scan kit](first-scan-kit.md) for the prompt, private receipt, and troubleshooting steps.

**[SCAN YOUR PROJECT](https://brainscanner.dev/connect?utm_source=github&utm_medium=owned&utm_campaign=first_scan_20260917)**

Prepared by Kevin Lozada Santos's AI assistant for Brain Scanner. p-limit belongs to its upstream maintainers; the example does not imply their endorsement.
