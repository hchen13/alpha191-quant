# Alpha191 Quant

Alpha191 Quant is a planning and prototype repository for an A-share daily multi-factor stock selection system.

The V1 strategy is intentionally narrow:

- Long-only A-share stock selection
- Daily signal generation
- Manual trading execution
- Top 5 target holdings
- Top 15 rebalance buffer
- Local data cache with incremental updates
- No automated broker order placement
- No intraday high-frequency trading
- No CTA overlay in V1

## Documents

- `docs/alpha191-quant-system-spec.html` is the main implementation specification.
- `docs/alpha191-workbench-prototype.html` is the interactive workbench prototype.
- `AGENTS.md` defines long-lived agent operating rules for this project.

## Confirmed Data Interface Capabilities

The system specification assumes the following data interface capabilities are already confirmed:

- Query one symbol for a specified time range.
- Fetch one symbol's full previous trading day 1-minute bars from 09:30 to 15:00.
- Fetch one symbol's 500-day or 1000-day daily K-line history in a single request.
- Fetch large historical datasets through `offset` and `limit` pagination.
- Query thousands of symbols for the same trading day in one batch request.

## V1 Strategy Shape

The strategy workflow is:

1. Update local data incrementally.
2. Build the tradable stock universe.
3. Compute active factors.
4. Winsorize, center, standardize, and align factor directions.
5. Combine active factors with equal weights.
6. Select Top 5 target holdings.
7. Keep existing holdings while they remain inside the Top 15 buffer.
8. Generate a manual trade plan for 09:30 and later execution.

## UI Prototype

Open the prototype directly in a browser:

```text
docs/alpha191-workbench-prototype.html
```

The prototype covers:

- Strategy overview
- AI-assisted factor discovery
- Factor pool evaluation
- Strategy configuration
- Backtesting metrics
- Daily stock selection
- Per-stock detail view

## Security

Secrets must never be committed.

The repository ignores `.env`, temporary files, local data caches, generated artifacts, and logs.
