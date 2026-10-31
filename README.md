# getting-started

Connect an agent to Audienti: report its tools, introduce it and propose a first campaign test.

Agent skill for Audienti (https://exo.audienti.com). It is also served by Audienti itself:
`audienti skills show getting-started`. The authored copy lives in the Audienti application
repository and is exported here with `scripts/export-skill-plugin.mjs`; edit it there.

Installing the skill does not grant any permission in Audienti or authorize outreach.

Claude Code installation:

```sh
claude plugin install getting-started --marketplace audienti/plugins
```

Codex installation (after adding the Audienti marketplace):

```sh
codex plugin add getting-started@audienti
```
