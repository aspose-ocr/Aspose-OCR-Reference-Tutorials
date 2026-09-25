---
category: general
date: 2026-01-02
description: 學習如何校正影像傾斜並提升影像對比度，以快速取得純文字。包括逐步的 Python 程式碼以及提取文字的技巧。
draft: false
keywords:
- how to deskew image
- boost image contrast
- get plain text
- how to boost contrast
- how to extract text
language: zh-hant
og_description: 如何校正圖像傾斜並提升對比度以獲取純文字。完整的 Python 範例，包含表格提取與 GPU 加速。
og_title: 如何校正圖像 – 完整 GPU OCR 教學
tags:
- OCR
- Python
- Image Processing
title: 如何校正圖像傾斜 – GPU 加速 OCR 指南
url: /zh-hant/python-java/general/how-to-deskew-image-gpu-accelerated-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何校正圖像 – GPU 加速 OCR 指南

有沒有想過 **how to deskew image**，當你的收據以奇怪的角度拍攝時？你並不孤單；傾斜的照片會把本來清晰可讀的收據變成一團亂碼。好消息是，只要幾行 Python 程式碼，你就能自動校正、提升對比度，並提取乾淨的純文字——不需要手動使用 Photoshop。  

在本教學中，我們將逐步說明一個完整且可執行的範例，除了 **how to deskew image**，還示範 **how to boost contrast**、**get plain text**，甚至 **how to extract text** 從 OCR 引擎偵測到的表格中。完成後，你將擁有一個可直接放入任何專案的獨立腳本。

## 你需要的條件

- 已安裝 Python 3.9+（程式碼使用型別提示，較新版的直譯器較佳）
- `ocr` 函式庫，提供 `OcrEngine`、`EngineMode`、`ImageProcessingOptions` 與 `OcrResult`（透過 `pip install ocr‑sdk` 安裝——請以實際使用的套件名稱取代）
- 具備相容驅動程式的 GPU（若想提升速度，可選擇使用，非必須但建議）
- 一張略為旋轉或低對比度的影像檔，例如 `receipt_skewed.jpg`

> **專業提示：** 若沒有 GPU，只需將 `EngineMode.GPU` 改為 `EngineMode.CPU`，腳本仍能運作——只是稍慢一些。

## 步驟實作說明

以下我們將解決方案分成多個邏輯區塊。每個區塊都有描述性的 **H2**，其中包含主要關鍵字 *how to deskew image* 或次要關鍵字。程式碼完整、附有註解，且可直接執行。

### 使用 GPU 加速 OCR 進行圖像校正

我們首先告訴 OCR 引擎使用 GPU 執行，並啟用自動校正功能。Auto‑deskew 會分析影像的幾何形狀，將其旋轉回正立。

```python
# Import the required classes from the OCR SDK
from ocr import OcrEngine, EngineMode, ImageProcessingOptions, OcrResult

# Step 1: Initialize the OCR engine with GPU acceleration
ocr_engine = OcrEngine()
ocr_engine.set_engine_mode(EngineMode.GPU)  # Enables GPU backend for faster processing
```

> **為何重要：** GPU 加速可將處理時間從秒級縮減至毫秒級，對於每分鐘處理數十張收據的情況至關重要。

### 提升影像對比度以改善辨識

低對比度的收據對任何 OCR 系統而言都是噩夢。提升對比度可讓引擎獲得更清晰的邊緣資訊。

```python
# Step 2: Configure image preprocessing (auto‑deskew and contrast boost)
processing_options = ImageProcessingOptions()
processing_options.set_auto_deskew(True)          # Corrects slight rotation
processing_options.set_contrast_boost(30)         # Improves readability
ocr_engine.set_image_processing_options(processing_options)
```

> **如何提升對比度：** `set_contrast_boost` 方法接受百分比參數；30 % 為大多數掃描收據的安全預設值。若影像特別暗，可提升至 50 % 或自行嘗試。

### 從處理後的影像取得純文字

現在影像已校正且亮度提升，我們將其送入引擎，請求取得純文字結果。

```python
# Step 3: Load the target image and perform OCR
image_path = "YOUR_DIRECTORY/receipt_skewed.jpg"
ocr_result: OcrResult = ocr_engine.recognize_image(image_path)

# Step 4: Output the recognized plain text
print("Detected text:")
print(ocr_result.get_text())
```

**預期輸出**（為簡潔起見已截斷）：

```
Detected text:
Store: Coffee Corner
Date: 2025-12-31
Item          Qty   Price
Latte          1    $3.50
Muffin         2    $5.00
Total                $8.50
```

> **如何取得純文字：** `get_text()` 方法會去除所有版面資訊，回傳乾淨的字串，你可以將其儲存於資料庫、傳送至 API，或供下游分析使用。

### 從偵測到的表格中提取文字

收據常包含表格資料（項目、數量、價格）。OCR SDK 能偵測表格，並允許你遍歷列與儲存格。

```python
# Step 5: If tables are detected, print their contents
if ocr_result.get_tables():
    for idx, table in enumerate(ocr_result.get_tables()):
        print(f"\nTable {idx + 1}:")
        for row in table.get_rows():
            # Join each cell's text with a tab for easy copy‑paste
            print("\t".join(cell.get_text() for cell in row.get_cells()))
```

**範例表格輸出**：

```
Table 1:
Item	Qty	Price
Latte	1	$3.50
Muffin	2	$5.00
Total		$8.50
```

> **為何提取表格：** 結構化資料可輕鬆計算總額、產生報表，或匯入會計軟體。

### 完整可執行腳本

將所有步驟整合後，以下是可直接複製貼上至 `deskew_and_ocr.py` 的腳本：

```python
# deskew_and_ocr.py
from ocr import OcrEngine, EngineMode, ImageProcessingOptions, OcrResult

def main(image_path: str) -> None:
    # Initialize OCR engine with GPU acceleration
    ocr_engine = OcrEngine()
    ocr_engine.set_engine_mode(EngineMode.GPU)

    # Configure preprocessing: auto‑deskew + contrast boost
    opts = ImageProcessingOptions()
    opts.set_auto_deskew(True)
    opts.set_contrast_boost(30)  # Adjust if needed
    ocr_engine.set_image_processing_options(opts)

    # Perform OCR
    result: OcrResult = ocr_engine.recognize_image(image_path)

    # Print plain text
    print("Detected text:")
    print(result.get_text())

    # Print tables, if any
    if result.get_tables():
        for i, tbl in enumerate(result.get_tables(), start=1):
            print(f"\nTable {i}:")
            for row in tbl.get_rows():
                print("\t".join(cell.get_text() for cell in row.get_cells()))

if __name__ == "__main__":
    # Replace with your actual image location
    main("YOUR_DIRECTORY/receipt_skewed.jpg")
```

執行方式：

```bash
python deskew_and_ocr.py
```

你應該會在主控台看到已清理的文字以及任何偵測到的表格。

## 常見邊緣情況與處理方式

| 情況 | 處理方式 |
|-----------|------------|
| **影像倒置** | 若 SDK 支援，可同時呼叫 `set_rotation_correction(True)` 以提升 `set_auto_deskew(True)` 的信心。 |
| **對比度提升使影像過亮** | 降低傳入 `set_contrast_boost` 的百分比（例如 15 %）。 |
| **GPU 不可用** | 將 `EngineMode.GPU` 改為 `EngineMode.CPU`；其餘流程保持不變。 |
| **表格被遺漏** | 嘗試更高解析度的掃描，或若函式庫提供，啟用 `set_table_detection(True)`。 |

## 往後步驟：從純文字到結構化資料

既然你已了解 **how to deskew image**、**how to boost contrast** 與 **how to get plain text**，接下來可能想要：

- 使用正規表達式解析純文字，以抽取鍵值對（例如 `total`、`date`）。
- 將結果儲存於 SQLite 或 PostgreSQL 資料庫，以供日後報表使用。
- 將腳本掛接至無伺服器函式（如 AWS Lambda、Azure Functions），自動處理上傳的檔案。

上述所有延伸功能皆基於本教學所介紹的基礎。

## 結論

我們已說明如何使用 GPU 加速的 OCR 引擎 **how to deskew image**，示範 **how to boost contrast** 以提升辨識清晰度，精確展示 **how to get plain text**，甚至說明 **how to extract text** 從表格中提取。完整且可執行的腳本將所有步驟串接起來，讓你能直接放入任何 Python 專案，立即從傾斜、低對比度的照片中擷取乾淨的資料。

試著使用自己的幾張收據執行，調整對比度參數，讓 OCR 為你完成繁重的工作。若遇到異常，請回顧上方的邊緣情況表格——大多數問題只需要微調即可解決。

祝編程愉快，願你的影像永遠保持正立且明亮！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}