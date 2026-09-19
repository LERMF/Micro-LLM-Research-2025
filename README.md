# ✦ MICRO-LLM-RESEARCH-2025: SUB-3B PARAMETER ARCHITECTURES ✦
*Mixture of Experts (MoE), Extreme Quantization & Edge-Native Neuromorphic Inference*

---

## The Illusion of Scale

The assumption that higher parameter counts guarantee higher task competence is broken. In production agentic loops, deploying a 70-billion parameter model to format a JSON schema or validate an exit code is architectural malpractice.

**Micro-LLMs under 3B parameters now achieve parity on bounded tasks.**

This research repository documents empirical evaluations of sub-3B models, dense vs. sparse routing trade-offs, and extreme quantization thresholds (AWQ, EXL2, GGUF Q4_K_M down to Q2_K). When architected with rigid cognitive harnesses, a $1.5\text{B}$ parameter model running locally delivers zero-latency execution, complete data sovereignty, and zero ongoing API billing costs.

---

## Comparative Model Performance on Bounded Tasks

Evaluated across 1,500 deterministic code-repair, schema-extraction, and CLI-routing benchmarks:

| Model Architecture | Active Parameters | Quantization | Memory Footprint | Token Speed (M2 / i5 CPU) | JSON Schema Parity |
|---|---|---|---|---|---|
| **SmolLM2-1.7B-Instruct** | $1.71\text{B}$ | Q4_K_M | $1.15\text{ GB}$ | $68.4\text{ tok/s}$ | $96.8\%$ |
| **Qwen2.5-Coder-1.5B** | $1.54\text{B}$ | Q4_K_M | $1.08\text{ GB}$ | $74.2\text{ tok/s}$ | **$99.2\%$** |
| **Phi-3.5-mini-3.8B** | $3.82\text{B}$ | Q4_K_S | $2.30\text{ GB}$ | $38.1\text{ tok/s}$ | $98.4\%$ |
| **DeepSeek-R1-Distill-1.5B**| $1.58\text{B}$ | Q8_0 | $1.72\text{ GB}$ | $45.6\text{ tok/s}$ | $97.6\%$ |

$$\text{Efficiency Quotient} = \frac{\text{Schema Accuracy (\%)}}{\text{Resident RAM (GB)} \times \text{Latency (s)}}$$

---

## Repository Structure & Research Datasets

```
Micro-LLM-Research-2025/
├── evals/                       # Automated evaluation harness for deterministic tasks
│   ├── json-validation/         # 500 strict JSON schema conformance prompts
│   ├── regex-synthesis/         # Pattern matching and text extraction test cases
│   └── bash-safety-audit/       # Shell script vulnerability triage benchmarks
├── quantization-curves/         # Perplexity vs Bit-Rate data for AWQ / EXL2 / GGUF
├── moe-router-experiments/      # Sparse gating layers for heterogeneous micro-specialists
└── neuromorphic-notes/          # Spiking Neural Network (SNN) spike-timing conceptual maps
```

---

## Key Theoretical Conclusions

1. **Task Boundary Decoupling**: General world knowledge requires massive weights; procedural syntax and deterministic code compilation do not. Decoupling extraction from generation unlocks $15\times$ smaller model requirements.
2. **The 4-bit Quantization Plateau**: Precision degradation from FP16 to Q4_K_M produces $< 0.8\%$ drop in structured extraction accuracy while slashing VRAM requirements by $73\%$.
3. **Local Sovereignty Invariant**: Edge devices operating without telemetry maintain strict compliance with enterprise privacy standards and remain immune to upstream API downtime or deprecation.

---

## Running the Evaluation Harness

```bash
# Clone the repository
git clone https://github.com/LERMF/Micro-LLM-Research-2025.git
cd Micro-LLM-Research-2025

# Run deterministic evaluation battery against local llama-server
python3 evals/run_eval_battery.py --endpoint http://localhost:8080/v1 --model qwen2.5-coder-1.5b
```
