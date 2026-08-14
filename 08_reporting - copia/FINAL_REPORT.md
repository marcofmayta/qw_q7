# Marco Revalidation v2 — Final Technical Report

Generated: 2026-08-11T23:23:29.519730+00:00

## Scope and locked protocol

The analysis revalidates augmentation on CIC-MalMem-2022 from the canonical SHA-256 `cc7a637a174ffe797e0af0375bce3c09561f0dc8b8115c0a6292718034f5012a`. After removing 534 exact full-record duplicates, the locked dataset contains 58,062 rows: 29,231 Benign, 9,529 Ransomware, 9,815 Spyware, and 9,487 Trojan. The fixed split is 40,642 / 8,710 / 8,710 (train / validation / fixed evaluation), seed 42. All later stages load the same row assignments and 52-feature train-only preprocessing.

Twelve feature-equivalent groups cross partitions. The split is retained for comparability and the limitation is disclosed. The final partition was inspected in older iterations, so it is described as a fixed evaluation partition reused for protocol reconciliation.

## Augmentation methods

Classical interpolation includes SMOTE, Borderline-SMOTE, and ADASYN. CTGAN was retrained on every locked training row with independent epoch-budget restarts; the selected checkpoint used 300 epochs. The stabilized QGAN used 6 qubits, 8 PCA components, two data-reuploading layers, ring-CNOT entanglement, analytic simulation, moment regularization, small initialization, and training-only output-bias calibration.

## Fidelity

One common bootstrap implementation evaluated featurewise KS, featurewise Wasserstein, and RBF-MMD against real validation rows. The best mean fidelity rank was **Original** (1.00). Fidelity is reported separately from classifier utility; no causal equivalence is assumed.

## Downstream classifier results

Validation selected **ADASYN + Random Forest**. Its fixed-evaluation Macro-F1 was 0.8044 ± 0.0005, MCC was 0.8055, and Trojan F1 was 0.7171. Across each method's best classifier, the highest fixed-evaluation Macro-F1 was **Original + LightGBM** at 0.8051 ± 0.0015.

- **Original** — best fixed-evaluation classifier: LightGBM; Macro-F1 0.8051 ± 0.0015; MCC 0.8062; Trojan F1 0.7228; mean fidelity rank 1.00.
- **ADASYN** — best fixed-evaluation classifier: Random Forest; Macro-F1 0.8044 ± 0.0005; MCC 0.8055; Trojan F1 0.7171; mean fidelity rank 3.00.
- **QGAN stabilized** — best fixed-evaluation classifier: LightGBM; Macro-F1 0.8035 ± 0.0005; MCC 0.8047; Trojan F1 0.7207; mean fidelity rank 6.00.
- **Borderline-SMOTE** — best fixed-evaluation classifier: Random Forest; Macro-F1 0.8027 ± 0.0000; MCC 0.8037; Trojan F1 0.7178; mean fidelity rank 4.00.
- **SMOTE** — best fixed-evaluation classifier: Random Forest; Macro-F1 0.7982 ± 0.0011; MCC 0.7991; Trojan F1 0.7129; mean fidelity rank 2.00.
- **CTGAN** — best fixed-evaluation classifier: Random Forest; Macro-F1 0.7981 ± 0.0004; MCC 0.7990; Trojan F1 0.7108; mean fidelity rank 5.00.

## Quantum handoff

The package exports balanced n=200 and n=1000 training sets in a PCA basis fit only on original real training data. The canonical convention is q=6 and 12 features (two per qubit); optional q=4/8/12 files support capacity analysis. All methods share identical validation rows. No fixed-evaluation rows or quantum outcome claims are included in the handoff.

## Conclusions and limitations

1. Fidelity and downstream utility are distinct axes and are interpreted separately.
2. The QGAN result is simulator-based and uses a declared per-class training cap.
3. CTGAN checkpoint candidates are independent deterministic restarts.
4. A group-aware sensitivity split is required before a publication-level claim.
5. No model was retuned after fixed-evaluation results were computed.