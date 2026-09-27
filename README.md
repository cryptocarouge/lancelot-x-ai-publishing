# Lancelot X AI Publishing

An autonomous research, editorial and publishing pipeline built with n8n.

The private production system combines scheduled editions, live data, LLM-based editorial work, image generation, publication controls and Telegram operations. This repository documents the architecture without exposing production keys, private prompts or account identifiers.

## What it demonstrates

- Scheduled editorial editions
- Market and macro data collection
- RSS/news ingestion
- Fact-building before generation
- Separate editorial and AI-research paths
- LLM-assisted copy generation
- AI image generation
- X media upload and publishing
- Anti-spam and duplicate protection
- Post-publication verification
- Memory written only after confirmed publication
- Manual Telegram commands
- Success/error notifications and voice feedback

## Architecture

```text
Schedules / Manual Command
          |
          v
 Data + News Collection
          |
          v
   Fact Construction
          |
          +--> Editorial Prompt
          |
          +--> AI Research Prompt
          |
          v
      LLM Generation
          |
          v
 Validation / Anti-Spam
          |
          +--> Image Generation
          |
          v
       Publish to X
          |
          v
 Publication Verification
          |
          +--> Persist Memory
          |
          +--> Telegram Feedback
```

## Design choices

The workflow deliberately keeps deterministic tasks outside the model where possible. Data gathering, routing, anti-spam checks, publication verification and state updates are handled as workflow logic.

AI is used where it materially helps: research synthesis, editorial writing and image generation.

## Security boundary

The private production workflow currently contains account-specific integrations and credentials. They are not published here.

This public repository excludes:

- OpenAI keys
- X OAuth credentials
- Telegram credentials and chat IDs
- Private prompts
- Account-specific publishing settings
- Private memory/state
- Production workflow JSON

## Status

Public architecture showcase. Production system remains private.
