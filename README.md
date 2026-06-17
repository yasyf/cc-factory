# cc-factory

![cc-factory banner](docs/assets/readme-banner.webp)

[![CI](https://img.shields.io/github/actions/workflow/status/yasyf/cc-factory/ci.yml?branch=main&label=CI)](https://github.com/yasyf/cc-factory/actions/workflows/ci.yml)
[![License: PolyForm-Noncommercial-1.0.0](https://img.shields.io/badge/License-PolyForm-Noncommercial-1.0.0-blue.svg)](https://github.com/yasyf/cc-factory/blob/main/LICENSE)

A software factory for Claude Code: orchestrated agents that plan, build, review, and ship software.

cc-factory runs a spec down an assembly line of Claude Code agents: one plans the
work, a pool of workers builds it in parallel, and separate agents review the diff
and push back before anything ships. The payoff is the hand-offs — plan, build,
critique, and ship move on their own, so you describe what you want instead of
steering one session through every step.

## Install

cc-factory is a Claude Code plugin. Add the marketplace, then install it:

```
/plugin marketplace add yasyf/cc-factory
/plugin install cc-factory@cc-factory
```

## Quickstart

Hand the factory a one-line spec and let the pipeline run:

```
/cc-factory:build "Add per-key rate limiting to the public API, 100 req/min"
```

The factory plans the change, dispatches a pool of `claude-pool` workers to
implement it, opens a `cc-review` on the resulting diff, and surfaces any
`cc-pushback` objections for you to resolve before it merges.

## What problems does this solve?

- **One session, one thread of attention.** A single Claude session does one thing
  at a time and loses context across compactions. cc-factory fans the build across
  `claude-pool` workers and keeps decisions in `cc-notes`, so parallel work and long
  memory stop being your job.
- **Nobody checks the work.** Code an agent writes ships as fast as it's written,
  bugs and all. cc-factory routes every diff through `cc-review` and an adversarial
  `cc-pushback` pass before it lands.
- **Orchestration gets hand-rolled every time.** Stitching plan, build, review, and
  ship into one pipeline means wiring prompts and shell by hand for each project.
  `cc-orchestrate` holds the pipeline; cc-factory ships the wiring.
- **Guardrails are an afterthought.** Agents touch files they shouldn't and skip the
  lint. `captain-hook` enforces the guards declaratively, on every step.

## License

PolyForm-Noncommercial-1.0.0. See [LICENSE](https://github.com/yasyf/cc-factory/blob/main/LICENSE).
