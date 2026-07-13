# board-spec

Source of truth for Qualcomm Yocto BSP board specs, consumed by the
`qcom-yocto-new-machine` and `qcom-partition-conf-new-board` skills via the
`board-spec-mcp` MCP server, replacing the previous Confluence-page workflow.

## Layout

- `schema/machine-spec.schema.json` — JSON Schema a board's `machine.yaml`
  validates against (this branch).
- `schema/partition-spec.schema.json` — JSON Schema a board's
  `partition.yaml` validates against (this branch).
- Each board lives on its own branch, named after the machine, at
  `boards/<machine>/machine.yaml` and `boards/<machine>/partition.yaml`.

## Adding a new board

1. Branch off `main`: `git checkout -b <machine>`.
2. Add `boards/<machine>/machine.yaml` following
   `schema/machine-spec.schema.json`, and `boards/<machine>/partition.yaml`
   following `schema/partition-spec.schema.json`.
3. Open a PR against `<machine>` (not `main`) for review.
4. Once merged, the `board-spec-mcp` server picks it up via `refresh_specs`.

Specs are human-authored and reviewed via PR — the MCP server and skills only
read; they never write back to this repo.
