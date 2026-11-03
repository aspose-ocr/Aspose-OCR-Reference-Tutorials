---
category: general
date: 2026-06-25
description: Get OCR supported characters quickly using the aocr library. Learn how
  to list OCR characters, set languages, and debug your OCR engine in Python.
draft: false
keywords:
- get OCR supported characters
- OCR engine Python
- list OCR characters
- supported OCR languages
- aocr library
language: en
og_description: Get OCR supported characters with aocr. This guide shows you how to
  list OCR characters, choose languages, and handle edge cases in Python.
og_title: Get OCR Supported Characters in Python – Full Tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Get OCR supported characters quickly using the aocr library. Learn
    how to list OCR characters, set languages, and debug your OCR engine in Python.
  headline: Get OCR Supported Characters in Python – Complete Guide
  type: TechArticle
- description: Get OCR supported characters quickly using the aocr library. Learn
    how to list OCR characters, set languages, and debug your OCR engine in Python.
  name: Get OCR Supported Characters in Python – Complete Guide
  steps:
  - name: What if the language pack is missing?
    text: 'If you request a language that isn’t bundled, `aocr.Language` won’t contain
      the enum, and you’ll hit an `AttributeError`. Guard against this with a simple
      check:'
  - name: Empty character list
    text: 'Some niche languages might return an empty list if the underlying training
      data is incomplete. In that scenario, you can fall back to a default (e.g.,
      English) or raise a warning:'
  - name: Unicode normalization
    text: 'The list may contain combined characters (e.g., “é” as `e` + acute accent).
      If your downstream processing expects pre‑composed glyphs, run a normalization
      step:'
  type: HowTo
- questions:
  - answer: Yes, the `get_supported_characters()` method is stable across 1.x and
      2.x. The only change is that language enums were moved to `aocr.languages`.
    question: Does this work with aocr version 2.x?
  - answer: 'Absolutely. Use `ord(ch)` inside a list comprehension: ```python code_points
      = [hex(ord(ch)) for ch in supported_chars] ```'
    question: Can I get the Unicode code point for each character?
  - answer: 'aocr includes an `ARABIC` enum. The character list will contain Arabic
      glyphs, but you may need to enable RTL rendering in your downstream UI. ---
      ## Conclusion You now know **how to get OCR supported characters** using the
      aocr library in Python, how to switch between **supported OCR languages**, a'
    question: What about right‑to‑left scripts like Arabic?
  type: FAQPage
tags:
- OCR
- Python
- aocr
title: Get OCR Supported Characters in Python – Complete Guide
url: /python/general/get-ocr-supported-characters-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Get OCR Supported Characters in Python – Complete Guide

Ever wondered how to **get OCR supported characters** for a specific language when you’re tinkering with an OCR engine? You’re not alone. Whether you’re building a receipt scanner or a multilingual document parser, knowing exactly which glyphs your engine can recognize is a lifesaver. In this tutorial we’ll walk through the whole process—installing the library, configuring the language, and finally listing those characters—so you can debug and fine‑tune your OCR pipeline in minutes.

We’ll use the **aocr** library, a lightweight Python OCR engine that makes it painless to query language capabilities. By the end of this guide you’ll be able to **list OCR characters**, switch between **supported OCR languages**, and even spot gaps in coverage before they bite you in production.

---

## Prerequisites

Before we dive in, make sure you have:

* Python 3.8 or newer (the aocr package drops support for 3.7)
* A terminal or command prompt with internet access
* Basic familiarity with Python scripting (if you’ve written a `print()` before, you’re good)

No heavy external dependencies—just the `aocr` pip package.

---

## Install the aocr Library (OCR Engine Python)

The first thing you need is a working **OCR engine Python** installation. The aocr package ships on PyPI, so a single pip command does the trick:

```bash
pip install aocr
```

If you’re using a virtual environment (highly recommended), activate it first:

```bash
python -m venv .venv
source .venv/bin/activate   # macOS/Linux
.\.venv\Scripts\activate    # Windows
```

> **Pro tip:** Pin the version (`pip install aocr==1.2.4`) to avoid unexpected API changes later on.

---

## Choose a Language (Supported OCR Languages)

aocr ships with a handful of built‑in language packs. Each pack defines the set of Unicode code points the engine can recognize. To query those packs you’ll need to set the `language` attribute on the engine instance.

```python
import aocr

# Create the OCR engine instance
ocr_engine = aocr.OcrEngine()

# Pick the language you care about – here we use English
ocr_engine.language = aocr.Language.ENGLISH
```

You can replace `aocr.Language.ENGLISH` with any other enum value (`FRENCH`, `GERMAN`, etc.). If you attempt to assign a language that isn’t bundled, aocr raises a `ValueError`. That’s why it’s a good idea to check the **supported OCR languages** list first:

```python
print("Available languages:", [lang.name for lang in aocr.Language])
```

---

## Retrieve the Set of Characters (Get OCR Supported Characters)

Now comes the heart of the tutorial: actually **get OCR supported characters**. The engine exposes a handy method called `get_supported_characters()` which returns a list of single‑character strings.

```python
# Step 3: Retrieve the set of characters that the engine can recognize
supported_chars = ocr_engine.get_supported_characters()
```

Behind the scenes, aocr reads a JSON file bundled with the language pack and converts each Unicode code point into a Python string. The result is deterministic, meaning you’ll get the same list every time you run the script on the same language version.

---

## Show How Many Characters Are Supported

Knowing the count helps you quickly gauge the breadth of coverage. For English, you’ll typically see a few thousand characters (including punctuation and digits).

```python
# Step 4: Show how many characters are supported
print(f"{len(supported_chars)} characters supported for ENGLISH:")
```

The `len()` call is O(1) because Python stores the list length internally, so there’s no performance penalty even for large alphabets.

---

## Preview the First 100 Supported Characters

A quick visual check can reveal whether the engine includes the symbols you need (think of the Euro sign or smart quotes). Let’s print the first hundred characters:

```python
# Step 5: Preview the first 100 supported characters
print("".join(supported_chars[:100]), "...")
```

The `join` operation concatenates the slice into a single string, which is more readable than printing a Python list.

---

## Full Script – All Steps in One Place

Below is the complete, runnable example that ties everything together. Save it as `list_supported_chars.py` and run `python list_supported_chars.py` from your terminal.

```python
# list_supported_chars.py
"""
Complete example showing how to get OCR supported characters
using the aocr library in Python.
"""

import aocr

def main():
    # 1️⃣ Create an OCR engine instance
    ocr_engine = aocr.OcrEngine()

    # 2️⃣ Select the language you want to work with (e.g., English)
    # You can change this to any language supported by aocr.
    ocr_engine.language = aocr.Language.ENGLISH

    # 3️⃣ Retrieve the set of characters that the engine can recognize
    supported_chars = ocr_engine.get_supported_characters()

    # 4️⃣ Show how many characters are supported
    print(f"{len(supported_chars)} characters supported for ENGLISH:")

    # 5️⃣ Preview the first 100 supported characters
    preview = "".join(supported_chars[:100])
    print(preview, "...")

if __name__ == "__main__":
    main()
```

**Expected output (truncated for brevity):**

```
2565 characters supported for ENGLISH:
ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789.,!?'"()[]{}-+*/%$#@&... 
```

The exact count may differ slightly depending on the aocr version, but you’ll always see a long alphabet plus common punctuation.

---

## Handling Edge Cases

### What if the language pack is missing?

If you request a language that isn’t bundled, `aocr.Language` won’t contain the enum, and you’ll hit an `AttributeError`. Guard against this with a simple check:

```python
if hasattr(aocr.Language, "SPANISH"):
    ocr_engine.language = aocr.Language.SPANISH
else:
    raise RuntimeError("Spanish language pack not installed.")
```

### Empty character list

Some niche languages might return an empty list if the underlying training data is incomplete. In that scenario, you can fall back to a default (e.g., English) or raise a warning:

```python
if not supported_chars:
    print("Warning: No characters returned for the selected language.")
```

### Unicode normalization

The list may contain combined characters (e.g., “é” as `e` + acute accent). If your downstream processing expects pre‑composed glyphs, run a normalization step:

```python
import unicodedata
normalized = [unicodedata.normalize("NFC", ch) for ch in supported_chars]
```

---

## Pro Tips for Real‑World Projects

* **Cache the character list** – If you’re processing thousands of images, calling `get_supported_characters()` on every iteration adds unnecessary overhead. Store the list in a module‑level variable or serialize it to JSON for later reuse.
* **Cross‑language validation** – When you support multiple languages in a single app, intersect the character sets to find a common subset. This helps you design UI elements that stay consistent across locales.
* **Debugging OCR failures** – If the engine misclassifies a glyph, compare the offending character against the output of `list_supported_chars`. If it’s missing, you’ve identified a coverage gap that may require a custom training step.
* **Combine with custom fonts** – aocr respects the Unicode range, but rendering quality can vary by font. Test your supported characters with the exact font you’ll use in production to avoid surprises.

---

## Frequently Asked Questions

**Q: Does this work with aocr version 2.x?**  
A: Yes, the `get_supported_characters()` method is stable across 1.x and 2.x. The only change is that language enums were moved to `aocr.languages`.

**Q: Can I get the Unicode code point for each character?**  
A: Absolutely. Use `ord(ch)` inside a list comprehension:

```python
code_points = [hex(ord(ch)) for ch in supported_chars]
```

**Q: What about right‑to‑left scripts like Arabic?**  
A: aocr includes an `ARABIC` enum. The character list will contain Arabic glyphs, but you may need to enable RTL rendering in your downstream UI.

---

## Conclusion

You now know **how to get OCR supported characters** using the aocr library in Python, how to switch between **supported OCR languages**, and why **listing OCR characters** is essential for robust text‑recognition pipelines. Armed with the full script and the tips above, you can quickly verify language coverage, debug missing glyphs, and build smarter OCR‑driven applications.

Ready for the next step? Try pairing this character list with a custom word‑list filter, or experiment with a different OCR engine (Tesseract, EasyOCR) and compare the results. The more you explore, the better your OCR solutions will become.

Happy coding, and may your character sets always be complete!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Specify Allowed Characters OCR – Using Aspose.OCR for .NET](/ocr/english/net/ocr-settings/specify-allowed-characters/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [OCR Post Processing – Get Character Choices](/ocr/english/net/text-recognition/get-choices-for-recognized-characters/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}