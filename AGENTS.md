## Artifact verification policy

- Do not compute, record, freeze, or report SHA-256 hashes by default.
- Hash only when explicitly requested, when checking a download against an authoritative checksum, or when cryptographic identity is essential.
- When hashing is necessary, hash only the minimum final artifact once.
- Never create hash manifests or hash every source, binary, log, VM image, or intermediate artifact unless explicitly requested.
- Do not include hashes in progress updates or final responses unless requested or reporting a mismatch.
- Prefer functional tests, content checks, filenames, and file sizes for routine verification.
