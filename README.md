# Filigree — Invoice Integrity

Tamper-evident invoices. The signature is woven into the invoice text itself
via invisible Unicode carriers, distributed across every visible character.
Change one digit of an IBAN — verification fails. Change the amount —
verification fails. No metadata to strip, no signature block to detach, no
certificate authority to query.

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

## For sale

This started as a one-night side project off the back of unrelated AI/
philosophy research — we noticed the construction worked and wrote it up,
but we are not commercialising it ourselves.

Looking for a buyer in AP automation, B2B fintech, e-signature,
compliance/audit, or BEC defence who can integrate it as a differentiating
feature. Less than a sprint of engineering time with the literature review,
carrier-choice decisions, payload distribution, canonicalisation, and
channel-survival analysis already done.

- **IP for invoice-fraud use:** asking in the low-five-figure range,
  scaling with exclusivity scope in adjacent verticals.
- **Optional advisory hours** at an hourly rate after transfer.
- **Bundle:** the additional reference implementations and the protocol
  document can be included for a larger deal.

Contact: **liam.researchoutreach@proton.me**

## License

Copyright © 2026. All rights reserved. The source in this repository is
published for evaluation only. Commercial use, redistribution, and
derivative works require a license. Contact for terms.
