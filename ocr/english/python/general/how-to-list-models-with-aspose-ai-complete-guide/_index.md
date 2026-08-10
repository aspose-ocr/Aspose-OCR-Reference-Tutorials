---
category: general
date: 2026-07-05
description: How to list models with Aspose AI, enable auto download, and download
  Hugging Face model in Python. Follow this step‑by‑step tutorial to set up cache
  and start using Aspose AI today.
draft: false
keywords:
- how to list models
- enable auto download
- download hugging face model
- how to use aspose
- how to set cache
language: en
og_description: How to list models with Aspose AI, enable auto download and download
  a Hugging Face model. Learn to set cache and use Aspose AI in minutes.
og_title: How to list models with Aspose AI – Full Tutorial
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: How to list models with Aspose AI, enable auto download, and download
    Hugging Face model in Python. Follow this step‑by‑step tutorial to set up cache
    and start using Aspose AI today.
  headline: How to list models with Aspose AI – Complete Guide
  type: TechArticle
- description: How to list models with Aspose AI, enable auto download, and download
    Hugging Face model in Python. Follow this step‑by‑step tutorial to set up cache
    and start using Aspose AI today.
  name: How to list models with Aspose AI – Complete Guide
  steps:
  - name: Create an `AsposeAI` object and a `AsposeAIModelConfig`.
    text: Create an `AsposeAI` object and a `AsposeAIModelConfig`.
  - name: Set `allow_auto_download = "true"` and point `directory_model_path` to a
      folder you control.
    text: Set `allow_auto_download = "true"` and point `directory_model_path` to a
      folder you control.
  - name: Initialise the AI, then call `list_local()` to see exactly what’s cached.
    text: Initialise the AI, then call `list_local()` to see exactly what’s cached.
  - name: Use the listed model name for inference, and you’re ready to build real‑world
      applications.
    text: Use the listed model name for inference, and you’re ready to build real‑world
      applications.
  type: HowTo
tags:
- Aspose
- Python
- LLM
- Model Management
title: How to list models with Aspose AI – Complete Guide
url: /python/general/how-to-list-models-with-aspose-ai-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to list models with Aspose AI – Complete Guide

How to list models with Aspose AI is a question that pops up the moment you start experimenting with large language models in Python. In this tutorial we’ll walk through enabling **auto download**, configuring a local cache, and pulling a model straight from Hugging Face—so you can get up and running without hunting for files manually.

If you’ve ever wondered *“how do I use Aspose for OCR‑driven AI?”* or *“what’s the easiest way to set cache for model files?”* you’re in the right place. By the end you’ll have a fully functional script that lists every model stored locally, automatically downloads missing ones, and shows you exactly where the files live on disk.

---

## What You’ll Need

Before we dive in, make sure you have:

- Python 3.9 or newer (the library uses type hints that require a recent interpreter)
- `pip` access to install the **Aspose OCR** package (`aocr`).  
  ```bash
  pip install aocr
  ```
- An internet connection for the first download from Hugging Face.
- A folder where you’d like to keep the model cache (e.g., `./model_cache`).

That’s it—no extra Docker containers, no heavyweight virtual environments beyond a clean Python install.

---

## ## How to list models with Aspose AI

The heart of this guide is the ability to **list models** that Aspose AI has cached locally. Once the cache is set up, the library can enumerate everything it knows about, making debugging and version control a breeze.

```python
import aocr

# 1️⃣ Create an Aspose AI instance
ai = aocr.AsposeAI()

# 2️⃣ Configure the model cache and auto‑download behavior
cfg = aocr.AsposeAIModelConfig()
cfg.allow_auto_download = "true"                     # ← enable auto download
cfg.directory_model_path = r"./model_cache"          # ← how to set cache
cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"

# 3️⃣ Initialise the AI with the config we just built
ai.initialize(cfg)

# 4️⃣ List the models that are already cached locally
print("🗂️ Models cached at:", ai.get_local_path())
print("📦 Available models:", ai.list_local())
```

**Why this works:**  
- `AsposeAI()` creates the high‑level entry point that talks to the underlying inference engine.  
- `AsposeAIModelConfig()` holds all the knobs you can turn; setting `allow_auto_download` to `"true"` tells the library to fetch missing files automatically from the repository you specify.  
- `directory_model_path` is the *cache directory*—the place where all downloaded binaries live.  
- `initialize()` applies the configuration, performing the first download if the cache is empty.  
- Finally, `list_local()` scans the cache folder and returns a Python list of model identifiers, which we print out.

### Expected output (first run)

```
🗂️ Models cached at: ./model_cache
📦 Available models: ['Qwen2.5-3B-Instruct-GGUF']
```

If you run the script again, the library will skip the download and simply list the already‑present model, proving that **how to set cache** really pays off for subsequent runs.

---

## ## Enable auto download for missing models

Often you’ll work with several models across projects. Manually pulling each one from Hugging Face can be tedious. By enabling auto download, Aspose AI takes care of the heavy lifting.

```python
cfg.allow_auto_download = "true"
```

> **Pro tip:** Keep `allow_auto_download` set to `"true"` **only** in development or CI environments. In production you might want to lock down the cache to avoid unexpected network traffic.

If you later decide to turn it off, just set the flag to `"false"` before calling `initialize()` again.

---

## ## Download Hugging Face model on the fly

The line

```python
cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
```

tells Aspose AI which remote repository to pull from. The library supports any public model on Hugging Face that provides a GGUF file. Want a different model? Swap the repo ID:

```python
cfg.hugging_face_repo_id = "mistralai/Mistral-7B-Instruct-v0.2"
```

When you run the script, Aspose AI checks the cache:

- **If the model exists**, it loads it instantly.  
- **If it doesn’t**, the auto‑download flag triggers a download, stores the file under `directory_model_path`, and then registers it for immediate use.

This approach eliminates the “download‑then‑run” two‑step process many tutorials force you to follow.

---

## ## How to use Aspose AI after the model is listed

Listing models is only half the story. Once you know a model is present, you can start inference:

```python
# Assume the model we just listed is the one we want to use
model_name = ai.list_local()[0]

# Create a simple prompt
prompt = "Explain the difference between supervised and unsupervised learning."

# Run inference
response = ai.run_inference(model_name, prompt)

print("🤖 Model response:", response)
```

**Why this matters:**  
- `run_inference()` abstracts away tokenization, batching, and GPU handling.  
- By passing the *model name* you obtained from `list_local()`, you guarantee that the inference call matches the exact file on disk.

---

## ## How to set cache location for multiple projects

If you juggle several projects, you might want each to have its own cache folder. The `directory_model_path` field is just a plain string, so you can build it dynamically:

```python
import os

project_name = "sentiment_analysis"
cache_root   = "./model_cache"
cfg.directory_model_path = os.path.join(cache_root, project_name)
```

Now each project gets an isolated sub‑folder (`./model_cache/sentiment_analysis`), preventing version clashes and making clean‑up straightforward.

---

## ## Common pitfalls and how to avoid them

| Symptom | Likely cause | Fix |
|---------|--------------|-----|
| **`PermissionError` when accessing cache** | Cache folder owned by another user (common on shared servers) | Create the folder manually with proper permissions: `mkdir -p ./model_cache && chmod 775 ./model_cache` |
| **Model never appears in `list_local()`** | `allow_auto_download` set to `"false"` and the model isn’t cached yet | Turn the flag on temporarily, run once, then switch off if desired |
| **Unexpected model version** | Two different repos share the same name but different files | Pin the exact repo ID (including tag/commit) or lock the cache by disabling auto‑download after the first successful pull |
| **Out‑of‑memory errors** | Large GGUF files on a machine without enough RAM/VRAM | Use a smaller model (e.g., `Qwen2.5-1.5B`) or set `cfg.device = "cpu"` to force CPU inference |

---

## ## Full script you can copy‑paste

Below is the complete, ready‑to‑run example that incorporates all the concepts above. Save it as `list_models_demo.py` and execute with `python list_models_demo.py`.

```python
# list_models_demo.py
import os
import aocr

def main():
    # ------------------------------------------------------------------
    # 1️⃣ Create the Aspose AI instance
    # ------------------------------------------------------------------
    ai = aocr.AsposeAI()

    # ------------------------------------------------------------------
    # 2️⃣ Build configuration: enable auto download, set cache path,
    #    and point at a Hugging Face repo
    # ------------------------------------------------------------------
    cfg = aocr.AsposeAIModelConfig()
    cfg.allow_auto_download = "true"                               # enable auto download
    cfg.directory_model_path = os.path.abspath("./model_cache")   # how to set cache
    cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"

    # ------------------------------------------------------------------
    # 3️⃣ Initialise the AI with the configuration
    # ------------------------------------------------------------------
    ai.initialize(cfg)

    # ------------------------------------------------------------------
    # 4️⃣ Verify cache location and list all locally available models
    # ------------------------------------------------------------------
    print("🗂️ Models cached at:", ai.get_local_path())
    print("📦 Available models:", ai.list_local())

    # ------------------------------------------------------------------
    # 5️⃣ (Optional) Run a quick inference using the first listed model
    # ------------------------------------------------------------------
    if ai.list_local():
        model_name = ai.list_local()[0]
        prompt = "Give a short summary of the Python GIL."
        response = ai.run_inference(model_name, prompt)
        print("\n🤖 Model response:", response)

if __name__ == "__main__":
    main()
```

**Running it** will produce output similar to the earlier example, followed by a concise answer from the model. Feel free to replace the prompt with anything you like—this is the fastest way to test that the model is truly usable after you’ve **how to list models**.

---

## ## Summary

We’ve covered everything you need to **how to list models** using Aspose AI, from enabling **auto download** to configuring a persistent **cache** and pulling a **Hugging Face model** on demand. The key takeaways:

1. Create an `AsposeAI` object and a `AsposeAIModelConfig`.  
2. Set `allow_auto_download = "true"` and point `directory_model_path` to a folder you control.  
3. Initialise the AI, then call `list_local()` to see exactly what’s cached.  
4. Use the listed model name for inference, and you’re ready to build real‑world applications.

---

## What’s Next?

- **Experiment with different models** – swap `cfg.hugging_face_repo_id` for another repo and see how the list changes.  
- **Fine‑tune cache


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [How to Set Aspose OCR License and Verify It in Java](/ocr/english/java/ocr-basics/set-license/)
- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}