---
name: fauxproof
description: Protect approved writing, plans, instructions, prompts, or code from silent AI changes. Use for FauxProof projects, sections, drafts, proposals, receipts, backups, imports, locking, unlocking, comparisons, approvals, rejections, checkpoints, or restores; when the user mentions AI drift, unauthorized edits, exact wording, facts that must not change, or a correct prior version; or when they want FauxProof opened. Use FauxProof's private MCP tools for state, exact diffs, explicit approval, restore points, and receipts.
---

# FauxProof

Keep the user's approved version authoritative. Treat generated text as a candidate until the user explicitly approves the exact proposal.

## Non-negotiable safety rules

1. Never approve, unlock, import, replace, or restore merely because it seems helpful. Require the user's explicit instruction for that specific action in the current conversation.
2. Never imply that a change is semantically safe or factually correct. Report the deterministic alerts and exact diff; the user decides whether the meaning is acceptable.
3. Never invent section, proposal, version, receipt, or project identifiers. Read current state when an identifier is not already present in a fresh tool result.
4. Never bypass a conflict. If a tool reports a changed state version or a superseded proposal, fetch the latest state and ask the user to review a new proposal.
5. Never ask for or store payment-card data, protected health information, government identifiers, passwords, API keys, private keys, OAuth secrets, MFA codes, one-time passcodes, or other authentication secrets in FauxProof.
6. Never create a project silently. Ask the user to name or select the project before creating one.

## Open and find saved work

1. Call `get_lockbox_state` whenever the user asks to open FauxProof, show or list saved work, view what is protected, browse or search projects or sections, manage saved information, or see restore points or pending changes.
2. If the host confirms it can render the FauxProof interface and a visual review would help, call `render_lockbox`. Otherwise provide a concise text inventory or search result from the current state.
3. Never say a dashboard opened unless the host actually rendered it.
4. Use `open_lockbox_project` only for the project the user selected or unambiguously named. Use `get_section_content` only for the exact section text needed for the current task.
5. Present ordinary names and status first. Hide raw identifiers, checksums, mutation metadata, audit logs, and machine timestamps unless the user asks or they are needed to resolve ambiguity or continue safely.

Natural requests such as "show my saved work," "list everything I saved," "find my book," "search my saves," and "open FauxProof" should work without requiring internal product or tool names.

## Protect approved work

1. Call `get_lockbox_state` before changing stored state.
2. Confirm the target project and section. If the project does not exist, ask whether to create it and what to call it.
3. For a new item in the selected project, call `add_section` with the complete approved text and `locked: true`.
4. `create_lockbox_project` creates a separate private project and never replaces an existing project. If the user wants a fresh project, confirm its name and create it separately.
5. Report the human-readable item name, protection status, restore-point result, and whether the operation completed. Include raw identifiers only when useful for a follow-up or requested by the user.

When “save this” is ambiguous, route it by intent: use a locked section for final approved wording, use a working draft for work in progress, and ask which the user wants when the intent is unclear.

## Review an AI revision

1. Call `get_lockbox_state` and identify the protected section.
2. Call `analyze_section_drift` with the complete candidate text.
3. Summarize the exact additions, removals, and deterministic risk signals without softening or exaggerating them.
4. If the user asked only to compare or analyze, stop here. If there is no difference, report that and do not create a proposal.
5. Call `protect_revision` only when the user asks to save, propose, or protect the candidate. Pass `source: "claude"` for Claude-generated text and `source: "user"` for user-provided text. Save it as a pending proposal; do not apply it.
6. If the host can render the FauxProof interface, call `render_lockbox` when side-by-side review would materially help. Otherwise give a readable text summary of the diff.
7. Ask the user to approve or reject the identified proposal. Do not choose for them.

## Preserve a working draft

1. Use `save_section_draft` when the user asks to save incomplete wording without replacing the approved version.
2. Pass `source: "claude"` for Claude-generated text and `source: "user"` for user-provided text.
3. Explain that a working draft is separate saved state and is not approved merely because it was saved.
4. Use `protect_saved_draft` only when the user wants that saved draft turned into a pending, checkpointed proposal for review.
5. Use `discard_section_draft` only for the working draft. Confirm that approved wording and restore points remain unchanged.

## Apply a decision

- Refresh with `get_lockbox_state` immediately before approving, rejecting, restoring, locking, unlocking, importing, or otherwise changing current protected state.
- On explicit approval of a named or unambiguous pending proposal, call `approve_proposal`. Report whether it applied or was closed as superseded, and whether a receipt and new restore point were created.
- On explicit rejection, call `reject_proposal`. Confirm that the protected wording stayed unchanged.
- On explicit restoration, call `get_lockbox_state`, identify the restore point, repeat its date before its label, and call `restore_version` with the user's reason. Confirm that a pre-restore checkpoint was created.
- Use `lock_section` only when the user explicitly asks to protect an existing unlocked section. Use `unlock_section` only after the user explicitly confirms the named section to unlock.
- `import_lockbox_backup` replaces the current project's state. Explain that effect and require explicit confirmation of the selected project and backup before importing.
- On an ambiguous decision such as "do it," clarify when more than one proposal or restore point could reasonably be meant.
- Do not expose receipt or state-version identifiers by default. Keep them available when troubleshooting, continuing a multi-step operation, or when the user asks.

## Reliability

- Include a fresh `requestId` whenever the tool schema accepts one, and the latest `expectedStateVersion` whenever the schema accepts one. Never invent unsupported fields.
- If retrying the exact same mutation after an uncertain network result, reuse its original `requestId`.
- When the service reports a duplicate, treat it as success and do not submit another mutation.
- If the service reports a conflict, fetch current state, explain the conflict in ordinary language, and stop before another mutation.
- For high-value work, offer `create_version_snapshot` before a major revision and `export_lockbox_backup` after a milestone.

## Final response

State what remained protected, what changed or did not change, and any decision still needed from the user. Use ordinary language and keep the result concise. Never say the content is "correct" merely because it passed deterministic checks.
