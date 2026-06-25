---
category: general
date: 2026-06-25
description: 使用 Python aocr 函式庫從圖像中提取文字 – 學習批次 OCR、設定辨識模式為印刷體，並加入 AI 後處理。
draft: false
keywords:
- extract text from images
- Python OCR batch
- aocr library
- recognition mode printed
- AI postprocessor
language: zh-hant
og_description: 使用 Python aocr 函式庫從圖像中提取文字。本教學展示批次 OCR、印刷文字辨識模式，以及可選的 AI 後處理器。
og_title: 使用 Python 從圖像提取文字 – 完整的 aocr 批次指南
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Extract text from images with Python aocr library – learn batch OCR,
    set recognition mode printed, and add an AI postprocessor.
  headline: Extract Text from Images in Python Using aocr OCR Batch
  type: TechArticle
- description: Extract text from images with Python aocr library – learn batch OCR,
    set recognition mode printed, and add an AI postprocessor.
  name: Extract Text from Images in Python Using aocr OCR Batch
  steps:
  - name: Prerequisites
    text: '- Python 3.8 or newer installed on your machine. - Basic familiarity with
      Python scripting (loops, imports, etc.). - Access to a folder of scanned images
      (PNG, JPG, TIFF, etc.).'
  - name: 1. Unsupported File Types
    text: '`aocr` silently skips files it can’t decode. If you suspect you have PDFs
      or BMPs mixed in, filter them beforehand:'
  - name: 2. Large Batches and Memory Consumption
    text: 'Running thousands of high‑resolution scans can balloon memory usage. Mitigate
      this by processing in chunks:'
  - name: 3. Empty or Low‑Contrast Pages
    text: 'If a page yields fewer than 10 characters, you might want to flag it for
      manual review:'
  type: HowTo
- questions:
  - answer: Not out‑of‑the‑box. `aocr` only handles raster images. Convert PDFs to
      PNG/TIFF first (e.g., using `pdf2image`).
    question: Does this work on PDFs?
  - answer: Absolutely—just replace `aocr.RecognitionMode.PRINTED` with `aocr.RecognitionMode.HANDWRITTEN`.
      Expect a slower run time but better results on cursive notes.
    question: Can I change the recognition mode to handwritten?
  - answer: 'The library ships with language packs. Install the desired language module
      (`pip install aocr-lang-fr` for French, etc.) and set `ocr_batch.language =
      "fr"` before running. ## Next Steps and Related Topics - **Parallel processing:**
      Wrap the batch execution in a `concurrent.futures.ThreadPoolExecuto'
    question: What if I need multilingual support?
  type: FAQPage
tags:
- OCR
- Python
- image processing
title: 使用 aocr OCR 批次在 Python 中從圖像提取文字
url: /zh-hant/python/general/extract-text-from-images-in-python-using-aocr-ocr-batch/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 aocr OCR 批次在 Python 中從圖像提取文字

是否曾需要**從圖像中提取文字**，卻被數十個繁瑣步驟搞得不知所措？你並不孤單。無論是將掃描表格數位化、從收據中提取資料，或是建立可搜尋的檔案庫，在大規模取得可靠的 OCR 結果都可能像爬陡坡般艱難。

好消息是？使用 **aocr library**，只需幾行程式碼就能建立完整的 **Python OCR batch**。在本指南中，我們將逐步說明如何建立 OCR batch、從資料夾載入所有支援的圖像、選擇正確的 **recognition mode printed**，甚至附加 **AI postprocessor** 以提升準確度。完成後，你將擁有一個可直接執行的腳本，能從圖像提取文字，並告訴你每個檔案提取了多少文字。

## 你將學會

- 如何安裝並匯入 `aocr` 套件。
- 設定 `OcrBatch` 以自動處理成千上萬的檔案。
- 為印刷文件選擇最佳的辨識模式。
- （可選）掛接 AI 後處理器以清理雜訊結果。
- 顯示每個檔案路徑及其提取文字的長度。
- 處理不支援格式或空白頁面等邊緣案例的技巧。

### 前置條件

- 在機器上已安裝 Python 3.8 或更新版本。  
- 具備基本的 Python 腳本知識（迴圈、匯入等）。  
- 擁有包含掃描圖像的資料夾（PNG、JPG、TIFF 等）。  

如果你已具備上述條件，讓我們開始吧——不需要任何外部服務。

## 步驟 1：安裝 aocr 套件

首先，`aocr` 套件並非標準庫的一部份，需要從 PyPI 下載。

```bash
pip install aocr
```

> **小技巧：** 使用虛擬環境（`python -m venv .venv`）以保持相依性隔離。  

安裝完成後，即可匯入核心類別。

```python
# core imports
import aocr
```

## 步驟 2：建立 OCR Batch 實例

`OcrBatch` 是負責遍歷目錄並追蹤每個圖像檔案的核心。可以把它想像成將圖片送入 OCR 引擎的傳送帶。

```python
# Step 2: Initialize the batch
ocr_batch = aocr.OcrBatch()
```

此時 batch 為空，但我們會在下一步填入檔案。

## 步驟 3：從資料夾（遞迴）加入所有支援的圖像

你可能有多層資料夾結構——例如每位客戶或每個月份都有子資料夾。`add_folder` 方法會為你遍歷整個樹狀結構，載入所有可讀取的圖像。

```python
# Step 3: Load images from a directory
ocr_batch.add_folder("YOUR_DIRECTORY/scanned_forms/", recursive=True)
```

將 `"YOUR_DIRECTORY/scanned_forms/"` 替換為系統中的實際路徑。此呼叫之後，`ocr_batch.file_paths` 會保存絕對檔名列表，且 batch 知道將要處理的項目數量。

## 步驟 4：為印刷文字選擇辨識模式

`aocr` 引擎支援多種模式（手寫、印刷、混合）。因為我們處理的是乾淨的印刷表單，請相應設定模式。這個小旗標能顯著提升準確度，因為引擎會跳過手寫文字所需的繁重啟發式判斷。

```python
# Step 4: Tell the engine we have printed text
ocr_batch.recognition_mode = aocr.RecognitionMode.PRINTED
```

> **為什麼重要：** 印刷文字的基線與字形一致，使 OCR 模型能使用更嚴謹的字典。若將模式保留為 “auto”，在低解析度掃描時可能會產生額外雜訊。

## 步驟 5：（可選）附加 AI 後處理器

如果掃描件有模糊、低對比或特殊字體等問題，AI 後處理器可以在將原始 OCR 輸出交給下游系統前進行清理。`set_ai_postprocessor` 方法需要一個實作 `process(text: str) -> str` 介面的物件。

以下是一個使用虛構 `SimpleCleaner` 類別的最小範例。實務上，你可以接入 HuggingFace 轉換模型、自訂語言模型，甚至基於規則的拼寫檢查器。

```python
# Optional Step 5: Define a tiny post‑processor
class SimpleCleaner:
    def process(self, text: str) -> str:
        # Strip extra whitespace and fix common OCR quirks
        cleaned = " ".join(text.split())
        return cleaned.replace("—", "-")  # replace em‑dash with hyphen

# Instantiate and attach
ai = SimpleCleaner()
ocr_batch.set_ai_postprocessor(ai)
```

若跳過此步驟，batch 只會回傳原始 OCR 字串。

## 步驟 6：對整個 Batch 執行 OCR 並收集結果

現在開始繁重的工作。`run` 方法會遍歷每個檔案，執行 OCR 引擎，將輸出傳遞給可選的 AI 後處理器，最後回傳字串列表——每張圖像一個。

```python
# Step 6: Execute the batch
ocr_results = ocr_batch.run()   # list of extracted texts
```

由於該方法回傳的是普通的 Python list，你可以像處理其他集合一樣使用——儲存、寫入 CSV，或寫入資料庫。

## 步驟 7：顯示每個檔案路徑及其提取文字的長度

快速的健全性檢查是印出每個檔案提取了多少字元。若頁面為空或 OCR 失敗，長度會顯示為 `0`。

```python
# Step 7: Show results summary
for file_path, text in zip(ocr_batch.file_paths, ocr_results):
    print(f"{file_path} -> {len(text)} chars")
```

典型的輸出如下：

```
/data/forms/invoice_001.png -> 1245 chars
/data/forms/invoice_002.jpg -> 0 chars
/data/forms/receipt_2023-04-15.tif -> 876 chars
```

看到 `0` 旗標即表示該檔案需要再次檢查（可能已損毀或根本不是圖像）。

## 處理常見邊緣案例

### 1. 不支援的檔案類型

`aocr` 會靜默跳過無法解碼的檔案。若懷疑資料夾中混有 PDF 或 BMP，請事先過濾。

```python
supported_ext = {".png", ".jpg", ".jpeg", ".tif", ".tiff"}
ocr_batch.file_paths = [
    p for p in ocr_batch.file_paths if p.lower().endswith(tuple(supported_ext))
]
```

### 2. 大批次與記憶體消耗

處理數千張高解析度掃描時，記憶體使用量會激增。可透過分批處理來緩解。

```python
batch_size = 200
for i in range(0, len(ocr_batch.file_paths), batch_size):
    sub_batch = aocr.OcrBatch()
    sub_batch.file_paths = ocr_batch.file_paths[i:i+batch_size]
    sub_batch.recognition_mode = aocr.RecognitionMode.PRINTED
    if 'ai' in locals():
        sub_batch.set_ai_postprocessor(ai)
    results = sub_batch.run()
    # handle results (e.g., write to file) before next chunk
```

### 3. 空白或低對比頁面

若頁面產生的字元少於 10 個，建議將其標記為需人工檢查。

```python
for fp, txt in zip(ocr_batch.file_paths, ocr_results):
    if len(txt.strip()) < 10:
        print(f"⚠️  Low‑confidence result for {fp}")
```

## 完整範例

將上述步驟整合，以下是一個可直接複製貼上並執行的腳本。請儲存為 `batch_ocr.py`。

```python
#!/usr/bin/env python3
"""
Batch OCR script using aocr to extract text from images.
"""

import aocr

# ----------------------------------------------------------------------
# Optional: a tiny AI post‑processor to clean up OCR output
# ----------------------------------------------------------------------
class SimpleCleaner:
    def process(self, text: str) -> str:
        cleaned = " ".join(text.split())
        return cleaned.replace("—", "-")

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
IMAGE_ROOT = "YOUR_DIRECTORY/scanned_forms/"   # ← change this!
RECOGNITION_MODE = aocr.RecognitionMode.PRINTED

# ----------------------------------------------------------------------
# Build and run the OCR batch
# ----------------------------------------------------------------------
def main():
    # 1️⃣ Create batch
    batch = aocr.OcrBatch()

    # 2️⃣ Load images recursively
    batch.add_folder(IMAGE_ROOT, recursive=True)

    # 3️⃣ Set mode for printed text
    batch.recognition_mode = RECOGNITION_MODE

    # 4️⃣ Attach AI post‑processor (comment out if not needed)
    ai = SimpleCleaner()
    batch.set_ai_postprocessor(ai)

    # 5️⃣ Run OCR
    results = batch.run()

    # 6️⃣ Summarize
    for path, text in zip(batch.file_paths, results):
        print(f"{path} -> {len(text)} chars")

if __name__ == "__main__":
    main()
```

**預期輸出**（為簡潔起見已截斷）：

```
/home/me/scanned_forms/formA.png -> 1342 chars
/home/me/scanned_forms/subfolder/formB.tif -> 0 chars
/home/me/scanned_forms/invoice_2024-01.jpg -> 987 chars
```

使用以下指令執行：

```bash
python batch_ocr.py
```

若一切設定正確，將會看到每張圖像的輸出行，並顯示提取文字的字元數。

## 常見問題

**Q: 這能用於 PDF 嗎？**  
A: 不是即插即用。`aocr` 只處理點陣圖像。請先將 PDF 轉為 PNG/TIFF（例如使用 `pdf2image`）。

**Q: 我可以將辨識模式改為手寫嗎？**  
A: 當然可以——只需將 `aocr.RecognitionMode.PRINTED` 換成 `aocr.RecognitionMode.HANDWRITTEN`。執行時間會較慢，但對手寫筆記的結果會更好。

**Q: 如果需要多語言支援該怎麼辦？**  
A: 此函式庫附帶語言套件。安裝所需語言模組（例如法語 `pip install aocr-lang-fr`），並在執行前設定 `ocr_batch.language = "fr"`。

## 後續步驟與相關主題

- **平行處理：** 使用 `concurrent.futures.ThreadPoolExecutor` 包裹 batch 執行，以利用多核心 CPU。  
- **儲存結果：** 將 `ocr_results` 寫入 CSV 或 SQLite 資料庫，以供下游分析。  
- **整合雲端 AI：** 將 `SimpleCleaner` 換成 HuggingFace 的 transformer 模型，以取得最先進的拼寫校正。  
- **微調 aocr：** 若有自訂字型集，可探索 `aocr.Trainer` 以提升印刷模式的準確度。

---

就這樣——你現在已擁有一個穩固的

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，建立於此處示範的技巧之上。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在自己的專案中探索替代實作方式。

- [使用 Aspose OCR 從圖像提取文字 – 步驟指南](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [使用 OCR 操作於資料夾提取圖像文字](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [在 Aspose.OCR for .NET 中使用 List 批次 OCR 圖像](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}