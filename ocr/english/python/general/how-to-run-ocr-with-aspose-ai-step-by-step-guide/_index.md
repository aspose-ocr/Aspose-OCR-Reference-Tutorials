---
category: general
date: 2026-02-09
description: how to run OCR using Aspose AI and a Hugging Face model – learn to download
  hugging face model, correct OCR errors and free GPU memory.
draft: false
keywords:
- how to run OCR
- download hugging face model
- free gpu memory
- how to free gpu
- correct OCR errors
language: en
og_description: how to run OCR with Aspose AI is explained in the first paragraph
  – discover how to download hugging face model, correct OCR errors and free GPU memory.
og_title: how to run OCR with Aspose AI – Complete Guide
tags:
- OCR
- Aspose
- AI
- HuggingFace
title: how to run OCR with Aspose AI – Step‑by‑Step Guide
url: /python/general/how-to-run-ocr-with-aspose-ai-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# how to run OCR with Aspose AI – Complete Guide

Ever wondered **how to run OCR** on a scanned invoice and get perfectly clean numbers without spending hours fixing typos? You're not alone. In many real‑world projects the raw text that comes out of a classic OCR engine still contains stray characters, broken currency symbols, or garbled digits—especially when the source image is noisy.  

The good news is that you can hook an LLM up to Aspose OCR, download a Hugging Face model on‑the‑fly, and let the AI polish the output for you. In this tutorial we’ll walk through the whole pipeline, from pulling the model (yes, we’ll show you how to **download hugging face model** automatically) to freeing up GPU resources when you’re done. By the end you’ll have a reproducible script that **corrects OCR errors**, runs fast on a modest GPU, and cleans up after itself so you don’t waste memory.

## What You’ll Learn

- Configure Aspose AI to fetch a **Qwen2.5‑3B‑Instruct‑GGUF** model from Hugging Face.
- Run the standard Aspose OCR engine on an image file.
- Use a custom LLM prompt that keeps numbers and currency symbols intact.
- Release GPU memory with the built‑in **free gpu memory** routine.
- Tweak the workflow for edge cases like multi‑page PDFs or low‑end GPUs.

> **Prerequisites** – Python 3.9+, `aspose-ocr` package, internet access for the first model download, and a GPU with at least 4 GB VRAM (optional but recommended). If you don’t have a GPU, the script will automatically fall back to CPU for the remaining layers.

---

## How to Run OCR and Enhance Results

Below is the full, ready‑to‑run Python script. Save it as `ocr_with_ai.py` and replace the placeholder paths with your own files.

```python
# ocr_with_ai.py
import aspose.ocr as aocr
from aspose.ocr.ai import AsposeAI, AsposeAIModelConfig

# -------------------------------------------------
# Step 1 – Configure the AI engine (download hugging face model)
# -------------------------------------------------
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",                     # auto‑download if missing
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",               # tiny memory footprint
    gpu_layers=20,                                  # 20 layers on GPU, rest on CPU
    directory_model_path=r"YOUR_DIRECTORY/Models"  # optional custom folder
)
ai = AsposeAI(ai_config)

# -------------------------------------------------
# Step 2 – Load an image and run the classic OCR engine
# -------------------------------------------------
ocr_engine = aocr.OcrEngine()
ocr_engine.load_image(r"YOUR_DIRECTORY/invoice.png")
raw_text = ocr_engine.recognize()   # returns plain‑text string

# -------------------------------------------------
# Step 3 – Register a custom LLM prompt (correct OCR errors)
# -------------------------------------------------
def financial_prompt():
    # Bias the model toward financial terminology
    return {"prompt": "Correct OCR errors, keep numbers and currency symbols intact"}

ai.set_post_processor("llm_correction", financial_prompt)

# -------------------------------------------------
# Step 4 – Let the LLM polish the output
# -------------------------------------------------
corrected_text = ai.run_postprocessor(raw_text)

print("Original :", raw_text)
print("Enhanced :", corrected_text)

# -------------------------------------------------
# Step 5 – Release resources (free gpu memory)
# -------------------------------------------------
ai.free_resources()
```

> **Pro tip:** The `gpu_layers` parameter lets you decide how many transformer layers stay on the GPU. If you’re hitting out‑of‑memory errors, lower this number and the rest will run on CPU – you’ll still **free gpu memory** later with `ai.free_resources()`.

### Expected Output

Running the script on a sample invoice yields something like:

```
Original : Invoic # 12345 \n Total: $1O0.00\n Date: 2023-07-15
Enhanced : Invoice # 12345
Total: $100.00
Date: 2023-07-15
```

Notice how the AI corrected the “O” in `$1O0.00` to a proper zero while preserving the dollar sign. That’s the essence of **correct OCR errors** for financial documents.

---

## Download Hugging Face Model – What Happens Under the Hood?

When you set `allow_auto_download="true"` the Aspose AI wrapper checks the `directory_model_path`. If the model files aren’t there, it reaches out to the Hugging Face Hub, pulls the **int8‑quantized** version of `Qwen2.5‑3B‑Instruct‑GGUF`, and stores it locally. This one‑time download is typically under 2 GB, making it feasible even on modest SSDs.

> **Why int8?** Quantizing to 8‑bit reduces memory usage dramatically—crucial when you also want to **free gpu memory** after processing. The trade‑off is a tiny hit to accuracy, but for post‑processing OCR text the impact is negligible.

If you prefer to host the model yourself, simply drop the `.gguf` files into `YOUR_DIRECTORY/Models` and Aspose will pick them up without hitting the internet again.

---

## How to Free GPU – Best Practices

GPU resources are a shared commodity on many workstations. Leaving tensors alive after your script finishes can cause “CUDA out of memory” errors for subsequent jobs. The `ai.free_resources()` call does three things:

1. **Disposes the underlying transformer** – all GPU‑resident weights are released.
2. **Clears the PyTorch cache** – `torch.cuda.empty_cache()` is invoked internally.
3. **Deletes temporary files** – any on‑disk caches created during the download are removed.

You can also manually invoke `torch.cuda.empty_cache()` if you’re mixing Aspose AI with other PyTorch workloads, but the built‑in method is usually sufficient.

---

## Step‑by‑Step Walk‑through (H2s with Secondary Keywords)

### Download Hugging Face Model Automatically

The `AsposeAIModelConfig` constructor hides the complexity of dealing with the Hugging Face API. Just make sure you have internet access the first time you run the script. After that, the model lives in `YOUR_DIRECTORY/Models`, and subsequent runs start instantly.

### Free GPU Memory After Inference

If you’re running this inside a long‑running service (e.g., a Flask API), call `ai.free_resources()` after each request. This prevents memory leaks and ensures that the next request can reuse the same GPU without hiccups.

### Correct OCR Errors with a Custom Prompt

Our `financial_prompt` function returns a dictionary with a single key `prompt`. You can tailor this to any domain:

```python
def medical_prompt():
    return {"prompt": "Fix OCR mistakes, keep dosage numbers and units unchanged"}
```

Swap the function name in `ai.set_post_processor(...)` and you’ve got a **correct OCR errors** pipeline for medical records.

### How to Run OCR on Multi‑Page PDFs

Aspose OCR can handle PDFs out of the box:

```python
ocr_engine.load_document(r"YOUR_DIRECTORY/multi_page.pdf")
raw_text = ocr_engine.recognize()  # concatenates pages automatically
```

After you get the raw string, the same LLM post‑processor will clean up each page’s text. No extra code needed.

### When You Don’t Have a GPU – How to Free GPU (Even Without One)

Even on CPU‑only machines, calling `ai.free_resources()` is harmless. It simply clears internal caches, which can still free up RAM. So the **how to free gpu** advice applies universally: always clean up after yourself.

---

## Common Pitfalls & How We Solved Them

| Issue | Why It Happens | Fix |
|-------|----------------|-----|
| **Out‑of‑Memory on GPU** | `gpu_layers` set too high for your card | Reduce `gpu_layers` to 10 or 5, let the rest run on CPU |
| **Model never downloads** | Corporate firewall blocks HTTPS to huggingface.co | Download the model manually on a different network, then point `directory_model_path` to the local folder |
| **Numbers get corrupted** | Prompt not explicit enough about keeping digits | Add “preserve all numeric values and currency symbols exactly as they appear” to the prompt |
| **`free_resources` raises an exception** | Using an older Aspose OCR version | Upgrade to the latest `aspose-ocr` package (pip install --upgrade aspose-ocr) |

---

## Full Example Recap

Here’s the script again, this time with inline comments that explain every line for future reference:

```python
import aspose.ocr as aocr
from aspose.ocr.ai import AsposeAI, AsposeAIModelConfig

# 1️⃣ Configure AI – will auto‑download the model if needed
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20,                     # adjust based on your GPU size
    directory_model_path=r"YOUR_DIRECTORY/Models"
)
ai = AsposeAI(ai_config)               # initialise the engine

# 2️⃣ Run classic OCR on an image (or PDF)
ocr_engine = aocr.OcrEngine()
ocr_engine.load_image(r"YOUR_DIRECTORY/invoice.png")
raw_text = ocr_engine.recognize()      # plain‑text result

# 3️⃣ Define a prompt that tells the LLM to keep numbers intact
def financial_prompt():
    return {"prompt": "Correct OCR errors, keep numbers and currency symbols intact"}

ai.set_post_processor("llm_correction", financial_prompt)

# 4️⃣ Let the LLM clean the text
corrected_text = ai.run_postprocessor(raw_text)

# 5️⃣ Show before/after
print("Original :", raw_text)
print("Enhanced :", corrected_text)

# 6️⃣ Clean up – this frees GPU memory for the next run
ai.free_resources()
```

---

## Conclusion

We’ve covered **how to run OCR** with Aspose, download a Hugging Face model on demand, craft a prompt that **corrects OCR errors**, and finally **free gpu memory** so your workstation stays responsive. The whole workflow fits into a single, self‑contained Python file—no external scripts, no manual model handling, and no lingering GPU allocations.

Next steps? Try swapping the `financial_prompt` for a

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}