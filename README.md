# Snakemake PBS executor plugin

This is a plugin for the [Snakemake](https://snakemake.readthedocs.io/en/stable/) workflow management system (Snakemake >= 8) that allows you to submit jobs to a PBS cluster. Specifically, this also includes a workaround for cases where the job status of a completed job is not reported.

## Installation

To install the plugin, pip install the checked out repository:

```bash
git clone git@github.com:dpohanlon/snakemake-executor-plugin-pbs.git;
cd snakemake-executor-plugin-pbs;
pip install .;
```

## Usage

To use the plugin, you need to specify the `--executor pbs` flag when running Snakemake. However the easiest way is to specify configuration arguments via a configuration YAML file, `config.yaml`:

```yaml
executor: pbs
jobs: 100

default-resources:
    mem: "8"
    walltime: 1:00
    cpus: 1
```

where this can be placed in a `pbs` directory in the working directory, and passed to snakemake via `--profile pbs`.
