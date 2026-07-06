---
category: general
date: 2026-02-22
description: Learn how to list cached models and quickly show cache directory on your
  machine. Includes steps to view cache folder and manage local AI model storage.
draft: false
keywords:
- list cached models
- show cache directory
- how to view cache folder
- AI model cache
- local model storage
language: en
og_description: Find out how to list cached models, show cache directory, and view
  the cache folder in a few easy steps. Complete Python example included.
og_title: list cached models – quick guide to view cache directory
tags:
- AI
- caching
- Python
- development
title: list cached models – how to view cache folder and show cache directory
url: /python/general/list-cached-models-how-to-view-cache-folder-and-show-cache-d/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# list cached models – quick guide to view cache directory

Ever wondered how to **list cached models** on your workstation without digging through obscure folders? You're not the only one. Many developers hit a wall when they need to verify which AI models are already stored locally, especially when disk space is at a premium. The good news? In just a handful of lines you can both **list cached models** and **show cache directory**, giving you full visibility into your cache folder.

In this tutorial we’ll walk through a self‑contained Python script that does exactly that. By the end you’ll know how to view the cache folder, understand where the cache lives on different OSes, and even see a tidy printed list of every model that’s been downloaded. No external docs, no guesswork—just clear code and explanations you can copy‑paste right now.

## What You’ll Learn

- How to initialize an AI client (or a stub) that offers caching utilities.  
- The exact commands to **list cached models** and **show cache directory**.  
- Where the cache lives on Windows, macOS, and Linux, so you can navigate to it manually if you wish.  
- Tips for handling edge cases such as an empty cache or a custom cache path.  

**Prerequisites** – you need Python 3.8+ and a pip‑installable AI client that implements `list_local()`, `get_local_path()`, and optionally `clear_local()`. If you don’t have one yet, the example uses a mock `YourAIClient` class that you can replace with the real SDK (e.g., `openai`, `huggingface_hub`, etc.).  

Ready? Let’s dive in.

## Step 1: Set Up the AI Client (or a Mock)

If you already have a client object, skip this block. Otherwise, create a tiny stand‑in that mimics the caching interface. This makes the script runnable even without a real SDK.

```python
# step_1_client_setup.py
import os
from pathlib import Path

class YourAIClient:
    """
    Minimal mock of an AI client that stores downloaded models in a
    directory called `.ai_cache` inside the user's home folder.
    """
    def __init__(self, cache_dir: Path | None = None):
        # Use a custom path if supplied, otherwise default to ~/.ai_cache
        self.cache_dir = Path(cache_dir) if cache_dir else Path.home() / ".ai_cache"
        self.cache_dir.mkdir(parents=True, exist_ok=True)

    def list_local(self):
        """Return a list of model folder names that exist in the cache."""
        return [p.name for p in self.cache_dir.iterdir() if p.is_dir()]

    def get_local_path(self):
        """Absolute path to the cache directory."""
        return str(self.cache_dir.resolve())

    # Optional helper for demonstration purposes
    def _populate_dummy_models(self, count=3):
        for i in range(1, count + 1):
            (self.cache_dir / f"model_{i}").mkdir(exist_ok=True)

# Initialize the client (replace with real client if you have one)
ai = YourAIClient()
# Populate with dummy data the first time you run the script
if not ai.list_local():
    ai._populate_dummy_models()
```

> **Pro tip:** If you already have a real client (e.g., `from huggingface_hub import HfApi`), just replace the `YourAIClient()` call with `HfApi()` and make sure the methods `list_local` and `get_local_path` exist or are wrapped accordingly.

## Step 2: **list cached models** – retrieve and display them

Now that the client is ready, we can ask it to enumerate everything it knows about locally. This is the core of our **list cached models** operation.

```python
# step_2_list_models.py
print("Cached models:")
for model_name in ai.list_local():
    print(" -", model_name)
```

**Expected output** (with the dummy data from step 1):

```
Cached models:
 - model_1
 - model_2
 - model_3
```

If the cache is empty you’ll simply see:

```
Cached models:
```

That little blank line tells you there’s nothing stored yet—handy when you’re scripting clean‑up routines.

## Step 3: **show cache directory** – where does the cache live?

Knowing the path is often half the battle. Different operating systems place caches in different default locations, and some SDKs let you override it via environment variables. The following snippet prints the absolute path so you can `cd` into it or open it in a file explorer.

```python
# step_3_show_path.py
print("\nCache directory:", ai.get_local_path())
```

**Typical output** on a Unix‑like system:

```
Cache directory: /home/youruser/.ai_cache
```

On Windows you might see something like:

```
Cache directory: C:\Users\YourUser\.ai_cache
```

Now you know exactly **how to view cache folder** on any platform.

## Step 4: Put It All Together – a single runnable script

Below is the complete, ready‑to‑run program that combines the three steps. Save it as `view_ai_cache.py` and execute `python view_ai_cache.py`.

```python
# view_ai_cache.py
import os
from pathlib import Path

class YourAIClient:
    """Simple mock client exposing cache‑related utilities."""
    def __init__(self, cache_dir: Path | None = None):
        self.cache_dir = Path(cache_dir) if cache_dir else Path.home() / ".ai_cache"
        self.cache_dir.mkdir(parents=True, exist_ok=True)

    def list_local(self):
        return [p.name for p in self.cache_dir.iterdir() if p.is_dir()]

    def get_local_path(self):
        return str(self.cache_dir.resolve())

    def _populate_dummy_models(self, count=3):
        for i in range(1, count + 1):
            (self.cache_dir / f"model_{i}").mkdir(exist_ok=True)

# ----------------------------------------------------------------------
# Main execution block
# ----------------------------------------------------------------------
if __name__ == "__main__":
    # Initialize (replace with real client if available)
    ai = YourAIClient()

    # Populate dummy data only on first run – remove this in production
    if not ai.list_local():
        ai._populate_dummy_models()

    # Step 1: list cached models
    print("Cached models:")
    for model_name in ai.list_local():
        print(" -", model_name)

    # Step 2: show cache directory
    print("\nCache directory:", ai.get_local_path())
```

Run it and you’ll instantly see both the list of cached models **and** the location of the cache directory.

## Edge Cases & Variations

| Situation | What to Do |
|-----------|------------|
| **Empty cache** | The script will print “Cached models:” with no entries. You can add a conditional warning: `if not models: print("⚠️ No models cached yet.")` |
| **Custom cache path** | Pass a path when constructing the client: `YourAIClient(cache_dir=Path("/tmp/my_ai_cache"))`. The `get_local_path()` call will reflect that custom location. |
| **Permission errors** | On restricted machines, the client may raise `PermissionError`. Wrap the initialization in a `try/except` block and fallback to a user‑writable directory. |
| **Real SDK usage** | Replace `YourAIClient` with the actual client class and ensure the method names match. Many SDKs expose a `cache_dir` attribute you can read directly. |

## Pro Tips for Managing Your Cache

- **Periodic cleanup:** If you frequently download large models, schedule a cron job that calls `shutil.rmtree(ai.get_local_path())` after confirming you no longer need them.  
- **Disk usage monitoring:** Use `du -sh $(ai.get_local_path())` on Linux/macOS or `Get-ChildItem -Recurse | Measure-Object -Property Length -Sum` in PowerShell to keep an eye on size.  
- **Versioned folders:** Some clients create subfolders per model version. When you **list cached models**, you’ll see each version as a separate entry—use that to prune older revisions.  

## Visual Overview

![list cached models screenshot](https://example.com/images/list-cached-models.png "list cached models – console output showing models and cache path")

*Alt text:* *list cached models – console output displaying cached model names and the cache directory path.*

## Conclusion

We’ve covered everything you need to **list cached models**, **show cache directory**, and generally **how to view cache folder** on any system. The short script demonstrates a complete, runnable solution, explains **why** each step matters, and offers practical tips for real‑world usage.  

Next, you might explore **how to clear the cache** programmatically, or integrate these calls into a larger deployment pipeline that validates model availability before launching inference jobs. Either way, you now have the foundation to manage local AI model storage with confidence.

Got questions about a specific AI SDK? Drop a comment below, and happy caching!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}