# Invoice Data Extraction using OCR and Large Language Models

This repository implements two high-accuracy methods for extracting key data fields from invoices, including invoice numbers, dates, and amounts, using GPU-optimized techniques. The approaches ensure high accuracy while maintaining scalability and cost-efficiency.

## Methods Overview

### 1. OCR + Zephyr-7B Model Pipeline
This approach integrates Optical Character Recognition (OCR) with a Large Language Model (LLM) to handle both regular and scanned PDF invoices.

#### Key Steps:
- **PDF Handling**: Uses `fitz` (PyMuPDF) to extract pages from PDFs and preprocess for OCR.
- **OCR (PaddleOCR)**: Configured with GPU acceleration to extract text and calculate confidence scores.
- **Text Interpretation (Zephyr-7B)**: The extracted text is processed using a transformer-based model to identify and structure key invoice fields.
- **Trustworthiness Assessment**: Combines OCR confidence scores with LLM output to determine the reliability of the extracted data.
- **Output**: Extracted data is structured in JSON format for further use.

### 2. LayoutLM for Data Extraction
A supervised learning approach that fine-tunes the LayoutLM model for document understanding tasks.

#### Key Steps:
- **Data Preparation**: Annotates a custom dataset of PDFs using `LabelStudio`.
- **Model Fine-Tuning**: The LayoutLM model is fine-tuned to recognize key invoice fields and handle complex document layouts.
- **Performance**: LayoutLM is well-suited for complex layouts and spatial data extraction tasks.

## Requirements

- **Python 3.x**
- **PyMuPDF (fitz)**
- **PaddleOCR**
- **Hugging Face Transformers (Zephyr-7B, LayoutLM)**
- **LabelStudio** (For data annotation in the second method)
- **GPU with CUDA support** (Optional but recommended for faster processing)

### Python Packages:
Install the required packages via `pip`:
```bash
pip install pymupdf paddleocr transformers
```
