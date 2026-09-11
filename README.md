# 🌍 NLLB Multilingual Customer-Support Translation System

> 🤖 An inference-based NLP translation pipeline for multilingual customer-support messages using the pretrained **`facebook/nllb-200-distilled-600M`** Transformer model.

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue?logo=python)](https://www.python.org/)
[![PyTorch](https://img.shields.io/badge/PyTorch-Deep%20Learning-ee4c2c?logo=pytorch)](https://pytorch.org/)
[![Hugging Face](https://img.shields.io/badge/Hugging%20Face-NLLB--200-yellow?logo=huggingface)](https://huggingface.co/facebook/nllb-200-distilled-600M)
[![NLP](https://img.shields.io/badge/Domain-NLP-green)](https://en.wikipedia.org/wiki/Natural_language_processing)

## ✨ Overview

This project implements a multilingual customer-support translation pipeline designed for **support tickets, chat messages, and emails**.

The system uses the pretrained **NLLB-200 distilled 600M** sequence-to-sequence Transformer and combines it with:

- 🔎 Automatic source-language detection
- 🧹 Input validation and cleaning
- 🔐 Protection of technical/non-translatable terms
- 🔤 NLLB/FLORES-200 language-code mapping
- 🧠 Transformer encoder-decoder inference
- 🎯 Forced target-language decoding
- 🚀 Beam-search generation
- 📦 Efficient batch translation
- 📊 BLEU and chrF evaluation
- 🧪 Optional COMET evaluation
- 🛡️ Handling of URLs, emails, error codes, product IDs/SKUs, tags, emojis, typos, and code-switched text
- 🧾 Structured translation metadata and latency reporting

The primary goal is to preserve **intent, sentiment, urgency, and technical accuracy** while translating multilingual support content.

## 🌐 Supported Languages

| Language | ISO-639-1 | NLLB / FLORES-200 code |
|---|---|---|
| 🇺🇸 English | `en` | `eng_Latn` |
| 🇫🇷 French | `fr` | `fra_Latn` |
| 🇪🇸 Spanish | `es` | `spa_Latn` |
| 🇮🇳 Hindi | `hi` | `hin_Deva` |
| 🇮🇳 Tamil | `ta` | `tam_Taml` |

### 🔄 Supported Translation Directions

- 🇺🇸 English ↔ 🇫🇷 French
- 🇺🇸 English ↔ 🇪🇸 Spanish
- 🇺🇸 English ↔ 🇮🇳 Hindi
- 🇺🇸 English ↔ 🇮🇳 Tamil

## 🏗️ Architecture

```text
Customer Support Message
          │
          ▼
┌──────────────────────────┐
│  1. Input Validation     │
└────────────┬─────────────┘
             ▼
┌──────────────────────────┐
│  2. Language Detection   │
│     langdetect           │
└────────────┬─────────────┘
             ▼
┌──────────────────────────┐
│  3. Language Code Mapping│
│     ISO → NLLB/FLORES    │
└────────────┬─────────────┘
             ▼
┌──────────────────────────┐
│  4. Term Protection      │
│ URLs • Emails • IDs      │
│ Error Codes • SKUs       │
└────────────┬─────────────┘
             ▼
┌──────────────────────────┐
│  5. SentencePiece        │
│     Tokenization         │
└────────────┬─────────────┘
             ▼
┌──────────────────────────┐
│  6. NLLB Transformer     │
│     Encoder → Decoder    │
│     Beam Search          │
└────────────┬─────────────┘
             ▼
┌──────────────────────────┐
│  7. Post-Processing      │
│ Restore Terms + Cleanup  │
└────────────┬─────────────┘
             ▼
      🌍 Translation Output
