# DASE7506 Peer Review Report: Submission SLM v1.0

Independent reproduction of the published frozen checkpoint for submission SLM v1.0 | SwiGLU-768. Both validation-set and test-set BPB agree with the reported results within ~4e-7. This review does not reproduce training from scratch.

| Measurement | Value |
|---|---|
| Author's reported validation BPB | 1.390092 |
| Reproduced validation BPB | 1.3900916118339428 |
| Author's reported test BPB | 1.403510 |
| Reproduced test BPB, run 1 | 1.4035102536637925 |
| Reproduced test BPB, run 2 | 1.4035102536637925 |
| Validation reproduced minus reported | -3.88e-7 |
| Test reproduced minus reported | +2.54e-7 |
| Test targets | 428,405 |
| Test UTF-8 bytes | 1,292,013 |
| Scoring time, runs 1 / 2 | 44.180 / 44.306 seconds |

The two local test runs have bit-identical per-window losses. The small differences from the author's scores are consistent with cross-platform FP32 rounding; cross-platform bitwise equality is not claimed. 1.40351 is the reproduced test-set score rounded to five decimal places for the course form.

### Exact submission reviewed
- Source repository: https://github.com/wuyimingai2004-cloud/DASE7506_MP1
- Pinned commit: `0b29561bae0d1bdf1a202e137d4f048256744f3b`

### Published checkpoint
- Checkpoint SHA256: `b268841422fe04c90dd9afecab3cf29851d3361125a26a7724caa209188d956`
- Protocol: `7506-mp1-wt2-v2`, CPU / FP32 / 4 threads, full test split.

The checkpoint hash matches the author's official release SHA256SUMS exactly. The evaluator script, implementation code, tokenizer, and all three raw text splits were verified to match the standard course starter and the submitted version via SHA256 digests. These checks establish the inputs used for this evaluation; they do not establish historical training provenance.

### Environment and reproduction
Evaluation date: 2026-10-05.
Environment: Windows, CPU, Python 3.12, FP32 precision.

The following portable commands produce the same evaluation with the pinned source and flags:
```powershell
git clone https://github.com/wuyimingai2004-cloud/DASE7506_MP1.git
cd DASE7506_MP1
git checkout --detach 0b29561bae0d1bdf1a202e137d4f048256744f3b
cd code
python -m venv .venv
.venv\Scripts\Activate.ps1
pip install -r requirements.txt
python evaluate.py --checkpoint ../slm-v1.0-best.pt --split test --device cpu --precision fp32 --threads 4 --output ../evidence/test_result.json
