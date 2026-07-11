---
type: workflow
id: word-count-gated-writer
title: Word-Count Gated Writer
description: "Deterministically checks a draft against a word-count range, then revises it to fit."
tags: [Production, Content, Writing]
connections:
  - target: revise-to-length
    type: uses
  - target: llm-service
    type: runs_on
metadata:
  estimated_duration: "1-2 minutes"
  trigger: manual
output_step: "revise-to-length"
execution:
  - id: "word-count-gate"
    step_type: "local.builtin"
    input: "{{input.draft}}"
    context:
      operation: "word-count-gate"
      min: "150"
      max: "250"
    output: { name: "word_count_verdict", type: "json" }
  - skill: "revise-to-length"
    step_type: "generation"
    prompt: "revise-draft"
    output: { name: "revised_draft", type: "text" }
---

## Overview

Language models are unreliable at counting their own words — ask for "exactly 200 words" and you get anywhere from 150 to 400. This skrpt fixes that with a deterministic, zero-token **word-count gate**: a builtin that counts the draft exactly and returns a pass/fail verdict against a target range, which then steers a single revision pass.

## Pipeline Stages

### Stage 1: Word-Count Gate (builtin)

The **word-count-gate** builtin counts the draft (`{{input.draft}}`) and returns `{count, pass, reason}` for the 150–250 word range — exact, deterministic, no model call.

**Output:** the count verdict.

### Stage 2: Revise to Length

The **revise-to-length** step edits the draft toward the target range, guided by the verdict — trimming if over, expanding if under, or lightly polishing if it already passes.

**Output:** the revised draft.

## Inputs

| Name | Required | Description | Example |
|------|----------|-------------|---------|
| `{{input.draft}}` | Yes | The draft text to check and revise | `A 180-word blog intro…` |

## Example Input

```
Draft: "Paste your draft here. The gate counts it exactly and the revision brings it into the 150–250 word target."
```
