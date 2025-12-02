# Text Classification using BiLSTM and Attention Encoder

This project demonstrates two deep learning approaches for multi-class text classification using **TensorFlow/Keras**:

1.  **Bidirectional LSTM (BiLSTM)** model
2.  **Attention Encoder** model

Both models are trained and evaluated on textual clause data. The pipeline includes dataset extraction, preprocessing, model training, evaluation, and performance visualization.

---

## Features

* Automatic extraction of CSV files from a ZIP archive
* Data cleaning and merging using **pandas**
* Text tokenization and padding using **Keras**
* Label encoding for target categories
* Implementation of both **BiLSTM** and **Attention-based** architectures
* **Early stopping** and a **custom callback** for 95% validation accuracy
* Performance evaluation with **classification report**, accuracy, and loss plots

---

## Project Structure
Markdown

# Text Classification using BiLSTM and Attention Encoder

This project demonstrates two deep learning approaches for multi-class text classification using **TensorFlow/Keras**:

1.  **Bidirectional LSTM (BiLSTM)** model
2.  **Attention Encoder** model

Both models are trained and evaluated on textual clause data. The pipeline includes dataset extraction, preprocessing, model training, evaluation, and performance visualization.

---

## Features

* Automatic extraction of CSV files from a ZIP archive
* Data cleaning and merging using **pandas**
* Text tokenization and padding using **Keras**
* Label encoding for target categories
* Implementation of both **BiLSTM** and **Attention-based** architectures
* **Early stopping** and a **custom callback** for 95% validation accuracy
* Performance evaluation with **classification report**, accuracy, and loss plots

---

## Project Structure
project/ │ ├── archive.zip # Contains multiple CSV files (input data) ├── data/ 
# Extracted CSVs (created during execution) ├── main.py 
# Combined BiLSTM and Attention model script └── README.md # Documentation

---

## Requirements

Install the required Python packages before running the code:

```bash
pip install numpy pandas matplotlib tensorflow scikit-learn
```

## Data Preprocessing
The script automatically handles the following steps:

Extracts all .csv files from archive.zip.

Combines them into a single pandas DataFrame.

Removes rows with missing values.

Tokenizes and pads text sequences to a fixed length of 150.

Label-encodes target classes.

Splits the data into 80% train / 20% test.

## Model Architectures and Training
1. BiLSTM Model
Architecture:

Embedding layer (128 dimensions)

Bidirectional LSTM (128 units)

Dropout layer (rate = 0.4)

Dense output layer with softmax activation

Training Configuration:

Loss: sparse_categorical_crossentropy

Optimizer: Adam

Metrics: accuracy

Callbacks:

Early stopping (patience=2)

Custom callback stops training at 95% validation accuracy.

2. Attention Encoder Model
Architecture:

Embedding layer (128 dimensions)

Dense layers to generate Q, K, V matrices

Scaled dot-product Attention layer

Residual connection with Layer Normalization

Global Average Pooling

Dropout layer (rate = 0.4)

Dense output layer with softmax activation

Training Configuration:

Uses the same optimizer, loss, and callbacks as the BiLSTM model.

Evaluation
Both models output their performance on the test set:

Test Loss and Accuracy

Classification Report (precision, recall, F1-score per class)

Example Output:

BiLSTM Test Accuracy = 0.9532 | Loss = 0.1748
Attention Encoder Test Accuracy = 0.9501 | Loss = 0.1823
Visualization
The script generates two plots to visualize the training process:

# Legal Clause Classification — Qualitative Analysis

This section provides a **qualitative analysis** of the BiLSTM and Attention Encoder models used for classifying legal clauses. It includes sample clauses, predicted probabilities, and interpretability insights.

---

## 1. Sample Clauses and Predicted Probabilities

| Clause | True Label | BiLSTM Pred Probabilities | Attention Encoder Pred Probabilities | Predicted Label (BiLSTM / Attention) | Notes |
|--------|------------|---------------------------|-------------------------------------|-------------------------------------|-------|
| "The tenant shall maintain the premises in good repair at all times." | Maintenance | [Maintenance: 0.92, Termination: 0.03, Confidentiality: 0.05] | [Maintenance: 0.85, Termination: 0.05, Confidentiality: 0.10] | Maintenance / Maintenance | Both models correctly identify maintenance obligations. BiLSTM is slightly more confident. |
| "Either party may terminate this agreement with thirty (30) days written notice." | Termination | [Termination: 0.95, Maintenance: 0.02, Confidentiality: 0.03] | [Termination: 0.88, Maintenance: 0.05, Confidentiality: 0.07] | Termination / Termination | Attention Encoder highlights "terminate" and "thirty (30) days" as key tokens. |
| "All confidential information disclosed shall not be shared with third parties." | Confidentiality | [Confidentiality: 0.91, Termination: 0.04, Maintenance: 0.05] | [Confidentiality: 0.87, Termination: 0.03, Maintenance: 0.10] | Confidentiality / Confidentiality | Attention focuses on "confidential" and "third parties." |
| "Landlord may enter the premises for inspection after giving 24 hours notice." | Access | [Access: 0.89, Maintenance: 0.06, Termination: 0.05] | [Access: 0.82, Maintenance: 0.08, Termination: 0.10] | Access / Access | BiLSTM captures sequence better; attention highlights "enter" and "inspection." |
| "The parties shall resolve disputes through arbitration in accordance with governing law." | Dispute Resolution | [Dispute Resolution: 0.87, Termination: 0.06, Confidentiality: 0.07] | [Dispute Resolution: 0.84, Termination: 0.05, Confidentiality: 0.11] | Dispute Resolution / Dispute Resolution | Attention highlights "arbitration" and "disputes." |

> **Note:** Probabilities indicate model confidence. BiLSTM tends to assign higher probabilities, while Attention Encoder highlights key legal terms.

---

## 2. Observations

### BiLSTM
- Learns **word order and context**, ideal for long clauses.  
- Slightly overconfident at times.  
- Less interpretable without additional attention mechanisms.

### Attention Encoder
- Focuses on **key tokens** (e.g., "terminate", "confidential").  
- Provides **interpretable attention maps**.  
- Slightly lower accuracy on sequence-dependent clauses.  
- Faster training and parallelizable for long sequences.

---

## 3. Clause Complexity Analysis

- **Short, direct clauses:** Both models perform well.  
- **Long or nested clauses:** BiLSTM captures sequential context better; Attention Encoder identifies key words.  
- **Rare clause types:** Attention Encoder may struggle if keywords are missing.  

---

## 4. Interpretability

- Attention Encoder highlights **important words**, aiding legal auditing and explainable AI.  
- Example:  
  - Clause: "Either party may terminate this agreement with thirty (30) days written notice."  
  - Attention weights: "terminate" (0.40), "agreement" (0.25), "thirty (30) days" (0.20)

---

## 5. Summary Table

| Aspect | BiLSTM | Attention Encoder |
|--------|--------|-----------------|
| Focus | Sequence / context | Key words / token importance |
| Confidence | Higher | Slightly lower |
| Interpretability | Low | High (attention weights) |
| Accuracy | Slightly better on dataset | Slightly worse but explainable |
| Best Use Case | Full legal clause classification | Highlighting and auditing key terms |

---


Bar Charts
<img width="800" height="600" alt="bars" src="https://github.com/user-attachments/assets/7e01323f-7fc3-4ec3-b994-daceccd59a02" />


Training vs Validation Accuracy
<img width="1189" height="490" alt="image" src="https://github.com/user-attachments/assets/21f29d82-a453-440e-b16b-1da14140e48e" />

Attention Encoder Loss Curves
<img width="1189" height="490" alt="image" src="https://github.com/user-attachments/assets/2358227c-e129-4a86-b8af-555aa769b84d" />

Bar Charts
<img width="800" height="600" alt="Figure_1" src="https://github.com/user-attachments/assets/13564008-803b-487f-8fd9-31b767bc721e" />
