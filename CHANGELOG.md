# Changelog

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
