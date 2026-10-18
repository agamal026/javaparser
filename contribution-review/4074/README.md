# JavaParser #4074: source and validation evidence

The focused fix is published at [`2a437e500bf54024772dd9f3d6d4149506defed2`](https://github.com/agamal026/javaparser/commit/2a437e500bf54024772dd9f3d6d4149506defed2) on `fix/4074-preserve-import-spacing`. It changes two source/test files: 142 insertions and one deletion. The source branch contains no review archive.

The final validation run completed on October 18, 2026, before the publication commit was created. Recovery verified the two file hashes and the entire candidate Git tree against the tested checkpoint; source was not changed or rebuilt during publication.

## Exact source

| Identity | Value |
| --- | --- |
| Upstream base | `dc6bc07155cb0d0d7a8a427b76411848eb862136` |
| Published source commit | `2a437e500bf54024772dd9f3d6d4149506defed2` |
| Tested and published Git tree | `be582247d3fdd80bf6e72c7dca6a52922cbd19a7` |
| Patch SHA-256 | `0cb1bfaaf7ea00dc7bceea187373c0b6843c4f6f350ad93bbc743468985f60b9` |
| Production file SHA-256 | `2f2332d18e4aa3f3a3ffd05b728c316fa076acda041eeec4431e25f6688a5ffd` |
| Regression file SHA-256 | `728756173731ad002590c82f706a8664bfff97456f0e4a87c96f6454a0dbe996` |

## Complete review packet

[Download the frozen review packet](javaparser-4074-review-package.zip). The 886,410-byte ZIP has SHA-256 `53b6045723923e76da627a82e19245a83c617bf97f842a520498c37a8372d0bc`.

Extract it and start with `javaparser-4074-review/README.md` and `REPRODUCE.md`. It includes the exact patch, regression and rejected-experiment evidence, command receipts, complete final Maven log, retained test reports and diagnostics, automated review, licensing notices, and checksums. All 871 entries in `SHA256SUMS` were independently checked after recovery.

This archive preserves the pre-publication checkpoint unchanged. Its historical draft and access-status statements describe that checkpoint. This page records the later source publication. The archive does not claim an exhaustive collection of every Surefire text report: its README identifies the earlier missing nested/display-group files and treats the complete Maven logs as authoritative.

## Validation

On Linux with Temurin Java 17.0.20.1 and Maven 3.10.0, the final `clean test --activate-profiles AlsoSlowTests` reactor reported **5,831 tests, zero failures, zero errors, and 35 skips**, with all nine modules successful. This includes all 20 final regression cases. The authoritative log and command are inside `final-reactor-slow/`; [the retained run summary](FINAL-REACTOR.json) records hashes and scope.

Both explicit generator stages, the final root install, Spotless application, and `checkstyle:check spotless:check` passed. The earlier single-case baseline failed as expected; the expanded baseline selection had six failures. The final fix preserves the existing blank-line count across LF/CRLF cases without modifying `Difference.java`.

The full log's SHA-256 is `b3691d527a7539384101b29cdacc653dd270712556fdb5a4cb6b04290773c998`. An independent automated review reconciled its 617 per-group summaries to the same totals. Surefire's retained native-stream warning contains informational G1 GC output; no test failure or error was reported. Earlier setup failures, two incomplete intermediate console captures, and their limitations remain documented.

These are the recorded Linux/Java 17 results. LF/CRLF fixtures do not establish a Windows execution, and this checkpoint does not claim that the upstream hosted OS/JDK matrix has run.

## Review and prior work

[Automated source review](AUTOMATED_REVIEW.md) preserves its original technical findings and limitations. A separate recovery review independently matched the archive, source tree, file hashes, final receipts and test totals. The coordinator separately read back the published source commit and its two-file diff from GitHub.

Prior work includes MysterAitch's [#2704](https://github.com/javaparser/javaparser/pull/2704) and SaltedReed's closed, unmerged [#4584](https://github.com/javaparser/javaparser/pull/4584) and [#4590](https://github.com/javaparser/javaparser/pull/4590). The latter discussions requested a focused change, a regression and explanatory comments. The current approach normalizes the import separator's structural alignment. The rejected local generic-whitespace experiment and its regression failures remain distinct from those historical PRs.

AI assisted investigation, implementation, regression development, validation triage and documentation. Automated review is recorded as automated; no personal review, legal signature, maintainer acceptance, benefit eligibility or payment is asserted.

At creation of this evidence commit, the upstream PR is prepared but not yet submitted. The contribution hub will link the actual upstream submission after verification.
