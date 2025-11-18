#  Bangla Dialect ASR System | শব্দতরী Competition (Televerse 1.0 - CUET)

This repository contains our submission pipeline for the Kaggle-hosted **শব্দতরী** competition, where the goal is to develop an **automatic speech recognition (ASR)** system that transcribes dialectal Bangladeshi speech into formal standard Bangla.

---

## 🏁 Competition Overview

- **Host**: Department of ETE, CUET (Televerse 1.0)
- **Challenge**: Build an ASR model that accurately transcribes 3,800+ dialectal Bangla audio recordings (across 20 regions) into standardized Bangla text.
- **Evaluation Metric**: **Normalized Levenshtein Similarity** between predicted and ground-truth transcriptions.
- **Submission Format**: `.csv` with `audio,text` columns for 500 test samples.
- **Restrictions**:
  - ❌ No API-based models (e.g. Whisper API, OpenAI, Google, etc.)
  - ❌ No manual transcription or use of closed-source models
  - ✅ Only open-source, locally executed models are allowed

---

## 🧠 Methodology

### 1. **Base ASR: Fine-Tuned Whisper-Small**
- Open-source model from Hugging Face: `openai/whisper-small`
- Fine-tuned locally on the 3,350 provided dialectal samples using region-tagged annotations
- Trained for 4 epochs using CTC loss on Mel spectrograms

### 2. **Post-Processing: BanglaT5 Sequence-to-Sequence**
- Model: `csebuetnlp/banglat5_base` (optionally `banglat5_small`)
- Task: Correct grammar, syntax, and morphological inconsistencies in Whisper outputs
- Trained on pairs of `(raw ASR output, normalized Bangla sentence)` using noisy supervision
- Metric-guided fine-tuning (WER + NLS), early stopping, and label smoothing used

---

## 📂 Folder Structure

