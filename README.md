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

## Usage

### OCR + Zephyr-7B Pipeline:
1. Load PDF invoices and extract key fields using PaddleOCR.
2. Use Zephyr-7B to interpret and structure the data.
3. Store the results in JSON format.

### LayoutLM Method:
1. Fine-tune the LayoutLM model on annotated invoice data.
2. Use the model to extract fields from complex invoices.

Both methods are scalable, leveraging GPU acceleration for large datasets.

## Architecture

### OCR + LLM Pipeline:
1. Text extraction using PaddleOCR (GPU-accelerated).
2. Text analysis with the Zephyr-7B model.
3. Confidence score-based trust determination.
4. Data structuring in JSON format.

### LayoutLM Approach:
1. Fine-tune LayoutLM on labeled data.
2. Extract and categorize key invoice fields using spatial document understanding.

## Error Handling
- Low OCR confidence triggers manual review.
- Non-standard layouts are flagged for further data annotation to improve model accuracy.
