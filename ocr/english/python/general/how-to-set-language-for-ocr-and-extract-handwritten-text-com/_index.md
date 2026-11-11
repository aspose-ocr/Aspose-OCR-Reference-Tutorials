---
category: general
date: 2026-03-26
description: How to set language in an OCR engine and extract handwritten text from
  images – step‑by‑step tutorial to convert image to text.
draft: false
keywords:
- how to set language
- extract handwritten text
- convert image to text
- how to extract handwritten
- recognize handwritten notes
language: en
og_description: How to set language in an OCR engine and extract handwritten notes
  from images. Learn to convert image to text in minutes.
og_title: How to Set Language for OCR – Extract Handwritten Text Easily
tags:
- OCR
- Python
- Image Processing
title: How to Set Language for OCR and Extract Handwritten Text – Complete Guide
url: /python/general/how-to-set-language-for-ocr-and-extract-handwritten-text-com/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Set Language for OCR and Extract Handwritten Text – Complete Guide

Ever wondered **how to set language** on your OCR engine so it actually understands the characters you need? Maybe you’ve got a photo of a grocery list, a meeting note, or a sketchy‑looking diagram and you just can’t get the text out. The good news? You don’t need a PhD in computer vision—just a few lines of Python and the right flags.

In this tutorial we’ll walk through the exact steps to **extract handwritten text** from a PNG, convert that image to plain text, and explain the “why” behind each setting. By the end you’ll be able to recognize handwritten notes in any project, whether it’s a note‑taking app or a batch‑processing pipeline.

> **What you’ll need**  
> • Python 3.8+ (the code works with 3.10 as well)  
> • The `ocr` library (or any compatible wrapper that exposes `OcrEngine`)  
> • A sample image like `note_handwritten.png` – any image with extended Latin characters will do.

Let’s get started.

---

## How to Set Language and Enable Handwritten Recognition

The first thing you must do is tell the OCR engine which alphabet it should expect. If you skip this step, the engine defaults to a generic set that often mis‑recognizes accented letters or special symbols.

```python
import ocr  # Assuming the library is named `ocr`

# Step 1: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()

# Step 2: Choose the language that includes extended Latin characters
ocr_engine.language = ocr.Language.ExtendedLatin

# Step 3: Turn on the handwritten‑text flag
ocr_engine.recognize_handwritten = True
```

**Why this matters:**  
- **ExtendedLatin** covers characters like “ñ”, “ø”, and “ç”, which are common in many European notes.  
- The `recognize_handwritten` flag switches the underlying model from printed‑text OCR to a neural network trained on cursive strokes. Without it, the engine treats your scribbles as noise.

> **Pro tip:** If you’re processing documents in multiple languages, instantiate a separate engine per language or dynamically switch `ocr_engine.language` before each call. This avoids the overhead of loading unused character sets.

![Screenshot of OCR engine configuration showing how to set language](/images/ocr-set-language.png "How to set language on OCR engine")

*Image alt text: “How to set language on OCR engine configuration screen.”*

---

## Extract Handwritten Text from a PNG Image

Now that the engine knows what to look for, it’s time to feed it an image. The `recognize_image` method returns a rich result object; the `text` attribute holds the plain string you care about.

```python
# Step 4: Perform OCR on the input image
handwritten_result = ocr_engine.recognize_image("YOUR_DIRECTORY/note_handwritten.png")

# Step 5: Print the extracted text
print(handwritten_result.text)
```

When you run the script, you should see something like:

```
Buy milk
Call Dr. García at 5 pm
Pick up résumé
```

That output proves you successfully **convert image to text** and that the engine respected the language setting you supplied.

**Common pitfalls**  
- **Incorrect path** – Double‑check the file location; a missing file raises a `FileNotFoundError`.  
- **Low‑resolution image** – Handwritten OCR struggles below 300 dpi. Upscale or rescan if the output looks garbled.  
- **Color inversion** – If the background is dark and the ink is light, invert the colors first (`Pillow` can help).

---

## Convert Image to Text Using a Helper Function

If you plan to run OCR on dozens of files, wrap the logic in a reusable function. This also makes the code easier to test and to integrate with other pipelines.

```python
def extract_handwritten_text(image_path: str) -> str:
    """
    Loads an image, sets the OCR engine to ExtendedLatin,
    enables handwritten recognition, and returns the plain text.
    """
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ExtendedLatin
    engine.recognize_handwritten = True

    result = engine.recognize_image(image_path)
    return result.text.strip()   # Remove leading/trailing whitespace


# Example usage
if __name__ == "__main__":
    txt = extract_handwritten_text("YOUR_DIRECTORY/note_handwritten.png")
    print("📝 Handwritten notes:\n", txt)
```

The helper isolates the **how to extract handwritten** logic, so you can call it from a Flask endpoint, a CLI tool, or a batch job without rewriting the configuration each time.

---

## Recognize Handwritten Notes in Real‑World Scenarios

Below are a few situations where you’ll likely need to **recognize handwritten notes** and how this setup adapts:

| Scenario | Why language matters | Suggested tweak |
|----------|---------------------|-----------------|
| **Multilingual grocery lists** | Items may contain accents (e.g., “crème”) | Switch `ocr_engine.language` per list or use `ocr.Language.AutoDetect` if supported |
| **Classroom whiteboard photos** | Chalk may produce faint strokes | Increase image contrast before feeding it to the engine |
| **Medical prescriptions** | Handwriting is notoriously messy | Pair OCR with a spelling‑correction dictionary for drug names |

In each case, the core steps—**how to set language**, enable handwritten mode, and call `recognize_image`—remain identical. That consistency is what makes the approach both robust and easy to maintain.

---

## Edge Cases & Advanced Tweaks

1. **Batch processing** – Load the engine once, loop over files, and only change the `language` attribute when needed. This cuts down on initialization overhead.

2. **Non‑Latin scripts** – If you need to process Cyrillic or Arabic, replace `ExtendedLatin` with the appropriate enum (e.g., `ocr.Language.Cyrillic`). The same pattern applies.

3. **Partial recognition** – Sometimes the engine returns empty strings for very short strokes. A quick sanity check (`if not result.text.strip(): …`) lets you fallback to a secondary model or ask the user to rescan.

4. **Performance profiling** – For large datasets, time the `recognize_image` call. If it becomes a bottleneck, consider parallelizing using `concurrent.futures.ThreadPoolExecutor`.

---

## Full Working Example

Below is the complete script you can copy‑paste into a file named `handwritten_ocr.py`. It includes argument parsing so you can point it at any image from the command line.

```python
#!/usr/bin/env python3
"""
handwritten_ocr.py – Convert an image containing handwritten notes
to plain text using the OCR library.

Usage:
    python handwritten_ocr.py path/to/image.png
"""

import sys
import argparse
import ocr  # Replace with the actual import if the library name differs


def extract_handwritten_text(image_path: str) -> str:
    """Extracts handwritten text from the given image."""
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ExtendedLatin
    engine.recognize_handwritten = True

    result = engine.recognize_image(image_path)
    return result.text.strip()


def main():
    parser = argparse.ArgumentParser(
        description="Convert handwritten image to text (how to set language, extract handwritten text)."
    )
    parser.add_argument("image", help="Path to the PNG/JPG image containing handwritten notes")
    args = parser.parse_args()

    try:
        text = extract_handwritten_text(args.image)
        if text:
            print("✅ Extracted text:\n", text)
        else:
            print("⚠️ No text detected – try a higher‑resolution image.")
    except Exception as e:
        print(f"❌ Error processing {args.image}: {e}", file=sys.stderr)
        sys.exit(1)


if __name__ == "__main__":
    main()
```

Run it like:

```bash
python handwritten_ocr.py YOUR_DIRECTORY/note_handwritten.png
```

You should see the same output as the earlier snippet, confirming that you’ve successfully **convert image to text** and **recognize handwritten notes**.

---

## Conclusion

We’ve covered **how to set language** on an OCR engine, turned on the handwritten‑text flag, and built a reusable function that **extract handwritten text** from any image. By following the steps above you can reliably **convert image to text**, whether you’re handling a single note or a massive archive of scanned documents.

Next, try experimenting with different language packs, batch‑process a folder of images, or integrate this logic into a web service that returns JSON results. The fundamentals stay the same, and the flexibility of the `ocr` library means you can adapt to almost any use case.

Got questions about edge cases, performance, or extending the script to other languages? Drop a comment or ping me on GitHub – happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}