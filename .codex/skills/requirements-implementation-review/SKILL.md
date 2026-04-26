---
name: requirements-implementation-review
description: Review whether implementation, tests, and behavior conform to a requirements definition document. Use when Codex is asked to compare code against requirements, find missing or conflicting implementation, build a requirement-to-code traceability review, check acceptance criteria, or audit feature completeness from a requirements document in Japanese or English.
---

# Requirements Implementation Review

## Overview

要件定義書を基準に、実装・テスト・設定・運用面が要求を満たしているかをレビューする。通常のコード品質レビューではなく、要件 ID と実装証跡の対応、未実装、過剰実装、矛盾、テスト不足を優先して扱う。

## Quick Start

1. Locate the requirements source. Prefer a user-specified file; otherwise search for `requirements.md`, `*-requirements.md`, `要件定義.md`, `docs/requirements/*`, and this repository's `atcoder-fes-bot-requirements.md`.
2. Extract reviewable requirements into a working checklist. Keep IDs, priority, actor, expected behavior, acceptance criteria, and relevant non-functional constraints.
3. Inspect implementation, tests, configuration, schemas, commands, API routes, UI, jobs, and logs for evidence.
4. Map each reviewed requirement to one of: `Satisfied`, `Partially satisfied`, `Not satisfied`, `Contradicted`, `Not assessable`, or `Out of reviewed scope`.
5. Report findings first, ordered by severity, with requirement IDs and file references.

## Review Rules

- Treat the requirements document as the source of truth. Do not fail implementation for behavior the document does not require unless it conflicts with scope, security, data integrity, or user expectations stated in the document.
- Prefer concrete evidence over inference. Cite files, line numbers, tests, command output, schemas, or absent code paths.
- Distinguish clearly between requirement gaps, implementation bugs, missing tests, unclear requirements, and out-of-scope enhancements.
- Check Must requirements first, then Should, then Could. Mention Won't items only when implementation appears to contradict them.
- Include non-functional requirements such as security, permissions, audit logs, secrets, reliability, and operational observability.
- Do not edit code during a review unless the user explicitly asks to fix findings.

## Evidence Mapping

For each important requirement, collect:

- Requirement ID and priority.
- Expected behavior from the document.
- Implementation evidence, with file references.
- Test evidence, with file references or executed test commands.
- Status and confidence.
- Review note explaining any gap or ambiguity.

Use a compact matrix when many requirements are involved:

| Requirement | Priority | Status | Evidence | Gap |
|---|---|---|---|---|
| F-001 | Must | Satisfied | `path/file.ext:line` | None |

## Finding Criteria

Raise a finding when:

- A Must or Should requirement has no implementation path.
- The implementation handles only the happy path while the requirement implies permission, validation, error, retry, logging, or state-transition behavior.
- The implementation contradicts scope, priority, actor permissions, data constraints, or security requirements.
- The implementation exists but has no meaningful tests for a high-risk requirement.
- The requirements are too ambiguous to assess and that ambiguity blocks implementation confidence.

## Severity Guide

- `Critical`: contradiction or missing behavior that can expose secrets, corrupt data, bypass permissions, or make a Must workflow unusable.
- `High`: missing or partial implementation of a Must requirement, or no test coverage for a risky Must workflow.
- `Medium`: partial Should requirement, important edge case, traceability gap, or unclear requirement that could cause rework.
- `Low`: documentation mismatch, minor acceptance-criteria gap, or Could-level incompleteness.

## Output Shape

Use this structure unless the user asks for another format:

1. `Verdict`: `Conforms`, `Partially conforms`, `Does not conform`, or `Insufficient evidence`.
2. `Findings`: lead with issues, ordered by severity. Include requirement ID, priority, evidence, and concrete impact.
3. `Traceability summary`: compact matrix for reviewed requirements.
4. `Test gaps`: missing or weak tests tied to requirement IDs.
5. `Open questions`: requirement ambiguities that block confident assessment.
