# Swahili-English Machine Translation Using Seq2Seq

This task implements a Swahili-English neural machine translation (NMT) model using a Seq2Seq (Encoder-Decoder) architecture with LSTM. The dataset is sourced from various Swahili-English corpora, including Tatoeba. The model achieves moderate BLEU scores but exhibits low accuracy, indicating areas for improvement.

## Project Overview
- Implemented a Neural Machine Translation (NMT) model.
- Utilized a Seq2Seq framework with LSTM-based encoder and decoder.
- Trained on Swahili-English parallel sentence pairs.
- Evaluated using BLEU scores and accuracy metrics.

## Architecture
The model follows a standard Encoder-Decoder framework:

1. **Encoder**: A bidirectional LSTM processes the source sentence.
2. **Decoder**: A unidirectional LSTM generates the translation.
3. **Seq2Seq Coordination**:
  - Uses **Teacher Forcing** during training.
  - Decodes one word at a time during inference.

## Dataset
The dataset includes Swahili-English sentence pairs extracted from multiple sources:
- **Source Language**: Swahili (`swh`)
- **Target Language**: English (`eng`)
- **Total Sentences**: ~4,293
- **Filtered Dataset**: Kept sequences ≤10 words long.

### Preprocessing Steps:
- Tokenization using `nltk.tokenize.WordPunctTokenizer()`.
- Replaced rare words with `<unk>` token.
- Saved processed vocabulary for training.

## Training Process
- **Optimizer**: Adam (`lr=0.001`)
- **Loss Function**: CrossEntropyLoss
- **Batch Size**: 100
- **Epochs**: Early stopping used (~65 epochs max)
- **Training Speed**: GPU-enabled for acceleration.

### Loss History
The loss consistently decreased, indicating model learning.

### Evaluation Metrics
The model was evaluated using:
- **BLEU (Bilingual Evaluation Understudy)**: Measures n-gram overlap between predictions and references.
- **Accuracy**: Percentage of exact matches (low in this case).

### Final Scores
```
BLEU-1: 0.2371
BLEU-2: 0.0819
BLEU-3: 0.0421
BLEU-4: 0.0242
Accuracy: 0.0062
```
- BLEU-1 score is reasonable, but BLEU-4 is quite low.
- Accuracy remains close to 0, indicating that exact word-for-word translations are rarely correct.

## **Example Translations**
The model struggles with semantic accuracy, as shown in the examples below:

```
Source: "i have absolutely no clue."
Reference: "sina habari kamwe."
Translation: "tutaishughulikia."

Source: "only the paranoid survive."
Reference: "wale wenye wasiwasi ndio huishi."
Translation: "ilifanyika."

Source: "my teacher is mrs. li."
Reference: "mwalimu wangu ni bi. li"
Translation: "rafiki yangu alinialika kwa chajio."

Source: "millie has blue eyes."
Reference: "millie ana macho ya bluu."
Translation: "millie ana macho ya kijani."

Source: "he comes from wales."
Reference: "anatoka welisi."
Translation: "anatoka genova."
```
- Some translations are **completely unrelated** (e.g., *"only the paranoid survive." → "ilifanyika."*).
- The model **fails to generalize well** to unseen sentence structures.
- Common errors include **hallucinations** (producing sentences that are grammatically correct but unrelated to input).

## Issues & Limitations

1. Low Translation Accuracy:
   - Many translations are **grammatically incorrect** or **unrelated**.
   - Possible causes:
     - **Insufficient training data** (~4k sentences may be too few).
     - **Lack of an Attention mechanism** for proper context alignment.

2. **Early Stopping**:
   - The model stopped after ~65 epochs due to BLEU stagnation.
   - Training longer without structural improvements may not help.

3. **Potential Overfitting**:
   - Loss is low, but BLEU scores remain limited.
   - The model **memorizes training data** rather than generalizing well.

## Possible Improvements
- **Implement Attention Mechanism** (Bahdanau, Luong) for better alignment.
- **Increase dataset size** using additional Swahili-English corpora.
- **Use pre-trained word embeddings** (e.g., FastText, Word2Vec) to improve generalization.
- **Hyperparameter tuning** (dropout, learning rate scheduling).
- **Try Transformer models** (e.g., MarianMT, mBART) instead of LSTMs.

## Next Steps
1. Implement **Attention** for better sequence alignment.
2. Expand dataset with **additional corpora**.
3. Experiment with **Transformer-based models**.

## Contact

For any questions or collaboration opportunities, feel free to reach out at [hey@njoguevans.me](mailto:hey@njoguevans.me).
