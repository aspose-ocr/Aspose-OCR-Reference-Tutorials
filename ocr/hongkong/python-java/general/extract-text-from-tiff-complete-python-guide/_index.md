---
category: general
date: 2026-06-16
description: 使用 Python OCR 從 TIFF 檔案提取文字。一步一步學習如何將 TIFF 轉換為文字，輕鬆處理多頁文件。
draft: false
keywords:
- extract text from tiff
- convert tiff to text
- Python OCR multi‑page TIFF
- OCR language settings
- OCR engine Python
language: zh-hant
og_description: 使用 Python OCR 從 TIFF 檔案提取文字。遵循本指南將 TIFF 轉換為文字，處理多頁掃描，並獲得乾淨的結果。
og_title: 從 TIFF 提取文字 – 完整 Python 指南
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Extract text from TIFF files using Python OCR. Learn how to convert
    TIFF to text step‑by‑step, handling multi‑page documents with ease.
  headline: Extract Text from TIFF – Complete Python Guide
  type: TechArticle
- description: Extract text from TIFF files using Python OCR. Learn how to convert
    TIFF to text step‑by‑step, handling multi‑page documents with ease.
  name: Extract Text from TIFF – Complete Python Guide
  steps:
  - name: '**Batch conversion** – Wrap the whole flow in a function `def ocr_tiff(path):`
      and iterate over a directory of TIFF files.'
    text: '**Batch conversion** – Wrap the whole flow in a function `def ocr_tiff(path):`
      and iterate over a directory of TIFF files.'
  - name: '**Output to files** – Instead of printing, write each page’s text to `page_{i}.txt`
      or concatenate everything into a single document.'
    text: '**Output to files** – Instead of printing, write each page’s text to `page_{i}.txt`
      or concatenate everything into a single document.'
  - name: '**Alternative OCR engines** – If you need higher accuracy, swap `ocr.OcrEngine()`
      for Tesseract (`pytesseract`) or Azure Cognitive Services—just keep the same
      “extract text from TIFF” logic.'
    text: '**Alternative OCR engines** – If you need higher accuracy, swap `ocr.OcrEngine()`
      for Tesseract (`pytesseract`) or Azure Cognitive Services—just keep the same
      “extract text from TIFF” logic.'
  - name: '**Post‑processing** – Run spell‑check, language detection, or regex cleanup
      to tidy up the raw OCR output.'
    text: '**Post‑processing** – Run spell‑check, language detection, or regex cleanup
      to tidy up the raw OCR output.'
  type: HowTo
tags:
- OCR
- Python
- TIFF
- Text extraction
title: 從 TIFF 提取文字 – 完整 Python 指南
url: /zh-hant/python-java/general/extract-text-from-tiff-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從 TIFF 提取文字 – 完整 Python 指南

有沒有需要 **從 TIFF 提取文字** 卻不知從何下手？你並不孤單——許多開發者在處理掃描檔案或舊有文件時都會卡在這裡。好消息是，只要幾行 Python 程式碼，就能 **將 TIFF 轉換為文字**，即使檔案包含數十頁也不在話下。

在本教學中，我們將示範一個實務案例：載入多頁 TIFF、將 OCR 語言設定為法文，並從每一頁中抽取辨識出的文字。完成後，你將擁有一個可直接執行的腳本，了解每一步的意義，並知道如何為其他語言或影像格式做調整。

## 前置條件

在開始之前，請確保你已具備：

- 已安裝 Python 3.8 或更新版本。
- `ocr` 套件（或任何提供 `OcrEngine` 類別的相容 OCR 函式庫）。可使用 `pip install ocr-lib` 安裝——請以實際使用的套件名稱取代。
- 一個多頁 TIFF 檔案（例如 `french-scans.tif`）供你處理。
- 基本的 Python 腳本撰寫經驗。

不需要額外的重型依賴，也不需要外部服務——純粹使用 Python 與 OCR 引擎即可。

---

## 步驟 1：設定 OCR 引擎以 **從 TIFF 提取文字**

首先，我們需要建立 OCR 引擎實例，並告訴它要使用哪種語言。此處的原始資料是法文，所以要相應設定語言。

```python
import ocr  # Replace with the actual import if your OCR library uses a different name

# Create the OCR engine
engine = ocr.OcrEngine()

# Tell the engine to look for French characters
engine.language = ocr.Language.FRENCH
```

**為什麼這很重要：**  
語言設定會大幅提升辨識準確度。像 “é” 或 “ç” 這類法文字符，若引擎預設為英語，會被誤讀成通用符號。明確選擇法文即可提供正確的字元對照表。

> **小技巧：** 若要同時處理多種語言的文件，可在每次呼叫 `recognize()` 前動態變更 `engine.language`。

---

## 步驟 2：載入要 **將 TIFF 轉換為文字** 的多頁 TIFF

TIFF 可以包含多個影格——把每個影格想像成一頁。OCR 函式庫已為我們抽象化這個概念，只要指向檔案即可。

```python
# Path to your multi‑page TIFF
tiff_path = "YOUR_DIRECTORY/french-scans.tif"

# Load the file; the engine now knows how many pages it contains
engine.load_from_file(tiff_path)
```

**邊緣案例提醒：**  
若檔案路徑錯誤或 TIFF 已損毀，`load_from_file` 方法會拋出例外。正式環境建議以 `try/except` 包住：

```python
try:
    engine.load_from_file(tiff_path)
except Exception as e:
    print(f"Failed to load TIFF: {e}")
    raise
```

---

## 步驟 3：對整份文件執行 OCR – **從 TIFF 提取文字** 的核心

現在讓引擎發揮魔法。`recognize()` 會一次處理所有頁面，並回傳一個豐富的結果物件。

```python
# Perform OCR on all pages at once
multi_result = engine.recognize()
```

**底層發生了什麼？**  
引擎會遍歷每個影格，執行前處理（去斜、二值化），然後跑神經網路，最後彙總輸出。因為只呼叫一次 `recognize()`，函式庫能在頁面之間共享資源，速度比手動逐頁迴圈更快。

---

## 步驟 4：從 JSON 結果中抽取辨識文字 – **將 TIFF 轉換為文字**（逐頁）

結果物件可序列化為 JSON。於 JSON 中會看到 `pages` 陣列，每個元素都有 `text` 欄位。

```python
# Convert the result to a Python dict (JSON-like)
result_dict = multi_result.to_json()

# Extract the list of pages
pages = result_dict["pages"]
```

現在我們得到一個乾淨的 Python list，裡面的每個元素對應到一頁的 OCR 輸出。

---

## 步驟 5：列印或儲存每頁文字 – 完成 **從 TIFF 提取文字** 的最後一步

讓我們遍歷各頁並顯示抽出的文字。若需要，也可以把每頁寫入單獨的 `.txt` 檔案。

```python
for i, page in enumerate(pages, start=1):
    print(f"--- Page {i} ---")
    print(page["text"])
    print()  # Blank line for readability
```

### 預期輸出（範例）

```
--- Page 1 ---
Bonjour, ceci est un exemple de texte extrait d'une image TIFF.

--- Page 2 ---
Le deuxième page contient davantage d'informations en français.
```

如果 OCR 成功，你會看到每頁都有整齊的法文句子。若出現亂碼，請再次確認語言設定，或考慮在 OCR 前提升影像解析度。

---

## 處理常見問題 – **將 TIFF 轉換為文字** 時的注意事項

| 問題 | 為何會發生 | 快速解決方案 |
|------|------------|--------------|
| **`pages` 陣列為空** | TIFF 未正確載入或沒有影格。 | 檢查檔案路徑，確保 TIFF 不是偽裝成 TIFF 的單頁 PNG。 |
| **出現雜訊字元** | 語言不符或影像品質太低。 | 設定正確的 `engine.language`，並在 OCR 前做前處理（如提升 DPI）。 |
| **大型 TIFF 記憶體暴增** | 一次載入所有頁面會佔用大量 RAM。 | 分批處理：載入單一影格、辨識、釋放後再載入下一頁。 |
| **列印時出現 Unicode 錯誤** | 主控台編碼不支援帶重音的字元。 | 使用 `print(page["text"].encode('utf-8').decode('utf-8'))`，或將終端機設定為 UTF‑8。 |

---

## 擴充腳本：從 **從 TIFF 提取文字** 到批次處理

有了穩固的基礎後，你可以考慮以下進階步驟：

1. **批次轉換** – 將整個流程封裝成 `def ocr_tiff(path):`，再對資料夾內的所有 TIFF 檔案迭代執行。
2. **輸出為檔案** – 改為寫入 `page_{i}.txt`，或把所有頁面合併成單一文件。
3. **替換 OCR 引擎** – 若需要更高精度，可將 `ocr.OcrEngine()` 換成 Tesseract (`pytesseract`) 或 Azure Cognitive Services——只要保留「從 TIFF 提取文字」的邏輯即可。
4. **後處理** – 加入拼寫檢查、語言偵測或正規表達式清理，讓原始 OCR 輸出更整潔。

---

## 完整、可直接執行的腳本

以下提供完整程式碼，直接複製貼上即可使用。內含基本錯誤處理，並可選擇將每頁文字儲存為獨立檔案。

```python
import ocr  # Adjust import based on your OCR library
import os

def extract_text_from_tiff(tiff_path: str, output_dir: str = None) -> list:
    """
    Loads a multi‑page TIFF, runs OCR, and returns a list of strings,
    one per page. Optionally saves each page to a .txt file.
    """
    # Initialize engine and set language
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.FRENCH

    # Load the TIFF file
    try:
        engine.load_from_file(tiff_path)
    except Exception as e:
        raise RuntimeError(f"Unable to load {tiff_path}: {e}")

    # Run OCR on all pages
    multi_result = engine.recognize()

    # Parse JSON result
    pages = multi_result.to_json()["pages"]
    texts = [page["text"] for page in pages]

    # If an output directory is provided, write each page to a file
    if output_dir:
        os.makedirs(output_dir, exist_ok=True)
        for i, text in enumerate(texts, start=1):
            file_path = os.path.join(output_dir, f"page_{i}.txt")
            with open(file_path, "w", encoding="utf-8") as f:
                f.write(text)

    return texts

if __name__ == "__main__":
    # Example usage – replace with your actual TIFF path
    tiff_file = "YOUR_DIRECTORY/french-scans.tif"
    # Optional: where to store per‑page text files
    out_folder = "extracted_pages"

    page_texts = extract_text_from_tiff(tiff_file, out_folder)

    for i, txt in enumerate(page_texts, start=1):
        print(f"--- Page {i} ---")
        print(txt)
        print()
```

執行此腳本，將 `tiff_file` 指向你的文件，觀察主控台輸出整潔的法文句子。若提供了 `out_folder`，還會在該資料夾內產生一系列 `page_#.txt` 檔案，供後續處理使用。

---

## 結論

我們剛剛使用簡單的 Python OCR 工作流程 **從 TIFF 提取文字**，並學會如何可靠地 **將 TIFF 轉換為文字**。從以正確語言初始化引擎，到遍歷每頁的 JSON 結果，每一步都說明了背後的「為什麼」，讓你能將此模式套用到其他語言、影像格式或更大規模的批次作業。

接下來可以嘗試換用 Tesseract、實驗不同的語言套件，或將輸出整合至可搜尋的資料庫。只要能穩定將掃描圖像轉成可搜尋文字，未來的可能性就無限。

如果在實作過程中遇到問題或有改進想法，歡迎留下評論。祝開發順利！

## 接下來該學什麼？

以下教學與本指南緊密相關，能幫助你進一步掌握 API 功能，並探索其他實作方式：

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}