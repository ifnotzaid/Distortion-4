# RU → EN Machine Translation (NLP Project) 🇷🇺➡️🇬🇧✨

This repo compares **7 different machine translation approaches** on a **Russian→English** task, ranging from classic statistical baselines to strong pretrained Transformer models.

---

## 📦 Dataset

We used **OPUS-100 (en-ru)** from Hugging Face (`Helsinki-NLP/opus-100`, config `en-ru`).

**Splits**
- **Train**: used for learning model parameters
- **Dev/Validation**: used for tuning + checking progress during training
- **Test**: final evaluation only (no training/tuning on it)

**Preprocessing (common)**
- Lowercasing + tokenization
- Sentence length filtering (e.g., 1–40 tokens for some baselines to keep training fast/stable)
- BLEU used as the main metric 🧪

---

## 🧠 Models (7 total)

### 1) Word-to-Word Co-occurrence Baseline 🧱
A very simple dictionary baseline:
- For each RU token, choose the most frequent EN token that appears with it in paired sentences.
- No alignment, no phrases, no reordering → very weak but useful as a “floor” baseline.

---

### 2) IBM Model 1 (EM) 📊
Classic statistical MT model trained with EM:
- Learns word translation probabilities **t(e|f)**.
- Includes special tokens like `<NULL>` (to generate extra words not aligned to any source word) and `<UNK>` for unseen vocabulary.
- Stronger than word-to-word, still limited (no phrase modeling, weak fluency).

---

### 3) Seq2Seq RNN + Bahdanau Attention 🔁🎯
A neural baseline built from scratch:
- Encoder–decoder RNN with attention over source tokens.
- Can learn soft alignments, but typically underperforms Transformers on large-scale MT.
- Good “classic NMT” baseline for comparison.

---

### 4) mT5 Fine-tuned 🧩🌍
We fine-tuned **google/mt5-small** for RU→EN:
- mT5 is a multilingual **text-to-text** model (not translation-only).
- Works reasonably after fine-tuning, but not as strong as translation-specialized models on this task.

---

### 5) MarianMT Fine-tuned 🚀
We fine-tuned a Marian (Transformer) translation model:
- Marian is designed for MT and usually learns faster + stronger than RNN baselines.
- Produces fluent translations after fine-tuning and achieves solid BLEU.

---

### 6) NLLB (Pretrained “Beast” Model) 🦁
We evaluated a pretrained **NLLB** RU→EN model:
- Large multilingual translation-focused Transformer.
- Strong quality without task-specific training (or with minimal setup).
- Very good generalization and robustness.

---

### 7) WMT19 RU→EN (facebook/wmt19-ru-en) 🏆
Our strongest model in this project:
- Transformer trained specifically for WMT RU→EN.
- Achieved the best BLEU among tested models and produced very accurate demo translations.

---

## 📏 Evaluation

We report **BLEU** on:
- **Dev** (during training for checkpoints/progress)
- **Test** (final score)

BLEU measures n-gram overlap between model translations and reference translations:
- Higher BLEU = closer to references (generally better MT quality)
- BLEU is useful but not perfect (it can miss meaning/fluency edge cases)

---

## 🧪 Demo Sentences (Quick Qualitative Check)

We also tested each model on 3 fixed RU sentences to compare outputs qualitatively (fluency, word choice, coverage).

---
