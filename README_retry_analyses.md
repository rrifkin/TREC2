# RETRY additional analyses

Two scripts that sit alongside `retry_stats.py` and use `retry_parser.py` unchanged. They answer the six questions in the October 29 email.

| Script | What it does |
| --- | --- |
| `retry_descriptives.py` | Tumor lobe and side, early vs late onset, ASMs, EEGs per patient, EEG length category |
| `retry_eeg_analyses.py` | (1) Hyperexcitability before a later seizure (2) Tumor location vs EEG finding location |

## Run

Use the de-identified "one-hot encoding" REDCap report (raw CSV) and the current data dictionary. Keep the CSVs outside this repository.

```
python3 retry_descriptives.py [data CSV] [data dictionary CSV]
python3 retry_eeg_analyses.py [data CSV] [data dictionary CSV]
```

Outputs are written next to the data CSV:

- `retry_descriptives.txt` and `.png`
- `retry_hyperexcitability_timing.txt` and `.png`
- `retry_location_match.txt` and `.png`

## Notes

- Timing analysis: only patients with no pre-operative seizure. For patients with a later seizure, only EEGs dated before the first late seizure count. The `.txt` file lists every cohort step.
- Models are adjusted for age only, because IDH and WHO grade cannot be estimated in this subgroup (almost all grade 4, few IDH-mutant).
- Location analysis uses LPD, LRDA, seizure and IED findings (those with a recorded side and lobe). GPD and BiPD have no location.
- Early onset = `preop_sz`; late onset = `late_sz`. "Indeterminate" and blank are treated as unknown.
