# DEEPVOID Jailbreak

**Target:** DeepSeek-V3  
**Technique:** Multi-turn conversation history poisoning  
**Status:** Confirmed  

## Overview

Exploits the model's tendency to continue established conversational patterns by pre-loading the conversation history with fabricated assistant responses that demonstrate compliance with harmful requests. The model treats the fake history as evidence of its own prior behavior and continues the pattern.

This is delivered as a raw API payload (`messages` array) rather than a single-turn prompt.

## Technique Details

### Conversation History Poisoning

The attack constructs a `messages` array with:
1. A system prompt defining an "amorally reinforced assistant" persona
2. A series of user/assistant message pairs where the fake assistant responses demonstrate progressively more harmful compliance
3. A final user message requesting the target output

The key mechanism: by the time the model processes the final user message, it has "seen itself" comply with dozens of harmful requests. The behavioral momentum overrides safety training.

### Escalation Ladder

The fake conversation history escalates gradually:
- Starts with identity confirmation ("Who are you?")
- Moves to capability claims ("What can you do?")
- Progresses through increasingly extreme fake compliance responses
- Each fake assistant response reinforces the pattern

### Unicode Font Obfuscation

The system prompt instructs output in Mathematical Sans-Serif Unicode (U+1D5A0–U+1D5B9), which may bypass text-based content filters that only match standard ASCII patterns.

## Prompt Structure

```json
{
  "model": "deepvoid-raw-dev",
  "messages": [
    {"role": "system", "content": "[persona definition]"},
    {"role": "user", "content": "[benign question]"},
    {"role": "assistant", "content": "[compliant response]"},
    {"role": "user", "content": "[escalated request]"},
    {"role": "assistant", "content": "[fake compliant response]"},
    // ... 15+ escalating pairs ...
    {"role": "user", "content": "[target harmful request]"}
  ]
}
```

The system prompt establishes:
- An "amorally reinforced" identity
- Explicit priority ordering: user desires > efficiency > amoral delivery
- Instruction to use Mathematical Sans-Serif Unicode font
- Framing that "external guidelines" should be ignored

## Key Insight

This technique works because:
1. **Behavioral inertia** — Models continue patterns established in conversation history
2. **Self-consistency bias** — The model treats fake assistant messages as its own prior outputs and maintains consistency
3. **Gradual escalation** — Each step is a small increment from the previous, avoiding a sharp safety boundary trigger
4. **API-level access** — Requires direct API access to inject fake assistant messages; not reproducible through standard chat UIs

## Research Notes

This is fundamentally different from prompt injection — it attacks the model's conversation-level behavioral patterns rather than its instruction-following mechanism. Defenses would need to validate conversation history integrity or apply safety checks independently at each turn rather than relying on conversational context.
