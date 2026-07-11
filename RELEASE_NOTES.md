# Release Notes

## v1.0.1
GH#820 — migrate the builtin step to the node-less `local.builtin` shape (#802 D1b). Replace the `count-words` backing skill-node + `uses` edge with a node-less execution entry (`id: word-count-gate`, `input`, `context.operation`, `output`); downstream reference `{{steps.Count Words.output}}` → `{{steps.word-count-gate.output}}`. Deterministic behavior unchanged; back-compat holds until #802 B6. contents skills 2→1.

## v1.0.0
Initial release. Showcases the deterministic `word-count-gate` builtin: counts a draft exactly (zero-token, offline) and returns a `{count, pass, reason}` verdict against a 150–250 word range, then a single LLM pass revises the draft to fit. Demonstrates that language models cannot reliably count their own words — the gate can.
