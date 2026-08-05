---
name: my-agent
description: What this agent does and when to dispatch it.
# Optional fields:
# systemPrompt: |              # alternative to the markdown body below
#   Full system prompt here.
# tools: read, grep, glob      # tool allowlist; yield is added automatically
# spawns: "*"                  # "*" or CSV of agents this agent may spawn
# model: "@my-role"            # model selector or role alias
# thinkingLevel: medium        # low | medium | high
# output: {}                   # structured-output JSON schema
# blocking: false              # true = parent waits for this agent
# autoloadSkills: []           # skill names from the parent session to inject
# readSummarize: true          # false = subagent read returns verbatim file content
# prewalk: false               # true = hand off to a faster model at first edit
---

# My Agent

The agent's instructions, written in the same style as OMP's bundled agents:
what it does, how it behaves, its method, and its boundaries.
