---
category: general
date: 2026-03-18
description: basic ocr python tutorial shows how to convert TIFF to text, load image
  OCR, set GPU layers, and fix leading zeroes with Aspose AI.
draft: false
keywords:
- basic ocr python
- convert tiff to text
- load image ocr
- set gpu layers
- fix leading zeroes
language: en
og_description: basic ocr python tutorial walks you through converting TIFF files
  to clean text, loading images, setting GPU layers, and fixing leading zeroes.
og_title: basic ocr python – convert TIFF to text
tags:
- OCR
- Python
- AI
- Aspose
title: basic ocr python – convert TIFF to text
url: /python/general/basic-ocr-python-convert-tiff-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# basic ocr python – Convert TIFF to Text with AI Post‑Processing

Looking for a way to do **basic ocr python** on your scanned documents? In this guide we’ll walk through converting a TIFF file to clean, searchable text using Aspose OCR and an AI post‑processor.  

If you’ve ever struggled to **convert TIFF to text** because the raw output is riddled with typos or odd symbols, you’re not alone. We’ll also show you how to **load image OCR**, tweak the engine to **set GPU layers**, and even **fix leading zeroes** that commonly appear in invoice numbers.

## What You’ll Learn

- How to initialise the Aspose OCR engine for printed documents.  
- The exact steps to **load image OCR** from a TIFF file and get raw text.  
- Configuring an AI model, downloading it automatically, and **setting GPU layers** for faster inference.  
- Adding built‑in spell‑check plus a custom function that **fixes leading zeroes**.  
- Cleaning the OCR result and releasing resources properly.  

By the end of this tutorial you’ll have a single, reusable Python script that turns any TIFF into polished, searchable text—no manual copy‑pasting required.  

### Prerequisites

- Python 3.8+ installed on your machine.  
- `aspose-ocr` package (`pip install aspose-ocr`).  
- Optional: a GPU with at least 4 GB VRAM if you want to **set GPU layers**; otherwise the code falls back to CPU automatically.  

---

## basic ocr python – load image and recognize text

The first thing we need to do is **load image OCR** so the engine can read the pixels. Aspose’s `OcrEngine` handles many formats, but here we focus on TIFF because it’s the most common for scanned invoices.

```python
import aspose.ocr as ocr

# Initialise the OCR engine for printed documents
ocr_engine = ocr.OcrEngine()
ocr_engine.set_recognition_mode(ocr.RecognitionMode.PRINTED)   # use HANDWRITTEN for handwritten docs

# Load the TIFF file – replace with your own path
ocr_engine.load_image("YOUR_DIRECTORY/input.tif")
```

> **Pro tip:** If you’re dealing with multi‑page TIFFs, Aspose automatically processes each page in sequence, so you don’t need extra loops.

Now that the image is loaded, let’s run a basic recognition pass.

```python
# Perform basic OCR and capture the raw string
raw_text = ocr_engine.recognize()
print("Raw OCR:", raw_text)
```

You’ll see something like:

```
Raw OCR: Inv0ce N0: 0123AB4
Total Amt: $1,200.00
Date: 2024-07-15
```

Notice the *zeroes* before the letters? That’s a classic OCR artifact we’ll clean up later.

![basic ocr python workflow](/images/ocr-workflow.png "basic ocr python workflow diagram")

---

## Step 2: Convert TIFF to text – prepare the AI post‑processor

Raw OCR is useful, but most production pipelines need a polished version. Aspose provides an `AsposeAI` wrapper that can download a model from Hugging Face, run it on the GPU, and apply spell‑check automatically.

```python
from aspose.ocr.ai import AsposeAI, AsposeAIModelConfig

# Configure the AI model – we’ll download Qwen2.5‑3B‑Instruct automatically
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",
    directory_model_path="YOUR_DIRECTORY/ocr_ai_models",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=25          # <-- this is where we **set GPU layers**
)

ocr_ai = AsposeAI(ai_config)
```

### Why `set GPU layers` matters

The `gpu_layers` parameter tells the underlying GGUF model how many transformer layers to keep on the GPU. More layers = faster inference but higher VRAM usage. If you’re on a modest laptop, drop the value to `10` or omit it entirely to stay on CPU.

---

## Step 3: Apply spellcheck and **fix leading zeroes**

Aspose AI ships with a built‑in spell‑checker, which catches most English misspellings. However, domain‑specific fixes—like turning a leading `0` into an `O` for invoice codes—require a custom post‑processor.

```python
# Enable the built‑in spell‑check
ocr_ai.set_post_processor("spellcheck")

# Custom function to replace a leading zero before three capital letters
def invoice_fix(txt: str) -> str:
    import re
    # Example: "0ABC" -> "OABC"
    return re.sub(r"\b0([A-Z]{3})\b", r"O\1", txt)

# Register the custom fix – it runs after spellcheck
ocr_ai.set_post_processor(invoice_fix)
```

> **Why this works:** The regular expression looks for a word boundary (`\b`), a zero, then exactly three capital letters. It then substitutes the zero with the letter “O”. You can extend the pattern for other quirks (e.g., `0[0-9]{2}` for mis‑read numbers).

---

## Step 4: Clean the OCR result with the AI post‑processor

Now we combine everything: the raw string from **basic ocr python**, the spell‑check, and our zero‑fix. The `run_postprocessor` method returns a cleaned version ready for downstream systems.

```python
cleaned_text = ocr_ai.run_postprocessor(raw_text)
print("\nCleaned OCR:", cleaned_text)
```

Typical output after the post‑processor:

```
Cleaned OCR: Invoice No: O123AB4
Total Amt: $1,200.00
Date: 2024-07-15
```

You can see that the leading zero has turned into an `O`, and common misspellings are corrected. The text is now suitable for indexing in a search engine or feeding into a data‑extraction pipeline.

---

## Step 5: Release AI resources – keep your GPU happy

If you’re running multiple OCR jobs in a long‑running service, it’s good practice to free the model’s GPU memory when you’re done.

```python
ocr_ai.free_resources()
```

Skipping this step can lead to “out‑of‑memory” errors on subsequent calls, especially when **set GPU layers** to a high value.

---

## Optional Variations & Edge Cases

| Situation | What to change |
|-----------|----------------|
| **Handwritten documents** | Use `ocr_engine.set_recognition_mode(ocr.RecognitionMode.HANDWRITTEN)` instead of `PRINTED`. |
| **No GPU available** | Set `gpu_layers=0` or omit the argument; the model will run on CPU (slower but safe). |
| **Different language** | Swap the Hugging Face repo ID to a language‑specific model, e.g., `microsoft/Florence-2-base`. |
| **Batch processing** | Wrap the steps in a `for file in glob("*.tif"):` loop and accumulate results in a list or CSV. |
| **More complex zero patterns** | Extend `invoice_fix` with additional regexes, such as `r"\b0+([A-Z]{2,})\b"` for multiple leading zeroes. |

---

## Conclusion

We’ve just completed a **basic ocr python** pipeline that loads a TIFF, extracts raw text, and then cleans it using an AI model while **setting GPU layers** for performance. The custom post‑processor demonstrates how to **fix leading zeroes**, a small but often‑overlooked detail that can break downstream analytics.

Feel free to experiment: try a different quantization (`float16` for higher accuracy), swap the spell‑check for a domain‑specific dictionary, or chain multiple custom fixes together. The pattern stays the same—load, recognize, configure AI, post‑process, and clean up.

**Next steps** you might explore include:

- Integrating the cleaned output with a database or Elasticsearch index.  
- Using the same approach to **convert TIFF to text** for multi‑language PDFs.  
- Adding a UI with Flask or FastAPI so non‑technical users can upload files and receive cleaned text instantly.  

Happy coding, and may your OCR results always be crisp and zero‑free!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}