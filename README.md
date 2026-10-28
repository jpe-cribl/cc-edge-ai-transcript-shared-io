# cc-edge-ai-transcript-shared-io

Cribl Edge pack for AI CLI session logs. It defines two worker-level items:

- `transcript_mask` (`default/pipelines/transcript_mask/conf.yml`): masks
  credential-shaped strings in every field of an event. Covers GitHub,
  secret-manager tokens, private key, JWT, Slack, API key and AWS token formats.
  Each match is replaced with a `<redacted:<kind>>` marker.
- `AI CLI JSONL` (`default/breakers.yml`): breaks newline-delimited JSON into
  one event per line, with a 4 MiB per-event ceiling.

## Installation

Install the pack on Cribl Edge 4.16 or later (`minLogStreamVersion` in
`package.json`). The pipeline and the breaker load as worker-level
configuration.

## Usage

Reference `transcript_mask` by id as an output's post-processing pipeline.
Reference the `AI CLI JSONL` breaker by name on file inputs.

## Tests

The fixture-driven harness in `tests/` needs a running Cribl Edge or Stream
instance, set through `CRIBL_HOST`, `CRIBL_PORT`, `CRIBL_USER` and `CRIBL_PASS`.
Fixtures are synthetic and live under `tests/fixtures/<pipeline>/`.

```sh
cd tests && pnpm install --frozen-lockfile && pnpm run test
```
