# ReviewKit publication probe

Disposable, explicitly authorized public verification repository. It contains synthetic review data, the bundled CLI from MBrunoS/reviewkit commit `4d1e39b9080a9455db88d9b6916786356c3527b3`, and the composite action under test. No agent is launched: the wrapper supplies synthetic Phase A output, while rendering, exporting, GitHub check publication, SARIF upload, and artifact upload use the real implementations.

The first run used the original action and exposed SARIF being attached to the workflow checkout SHA despite its explicit `sha` input. The current action includes the fix: give upload-sarif a temporary `--no-checkout` worktree pinned to the reviewed commit. The fixture PR head differs from the workflow SHA.

The four-case workflow grants `checks: write` and `security-events: write`; it asserts neutral checks on the reviewed SHA, processed SARIF analyses on that SHA, and disabled-input controls. The fixture workflow fetches the PR commit because the synthetic Phase A wrapper does not do the normal review CLI's fetch.
