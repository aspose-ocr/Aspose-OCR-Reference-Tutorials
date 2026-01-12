---
category: general
date: 2026-01-12
description: How to run OCR on PDFs using Aspose OCR, load PDF OCR, enable handwritten
  OCR mode and integrate a Hugging Face OCR model for post‑processing.
draft: false
keywords:
- how to run OCR
- load pdf OCR
- handwritten OCR mode
- hugging face OCR model
language: en
og_description: How to run OCR on PDFs with Aspose OCR, enable handwritten OCR mode
  and boost accuracy using a Hugging Face OCR model.
og_title: How to Run OCR on PDFs – Complete Tutorial
tags:
- OCR
- Python
- Aspose
- Hugging Face
title: How to Run OCR on PDFs – Step‑by‑Step Guide with Handwritten Mode
url: /python/general/how-to-run-ocr-on-pdfs-step-by-step-guide-with-handwritten-m/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Run OCR on PDFs – Complete Tutorial

Ever wondered **how to run OCR** on a multi‑language PDF that contains messy handwriting? You're not alone. In many real‑world projects—think invoice digitization or archival of historic letters—plain text extraction just isn’t enough. This guide shows you exactly how to run OCR on PDFs, load PDF OCR, switch to handwritten OCR mode, and then polish the results with a **Hugging Face OCR model** for spelling and grammar fixes.

We'll walk through everything you need: from installing the Aspose OCR Cloud SDK, to configuring GPU acceleration, to wiring up a lightweight Qwen model from Hugging Face. By the end you’ll have a ready‑to‑run script that you can drop into any Python project.

> **Prerequisites**  
> • Python 3.9 or newer  
> • An Aspose OCR Cloud license (set as an environment variable)  
> • Optional: a CUDA‑compatible GPU for faster inference  

---

## What This Tutorial Covers

- Activating the Aspose OCR license from the environment  
- Loading a PDF with `load_pdf OCR` and enabling **handwritten OCR mode**  
- Running structured OCR to get block‑level text and language data  
- Setting up a **Hugging Face OCR model** (Qwen 2.5‑3B‑Instruct) for post‑processing  
- Applying spell‑checking and grammar correction block by block  
- Cleaning up AI resources to avoid memory leaks  

If you’ve ever tried a vanilla OCR engine and got gibberish on handwritten notes, the “handwritten OCR mode” flag is the game‑changer you’ve been missing. And thanks to the Hugging Face model, you’ll also get a professional‑grade polish without leaving your Python environment.

---

![how to run OCR diagram](https://example.com/ocr-workflow.png "how to run OCR")

*Image alt text: how to run OCR workflow diagram*

---

## Step 1: Install Required Packages

First, make sure the Aspose OCR Cloud SDK and the `transformers` library are installed. Run the following in your terminal:

```bash
pip install aspose-ocr-cloud transformers huggingface-hub
```

> **Pro tip:** If you plan to use GPU acceleration, also install `torch` with CUDA support (`pip install torch==2.2.0+cu121 -f https://download.pytorch.org/whl/torch_stable.html`).

---

## Step 2: Activate the Aspose OCR License

Activating the license from an environment variable keeps your key out of source control. Set `ASPOSE_OCR_LICENSE` in your shell, then call `activate_from_env()`:

```python
import asposeocrcloud as ocr

# Pull the license string from the ASPOSE_OCR_LICENSE environment variable
ocr.activate_from_env()
```

> Why this matters: Without a valid license the SDK falls back to a trial mode that limits page count and disables GPU usage.

---

## Step 3: Initialise the OCR Engine in Handwritten Mode

We create an `OcrEngine`, turn on GPU (if available), and explicitly request **handwritten OCR mode**. This mode tweaks the underlying neural network to better handle cursive strokes.

```python
# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Enable GPU acceleration – optional but speeds up large PDFs dramatically
ocr_engine.set_use_gpu(True)

# Switch to handwritten recognition mode for better accuracy on cursive text
ocr_engine.set_recognition_mode(ocr.RecognitionMode.HANDWRITTEN)
```

> **Note:** If you don’t have a GPU, `set_use_gpu(False)` still works; the engine will fall back to CPU.

---

## Step 4: Load Your PDF and Run Structured OCR

Now we actually **load PDF OCR**. The `load_image` method accepts PDF, TIFF, JPG, etc. Structured OCR returns blocks that contain both the raw text and detected language.

```python
# Replace the path with your own PDF location
pdf_path = "YOUR_DIRECTORY/multilingual_handwritten.pdf"
ocr_engine.load_image(pdf_path)

# Perform structured OCR – returns a hierarchy of blocks
structured_result = ocr_engine.recognize_structured()
```

The `structured_result.blocks` list might look like this (truncated for brevity):

```python
[
    Block(text="Bonjour le monde", language="fr"),
    Block(text="Hello world", language="en"),
    Block(text="こんにちは世界", language="ja")
]
```

---

## Step 5: Configure a Hugging Face OCR Model for Post‑Processing

We’ll use the **Qwen 2.5‑3B‑Instruct** model from Hugging Face, quantized to `int8` for a small memory footprint. The `AsposeAIModelConfig` wrapper tells the Aspose AI post‑processor how to download and run the model.

```python
from asposeocrcloud import AsposeAI, AsposeAIModelConfig

model_cfg = AsposeAIModelConfig(
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=25,                # Number of transformer layers to keep on GPU
    allow_auto_download="true"   # Auto‑download the model if not cached
)

spell_corrector = AsposeAI()
spell_corrector.set_post_processor("spell_corrector", model_cfg)
```

> **Why this model?** Qwen 2.5‑3B‑Instruct balances speed and quality. The `int8` quantization reduces RAM usage to ~4 GB, making it feasible on most modern laptops.

---

## Step 6: Apply Spell‑Checking Block by Block

We loop through each OCR block, hand it to the AI post‑processor, and print the corrected text along with its detected language. This is the core of the **load PDF OCR → post‑process** pipeline.

```python
for block in structured_result.blocks:
    # Run the correction; `run_postprocessor` returns an object with a .text attribute
    corrected = spell_corrector.run_postprocessor(block)
    print(f"[{block.language}] {corrected.text}")
```

### Expected Output

```
[fr] Bonjour le monde
[en] Hello world
[ja] こんにちは世界
```

If the original OCR had misspellings like “Helllo wrold”, the model would output the corrected version.

---

## Step 7: Clean Up AI Resources

Always free GPU memory when you’re done. The `free_resources()` call unloads the model and clears the CUDA cache.

```python
spell_corrector.free_resources()
```

---

## Common Pitfalls & How to Avoid Them

| Issue | Symptom | Fix |
|-------|----------|-----|
| **GPU not detected** | `set_use_gpu(True)` silently falls back to CPU | Verify CUDA drivers (`nvidia-smi`) and install the correct `torch` wheel |
| **Model download fails** | `allow_auto_download` throws a network error | Ensure outbound HTTPS is allowed, or manually download the GGUF file and point `hugging_face_repo_id` to the local path |
| **Handwritten text still garbled** | Low confidence scores in `structured_result` | Increase `set_recognition_mode` to `HANDWRITTEN` (already done) and consider pre‑processing the PDF with image sharpening (`opencv`) before OCR |
| **Out‑of‑memory on GPU** | `RuntimeError: CUDA out of memory` | Reduce `gpu_layers` (e.g., to 10) or switch to CPU inference (`set_use_gpu(False)`) |

---

## Extending the Workflow

- **Batch processing:** Wrap the whole script in a function that accepts a list of PDF paths and writes corrected output to separate `.txt` files.  
- **Custom vocabularies:** If your domain uses specialized terminology (e.g., medical acronyms), fine‑tune the Hugging Face model with a small dataset.  
- **Alternative models:** Swap `Qwen/Qwen2.5-3B-Instruct-GGUF` for `mistralai/Mistral-7B-Instruct-v0.2` if you need a larger context window.

---

## Conclusion

You now know **how to run OCR** on PDFs, load PDF OCR, enable **handwritten OCR mode**, and boost accuracy with a **Hugging Face OCR model**. The complete script—license activation, GPU‑enabled engine, structured OCR, AI post‑processing, and cleanup—covers every step a developer typically asks about, from “what if I don’t have a GPU?” to “how do I free resources?”. 

Give it a spin with your own documents, experiment with different models, or integrate the pipeline into a larger document‑processing service. The sky’s the limit once you’ve mastered this combination of Aspose OCR and Hugging Face AI.

---

**Next Steps**

- Try the same workflow on scanned images (`.png`, `.jpg`) to see how the engine adapts.  
- Explore the Aspose OCR **layout analysis** features for table extraction.  
- Dive deeper into Hugging Face quantization techniques to shrink model size even further.

Happy OCR hacking!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}