---
category: general
date: 2026-01-12
description: Python OCR 教學示範如何從圖像中提取表格文字。學習如何從圖像讀取表格，並使用 Aspose OCR 提取選定文字。
draft: false
keywords:
- python ocr tutorial
- extract table text
- read table from image
- extract selected text
- how to extract table
language: zh-hant
og_description: Python OCR 教學，教你如何從圖片中提取表格文字、讀取圖片中的表格，並使用 Aspose OCR 提取選取的文字。
og_title: Python OCR 教學：從圖片中提取表格文字
tags:
- OCR
- Python
- AsposeOCR
title: Python OCR 教學：從圖像中提取表格文字
url: /zh-hant/python-java/general/python-ocr-tutorial-extract-table-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python OCR 教學：從圖像中提取表格文字

有沒有需要一個實際示範如何從掃描表單中提取表格的 **python ocr tutorial**？你並不是唯一有此需求的人。大多數教學只停留在一般文字提取，讓你不知道如何將關注的整齊資料格子分離出來。  

在本指南中，我們將走過一個真實情境：從圖像中讀取表格、只提取你需要的選定文字，最後列印結果。過程中我們也會分享 **how to extract table** 資料的可靠技巧，讓你不必每次都重新發明輪子。

## What You’ll Learn

- 如何為 Python 設定 Aspose OCR。
- 如何定義包含表格的矩形區域。
- **extract table text** 與 **read table from image** 的完整步驟。
- 處理多語言或不規則表格佈局的技巧。
- 一個完整、可直接執行的腳本，今天就能放入你的專案。

**Prerequisites**  
- Python 3.8 或更新版本。  
- 基本的 OCR 概念認識（不需要深入專業知識）。  
- 一張包含清晰表格的 PNG 或 JPEG 圖片（我們稱之為 `form_with_table.png`）。  

如果你已具備上述條件，讓我們直接進入正題——不囉嗦，只給可執行的程式碼。

![python ocr tutorial example of table region](table_region_example.png){alt="python ocr 教學示例顯示表格區域"}

## Step 1: Install and Import Aspose OCR

First things first: you need the Aspose OCR library. The package is on PyPI, so a single `pip` command does the trick.

```bash
pip install aspose-ocr
```

Now import the module and any helpers you’ll need.

```python
# Step 1: Import the Aspose OCR package
import asposeocr as ocr
```

*Pro tip:* Keep your dependencies in a `requirements.txt` file. It makes reproducing the environment a breeze.

## Step 2: Initialise the OCR Engine (Python OCR Tutorial Core)

Creating the engine is the heart of any **python ocr tutorial**. Here we also set the default language to English—feel free to swap it out later.

```python
# Step 2: Create an OCR engine and set the default language
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

Why set the language? OCR accuracy can jump dramatically when the engine knows what characters to expect. If you’re dealing with multilingual forms, you can either set a list of languages or override per region (see later).

## Step 3: Load Your Image

Aspose OCR works with most common image formats. Just point it at the file path, and you’ll have an `Image` object ready for processing.

```python
# Step 3: Load the image that contains the form with the table
image_page = ocr.Image.load("YOUR_DIRECTORY/form_with_table.png")
```

*Edge case:* Large images (over 5 MB) can slow down processing. Consider resizing or compressing them before OCR if performance becomes an issue.

## Step 4: Define the Table Region (Read Table from Image)

Now comes the fun part: telling the engine *where* the table lives. You provide an `OcrRegion` with a `Rectangle` (x, y, width, height). The coordinates are pixel‑based, so you may need to experiment a bit.

```python
# Step 4: Define the rectangular area where the table is located
# (x, y, width, height) – adjust these values for your image
table_region = ocr.OcrRegion(
    image_page,
    ocr.Rectangle(120, 340, 800, 450)
)

# Optional: override language for this specific region
table_region.language = ocr.Language.ENGLISH
```

Why use a region? By limiting OCR to the table area we **extract selected text** faster and avoid noise from surrounding labels or graphics. It also improves accuracy because the engine can focus on a uniform layout.

## Step 5: Run OCR on the Defined Region

With the region set, we invoke `process_region`. The method returns an `OcrResult` object that holds the raw text, confidence scores, and even bounding boxes if you need them later.

```python
# Step 5: Run OCR only on the defined region
region_result = ocr_engine.process_region(table_region)
```

If you need to extract multiple tables, simply repeat Steps 4‑5 with different rectangles.

## Step 6: Output the Extracted Table Text

Finally, print—or store—the table’s textual representation. Aspose OCR returns plain text with line breaks that usually align with rows, making post‑processing straightforward.

```python
# Step 6: Output the extracted table text
print("Table text:\n", region_result.text)
```

**Expected output** (example):

```
Table text:
 Item        Qty   Price
 Apple       10    $1.20
 Banana      5     $0.80
 Orange      8     $1.00
```

You can now feed this string into `csv` parsers, pandas DataFrames, or any downstream analytics pipeline.

## Full Working Example

Putting it all together, here’s the complete script you can run immediately. Replace `YOUR_DIRECTORY/form_with_table.png` with the actual path to your image.

```python
# -*- coding: utf-8 -*-
"""
Python OCR Tutorial: Extract Table Text from Images
---------------------------------------------------
A self‑contained example that demonstrates how to read a table from an image
using Aspose OCR for Python.
"""

# Install the library first:
# pip install aspose-ocr

import asposeocr as ocr

def extract_table(image_path, rect):
    """
    Extracts text from a rectangular region that contains a table.

    :param image_path: Path to the PNG/JPEG image.
    :param rect: Tuple (x, y, width, height) defining the table region.
    :return: Plain‑text representation of the table.
    """
    # Initialise OCR engine with English language
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # Load the image
    img = ocr.Image.load(image_path)

    # Define the region (override language if needed)
    region = ocr.OcrRegion(img, ocr.Rectangle(*rect))
    region.language = ocr.Language.ENGLISH  # optional per‑region override

    # Process only this region
    result = engine.process_region(region)

    return result.text

if __name__ == "__main__":
    # Adjust these coordinates to match your table location
    table_rect = (120, 340, 800, 450)   # x, y, width, height

    # Path to your image file
    img_file = "YOUR_DIRECTORY/form_with_table.png"

    extracted_text = extract_table(img_file, table_rect)
    print("=== Extracted Table Text ===")
    print(extracted_text)
```

Run the script with `python extract_table.py`. If everything lines up, you’ll see the table printed to your console.

## Common Questions & Edge‑Case Handling

**What if the table isn’t perfectly rectangular?**  
You can split the table into multiple overlapping regions or use a larger rectangle that covers the whole area and then post‑process the text (e.g., split on line breaks).

**Can I extract only specific columns?**  
After you have the full table text, use Python’s `csv` or `pandas` to slice out the columns you care about. The OCR step itself returns everything inside the rectangle.

**How do I work with non‑English tables?**  
Set `ocr_engine.language` (or `region.language`) to the appropriate enum, such as `ocr.Language.FRENCH` or combine multiple languages using `ocr.Language.ENGLISH | ocr.Language.SPANISH`.

**Is there a way to get bounding boxes for each cell?**  
Aspose OCR can return `region_result.words` where each word includes a bounding box. You’d need to map those boxes back to a grid—useful for advanced layout analysis.

## Tips for Better Accuracy

- **Clean the image**: Binarize or increase contrast before feeding it to OCR. Libraries like Pillow can help.
- **Avoid compression artifacts**: Save scans as PNG when possible.
- **Mind DPI**: 300 dpi is a sweet spot; lower values can cause missed characters.
- **Test different rectangle sizes**: Slightly larger rectangles often capture stray characters that belong to the table.

## Next Steps

Now that you’ve mastered **how to table** data with Aspose OCR, you might explore:

- Converting the extracted text into a CSV file with Python’s `csv` module.
- Feeding the data into a **pandas** DataFrame for analysis.
- Using OCR to read handwritten forms (requires a different engine or additional training).
- Automating batch processing of dozens of scanned forms using a simple `for` loop.

Each of these extensions builds on the core concepts covered in this **python ocr tutorial**, so you’re well‑positioned to scale up.

---

*Happy coding! If you hit any snags, drop a comment below—I'll be glad to help you fine‑tune the extraction.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}