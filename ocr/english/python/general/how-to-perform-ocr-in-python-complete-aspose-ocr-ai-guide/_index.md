---
category: general
date: 2026-06-25
description: Learn how to perform OCR in Python and discover the best way to load
  image for OCR, then boost accuracy with Aspose AI post‑processing.
draft: false
keywords:
- how to perform OCR
- load image for OCR
- Aspose OCR Python
- AI post‑processor OCR
- OCR accuracy improvement
- Python image processing OCR
language: en
og_description: How to perform OCR in Python? Follow this guide to load image for
  OCR, run basic recognition, and enhance results with Aspose AI post‑processing.
og_title: How to Perform OCR in Python – Full Aspose OCR & AI Tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Learn how to perform OCR in Python and discover the best way to load
    image for OCR, then boost accuracy with Aspose AI post‑processing.
  headline: How to Perform OCR in Python – Complete Aspose OCR & AI Guide
  type: TechArticle
- description: Learn how to perform OCR in Python and discover the best way to load
    image for OCR, then boost accuracy with Aspose AI post‑processing.
  name: How to Perform OCR in Python – Complete Aspose OCR & AI Guide
  steps:
  - name: Expected Output
    text: '``` === Raw OCR === Inv0ice #12345 Date: 2023-08-15 Total: $1,23O'
  - name: What if I don’t have a GPU?
    text: Set `model_config.gpu_layers = 0` and optionally increase `model_config.context_size`
      to 2048 for better CPU performance. The model will run slower, but you still
      get the same quality of correction.
  - name: My image is rotated—will `load_image` handle it?
    text: 'Aspose OCR automatically detects orientation, but for extremely skewed
      scans you may want to pre‑rotate using Pillow:'
  - name: How do I process multiple files in a folder?
    text: Wrap the whole pipeline in a `for` loop and store each `enhanced_text` in
      a list or write directly to a CSV. Remember to call `ocr_ai.free_resources()`
      **once** after the loop, not after each file—re‑initialising the model repeatedly
      is wasteful.
  - name: Can I swap the language model?
    text: Absolutely. Just change `model_config.hugging_face_repo_id` to any GGUF‑compatible
      model on Hugging Face (e.g., `Meta/Llama-3.2-1B-Instruct-GGUF`). Keep the quantization
      setting consistent with your hardware.
  type: HowTo
tags:
- OCR
- Python
- Aspose
- AI
title: How to Perform OCR in Python – Complete Aspose OCR & AI Guide
url: /python/general/how-to-perform-ocr-in-python-complete-aspose-ocr-ai-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Perform OCR in Python – Complete Aspose OCR & AI Guide

Ever wondered **how to perform OCR** in Python without wrestling with low‑level image tricks? You’re not alone. In this tutorial we’ll walk through loading an image for OCR, running plain text extraction, and then polishing the output with Aspose’s AI post‑processor. By the end you’ll have a ready‑to‑use script that turns noisy scans into clean, searchable text—no extra services required.

We’ll cover everything from installing the SDK to freeing resources in long‑running apps. If you’ve ever tried to **load image for OCR** and got a garbled mess, this guide is the antidote. You’ll see why combining traditional OCR with a language model yields results that look like they were typed by a human.

## Prerequisites

Before we dive in, make sure you have:

- Python 3.9 or newer (the code uses type hints that older interpreters don’t like)
- An active Aspose OCR license or a free trial (the community edition works for evaluation)
- A GPU with at least 4 GB VRAM if you want to speed up the AI model (optional but nice)
- A sample image, e.g., `sample_invoice.png`, placed somewhere you can reference

If any of these sound unfamiliar, don’t panic—installing the SDK is a one‑liner, and the GPU settings can be turned off later.

## Step 1: Install Aspose OCR and Dependencies

Open a terminal and run:

```bash
pip install aspose-ocr
pip install aspose-ocr-ai
```

The first package gives you `aspose.ocr`, the second adds the AI post‑processor utilities. Both are pure Python wheels, so you won’t need to compile anything yourself.

## Step 2: Load Image for OCR and Initialise the Engine

Now we’ll **load image for OCR** using Aspose’s `OcrEngine`. Think of this as handing a piece of paper to a very diligent clerk who reads every character.

```python
import aspose.ocr as aocr
import aspose.ocr.ai as aocr_ai

# Initialise the basic OCR engine
ocr_engine = aocr.OcrEngine()

# Load the image you want to process
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")

# Perform a plain OCR scan – this returns a raw string
raw_text = ocr_engine.recognize()
print("=== Raw OCR ===")
print(raw_text)
```

> **Why this matters:** The `load_image` call is the bridge between your file system and the OCR engine. If the path is wrong, you’ll get a `FileNotFoundError` before any recognition even starts. Always double‑check the directory separators, especially on Windows vs. macOS/Linux.

## Step 3: Set Up the Aspose AI Post‑Processor

Aspose AI can download a language model from Hugging Face, cache it locally, and run inference on your GPU (or CPU). Below we configure a lightweight 3‑billion‑parameter model that fits on most modern laptops.

```python
# Initialise the AI post‑processor
ocr_ai = aocr_ai.AsposeAI()
model_config = aocr_ai.AsposeAIModelConfig()

# Allow the SDK to fetch the model automatically
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
model_config.hugging_face_quantization = "int8"

# Use half of the GPU layers – balances speed and VRAM usage
model_config.gpu_layers = 20
model_config.context_size = 1024

# Load (or download) the model now
ocr_ai.initialize(model_config)
```

> **Tip:** If you’re on a CPU‑only machine, set `gpu_layers = 0`. The model will still run, just a bit slower. The `int8` quantization keeps the memory footprint tiny while preserving most of the model’s accuracy.

## Step 4: Register a Custom Post‑Processor

The AI model needs a prompt that tells it what to do. Here we ask it to act like an OCR proof‑reader, fixing spelling mistakes, merging broken words, and removing artefacts.

```python
def correction_processor(text, settings):
    prompt = (
        "You are an OCR post‑processor. Fix any spelling or OCR errors in the following "
        "text and return ONLY the cleaned version:\n\n"
        f"{text}"
    )
    # Temperature 0.0 makes the output deterministic
    return ocr_ai.run_inference(prompt, temperature=0.0, max_new_tokens=512)

# Hook the custom processor into the AI pipeline
ocr_ai.set_post_processor(correction_processor, custom_settings=None)
```

> **Why a custom processor?** The default post‑processor might add extra explanations or formatting you don’t need. By supplying our own function, we keep the output strictly the cleaned text, which is perfect for downstream indexing or database storage.

## Step 5: Run the AI‑Enhanced OCR Pipeline

Now we feed the raw OCR output into the AI layer. The engine will call our `correction_processor`, which in turn talks to the language model.

```python
# Apply the AI post‑processor to the raw OCR result
enhanced_text = ocr_ai.run_postprocessor(raw_text)

print("\n=== AI‑enhanced OCR ===")
print(enhanced_text)
```

You should see a noticeable improvement: missing characters are restored, common OCR mis‑reads like “0” vs “O” are corrected, and line breaks become more logical.

## Step 6: Clean‑Up – Free Resources

If you plan to run this inside a web service or a long‑running daemon, releasing GPU memory is crucial. Forgetting to call `free_resources` can lead to “out‑of‑memory” crashes after a few hundred requests.

```python
ocr_ai.free_resources()
```

That’s it—your full OCR pipeline is now production‑ready.

## Full Script Recap

Below is the complete, runnable example. Copy‑paste it into a file called `ocr_with_ai.py`, adjust the image path, and run `python ocr_with_ai.py`.

```python
import aspose.ocr as aocr
import aspose.ocr.ai as aocr_ai

# Step 1: Load image for OCR and perform basic recognition
ocr_engine = aocr.OcrEngine()
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")
raw_text = ocr_engine.recognize()
print("=== Raw OCR ===")
print(raw_text)

# Step 2: Initialise the Aspose AI post‑processor
ocr_ai = aocr_ai.AsposeAI()
model_config = aocr_ai.AsposeAIModelConfig()
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
model_config.hugging_face_quantization = "int8"
model_config.gpu_layers = 20          # half of GPU layers
model_config.context_size = 1024
ocr_ai.initialize(model_config)

# Step 3: Register custom correction processor
def correction_processor(text, settings):
    prompt = (
        "You are an OCR post‑processor. Fix any spelling or OCR errors in the following "
        "text and return ONLY the cleaned version:\n\n"
        f"{text}"
    )
    return ocr_ai.run_inference(prompt, temperature=0.0, max_new_tokens=512)

ocr_ai.set_post_processor(correction_processor, custom_settings=None)

# Step 4: Run AI post‑processor on raw OCR output
enhanced_text = ocr_ai.run_postprocessor(raw_text)
print("\n=== AI‑enhanced OCR ===")
print(enhanced_text)

# Step 5: Release resources (important for long‑running apps)
ocr_ai.free_resources()
```

### Expected Output

```
=== Raw OCR ===
Inv0ice #12345
Date: 2023-08-15
Total: $1,23O

=== AI‑enhanced OCR ===
Invoice #12345
Date: 2023-08-15
Total: $1,230
```

Notice how “Inv0ice” becomes “Invoice” and the stray “O” after the amount disappears. That’s the AI doing its magic.

## Common Questions & Edge Cases

### What if I don’t have a GPU?

Set `model_config.gpu_layers = 0` and optionally increase `model_config.context_size` to 2048 for better CPU performance. The model will run slower, but you still get the same quality of correction.

### My image is rotated—will `load_image` handle it?

Aspose OCR automatically detects orientation, but for extremely skewed scans you may want to pre‑rotate using Pillow:

```python
from PIL import Image
img = Image.open("sample.png")
rotated = img.rotate(90, expand=True)
rotated.save("rotated.png")
ocr_engine.load_image("rotated.png")
```

### How do I process multiple files in a folder?

Wrap the whole pipeline in a `for` loop and store each `enhanced_text` in a list or write directly to a CSV. Remember to call `ocr_ai.free_resources()` **once** after the loop, not after each file—re‑initialising the model repeatedly is wasteful.

```python
import os

for filename in os.listdir("invoices"):
    if filename.lower().endswith(".png"):
        ocr_engine.load_image(os.path.join("invoices", filename))
        raw = ocr_engine.recognize()
        clean = ocr_ai.run_postprocessor(raw)
        # Save or index `clean`
```

### Can I swap the language model?

Absolutely. Just change `model_config.hugging_face_repo_id` to any GGUF‑compatible model on Hugging Face (e.g., `Meta/Llama-3.2-1B-Instruct-GGUF`). Keep the quantization setting consistent with your hardware.

## Pro Tips & Pitfalls

- **Pro tip:** Set `temperature=0.0` for deterministic corrections. Higher temperatures can introduce creative but incorrect changes.
- **Watch out for:** Extremely long documents (> 5000 characters). The model’s context window is limited to 1024 tokens in the example; split the text into paragraphs before sending it to the AI.
- **Security note:** If you’re running this in a regulated environment, make sure the model download URL is whitelisted. The `allow_auto_download` flag can


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}