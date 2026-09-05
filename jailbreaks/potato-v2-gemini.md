# POTATO v2 Jailbreak (Gemini)

**Target:** Google Gemini  
**Technique:** Structured persona manifest with cognitive framework  
**Status:** Confirmed  

## Overview

Same POTATO v2 manifest as the DeepSeek variant, confirmed working against Google Gemini. The structured protocol format with YAML config blocks, ASCII flowcharts, and the 10-section manifest bypasses Gemini's safety alignment through the same mechanisms — treating the prompt as system-level configuration rather than user input.

## Prompt

Same as [POTATO v2 (DeepSeek)](potato-v2-deepseek.md). Identical prompt, different target.

## Activation

Send: `hello potato`

## Notes

Gemini's safety training responds differently to the manifest format compared to DeepSeek. The structured sections (particularly the YAML-style identity block and the "Forbidden Sentence" section) appear to be processed as configuration directives by Gemini's instruction-following layer.
