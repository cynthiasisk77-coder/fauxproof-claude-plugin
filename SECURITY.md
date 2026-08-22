# Security

Report a suspected FauxProof security issue privately to [fauxproof.support@gmail.com](mailto:fauxproof.support@gmail.com). Do not open a public issue with credentials, access tokens, private documents, account identifiers, or exploit details.

Include only the minimum information needed to reproduce the issue. FauxProof support will never ask you to send a password, access token, payment-card number, full protected document, MFA code, or one-time passcode by email.

The Claude plugin contains no secret credentials. Its bundled OAuth client ID is a public identifier for the Claude Code PKCE flow; no client secret is included. It connects over HTTPS and requests only the OAuth scope `lockbox:access`.
