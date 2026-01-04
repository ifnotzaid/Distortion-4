# RU → EN Machine Translation Baselines (7 Models)

This repo contains a mini MT project comparing **seven RU→EN translation approaches**, ranging from classic statistical baselines to large pretrained “beast” transformers.  
We train/evaluate models, report **BLEU on dev/test**, and run the same **3 demo sentences** across all systems for qualitative comparison.

---

## Dataset

We use **OPUS-100 (en-ru)** from Hugging Face (`Helsinki-NLP/opus-100`, config `en-ru`).

- **Train:** up to 1,000,000 sentence pairs (we typically subsample for faster experiments, e.g., 20k–50k)
- **Validation (dev):** 2,000 sentence pairs
- **Test:** 2,000 sentence pairs
- Language direction: **Russian (ru) → English (en)**

> Tokenization and filtering vary by model (simple word tokenization for IBM/word-based baselines; SentencePiece/BPE for neural models).

---

## Evaluation

We evaluate using **BLEU** (via `sacrebleu`), reported on:
- **Dev BLEU**
- **Test BLEU**

We also translate a shared set of **3 demo sentences** at the end of each run:
```python
examples_ru = [
  "я люблю машинное обучение",
  "сегодня погода очень хорошая, но немного холодно",
  "пожалуйста, скажи мне где находится ближайшая станция метро"
]
