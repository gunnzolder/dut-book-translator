# Book Translator

## Description
It uses OpenAI's `gpt-4-vision` to parse images into markdown (Claude is refusing to work because of content policy). Translation into Ukrainian is done by Anthropic's `claude-3-sonnet` model - it's highly recommended to keep it, as it gives much better quality than OpenAI's `gpt-4` model while being few times cheaper.

## Usage

1. Use `pdf_to_jpeg.ipynb` to convert pdf pages to jpeg images and upload them to the S3 storage (gpt-4-vision requires live URLs).
2. Use `parser.ipynb` to parse the images to markdown + LateX and to translate them to Ukrainian.

## Requirements
1. OpenAI API key
2. Anthropic API key

## Possible improvements
- Add script to merge Ukrainian markdown files keeping the sentence structure.