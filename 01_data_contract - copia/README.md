# Revalidation v2 — locked CIC-MalMem-2022 data contract

- Source SHA-256: `cc7a637a174ffe797e0af0375bce3c09561f0dc8b8115c0a6292718034f5012a`
- Raw shape: (58596, 58)
- Exact full-record duplicates removed: 534
- Additional feature-equivalent distinct files retained: 25
- Feature-equivalent groups crossing partitions: 12
- Clean rows: 58,062
- Split seed: 42
- Train / validation / test: 40,642 / 8,710 / 8,710
- Candidate features: 55
- Retained after training-only constant filter: 52

All later experiments must load `split_manifest.csv` or
`malmem2022_clean_locked.csv.gz`; they must not create a new split.
