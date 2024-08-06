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
    ncpus: 1

set-resources:
    gpu_job:
        mem: "4"
        walltime: 5:00
        ncpus: 1
        ngpus: 1
        gpu_type: "A40"
```

where this can be placed in a `pbs` directory in the working directory, and passed to snakemake via `--profile pbs`. If resources are not listed under rule names in the `set-resources` section (such as those for `gpu-job` in this example), then they will be taken from `default-resources`.
