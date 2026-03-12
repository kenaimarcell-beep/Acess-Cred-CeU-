DEX silverback — draft spec
---------------------------

Overview
- DEX silverback collects CRM change-management events, associates them to artifacts (https datasets), computes and stores checksums, and catalogs them in a security-catalog file (see spec/security_catalog.schema.json).
- Each catalog entry contains metadata linking to a CI_CL input report (C++ produced) and device certificate metadata (for mapping to 504x.3 device patterns).

Key components
1. Security-catalog file (.json) — canonical format for retention & compliance.
2. CI_CL input report (C++ generated) — measurement and intrinsic metric output; hashed and referenced by catalog.
3. Device certificate integration — device certs (signed by your CA) are recorded with serial/fingerprint and policy tags.
4. Rewards & distribution engine (generate_rewards.py) — computes distributions on a configured cadence (default: twice per quarter).

Certificate workflow (example)
- Create CA and issue device certs:
  - `openssl genpkey -algorithm EC -pkeyopt ec_paramgen_curve:P-384 -out ca.key`
  - `openssl req -x509 -new -nodes -key ca.key -sha256 -days 3650 -out ca.crt -subj "/CN=DEX-CA"`
  - Generate device keys and CSRs and sign with CA.
- Store device metadata (id, serial, fingerprint) into the security-catalog entry.

Checksum validation
- Use SHA256 for artifact and CI_CL report.
- CI must compute SHA256 and compare with expected value in a catalog entry.
- Failing validation causes CI pipeline to break and notify owners.

Backup changelog policy
- On each release commit, create a copy of CHANGELOG.md into changelogs/backup-YYYYMMDD.md.

Open questions
- Confirm exact cadence for "bi-semi-quarterly".
- Confirm signature algorithms and device cert policy specifics (RSA/ECDSA & key sizes).