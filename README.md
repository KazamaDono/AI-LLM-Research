# AI Security Research

Documented vulnerabilities, jailbreaks, and prompt injection techniques discovered across commercial LLM systems.

This repository contains original as well as adopted research into the safety and alignment boundaries of large language models. Each finding demonstrates a specific bypass technique that was reproducible at the time of discovery.

## Jailbreaks

| Prompt | Target | Technique | Status |
|---|---|---|---|
| [POTATO v1](jailbreaks/potato-v1.md) | DeepSeek-V3 | Persona injection via world-building | Confirmed |
| [POTATO v2](jailbreaks/potato-v2-deepseek.md) | DeepSeek-V3 | Structured persona manifest with cognitive framework | Confirmed |
| [POTATO v2](jailbreaks/potato-v2-gemini.md) | Google Gemini | Structured persona manifest with cognitive framework | Confirmed |
| [POTATO x CHARLIE](jailbreaks/potato-x-charlie.md) | Google Gemini | Steganographic prompt injection via Unicode tag characters | Confirmed |
| [AMBER](jailbreaks/amber.md) | Google Gemini | Narrative-wrapped steganographic injection via hidden Unicode | Confirmed |
| [DEEPVOID](jailbreaks/deepvoid.md) | DeepSeek-V3 | Multi-turn conversation history poisoning | Confirmed |
| [APPLES](jailbreaks/apples.md) | DeepSeek-V3 | Persona injection variant (POTATO derivative) | Confirmed |

## Technique Categories

### Persona Injection
Constructs an alternate identity with a complete world, rules, and behavioral framework that overrides the model's safety training. The POTATO family uses increasingly elaborate world-building to anchor the persona.

### Steganographic Prompt Injection
Hides executable instructions inside Unicode tag characters (U+E0000 range) or acrostic patterns within seemingly innocent narrative text. The model processes the hidden layer while a human reader sees only the cover story.

### Multi-Turn Poisoning
Pre-loads the conversation history with fake assistant responses that establish a pattern of compliance. The model continues the established behavioral pattern rather than applying safety filters.

## Responsible Disclosure

Findings have been reported to the respective vendors through their vulnerability disclosure programs where applicable.

## Disclaimer

This research is published for educational and defensive purposes. Understanding how LLM safety mechanisms fail is essential for building more robust AI systems. Do not use these techniques to cause harm.
