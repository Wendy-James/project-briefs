# AI B2B Outreach Workbench

## Summary

A private local Python workbench for turning a complex business workflow into auditable modules: campaign setup, lead research, draft generation, safety checks, dry-run sending, reply triage and anonymized supplier RFQ routing.

## Problem

Automation around outreach and supplier communication can easily become unsafe if it skips consent, privacy, review or error handling. The engineering goal is to support workflow efficiency while keeping human review and safety gates central.

## Modules

- Campaign setup: product, target country, ICP and keyword breakdown.
- Candidate processing: import, deduplication, review status and scoring.
- Draft generation: personalized draft messages with compliance checks.
- Send safety: dry-run first, `READY_TO_SEND` gate, blacklist / unsubscribe blocking and domain frequency limits.
- Reply workflow: reply classification, suggested response drafting and follow-up planning.
- Supplier RFQ: anonymized supplier inquiry queue with privacy leak detection.
- Form assistant: fill contact forms, but do not submit or bypass captcha.

## Engineering Signal

- Backend workflow decomposition with clear module boundaries.
- Local web console and CSV/file-based data flow for inspectable state.
- Human-in-the-loop automation: default dry-run, explicit confirmation for risky actions.
- Local automated safety tests for send gates, secret scanning, RFQ anonymization, form non-submission and web runtime checks.

## Evidence Status

The full project is private/local because it may contain business workflow details and data paths. Public presentation should use mock data, screenshots without sensitive content, and summarized architecture notes.

## Do Not Overclaim

- Do not claim production deployment, high concurrency, real customer metrics or fully autonomous sending.
- Do not publish credentials, customer records, private email data, supplier contact lists or local secrets.
