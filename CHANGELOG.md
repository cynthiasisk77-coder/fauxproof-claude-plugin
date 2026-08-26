# Changelog

## 1.5.2 — 2026-08-26

- Made Claude call `open_picture_upload` immediately instead of leading with the chat-attachment limitation.
- Documented the clickable **Add a picture to FauxProof** action and same-picture device selection.
- Kept saved-picture retrieval on `list_project_files` followed by `open_project_file`.

## 1.5.1 — 2026-08-24

- Taught Claude to open FauxProof's real device picker for pictures attached in chat, with no public URL request.
- Added explicit saved-picture retrieval through `list_project_files` and `open_project_file`.
- Clarified that retrieval returns the exact stored image and exact-file download rather than a text description.
- Added picture, screenshot, graph, upload, and retrieval phrases to the FauxProof skill trigger.

## 1.5.0 — 2026-08-24

- Added secure PNG, JPEG, GIF, and WebP attachment from the FauxProof review board in Claude.
- Added a host-independent browser upload path using a short-lived, single-use credential.
- Kept upload credentials out of URLs and Claude tool arguments.
- Added server-side file-size, checksum, file-signature, project, and account validation before encrypted storage.
- Preserved the existing text workflow and clarified that picture attachment is not visual-difference analysis.

## 1.4.4 — 2026-08-22

- Added the first Claude Code plugin wrapper for the FauxProof 1.4.4 service.
- Added remote MCP configuration with OAuth scope `lockbox:access`.
- Added a reusable public OAuth client and fixed loopback callback for Claude Code, avoiding a new Auth0 application registration for every fresh installation.
- Added a dedicated strict-OAuth Claude route that reuses the existing FauxProof application core, Auth0 tenant, and private storage.
- Added host-neutral workflow instructions with a text fallback when a visual review surface is unavailable.
- Added explicit setup, consent, conflict, secret-handling, and restore safeguards.
- Limited capability wording to currently supported text-based material: writing, plans, prompts, instructions, and code.
- Licensed this public Claude Code plugin wrapper under Apache License 2.0; the private FauxProof backend and hosted service are not included.
