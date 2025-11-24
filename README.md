# Pdf parsing RAG and Analysis Pipeline using Unstructured, Poppler, Gemini, and Llama

This project demonstrates a full workflow for parsing PDFs, extracting text, tables, and images, generating captions, and producing descriptions using both cloud-based and local LLM models.
It includes detailed examples for working with:

- unstructured (PDF parsing)

- pdf2image + Poppler (PDF → Image conversion)

- Gemini 2.5 Flash (image & table description)

- Ollama Llama3 (local table description)

- NLTK-free text chunking (fallback)

- PyPDF2 (manual text extraction)

---------------------------------------------------------------------------------------------

__Features__

1. PDF Parsing
  
  Extracts text, images, tables, and figure captions using partition_pdf.
  
  Supports high-resolution parsing via Poppler.
  
  Generates structured chunks for further processing.

2. Image Extraction & Processing

  Extracts images as base64.
  
  Automatically detects figure captions.
  
  Uses Gemini to generate detailed image descriptions.

3. Table Extraction & Analysis

  Extracts tables from PDFs in structured HTML format.
  
  Generates table descriptions using:
  
    Gemini API
    
    Ollama local Llama3 model

4. Natural Language Processing

  Supports semantic chunking using Unstructured’s CompositeElement.
  
  Custom sentence tokenization without relying on NLTK, avoiding punkt errors.

5. Fallback PDF Text Extraction

  Uses PyPDF2 to extract raw text.
  
  Custom chunking into 500-word blocks (works fully offline).
  
-----------------------------------------------------------------------------------------------

  __Installation__
1. Clone the repo
git clone https://github.com/<your-username>/<repo-name>.git
cd <repo-name>

2. Create virtual environment
python3 -m venv .venv
source .venv/bin/activate

-----------------------------------------------------------------------------------------------
__REquired Libraries__

1] Core parsing:
  from unstructured.partition.pdf import partition_pdf
  from unstructured.documents.elements import Element, Text, Image, FigureCaption, Table

2] pdf to image
  from pdf2image import convert_from_path

3] Image display:
  from IPython.display import Image as IPImage, display

4] LLM Models
  import google.generativeai as genai
  import requests   # for Ollama

5] Text extraction fallback
  import PyPDF2

6] Set up poppler (macOS):

  Install Poppler:
    > brew install poppler
  
  Verify:
    > which pdfinfo
  
  Add to PATH:
    > os.environ["PATH"] = "/opt/homebrew/bin:" + os.environ["PATH"]
