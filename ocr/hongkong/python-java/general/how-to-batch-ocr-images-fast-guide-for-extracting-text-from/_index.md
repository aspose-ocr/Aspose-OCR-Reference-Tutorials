---
category: general
date: 2026-01-12
description: 如何快速批量 OCR 圖像並從 JPEG 檔案中提取文字（Python）。學習逐步批次處理，提供完整可執行範例。
draft: false
keywords:
- how to batch OCR images
- extract text from JPEG files
language: zh-hant
og_description: 如何批次 OCR 圖像並從 JPEG 檔案中提取文字。本指南將帶您一步步完成一個完整、可直接執行的 Python 解決方案。
og_title: 如何批量 OCR 圖像 – 快速 Python 教學
tags:
- OCR
- Python
- image processing
title: 如何批次 OCR 圖像 – 從 JPEG 檔案提取文字的快速指南
url: /zh-hant/python-java/general/how-to-batch-ocr-images-fast-guide-for-extracting-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何批次 OCR 圖片 – 快速指南：從 JPEG 檔案擷取文字

有沒有想過 **如何批次 OCR 圖片**，卻不需要為每個檔案寫一個獨立腳本？你並不孤單。無論是發票掃描、檔案數位化，或是內容審核，我們常常需要一次性從數十甚至數百張 JPEG 檔案中抽取文字。好消息是，只要幾行 Python 程式碼，就能完成，而且還能得到一個可重複使用的引擎，隨時嵌入任何工作流程。

在本教學中，我們將完整示範 **如何批次 OCR 圖片**，接著說明如何從 JPEG 檔案擷取文字、處理例外情況，並驗證輸出結果。完成後，你將擁有一個自包含的腳本，能對任意資料夾的圖片執行批次處理，並了解批次處理對效能與可維護性的重要性。

## 你將學會

- 建立簡易 OCR 引擎並設定為英文。
- 使用 `pathlib` 收集目錄下所有 JPEG 檔案。
- 只呼叫一次 OCR 引擎，即可處理整批圖片。
- 為每張圖片顯示辨識文字的預覽。
- 處理大型批次、不同語言與常見陷阱的技巧。

**先備條件**：Python 3.8+、`ocr` 套件（或任何相容的封裝），以及一個放置 JPEG 圖片的資料夾。無需外部服務——全部在本機執行。

---

## 步驟 1：初始化 OCR 引擎 – 批次 OCR 圖片的核心

在能 **批次 OCR 圖片** 之前，我們需要一個會讀取文字的引擎。大多數函式庫都是先建立引擎物件，選擇語言，然後在每個檔案上重複使用。

```python
import ocr
import pathlib

# Create the OCR engine and set it to English (the most common case)
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

*為什麼這很重要*：只初始化一次引擎，可避免重複載入語言模型的開銷。也讓你只需在單一位置調整設定（例如 DPI、字元白名單），即可套用到整個批次。

> **專業小技巧**：若要處理多語言文件，將 `ocr.Language.ENGLISH` 改為 `ocr.Language.MULTI`，或在批次開始前載入多個語言包。

---

## 步驟 2：收集所有 JPEG 檔案 – 「從 JPEG 檔案擷取文字」的部分

引擎準備好後，我們需要告訴它要處理哪些圖片。使用 `pathlib` 可讓程式跨平台且簡潔。

```python
# Replace YOUR_DIRECTORY with the path that holds your JPEG files
image_dir = pathlib.Path("YOUR_DIRECTORY/")
image_paths = list(image_dir.glob("*.jpg"))  # only JPEG files, case‑sensitive
```

*為什麼這很重要*：先收集檔案清單，才能一次將整個集合傳給 OCR 引擎——這正是 **如何批次 OCR 圖片** 的核心。如果有子資料夾，只要把 `glob("**/*.jpg")` 改成遞迴搜尋即可。

> **例外情況**：若圖片副檔名混雜（`.jpeg`, `.JPG`），可擴充 glob 模式：`image_dir.rglob("*.[jJ][pP][eE]?g")`。

---

## 步驟 3：一次呼叫處理整批 – 批次 OCR 的真正威力

大多數現代 OCR 函式庫都提供 `process_batch`（或類似）方法，接受可迭代的檔案路徑。這就是高效 **批次 OCR 圖片** 的核心。

```python
# Process every JPEG file in a single batch operation
ocr_results = ocr_engine.process_batch(image_paths)
```

*為什麼這很重要*：一次批次呼叫可減少 Python 與 C 之間的切換次數，保持語言模型常駐記憶體，且常能啟用內部平行化。最終會得到一個物件列表——每個物件包含辨識文字與信心分數。

> **效能說明**：若批次非常龐大（上千張圖片），建議將清單切成較小的區塊（例如 200 檔）以避免記憶體過度使用。

---

## 步驟 4：顯示擷取文字的預覽 – 快速驗證

批次完成後，先看每個結果的前幾個字元很有幫助。這能讓你確認 OCR 是否真的從 JPEG 檔案中抽出文字。

```python
for image_path, ocr_result in zip(image_paths, ocr_results):
    # Show the image name and the first 100 characters of its recognised text
    preview = ocr_result.text[:100].replace("\n", " ").strip()
    print(f"{image_path.name}: {preview}...")
```

*為什麼這很重要*：簡短的預覽讓你在不開每個檔案的情況下，快速發現明顯失敗（例如空白輸出、亂碼）。若發現系統性問題，可調整引擎設定後重新執行批次。

> **常見陷阱**：忘記去除換行字元會讓預覽變得雜亂。`replace("\n", " ")` 這行程式碼會把換行換成空格。

---

## 完整範例 – 結合所有步驟

以下是可直接複製貼上的完整腳本，只要調整資料夾路徑後執行，即可示範 **如何批次 OCR 圖片** 的全流程。

```python
import ocr
import pathlib

def batch_ocr_jpeg(folder: str):
    """
    Process all JPEG files in `folder` and print a 100‑character preview
    of the recognised text for each image.
    """
    # Step 1 – Initialise OCR engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # Step 2 – Gather JPEG paths
    img_dir = pathlib.Path(folder)
    jpeg_paths = list(img_dir.glob("*.jpg"))  # add more patterns if needed

    if not jpeg_paths:
        print("No JPEG files found in the specified directory.")
        return

    # Step 3 – Batch process
    results = engine.process_batch(jpeg_paths)

    # Step 4 – Display previews
    for path, res in zip(jpeg_paths, results):
        preview = res.text[:100].replace("\n", " ").strip()
        print(f"{path.name}: {preview}...")

if __name__ == "__main__":
    # Replace with the path containing your JPEG images
    batch_ocr_jpeg("YOUR_DIRECTORY/")
```

**預期輸出**（範例）：

```
invoice_001.jpg: Invoice #001  Date: 2024-03-15  Total: $1,245.00  Bill To: Acme Corp...
receipt_202.jpg: Receipt 202  Store: QuickMart  Total: $45.67  Date: 03/12/2024...
...
```

如果預覽顯示有意義的文字，代表你已成功使用批次方式 **從 JPEG 檔案擷取文字**。

---

## 處理大型批次與進階情境

### 將大量工作分塊
面對上千張圖片時，記憶體可能成為瓶頸。可將清單切成較小的區塊：

```python
from itertools import islice

def chunked(iterable, size):
    it = iter(iterable)
    while True:
        chunk = list(islice(it, size))
        if not chunk:
            break
        yield chunk

for chunk in chunked(jpeg_paths, 200):  # 200 files per batch
    results = engine.process_batch(chunk)
    # process results as shown earlier
```

### 切換語言
若文件包含法文或西班牙文，請在批次前變更語言設定：

```python
engine.language = ocr.Language.FRENCH  # or ocr.Language.SPANISH
```

### 將結果寫入磁碟
如果不想只印出結果，可以把每筆 OCR 結果寫成 `.txt` 檔案：

```python
output_dir = pathlib.Path("ocr_output")
output_dir.mkdir(exist_ok=True)

for path, res in zip(jpeg_paths, results):
    txt_path = output_dir / f"{path.stem}.txt"
    txt_path.write_text(res.text, encoding="utf-8")
```

---

## 結論

現在你已掌握 **如何批次 OCR 圖片**，並能可靠地 **從 JPEG 檔案擷取文字**，只需一個簡潔的 Python 腳本。透過一次初始化引擎、收集所有 JPEG 路徑、一次批次處理、以及預覽輸出，你即可同時兼顧速度與簡易性。接下來，你可以擴充工作流程——加入多語言支援、將結果儲存至資料庫，或將腳本整合到更大的文件處理管線。

準備好進一步挑戰了嗎？試著把 `ocr` 套件換成 Tesseract，實驗不同的影像前處理（二值化、縮放），或把擷取的文字送入自然語言處理模型進行自動分類。可能性無限，而你已擁有堅實的基礎。

祝程式開發順利，願你的 OCR 批次永遠無錯誤！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}