---
category: general
date: 2026-06-25
description: 使用 Python 對 PDF 進行光學字符辨識（OCR）——學習如何載入 PDF 以執行 OCR、從 PDF 頁面提取文字，並有效預覽辨識結果。
draft: false
keywords:
- perform OCR on PDF
- extract text from PDF pages
- load PDF for OCR
- how to OCR large PDF
- preview recognized text
language: zh-hant
og_description: 在 Python 中對 PDF 進行 OCR。本指南說明如何載入 PDF 以執行 OCR、從 PDF 頁面提取文字，以及快速預覽辨識出的文字。
og_title: 使用 Python 對 PDF 進行 OCR – 步驟教學
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Perform OCR on PDF using Python—learn how to load PDF for OCR, extract
    text from PDF pages, and preview recognized text efficiently.
  headline: Perform OCR on PDF with Python – Complete Guide
  type: TechArticle
- description: Perform OCR on PDF using Python—learn how to load PDF for OCR, extract
    text from PDF pages, and preview recognized text efficiently.
  name: Perform OCR on PDF with Python – Complete Guide
  steps:
  - name: '**Parallelize per page** – Use `concurrent.futures.ThreadPoolExecutor`
      if the OCR engine is thread‑safe.'
    text: '**Parallelize per page** – Use `concurrent.futures.ThreadPoolExecutor`
      if the OCR engine is thread‑safe.'
  - name: '**Cache intermediate images** – Some engines let you store rasterized pages
      on SSD, dramatically cutting CPU load on re‑runs.'
    text: '**Cache intermediate images** – Some engines let you store rasterized pages
      on SSD, dramatically cutting CPU load on re‑runs.'
  - name: '**Batch write output** – Instead of appending to a Python list, open the
      output file once and write each page’s text as soon as it’s ready.'
    text: '**Batch write output** – Instead of appending to a Python list, open the
      output file once and write each page’s text as soon as it’s ready.'
  - name: '**Adjust DPI** – Lowering the DPI during rasterization reduces memory but
      may affect accuracy; find a sweet spot (usually 200‑300 DPI).'
    text: '**Adjust DPI** – Lowering the DPI during rasterization reduces memory but
      may affect accuracy; find a sweet spot (usually 200‑300 DPI).'
  type: HowTo
tags:
- OCR
- Python
- PDF processing
title: 使用 Python 對 PDF 進行 OCR – 完整指南
url: /zh-hant/python/general/perform-ocr-on-pdf-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Python 中對 PDF 進行 OCR – 完整指南

曾經需要對 **perform OCR on PDF** 檔案執行 OCR，但不知從何入手嗎？也許你有一大堆掃描的合約，或是一份龐大的手冊，無法配合你平常的文字提取工具。簡而言之，你想要 **load PDF for OCR**，提取文字，並快速預覽——且不會耗盡機器記憶體。

好消息，你來對地方了。在本教學中，我們將逐步說明一個完整的 Python 腳本，**extracts text from PDF pages**，示範如何 **preview recognized text**，甚至解決 **how to OCR large PDF** 的經典問題。

完成後，你將擁有一個可直接執行的程式、對每個設定參數的清晰了解，以及避免新手常見陷阱的多項技巧。

---

## 你將學會什麼

- 如何使用 `aocr` 套件 **load PDF for OCR**。
- 逐頁 **perform OCR on PDF** 的完整步驟。
- 在控制記憶體使用量的同時 **extract text from PDF pages** 的方法。
- 如何 **preview recognized text** 以檢查結果的合理性。
- 處理 **large PDFs** 而不耗盡記憶體的策略。

> **提示：** 本指南假設你已安裝 Python 3.9 以上，並對虛擬環境有基本了解。如果你是 Python 新手，請先建立 virtualenv——相信我，之後會省下很多麻煩。

---

## 前置條件

| 需求 | 原因說明 |
|------|----------|
| `aocr` Python 套件（或任何相容的 OCR 引擎） | 提供腳本中使用的 `OcrEngine` 類別。 |
| `pip` 與虛擬環境 | 將相依套件與系統 Python 隔離。 |
| 足夠的磁碟空間以暫存影像抽取 | 部分 OCR 引擎會在處理前將頁面影像寫入磁碟。 |
| 可選：`tqdm` 進度條 | 在處理 **how to OCR large PDF** 任務時提升使用者體驗。 |

使用以下指令安裝必要套件：

```bash
python -m venv ocr-env
source ocr-env/bin/activate   # Windows: ocr-env\Scripts\activate
pip install aocr tqdm
```

如果你的 PDF 受密碼保護，稍後需要提供密碼——請參閱「Edge Cases」章節。

---

## 步驟 1：Perform OCR on PDF – 設定引擎

首先，我們需要建立一個 OCR 引擎實例。它就像大腦，會讀取每頁的影像並輸出純文字。

```python
import aocr                     # The OCR library
from tqdm import tqdm           # Optional, for a nice progress bar

def create_engine():
    """
    Initialise the OcrEngine with sensible defaults.
    Returns the configured engine ready for processing.
    """
    engine = aocr.OcrEngine()
    # Limit memory usage – crucial when tackling how to OCR large PDF files
    engine.max_memory_mb = 200               # 200 MB cap, adjust if needed
    # Choose a recognition mode that matches your source material
    engine.recognition_mode = aocr.RecognitionMode.PRINTED
    return engine
```

> **為何設定 `max_memory_mb`？**  
> OCR 引擎常會在記憶體中快取頁面影像。透過限制記憶體使用量，可防止在處理 500 頁合約時腳本崩潰。

---

## 步驟 2：Load PDF for OCR 並設定參數

現在我們真正 **load PDF for OCR**。路徑可以是絕對或相對路徑，只要確保檔案存在即可。

```python
def load_pdf(engine, pdf_path):
    """
    Loads the PDF into the OCR engine.
    Raises FileNotFoundError if the file does not exist.
    """
    try:
        engine.load_pdf(pdf_path)
        print(f"✅ Loaded '{pdf_path}' – {engine.page_count} pages ready.")
    except Exception as e:
        raise RuntimeError(f"Failed to load PDF: {e}")
```

如果 PDF 被加密，`engine.load_pdf` 通常會拋出例外。此時可改為呼叫 `engine.load_pdf(pdf_path, password="secret")`——稍後會詳細說明。

---

## 步驟 3：Extract Text from PDF Pages – 核心迴圈

這裡是逐頁 **perform OCR on PDF** 的地方。我們也會 **preview recognized text** 前幾百個字元，以便驗證是否正常運作。

```python
def ocr_pages(engine, preview_len=200):
    """
    Iterates over each page, runs OCR, and yields the recognized text.
    Also prints a short preview for each page.
    """
    for page_index in tqdm(range(engine.page_count), desc="Processing pages"):
        # Select the current page – essential for multi‑page PDFs
        engine.select_page(page_index)

        # Perform the actual OCR
        page_text = engine.recognize()

        # Preview the first `preview_len` characters (helps with debugging)
        print(f"\n--- Page {page_index + 1} Preview ---")
        print(page_text[:preview_len] + ("…" if len(page_text) > preview_len else ""))

        yield page_text
```

> **專業提示：** `tqdm` 進度條能提供視覺提示，對於處理需要數分鐘的 **how to OCR large PDF** 文件特別有用。

---

## 步驟 4：Putting It All Together – 可直接執行的腳本

以下是完整、可執行的範例。將其儲存為 `pdf_ocr.py`，並以 `python pdf_ocr.py path/to/your/file.pdf` 執行。

```python
#!/usr/bin/env python3
"""
Complete script to perform OCR on PDF, extract text from PDF pages,
and preview recognized text. Works for both small and large PDFs.
"""

import sys
import aocr
from tqdm import tqdm

def create_engine():
    engine = aocr.OcrEngine()
    engine.max_memory_mb = 200
    engine.recognition_mode = aocr.RecognitionMode.PRINTED
    return engine

def load_pdf(engine, pdf_path):
    try:
        engine.load_pdf(pdf_path)
        print(f"✅ Loaded '{pdf_path}' – {engine.page_count} pages.")
    except Exception as exc:
        raise RuntimeError(f"Unable to load PDF: {exc}")

def ocr_pages(engine, preview_len=200):
    for page_index in tqdm(range(engine.page_count), desc="OCR progress"):
        engine.select_page(page_index)
        page_text = engine.recognize()
        print(f"\n--- Page {page_index + 1} Preview ---")
        print(page_text[:preview_len] + ("…" if len(page_text) > preview_len else ""))
        yield page_text

def main(pdf_path):
    engine = create_engine()
    load_pdf(engine, pdf_path)

    all_text = []
    for txt in ocr_pages(engine):
        all_text.append(txt)

    # Optional: write the combined output to a .txt file
    out_path = pdf_path.rsplit(".", 1)[0] + "_ocr.txt"
    with open(out_path, "w", encoding="utf-8") as f:
        f.write("\n\n".join(all_text))
    print(f"\n✅ OCR complete. Full text saved to: {out_path}")

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python pdf_ocr.py <path_to_pdf>")
        sys.exit(1)
    pdf_file = sys.argv[1]
    main(pdf_file)
```

### 預期輸出（節錄）

```
✅ Loaded 'large_contract.pdf' – 342 pages.

--- Page 1 Preview ---
Contract Agreement between Party A and Party B ... 

--- Page 2 Preview ---
Recitals: Whereas, the parties desire to ...

...
✅ OCR complete. Full text saved to: large_contract_ocr.txt
```

你會看到每頁的簡短預覽，最後確認已寫入合併後的文字檔。

---

## 邊緣情況與實用技巧

| 情況 | 處理方式 |
|------|----------|
| **Encrypted PDF** | 傳入密碼：`engine.load_pdf(pdf_path, password="mySecret")`。 |
| **Very large PDF (> 1000 pages)** | 謹慎提升 `max_memory_mb`，或分批處理（例如一次 200 頁）。 |
| **Mixed content (printed + handwritten)** | 若套件支援，將 `engine.recognition_mode` 切換為 `aocr.RecognitionMode.MIXED`。 |
| **Missing fonts or poor scan quality** | 在呼叫 `recognize()` 前，使用影像增強套件（如 Pillow）預處理頁面。 |
| **Out‑of‑memory crashes** | 降低 `preview_len`，或將每頁文字直接寫入磁碟，而非全部保存在列表中。 |

---

## How to OCR Large PDF Efficiently – 進階策略

在處理 **how to OCR large PDF** 時，速度與穩定性變得至關重要。以下提供幾個可加入腳本的技巧：

1. **Parallelize per page** – 若 OCR 引擎支援執行緒安全，可使用 `concurrent.futures.ThreadPoolExecutor`。  
2. **Cache intermediate images** – 部分引擎允許將光柵化頁面存於 SSD，顯著降低重新執行時的 CPU 負載。  
3. **Batch write output** – 與其將文字累加至 Python 列表，不如一次開啟輸出檔，並在每頁文字完成時即寫入。  
4. **Adjust DPI** – 在光柵化時降低 DPI 可減少記憶體使用，但可能影響準確度；請找出最佳平衡點（通常 200‑300 DPI）。

```python
# from concurrent.futures import ThreadPoolExecutor

# def ocr_page(engine, idx):
#     engine.select_page(idx)
#     return engine.recognize()

# with ThreadPoolExecutor(max_workers=4) as executor:
#     results = list(tqdm(executor.map(lambda i: ocr_page(engine, i),
#                                    range(engine.page_count)),
#                     total=engine.page_count,
#                     desc="Parallel OCR"))
```

請記住：平行化可能會提升 CPU 使用率，長時間執行時請留意系統溫度。

---

## 常見問題

**Q: 我可以將此腳本與其他 OCR 套件（如 Tesseract）一起使用嗎？**  
A: 當然可以。只要將 `aocr` 的呼叫改為 `pytesseract.image_to` 即可。

---

## 接下來該學什麼？

以下教學與本指南緊密相關，能在此基礎上進一步深化技巧。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你掌握更多 API 功能，並探索在專案中使用的其他實作方式。

- [如何在 .NET 使用 Aspose.OCR 進行 PDF OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [如何使用 Aspose OCR 從串流執行影像文字提取](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [如何使用 Aspose.OCR for Java 從 URL 提取影像文字](/ocr/english/java/advanced-ocr-techniques/perform-ocr-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}