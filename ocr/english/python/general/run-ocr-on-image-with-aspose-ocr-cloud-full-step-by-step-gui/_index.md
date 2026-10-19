---
category: general
date: 2026-03-28
description: Learn how to run OCR on image, download Hugging Face model automatically,
  clean OCR text and configure LLM model in Python using Aspose OCR Cloud.
draft: false
keywords:
- run OCR on image
- download hugging face model
- clean OCR text
- configure LLM model
language: en
og_description: Run OCR on image and clean the output using an auto‑downloaded Hugging Face
  model. This guide shows how to configure LLM model in Python.
og_title: Run OCR on Image – Complete Aspose OCR Cloud Tutorial
tags:
- OCR
- Python
- LLM
- HuggingFace
title: Run OCR on Image with Aspose OCR Cloud – Full Step‑by‑Step Guide
url: /python/general/run-ocr-on-image-with-aspose-ocr-cloud-full-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Run OCR on Image – Complete Aspose OCR Cloud Tutorial

Ever needed to run OCR on image files but the raw output looked like a jumbled mess? In my experience the biggest pain point isn’t the recognition itself—it’s the cleanup. Luckily, Aspose OCR Cloud lets you attach an LLM post‑processor that can *clean OCR text* automatically. In this tutorial we’ll walk through everything you need: from **downloading a Hugging Face model** to configuring the LLM, running the OCR engine, and finally polishing the result.

By the end of this guide you’ll have a ready‑to‑run script that:

1. Pulls a compact Qwen 2.5 model from Hugging Face (auto‑downloaded for you).  
2. Configures the model to run part of the network on GPU and the rest on CPU.  
3. Executes the OCR engine on a handwritten note image.  
4. Uses the LLM to clean the recognised text, giving you human‑readable output.

> **Prerequisites** – Python 3.8+, `asposeocrcloud` package, a GPU with at least 4 GB VRAM (optional but recommended), and an internet connection for the first model download.

---

## What You’ll Need

- **Aspose OCR Cloud SDK** – install via `pip install asposeocrcloud`.  
- **A sample image** – e.g., `handwritten_note.jpg` placed in a local folder.  
- **GPU support** – if you have a CUDA‑enabled GPU, the script will offload 30 layers; otherwise it will fall back to CPU automatically.  
- **Write permission** – the script caches the model in `YOUR_DIRECTORY`; make sure the folder exists.

---

## Step 1 – Configure the LLM Model (download Hugging Face model)

The first thing we do is tell Aspose AI where to fetch the model from. The `AsposeAIModelConfig` class handles auto‑download, quantization, and GPU layer allocation.

```python
import asposeocrcloud as ocr
from asposeocrcloud.ai import AsposeAI, AsposeAIModelConfig

# ----------------------------------------------------------------------
# Step 1: Model configuration – this will download the model if it’s missing
# ----------------------------------------------------------------------
model_config = AsposeAIModelConfig(
    allow_auto_download="true",                           # Enables auto‑download
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF", # Repo on Hugging Face
    hugging_face_quantization="int8",                     # Small footprint, fast inference
    gpu_layers=30,                                        # 30 layers on GPU, rest on CPU
    directory_model_path=r"YOUR_DIRECTORY"               # Cache folder (optional)
)
```

**Why this matters** – Quantizing to `int8` shaves memory usage dramatically (≈ 4 GB vs 12 GB). Splitting the model between GPU and CPU lets you run a 3‑billion‑parameter LLM even on a modest RTX 3060. If you don’t have a GPU, set `gpu_layers=0` and the SDK will keep everything on CPU.

> **Tip:** The first run will download ~ 1.5 GB, so give it a few minutes and a stable connection.

---

## Step 2 – Initialise the AI Engine with the Model Configuration

Now we spin up the Aspose AI engine and feed it the configuration we just created.

```python
# ----------------------------------------------------------------------
# Step 2: Initialise the AI engine – pulls the model if needed
# ----------------------------------------------------------------------
ocr_ai = AsposeAI()
ocr_ai.initialize(model_config)  # This call blocks until the model is ready
```

**What’s happening under the hood?** The SDK checks `directory_model_path` for an existing model. If it finds a matching version it loads it instantly; otherwise it downloads the GGUF file from Hugging Face, unpacks it, and prepares the inference pipeline.

---

## Step 3 – Create the OCR Engine and Attach the AI Post‑Processor

The OCR engine does the heavy lifting of recognising characters. By attaching `ocr_ai.run_postprocessor` we enable **clean OCR text** automatically after recognition.

```python
# ----------------------------------------------------------------------
# Step 3: Build the OCR engine and bind the LLM post‑processor
# ----------------------------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.set_post_processor(ocr_ai.run_postprocessor, custom_settings=None)
```

**Why use a post‑processor?** Raw OCR often includes line breaks in the wrong places, mis‑detected punctuation, or stray symbols. The LLM can rewrite the output into proper sentences, correct spelling, and even infer missing words—essentially turning a raw dump into polished prose.

---

## Step 4 – Run OCR on an Image File

With everything wired together, it’s time to feed an image to the engine.

```python
# ----------------------------------------------------------------------
# Step 4: Load the image and run OCR
# ----------------------------------------------------------------------
input_image = ocr.Image.load(r"YOUR_DIRECTORY/handwritten_note.jpg")
raw_result = ocr_engine.recognize(input_image)   # Returns an OcrResult object
```

**Edge case:** If the image is large (> 5 MP), you might want to resize it first to speed up processing. The SDK accepts a Pillow `Image` object, so you can pre‑process with `PIL.Image.thumbnail()` if needed.

---

## Step 5 – Let the AI Clean Up the Recognised Text and Show Both Versions

Finally we invoke the post‑processor we attached earlier. This step demonstrates the contrast between *before* and *after* cleaning.

```python
# ----------------------------------------------------------------------
# Step 5: Clean the OCR output using the LLM and display both results
# ----------------------------------------------------------------------
cleaned_result = ocr_engine.run_postprocessor(raw_result)

print("=== Before AI ===")
print(raw_result.text)

print("\n=== After AI ===")
print(cleaned_result.text)
```

### Expected Output

```
=== Before AI ===
Th1s 1s a h@ndwr1tt3n n0te.  It c0nta1ns m1st@k3s, l1n3 br3aks, & sp3c!@l ch@r@ct3rs.

=== After AI ===
This is a handwritten note. It contains mistakes, line breaks, and special characters.
```

Notice how the LLM has:

- Fixed common OCR mis‑recognitions (`Th1s` → `This`).  
- Removed stray symbols (`&` → `and`).  
- Normalised line breaks into proper sentences.

---

## 🎨 Visual Overview (Run OCR on image Workflow)

![Run OCR on image workflow](run_ocr_on_image_workflow.png "Diagram showing the run OCR on image pipeline from model download to cleaned output")

The diagram above summarises the full pipeline: **download Hugging Face model → configure LLM → initialise AI → OCR engine → AI post‑processor → clean OCR text**.

---

## Common Questions & Pro Tips

### What if I don’t have a GPU?

Set `gpu_layers=0` in the `AsposeAIModelConfig`. The model will run entirely on CPU, which is slower but still functional. You can also switch to a smaller model (e.g., `Qwen/Qwen2.5-1.5B‑Instruct‑GGUF`) to keep inference time reasonable.

### How do I change the model later?

Just update `hugging_face_repo_id` and re‑run `ocr_ai.initialize(model_config)`. The SDK will detect the version change, download the new model, and replace the cached files.

### Can I customise the post‑processor prompt?

Yes. Pass a dictionary to `custom_settings` with a `prompt_template` key. For example:

```python
custom_prompt = {
    "prompt_template": "Correct the following OCR text and keep line breaks:\n{ocr_text}"
}
ocr_engine.set_post_processor(ocr_ai.run_postprocessor, custom_settings=custom_prompt)
```

### Should I store the cleaned text to a file?

Definitely. After cleaning you can write the result to a `.txt` or `.json` file for downstream processing:

```python
with open("cleaned_note.txt", "w", encoding="utf-8") as f:
    f.write(cleaned_result.text)
```

---

## Conclusion

We’ve just shown you how to **run OCR on image** files with Aspose OCR Cloud, automatically **download a Hugging Face model**, expertly **configure LLM model** settings, and finally **clean OCR text** using a powerful LLM post‑processor. The whole process fits into a single, easy‑to‑run Python script and works on both GPU‑enabled and CPU‑only machines.

If you’re comfortable with this pipeline, consider experimenting with:

- **Different LLMs** – try `meta-llama/Meta-Llama-3-8B‑Instruct‑GGUF` for a larger context window.  
- **Batch processing** – loop over a folder of images and aggregate cleaned results into a CSV.  
- **Custom prompts** – tailor the AI to your domain (legal documents, medical notes, etc.).

Feel free to tweak the `gpu_layers` value, swap the model, or plug in your own prompt. The sky’s the limit, and the code you have now is the launchpad.

Happy coding, and may your OCR outputs be ever clean! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}