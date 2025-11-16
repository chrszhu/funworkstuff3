Short summary
- C-based simulation/filtering project that synthesizes a noisy 3D image volume, applies a particle-filter-like algorithm, and outputs processed values. The code uses OpenMP for parallelism and includes custom RNG and simple morphological operations.

Why this matters to recruiters
- Demonstrates systems-level C programming, performance tuning, and parallelization with OpenMP.
- Shows practical use of numerical methods, array memory layout, and performance measurement.
- Contains build automation via `Makefile` and simple instrumentation for profiling/memory tracing.

Tech stack & tools
- Language: C
- Parallelism: OpenMP
- Build: `Makefile` / `gcc`
- Tools: `gprof` (optional), `mtrace` (optional)

What I implemented / contributions to highlight
- Custom random number generators and statistical sampling routines.
- 3D array indexing and morphology utilities (`imdilateDisk`, `dilateMatrix`).
- Particle-filter-style functions (`func0`..`func5`) implementing weighting, resampling, and estimation.
- Performance-focused build flags and optional instrumentation (`-O3`, `-DMTRACE`, `-pg`).

Build & Run
1. Build the parallel binary (recommended):

```sh
make omp
```

2. Run the program (it reads `seed.txt` and writes `output.txt`):

```sh
./omp
```

Notes
- The code expects `seed.txt` to exist in the working directory (the repository contains a large `seed.txt` used for repeatable results).
- To build a non-OpenMP binary: `make seq`.
- To enable memory tracing (requires `mtrace`): `make MTRACE=1 omp` then run and inspect `mtrace.out`.

Files of interest (quick guide for reviewers)
- `main.c` — program entry, array allocation, initialization, filter invocation, timing.
- `func.c` / `func.h` — particle-filter components and resampling logic.
- `util.c` / `util.h` — utility functions: RNGs, morphology, helpers, timing.
- `filter.c` — orchestrates the filtering algorithm (primary pipeline).
- `Makefile` — build targets `seq`, `omp`, and instrumentation flags.

Suggested talking points for interviews
- Memory layout choices for 3D data and cache-friendly iteration.
- Parallelization strategy and thread-safety considerations with OpenMP.
- RNG implementation and statistical correctness of sampling/resampling.
- Performance tuning steps you took (compiler flags, profiling, instrumentation).

Next steps I can do
- Polish README tone and add a one-paragraph personal summary/role description.
- Add example output snapshot or simple test harness.
- Add CI build (GitHub Actions) to compile `omp` and run smoke tests.

Contact
- If you want me to tailor this README to a specific role or audience (engineer vs recruiter), tell me the target and I will adapt it.
