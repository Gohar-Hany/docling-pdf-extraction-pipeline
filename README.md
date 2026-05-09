# Docling PDF Extraction Pipeline

A robust, multi-layer PDF extraction pipeline that combines structure parsing, image extraction, OCR, and vision-language description to produce high-quality Markdown and JSON outputs.

## Features

- Structured text and table extraction using Docling
- Embedded image extraction using PyMuPDF
- Vector graphics capture through full-page rendering
- OCR for image text extraction (PaddleOCR)
- Visual understanding and description using Ollama vision models
- Formula handling with LaTeX-friendly reconstruction
- Deterministic JSON export using Docling native structure
- Reconstructed Markdown output in reading order

## Project Structure

- `local_pdf_pipeline.py`: main end-to-end pipeline
- `Doc.py`: additional script in this workspace
- `pipeline_output/`: generated Markdown, JSON, extracted images, and page renders
- `output/`: previous output artifacts

## Requirements

- Python 3.10+
- Optional but recommended:
  - Ollama running locally on `http://localhost:11434`
  - PaddleOCR for image OCR step

Install common dependencies:

```bash
pip install docling pymupdf pillow ollama paddleocr
```

## Usage

Run the pipeline on any PDF:

```bash
python local_pdf_pipeline.py sample.pdf
```

Useful options:

```bash
python local_pdf_pipeline.py sample.pdf --vision-model minicpm-v --text-model phi3:mini --dpi 150 --output-dir pipeline_output
```

## Outputs

For an input PDF named `sample.pdf`, the pipeline generates:

- `pipeline_output/sample_output.md`
- `pipeline_output/sample_structured.json`
- `pipeline_output/sample_toc.json`
- `pipeline_output/extracted_images/*`
- `pipeline_output/page_renders/*`

## Notes

- If PaddleOCR is not installed, OCR step is skipped and the pipeline continues.
- If a vision request times out, the pipeline writes a fallback marker and continues.
- The JSON export is generated directly from Docling, not from LLM text conversion.

## License

Choose a license before publishing publicly (for example, MIT).