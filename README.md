# Negation-Aligned Scorer (NAS): Hybrid Semantic Similarity Framework

## 🧠 Project Overview

This project addresses a critical limitation in Auto-Evaluation Systems (AES) used in education: the inability of existing Sentence Similarity Tools (SSTs) to accurately handle negation in student responses. With UNESCO projecting a need for 44 million additional teachers by 2030 and teachers spending nearly half their time on non-teaching tasks, automated evaluation systems are essential—but they must be accurate.

Traditional SSTs using BERT, Sentence-BERT, and similar models struggle with negated sentences because their embeddings place negated and non-negated sentences too close together in representation space. For example, "The theory is applicable here" and "The theory is not applicable here" receive high similarity scores despite having opposite meanings, leading to unfair automated grading.

### The Negation Problem

Current embedding-based approaches fail to capture:
- **Positional impact**: "The system is not entirely stable" vs "The system is entirely not stable"
- **Frequency effects**: Odd counts of negation words reverse meaning, even counts may neutralize it
- **Contextual nuances**: "The method is not accurate for extreme cases" vs "The method is not accurate"

## 🚀 Solution: Negation-Aligned Scorer (NAS)

The NAS model introduces a novel **Hybrid Semantic Similarity (HSS)** framework that combines:

### Phase 1: Shared Feature Extraction
- **Multi-Embedding Fusion**: Integrates four pretrained models (BERT, RoBERTa, Sentence-BERT, Word2Vec) to capture complementary semantic information
- **Siamese Architecture**: Both sentences pass through the same encoder for comparable representations
- **Bi-Directional LSTM**: Processes fused embeddings to capture sequential context and produce 256-dimensional semantic vectors

### Phase 2: Negation-Aligned Similarity Prediction
- **Negation Feature Engineering**: 9-dimensional handcrafted feature vector capturing negation presence, frequency, placement, and cross-sentence alignment
- **Interaction Modeling**: Computes absolute difference, element-wise product, and original embeddings to distinguish semantic similarity from negation-induced divergence
- **Regression Head**: Multi-layer network learns non-linear dependencies between semantic representations and negation-sensitive features

## 🎯 Key Features

✅ **Multi-Model Integration**: Combines BERT, RoBERTa, SBERT, and Word2Vec embeddings for robust semantic understanding

✅ **Explicit Negation Awareness**: Unlike pure embedding approaches, explicitly models negation presence, count, and position

✅ **Siamese Bi-LSTM Architecture**: Ensures sentences are encoded in shared latent space while capturing sequential dependencies

✅ **Hybrid Scoring**: Combines learned deep semantic features with handcrafted negation-aware features for accurate similarity assessment

✅ **Education-Focused**: Trained on Negation-Sensitive Similarity Dataset (NSSD) across four pedagogical domains

## 📊 Dataset

**Negation-Sensitive Similarity Dataset (NSSD)**
- Constructed using systematic negation transformations
- Covers four pedagogical domains
- Includes structural and complex negation patterns
- Designed specifically for auto-evaluation system contexts

## 🏗️ Architecture

The model operates in two phases:

**Phase 1: Feature Extraction**
```
Input Sentences → [BERT, SBERT, RoBERTa, Word2Vec] → Fusion → Projection → Bi-LSTM → Semantic Vectors (f1, f2)
```

**Phase 2: Similarity Scoring**
```
Semantic Vectors + Negation Features → Interaction Modeling → Feature Fusion → Regression Head → Similarity Score
```

## 🎓 Applications

- **Auto-Evaluation Systems (AES)**: Fair and accurate automated grading of student responses
- **Educational Assessment**: Handles real-world student answers with negations and qualifications
- **Semantic Search**: Improved accuracy when negation affects meaning
- **Question Answering**: Better understanding of negated queries and responses

## 📈 Impact

This work directly addresses the scalability challenges in global education by:
- Reducing teacher workload on manual assessment
- Providing consistent, fatigue-free evaluation
- Maintaining accuracy even with complex linguistic structures
- Supporting the 14:1 and 13:1 student-teacher ratios common in OECD countries

## 🔬 Technical Innovation

Unlike traditional SSTs that treat negation as superficial modification, NAS recognizes negation as a **fundamental semantic transformation** by:
1. Explicitly modeling negation features alongside embeddings
2. Using multi-model fusion to capture diverse semantic aspects
3. Employing Bi-LSTM to understand sequential negation effects
4. Integrating handcrafted features with learned representations


**Note**: This project specifically focuses on negation handling in educational assessment contexts, where accurate semantic similarity is critical for fair automated grading.
