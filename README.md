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

Bar Charts
<img width="800" height="600" alt="bars" src="https://github.com/user-attachments/assets/7e01323f-7fc3-4ec3-b994-daceccd59a02" />


Training vs Validation Accuracy
<img width="1189" height="490" alt="image" src="https://github.com/user-attachments/assets/21f29d82-a453-440e-b16b-1da14140e48e" />

