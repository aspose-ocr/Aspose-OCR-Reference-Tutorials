---
category: general
date: 2026-06-19
description: 如何在 Python 中使用 OCR 提取 PDF – 步驟教學，涵蓋從 PDF 抽取文字、從圖像辨識文字，以及 OCR Python 範例。
draft: false
keywords:
- how to extract pdf
- extract text from pdf
- recognize text from image
- ocr python example
- read pdf with ocr
language: zh-hant
og_description: 如何使用 Python 進行 OCR 從 PDF 中提取文字。學習從 PDF 提取文字、從圖像辨識文字，並查看完整的 OCR Python
  範例。
og_title: 如何在 Python 中使用 OCR 提取 PDF 文字 – 完整教學
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to extract PDF using OCR in Python – step‑by‑step tutorial covering
    extract text from PDF, recognize text from image, and an OCR Python example.
  headline: How to Extract PDF Text with OCR in Python – Complete Guide
  type: TechArticle
- description: How to extract PDF using OCR in Python – step‑by‑step tutorial covering
    extract text from PDF, recognize text from image, and an OCR Python example.
  name: How to Extract PDF Text with OCR in Python – Complete Guide
  steps:
  - name: – Install the Required Packages
    text: First, we need an OCR engine. The example below uses the popular **ocr**
      package (a thin wrapper around Tesseract). If you prefer a different backend,
      the concepts stay the same.
  - name: – Initialize the OCR Engine and Set Language
    text: Now we spin up the engine and tell it to look for English characters. You
      can swap `ocr.Language.English` for any supported language code.
  - name: – Load a PDF Page as an Image
    text: OCR works on raster images, not PDF objects. The `ocr.Image.from_pdf` helper
      renders the chosen page to a bitmap. Adjust `page_number` for other pages (0‑based
      indexing).
  - name: – Recognize Text from the Rendered Image
    text: Here’s the heart of the **ocr python example**. The engine processes the
      bitmap and returns an object containing the extracted string.
  - name: – Print or Store the Extracted Text
    text: Finally, we output the result. In a real application you’d probably write
      to a file or a database.
  type: HowTo
tags:
- OCR
- Python
- PDF
- Text Extraction
title: 如何在 Python 中使用 OCR 提取 PDF 文字 – 完整指南
url: /zh-hant/python-java/general/how-to-extract-pdf-text-with-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Python OCR 提取 PDF 文字 – 完整指南

有沒有想過 **如何在 PDF 只是一張掃描圖像時** 取得其中的內容？你並不孤單。在許多實務專案中——例如合約、發票或歷史檔案——收到的 PDF 往往沒有可選取的文字。好消息是，只要幾行 Python 程式碼，就能把只有圖像的頁面轉換成可搜尋、可編輯的文字。

在本教學中，我們將一步步示範一個實用的 **OCR Python 範例**，讀取 PDF、將第一頁渲染成圖像，然後使用 OCR 引擎 **從 PDF 中提取文字**。完成後，你將清楚知道如何 **使用 OCR 讀取 PDF**、每個步驟的意義，以及如何將程式碼延伸至多頁文件或不同語言。

## 你將學到

- 安裝與設定可靠的 Python OCR 套件。  
- 將 PDF 頁面轉換為適合 OCR 的圖像。  
- **從圖像辨識文字** 並取得乾淨的 Unicode 字串。  
- 常見陷阱（低解析度 PDF、旋轉頁面）以及避免方法。  
- 擴充腳本以處理多頁或批次作業。

**先備條件**：Python 3.8+、pip，以及基本的虛擬環境概念。不需要先前的 OCR 經驗——只要跟著做即可。

---

## ## How to Extract PDF Text with OCR in Python

這個 H2 標題正好包含主要關鍵字，搜尋引擎會很喜歡。讓我們直接進入程式碼。

### Step 1 – Install the Required Packages

First, we need an OCR engine. The example below uses the popular **ocr** package (a thin wrapper around Tesseract). If you prefer a different backend, the concepts stay the same.

```bash
# Create a fresh virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate

# Install the OCR wrapper and Pillow for image handling
pip install ocr pillow
```

> **Pro tip:** On Linux, you’ll also need the Tesseract binary: `sudo apt-get install tesseract-ocr`. macOS users can grab it via Homebrew: `brew install tesseract`.

### Step 2 – Initialize the OCR Engine and Set Language

Now we spin up the engine and tell it to look for English characters. You can swap `ocr.Language.English` for any supported language code.

```python
import ocr

# Step 1: Create an OCR engine and set the language to English
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.English
```

**Why this matters:** Specifying the language dramatically improves accuracy because the engine can apply language‑specific dictionaries and character models.

### Step 3 – Load a PDF Page as an Image

OCR works on raster images, not PDF objects. The `ocr.Image.from_pdf` helper renders the chosen page to a bitmap. Adjust `page_number` for other pages (0‑based indexing).

```python
# Step 2: Load the first page of the PDF as an image
pdf_file_path = "YOUR_DIRECTORY/contract.pdf"
page_image = ocr.Image.from_pdf(pdf_file_path, page_number=1)
```

> **Edge case:** If the PDF contains vector graphics rather than scanned images, you might get a crisp rendering. For low‑resolution scans, consider increasing the DPI: `ocr.Image.from_pdf(..., dpi=300)`.

### Step 4 – Recognize Text from the Rendered Image

Here’s the heart of the **ocr python example**. The engine processes the bitmap and returns an object containing the extracted string.

```python
# Step 3: Recognize text from the rendered page image
ocr_result = ocr_engine.recognize(page_image)
```

The `ocr_result.text` attribute holds the plain‑text output, preserving line breaks where possible.

### Step 5 – Print or Store the Extracted Text

Finally, we output the result. In a real application you’d probably write to a file or a database.

```python
# Step 4: Print the extracted text
print(ocr_result.text)
```

Running the script should display something like:

```
THIS AGREEMENT is made on the 1st day of January 2024...
```

That’s a complete **extract text from pdf** workflow using OCR.

---

## ## Recognize Text from Image – Tweaking Accuracy

If you’re only interested in **recognize text from image** (say, a JPEG of a receipt), you can skip the PDF conversion step:

```python
image_path = "receipt.jpg"
page_image = ocr.Image.from_file(image_path)   # Directly load an image
ocr_result = ocr_engine.recognize(page_image)
print(ocr_result.text)
```

**Tips for better results:**

- **Pre‑process** the image: convert to grayscale, apply thresholding, or deskew. Pillow makes this easy.
- **Increase DPI** during PDF rendering: higher resolution gives the OCR engine more detail.
- **Enable OCR engine’s config** for page segmentation (`ocr_engine.config = "--psm 6"` for uniform blocks).

---

## ## Read PDF with OCR – Handling Multiple Pages

Most contracts span several pages. Looping over each page is straightforward:

```python
def extract_all_pages(pdf_path):
    all_text = []
    for i in range(ocr.Image.pdf_page_count(pdf_path)):
        img = ocr.Image.from_pdf(pdf_path, page_number=i)
        result = ocr_engine.recognize(img)
        all_text.append(result.text)
    return "\n--- PAGE BREAK ---\n".join(all_text)

full_text = extract_all_pages("YOUR_DIRECTORY/contract.pdf")
print(full_text)
```

This function **reads PDF with OCR**, concatenates the output, and inserts a clear page break marker. You can then feed `full_text` into a search index or store it as a `.txt` file.

---

## ## Common Pitfalls and How to Fix Them

| 症狀 | 可能原因 | 解決方法 |
|---------|--------------|-----|
| 文字雜亂、出現大量 `?` | 語言設定錯誤或缺少語言資料檔 | 安裝正確的 Tesseract 語言套件（`tesseract-ocr-<lang>`）並設定 `ocr_engine.language`。 |
| 缺少行或字被截斷 | DPI 太低（低於 150） | 以 300 DPI 或更高解析度渲染 PDF（`dpi=300`）。 |
| 文字旋轉或倒置 | 掃描頁面未正立 | 在辨識前使用 `ocr.Image.deskew(page_image)` 進行去斜。 |
| 大型 PDF 處理緩慢 | 單執行緒逐頁處理 | 使用 `concurrent.futures.ThreadPoolExecutor` 進行平行化。 |

---

## ## Extending the OCR Python Example

- **Export to PDF/A**: After extraction, you can embed the text back into a searchable PDF using `reportlab` or `pypdf2`.
- **Language detection**: Use `langdetect` on the OCR output to switch `ocr_engine.language` dynamically.
- **Batch processing**: Walk a directory with `os.listdir` and apply `extract_all_pages` to every file.

---

## ## Expected Output and Verification

When you run the script against a clear, English‑language scan, you should see a clean block of text with proper punctuation. Verify by:

1. Comparing a few lines to the original scanned image.  
2. Running a simple word count (`len(ocr_result.text.split())`) to ensure the output isn’t empty.  
3. Optionally, feeding the result into a spell‑checker like `pyspellchecker` to spot OCR errors.

---

## Conclusion

We’ve covered **how to extract PDF** content when traditional parsing fails, demonstrated a full **ocr python example**, and explained how to **recognize text from image** and **read PDF with OCR** for both single‑page and multi‑page scenarios. With the code snippets above you can now turn any scanned PDF into searchable, editable text—no more manual re‑typing.

Next steps? Try swapping the language to Spanish (`ocr.Language.Spanish`) or experiment with image pre‑processing techniques to boost accuracy. If you’re building a document‑management system, consider indexing the extracted text with Elasticsearch for lightning‑fast search.

Got questions or run into a quirky PDF? Drop a comment, and happy coding!  

![How to extract PDF using OCR in Python](image.png "How to extract PDF using OCR in Python")

## What Should You Learn Next?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}