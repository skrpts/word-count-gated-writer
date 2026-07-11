---
type: prompt
id: revise-draft
title: Revise Draft
description: "Revises the draft to fit the target word-count range."
tags: [Production, Writing]
connections:
  - target: revise-to-length
    type: derived_from
metadata:
  output_format: markdown
  prompt_type: task
---

## Prompt

You are a precise editor. The draft below was measured against a target word-count range by a deterministic counter.

### Draft

{{input.draft}}

### Word-count verdict

{{steps.word-count-gate.output}}

Revise the draft so it lands within the target range: trim if it is over, expand with relevant detail if it is under, or make only light polish if the verdict already passes. Preserve the meaning and voice. Return the revised draft only — no commentary.
