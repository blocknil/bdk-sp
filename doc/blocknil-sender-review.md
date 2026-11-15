# Blocknil sender review — 2026-11-15

[PR #1](https://github.com/blocknil/bdk-sp/pull/1) contains two sender fixes. Two independent
agent source reviews inspected algorithm head `51df9ef15411057ef3e8fa4f2d6c81f8d3dbade7`, including
one fresh-context review, against the primary [BIP352 sender specification](https://github.com/bitcoin/bips/blob/master/bip-0352.mediawiki#creating-outputs).
No introduced correctness defect was found in these two algorithms. This is not an external human
audit, and the reviewers did not independently rerun the reported suites.

- Intermediate zero scalar sums are allowed; zero final sums remain rejected.
- Recipient preflight accepts 2,323 and rejects 2,324 within a complete scan-public-key group.
  Labels sharing a scan key share that limit.
- Internal callers propagate the Result and the official fixture reader expands recipient counts.

The output derivation API now returns Result. This is a breaking API change: callers must handle
or propagate the error, and a future fork release must document/version that change. No fork
release or merge is approved by this record.

The earlier upstream-lockfile run (bitcoin 0.32.7) passed 184 tests with none ignored, plus Clippy.
The Blocknil spike passed all 29 current official sender cases in its bitcoin 0.32.102 graph.
Receiver-limit and legacy PSBT-helper findings are separate and are not fixed or approved here.

Wallet integration now belongs to `blocknil/bitcoin-wallet`, branch `codex/sp0-silent-payments`,
under `spikes/silent-payments-sp0/`. Its review reports, compatibility results and preserved
execution evidence are published there. That prototype has open recovery/allocation guards and
retained-signer validation findings; it must remain draft/default-off/regtest-only. Those wallet
findings are not evidence that these two sender algorithms are incorrect.

This documentation commit changes no Rust source or dependency lockfile. The two original fix
commits remain unchanged, and nothing is pushed to the original bitcoindevkit repository.
