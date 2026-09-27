# Case Study — Lancelot X AI Publishing

## Problem

Automated publishing can easily become low-quality spam if an LLM is asked to research, write and publish in one step. The core challenge was to separate factual inputs, editorial generation, publication controls and memory.

## Architecture decision

The workflow uses a staged pipeline:

1. **Scheduled or manual intent** selects the edition.
2. **Market, macro and news sources** are collected deterministically.
3. **Fact construction** converts raw source responses into a bounded factual context.
4. **Editorial generation** receives that context instead of browsing blindly.
5. **Validation and anti-spam logic** run before publishing.
6. **Image generation** is a separate optional stage.
7. **Publishing** happens through the X integration.
8. **Verification** confirms that the publication actually succeeded.
9. **Memory** is written only after confirmed publication.
10. **Telegram operations** expose manual controls and success/error feedback.

## Why fact construction matters

The model is not used as the source of truth. The workflow first builds a factual input from external sources, then asks the model to interpret and write from those facts.

This reduces hallucination risk and makes the editorial step easier to inspect.

## Memory after confirmation

A subtle but important rule is that a draft is not remembered as published content. Memory is persisted only after the publication path confirms success.

That prevents failed posts from contaminating duplicate detection and future editorial context.

## Manual and autonomous paths

Scheduled publishing and manual Telegram commands share the same downstream controls. Manual operation therefore does not bypass validation, publication verification or state handling.

## What remains private

The public repository excludes API keys, X OAuth credentials, Telegram identifiers, production prompts, account-specific style rules, internal memory and the production workflow.

## Takeaway

The project demonstrates a reusable pattern for AI publishing: **facts first, generation second, deterministic controls around the model, and confirmation before state mutation**.
