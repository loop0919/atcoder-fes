---
name: requirements-manager
description: Manage requirements definition documents and requirement change control. Use when Codex is asked to create, update, organize, refine, split, prioritize, or audit requirements docs, use cases, acceptance criteria, scope statements, non-functional requirements, requirement IDs, traceability notes, or open questions in Japanese or English projects.
---

# Requirements Manager

## Overview

要件定義書をプロダクト判断の基準として保守する。実装方針を書きすぎず、利用者価値、スコープ、制約、受け入れ条件、未決事項を追跡できる状態にする。

## Quick Start

1. Locate the requirements source. Prefer a user-specified file; otherwise search for names such as `requirements.md`, `*-requirements.md`, `要件定義.md`, `docs/requirements/*`, and this repository's `atcoder-fes-bot-requirements.md`.
2. Identify the change intent: new feature, scope clarification, priority change, constraint, acceptance criterion, risk, or removal.
3. Preserve stable requirement IDs when they exist. Add IDs for new testable requirements using the surrounding document's style.
4. Update the smallest necessary sections and keep related tables consistent: users, scope, use cases, functional requirements, non-functional requirements, data, operations, constraints, and open questions.
5. Report the changed requirement IDs, affected sections, assumptions, and unresolved decisions.

## Management Rules

- Treat requirements as contracts, not design notes. Include implementation details only when they are externally visible, security relevant, or a true constraint.
- Write requirements so they can be reviewed or tested. Prefer observable behavior, actors, trigger conditions, expected outcomes, and error cases.
- Maintain traceability from use cases to functional requirements. If a use case implies missing requirements, add or flag them.
- Keep priorities meaningful. Use the document's existing scale; if none exists, use Must, Should, Could, Won't.
- Separate confirmed requirements from assumptions and open questions. Do not silently turn ambiguous decisions into requirements.
- Keep scope boundaries explicit. When adding a requirement, check whether it conflicts with the out-of-scope list.
- Preserve Japanese terminology used by the document. Introduce new terms only when they reduce ambiguity.

## Change Workflow

### 1. Inspect

- Read the relevant requirement sections before editing.
- Check whether the requested change is already covered by an existing requirement.
- Identify impacted actors, workflows, commands, data, permissions, logs, integrations, and non-functional qualities.

### 2. Edit

- Add or update requirement rows with stable IDs, clear names, concise requirement text, and priority.
- Add acceptance criteria when behavior needs more detail than a table row can hold.
- Add negative and error cases when they affect user-visible behavior, security, or operations.
- Update dependent sections together. For example, a new administrator command may affect use cases, functional requirements, permissions, audit logs, and non-functional requirements.

### 3. Validate

- Check ID uniqueness and priority consistency.
- Check that each Must requirement has enough detail for implementation review.
- Check that out-of-scope items still remain out of scope.
- Check that the document does not mix requirement, design, and task tracking in the same row.

## Requirement Quality Checklist

- Actor is clear.
- Trigger or condition is clear.
- Required behavior is observable.
- Success outcome is clear.
- Failure or permission behavior is covered when relevant.
- Priority is assigned.
- The requirement can be mapped to implementation or tests.
- The wording avoids vague terms such as "properly", "fast", or "easy" unless the document defines measurable criteria.

## Output Shape

When editing requirements, end with:

- `Updated`: files and sections changed.
- `Requirement IDs`: added, changed, removed, or marked open.
- `Assumptions`: decisions made because the request was underspecified.
- `Open questions`: items that should not be finalized without stakeholder input.
