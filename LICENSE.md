# License

Copyright © 2026 Ian D.L.N. McLean.

This repository is dual-licensed by content type:

## Documentation and prose — CC BY-SA 4.0

Everything under `docs/`, this file's sibling `README.md`, and any other
prose, diagrams, or written research content in this repository is licensed
under the **Creative Commons Attribution-ShareAlike 4.0 International**
license. The full legal text is in
[`LICENSE-CC-BY-SA-4.0.txt`](LICENSE-CC-BY-SA-4.0.txt). In brief (this
summary is not a substitute for the full text): you may copy, redistribute,
remix, and build upon this material for any purpose, including commercially,
as long as you give appropriate credit and distribute any derivative works
under the same license.

## Code — AGPL-3.0

Any executable code added to this repository — workflow YAML, scripts,
formal implementations, test suites, or other software artifacts — is
licensed under the **GNU Affero General Public License, version 3.0**. The
full legal text is in [`LICENSE-AGPL-3.0.txt`](LICENSE-AGPL-3.0.txt). In
brief (this summary is not a substitute for the full text): you may run,
study, modify, and redistribute this code, including as part of a networked
service, provided that any modified version you make available to users
over a network — not just distributed as a copy — is also made available
under the AGPL-3.0, source included.

## Rationale for the split

This repository's actual content, as of its creation, is research prose
(a deep-research report, a research memo, and working notes) rather than
code — CC BY-SA 4.0 is the standard, appropriate license for that kind of
academic/research writing, matching how research papers and wikis are
typically licensed for maximal reuse with attribution and share-alike
continuity. AGPL-3.0 is declared in advance for any code this repository
comes to contain later (e.g., an actual formal implementation, proof
scripts, or example workflow files demonstrating a proposed
correspondence), specifically because AGPL-3.0's network-use clause matters
if any such code is ever run as a hosted service rather than only
distributed as source — a stronger copyleft guarantee than GPL-3.0 alone
would give for that case.

If a specific file's licensing is ambiguous under this split (for example,
a file mixing prose and executable examples), the file's own header should
state which license applies to it, and that statement controls.
