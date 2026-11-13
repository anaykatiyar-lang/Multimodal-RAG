# Multimodal-RAG

**Evidence-Grounded Multimodal Retrieval-Augmented Generation on AMD Instinct MI300X**

## Overview

Multimodal-RAG is a document intelligence and question-answering system developed as part of **AMD Mini-Challenge 3**.

The project addresses the challenge of retrieving accurate technical information from complex engineering documentation containing PDFs, Word documents, spreadsheets, images, CSV files, logs, and source code.

It combines semantic retrieval with multimodal language-model reasoning to generate evidence-grounded answers with precise source citations.

## Architecture

The system uses two complementary models:

- **Qwen2.5-VL-7B-Instruct:** Multimodal language model for document understanding and answer generation.
- **BAAI/bge-small-en-v1.5:** Embedding model for semantic document retrieval.

### Processing Pipeline

1. **Document Ingestion:** Reads and processes heterogeneous engineering documents.
2. **Document Indexing:** Extracts document content and generates semantic embeddings.
3. **Retrieval:** Finds relevant evidence for incoming questions.
4. **Multimodal Reasoning:** Uses Qwen2.5-VL to interpret retrieved context and generate answers.
5. **Citation Generation:** Returns corpus-relative source paths supporting the answer.
6. **Output Validation:** Produces structured JSON responses with answers, citations, and confidence scores.

## Technology Stack

| Component             | Technology             |
| --------------------- | ---------------------- |
| Language              | Python                 |
| Deep Learning         | PyTorch                |
| GPU Acceleration      | AMD ROCm               |
| GPU Hardware          | AMD Instinct MI300X    |
| Vision-Language Model | Qwen2.5-VL-7B-Instruct |
| Embedding Model       | BAAI/bge-small-en-v1.5 |
| Containerization      | Docker                 |
| Communication         | Unix Domain Socket     |

## Key Engineering Features

- Multimodal technical document understanding.
- Semantic retrieval using dense embeddings.
- GPU-accelerated model inference.
- Persistent model-serving architecture.
- Source-level citation generation.
- Offline inference without external network access at evaluation time.
- Structured JSON output.
- Document-processing error handling.
- Designed around strict startup, inference latency, and GPU-memory constraints.

## Repository Structure
```
Multimodal-RAG/
├── README.md
├── CONTRACT.md
├── sample-questions.json
├── selfcheck.py
├── selfcheck_gpu.py
├── setup.sh
├── starter/
│   ├── Dockerfile
│   └── app/
└── submission/
    ├── Dockerfile
    ├── app/
    │   ├── app.py
    │   ├── server.py
    │   └── requirements.txt
    ├── build_and_test.sh
    └── run_all_questions.sh
```

## Sample Evaluation Results

The implementation achieved a perfect score on the supplied ten-question sample evaluation.

| Evaluation Metric   | Result      |
| ------------------- | ----------- |
| Questions Evaluated | 10          |
| Answer Validation   | 10/10 PASS  |
| Citation Validation | 10/10 PASS  |
| Total Score         | **200/200** |

All ten sample questions passed both answer and citation checks.

*Note: These are sample-set results, not an official hidden-test score.*

## AMD GPU Deployment

The application was built and tested on an AMD Instinct MI300X GPU environment using ROCm-enabled PyTorch.

The deployment uses Docker to package the application, dependencies, and model weights. A persistent inference server loads the embedding and vision-language models onto the GPU, allowing subsequent questions to reuse the loaded models.

## Running the Project

Build the Docker image:
```
bash submission/build_and_test.sh
```

Run the sample evaluation:
```
bash submission/run_all_questions.sh
```

Run the GPU-enabled self-check:
```
python3 selfcheck_gpu.py mc3-rag:latest mc3-corpus
```

The sample corpus is a challenge test asset and is not included in this public repository.

## Project Context

**Challenge:** AMD Mini-Challenge 3 – Multimodal RAG

**Focus:** Engineering Document Intelligence, Multimodal Retrieval, Evidence-Grounded Question Answering, and GPU-Accelerated Inference.

**Hardware:** AMD Instinct MI300X

**Repository:** [Multimodal-RAG](https://github.com/anaykatiyar-lang/Multimodal-RAG)