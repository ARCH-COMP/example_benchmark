# ARCH-COMP benchmark skeleton

Minimal skeleton for an ARCH-COMP benchmark set. Unlike VNN-COMP (one repository per
benchmark), an ARCH-COMP **category** ships a single repository whose `instances.csv`
lists every benchmark and instance in that category.

Submitting a benchmark set is naming `(category, repository, commit)`: the platform
reads `instances.csv` at that commit and fans it out into one benchmark per distinct
`benchmark` value, each owning its instances. The loaded benchmarks then become
selectable when a tool is submitted in that category.

## `instances.csv`

One row per instance. The first two columns are required:

```
benchmark,instance
ExampleBenchmark,case-a
ExampleBenchmark,case-b
AnotherBenchmark,default
```

- `benchmark` — groups instances into a benchmark (the unit a tool selects).
- `instance` — the case within that benchmark.

A category may add further columns; they are passed, in file order, to
`prepare_instance.sh` / `run_instance.sh`. One column is special by convention:

- `timeout` — per-instance wall-clock cap in seconds, enforced by the harness. Omit the
  column to leave instances uncapped.

Example with a timeout column:

```
benchmark,instance,timeout
ExampleBenchmark,case-a,300
ExampleBenchmark,case-b,300
```

## Data files

The networks, dynamics, and specification files your benchmarks reference live in this
repository (the layout is category-specific — `data/` here is just a placeholder). The
tool's `prepare_instance.sh` / `run_instance.sh` locate them by the `benchmark` and
`instance` names from each row.

See the benchmark info page for how a category's benchmarks are loaded.
