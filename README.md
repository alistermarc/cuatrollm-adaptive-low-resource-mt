# CuatroLLM: Niche Translations with Adaptive In-Context Learning

This project explores the capabilities of CuatroLLM, a 1.3B parameter, four-language (English, French, Spanish, German) large language model, for niche machine translation tasks. We use an adaptive fine-tuning approach to enhance its performance on specialized domains and explore its potential for low-resource languages like Filipino.

## Base Model

The experiments are centered around the `britllm/CuatroLLM` model, available on Hugging Face:
[https://huggingface.co/britllm/CuatroLLM](https://huggingface.co/britllm/CuatroLLM)

## Project Objectives

This project has three primary objectives:

1.  **Benchmark Replication:** Replicate the baseline performance of CuatroLLM on complex reasoning tasks (ARC-C, Hellaswag, PAWS-X, etc.) as reported in the original paper.
2.  **Adaptive Fine-Tuning for EN-FR:** Evaluate and enhance CuatroLLM's English-to-French translation capabilities in the scientific domain using the adaptive machine translation (MT) approach, which leverages in-context learning from a few examples.
3.  **Low-Resource Translation for EN-FIL:** Explore the feasibility of fine-tuning CuatroLLM for English-to-Filipino translation, a language it was not pre-trained on, using a small, compiled dataset.

## Repository Structure

*   `evaluation/`: Contains the Jupyter notebooks used to conduct the experiments for each objective.
    *   `objective_1/`: Notebooks for replicating the baseline reasoning benchmarks.
    *   `objective_2/`: Notebooks for fine-tuning and evaluating English-French translation.
    *   `objective_3/`: Notebooks for the English-Filipino translation experiment.
*   `results/`: Contains the raw JSON output files from the evaluation scripts.

## Key Findings

### 1. Benchmark Replication

We successfully replicated the complex reasoning benchmarks from the original CuatroLLM paper, confirming the baseline performance of the model across English, French, German, and Spanish. Our results were not statistically different from the reported values (p > 0.05), except for German.

### 2. English-French Niche Translation

The adaptive fine-tuning approach significantly improved translation quality for the niche scientific domain.

*   **One-shot learning is powerful:** Providing a single correct translation example (one-shot) dramatically boosted performance compared to zero-shot translations.
*   **Efficient Fine-Tuning:** The adaptive MT fine-tuning method (using PEFT/LoRA) proved more effective for this niche task than the continued pre-training approach from the original paper, without requiring large additional datasets.

**English-French Translation Performance (Fine-Tuned Model)**
| MT Metric | Replicated fine-tuned (0-shot) | Replicated fine-tuned (1-shot) |
| :--- | :--- | :--- |
| **BLEU** | 33.51 | 43.39 |
| **chrF++** | 56.49 | 62.85 |
| **TER** | 63.37 | 52.84 |

### 3. English-Filipino Low-Resource Translation

The attempt to fine-tune CuatroLLM for English-to-Filipino translation was largely unsuccessful.

*   The model struggled to produce meaningful translations, as indicated by the very low BLEU and chrF++ scores compared to a dedicated translation model like NLLB.
*   This is likely because Filipino was not part of the model's pre-training, and the small size of our fine-tuning dataset was insufficient to teach the new language patterns effectively.

**English-Filipino Translation Performance Comparison**
| MT Metric | CuatroLLM (1-shot) | NLLB (0-shot) |
| :--- | :--- | :--- |
| **BLEU** | 0.14 | 40.14 |
| **chrF++** | 6.25 | 61.79 |
| **TER** | 116.40 | 50.53 |

## Conclusion

CuatroLLM demonstrates strong potential for niche translation tasks when guided by adaptive, in-context learning methods. This approach is highly effective for domain-specific translations in its pre-trained languages. However, extending the model to new, low-resource languages like Filipino requires more than just a small fine-tuning dataset; inclusion in the pre-training corpus would likely be necessary for success.

## How to Replicate

The experiments can be reproduced by running the Jupyter notebooks located in the `evaluation/` directory, corresponding to each of the three objectives.

## Authors & Acknowledgements

*   Jace Roldan
*   Drandreb Earl Juanico
*   Alister Marc Domilies

This project was completed for the AI351 course of the MEngAI program at the University of the Philippines Diliman.