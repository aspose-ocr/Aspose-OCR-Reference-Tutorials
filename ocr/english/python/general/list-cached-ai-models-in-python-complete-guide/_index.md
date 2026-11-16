---
category: general
date: 2026-06-22
description: Learn how to list cached AI models using the AI SDK in Python. Includes
  steps to retrieve model cache directory and manage local AI models efficiently.
draft: false
keywords:
- list cached ai models
- retrieve model cache directory
- list local ai models
- ai sdk python
- manage ai model cache
language: en
og_description: List cached AI models with Python using the AI SDK. Follow this step‑by‑step
  tutorial to retrieve the model cache directory and handle local AI models.
og_title: List Cached AI Models in Python – Complete Guide
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Learn how to list cached AI models using the AI SDK in Python. Includes
    steps to retrieve model cache directory and manage local AI models efficiently.
  headline: List Cached AI Models in Python – Complete Guide
  type: TechArticle
- description: Learn how to list cached AI models using the AI SDK in Python. Includes
    steps to retrieve model cache directory and manage local AI models efficiently.
  name: List Cached AI Models in Python – Complete Guide
  steps:
  - name: Import the AI SDK
    text: '```python # Step 1: Import the AI SDK (replace with the actual package
      name if different) import ai ```'
  - name: List All Cached Models
    text: '```python # Step 2: List all models that are cached locally cached_models
      = ai.list_local() print("Cached models:", cached_models) ```'
  - name: Retrieve the Model Cache Directory
    text: '```python # Step 3: Retrieve the directory where the model files are stored
      cache_dir = ai.get_local_path() print("Model cache directory:", cache_dir) ```'
  - name: Empty Cache
    text: If `ai.list_local()` returns an empty list, you might wonder whether the
      SDK is misconfigured. Double‑check the environment variable `AI_CACHE_DIR` (or
      the SDK’s config file) to ensure it points to a writable location.
  - name: Permissions Issues
    text: When accessing `ai.get_local_path()`, a `PermissionError` can surface on
      restrictive systems. The fix is usually to run the script with appropriate user
      rights or to adjust the directory’s ACLs.
  - name: Version Mismatches
    text: 'Sometimes the cache contains an older version of a model while your code
      requests a newer one. The SDK will automatically download the newer version,
      but you can pre‑empt this by inspecting the version tag in the list:'
  - name: Cleaning Up Old Models
    text: 'If you need to free up space, you can delete a specific model folder directly:'
  type: HowTo
- questions:
  - answer: Yes. The SDK abstracts away OS‑specific paths, so `ai.get_local_path()`
      returns a valid string on Linux, macOS, and Windows.
    question: Does this work on all operating systems?
  - answer: The built‑in `list_local()` only reports locally stored artifacts. For
      remote registries you’d use `ai.list_remote()` (if your SDK version provides
      it).
    question: Can I list models from a remote cache?
  - answer: 'Replace the import line with the actual package name, e.g., `import myai
      as ai`. All subsequent calls stay the same because the API contract is consistent
      across implementations. --- ## Conclusion You now have a solid, production‑ready
      method to **list cached AI models** using the **AI SDK Python** '
    question: What if the SDK name isn’t `ai`?
  type: FAQPage
tags:
- python
- ai
- sdk
title: List Cached AI Models in Python – Complete Guide
url: /python/general/list-cached-ai-models-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# List Cached AI Models in Python – Complete Guide

Ever wondered how to **list cached AI models** on your workstation without digging through obscure folders? You're not alone. Many developers hit a wall when they need to verify which models are already stored locally, especially when working with limited bandwidth or offline deployments. In this tutorial you’ll see a quick, no‑fluff way to query the AI SDK, print the cache contents, and discover exactly where those files live.

We’ll also touch on related topics like **retrieving the model cache directory**, handling empty caches, and best practices for **managing AI model cache** in production scripts. By the end you’ll have a self‑contained snippet you can drop into any Python project.

## Prerequisites

Before we dive in, make sure you have:

- Python 3.8 or newer installed.
- The AI SDK (the `ai` package) installed via `pip install ai-sdk` or your organization’s internal repository.
- Basic familiarity with running scripts from the command line.

No additional libraries are required, so the example stays lightweight and portable.

---

## List Cached AI Models – Quick Overview

The first thing you need to do is import the SDK and call its helper functions. The SDK exposes two handy methods:

1. `ai.list_local()` – returns a Python list of model identifiers that are already cached.
2. `ai.get_local_path()` – returns the absolute directory where those model files reside.

Both calls are synchronous and raise a clear `AIError` if something goes wrong, which makes error handling straightforward.

> **Why use these functions?**  
> Knowing the exact set of cached models lets you avoid unnecessary downloads, debug version mismatches, and clean up old artifacts automatically. It’s a small piece of the larger **AI SDK Python** workflow, but it can save you hours of manual file‑system hunting.

### Step 1: Import the AI SDK

```python
# Step 1: Import the AI SDK (replace with the actual package name if different)
import ai
```

*Why this matters:* Importing the package registers the underlying C‑extensions and loads configuration files (like cache paths) from your environment. Skipping this step will raise a `ModuleNotFoundError` the moment you call any SDK function.

### Step 2: List All Cached Models

```python
# Step 2: List all models that are cached locally
cached_models = ai.list_local()
print("Cached models:", cached_models)
```

**What you’ll see:** If you have three models stored, the output might look like:

```
Cached models: ['gpt-4-mini', 'bert-base-uncased', 'stable-diffusion-v1']
```

If the cache is empty, you’ll get an empty list:

```
Cached models: []
```

> **Pro tip:** Wrap the call in a try/except block if you suspect the SDK might not be initialized correctly.

```python
try:
    cached_models = ai.list_local()
except ai.AIError as e:
    print("Failed to list cached models:", e)
    cached_models = []
```

### Step 3: Retrieve the Model Cache Directory

```python
# Step 3: Retrieve the directory where the model files are stored
cache_dir = ai.get_local_path()
print("Model cache directory:", cache_dir)
```

Typical output on a Unix‑like system:

```
Model cache directory: /home/you/.cache/ai/models
```

On Windows you might see something like `C:\Users\you\AppData\Local\ai\models`. Knowing this path is essential when you need to **manage AI model cache** manually—perhaps to purge old versions or to copy files to a shared drive.

---

## Visual Summary

![Diagram showing how to list cached AI models, retrieve their names, and locate the cache directory](https://example.com/images/list-cached-ai-models.png)

*Alt text:* Diagram illustrating the process to **list cached AI models** using the AI SDK in Python.

---

## Handling Edge Cases and Common Pitfalls

### Empty Cache

If `ai.list_local()` returns an empty list, you might wonder whether the SDK is misconfigured. Double‑check the environment variable `AI_CACHE_DIR` (or the SDK’s config file) to ensure it points to a writable location.

```python
if not cached_models:
    print("No models are cached. Consider downloading a model first.")
```

### Permissions Issues

When accessing `ai.get_local_path()`, a `PermissionError` can surface on restrictive systems. The fix is usually to run the script with appropriate user rights or to adjust the directory’s ACLs.

### Version Mismatches

Sometimes the cache contains an older version of a model while your code requests a newer one. The SDK will automatically download the newer version, but you can pre‑empt this by inspecting the version tag in the list:

```python
for model in cached_models:
    if "v2" not in model:
        print(f"Model {model} may be outdated.")
```

### Cleaning Up Old Models

If you need to free up space, you can delete a specific model folder directly:

```python
import shutil, os

def purge_model(model_name):
    path = os.path.join(cache_dir, model_name)
    if os.path.isdir(path):
        shutil.rmtree(path)
        print(f"Purged {model_name} from cache.")
    else:
        print(f"{model_name} not found in cache.")
```

Running `purge_model('bert-base-uncased')` will remove that model and free up disk space.

---

## Full Script You Can Copy‑Paste

Below is a ready‑to‑run script that combines all the steps, adds basic error handling, and prints a friendly summary.

```python
#!/usr/bin/env python3
"""
Complete example: list cached AI models and show cache directory.
"""

import ai
import os
import sys
import shutil

def main():
    try:
        # Retrieve cached model list
        cached = ai.list_local()
        print("Cached models:", cached)

        # Retrieve cache directory
        cache_dir = ai.get_local_path()
        print("Model cache directory:", cache_dir)

        # Summarize status
        if not cached:
            print("\n⚠️  No models are currently cached.")
        else:
            print("\n✅  Found {} model(s) in cache.".format(len(cached)))

        # Optional: ask user if they want to purge an old model
        if cached:
            to_purge = input("\nEnter a model name to purge (or press Enter to skip): ").strip()
            if to_purge:
                purge_path = os.path.join(cache_dir, to_purge)
                if os.path.isdir(purge_path):
                    shutil.rmtree(purge_path)
                    print(f"🗑️  Purged {to_purge} from cache.")
                else:
                    print(f"❌  Model {to_purge} not found in cache.")
    except ai.AIError as err:
        print("AI SDK error:", err, file=sys.stderr)
        sys.exit(1)
    except Exception as exc:
        print("Unexpected error:", exc, file=sys.stderr)
        sys.exit(1)

if __name__ == "__main__":
    main()
```

**Expected output (when cache is populated):**

```
Cached models: ['gpt-4-mini', 'bert-base-uncased', 'stable-diffusion-v1']
Model cache directory: /home/you/.cache/ai/models

✅  Found 3 model(s) in cache.

Enter a model name to purge (or press Enter to skip):
```

Run the script with `python list_models.py` and you’ll instantly know what’s sitting on disk.

---

## Frequently Asked Questions

**Q: Does this work on all operating systems?**  
A: Yes. The SDK abstracts away OS‑specific paths, so `ai.get_local_path()` returns a valid string on Linux, macOS, and Windows.

**Q: Can I list models from a remote cache?**  
A: The built‑in `list_local()` only reports locally stored artifacts. For remote registries you’d use `ai.list_remote()` (if your SDK version provides it).

**Q: What if the SDK name isn’t `ai`?**  
A: Replace the import line with the actual package name, e.g., `import myai as ai`. All subsequent calls stay the same because the API contract is consistent across implementations.

---

## Conclusion

You now have a solid, production‑ready method to **list cached AI models** using the **AI SDK Python** library, retrieve the **model cache directory**, and even clean up old files. This knowledge helps you keep your environment tidy, avoid redundant downloads, and debug version issues with ease.

Ready for the next step? Try extending the script to automatically download missing models, or integrate it into a CI pipeline that validates cache health before each build. Exploring **manage AI model cache** strategies will make your AI‑powered applications faster and more reliable.

Happy coding, and may your caches stay lean!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Extract Text from ZIP Archives Using Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}