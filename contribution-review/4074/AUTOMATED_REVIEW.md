# Published evidence context

This is the unchanged automated review from the frozen October 18 checkpoint. Its pre-publication status statements are historical. The candidate is now published at [2a437e500bf54024772dd9f3d6d4149506defed2](https://github.com/agamal026/javaparser/commit/2a437e500bf54024772dd9f3d6d4149506defed2); the coordinator verified its complete tree and two-file diff. See [the current evidence index](README.md) and [the frozen packet](javaparser-4074-review-package.zip) for referenced local logs and receipts.

---

# Automated review — JavaParser #4074 candidate

**Review type:** automated source review and evidence consistency review.
**Disposition:** no blocking source correctness issue was reported by the
independent automated reviewer. The explicit generator stages, style checks,
and final full reactor completed successfully. Publication remains blocked;
automated review is distinct from personal review and maintainer acceptance.

## Reviewed source

The review concerns the candidate against upstream base
[`dc6bc07155cb0d0d7a8a427b76411848eb862136`](https://github.com/javaparser/javaparser/commit/dc6bc07155cb0d0d7a8a427b76411848eb862136):

- `LexicalDifferenceCalculator.java`:
  `2f2332d18e4aa3f3a3ffd05b728c316fa076acda041eeec4431e25f6688a5ffd`.
- Final formatted `Issue4074Test.java`:
  `728756173731ad002590c82f706a8664bfff97456f0e4a87c96f6454a0dbe996`.
- Restored `Difference.java`:
  `6889d919ff394c46f062aaf762a43ae8e2f0189b34c2eb1ac732cc3ecca2603e`.

Full relative paths and executed commands are in the [packet README](README.md).
The final patch has SHA-256
`0cb1bfaaf7ea00dc7bceea187373c0b6843c4f6f350ad93bbc743468985f60b9`.
`patch-verification.json` records isolated-index application against the pinned
base, recovering exactly tree `be582247d3fdd80bf6e72c7dca6a52922cbd19a7`.
The candidate changes only the production calculator and the new regression
file. This verification does not establish a published source commit.

The separate source reviewer first inspected the production method and the
20-case regression source before final formatting, while accurately limiting
the 208-test focused receipt to its earlier 18-case version. A subsequent
independent evidence audit reconciled the final reactor's module/per-group
totals, final source bytes and patch receipt, and the Surefire diagnostic.
The document preparer separately read the final patch, receipts, generator/style
logs, final Maven log and summary. These reviews ran no additional tests and
made no source or publication changes.

## Correctness considerations

The final production change acts on the calculated list-removal difference.
Its `IMPORTS` guard, final-index check, and predecessor requirement limit it to
the intended list operation. The independent reviewer checked that
`NodeList.remove` notifies observers before mutating the list, so the last-index
and removed-node identity checks refer to the original list. The removed child
is checked by identity against the node being removed. Every surrounding element
must have the expected kept/removed and newline classification before the swap
occurs. An unmatched pattern falls through to the original calculated result.

Moving the removed separator before the import addresses the ambiguous model
alignment without globally changing how `Difference` consumes whitespace.
That matters because the retained rejected adaptation fixed the one-blank-line
case but inserted a blank line where none existed. The final tests exercise both
preservation and that counterexample, for LF and CRLF.

The final 20-case regression class also exercises first/middle/last removal,
multiple and whitespace-filled blank lines, successive final-import removals,
a class documentation comment, and indentation before the removed import.
Those assertions establish the specific printed output in the tested cases;
they do not establish every possible comment attachment or formatting pattern.
Other existing lexical-preservation tests were included in the focused and core
commands.

Prior work is credited to
[MysterAitch's broad PR #2704](https://github.com/javaparser/javaparser/pull/2704).
The rejected local adaptation and its failure are recorded separately from the
final structural correction. No claim is made that the complete historical PR
was applied or independently validated on this base.

## Evidence reconciliation

| Run | Supported conclusion |
| --- | --- |
| Original baseline regression | One executed assertion failed by losing the blank line. Earlier DNS/TLS failures occurred before test execution. |
| Expanded baseline | Six failures among 202 tests, with four skips; 12 cases belonged to the new regression class. |
| Rejected horizontal-only adaptation | Two failures among the same 202 tests, with four skips; the two failures inserted an unwanted blank line. |
| Revised focused candidate | 208 tests, zero failures/errors, four skips, including 18 new regression cases. |
| Core candidate before final formatting | Maven's aggregate and 296 per-group log summaries agree on 2,924 tests, zero failures/errors, eight skips, including 20 new cases. |
| Generator and style stages | Both explicit generator modules and final root install succeeded; Spotless application and Checkstyle/Spotless checks succeeded. |
| Final formatted full reactor | All nine modules succeeded with `AlsoSlowTests`: 5,831 tests, zero failures/errors, 35 skips; all 20 new cases passed. |

The full core `build.log` is authoritative for the aggregate and includes
296 group summaries. The copied text-report collection contains only
246 summaries totalling 2,673 tests; it is incomplete for nested/display-named
groups accounting for the remaining 251 tests. The full log supports the
2,924 count, and the retained `Issue4074Test` report records all 20 pre-format cases.
This limitation affects the report collection, not the recorded successful Maven
aggregate. Do not silently substitute an earlier test file or sum the incomplete
collection as though it were complete.

That collection limitation applies to the earlier core run. Its test source
had SHA-256 `8380d49e42f93d8afe8df37f34fb85d4664913910d3403d19102779e5c44a600`.
The final formatted source has the different digest listed above and was tested
in the full reactor. Only the 12-case historical test source is separately saved
as `baseline-expanded-test.java`; the one-case and 18-case sources are identified
by receipt hashes rather than claimed as packaged snapshots.

The final Maven log's five module aggregates and all **617 per-group summaries**
independently total 5,831 tests: 2,924 core, 625 BDD, three generator,
11 serialization and 2,268 symbol-solver tests. Its SHA-256 is
`b3691d527a7539384101b29cdacc653dd270712556fdb5a4cb6b04290773c998`.
Commands using `--log-file` intentionally left `build.log` empty; the receipt's
`log_sha256` describes that empty console file. Their actual output is in
`maven.log`, with the final digest also recorded in `final-reactor-slow/summary.json`.

## Retained limitations and handoff

The original DNS/TLS setup attempts, rejected candidate, unclassified first
generator-script exit 1, and later failed generated-output cleanup remain
recorded. The prerequisite recovery succeeded across all nine modules with
tests skipped. The explicit generator and final root-build stages subsequently
completed, followed by final style and full-reactor checks.

Two post-metamodel root-install console captures returned exit 0 without terminal
Maven summaries. Their logging limitation remains unresolved. The later final
root install provides verified all-nine-module success for the build gate;
it does not retroactively verify those incomplete captures.

The final Surefire warning is classified: the retained dumpstream contains
324 informational JVM G1 GC native-output records and no exception, out-of-memory,
fatal, or other unclassified payload. Its SHA-256 is
`1370b90b080ee4b8a563098ef5d51bdb92f802aa82a940f028e7236e8ea5710a`.
The warning remains preserved alongside zero reported test failures/errors.

The diagnostic trace/helper belong to the rejected horizontal-only candidate.
They do not validate the final source; the helper requires instrumentation to
emit the internal trace. The compact packet excludes compiled classes and the
copied full instrumented third-party source.

The completed full reactor covers Linux and Java 17.0.20.1. CRLF fixtures do not
establish a Windows run, and no upstream hosted platform/JDK matrix has run.
Publication remains blocked as described in the README. Keep the unpublished
patch/source packet outside the hub under its `AGENTS.md` publication rule;
the hub receives only selected public progress. No upstream fork, comment, PR,
acceptance, bounty approval, or payment is established.
