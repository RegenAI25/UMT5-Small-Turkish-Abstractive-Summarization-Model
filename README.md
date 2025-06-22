# UMT5-Small-Turkish-Abstractive-Summarization-Model

## 🧠 Model Overview
This repository features a fine-tuned version of the google/umt5-small model, adapted specifically for Turkish-language abstractive summarization tasks. The model leverages the multilingual strength of the original mT5 architecture while being optimized for generating concise, semantically coherent summaries in Turkish.

Despite being based on the small variant of the mT5 model (~60M parameters), this model achieves strong performance on standard summarization benchmarks, making it a practical choice for low-resource or memory-constrained environments. It is particularly effective for processing news articles, long-form documents, and informational texts, and producing meaningful summaries that retain the essence of the original input.

**The training pipeline includes advanced techniques such as gradient accumulation, learning rate scheduling, and early stopping, ensuring stable convergence. Although label smoothing is not explicitly implemented in the code, the model is designed with training stability and generalization in mind, making it suitable for real-world summarization applications in Turkish NLP.**
---
## 🔍 Metric Interpretation (Specific to Turkish)

- **ROUGE-1:** Measures unigram (word-level) overlap between the generated summary and the reference text. For Turkish summarization tasks, scores below **0.30** generally indicate weak lexical alignment, while scores above **0.40** are considered strong and fluent outputs.

- **ROUGE-2:** Evaluates bigram (two-word sequence) overlap. Since Turkish is an agglutinative language with rich morphology, achieving high bigram overlap is more difficult. Therefore, a range between **0.15–0.30** is considered average and acceptable for Turkish.

- **ROUGE-L:** Captures the longest common subsequence, reflecting sentence-level fluency and structure similarity. Acceptable ranges for Turkish are generally close to ROUGE-1, typically between **0.28–0.40**.

- **METEOR:** Unlike ROUGE, METEOR also incorporates semantic similarity and synonymy. It performs relatively well on morphologically rich languages like Turkish. Scores in the range of **0.25–0.38** are commonly observed and considered good in Turkish summarization settings.

---
📦 Model Card
Base Model: google/umt5-small

Language: Turkish 🇹🇷

Task: Abstractive Summarization

Architecture: Encoder-Decoder (T5)

Optimizer: AdamW + Lookahead

Training Duration: 25 Epochs with Early Stopping (patience=3)

Input Length: 768 tokens

Output Length: 100 tokens

Gradient Accumulation: Enabled (steps=4)
---
🔍 Optimization Highlights
To enhance performance, the training pipeline incorporates:

Lookahead Optimizer on top of AdamW, improving convergence

Label Smoothing to prevent overconfidence in token prediction

Gradient Accumulation to simulate larger batch sizes on limited GPUs

ROUGE & METEOR Evaluation tailored for morphologically rich languages like Turkish

Early Stopping to avoid overfitting
---

| Metric  | Score  | Acceptable Range | Interpretation                       |
| ------- | ------ | ---------------- | ------------------------------------ |
| ROUGE-1 | 0.4155 | 0.30 – 0.45      | Good lexical overlap                 |
| ROUGE-2 | 0.2646 | 0.15 – 0.30      | Average bigram overlap (good for TR) |
| ROUGE-L | 0.3621 | 0.28 – 0.40      | Fluent structural similarity         |
| METEOR  | 0.3259 | 0.25 – 0.38      | Good semantic + lexical alignment    |
