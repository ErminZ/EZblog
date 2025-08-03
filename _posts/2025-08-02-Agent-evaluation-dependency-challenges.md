---
layout: post
title: "Agent Evaluation in Bioinformatics – Dependency Challenges"
---

## Overview

This post documents the first stage of evaluating an AI assistant agent for bioinformatics workflows, specifically targeting a **molecular dynamics simulation pipeline** for antibody-antigen complexes. While the agent was able to generate a reasonable plan in under 30 minutes, it encountered multiple issues related to dependency setup and reproducibility when the protocol was repeated.

This is **Part 1** of a multi-part series. The current focus is on initial usability, reproducibility, and DevOps-related challenges.

---

## Use Case: Accelerating New Analysis Onboarding

A common scenario in bioinformatics teams is being tasked with a data analysis workflow that hasn't been run in-house before. In such cases, significant time is often spent on:

- Literature review
- Tool discovery and comparison
- Setting up analysis environments
- Estimating timelines without clear baselines

This makes such tasks a strong candidate for AI agent support—particularly in rapidly generating scaffold workflows that can be later customized to institutional standards.

---

## Task: Molecular Dynamics Simulation

**Objective:**  
To assess whether a predicted antibody-antigen structure is stable in a simulated dynamic environment using molecular dynamics (MD) tools.

**Target Timeline:**  
Approx. 1 working day  
- Initial agent output: ~30 minutes  
- Debugging and re-running: several hours

---

## Initial Agent Performance

### ✅ Positive Observations

- **Clear Explanation and Checking of Input**  
  The agent provided a helpful summary of input formats after checking.

- **Great Interactive User Experience: Resilience to Execution Errors**  
  When Jupyter notebooks failed to execute, the agent pivoted to generate standalone Python scripts instead.

- **Productivity Boost for Initial Planning**  
  The agent’s scaffold saved several hours of setup and reading time. While not error-free, it offered a fast starting point.

---

## Limitations Encountered

### Environment and Dependency Issues

- **Jupyter Integration Failed**  
  Attempted three times, but notebooks failed to load or run. Ideally, the agent should a link like [Google Colab](https://colab.research.google.com/github/sokrypton/ColabFold/blob/main/AlphaFold2.ipynb#scrollTo=UGUBLzB3C6WN) or provide `.ipynb` files with download links.

- **Intepretation of Output Improvement**  
  No output files were linked for download, making it harder to test or intepret outputs without direct agent assistance.
  Further request on interpretation of output files encounter Conversation Error.

- **Tool Usage Lacked Context**  
  The pipeline would benefit from a concise summary of each tool’s:
  - Input format
  - Output type
  - Core function

---

## Reproducing the Pipeline: Docker-Related Errors
The first step is setup the enviroment to run/repeat locally since the Jupyter netwrok doesn't work.

### 🐳 Dockerfile Error #1
I provided the error messaged and agent generated newer Dockerfiles, but encountered different errors for 3 loops.
```
Error1_agent
failed to solve: nvidia/cuda:11.8-devel-ubuntu22.04: not found

Error2_agent: Miniconda Install Failure
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
exit code: 133

Error3_agent with Miniforge
rosetta error: failed to open elf at /lib64/ld-linux-x86-64.so.2
```

I checked Dockerfile Error #1, and noticed should be corrected to nvidia/cuda:11.8.0-devel-ubuntu22.04. But later encountered another error: 

```
ERROR: failed to build: failed to solve: process "/bin/sh -c wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O miniconda.sh && bash miniconda.sh -b -p /opt/conda && rm miniconda.sh" did not complete successfully: exit code: 133
```

Another LLM-based agent (Claude) was tested as a fallback but encountered other new errors. 

## Conclusion

In this early test, the AI agent demonstrated promising capabilities in quickly drafting a new analysis workflow, particularly for less familiar tasks. However, repeatability and deployment remain major blockers, for example the environment setup and Docker builds.


