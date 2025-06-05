# Music Genre Classification: Combining Lyrics and Audio Features

## Project Overview

This project aims to classify music genres by analyzing song lyrics and audio features. We believe that music genre classification is a multimodal task, and integrating the semantic information from lyrics with the acoustic characteristics from audio helps to build more accurate and comprehensive classification models.

## Data and Preprocessing

We used a dataset from Kaggle, which includes song lyrics and audio features obtained from Spotify. The dataset covers six music genres: Rap, EDM, Pop, Rock, Latin, and R&B.

The data underwent a series of preprocessing steps, including cleaning, encoding, feature selection, splitting, and standardization, to ensure data quality and suitability for model training.

## Model Introduction

We implemented and evaluated various models to explore the performance of different modalities and architectures in music genre classification:

* **MLP (Multi-Layer Perceptron) Based on Audio Features**: This is our audio baseline model, using structured audio features to capture the sonic style signals of a song to predict its genre.
* **CNN (Convolutional Neural Network) Based on Lyrics**: This is our lyrics baseline model, utilizing a multi-scale 1D CNN to extract linguistic patterns from lyrics, capturing local semantic patterns.
* **CNN+MLP Fusion Model**: This model combines the representations from lyrics (CNN) and audio (MLP). It leverages the complementary information from both modalities through feature concatenation and joint learning to improve classification performance.
* **Attention BiLSTM (Bidirectional Long Short-Term Memory) Model**: This model uses a bidirectional LSTM and an attention mechanism to process lyrics, better capturing sequential and contextual dependencies within the lyrics, and combines this with audio features for prediction.
* **GRU (Gated Recurrent Unit) + Cross Attention Model**: This model efficiently encodes lyrics using a GRU and employs a cross-attention mechanism where audio features guide the focus over the encoded lyrics, enabling dynamic interaction between modalities. Additionally, it incorporates artist embeddings to provide extra stylistic information.
* **BERT (Bidirectional Encoder Representations from Transformers) - Chunked Lyrics**: We explored BERT as both a standalone and a hybrid classifier. Due to BERT's input length limitations, lyrics were split into overlapping chunks for processing, with BERT aiming to capture deep semantic meaning from the lyrics. Its output can be further combined with audio features and classified using an MLP or Random Forest.
* **Transformer + MLP Model**: This model combines a Transformer to handle long-range dependencies in lyrics with an MLP to process numerical and dummy variables (like audio features). The outputs from both architectures are concatenated for final classification.
* **Ensemble (Majority Vote) Model**: This is our final model, which combines the predictions from all the preceding models using a majority voting scheme. This strategy aims to mitigate individual model biases and enhance the overall reliability and accuracy of the classification.
