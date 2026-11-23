# Exceptions

One row per rule this repository cannot meet yet. The reason and the revisit date
are required. The shared `standard` job reads this file.

| Rule | Reason | Revisit |
| --- | --- | --- |
| `C5.1` | The median of the last 20 pull request runs at the audit snapshot was 202 s. After this change the first run took 185 s with a cold NuGet cache and the second took 38 s warm, measured from the first job starting to the last required check finishing. The cold case is dominated by `security / trivy` (3m5s) and by the .NET restore/build/test cycle in the `fmt`, `test` and shared `coverage` jobs; the warm case is under the 60 s budget. The next step is to re-measure the median over the next 20 runs now that the NuGet cache is restored, and to share one build between the `test` and `coverage` jobs. | 2027-02-28 |
| `C7.4` | `scripts/coverage.mjs`, `scripts/cobertura-to-lcov.mjs`, `scripts/write-openapi.mjs`, `scripts/prune.mjs` and `scripts/agent-files.mjs` are still `.mjs` on Node. The application has no JavaScript or TypeScript sources, so the repository keeps the .NET toolchain behind the core recipe names and runs the helpers on the pinned Node until they port to Bun TypeScript. | 2027-05-31 |
