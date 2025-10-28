# dialogue_to_soap_note

A research / tooling repository to convert clinical dialogues into structured SOAP notes using a pipeline of speech-to-text, diarization, role classification, and summarization (fine-tuned LLMs).

## Table of contents
- [Overview](#overview)
- [Repository structure](#repository-structure)
- [Quick start](#quick-start)
- [Data / file conventions](#data--file-conventions)
- [Notebooks & key files](#notebooks--key-files)
- [Diagrams](#diagrams)
- [Contributing](#contributing)
- [License & contact](#license--contact)

## Overview
This repo implements an end-to-end pipeline that:
1. Converts audio dialogue to transcripts (Speech2Text).
2. Performs speaker diarization.
3. Classifies utterance roles (Doctor / Patient / Other).
4. Generates structured SOAP notes (Summarization).

## Repository structure
- [Convention/](Convention/) : transcription and annotation formats used across the project (example: transcripts, combined transcripts, and final summaries).
  - [Convention/1_Transcript_Whisper.json](Convention/1_Transcript_Whisper.json)
  - [Convention/4_Complete_Transcript.json](Convention/4_Complete_Transcript.json)
  - [Convention/7_Complete_Summary.json](Convention/7_Complete_Summary.json)
- [Pipeline/](Pipeline/) : main orchestration notebooks and pipeline code.
  - [Pipeline/pipeline_FINAL.ipynb](Pipeline/pipeline_FINAL.ipynb)
- [RoleClassifier/](RoleClassifier/) : role-classifier notebooks and inference code.
  - [RoleClassifier/Role_Classifier_Bert_Base_Uncased_3.ipynb](RoleClassifier/Role_Classifier_Bert_Base_Uncased_3.ipynb)
  - [RoleClassifier/bert_uncased_infer_3_FINAL.ipynb](RoleClassifier/bert_uncased_infer_3_FINAL.ipynb)
  - [RoleClassifier/Role_Classifier_Rule_Based_FINAL.ipynb](RoleClassifier/Role_Classifier_Rule_Based_FINAL.ipynb)
- [Speech2Text/](Speech2Text/) : S2T models & utilities (audio preprocessing, whisper configs).
- [Summarization/](Summarization/) : fine-tuning, datasets, and evaluation for clinical summarization models.
  - Example evaluation/test outputs:
    - [Summarization/3_Fine_Tune_LLM/bart/bio_bart/test_soap_50.csv](Summarization/3_Fine_Tune_LLM/bart/bio_bart/test_soap_50.csv)
    - [Summarization/3_Fine_Tune_LLM/bart/bio_bart/eval_test_soap_50.csv](Summarization/3_Fine_Tune_LLM/bart/bio_bart/eval_test_soap_50.csv)
  - Example training notebooks: [Summarization/3_Fine_Tune_LLM/bart/bio_bart/biobart_lora_1.ipynb](Summarization/3_Fine_Tune_LLM/bart/bio_bart/biobart_lora_1.ipynb)
- [assets/diagrams/files/](assets/diagrams/files/) : architecture and DB diagrams.
  - [assets/diagrams/files/general2.drawio](assets/diagrams/files/general2.drawio)
  - [assets/diagrams/files/db2 (1).drawio](assets/diagrams/files/db2.drawio)
  - [assets/diagrams/files/sequence.drawio](assets/diagrams/files/sequence.drawio)

## Quick start
1. Install Python environment (recommend virtualenv / conda) and Jupyter/Colab.
2. Open and run the orchestrating notebook:
   - [Pipeline/pipeline_FINAL.ipynb](Pipeline/pipeline_FINAL.ipynb)
3. To inspect transcripts and conventions:
   - [Convention/1_Transcript_Whisper.json](Convention/1_Transcript_Whisper.json)
   - [Convention/4_Complete_Transcript.json](Convention/4_Complete_Transcript.json)
4. Role classification and summarization experiments are available as notebooks under [RoleClassifier/](RoleClassifier/) and [Summarization/](Summarization/).

Notes:
- Many notebooks include Colab drive mount steps. Adapt these cells if running locally.
- Hardware: fine-tuning notebooks expect GPU resources (A100/T4/L4 referenced in notebooks).

## Data & file conventions
- Transcripts use Whisper-derived timestamps and token-level times. See [Convention/1_Transcript_Whisper.json](Convention/1_Transcript_Whisper.json).
- Combined utterance-level transcripts live in [Convention/4_Complete_Transcript.json](Convention/4_Complete_Transcript.json).
- Final structured summaries (sentence-indexed SOAP components) are in [Convention/7_Complete_Summary.json](Convention/7_Complete_Summary.json).

## Notebooks & key files
- Pipeline runner: [Pipeline/pipeline_FINAL.ipynb](Pipeline/pipeline_FINAL.ipynb)
- Role classifier (BERT-based and rule-based): files in [RoleClassifier/](RoleClassifier/)
  - [RoleClassifier/Role_Classifier_Bert_Base_Uncased_3.ipynb](RoleClassifier/Role_Classifier_Bert_Base_Uncased_3.ipynb)
  - [RoleClassifier/bert_uncased_infer_3_FINAL.ipynb](RoleClassifier/bert_uncased_infer_3_FINAL.ipynb)
  - [RoleClassifier/Role_Classifier_Rule_Based_FINAL.ipynb](RoleClassifier/Role_Classifier_Rule_Based_FINAL.ipynb)
- Summarization experiments and evaluation CSVs: [Summarization/3_Fine_Tune_LLM/bart/bio_bart/](Summarization/3_Fine_Tune_LLM/bart/bio_bart/)

## Diagrams
Architectural diagrams and sequence diagrams are stored under:
- [assets/diagrams/files/general2.drawio](assets/diagrams/files/general2.drawio)
- [assets/diagrams/files/general.drawio](assets/diagrams/files/general.drawio)
- [assets/diagrams/files/db2.drawio](assets/diagrams/files/db2.drawio)
- [assets/diagrams/files/sequence.drawio](assets/diagrams/files/sequence.drawio)

Open these with draw.io.
