Auto-i3rab: Arabic Diacritical Mark Prediction Using Joint Hidden Markov Models

A computational linguistics research project investigating how part-of-speech (POS) information can improve the prediction of Arabic word-ending diacritical marks through a two-layer Hidden Markov Model (HMM) and modified Viterbi decoding algorithm.

Key result: Achieved 81.44% test accuracy, improving upon a standalone word–mark HMM baseline of 78.80%, while increasing unseen-word accuracy from 22.58% to 32.25%.

Project Overview

Arabic text frequently omits diacritical marks that encode grammatical and morphological information. These omissions introduce ambiguity for natural language processing systems, particularly when interpreting Modern Standard Arabic (MSA).

This project investigates whether incorporating grammatical context through POS tagging improves the prediction of word-ending diacritical marks, known as i’rab.

The proposed approach combines two probabilistic sequence models through a joint Viterbi decoding framework.

Model Architecture

The system consists of three main components:

1. Part-of-Speech HMM

A Hidden Markov Model trained on word–POS sequences from the Kalimat Multicorpus dataset.

* Estimates initial, transition, and emission probabilities.
* Uses add-k smoothing to handle sparse observations.
* Implements Viterbi decoding in log-space.
* Handles unseen words through an unknown-token probability.
* Achieved 92% POS-tagging accuracy on the test set.

2. Word–Mark HMM

A second Hidden Markov Model trained on diacritized Arabic text derived from the Tashkeela corpus.

* Extracts word-ending diacritical marks through a custom preprocessing pipeline.
* Models nine possible ending-mark states, including the absence of a mark.
* Learns word–mark emission and mark-transition probabilities.
* Establishes a baseline test accuracy of 78.80%.

3. Joint Viterbi Decoder

The final model combines lexical and POS-based information to predict the most likely sequence of ending diacritical marks.

The modified decoder uses a weighted emission score:

[
S(m) = \alpha \log P(w \mid m) +
(1-\alpha)\log P(m \mid POS)
]

where:

* (w) represents the observed word.
* (m) represents a candidate ending diacritical mark.
* (POS) represents the predicted part-of-speech tag.
* (\alpha) controls the relative contribution of lexical and grammatical information.

The decoder incorporates mark-transition probabilities and uses dynamic programming with backtracking to recover the highest-scoring sequence.

Experimental Results

The joint model was evaluated against the standalone word–mark HMM baseline.

Metric	Baseline HMM	Joint HMM (α = 0.6)
Test accuracy	78.80%	81.44%
Known-word accuracy	80.22%	82.70%
Unknown-word accuracy	22.58%	32.25%
Macro F1	62.50%	68.28%

The joint model improved overall test accuracy by 2.64 percentage points and unknown-word accuracy by 9.67 percentage points.

Experiments also demonstrated the importance of tuning the weighting parameter. Over-reliance on POS information reduced accuracy, while balancing POS context with lexical information improved prediction performance.

Implementation

The project was implemented in Python using custom probabilistic sequence modeling algorithms.

Core technologies:

* Python and Jupyter Notebook
* NumPy
* scikit-learn
* Matplotlib
* NetworkX
* Regular expressions and Unicode text processing

Technical methods:

* Hidden Markov Models
* Viterbi decoding and dynamic programming
* Log-space probability calculations
* Add-k probability smoothing
* Unknown-word handling
* Hyperparameter experimentation
* Accuracy, F1, and confusion-matrix evaluation

Datasets

Two Arabic corpora were used:

Kalimat Multicorpus: POS-annotated Arabic news text used to train the initial POS-tagging model.

Arabic Text Diacritization Dataset (derived from Tashkeela): Fully diacritized Arabic text used to construct the word–mark prediction model.

Separate preprocessing pipelines were developed to normalize the data and construct the required sentence-level representations.

Repository Structure

AUTO_I3RAB/
├── Ayaat_JP_Code.ipynb
├── Datasets/
├── JP_Variables/
├── .gitattributes
└── README.md

The main notebook contains the experimental implementation, including preprocessing, probabilistic modeling, decoding, and evaluation.

Limitations and Future Work

The primary limitation is the lack of a sufficiently large corpus containing both POS annotations and full diacritization. Consequently, predicted POS labels were used to construct the joint training data, potentially introducing error propagation.

Potential improvements include:

* Developing a jointly annotated corpus.
* Incorporating morphological features.
* Improving unseen-word handling.
* Comparing probabilistic models with neural sequence architectures.
* Refactoring the experimental implementation into reusable software modules.

Research Context

Developed as an independent research project at Princeton University.

Researcher: Ayaat Al-Yasseri

Advisers: Christiane Fellbaum and Mounia Mnouer

Research report: Auto-i3rab: Using a Joint Hidden Markov Model to Predict Ending Diacritical Marks in Arabic Text (2026).
