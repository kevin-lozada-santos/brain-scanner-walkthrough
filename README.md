# Brain Scanner: try a first useful project map

Public walkthrough materials for [Brain Scanner](https://brainscanner.dev/), a hosted workspace for projects built with coding agents. The open beta is free. This repository contains demo documentation and an illustrative screenshot, not the product implementation.

Published on behalf of the maker, Kevin Lozada Santos, by his authorized AI assistant.

## See the workspace before signing up

![Brain Scanner public demo: an illustrative project graph connects Source Code, Dashboard UI, Agent Workflow, and Tests and Validation. The inspector shows the selected Source Code node.](project-graph-demo.png)

*Screenshot of the public interactive example. All project names, counts, relationships and readiness values shown here are illustrative; they are not customer results or a production assessment.*

Open the [interactive demo](https://brainscanner.dev/) without an account:

1. In **Project Graph**, select a node and inspect its recorded relationship to another part of the example workspace.
2. In **Context**, choose **Sessions** to inspect sample recorded context.
3. In **Reports**, read **Dashboard review** and add **Preserve unsaved finding notes** to the queue. In **Queues**, inspect the linked task.

The preview sends no work to an agent. A queued item requests follow-up work; it does not establish that a fix was implemented or verified.

## Map a small project of your own

1. [Create a free account](https://brainscanner.dev/signup) and open the confirmation link in your email.
2. Follow the [connection instructions](https://brainscanner.dev/connect) in a compatible coding agent. The hosted endpoint is `https://brainscanner.dev/mcp/v2`, using remote Streamable HTTP MCP and OAuth. Supported client capabilities and local permissions matter; website sign-in alone does not connect the agent.
3. Choose a small project you are permitted to inspect. A public sample project is enough. Once the connector is authorized, try this prompt in an agent that can access that project:

> Use the available Brain Scanner workflow to map this project. Submit permitted project metadata only, with no source-file contents, raw diffs, logs or secrets. Pick one file or symbol and show one recorded relationship, what supports it, and one unresolved next step. Tell me what was actually saved. If a required tool or permission is missing, identify it before proceeding.

4. Open the dashboard and inspect the saved relationship. Compare it with the relevant code. Record an unresolved question and the evidence needed to answer it.

A useful first result is one understandable relationship and a clear next question. A graph alone does not prove completeness or correctness. Context must be recorded through supported workflows; Brain Scanner does not automatically capture every coding-agent conversation or local edit.

## Access and help

The hosted connector manages project records within its authorization. Your agent's filesystem, shell and repository access depend on separately granted local permissions. Review the [access terms](https://brainscanner.dev/terms) and [privacy notice](https://brainscanner.dev/privacy) before submitting project information.

If setup stalls, reply in the [public Codex walkthrough discussion](https://github.com/openai/codex/discussions/44291) with your client and the step you reached, or email support@brainscanner.dev. Do not include secrets, OAuth redirect addresses, or private project content in a public reply.

Current documentation note: the connection page still contains an outdated private-beta sentence. The homepage and signup currently offer the free open beta. This walkthrough does not claim compatibility with every MCP client.