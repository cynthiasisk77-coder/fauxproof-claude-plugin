# FauxProof for Claude Code

FauxProof protects approved writing, plans, prompts, instructions, code, and supporting images from silent AI changes. Claude can compare a proposed text revision with the protected version, save it for review, and apply it only after you explicitly approve it.

FauxProof provides exact text differences, pending proposals, restore points, backups, receipts, and project picture attachments. Its checks are deterministic; they do not guarantee that wording is factually or semantically correct.

FauxProof acts only on content you explicitly provide or select for a FauxProof operation. It does not extract Claude's memory, unrelated conversation history, or unrelated uploaded content.

## What this plugin adds

- Private FauxProof projects and protected sections
- Exact change analysis before a revision is applied
- Explicit approve-or-reject decisions
- Working drafts that do not replace approved wording
- Secure PNG, JPEG, GIF, and WebP attachments from the visual review board
- Restore points and backup export
- A text workflow when a visual review surface is unavailable

FauxProof supports text-based material such as writing, plans, prompts, instructions, and code. The review board can also attach supported pictures to a project. Picture attachment does not claim visual-difference analysis, chart interpretation, or arbitrary-file comparison.

## Requirements

- Claude Code 2.1.231 or newer, installed and authenticated
- A web browser for the FauxProof sign-in flow
- A FauxProof account

## Test from source

Clone this repository and load the plugin directly:

```bash
git clone https://github.com/cynthiasisk77-coder/fauxproof-claude-plugin.git
claude --plugin-dir ./fauxproof-claude-plugin
```

`--plugin-dir` loads the source package directly for that session. Run `/mcp`, select `plugin:fauxproof:fauxproof`, and complete sign-in. Then try:

```text
Open FauxProof and show my protected work.
```

Open a project in the review board and choose **Add picture** to select a PNG, JPEG, GIF, or WebP file from your device.

During development, run `/reload-plugins` after changing the package.

## Community marketplace

After Anthropic approves the plugin for the `claude-community` marketplace, install it from Claude Code's plugin manager as `fauxproof@claude-community`. Because FauxProof connects to an external private service, an installed marketplace copy is disabled by default until you opt in. Enable it from `/plugin` or run `claude plugin enable fauxproof`, then connect from `/mcp`.

## Safety behavior

The included skill instructs Claude to:

- keep approved content authoritative until you approve an exact proposal;
- require current-conversation confirmation before approval, unlock, import, replacement, or restoration;
- report exact differences and deterministic warnings without claiming a change is semantically safe;
- stop on stale-state conflicts rather than forcing a write;
- avoid silently creating projects; and
- avoid storing credentials or secrets as protected content.

## Privacy and security

This public repository contains only the Claude plugin wrapper and instructions. It does not contain the private FauxProof backend or any secret credentials. The bundled OAuth client ID is a public identifier for Claude Code and uses PKCE; no client secret is included. The plugin connects to FauxProof's dedicated Claude MCP route over HTTPS and uses OAuth with the `lockbox:access` scope. That route shares the existing FauxProof application core and private account storage; it does not create a second database or account system.

For a picture attachment, the review board sends the selected bytes directly to FauxProof over HTTPS with a short-lived, single-use upload credential. The credential is not put in a URL or exposed in Claude's tool arguments. FauxProof validates the picture before attaching it to the selected project and encrypts it at rest.

- [Privacy](https://fauxproof.com/privacy)
- [Terms](https://fauxproof.com/terms)
- [Support](https://fauxproof.com/support)
- Email: [fauxproof.support@gmail.com](mailto:fauxproof.support@gmail.com)

## Version

Plugin version: 1.5.0

Copyright © 2026 Lacynthia Sisk.

The files in this public Claude Code plugin-wrapper repository are licensed under the [Apache License 2.0](LICENSE). That license applies only to this repository. It does not license the private FauxProof backend, hosted service, databases, website content, or FauxProof names and trademarks.
