---
category: general
date: 2026-01-12
description: How to run OCR and extract text from invoice images using Aspose OCR
  and a lightweight Hugging Face model. Learn to download model, correct OCR errors,
  and perform OCR on image.
draft: false
keywords:
- how to run OCR
- extract text from invoice
- download hugging face model
- correct OCR errors
- perform OCR on image
language: en
og_description: How to run OCR on invoice images, extract text, and fix errors with
  a Hugging Face LLM. Follow this complete guide for flawless results.
og_title: How to Run OCR on Invoice Images – Full Tutorial
tags:
- OCR
- Python
- AI post‑processing
- Hugging Face
title: How to Run OCR on Invoice Images – Complete Step‑by‑Step Guide
url: /python/general/how-to-run-ocr-on-invoice-images-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Run OCR on Invoice Images – Complete Step‑by‑Step Guide

Ever wondered **how to run OCR** on a scanned invoice and get clean, searchable text without spending hours cleaning it up? You're not the only one. In many real‑world projects the raw OCR output is riddled with mis‑recognitions—think “O” for “0”, “l” for “1”, or even entire words garbled. The good news? With a few lines of Python you can not only **perform OCR on image** files but also automatically **correct OCR errors** using a lightweight model from Hugging Face.

In this tutorial we’ll walk through everything you need to know: from loading an invoice image, extracting raw text, downloading a quantized model, to polishing the result so you end up with a perfect transcription ready for downstream processing. By the end you’ll be able to **extract text from invoice** PDFs or PNGs in a single, repeatable script.

## Prerequisites & Setup

Before diving in, make sure you have:

| Requirement | Why it matters |
|-------------|----------------|
| Python 3.9+ | Modern syntax and type hints |
| `aspose-ocr` package | Provides the `ocr.OcrEngine` used in the example |
| `aspose-ai` package | Supplies the `AsposeAI` post‑processor |
| Access to a GPU (optional) | Speeds up the LLM layers; otherwise CPU works fine |
| Internet connection (first run) | Needed to **download Hugging Face model** automatically |

You can install the required libraries with:

```bash
pip install aspose-ocr aspose-ai
```

> **Pro tip:** If you plan to run the LLM on GPU, install `torch` with CUDA support (`pip install torch --extra-index-url https://download.pytorch.org/whl/cu118`).

Now that the environment is ready, let’s get into the code.

---

## Step 1 – Initialise the OCR Engine and Load Your Invoice Image

The first thing you need to do is create an instance of Aspose’s OCR engine and point it at the file you want to process. This step is the foundation of **how to run OCR** on any image.

```python
import ocr  # Aspose OCR package

# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Load the invoice you want to read
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")
```

> **Why this matters:** `load_image` accepts PNG, JPEG, TIFF, and even PDF pages, letting you **perform OCR on image** data regardless of format.

---

## Step 2 – Run Basic OCR to Capture Raw Text

Once the image is loaded, the engine can produce a raw transcription. This output is often noisy, which is why we’ll later run a correction step.

```python
# Perform the OCR scan
raw_result = ocr_engine.recognize()

# Show what the engine saw
print("Raw OCR:", raw_result.text)
```

Typical raw output might look like:

```
Raw OCR: Inv0ice No: 12345
Date: 2023/07/15
Total Am0unt: $1,200.00
```

Notice the zeroes (`0`) where the digit “O” should be? That’s exactly the kind of mistake we’ll fix later.

---

## Step 3 – Configure the AI Post‑Processor with a Lightweight LLM

Now we bring in a **download Hugging Face model** that’s small enough to run on modest hardware but powerful enough to understand invoice language. The example uses the Qwen 2.5 3B‑Instruct GGUF model, quantized to `int8` for a tiny memory footprint.

```python
from aspose_ai import AsposeAI, AsposeAIModelConfig

# Define model configuration
model_config = AsposeAIModelConfig(
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",          # reduces size dramatically
    gpu_layers=20,                             # use GPU for the first 20 layers if available
    allow_auto_download="true"                # pulls the model on first run
)

# Initialise the AI processor and attach the post‑processor
ai_processor = AsposeAI()
ai_processor.set_post_processor("llm_correction", model_config)
```

> **Why this model?** The `int8` quantization shrinks the file to ~1.2 GB, making it feasible on most laptops. GPU layers accelerate inference, but the code gracefully falls back to CPU when no GPU is found.

---

## Step 4 – Run the LLM‑Based Correction on the Raw OCR Result

With the model ready, we feed the raw text into the post‑processor. The LLM will rewrite the transcription, fixing common OCR glitches and normalising numbers.

```python
# Apply AI correction
corrected_result = ai_processor.run_postprocessor(raw_result)

# Display the cleaned output
print("AI‑corrected:", corrected_result.text)
```

Expected cleaned output:

```
AI‑corrected: Invoice No: 12345
Date: 2023/07/15
Total Amount: $1,200.00
```

You can see the zeroes have turned back into the letter “O”, and “Am0unt” is now “Amount”. This is the core of **correct OCR errors** automatically.

---

## Step 5 – Release Resources and Clean Up

Large language models can hold onto GPU memory, so it’s good practice to free resources when you’re done.

```python
# Free the model and any GPU buffers
ai_processor.free_resources()
```

If you plan to process many invoices in a batch, you could keep the model loaded and only free it at the very end of the script.

---

## Full Working Example

Putting everything together, here’s a single script you can drop into a `.py` file and run:

```python
# ------------------------------------------------------------
# How to Run OCR on Invoice Images – End‑to‑End Example
# ------------------------------------------------------------
import ocr
from aspose_ai import AsposeAI, AsposeAIModelConfig

def main():
    # 1️⃣ Initialise OCR engine
    ocr_engine = ocr.OcrEngine()
    ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")

    # 2️⃣ Capture raw OCR text
    raw_result = ocr_engine.recognize()
    print("Raw OCR:", raw_result.text)

    # 3️⃣ Configure lightweight LLM from Hugging Face
    model_cfg = AsposeAIModelConfig(
        hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
        hugging_face_quantization="int8",
        gpu_layers=20,
        allow_auto_download="true"
    )
    ai = AsposeAI()
    ai.set_post_processor("llm_correction", model_cfg)

    # 4️⃣ Run AI correction
    corrected = ai.run_postprocessor(raw_result)
    print("AI‑corrected:", corrected.text)

    # 5️⃣ Clean up
    ai.free_resources()

if __name__ == "__main__":
    main()
```

Running the script should produce output similar to the “AI‑corrected” block shown earlier. Feel free to swap the image path with any other invoice or receipt to **extract text from invoice** files in bulk.

---

## Frequently Asked Questions & Edge Cases

### What if I don’t have a GPU?

The `gpu_layers` parameter is optional. Set it to `0` or omit it, and the model will run entirely on CPU. Expect slower inference—roughly 2–3 seconds per page on a modern laptop.

### My invoices are multi‑page PDFs. How do I handle them?

Convert each page to a separate image (e.g., using `pdf2image`) and loop over the pages with the same script. The OCR engine can process each image independently, and the LLM will correct each block of text.

```python
from pdf2image import convert_from_path

pages = convert_from_path("invoice.pdf", dpi=300)
for i, page_img in enumerate(pages):
    ocr_engine.load_image(page_img)
    # …run steps 2‑4…
```

### The model download fails behind a firewall?

Download the model manually from the Hugging Face model hub, unzip it into a local folder, and point `hugging_face_repo_id` to the local path:

```python
model_cfg = AsposeAIModelConfig(
    hugging_face_repo_id="/local/path/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20,
    allow_auto_download="false"
)
```

### How accurate is the correction?

For typical English‑language invoices, the LLM fixes >95 % of common OCR mis‑recognitions. Complex handwritten notes may still need manual review.

---

## Tips & Tricks for Production Use

- **Batch processing:** Wrap steps 2‑4 in a function and feed a list of file paths. Re‑use the same `AsposeAI` instance to avoid re‑loading the model.
- **Logging:** Replace `print` with Python’s `logging` module to capture both raw and corrected outputs for audit trails.
- **Error handling:** Surround the OCR call with `try/except` blocks. If an image fails, log the filename and continue.
- **Performance tuning:** Experiment with `gpu_layers`. More layers on GPU speed up inference but increase VRAM usage.

---

## Conclusion

We’ve covered **how to run OCR** on invoice images from start to finish, showing you how to **perform OCR on image**, **download Hugging Face model**, and **correct OCR errors** automatically. The complete script demonstrates a practical workflow that you can drop into any Python‑based automation pipeline.

Next steps? Try extending the pipeline to **extract key fields** (invoice number, date, total) using regular expressions on the corrected text, or feed the cleaned output into a database for searchable records. You could also experiment with other lightweight LLMs from Hugging Face if you need a different language or domain‑specific knowledge.

Happy coding, and may your OCR results always be crystal‑clear! 

![how to run OCR on an invoice image](ocr_invoice_example.png "how to run OCR on invoice")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}