---
category: general
date: 2026-03-26
description: 使用 Python OCR 從影像中提取表格並將影像轉換為試算表。學習如何載入影像進行 OCR、讀取表格以及提取表格資料。
draft: false
keywords:
- extract tables from image
- convert image to spreadsheet
- load image for ocr
- ocr read tables
- ocr extract table data
language: zh-hant
og_description: 使用 Python OCR 從圖片提取表格。本指南示範如何載入圖片進行 OCR、讀取表格，並將其轉換為試算表。
og_title: 從圖片中提取表格 – 完整 OCR 教學
tags:
- OCR
- Python
- Data Extraction
title: 從圖像提取表格 – 步驟式 OCR 指南
url: /zh-hant/python-java/general/extract-tables-from-image-step-by-step-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從圖像提取表格 – 完整 OCR 教學

曾經需要 **從圖像提取表格** 但不知從何入手嗎？你並不孤單。許多開發者在 PDF 或螢幕截圖中遇到必須轉換成可編輯列與欄的表格資料時會卡住。好消息是？只要幾行 Python 程式碼，加上穩定的 OCR 引擎，就能在數秒內把圖片變成可使用的試算表。

在本教學中，我們將逐步說明如何載入圖像進行 OCR、執行辨識引擎，並逐列抽取每張表格。完成後，你將能 **convert image to spreadsheet**，同時也會了解如何 **ocr read tables** 與 **ocr extract table data** 以供後續處理。沒有隱藏的魔法，只有清晰、可直接執行的程式碼，今天就可以放入你的專案。

---

## 需要的條件

在開始之前，請確保你已具備以下項目：

- **Python 3.9+** – 建議使用最新的穩定版。
- **`ocr`** 套件（或任何提供 `OcrEngine`、`Image` 與表格相關方法的相容 OCR SDK）。使用 `pip install ocr‑sdk` 安裝（請以實際套件名稱取代）。
- 一張包含清晰列印表格的圖像檔（`.png`、`.jpg` 等）。  
- 可選：**pandas**，若你想直接將抽取的資料寫入 CSV 或 Excel 檔案 (`pip install pandas`)。

全部準備好了嗎？太好了——讓我們開始吧。

---

## 步驟 1：匯入 OCR SDK 並設定環境

首先，我們需要把 OCR 類別匯入腳本，並建立一個小幫手，稍後用來將原始表格資料轉換成 DataFrame。

```python
# Step 1 – Imports and basic setup
import ocr                     # The OCR SDK
from pathlib import Path      # Handy for file paths
import pandas as pd           # For converting tables to spreadsheets

# Optional: configure logging to see what the engine is doing
import logging
logging.basicConfig(level=logging.INFO)
```

**為什麼這很重要：** 匯入 `ocr` 後，我們即可使用 `OcrEngine`、`Imaging.Image` 以及將要遍歷的表格物件。`pandas` 並非抽取必需，但它能讓 **convert image to spreadsheet** 的部分變得非常簡單。

---

## 步驟 2：載入要處理的圖像

現在我們實際 **load image for OCR**。SDK 需要一個 `Image` 物件，因此我們會使用輔助方法 `Image.load()` 包裝檔案路徑。

```python
# Step 2 – Load the image that contains a table
image_path = Path("YOUR_DIRECTORY/table_image.png")

# Verify the file exists early to avoid cryptic SDK errors
if not image_path.is_file():
    raise FileNotFoundError(f"Image not found: {image_path}")

# Create an OCR engine instance
ocr_engine = ocr.OcrEngine()

# Attach the image to the engine
ocr_engine.set_image(ocr.Imaging.Image.load(str(image_path)))
```

**小技巧：** 將圖像檔放在專屬資料夾（例如 `assets/` 或 `data/`）並使用相對路徑，這樣腳本在不同機器間搬移時仍能正常執行。

---

## 步驟 3：執行辨識程序

圖像已載入後，我們終於可以指示引擎 **ocr read tables**。`recognize()` 呼叫會回傳一個結果物件，裡面包含引擎偵測到的所有資訊——文字區塊、行列，最重要的是表格。

```python
# Step 3 – Perform OCR and obtain results
ocr_result = ocr_engine.recognize()

# Quick sanity check: did the engine find any tables?
if not ocr_result.get_tables():
    logging.warning("No tables detected in the image.")
else:
    logging.info(f"Found {len(ocr_result.get_tables())} table(s).")
```

**為什麼要檢查：** 有些圖像可能雜訊較多或表格框線較淡，導致引擎漏掉表格。記錄警告訊息可以在不中斷腳本的情況下，提前得到回饋。

---

## 步驟 4：抽取每張表格的列與儲存格

真正的魔法就在這裡。我們會遍歷每個偵測到的表格，取出每一列，然後取得每個儲存格的文字。內部的 list comprehension 讓程式碼保持簡潔，我們仍會說明其流程。

```python
# Step 4 – Iterate over detected tables and collect data
all_tables = []   # Will hold a list of pandas DataFrames

for table_idx, table_obj in enumerate(ocr_result.get_tables(), start=1):
    logging.info(f"Processing Table #{table_idx}")

    rows_data = []   # Temporary storage for this table's rows

    for row_obj in table_obj.get_rows():
        # Extract text from each cell in the current row
        cell_texts = [cell.get_text() for cell in row_obj.get_cells()]
        rows_data.append(cell_texts)

    # Convert the raw list of rows into a DataFrame
    df = pd.DataFrame(rows_data)
    all_tables.append(df)

    # Print a human‑readable version to the console
    print("\n=== New Table ===")
    for row in rows_data:
        print("\t".join(row))
```

**這段程式在做什麼？**  

- `enumerate(..., start=1)` 為日誌提供友善的表格編號。  
- `row_obj.get_cells()` 取得每個儲存格物件；`cell.get_text()` 取得 OCR 解碼後的字串。  
- 我們把列資料存入 `rows_data`，再交給 `pandas.DataFrame`，它會自動對齊欄位。  
- `print` 區塊呈現原始範例中的 **essential output**，讓你即時驗證結果。

**邊緣案例處理：** 若某列的儲存格數量與其他列不同，`pandas` 會以 `NaN` 填補缺漏。之後可使用 `df.fillna('')` 轉成空字串。

---

## 步驟 5：將抽取的表格儲存為試算表

現在我們已擁有一系列 DataFrame，只要把它們寫入 Excel 工作簿（或 CSV 檔）就輕而易舉，完美達成 “convert image to spreadsheet” 的目標。

```python
# Step 5 – Export tables to Excel (one sheet per table)
output_path = Path("extracted_tables.xlsx")
with pd.ExcelWriter(output_path, engine="openpyxl") as writer:
    for idx, df in enumerate(all_tables, start=1):
        sheet_name = f"Table_{idx}"
        df.to_excel(writer, sheet_name=sheet_name, index=False)

logging.info(f"All tables saved to {output_path}")
```

**為什麼選 Excel？** 大多數商業使用者偏好 `.xlsx`。如果你較喜歡 CSV，只需將迴圈改為 `df.to_csv(f"table_{idx}.csv", index=False)` 即可。

---

## 完整、可直接執行的腳本

把所有步驟整合起來，以下就是你可以直接複製貼上並執行的完整程式。

```python
import ocr
from pathlib import Path
import pandas as pd
import logging

logging.basicConfig(level=logging.INFO)

# ---------- Configuration ----------
image_path = Path("YOUR_DIRECTORY/table_image.png")
output_path = Path("extracted_tables.xlsx")
# ----------------------------------

# Verify image exists
if not image_path.is_file():
    raise FileNotFoundError(f"Image not found: {image_path}")

# Initialize OCR engine
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(ocr.Imaging.Image.load(str(image_path)))

# Run recognition
ocr_result = ocr_engine.recognize()

if not ocr_result.get_tables():
    logging.warning("No tables detected in the image.")
    exit(0)

all_tables = []

for table_idx, table_obj in enumerate(ocr_result.get_tables(), start=1):
    logging.info(f"Processing Table #{table_idx}")
    rows_data = []

    for row_obj in table_obj.get_rows():
        cell_texts = [cell.get_text() for cell in row_obj.get_cells()]
        rows_data.append(cell_texts)

    df = pd.DataFrame(rows_data)
    all_tables.append(df)

    print("\n=== New Table ===")
    for row in rows_data:
        print("\t".join(row))

# Save to Excel
with pd.ExcelWriter(output_path, engine="openpyxl") as writer:
    for idx, df in enumerate(all_tables, start=1):
        df.to_excel(writer, sheet_name=f"Table_{idx}", index=False)

logging.info(f"All tables saved to {output_path}")
```

**預期的主控台輸出**（假設是一個 2×3 的簡易表格）：

```
=== New Table ===
Header1    Header2    Header3
Row1Col1   Row1Col2   Row1Col3
Row2Col1   Row2Col2   Row2Col3
```

執行後，你會在腳本所在的資料夾找到 `extracted_tables.xlsx`，每張表格都會放在獨立的工作表中。

---

## 常見問題與小技巧

| Question | Answer |
|----------|--------|
| **Can I use a different OCR library?** | 絕對可以。流程保持不變：載入圖像 → 辨識 → 迭代 `get_tables()`。只要替換匯入的套件與物件名稱即可。 |
| **What if my image is noisy?** | 在送入 OCR 引擎前，可先使用 OpenCV 進行前處理（二值化、去斜）。降噪通常能提升 **ocr extract table data** 的準確度。 |
| **Do I need to install `openpyxl`?** | 需要，`pandas` 會在背後使用它來輸出 Excel。使用 `pip install openpyxl` 安裝。 |
| **How do I handle merged cells?** | 部分 SDK 會提供 `cell.is_merged()`；你可以自行偵測並將值填補至合併範圍內。 |
| **Is there a way to extract only specific tables?** | 可以依 `table_obj.get_confidence()` 或檢查表頭關鍵字來過濾，僅處理符合條件的表格。 |

---

## 結語

現在你已擁有一套完整的端對端解決方案，能 **extract tables from image**、將結果轉換成整齊的試算表，甚至在單張圖片中同時處理多張表格。此腳本示範了如何 **load image for OCR**、**ocr read tables** 與 **ocr extract table data**，同時保持足夠彈性以因應實務上的各種變化。

接下來可以嘗試把 PDF 頁面先轉成圖像再套用，或是測試不同語言與字型。你也可以直接把 DataFrame 輸入資料庫或報表工具——想像力是唯一的限制。

如果你覺得本指南對你有幫助，歡迎分享、為提供 SDK 的倉庫加星，或在下方留言分享你的技巧。祝開發順利，願你的表格永遠能被完美解析！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}