---
category: general
date: 2026-01-07
description: How to run OCR and extract text from image for invoice processing. Learn
  to improve OCR accuracy, load image for OCR, and process invoice OCR efficiently.
draft: false
keywords:
- how to run ocr
- extract text from image
- improve ocr accuracy
- load image for ocr
- process invoice ocr
language: en
og_description: How to run OCR on invoices step‑by‑step. Extract text from image,
  improve OCR accuracy, and load image for OCR using Aspose AI.
og_title: How to Run OCR on Invoices – Complete Python Guide
tags:
- OCR
- Python
- Image Processing
title: How to Run OCR on Invoices – Extract Text from Image with Python
url: /python/general/how-to-run-ocr-on-invoices-extract-text-from-image-with-pyth/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Run OCR on Invoices – Extract Text from Image with Python

Ever wondered **how to run OCR** on a scanned invoice and get clean, searchable text? You're not alone. Many developers hit a wall when the raw OCR output is riddled with misspellings, broken line breaks, and missing punctuation. In this tutorial we’ll walk through a full‑stack solution that not only **extracts text from image** but also **improves OCR accuracy** by post‑processing with an Aspose AI model.

You’ll see how to **load image for OCR**, run the built‑in engine, and then apply a lightweight spell‑check that makes the result ready for downstream analytics. By the end, you’ll have a reusable script that can be dropped into any invoice‑processing pipeline.

> **What you’ll need**  
> * Python 3.9 or newer  
> * `aspose-ocr` and `aspose-ai` packages (installed via `pip`)  
> * An invoice image (PNG, JPEG, or TIFF) – we’ll use `sample_invoice.png` as an example  
> * Optional: a GPU with at least 4 GB VRAM for faster model inference (the script works on CPU too)

---

## Step 1: Install Required Packages and Prepare the Environment

Before we can **load image for OCR**, we must ensure the necessary libraries are available. The Aspose OCR engine ships with a simple Python wrapper, while the AI post‑processor relies on a Hugging Face quantized model.

```bash
# Install Aspose OCR and AI packages
pip install aspose-ocr aspose-ai
```

> **Pro tip:** If you plan to use GPU acceleration, install `torch` with CUDA support (`pip install torch --extra-index-url https://download.pytorch.org/whl/cu121`).

---

## Step 2: Load the Invoice Image

Loading the image is straightforward, but it’s worth mentioning why we explicitly set the path as a raw string (`r"..."`). This prevents accidental escape‑character mishaps on Windows paths.

```python
import aspose.ocr as ocr

# Define the path to your invoice image
image_path = r"YOUR_DIRECTORY/sample_invoice.png"

# Initialize the OCR engine and attach the image
engine = ocr.OcrEngine()
engine.image = ocr.Image.load(image_path)
```

*Why this matters:* Using `ocr.Image.load` guarantees the image is pre‑processed (binarization, deskew) according to Aspose’s optimal defaults, which already **improves OCR accuracy** before any AI magic happens.

---

## Step 3: Run the Built‑In OCR Engine

Now we actually **run OCR** and capture the raw text. This step shows the typical output you’d get from a vanilla OCR run—often a mess of line breaks and occasional misspellings.

```python
# Perform OCR
engine.recognize()
raw_text = engine.recognized_text

print("Raw OCR output:")
print(raw_text)
```

**Typical raw output** (truncated for brevity):

```
INVOICE NO: 2023‑00123
Date: 06/15/2023
Bill To:
Acme Corp
123 Main St
...
Total Due: $1,250.00
```

You might notice that “Invoice” appears as “Invo1ce” or that punctuation is missing. That’s where the AI post‑processor steps in.

---

## Step 4: Configure the Aspose AI Model

The AI model we’ll use is **Qwen2.5‑3B‑Instruct‑GGUF**, a lightweight instruction‑tuned LLM that runs comfortably on a mid‑range GPU. The configuration below tells Aspose where to fetch the model, how many layers to keep on GPU, and the context size for handling long paragraphs.

```python
from aspose.ai import AsposeAI, AsposeAIModelConfig

model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="q4_k_m",
    gpu_layers=30,               # 30 layers on GPU, remainder on CPU
    context_size=4096            # larger context for long paragraphs
)

ai = AsposeAI()
ai.initialize(model_config)   # you could also pass `model_config` to the constructor
```

> **Why this config?**  
> * `gpu_layers=30` balances speed and memory—most inference happens on the GPU, while the remaining layers stay on CPU to avoid OOM errors.  
> * `context_size=4096` ensures the model can see the whole invoice at once, preventing it from truncating important fields.

---

## Step 5: Create a Simple Spell‑Check Post‑Processor

We’ll wrap the AI call in a tiny function called `simple_spell_check`. The prompt is deliberately concise: “Correct spelling and punctuation:” followed by the raw OCR text. The model returns a cleaned‑up version.

```python
def simple_spell_check(text):
    prompt = f"Correct spelling and punctuation:\n{text}"
    return ai.run_prompt(prompt)

# Register the post‑processor with the AI instance
ai.set_post_processor(simple_spell_check, None)
```

**How it works:** `ai.run_prompt` sends the prompt to the locally loaded LLM, which then returns a single string with corrected spelling, proper punctuation, and a more natural line‑break layout.

---

## Step 6: Apply the Post‑Processor to the Raw OCR Text

Now the magic happens. We feed the raw OCR output into our post‑processor and print the enhanced result.

```python
enhanced_text = ai.run_postprocessor(raw_text)

print("\nAI‑enhanced OCR output:")
print(enhanced_text)
```

**Sample enhanced output**:

```
Invoice No: 2023‑00123
Date: 06/15/2023
Bill To:
Acme Corp
123 Main St
...
Total Due: $1,250.00
```

Notice the corrected “Invoice” spelling, proper colon usage, and consistent line breaks—exactly what you need for reliable downstream parsing.

---

## Step 7: Clean Up Resources

Both the OCR engine and the AI model allocate native resources. It’s good practice to free them when you’re done, especially in long‑running services.

```python
ai.free_resources()
engine.dispose()
```

---

## Full Script – Ready to Paste

Below is the complete, runnable script that ties every step together. Save it as `invoice_ocr.py`, replace `YOUR_DIRECTORY` with the folder containing your invoice image, and execute with `python invoice_ocr.py`.

```python
# invoice_ocr.py
import aspose.ocr as ocr
from aspose.ai import AsposeAI, AsposeAIModelConfig

# -------------------------------------------------
# Step 1: Load the image to be processed
# -------------------------------------------------
image_path = r"YOUR_DIRECTORY/sample_invoice.png"
engine = ocr.OcrEngine()
engine.image = ocr.Image.load(image_path)

# -------------------------------------------------
# Step 2: Run the built‑in OCR engine and obtain raw text
# -------------------------------------------------
engine.recognize()
raw_text = engine.recognized_text
print("Raw OCR output:")
print(raw_text)

# -------------------------------------------------
# Step 3: Configure the Aspose AI model for post‑processing
# -------------------------------------------------
model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="q4_k_m",
    gpu_layers=30,
    context_size=4096
)

ai = AsposeAI()
ai.initialize(model_config)   # alternatively, pass config to the constructor

# -------------------------------------------------
# Step 4: Define a simple spell‑check post‑processor
# -------------------------------------------------
def simple_spell_check(text):
    prompt = f"Correct spelling and punctuation:\n{text}"
    return ai.run_prompt(prompt)

ai.set_post_processor(simple_spell_check, None)

# -------------------------------------------------
# Step 5: Apply the post‑processor to the raw OCR text
# -------------------------------------------------
enhanced_text = ai.run_postprocessor(raw_text)
print("\nAI‑enhanced OCR output:")
print(enhanced_text)

# -------------------------------------------------
# Step 6: Release resources
# -------------------------------------------------
ai.free_resources()
engine.dispose()
```

Run the script and you’ll see both the noisy raw OCR dump and the polished, **improved OCR accuracy** version side by side.

---

## Frequently Asked Questions & Edge Cases

### 1. What if my invoice image is a multi‑page PDF?

Aspose OCR can directly load PDF pages. Replace the image load line with:

```python
engine.image = ocr.Image.load("invoice.pdf", page_index=0)  # 0‑based page number
```

Iterate `page_index` to process each page sequentially.

### 2. My GPU runs out of memory—can I use CPU only?

Absolutely. Set `gpu_layers=0` in the `AsposeAIModelConfig`. The model will run entirely on CPU, which is slower but safe for low‑end hardware.

### 3. How do I handle non‑English invoices?

Swap the model repository ID for a language‑specific model, e.g., `"mistralai/Mistral-7B-Instruct-v0.2"` for multilingual support. The rest of the pipeline stays unchanged.

### 4. Can I chain multiple post‑processors (e.g., format dates, extract totals)?

Yes. `ai.set_post_processor` accepts a list of callables. For example:

```python
def extract_totals(text):
    # simple regex to pull monetary values
    import re
    totals = re.findall(r"\$\d+(?:,\d{3})*(?:\.\d{2})?", text)
    return "\n".join(totals)

ai.set_post_processor([simple_spell_check, extract_totals], None)
```

The output will first be spell‑checked, then have totals extracted.

---

## Performance Tips & Best Practices

| Tip | Why it Helps |
|-----|---------------|
| **Batch multiple invoices** – load them into a list and process in a loop. | Reduces Python interpreter overhead and keeps the AI model warm in memory. |
| **Cache the model** – avoid calling `initialize` repeatedly in a web service. | Model loading can take ~30 seconds; caching yields instant responses. |
| **Resize large images** to 1500 px width before OCR. | Smaller images speed up both OCR and AI inference without sacrificing accuracy. |
| **Set `allow_auto_download="false"` in production** – ship the model with your deployment. | Guarantees deterministic startup times and avoids network hiccups. |

---

## Conclusion

We’ve covered **how to run OCR** on invoices, from loading the image to polishing the result with an AI‑driven spell‑check. By following these steps you can reliably **extract text from image**, **improve OCR accuracy**, and seamlessly **process invoice OCR** in any Python‑based workflow.

Give it a spin with a few different invoice layouts—maybe a handwritten receipt or a scanned contract. The same pipeline adapts with minimal tweaks, proving that a well‑structured OCR + AI combo is a versatile tool for any document‑automation project.

If you found this guide helpful, consider sharing it with teammates or starring the repository that hosts the Aspose packages

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}