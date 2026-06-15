# Filigree — Invoice Integrity

Tamper-evident invoices. A cryptographic signature is carried inside the
invoice text itself — distributed across every visible character via
invisible Unicode carriers, not attached as metadata. Change one digit of an
IBAN — verification fails. Change the amount — verification fails. No
signature block to detach, no certificate authority to query.

**Live demo:** [liam499.github.io/filigree-invoice/demo.html](https://liam499.github.io/filigree-invoice/demo.html)

## Try the tamper case in two minutes

1. Open the demo.
2. Click **Generate new pair** to make a fresh key pair.
3. Copy the contents of [`sample-invoice.txt`](./sample-invoice.txt) into the
   Sign panel and click **Sign Invoice**.
4. Copy the signed output and the public key.
5. Switch to the **Verify** panel, paste both, click **Verify** — passes.
6. Edit *any character* in the signed invoice. Most obvious case: change
   one digit of the IBAN. Click **Verify** again — fails.

To a human reader the signed invoice looks identical to the original — the
carrier is invisible Unicode. The protection is bit-level: any character
edit, or any tool that strips the carrier, breaks the signature.

## How it works

ECDSA P-256 signature over the cleaned invoice text. The 512-bit signature
is distributed bit-by-bit across the visible characters via zero-width
Unicode carriers (U+200B, U+200C). A secondary homoglyph layer substitutes
visually-identical Cyrillic codepoints for a deterministic subset of Latin
letters, seeded by the signature itself. Verification is offline — the
verifier needs only the signed invoice and the vendor's public key.

The engine is ~500 lines of vanilla JavaScript, no dependencies, runs in any
modern browser.

## What's included

- `demo.html` — working sign/verify tool. Single file, no build step, drop
  into any static host or embed in an existing web app.
- `index.html` — overview / landing page.
- `sample-invoice.txt` — realistic invoice for demoing the tamper case.

A separate private repository contains additional reference implementations
(per-recipient leak attribution, paragraph-level tamper localisation), a
steganalysis CLI suite, and a working-draft protocol specification covering
the design choices, threat model, and channel-survival matrix. Included with
the sale on request.

## For sale — asking from $35k

This started as a one-night side project off the back of unrelated AI /
philosophy research. We noticed the construction worked, wrote it up, and
are not commercialising it ourselves.

Looking for a buyer in AP automation, B2B fintech, e-signature,
compliance / audit, or BEC defence who can integrate it as a differentiating
feature. Less than a sprint of engineering time, with the fragile-
watermarking literature review, carrier choice, payload distribution,
canonicalisation, and channel-survival analysis already done.

**Pricing ladder.**

- **From $35k** — IP for invoice-fraud use, non-exclusive. Full copyright
  assignment of this public repository.
- **From $60k** — Above, plus the companion private repository (per-
  recipient leak attribution, paragraph-level tamper localisation,
  steganalysis CLI suite, working-draft protocol specification) and
  scoped exclusivity in an adjacent vertical of your choice.
- **From $100k** — Full transfer of the entire research strand including
  the protocol IP.

**Plus.** Up to 16 hours of integration advisory at $250/hr after transfer.

Contact: **liam.researchoutreach@proton.me**

## License

Copyright © 2026. All rights reserved. The source in this repository is
published for evaluation only. Commercial use, redistribution, and
derivative works require a license. Contact for terms.
