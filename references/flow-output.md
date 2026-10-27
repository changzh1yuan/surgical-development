# Flow output

Use this reference when the main task is to explain a complex flow or configuration effect, or when a substantial code change needs a process diagram.

## Main flow

- Give a concise text flow using `来源 → 处理 → 状态 → 结果`.
- Name the initiator, processor, key state transition, and final result.
- Mark the responsibility of each database, cache, message queue, timer/job, third-party system, and deployment target that actually participates.
- Merge repeated content between the main flow and change-propagation flow instead of drawing both in full.

## Change propagation

Add a separate change-propagation flow only when configuration, state, or data changes spread across components. State:

- Who or what triggers the change.
- The propagation path.
- When the change takes effect.
- How to roll it back or recover, when that is meaningful.

## Exceptions and concurrency

Explain only relevant failure and concurrent behavior:

- Exception: trigger condition, handling method, and termination condition.
- Concurrency: which data source wins, how duplicate execution is prevented, and how consistency is maintained.

## Organization

For a complex requirement, organize the explanation as:

```text
关键假设
→ 主流程图
→ 变更流转图（如有）
→ 异常与并发处理（如有）
→ 结论
```

When information is incomplete, state the key assumptions first. If a business decision remains ambiguous, ask for confirmation before changing code.
