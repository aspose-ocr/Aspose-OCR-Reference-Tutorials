---
category: general
date: 2026-03-18
description: 學習如何使用 Aspose OCR 在 Python 中從圖片提取文字，並將掃描圖片的文字轉換為可編輯的字串。附有一步一步的程式碼示例。
draft: false
keywords:
- extract text from images
- convert scanned images text
- Aspose OCR Python
- batch OCR processing
- image to text conversion
language: zh-hant
og_description: 使用 Aspose OCR 於 Python 提取圖片文字。本教學示範如何僅用幾行程式碼將掃描圖片的文字轉換。
og_title: 使用 Aspose OCR 從圖片提取文字 – Python 指南
tags:
- OCR
- Python
- Aspose
- Image Processing
title: 使用 Aspose OCR 從圖像中提取文字 – Python 指南
url: /zh-hant/python-java/general/extract-text-from-images-with-aspose-ocr-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從圖像提取文字 – Aspose OCR Python 指南

曾經需要**從圖像提取文字**卻不知從何入手嗎？你並不孤單——開發人員經常面臨將掃描的 PDF、雜訊截圖或拍攝的收據轉換成可搜尋、可編輯字串的困擾。  

好消息是？使用 Aspose OCR for Python，你可以批量**轉換掃描圖像文字**，且全程不離開 IDE。在本教學中，我們將逐步示範一個完整、可直接執行的範例，說明如何操作、每一步的意義，以及需要留意的地方。

## 你將學會

- 在 Python 環境中設定 Aspose OCR 函式庫。  
- 準備圖像檔案清單（PNG、JPG、TIFF 等）。  
- 以單一方法呼叫執行批次 OCR。  
- 取得並顯示每個檔案的提取文字。  
- 處理常見問題，例如不支援的格式與大型檔案的記憶體使用。  

完成後，你將擁有一個可重複使用的腳本，能隨時**從圖像提取文字**——非常適合自動化資料輸入、文件索引，或供給下游 NLP 流程。

---

![使用 Aspose OCR 在 Python 中從圖像提取文字](/images/ocr-extract-text.png "從圖像提取文字")

*圖片說明文字：“使用 Aspose OCR 在 Python 中從圖像提取文字”*

## 前置條件

- Python 3.8 或更新版本（程式碼使用 f‑strings）。  
- 有效的 Aspose OCR for Python 授權或免費試用金鑰。  
- 要處理的圖像已本機儲存（可混合 PNG、JPG 或 TIFF）。  

如果你已經有虛擬環境，太好了——若沒有，請使用以下指令建立：

```bash
python -m venv ocr-env
source ocr-env/bin/activate   # On Windows: ocr-env\Scripts\activate
```

現在你可以安裝 SDK 了。

## 步驟 1：安裝 Aspose OCR SDK

Aspose 透過 PyPI 發佈 OCR 引擎，只需一條 `pip` 指令即可完成安裝：

```bash
pip install aspose-ocr
```

> **專業提示：** 鎖定版本（例如 `aspose-ocr==22.12`）以避免之後出現意外的破壞性變更。

## 步驟 2：匯入 OCR Engine 類別

你將使用的核心類別是 `OcrEngine`。在腳本開頭匯入它：

```python
# Step 2: Import the OCR engine class
from asposeocr import OcrEngine
```

> *為什麼重要：* 只匯入所需的類別可降低啟動時間，尤其在之後將腳本嵌入更大的應用程式時。

## 步驟 3：定義要處理的圖像檔案

建立一個 Python 串列，內含所有要掃描的圖像完整路徑。將 `YOUR_DIRECTORY` 替換為實際的資料夾路徑。

```python
# Step 3: Define the image files to be processed
image_files = [
    "YOUR_DIRECTORY/page1.png",
    "YOUR_DIRECTORY/page2.jpg",
    "YOUR_DIRECTORY/page3.tif"
]
```

> **邊緣情況：** 若檔案數量達數百個，建議使用 `glob.glob('*.png')` 程式化產生清單，以免手動編輯。

## 步驟 4：一次性對所有圖像執行 OCR

Aspose OCR 提供便利的 `processMultiple` 方法，會回傳 `OcrResult` 物件的串列——每個輸入檔案對應一個物件。

```python
# Step 4: Run OCR on all images at once
ocr_engine = OcrEngine()               # instantiate the engine
ocr_results = ocr_engine.processMultiple(image_files)
```

> *為什麼使用批次處理？* 單獨傳送每張圖像會產生額外開銷（初始化引擎、載入原生函式庫）。批次呼叫可減少 CPU 負載，提升整體執行速度。

### 優雅地處理錯誤

若圖像無法讀取（檔案損毀、不支援的格式），`processMultiple` 會拋出例外。將呼叫包在 `try/except` 區塊中，以保持腳本持續執行：

```python
try:
    ocr_results = ocr_engine.processMultiple(image_files)
except Exception as e:
    print(f"⚠️ OCR failed: {e}")
    ocr_results = []   # fallback to empty list
```

## 步驟 5：輸出每個檔案的提取文字

遍歷結果，將每個 `OcrResult` 與其原始檔名配對。`getText()` 方法會回傳辨識出的字串。

```python
# Step 5: Output the extracted text for each file
for index, result in enumerate(ocr_results, start=1):
    file_path = image_files[index - 1]
    print(f"--- Text from file {file_path} ---")
    print(result.getText())
    print("\n")   # add a blank line for readability
```

### 預期輸出

在三張簡單的螢幕截圖上執行完整腳本，可能會得到類似以下的輸出：

```
--- Text from file YOUR_DIRECTORY/page1.png ---
Invoice #12345
Date: 2024‑07‑01
Total: $256.78

--- Text from file YOUR_DIRECTORY/page2.jpg ---
Welcome to the Annual Report
Prepared by: Finance Dept.

--- Text from file YOUR_DIRECTORY/page3.tif ---
© 2025 Acme Corp. All rights reserved.
```

若圖像中沒有可辨識的字元，會顯示空字串——不會導致錯誤，你可以自行決定是否將該檔案標記為需人工檢查。

## 加分項：微調 OCR 準確度

Aspose OCR 提供多項可選設定，你可以自行嘗試：

| 設定 | 功能說明 | 使用時機 |
|---------|--------------|-------------|
| `ocr_engine.setLanguage('eng')` | 強制使用英文語言模型（降低偽陽性）。 | 主要為英文文件。 |
| `ocr_engine.setResolution(300)` | 提升低 DPI 掃描的準確度。 | DPI 低於 200 的掃描。 |
| `ocr_engine.setPageSegMode('single_block')` | 將整張圖像視為單一文字區塊。 | 簡單收據或身分證。 |

可以在建立 `ocr_engine` 後立即加入以下程式碼：

```python
ocr_engine.setLanguage('eng')
ocr_engine.setResolution(300)
ocr_engine.setPageSegMode('single_block')
```

## 常見陷阱與避免方法

1. **大型 TIFF 堆疊** – 多頁 TIFF 若一次全部載入，可能會佔用數 GB 記憶體。請在傳入 `processMultiple` 前，將檔案拆分為單頁圖像。  
2. **非拉丁文字** – 若需**從圖像提取文字**且內容包含西里爾文、阿拉伯文或中文，請相應調整語言代碼（`'rus'`、`'ara'`、`'chi_sim'`）。  
3. **檔案路徑含空格** – Windows 含空格的路徑可能導致 `FileNotFoundError`。請將每個路徑以原始字串包住（`r"C:\My Folder\image.png"`）或使用 `os.path.abspath`。  

提前處理這些問題，可避免日後出現難以理解的執行時錯誤。

---

## 完整範例

以下是完整腳本，你可以直接複製貼上為 `batch_ocr.py` 檔案。它已納入上述所有最佳實踐的調整。

```python
# batch_ocr.py
# -------------------------------------------------
# Complete example: extract text from images using Aspose OCR (Python)
# -------------------------------------------------

from asposeocr import OcrEngine
import os

# -------------------------------------------------
# Configuration – adjust these values for your environment
# -------------------------------------------------
IMAGE_DIR = "YOUR_DIRECTORY"   # <-- replace with your folder path
SUPPORTED_EXT = (".png", ".jpg", ".jpeg", ".tif", ".tiff")

# Build a list of image file paths automatically
image_files = [
    os.path.join(IMAGE_DIR, f)
    for f in os.listdir(IMAGE_DIR)
    if f.lower().endswith(SUPPORTED_EXT)
]

if not image_files:
    print("⚠️ No supported image files found in the specified directory.")
    exit(1)

# -------------------------------------------------
# Initialize OCR engine with optional tweaks
# -------------------------------------------------
ocr_engine = OcrEngine()
ocr_engine.setLanguage('eng')          # English language model
ocr_engine.setResolution(300)          # Boost low‑dpi accuracy
ocr_engine.setPageSegMode('single_block')  # Treat whole image as one block

# -------------------------------------------------
# Run batch OCR and handle potential errors
# -------------------------------------------------
try:
    ocr_results = ocr_engine.processMultiple(image_files)
except Exception as exc:
    print(f"❌ OCR processing failed: {exc}")
    ocr_results = []

# -------------------------------------------------
# Display extracted text
# -------------------------------------------------
for idx, result in enumerate(ocr_results, start=1):
    file_path = image_files[idx - 1]
    print(f"--- Text from file {file_path} ---")
    print(result.getText())
    print("\n")
```

儲存後，啟動你的虛擬環境，執行以下指令：

```bash
python batch_ocr.py
```

你應該會在主控台看到提取的字串，已可進一步處理（例如儲存至資料庫或供給自然語言模型）。

---

## 結論

本指南示範了如何使用 Aspose OCR for Python **從圖像提取文字**，涵蓋從安裝、批次處理到錯誤處理的全部步驟。此腳本簡潔、功能完整且易於擴充——無論你需要將**掃描圖像文字**轉成 CSV 檔、供給搜尋索引，或僅是自動化資料輸入，都能輕鬆應對。

準備好進一步了嗎？可將此 OCR 流程與 PDF 合併工具結合，產生可搜尋的 PDF，或接入雲端儲存觸發器，讓每次上傳的掃描檔即時處理。可能性無限，而你已擁有堅實的基礎可供構建。

有任何問題或改進建議嗎？歡迎在下方留言，祝開發愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}