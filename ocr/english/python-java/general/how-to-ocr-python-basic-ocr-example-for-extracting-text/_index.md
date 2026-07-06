---
category: general
date: 2026-04-26
description: 'how to ocr python: Learn to extract text from image and read tiff file
  python using a basic OCR example. Quick, runnable code included.'
draft: false
keywords:
- how to ocr python
- extract text from image
- read tiff file python
- basic ocr example
- convert scanned image text
language: en
og_description: 'how to ocr python: A step‑by‑step guide that shows how to extract
  text from image, read tiff file python, and convert scanned image text with a simple,
  runnable script.'
og_title: how to ocr python – Basic OCR Example for Extracting Text
tags:
- OCR
- Python
- Image Processing
title: how to ocr python – Basic OCR Example for Extracting Text
url: /python-java/general/how-to-ocr-python-basic-ocr-example-for-extracting-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# how to ocr python – Basic OCR Example for Extracting Text

Ever wondered **how to ocr python** when you have a scanned TIFF lying on your desk? You're not the only one staring at a bunch of image files and asking, “How do I get the words out of this?” The good news is that turning a picture into plain text is a piece of cake with the right library and a few clear steps.

In this tutorial we’ll walk through a **basic OCR example** that reads a TIFF file, extracts the text, and prints it to the console. By the end you’ll know exactly how to **extract text from image** files, how to handle the quirks of TIFF formats, and what to tweak if you need to **convert scanned image text** into something more useful. No hidden magic—just straightforward Python that you can copy‑paste and run today.

## What You’ll Need

Before we dive in, make sure you have:

- Python 3.9+ installed (the latest stable release is best).
- A pip‑installable OCR library. For this guide we’ll use a fictional `aocr` package that mimics popular tools like Tesseract; you can replace it with `pytesseract` or `easyocr` later.
- A TIFF image you want to process – name it `input.tiff` and drop it into a folder you’ll reference in the code.
- Basic familiarity with the command line (just to install the package).

That’s it. No heavyweight dependencies, no Docker containers, just a few lines of code.

## Step 1 – Install and Import Dependencies (how to ocr python)

First, get the OCR package. Open a terminal and run:

```bash
pip install aocr
```

If you prefer a real‑world library, swap `aocr` with `pytesseract` and install the Tesseract engine separately.

Now import what we need. The `Path` class from `pathlib` gives us a clean way to work with file paths across operating systems.

```python
# Step 1: Import the Path class for handling file paths
from pathlib import Path

# Import the OCR engine and image loader from the chosen library
from aocr import OcrEngine, Image
```

*Why use `Path`?* Because it abstracts away the slashes (`/` vs `\`) and lets you join directories without worrying about the underlying OS. That small detail often saves headaches when you later move the script to a CI server.

## Step 2 – Create the OCR Engine Instance (basic ocr example)

Next, spin up the OCR engine. Think of `OcrEngine` as the brain that will read the picture and spit out characters.

```python
# Step 2: Create an instance of the OCR engine
ocr_engine = OcrEngine()
```

Most OCR libraries let you tweak language, DPI, or confidence thresholds here. For this **basic OCR example** we’ll stick with the defaults, but you can explore `ocr_engine.config` later if you need to handle multilingual documents.

## Step 3 – Load Your TIFF Image (read tiff file python)

Here’s where the **read tiff file python** part comes in. TIFFs can be multi‑page, but `Image.load` will grab the first page by default—perfect for a single‑page scan.

```python
# Step 3: Load the image you want to recognize
# Using a generic placeholder path makes it easy to adapt the example
ocr_engine.image = Image.load(Path("YOUR_DIRECTORY/input.tiff"))
```

Replace `"YOUR_DIRECTORY"` with the actual folder that holds `input.tiff`. If you’re unsure where the script runs, `Path.cwd()` prints the current working directory—handy for debugging path issues.

## Step 4 – Run the OCR Process (extract text from image)

Now the magic happens. Calling `process()` sends the image through the OCR pipeline and returns a result object.

```python
# Step 4: Run the OCR process to extract text from the image
ocr_result = ocr_engine.process()
```

Behind the scenes the engine might be converting the image to grayscale, applying thresholding, and feeding it into a neural network. You don’t need to manage those steps; the library abstracts them away.

## Step 5 – Print the Recognized Text (convert scanned image text)

Finally, output the text. In real projects you’d probably write it to a file or a database, but printing keeps the example tidy.

```python
# Step 5: Print the recognized text to the console
print(ocr_result.text)
```

When you run the script, you should see something like:

```
Hello, world!
This is a sample scanned document.
```

If the output looks garbled, double‑check that the source image is clear and that the OCR language matches the text.

## Full Working Script

Putting it all together, here’s the complete, ready‑to‑run program:

```python
# Full script: how to ocr python – basic OCR example

from pathlib import Path
from aocr import OcrEngine, Image  # Replace with your OCR library if needed

def main():
    # Initialize the OCR engine
    ocr_engine = OcrEngine()

    # Load the TIFF image (adjust the path as needed)
    image_path = Path("YOUR_DIRECTORY/input.tiff")
    if not image_path.is_file():
        raise FileNotFoundError(f"Could not find {image_path}. Make sure the file exists.")
    
    ocr_engine.image = Image.load(image_path)

    # Perform OCR
    ocr_result = ocr_engine.process()

    # Output the extracted text
    print("=== OCR Output ===")
    print(ocr_result.text)

if __name__ == "__main__":
    main()
```

### Expected Output

```
=== OCR Output ===
Your scanned document’s text appears here, line by line.
```

If you need to **convert scanned image text** into a searchable PDF, you can pipe `ocr_result.text` into a PDF generator like `reportlab`—but that’s a whole tutorial on its own.

## Common Pitfalls & Pro Tips

- **Low‑resolution scans**: OCR struggles below 150 DPI. If your TIFF is fuzzy, up‑sample it first with Pillow (`Image.open(...).resize(...)`).
- **Multiple pages**: For multi‑page TIFFs, iterate over `Image.load_multi_page()` (if your library supports it) and concatenate the results.
- **Language support**: Many engines default to English. Set `ocr_engine.language = "spa"` for Spanish, for example.
- **Whitespace handling**: OCR often adds stray line breaks. Use `str.splitlines()` or regular expressions to clean up the output.
- **Performance**: For bulk processing, reuse a single `OcrEngine` instance instead of creating a new one per file.

## Extending the Example

Now that you’ve mastered **how to ocr python** for a single image, consider these next steps:

1. **Batch processing** – Loop over a directory of TIFFs and write each result to a `.txt` file.
2. **Integration with Pandas** – Store extracted text alongside metadata for quick analysis.
3. **Hybrid approach** – Combine OCR with NLP libraries like `spaCy` to extract entities (names, dates, amounts) from scanned invoices.
4. **Alternative file formats** – Swap `Image.load` for `Image.from_bytes` to handle images coming from an API or a database.

All of these build on the core idea of **extract text from image** and **convert scanned image text** into something machines can understand.

## Conclusion

We’ve walked through a clear, end‑to‑end **basic OCR example** that shows **how to ocr python**, how to **read tiff file python**, and how to **extract text from image** files with just a handful of lines. The script is self‑contained, includes error handling, and prints the result directly, making it a solid foundation for any project that needs to turn scanned documents into editable text.

Feel free to experiment—swap out the OCR backend, tweak the preprocessing, or hook the output into a downstream workflow. The sky’s the limit when you can reliably **convert scanned image text** into searchable, searchable data.

Got questions about edge cases, language packs, or performance tuning? Drop a comment below, and happy coding! 

![how to ocr python example](/images/ocr-python-example.png "Screenshot of how to ocr python script output")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}