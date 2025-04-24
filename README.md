# Emotion-Recognition-System

# Emotion Recognition using MFCC and Prosody Features

## Overview
This project develops a machine learning system for accurately recognizing human emotions from speech signals using the EmoDB (German emotional speech corpus) dataset. The system leverages multi-level acoustic features extracted at utterance, word, and syllable levels to classify speech into seven distinct emotional states: anger, boredom, anxiety, happiness, sadness, disgust, and neutral.

## Dataset
- **EmoDB**: German emotional speech corpus with 535 utterances at 16kHz sampling rate
- Contains 7 emotions: anger, boredom, anxiety, happiness, sadness, disgust, and neutral
- 10 different sentences spoken by professional actors expressing various emotions

## Feature Extraction
Our approach extracts two primary types of features:

### MFCC Features
- Mel-Frequency Cepstral Coefficients capture the spectral envelope of speech signals based on human auditory perception
- MFCCs represent the short-term power spectrum, providing crucial information about vocal tract configuration
- Extraction process:
  - Framing & Windowing – Dividing the signal into short frames with a Hamming window
  - Fourier Transform – Converting each frame from time domain to frequency domain
  - Mel-Scale Filtering – Applying a filter bank to emphasize frequencies perceived by human hearing
  - Logarithm & DCT – Taking the log of filter bank energies and applying Discrete Cosine Transform
  - Feature Aggregation – Extracting MFCCs at word, syllable, and utterance levels

### Prosodic Features
- Include pitch (F0), energy, duration, and rhythm patterns in speech
- Convey emotional information through variations in speaking rate, stress patterns, and intonation
- Extracted at three linguistic levels:
  1. **Word Level**: Features extracted for each word in the utterance
  2. **Syllable Level**: Words segmented into syllables using phonetic properties
  3. **Utterance Level**: Global-level statistics over the entire utterance (mean, variance, skewness)

## Model Architecture
We implemented multiple machine learning approaches:

### Machine Learning Models
- **Support Vector Machine (SVM)**: Tuned with grid search; best performance on MFCC features
- **Gaussian Mixture Model (GMM)**: Baseline probabilistic model; underperformed overall
- **Multi-Layer Perceptron (MLP)**: Fully connected feedforward network with dropout
- **XGBoost & LightGBM**: Gradient boosting models for structured/tabular features

### Deep Learning Models
- **Multi-Branch Neural Network (MBNN)**:
  - Independent models trained on each feature type:
    - MFCC Branch
    - Word-Level Prosody Branch
    - Syllable-Level Prosody Branch
    - Utterance-Level Prosody Branch

### Ensemble Methods
- **Feature-Level Ensemble Voting**: Combined multiple models (SVM, MLP, XGBoost, LightGBM) trained on the same feature set
- **Global Ensemble Voting**: Combined predictions from MFCC, word, syllable, and utterance ensemble models

## Results
- **MFCC Features** provided the best overall performance across most models
- **Word-Level Prosody** gave moderate individual performance, improved significantly with ensemble
- **Syllable-Level Prosody** showed limited standalone performance but improved through ensemble learning
- **Utterance-Level Prosody** was the least effective across models
- **Ensemble Voting** consistently achieved the highest accuracy

## Spectrogram Analysis
We analyzed spectrograms and pitch patterns across different emotions:

| Emotion | Gender | Pitch Characteristics | Spectrogram Appearance |
|---------|--------|----------------------|------------------------|
| Angry | Male | High | Bright, dense, sharp edges, forceful transitions |
| Angry | Female | Very high | Brighter, more pitch variation, sharper changes |
| Boredom | Male | Low, monotone | Dim, flat, low variation |
| Boredom | Female | Low-moderate | Slightly higher pitch, flat patterns |
| Disgust | Male | Irregular | Patchy brightness, rough transitions |
| Disgust | Female | Irregular, higher | Uneven spectrogram, more pitch fluctuation |
| Fear/Anxiety | Male | Shaky, high-moderate | Jittery bursts, irregular pitch patterns |
| Fear/Anxiety | Female | Very high & shaky | Tremble-like patterns, sharper intensity variations |
| Happy | Male | Varied, high-moderate | Rhythmic, melodic, bright |
| Happy | Female | High & sing-songy | Very melodic, fast rising/falling pitch |
| Sad | Male | Low & flat | Dim, slow pitch movement |
| Sad | Female | Low-moderate, flatter | Minimal pitch movement |
| Neutral | Male | Mid-low | Smooth, even tone, low variation |
| Neutral | Female | Mid | Slightly higher pitch, consistent transitions |

## Key Takeaways
- MFCC features were the most consistent and effective across all models
- Prosody features at word and syllable levels revealed valuable rhythmic and stress-based emotional cues
- Utterance-level prosody failed to capture finer emotional transitions
- Emotional signals are often embedded in short-term speech patterns
- Feature granularity matters: emotion is more detectable at word/syllable scale than at sentence scale
- Statistical analysis (Friedman Test) confirmed that feature type significantly affects model performance (P-value: 0.0047)

## Project Timeline
- Initial implementation focused on feature extraction and basic models (SVM, GMM, MLP)
- Post-evaluation improvements included:
  - Separate feature sets for MFCC and prosody at different levels
  - Switching from zero-padding to mean-based resampling
  - Adding XGBoost and LightGBM models
  - Implementing ensemble voting methods
  - Developing multi-branch neural networks

## References
- "Speech Emotion Recognition: Features, Classification Models, and Databases" - Zheng, Z., Zhang, Y., & Yu, H. (2019)
- "Extraction and Representation of Prosodic Features for Language and Speaker Recognition" - Leena Mary & B. Yegnanarayana, IIT Madras
- "Deep Learning for Audio-Based Emotion Recognition: A Review" - Trigeorgis, G., Ringeval, F., & Schuller, B. (2018)
- "Analyzing the Impact of Prosodic Feature (Pitch) on Learning Classifiers for Speech Emotion Corpus" - Syed Abbas Ali, Anas Khan, & Nazia Bashir (NED University)

## Team
- Vedant Nipane (2021102040)
- Himanshu Gupta (2022102002)
