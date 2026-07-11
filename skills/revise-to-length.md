---
type: skill
id: revise-to-length
title: Revise To Length
description: "Revises a draft toward a target word-count range, guided by the gate verdict."
tags: [Production, Writing]
connections:
  - target: llm-service
    type: runs_on
---

## Capability

Takes a draft and a word-count verdict and revises the draft to fall within the target range — trimming, expanding, or lightly polishing as the verdict indicates.
