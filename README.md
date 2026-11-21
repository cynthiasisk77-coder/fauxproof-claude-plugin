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

## Install

1. In Claude, open the plugin directory and search for **FauxProof**.
2. Select **Install**. Because FauxProof connects to an external private service, the plugin is disabled by default until you turn it on.
3. Turn the plugin on, then connect FauxProof and complete the sign-in in your browser. In Claude Code, enable it from `/plugin` and connect from `/mcp`.

Then try:

```text
Open FauxProof and show my protected work.
```

If you ask Claude to save an attached screenshot, photo, or graph, Claude should immediately call FauxProof's picture action and show **Add a picture to FauxProof**. Click it, choose **Add picture from device**, and select that same image. A public download link is neither needed nor requested. To bring it back later, ask Claude to open the saved picture; FauxProof returns the exact stored image and an exact-file download.

## Safety behavior

The included skill instructs Claude to:

- keep approved content authoritative until you approve an exact proposal;
- require current-conversation confirmation before approval, unlock, import, replacement, or restoration;
- report exact differences and deterministic warnings without claiming a change is semantically safe;
- stop on stale-state conflicts rather than forcing a write;
- avoid silently creating projects; and
- avoid storing credentials or secrets as protected content;
- route Claude chat pictures to FauxProof's private device picker without requesting a public URL; and
- retrieve saved pictures with `list_project_files` followed by `open_project_file`, returning the exact stored image instead of a text summary.

## Privacy and security

This public repository contains only the Claude plugin wrapper and instructions. It does not contain the private FauxProof backend or any secret credentials. The bundled OAuth client ID is a public identifier for Claude Code and uses PKCE; no client secret is included. The plugin connects to FauxProof's dedicated Claude MCP route over HTTPS and uses OAuth with the `lockbox:access` scope. That route shares the existing FauxProof application core and private account storage; it does not create a second database or account system.

For a picture attachment, Claude first calls `open_picture_upload` and shows **Add a picture to FauxProof**. After you click it, the upload page sends only the file you select through **Add picture from device** directly to FauxProof over HTTPS with a short-lived, single-use upload credential. Claude cannot forward an image attached at chat level into a remote connector, so the user reselects that same image; no public URL is required. The credential is not put in a URL or exposed in Claude's tool arguments. FauxProof validates the picture before attaching it to the selected project and encrypts it at rest. Saved pictures are returned through short-lived, account/project/file-bound private preview and exact-download links.

- [Privacy](https://fauxproof.com/privacy)
- [Terms](https://fauxproof.com/terms)
- [Support](https://fauxproof.com/support)
- Email: [fauxproof.support@gmail.com](mailto:fauxproof.support@gmail.com)

## Version

Plugin version: 1.5.6

Copyright © 2026 Lacynthia Sisk. All rights reserved.

The files in this repository are proprietary and may not be copied, modified, or redistributed without written permission; you may install and use the plugin to access the FauxProof service. See [LICENSE](LICENSE). This does not license the private FauxProof backend, hosted service, databases, website content, or FauxProof names and trademarks.
