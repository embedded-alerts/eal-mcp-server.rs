# Recovery delivery evidence

This repository was recovered from an earlier tangible ChatGPT artifact through the authenticated local GitHub CLI task `019fd526-f34d-7f72-94fa-2da6185f2d74`.

## Verified GitHub state

- Repository: `embedded-alerts/eal-mcp-server.rs`
- Visibility: public
- Initial repository commit: `28da347371497292f08e1245841f8b55d9bfe567`
- Original recovery-review base: `05384988c517b19e49022d32945a11c3393de0e4`
- Shared-graph main head used for the semantic rebase: `36fe20590fece70185432ccae88182dcc2cd1a89`
- Review branch: `agent/den-2287-recovery-review`
- Review pull request: `embedded-alerts/eal-mcp-server.rs#1`
- Canonical bootstrap issue: DEN-2287
- Durable recovery ledger: DEN-2797
- Shared runtime and fleet issue: DEN-957
- Wave coordination issue: `ORESoftware/mcp-rust-libs#15`
- Source reconciler SHA-256: `70e7bcdfa3a8a3e15bcbf8bd635a240baca53c9b95a36f01f4aa312f66fd18ae`

The initial implementation is preserved. The recovery branch was rebuilt on top of the merged shared Zed dependency-graph migration so it does not remove the exact shared revision, committed lockfile, closed tool descriptor, argument rejection, or locked Cargo validation.

The review delta is limited to delivery documentation and CI hardening. It does not change product package coordinates, the read-only tool boundary, or the still-pending official-`rmcp` lifecycle migration.

## Remaining sibling work

`embedded-alerts/eal-e2e` returned HTTP 404 during the 2026-08-08 reconciliation. Its repository creation remains a separate create-only queue item; this repository must not be renamed or repurposed as the E2E surface.

## Safety contract

- Never place personal access tokens, provider keys, private keys, or service credentials in source, Git configuration, workflow inputs, logs, issues, or pull requests.
- Never force-push or rewrite the published `main` history.
- Never treat an archive, local commit, or unverified branch as GitHub delivery evidence.
- Require a current repository read, exact commit SHA, pull-request URL, and CI result before marking a later recovery complete.
- Generate `.zpkg.lock` only through a real successful Zed resolver run.
- Preserve the immutable shared Rust revision and committed `Cargo.lock` until a separately reviewed dependency update lands.
