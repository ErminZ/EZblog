---
layout: post
title: "Testing a Bioinformatics AI Agent – Tahoe Reference Run"
date: 2025-09-02
categories: [AI, Bioinformatics, Reproducibility]
---

Recently, I tested a bioinformatics AI agent on the **Tahoe reference run**. The experience was both fascinating and instructive. I want to share some notes here — not as a critique, but as constructive feedback on what worked well and what can improve.

---

### First Impressions
Right from the start, the agent behaved very much like a professional bioinformatics scientist: it asked clarifying questions to scope the analysis, then structured the work into clear phases:

1. Environment Setup and Data Acquisition  
2. Data Preprocessing  
3. Model Setup and Configuration  
4. Inference Execution (`03_tahoe_inference.ipynb`)  
5. Results Analysis and Validation  
6. Reproducibility Assessment  

The organization was logical and easy to follow. The notebook and file structure looked excellent.

---

### Where Things Got Interesting
In **Phase 4 (Inference Execution)**, I expected to run something like:

```
state tx infer \
  --output "virtual_cell/output.h5ad" \
  --model_dir virtual_cell/ST_Tahoe \
  --checkpoint virtual_cell/ST_Tahoe/final.ckpt \
  --adata "virtual_cell/input.h5ad" \
  --pert_col "chemicals"
```
Instead, the notebook attempted inference with a custom minimal implementation:

```
inference_engine = StateInferenceEngine()
predictions = inference_engine.run_inference(
    adata, 
    perturbation_column=config['data']['perturbation_column']
)
```
Looking closer, I realized the agent had created its own MinimalStateModel inside the notebook rather than using the official STATE model from Arc Institute.
This “homemade” model was not trained on Tahoe-100M and therefore could not reproduce published results. It was essentially a placeholder, useful for demonstrating workflow structure, but not for scientific reproducibility.


### The Agent’s Response
When I raised the concern, the agent acknowledged the issue right away:

“You’re absolutely correct. The notebooks I created are using a minimal/dummy implementation, NOT the actual public STATE model. This would NOT give reproducible results from the Tahoe papers.”


### My Reflection

Working through this test felt a bit like being an examiner: I had to review the steps, trace definitions like StateInferenceEngine, and double-check where imports came from. That extra work took almost an hour before I could pinpoint the gap between “demo workflow” and “real Tahoe reproducibility.”

While the detour was unexpected, the process highlighted two important points:

* The agent is excellent at structuring pipelines, generating notebooks, and keeping workflow logic clean.

* For scientific reproducibility, it’s crucial that AI-generated workflows pull in the real, published models by default, rather than safe placeholder versions.


