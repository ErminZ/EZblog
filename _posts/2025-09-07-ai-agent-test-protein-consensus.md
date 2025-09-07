---
layout: post
title: "Testing a Bioinformatics AI Agent on Protein Consensus and Variant Analysis"
date: 2025-09-07
tags: [bioinformatics, AI, protein, uniprot, MSA]
---

### Analyzing Protein Sequences for Consensus and Variants  

Recently, I ran a test with an AI agent to see how well it could handle a practical **bioinformatics workflow** around protein sequence analysis.  

The task I posed with the agent was:  
1. Search the UniProt database for close, functionally similar protein sequences (100–250 sequences).  
2. Run **MAFFT** multiple sequence alignment.  
3. Find the consensus amino acid at each position, along with variants and their frequencies.  
4. Identify positions where the input sequence differs from consensus.  

---

### What Worked Well and Where It Fell Short

The agent’s whole pipeline logic was spot-on and the output/calculation of each module/step is correct.  

In the first run, things got tricky:  

- It switched to NCBI BLAST and ended up with only **9 sequences**, which is too few for meaningful evolutionary insights.  
- Sequence lengths varied wildly (112–4911 amino acids)

By contrast, when I dug into UniProt myself, I pulled **250 sequences** annotated as *T-cell surface glycoprotein CD3 zeta chain*.  
- Identity: 63.5–100%  
- E-values: all strong  
- Length: 1–600 aa (much more suitable for downstream analysis)  

Then I asked agent using the above input, it worked well.

---

### Key Lesson  

The biggest gap was **decision-making**:  
- How many sequences should be included?  
- Which filters (length, annotation, identity) are appropriate?  

These are critical questions in biology, and the AI agent didn’t ask them upfront. Instead, it charged ahead with defaults that didn’t serve the biological question.  

In this way, working with the AI agent felt a bit like **mentoring**—the potential is there, but guidance is needed at each decision point.  

---

### Positive Outcomes  

When I tested another input sequence, the agent performed better—filtering based on length and producing ~100 sequences, which is much closer to the expected scale. Although a cross validation is needed.


AI in bioinformatics is promising, but not plug-and-play. Success depends on **collaboration between the agent and the human expert**. The AI provides structure and speed, while the bioinformatics scientist ensures biological relevance, makes key decisions, and interprets or ** debugs** the agent's work when needed.   

This experience left me encouraged: the agent is useful today, and with the right mentorship, it could grow into a powerful research partner.  

