# Automatic Detection of Moral Values in Research Papers

## Overview
Research in Artificial Intelligence (AI), Machine Learning (ML), and Human–Computer Interaction increasingly discusses ethical, moral, and social values such as fairness, transparency, and accountability. However, identifying these values in research papers is usually performed manually and is time-consuming.

This project presents an **automatic pipeline for detecting moral values in scientific research papers** using Natural Language Processing (NLP) and transformer-based language models. The system processes PDF documents, extracts textual content, and predicts the presence of predefined moral values at scale.

---

## Moral Values
The project is based on **16 moral values** originally defined and used in prior research (Birhane et al., 2022; Nauta et al., 2023):

- Interpretable (to users)
- Transparent (to users)
- Privacy
- Fairness
- Not socially biased
- User influence
- Collective influence
- Deferral to humans
- Critiqability
- Beneficence
- Non-maleficence
- Justice
- Respect for Persons
- Autonomy (power to decide)
- Explicability
- Respect for Law and public interest

---

## Datasets

### Seed Papers (Training Set)
- **99 research papers**
- Manually annotated using the 16 moral values
- Annotations originate from *Birhane et al. (2022)*
- PDFs were downloaded and verified manually
- Used as the training and validation dataset

### All Papers (Testing Set)
- **~2,300 research papers**
- Extracted from **DBLP conference population data**
- Conferences: **NeurIPS and ICML**
- Years: **2008, 2009, 2018, 2019**
- PDFs were automatically downloaded via web scraping

---

## Pipeline

1. **PDF Collection**
   - Manual download for seed papers
   - Automated web scraping for DBLP conference papers

2. **Text Extraction**
   - PDF text extracted using `pypdf`
   - Full document text stored in JSON format

3. **Initial Annotation (Zero-Shot)**
   - Model: `roberta-large-mnli`
   - Zero-shot classification used to create initial moral value labels
   - Output saved as structured JSON files

4. **Supervised Model Training**
   - Model: `roberta-base`
   - Task: Multi-label classification
   - Loss: Binary Cross-Entropy with class weighting
   - Training on annotated seed papers

5. **Prediction & Analysis**
   - Model applied to all papers
   - Per-paper and per-value predictions generated
   - Confusion matrices and evaluation metrics computed

---

## Models Used

| Task | Model |
|-----|------|
| Zero-shot annotation | `roberta-large-mnli` |
| Moral value detection | `roberta-base` |
| Framework | Hugging Face Transformers |

---

## Evaluation
The model is evaluated using:

- Micro F1-score
- Macro F1-score
- Precision
- Recall
- Confusion matrices (per value and binary moral vs non-moral)

---

## Results Summary
- Successfully processed **over 2,300 research papers**
- Automatically detected moral values at scale
- Demonstrated feasibility of replacing manual annotation with NLP models
- Provided structured moral value insights across large academic corpora

---

## Future Work
- Introduce human validation studies to assess annotation quality
- Extend moral values to IR-style themes (ethics, social impact, governance)
- Apply chunk-based document classification for improved coverage
- Integrate retrieval-based evaluation (BM25, dense retrieval, reranking)

---

## References
- Birhane, A. et al. (2022). *The Values Encoded in Machine Learning Research*
- Nauta, P. et al. (2025). *Large Language Models Meet Moral Values*

---

## Repository Structure
├── seed_papers/
├── all_papers/
├── json_seed/
├── json_all/
├── training/
├── evaluation/
├── outputs/
