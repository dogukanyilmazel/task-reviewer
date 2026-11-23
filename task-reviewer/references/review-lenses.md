# Review lenses

Choose by affected behavior and verify against the project's runtime, APIs, and documented rules. Framework examples are entry points for investigation.

## Web, mobile, and desktop

- Test whether loading, empty, partial, stale, and error states communicate the correct result. Check that an earlier response cannot overwrite a newer selection and that repeated submissions have the intended effect.
- For lifecycle-sensitive behavior, trace subscriptions, timers, and pending work through mount and unmount, navigation or window reopening, and reconnect. On mobile, consider background and foreground transitions, unreliable connectivity, and support for old app versions. In browsers, include reloads and multiple tabs when shared state is involved.
- When interaction changes, inspect relevant keyboard, focus, accessibility, and viewport behavior. Check work on the UI thread, repeated requests or rendering, and cleanup if users can realistically notice a slowdown or resource increase.

## APIs, identity, and data boundaries

- Follow input validation, identity, authorization, and resource scoping to the operation that reads or writes data. Derive the actual boundary from the product, such as a workspace, organization, branch, user, or delegated role. Include related records, lists, exports, and async work if they use that boundary.
- Verify errors, missing or deleted records, and contract compatibility with existing clients. Check defaults, field and shape changes, mixed versions during deployment, and the order of any schema, backend, and client updates.

## Persistent data, time, and derived state

- Trace create, edit, delete, import, and retry paths that feed summaries, caches, alerts, and user-visible state. Check whether all affected consumers reflect the same source of truth. Consider rollback after partial failure and enforce invariants at the persistence layer where races otherwise permit duplicates or invalid state.
- For “current,” “latest,” or “today,” distinguish event time, record creation time, and processing time. Verify the authoritative timezone, freshness window, day boundaries, and active versus completed state. For example, importing an older event today should only change a current-state indicator if the product's time rules say it should.
- Inspect migrations against existing records and realistic rollout order. For changed hot queries, check scoping, bounds, sort, available indexes, pagination, and repeated reads or writes. For SQL or document stores, use a representative plan if feasible. Base index or scale findings on actual query shape, volume, and workload.

## Jobs, events, and realtime

- Trace enqueue through execution, retry, cancellation, and cleanup. Consider delayed or duplicate delivery, restarts, multiple workers, stale or deleted inputs, and overlapping runs. Verify idempotency or deduplication where repeated work changes outcomes.
- Check clock and timezone assumptions for schedules, bounds for batches and retries, and whether fan-out scales. For realtime clients, check reconnect and resubscription behavior and whether missed, duplicate, or out-of-order events leave inconsistent state.

## Libraries, build, and infrastructure

- Trace public API changes through existing consumers, supported versions, packaging, and platform configuration. Check defaults, failure paths, and how partial updates or mixed deployments behave.
- When reviewing config or infrastructure changes, use the available local validation or dry-run output. Inspect initialization, dependency ordering, rollback or recovery, and compatibility of existing state.
