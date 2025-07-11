# SNP Probe Binding and Mismatch Detection

This Python script analyzes the binding of a DNA probe sequence to a reference DNA sequence and its SNP (Single Nucleotide Polymorphism) variant. It identifies mismatches between the probe and the SNP variant at the binding site.

---

## Features

- Finds the binding position of the probe on the reference DNA sequence.
- Compares the probe binding on the SNP variant sequence.
- Reports mismatches including their positions and the differing nucleotides.

---

## Code Overview

```python
from Bio.Seq import Seq

# Reference and SNP variant sequences
reference_seq = "ATGCGTACGTTAGCTAGCTAGCGATCGATCGTTAGCTAGTCGATCGATGC"
snp_variant_seq = "ATGCGTACGTTAGCTAGCTAGCGATCGATTGTTAGCTAGTCGATCGATGC"
probe_seq = "AGCGATCGATCGTTAGCTAG"

# Find binding position
def find_binding_position(seq, probe):
    return seq.find(probe)

# Compare mismatches
def compare_binding(seq, probe, start_pos):
    mismatches = []
    for i in range(len(probe)):
        if seq[start_pos + i] != probe[i]:
            mismatches.append((i + 1, seq[start_pos + i], probe[i]))
    return mismatches

# Get position
ref_pos = find_binding_position(reference_seq, probe_seq)

# Evaluate mismatches
if ref_pos != -1:
    mismatches = compare_binding(snp_variant_seq, probe_seq, ref_pos)
    print(f"Probe mismatch count: {len(mismatches)}")
    for pos, actual, expected in mismatches:
        print(f"Position {pos}: '{actual}' → '{expected}' (Mismatch)")
else:
    print("Probe does not bind to the reference sequence.")
