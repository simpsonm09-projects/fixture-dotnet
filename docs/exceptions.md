# Exceptions

One row per rule this repository cannot meet yet. The reason and the revisit date
are required. The shared `standard` job reads this file.

| Rule | Reason | Revisit |
| --- | --- | --- |
| `C5.1` | The audit snapshot's median pull request run was 202 s. After this change the first pull request run took 185 s from the first job starting to the last required check finishing, with a cold NuGet cache: the `security / trivy` job (3m5s) and the .NET restore/build/test cycle in the `fmt`, `test` and shared `coverage` jobs dominate it. The NuGet cache is now restored on the pull request path. The next step is to re-measure the median over 20 runs once the cache is warm, to share one build between the `test` and `coverage` jobs, and to move the `fmt` check to a lighter tool. | 2027-02-28 |
| `C7.4` | `scripts/coverage.mjs`, `scripts/cobertura-to-lcov.mjs`, `scripts/write-openapi.mjs`, `scripts/prune.mjs` and `scripts/agent-files.mjs` are still `.mjs` on Node. The application has no JavaScript or TypeScript sources, so the repository keeps the .NET toolchain behind the core recipe names and runs the helpers on the pinned Node until they port to Bun TypeScript. | 2027-05-31 |
