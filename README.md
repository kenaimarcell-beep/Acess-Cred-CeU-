DEX Silverback — project bootstrap
-------------------------------

Purpose
- "DEX silverback" is a prototype framework for a new security-catalog file type (security catalog / changelog-backup) used to catalog CRM change-management retention records tied to device certificates and CI_CL/C++ measurement reports.
- Provides: data schema, CI_CL input report skeleton (C++), reward-distribution generator (Python), checksum validation, and GitHub Actions-based CI to validate integrity.

Quick start
1. Clone or initialize repository.
2. Generate keypair and device certs (see spec/ for commands).
3. Add your https dataset(s).
4. Run tests:
   - Python: `python3 scripts/checksum_test.py --file path/to/data --expected-checksum <hex>`
   - Build C++: use your toolchain (see src/).
5. Commit with author `kenaimarcell` if required:
   `git commit -m "chore: init DEX silverback" --author="kenaimarcell <kenaimarcell@users.noreply.github.com>"`

Notes
- Replace placeholder values in spec/ with your org’s certificate signing policies and device mapping.
- CI expects `GPG_PRIVATE_KEY` and `CA_CERT` (or other secrets) when performing signing steps.