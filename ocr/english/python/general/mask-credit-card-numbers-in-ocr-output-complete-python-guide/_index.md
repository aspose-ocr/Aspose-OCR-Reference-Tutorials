---
category: general
date: 2026-04-26
description: Mask credit card numbers quickly using AsposeAI OCR post‑processing.
  Learn PCI compliance, regular expression masking, and data sanitization in a step‑by‑step
  tutorial.
draft: false
keywords:
- mask credit card numbers
- PCI compliance
- OCR post‑processing
- AsposeAI
- regular expression masking
- data sanitization
language: en
og_description: Mask credit card numbers in OCR results with AsposeAI. This tutorial
  covers PCI compliance, regular expression masking, and data sanitization.
og_title: Mask Credit Card Numbers – Full Python OCR Post‑Processing Guide
tags:
- OCR
- Python
- security
title: Mask Credit Card Numbers in OCR Output – Complete Python Guide
url: /python/general/mask-credit-card-numbers-in-ocr-output-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mask Credit Card Numbers – Complete Python Guide

Ever needed to **mask credit card numbers** in text that comes straight from an OCR engine?  You’re not the only one.  In regulated industries, exposing a full PAN (Primary Account Number) can land you in hot water with PCI compliance auditors.  The good news?  With a few lines of Python and AsposeAI’s post‑processing hook, you can automatically hide the middle eight digits and stay on the safe side.

In this tutorial we’ll walk through a real‑world scenario: running OCR on a receipt image, then applying a custom **OCR post‑processing** function that sanitizes any PCI data.  By the end you’ll have a reusable snippet that you can drop into any AsposeAI workflow, plus a handful of practical tips for handling edge cases and scaling the solution.

## What You’ll Learn

- How to register a custom post‑processor with **AsposeAI**.
- Why a **regular expression masking** approach is both fast and reliable.
- The basics of **PCI compliance** related to data sanitization.
- Ways to extend the pattern for multiple card formats or international numbers.
- Expected output and how to verify that the masking worked.

> **Prerequisites** – You should have a working Python 3 environment, the Aspose.AI for OCR package installed (`pip install aspose-ocr`), and a sample image (e.g., `receipt.png`) that contains a credit‑card number. No other external services are required.

---

## Step 1: Define a Post‑Processor that Masks Credit Card Numbers

The heart of the solution lives in a tiny function that receives the OCR result, runs a **regular expression masking** routine, and returns the sanitized text.

```python
def mask_pci(data, settings):
    """
    Replace the middle 8 digits of any 16‑digit card number with asterisks.
    Keeps the first and last four digits visible for reference.
    """
    import re
    # Pattern captures groups: first 4 digits, middle 8, last 4
    pattern = r'(\d{4})\d{8}(\d{4})'
    # Replace middle portion with ****
    return re.sub(pattern, r'\1****\2', data.text)
```

**Why this works:**  
- The regex `(\d{4})\d{8}(\d{4})` matches exactly 16 consecutive digits, the common format for Visa, MasterCard, and many others.  
- By capturing the first and last four digits (`\1` and `\2`) we preserve enough information for debugging while complying with **PCI compliance** rules that forbid storing the full PAN.  
- The substitution `\1****\2` hides the sensitive middle eight digits, turning `1234567812345678` into `1234****5678`.

> **Pro tip:** If you need to support 15‑digit American Express numbers, add a second pattern like `r'(\d{4})\d{6}(\d{5})'` and run both replacements sequentially.

---

## Step 2: Initialise the AsposeAI Engine

Before we can attach our post‑processor, we need an instance of the OCR engine.  AsposeAI bundles the OCR model and a simple API for custom processing.

```python
from aspose.ocr import AsposeAI

# Initialise the AI engine – it will handle image loading, recognition, and post‑processing
ai = AsposeAI()
```

**Why initialise here?**  
Creating the `AsposeAI` object once and reusing it across multiple images reduces overhead.  The engine also caches language models, which speeds up subsequent calls—handy when you’re scanning batches of receipts.

---

## Step 3: Register the Custom Masking Function

AsposeAI exposes a `set_post_processor` method that lets you plug in any callable.  We pass our `mask_pci` function along with an optional settings dictionary (empty for now).

```python
# Register our masking routine; custom_settings can hold flags like "log_masked" if you expand later
ai.set_post_processor(mask_pci, custom_settings={})
```

**What’s happening behind the scenes?**  
When you later invoke `run_postprocessor`, AsposeAI will hand the raw OCR result to `mask_pci`.  The function receives a lightweight object (`data`) that contains the recognized text, and you return a new string.  This design keeps the core OCR untouched while letting you enforce **data sanitization** policies in a single place.

---

## Step 4: Run OCR on the Receipt Image

Now that the engine knows how to clean the output, we feed it an image.  For the sake of this tutorial we assume you already have an `engine` object configured with the right language and resolution settings.

```python
# Assume `engine` is a pre‑configured OCR object (e.g., with language='en')
ocr_engine = engine
raw_result = ocr_engine.recognize_image("receipt.png")
```

**Tip:** If you don’t have a pre‑configured object, you can create one with:

```python
from aspose.ocr import OcrEngine
ocr_engine = OcrEngine(language='en')
```

The `recognize_image` call returns an object whose `text` attribute holds the raw, unmasked string.

---

## Step 5: Apply the Registered Post‑Processor

With the raw OCR data in hand, we hand it over to the AI instance.  The engine automatically runs the `mask_pci` function we registered earlier.

```python
# This triggers the post‑processor and returns a new result object
final_result = ai.run_postprocessor(raw_result)
```

**Why use `run_postprocessor` instead of calling the function manually?**  
Doing so keeps the workflow consistent, especially when you have multiple post‑processors (e.g., spell‑checking, language detection).  AsposeAI queues them in the order you register, guaranteeing deterministic output.

---

## Step 6: Verify the Sanitized Output

Finally, let’s print the sanitized text and confirm that any credit‑card numbers are properly masked.

```python
print(final_result.text)
```

**Expected output** (excerpt):

```
Purchase at Café Latte – Total: $4.75
Card: 1234****5678
Date: 2026-04-25
Thank you!
```

If the receipt contained no card number, the text remains unchanged—nothing to mask, nothing to worry about.

---

## Handling Edge Cases and Common Variations

### Multiple Card Numbers in One Document
If a receipt includes more than one PAN (e.g., a loyalty card plus a payment card), the regex runs globally, masking all matches automatically. No extra code needed.

### Non‑Standard Formatting
Sometimes OCR inserts spaces or dashes (`1234 5678 1234 5678` or `1234-5678-1234-5678`). Extend the pattern to ignore those characters:

```python
pattern = r'(\d{4})[ -]?\d{4}[ -]?\d{4}[ -]?\d{4}'
```

The added `[ -]?` tolerates optional spaces or hyphens between digit blocks.

### International Cards
For 19‑digit PANs used in some regions, you can broaden the pattern:

```python
pattern = r'(\d{4})\d{11,15}(\d{4})'
```

Just remember that **PCI compliance** still mandates masking the middle digits, regardless of length.

### Logging Masked Values (Optional)
If you need audit trails, pass a flag via `custom_settings` and adjust the function:

```python
def mask_pci(data, settings):
    import re, logging
    pattern = r'(\d{4})\d{8}(\d{4})'
    def repl(match):
        masked = f"{match.group(1)}****{match.group(2)}"
        if settings.get('log'):
            logging.info(f"Masked PAN: {masked}")
        return masked
    return re.sub(pattern, repl, data.text)
```

Then register with:

```python
ai.set_post_processor(mask_pci, custom_settings={'log': True})
```

---

## Full Working Example (Copy‑Paste Ready)

```python
# ------------------------------------------------------------
# Mask Credit Card Numbers in OCR Output – Complete Example
# ------------------------------------------------------------
import re
from aspose.ocr import AsposeAI, OcrEngine

# 1️⃣ Define the post‑processor
def mask_pci(data, settings):
    """
    Hide the middle eight digits of any 16‑digit credit‑card number.
    """
    pattern = r'(\d{4})\d{8}(\d{4})'          # keep first & last 4 digits
    return re.sub(pattern, r'\1****\2', data.text)

# 2️⃣ Initialise the OCR engine and AsposeAI wrapper
ocr_engine = OcrEngine(language='en')       # configure as needed
ai = AsposeAI()

# 3️⃣ Register the masking function
ai.set_post_processor(mask_pci, custom_settings={})

# 4️⃣ Run OCR on a sample receipt
raw_result = ocr_engine.recognize_image("receipt.png")

# 5️⃣ Apply post‑processing (masking)
final_result = ai.run_postprocessor(raw_result)

# 6️⃣ Display sanitized text
print("Sanitized OCR output:")
print(final_result.text)
```

Running this script on a receipt that contains `4111111111111111` will produce:

```
Sanitized OCR output:
Purchase at Bookstore – $12.99
Card: 4111****1111
Date: 2026-04-26
```

That’s the whole pipeline—from raw OCR to **data sanitization**—wrapped in a few clean lines of Python.

---

## Conclusion

We’ve just shown you how to **mask credit card numbers** in OCR results using AsposeAI’s post‑processing hook, a concise regular‑expression routine, and a handful of best‑practice tips for **PCI compliance**.  The solution is fully self‑contained, works with any image that the OCR engine can read, and can be extended to cover more complex card formats or logging requirements.

Ready for the next step? Try coupling this mask with a **database insertion** routine that stores only the last four digits for reference, or integrate a **batch processor** that scans an entire folder of receipts overnight.  You might also explore other **OCR post‑processing** tasks like address standardization or language detection—each follows the same pattern we used here.

Got questions about edge cases, performance, or how to adapt the code for a different OCR library? Drop a comment below, and let’s keep the conversation going. Happy coding, and stay secure!  



![Diagram illustrating how mask credit card numbers works in an OCR pipeline](https://example.com/images/ocr-mask-flow.png "Diagram of OCR post‑processing masking flow")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}