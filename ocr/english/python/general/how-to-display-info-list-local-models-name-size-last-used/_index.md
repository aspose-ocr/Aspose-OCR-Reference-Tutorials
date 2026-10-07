---
category: general
date: 2026-01-12
description: Learn how to display info from AsposeAI by listing local models, showing
  model name, size, and last‑used timestamp in a clear Python example.
draft: false
keywords:
- how to display info
- list local models
- display model name
- show model size
- show last used
language: en
og_description: 'How to display info from AsposeAI: list local models, display model
  name, size, and last used timestamp with a complete Python walkthrough.'
og_title: How to Display Info – List Local Models, Name, Size, Last Used
tags:
- AsposeAI
- Python
- Model Management
title: How to Display Info – List Local Models, Name, Size, Last Used
url: /python/general/how-to-display-info-list-local-models-name-size-last-used/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Display Info – List Local Models, Name, Size, Last Used

Ever wondered **how to display info** from your AsposeAI installation without digging through logs or the UI? You're not the only one. In many data‑science pipelines the first thing you need is a quick glance at which models sit on your machine, what they’re called, how big they are, and when you last touched them.

That’s exactly what we’ll cover: a concise, end‑to‑end Python snippet that **lists local models**, then **displays model name**, **shows model size**, and **shows last used** timestamps. No external libraries, no hidden magic—just the AsposeAI client you already have.

By the end of this tutorial you’ll be able to drop the code into any script, run it, and instantly get a tidy table of your locally cached models. It’s perfect for sanity‑checking environments, building health dashboards, or simply satisfying a curiosity about what’s lurking on disk.

## Prerequisites

- Python 3.8 or newer (the example uses f‑strings, so 3.6+ is a must)
- `asposeai` package installed (`pip install asposeai`)
- A working AsposeAI license or trial key (the client will pick up credentials from environment variables or a config file)

If you’ve already got those boxes checked, great—let’s dive in.

## Step 1: How to Display Info – Initialize the AsposeAI Client

Before we can **list local models**, we need a client object that talks to the AsposeAI runtime. This step is the foundation; without it the rest of the code would raise a `NameError`.

```python
# Step 1: Create an instance of the AsposeAI client
# The client automatically reads credentials from the environment
aspose_ai = AsposeAI()
```

*Why this matters*: Initializing the client establishes a session with the local inference engine, loading any necessary native libraries. It also validates that your license is active, preventing cryptic errors later when you try to query models.

> **Pro tip**: If you run this on a CI server, set `ASPOSEAI_LICENSE` in the environment so the client can start without interactive prompts.

## Step 2: List Local Models – Retrieve the Available Models

Now that the client is ready, we can **list local models**. The `list_local()` method returns a collection of objects, each exposing properties like `name`, `size_mb`, and `last_used`.

```python
# Step 2: Retrieve the list of locally available models
local_models = aspose_ai.list_local()
```

*What’s happening under the hood*: `list_local()` scans the directory where AsposeAI caches model files (`~/.asposeai/models` by default) and builds lightweight metadata objects. This is fast because it doesn’t load the model weights—just reads a small JSON manifest.

If you ever wonder whether a particular model is already cached, this call is the quickest way to confirm.

## Step 3: Display Model Name, Show Model Size, and Show Last Used

With the models in hand, we finally **display info** by iterating over the collection and printing each attribute. This is where we **display model name**, **show model size**, and **show last used** all in one neat line.

```python
# Step 3: Print each model's name, size (in MB), and last‑used timestamp
print("Available local models:")
print("-" * 50)
for model_info in local_models:
    # Using an f‑string to format the output cleanly
    print(f"{model_info.name} – {model_info.size_mb} MB – last used {model_info.last_used}")
```

**Expected output** (your timestamps will differ):

```
Available local models:
--------------------------------------------------
gpt‑tiny‑en – 120 MB – last used 2025-11-02 14:23:11
bert‑base‑fr – 420 MB – last used 2025-10-18 09:07:45
whisper‑large‑audio – 1580 MB – last used 2025-09-30 22:41:02
```

*Why we format it this way*: The dash (`–`) separates fields for readability, and the header line makes the console output scan-friendly. If you need a machine‑readable format later (CSV, JSON), you can easily swap the `print` call for a `writer.writerow` or `json.dump`.

### Handling Edge Cases

- **No models cached** – `list_local()` returns an empty list. The loop will simply skip, leaving you with just the header. You might want to add a guard:

  ```python
  if not local_models:
      print("No local models found. Use aspose_ai.download(...) to fetch one.")
  ```

- **Missing attributes** – In rare cases a manifest may be corrupted. Accessing `model_info.last_used` could raise `AttributeError`. Wrap the print in a `try/except` if you anticipate such issues.

- **Large model directories** – If you have hundreds of models, consider paging the output or writing to a file instead of printing to the console.

## Visual Summary (Optional)

If you prefer a quick visual cue, the diagram below illustrates the flow from client initialization to final display.  

![Diagram showing how to display info from AsposeAI client](/images/how-to-display-info.png "how to display info diagram")

*Alt text*: **how to display info** – schematic of AsposeAI client initialization, model listing, and info display.

## Full Working Script

Putting everything together, here’s the complete, ready‑to‑run script:

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

"""
How to display info from AsposeAI:
List local models and show each model's name, size, and last‑used timestamp.
"""

from asposeai import AsposeAI

def main():
    # Initialize client
    aspose_ai = AsposeAI()

    # Retrieve local models
    local_models = aspose_ai.list_local()

    # Header
    print("Available local models:")
    print("-" * 50)

    if not local_models:
        print("No local models found. Use aspose_ai.download(...) to fetch one.")
        return

    # Display each model's details
    for model_info in local_models:
        try:
            print(f"{model_info.name} – {model_info.size_mb} MB – last used {model_info.last_used}")
        except AttributeError:
            # Fallback if any attribute is missing
            print(f"{model_info.name} – info incomplete")

if __name__ == "__main__":
    main()
```

Save this as `list_models.py`, make it executable (`chmod +x list_models.py`), and run:

```bash
./list_models.py
```

You’ll see the tidy list demonstrated earlier.

## Conclusion

We've walked through **how to display info** from AsposeAI by **listing local models**, then **displaying model name**, **showing model size**, and **showing last used** timestamps. The approach is lightweight, requires only the standard `asposeai` package, and can be dropped into any automation pipeline or debugging session.

From here you might:

- Export the output to CSV for spreadsheet analysis (`csv` module).
- Feed the timestamps into a monitoring dashboard to alert on stale models.
- Combine this script with `aspose_ai.download()` to automatically refresh models that haven’t been used in a while.

Remember, clear visibility into your model inventory saves time, reduces storage bloat, and keeps your AI services humming smoothly. Give the script a spin, tweak the formatting to your taste, and let it become a staple in your toolbox.

Happy coding, and may your models always be fresh!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}