![Banner](banner.png)

# misconfig-ConfigDiffAnomalyDetector
Compares each configuration file in a directory against a prior snapshot of the same file in a separate history directory, and flags the file when the diff line ratio passes one threshold. That is the whole method: one text diff ratio against one threshold. Content is compared as text and is not parsed. There is no frequency count, no severity weighting, no statistic over time, and no history kept between runs. The snapshot is supplied by the operator on each run with `--history-dir`. - Focused on Check for misconfigurations in configuration files or infrastructure definitions

## Install
`git clone https://github.com/ShadowStrikeHQ/misconfig-configdiffanomalydetector`
Then install the linters the scan runs: `pip install -r requirements.txt` (yamllint and jsonlint).

## Usage
`python3 main.py <current_dir> --history-dir <prior_snapshot_dir> [params]`
The history directory must be a different directory from the one being scanned. A file with no snapshot counterpart is noted as seen for the first time and does not count as compared.

## Parameters
- `-h`: Show help message and exit
- `--history-dir`: Directory holding the prior snapshot to compare against. Required.
- `-t`: Diff ratio threshold, 0 to 1. Defaults to 0.1.
- `-f`: No description provided
- `-d`: Enable debug logging.

## Exit codes
- Exit 0: at least one file was compared against its snapshot version, and no diff ratio passed the threshold.
- Exit 1: an anomaly was found, a validation failed, or no file was compared at all. An empty current directory, an empty scan list, and a run where a missing yamllint or jsonlint binary caused every file to be skipped all exit 1, and the run logs how many files were compared and how many were skipped. A run that checked nothing is never reported as a clean scan.

## License
Copyright (c) ShadowStrikeHQ
