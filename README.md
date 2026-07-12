# board-spec

Source of truth for Qualcomm Yocto BSP board specs, consumed by the
`qcom-yocto-new-machine` and `qcom-partition-conf-new-board` skills via the
`board-spec-mcp` MCP server, replacing the previous Confluence-page workflow.

## Layout

- `schema/machine-spec.schema.json` — JSON Schema for the machine identity + `machine_creation` half of a board spec.
- `schema/partition-spec.schema.json` — JSON Schema for the `partition_conf` half of a board spec.
- Each board lives on its own branch, named after the machine, split across two files:
  `boards/<machine>/machine.yaml` and `boards/<machine>/partition.yaml`.

## Adding a new board

1. Branch off `main`: `git checkout -b <machine>`.
2. Add `boards/<machine>/machine.yaml` following `schema/machine-spec.schema.json`.
3. Add `boards/<machine>/partition.yaml` following `schema/partition-spec.schema.json`.
4. Open a PR against `<machine>` (not `main`) for review.
5. Once merged, the `board-spec-mcp` server picks it up via `refresh_specs`.

Specs are human-authored and reviewed via PR — the MCP server and skills only
read; they never write back to this repo.
