---
category: general
date: 2026-03-18
description: Perform OCR on image to extract text from image quickly. Learn how to
  load image for OCR, create OCR engine, and improve OCR accuracy with language options.
draft: false
keywords:
- perform OCR on image
- extract text from image
- improve OCR accuracy
- load image for OCR
- create OCR engine
language: en
og_description: Perform OCR on image with this detailed guide. Learn to load image
  for OCR, create OCR engine, and improve OCR accuracy for reliable text extraction.
og_title: Perform OCR on Image – Complete Programming Tutorial
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: Perform OCR on Image – Step‑by‑Step Guide
url: /python-java/general/perform-ocr-on-image-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Perform OCR on Image – Complete Programming Tutorial

Ever needed to **perform OCR on image** but weren’t sure which library to pick or how to get reliable results? You’re not alone. In this guide we’ll walk through everything you need to **extract text from image**, from loading the picture to tweaking language options so you can **improve OCR accuracy** every step of the way.

We’ll cover how to **load image for OCR**, how to **create OCR engine**, and why each setting matters. By the end you’ll have a ready‑to‑run script that prints the recognized text, and you’ll understand the “why” behind each line—no vague “see the docs” shortcuts. Let’s dive in.

## What You’ll Need

- Python 3.8+ (the code uses f‑strings and type hints)
- The hypothetical `ocr_lib` package – install with `pip install ocr_lib`
- An image file containing clear, printed text (e.g., `lab_report.png`)
- A basic text editor or IDE (VS Code, PyCharm, whatever you like)

If you already have those, great—you’re set. If not, grab Python from python.org and run the pip command; it only takes a minute.

![perform OCR on image example](/images/ocr-example.png)

*Alt text: perform OCR on image – sample output showing extracted text.*

## Step 1: Create OCR Engine – How to **create OCR engine** in Python

Before any recognition can happen, the library needs an engine object that holds configuration and runtime state. Think of the engine as the brain behind the operation.

```python
# step_1_create_engine.py
from ocr_lib import OcrEngine, LanguageOptions, OcrResult

def build_engine() -> OcrEngine:
    """
    Initialize and return a fresh OcrEngine instance.
    Creating the engine once and reusing it is more efficient than
    instantiating it inside a loop.
    """
    engine = OcrEngine()
    return engine
```

**Why this matters:** Instantiating the engine early lets you attach language options later, and it also caches internal models for faster subsequent calls.

## Step 2: Load Image for OCR – The correct way to **load image for OCR**

Now that we have an engine, we must give it something to read. The `setImageFromFile` method accepts a filesystem path; the path can be absolute or relative to the script’s working directory.

```python
# step_2_load_image.py
def load_image(engine: OcrEngine, image_path: str) -> None:
    """
    Attach an image file to the engine.
    Raises FileNotFoundError if the file does not exist.
    """
    engine.setImageFromFile(image_path)
```

**Pro tip:** Use an absolute path or `os.path.join` to avoid “file not found” surprises when the script runs from a different folder.

```python
import os

image_file = os.path.join("YOUR_DIRECTORY", "lab_report.png")
load_image(my_engine, image_file)
```

## Step 3: Improve OCR Accuracy – Tweaking **language options** to **improve OCR accuracy**

Out‑of‑the‑box OCR works, but domain‑specific vocabularies (like lab jargon) often trip it up. By feeding a custom dictionary and a blacklist you reduce mis‑recognitions such as confusing “0” with “O”.

```python
# step_3_language_options.py
def configure_language(engine: OcrEngine) -> None:
    """
    Set up language options to help the engine recognize domain‑specific terms
    and ignore characters that are frequently misread.
    """
    language_opts = LanguageOptions()
    # Add terms that appear often in laboratory reports
    language_opts.setDictionary(["HPLC", "UV‑VIS", "chromatogram"])
    # Blacklist characters that cause confusion
    language_opts.setBlacklist(["0", "O", "l", "1"])
    engine.setLanguageOptions(language_opts)
```

**Why this helps:** The dictionary tells the OCR model that “HPLC” is a valid token, preventing it from breaking the word into nonsense. The blacklist tells the model to treat ambiguous symbols as noise, which directly **improves OCR accuracy**.

## Step 4: Perform OCR on Image – The core **perform OCR on image** call

With the engine primed and the image attached, it’s time to actually recognize the text. This step returns an `OcrResult` object that you can query for raw text, confidence scores, or bounding boxes.

```python
# step_4_recognize.py
def recognize_text(engine: OcrEngine) -> OcrResult:
    """
    Run the OCR process. This may take a few seconds depending on image size.
    Returns an OcrResult that contains the extracted string and metadata.
    """
    result = engine.recognize()
    return result
```

If the image is blurry, you’ll see lower confidence numbers in the result. That’s a cue to pre‑process the image (e.g., increase contrast) before feeding it to the engine.

## Step 5: Extract Text from Image – Pulling the final string out

Finally, we ask the `OcrResult` for its textual representation. The `getText()` method returns a plain‑text string ready for downstream processing (saving to a file, feeding into a database, etc.).

```python
# step_5_output.py
def print_result(result: OcrResult) -> None:
    """
    Output the recognized text to the console.
    You could also write it to a file with open('output.txt', 'w') …
    """
    extracted = result.getText()
    print("=== OCR Output Start ===")
    print(extracted)
    print("=== OCR Output End ===")
```

**Expected output:** Assuming `lab_report.png` contains a simple table, you might see something like:

```
=== OCR Output Start ===
Sample ID: 00123
Method: HPLC
Result: 5.67 mg/L
=== OCR Output End ===
```

That’s the **extract text from image** part done.

## Full Working Example – Put It All Together

Below is a single script that stitches the pieces from the previous sections. You can copy‑paste it into `run_ocr.py` and execute `python run_ocr.py`.

```python
# run_ocr.py
import os
from ocr_lib import OcrEngine, LanguageOptions, OcrResult

def build_engine() -> OcrEngine:
    engine = OcrEngine()
    return engine

def load_image(engine: OcrEngine, image_path: str) -> None:
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")
    engine.setImageFromFile(image_path)

def configure_language(engine: OcrEngine) -> None:
    language_opts = LanguageOptions()
    language_opts.setDictionary(["HPLC", "UV‑VIS", "chromatogram"])
    language_opts.setBlacklist(["0", "O", "l", "1"])
    engine.setLanguageOptions(language_opts)

def recognize_text(engine: OcrEngine) -> OcrResult:
    return engine.recognize()

def print_result(result: OcrResult) -> None:
    extracted = result.getText()
    print("\n=== OCR Output Start ===")
    print(extracted)
    print("=== OCR Output End ===\n")

def main() -> None:
    # 1️⃣ Create the OCR engine
    ocr_engine = build_engine()

    # 2️⃣ Load the image you want to process
    image_file = os.path.join("YOUR_DIRECTORY", "lab_report.png")
    load_image(ocr_engine, image_file)

    # 3️⃣ Apply language tweaks to **improve OCR accuracy**
    configure_language(ocr_engine)

    # 4️⃣ **Perform OCR on image** – this is the heavy lifting
    ocr_result = recognize_text(ocr_engine)

    # 5️⃣ **Extract text from image** and show it
    print_result(ocr_result)

if __name__ == "__main__":
    main()
```

### Quick verification checklist

| ✅ | Item |
|---|------|
| ✔️ | Engine is created (`create OCR engine`) |
| ✔️ | Image is loaded (`load image for OCR`) |
| ✔️ | Language options are set (`improve OCR accuracy`) |
| ✔️ | OCR is performed (`perform OCR on image`) |
| ✔️ | Text is extracted (`extract text from image`) |

Run the script and watch the console. If you see the “OCR Output” block with your report’s contents, you’ve successfully **performed OCR on image**.

## Common Pitfalls & How to Avoid Them

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| **Blurry input** | The OCR model can’t distinguish characters | Pre‑process with OpenCV: `cv2.GaussianBlur` or increase DPI |
| **Wrong language** | Default language may be set to something other than English | Call `engine.setLanguage("eng")` before `recognize()` |
| **Missing dictionary terms** | Domain‑specific words become garbled | Add them via `setDictionary` as shown in Step 3 |
| **Blacklisted characters cause

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}