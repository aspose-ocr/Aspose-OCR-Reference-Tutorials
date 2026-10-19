---
category: general
date: 2026-06-19
description: Create AsposeAI instance in Python quickly, covering default model configuration
  and a custom logging callback for better insight.
draft: false
keywords:
- create asposeai instance
- AsposeAI default instance
- Python logging callback
- custom logging for AsposeAI
- AsposeAI model configuration
- using AsposeAI in Python
language: en
og_description: Create AsposeAI instance in Python fast. Learn default and custom
  logging setups for robust AI integration.
og_title: Create AsposeAI Instance in Python – Step‑by‑Step Guide
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Create AsposeAI instance in Python quickly, covering default model
    configuration and a custom logging callback for better insight.
  headline: Create AsposeAI Instance in Python – Complete Guide
  type: TechArticle
- description: Create AsposeAI instance in Python quickly, covering default model
    configuration and a custom logging callback for better insight.
  name: Create AsposeAI Instance in Python – Complete Guide
  steps:
  - name: 1. Import the AsposeAI class
    text: First we bring the class into the current namespace. This mirrors the typical
      “import‑library” pattern you see in most Python SDKs.
  - name: 2. Spin up the default model configuration
    text: Creating an instance without any arguments gives you the SDK’s built‑in
      model, which is perfect for quick trials.
  - name: 3. Define a simple logging callback
    text: If you want insight into what the SDK is doing—like request payloads or
      internal warnings—you can attach a logging function. Here’s a minimal example
      that just prints to stdout.
  - name: 4. Create an instance that uses the custom logging callback
    text: Now we combine the default model with our logger. The `logging` parameter
      expects a callable that receives a single string argument.
  type: HowTo
tags:
- AsposeAI
- Python
- AI SDK
title: Create AsposeAI Instance in Python – Complete Guide
url: /python/general/create-asposeai-instance-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create AsposeAI Instance in Python – Complete Guide

Ever needed to **create AsposeAI instance** in a Python project but weren’t sure which constructor arguments to use? You’re not alone. Whether you’re prototyping a quick demo or building a production‑grade AI service, getting the instance right is the first step toward reliable results.

In this tutorial we’ll walk through the whole process: from spinning up the **AsposeAI default instance** to wiring a **custom logging callback** that lets you see exactly what the SDK is whispering under the hood. By the end you’ll have a working `AsposeAI` object you can drop into any script, plus a handful of tips to avoid the usual gotchas.

## What You’ll Need

Before we dive, make sure you have:

- Python 3.8 or newer installed (the SDK supports 3.7+).
- The `asposeai` package installed via `pip install asposeai`.
- A terminal or IDE you’re comfortable with (VS Code, PyCharm, or even a plain text editor works).

No extra credentials are required for the default built‑in model, so you can start experimenting right away.

## How to Create AsposeAI Instance – Step‑by‑Step

Below is a concise, numbered walkthrough. Each step includes a code snippet, an explanation of **why** it matters, and a quick sanity‑check you can run.

### 1. Import the AsposeAI class

First we bring the class into the current namespace. This mirrors the typical “import‑library” pattern you see in most Python SDKs.

```python
# Step 1: Import the AsposeAI class
from asposeai import AsposeAI
```

> **Why?** Importing isolates the SDK’s public API, keeping your script tidy and avoiding accidental name clashes.

### 2. Spin up the default model configuration

Creating an instance without any arguments gives you the SDK’s built‑in model, which is perfect for quick trials.

```python
# Step 2: Create an instance using the default built‑in model configuration
ai_default = AsposeAI()
```

> **What happens under the hood?** `AsposeAI()` loads a lightweight, locally‑bundled language model. It requires no network access, so you can run it offline.

### 3. Define a simple logging callback

If you want insight into what the SDK is doing—like request payloads or internal warnings—you can attach a logging function. Here’s a minimal example that just prints to stdout.

```python
# Step 3: Define a simple logging callback to capture AI messages
def log(message):
    print("[AI] " + message)
```

> **Why a callback?** The SDK emits log events through a user‑supplied function. This design lets you route logs wherever you like—stdout, a file, or a monitoring service.

### 4. Create an instance that uses the custom logging callback

Now we combine the default model with our logger. The `logging` parameter expects a callable that receives a single string argument.

```python
# Step 4: Create an instance that uses the custom logging callback
ai_with_logging = AsposeAI(logging=log)
```

> **Result:** Every internal message the SDK generates will now be printed with a `[AI]` prefix, giving you real‑time visibility.

#### Expected output (sample)

Running the snippet above won’t produce output immediately because the SDK only logs during actual inference calls. To see it in action, try a quick `generate` call (shown in the next section).

## Using the Default AsposeAI Instance

Once you have `ai_default`, you can call its methods just like any other Python object. Here’s a basic text generation example:

```python
# Generate a short response using the default instance
response = ai_default.generate(prompt="Explain the difference between AI and ML.")
print("Response:", response)
```

Typical console output:

```
Response: AI (Artificial Intelligence) is the broader concept...
```

No logging appears because we didn’t supply a logger, but the call succeeds, confirming that **create AsposeAI instance** works out of the box.

## Adding a Custom Logging Callback (Full Example)

Let’s combine everything into a single script that both creates the instance and demonstrates logging:

```python
from asposeai import AsposeAI

def log(message):
    # Simple logger that timestamps each line
    from datetime import datetime
    timestamp = datetime.now().strftime("%H:%M:%S")
    print(f"[{timestamp}] [AI] {message}")

# Create the instance with custom logging
ai = AsposeAI(logging=log)

# Trigger a request to see logs in action
result = ai.generate(prompt="What is the capital of France?")
print("Result:", result)
```

Sample console output:

```
[12:34:56] [AI] Sending request to AsposeAI service...
[12:34:56] [AI] Received response (status 200)
Result: Paris
```

> **Why this matters:** The log shows the request lifecycle, which is invaluable when debugging network timeouts or payload mismatches.

## Verifying the Instance Works Across Environments

A robust **AsposeAI model configuration** should behave the same on Windows, macOS, and Linux. To confirm:

1. Run the script on each OS.
2. Check that the response string is non‑empty and that the log lines appear (if you enabled logging).
3. Optionally, assert the output in a unit test:

```python
import unittest

class TestAsposeAI(unittest.TestCase):
    def test_default_instance(self):
        ai = AsposeAI()
        out = ai.generate(prompt="2+2")
        self.assertIn("4", out)

if __name__ == "__main__":
    unittest.main()
```

If the test passes, you’ve successfully **create AsposeAI instance** that works in a CI pipeline.

## Common Pitfalls and Pro Tips

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| `ImportError: cannot import name 'AsposeAI'` | Package not installed or wrong Python environment | Run `pip install asposeai` in the same interpreter |
| No logs appear even after passing `logging=log` | Callback signature mismatched (must accept a single string) | Ensure `def log(message):` not `def log(*args)` |
| `generate` hangs forever | Network blocked (when using cloud models) | Switch to default built‑in model or configure a proxy |
| Response is empty | Prompt too short or model not loaded | Provide a longer, clearer prompt; verify `ai` is not `None` |

> **Pro tip:** Keep the logger lightweight. Heavy I/O (like writing to a remote DB) inside the callback can slow down inference dramatically.

## Next Steps – Extending Your AsposeAI Setup

Now that you know how to **create AsposeAI instance** with both default and custom logging, consider these follow‑up topics:

- **Using AsposeAI model configuration** to load a fine‑tuned model from a local path.
- **Integrating with async code** (`await ai.generate_async(...)`) for high‑throughput services.
- **Redirecting logs to a file** or a structured logging system like `loguru` for production diagnostics.
- **Combining multiple instances** (e.g., one for quick answers, another for heavy‑weight reasoning) within the same application.

Each of these builds on the foundation we’ve laid here, letting you scale from a simple script to a full‑blown AI‑powered backend.

---

*Happy coding! If you hit any snags while trying to **create AsposeAI instance**, drop a comment below—I'm happy to help.*


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Extract OCR – OCR Configuration](/ocr/english/net/ocr-configuration/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}