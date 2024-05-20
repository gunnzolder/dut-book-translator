# Book Translator

## Description
It uses OpenAI's `gpt-4-o` model to parse images into markdown (Claude is refusing to work because of content policy). Translation into Ukrainian is done by Anthropic's `claude-3-sonnet` model - it's highly recommended to keep it, as it gives much better quality than OpenAI's `gpt-4` model while being few times cheaper.

## Usage

1. **Setup Environment**:
    - Create the `.env` file from the `.env.example` file:
      ```bash
      cp .env.example .env
      ```
    - Set up the virtual environment and install the dependencies by running:
      ```bash
      chmod +x setup.sh
      ./setup.sh
      ```

2. **Convert PDF to JPEG**:
    - Use `01-pdf_to_jpeg.ipynb` to convert PDF pages to JPEG images and upload them to the S3 storage (gpt-4-vision requires live URLs).

3. **Parse Images to Markdown and Translate**:
    - Use `02-parser.ipynb` to parse the images to markdown + LaTeX and translate them to Ukrainian.

4. **Join Markdown Pages, Convert Formulas to Images, and Generate DOCX**:
    - Use `03-md_to_docx.ipynb` to join markdown pages into one file, convert formulas into images, and generate the DOCX file.

## Requirements
1. OpenAI API key
2. Anthropic API key

## Possible Improvements
- Add script to merge Ukrainian markdown files while keeping the sentence structure.
