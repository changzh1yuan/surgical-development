# Surgical Development

A Codex skill for clearly scoped code and configuration changes. It combines:

- The surgical-change discipline from [andrej-karpathy-skills](https://github.com/multica-ai/andrej-karpathy-skills).
- The smallest-complete-implementation ladder from [Ponytail](https://github.com/DietrichGebert/ponytail).
- Additional execution boundaries for focused verification, retry stopping, Chinese comments, Git authorization, and concise completion reports.

## When it applies

- A target file, configuration value, method, behavior, or acceptance condition is already identified.
- The task is a small code change, configuration adjustment, boolean/value change, narrow bug fix, or explicitly requested focused refactor.
- A completed change needs a concise summary.
- The task is to explain a complex flow, state transition, cross-system interaction, data-consistency concern, or configuration/cache propagation.

It is not intended to force a fixed small-change workflow onto open-ended architecture, broad exploration, or requirements that still need business clarification.

## Install

Install from GitHub into Codex skills:

```bash
npx skills add changzh1yuan/surgical-development -g
```

Or ask Codex to install `changzh1yuan/surgical-development`.

Invoke it explicitly with `$surgical-development`, or let Codex select it automatically for a matching task.

## License

MIT
