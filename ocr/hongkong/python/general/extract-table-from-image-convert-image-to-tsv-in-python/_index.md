---
category: general
date: 2026-07-05
description: 使用 Python OCR 從影像中提取表格。學習如何提取表格、將影像轉換為 TSV，並掌握 OCR 表格影像的 Python 技巧。
draft: false
keywords:
- extract table from image
- how to extract table
- convert image to tsv
- ocr table image python
language: zh-hant
og_description: 使用 Python OCR 從圖像提取表格。本指南示範如何提取表格、將圖像轉換為 TSV，並使用 OCR 表格圖像 Python 工具。
og_title: 從圖像提取表格 – 在 Python 中將圖像轉換為 TSV
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract table from image using Python OCR. Learn how to extract table,
    convert image to TSV, and master ocr table image python techniques.
  headline: Extract Table from Image – Convert Image to TSV in Python
  type: TechArticle
- description: Extract table from image using Python OCR. Learn how to extract table,
    convert image to TSV, and master ocr table image python techniques.
  name: Extract Table from Image – Convert Image to TSV in Python
  steps:
  - name: Initialise the aocr OCR engine.
    text: Initialise the aocr OCR engine.
  - name: Attach the AI post‑processor.
    text: Attach the AI post‑processor.
  - name: Load a table image.
    text: Load a table image.
  - name: Perform structured OCR.
    text: Perform structured OCR.
  - name: Clean the results.
    text: Clean the results.
  - name: Export the table as a TSV file.
    text: Export the table as a TSV file.
  type: HowTo
tags:
- OCR
- Python
- Table Extraction
title: 從圖片提取表格 – 使用 Python 將圖片轉換為 TSV
url: /zh-hant/python/general/extract-table-from-image-convert-image-to-tsv-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從圖片提取表格 – 在 Python 中將圖片轉換為 TSV

有沒有想過如何在不抓狂的情況下從圖片中提取表格？在本教學中，我們將使用 `aocr` 套件一步步說明 **如何提取表格** 資料，然後將其轉換為整齊的 TSV 檔案。沒有魔法，只需要幾行 Python 程式碼加上一點 AI 後處理。

如果你曾經嘗試從掃描的發票或螢幕截圖中複製貼上表格，結果卻變成一團亂碼，你會明白為什麼掌握 OCR 為基礎的方法很重要。完成本教學後，你將能將任何表格圖片輸入 Python，取得乾淨的以制表符分隔的資料，直接用於試算表或資料庫。

---

## 你需要的條件

| 需求 | 為何重要 |
|------|----------|
| Python 3.9+ | `aocr` 套件針對現代的 Python 執行環境。 |
| `aocr` library (`pip install aocr`) | 提供我們將使用的 OCR 引擎與 AI 後處理器。 |
| An image file containing a table (PNG, JPG, etc.) | 我們將要提取的來源資料。 |
| Optional: a virtual environment | 將相依套件隔離，強烈建議使用。 |

事先準備好這些項目，可避免在教學過程中途被打斷。

## 安裝相依套件

首先，讓我們安裝 OCR 工具。打開終端機並執行以下指令：

```bash
# Create and activate a virtual environment (optional but clean)
python -m venv ocr-env
source ocr-env/bin/activate   # On Windows: ocr-env\Scripts\activate

# Install the aocr package
pip install aocr
```

> **小技巧：** 若遇到權限錯誤，請在 `pip install` 指令後加上 `--user`，或使用 `pipx` 進行全域安裝。

## 步驟 1 – 初始化 OCR 引擎

引擎是整個流程的核心。可以把它想像成「大腦」，會檢視每一個像素並決定哪個字元應該放在哪裡。

```python
import aocr

# Create an OCR engine instance – this sets up the model and default settings
engine = aocr.OcrEngine()
```

為什麼要實例化一個引擎，而不是直接呼叫單一函式？引擎物件讓我們之後可以附加自訂的後處理器，從而對輸出進行精細控制——在需要 **ocr table image python** 準確度時尤為重要。

## 步驟 2 – 附加 AI 後處理器

`aocr` 內建輕量級的 AI 後處理器，能在保留儲存格邊框的同時清理原始 OCR 結果。無需額外參數，使程式碼保持簡潔。

```python
# Hook the AI post‑processor into the engine
engine.set_post_processor(ai.run_postprocessor, None)
```

如果跳過此步驟，你仍會得到原始文字，但表格結構會很雜亂——就像每個儲存格都是謎團的試算表。後處理器負責將文字對齊至原始格線，完成繁重的工作。

## 步驟 3 – 載入表格影像

你可以從任意路徑載入影像，為了說明清楚，我們使用佔位目錄。請將 `"YOUR_DIRECTORY/invoice_table.png"` 替換為實際檔案的路徑。

```python
# Load the image that contains the table
image_path = "YOUR_DIRECTORY/invoice_table.png"
image = aocr.Image.from_file(image_path)
```

> **注意：** `aocr.Image` 會自動偵測影像格式並正規化色彩通道，除非影像嚴重退化，否則不需要事先處理檔案。

## 步驟 4 – 執行結構化 OCR

現在引擎會掃描影像並回傳原始表格物件。此物件包含列、欄以及每個儲存格的原始文字。

```python
# Recognise the table structure and extract raw cell data
raw_table = engine.recognize_structured(image)
```

為什麼使用 `recognize_structured` 而非一般的 `recognize` 呼叫？結構化版本會嘗試推斷列/欄的邊界，提供類似矩陣的結果，之後轉換為 TSV 時會更容易。

## 步驟 5 – 使用 AI 後處理器清理資料

執行後處理器會精練原始輸出：移除雜散字元、合併被切割的片段，並確保每個儲存格的文字正確對齊。

```python
# Apply the AI post‑processor to tidy up the table
processed_table = engine.run_postprocessor(raw_table)
```

如果檢查 `processed_table.table`，你會看到一個列的列表，每列都是 `Cell` 物件的列表。每個 `Cell` 都有 `.text` 屬性，保存清理後的字串。

## 步驟 6 – 匯出表格為 TSV

最後一步是將處理過的資料轉換為以制表符分隔的檔案（TSV）——這正是你在想要 **convert image to TSV** 以供 Excel 或 Google Sheets 使用時所需要的。

```python
import csv

# Define the output TSV path
tsv_path = "extracted_table.tsv"

# Open the file and write rows as tab‑separated values
with open(tsv_path, "w", newline="", encoding="utf-8") as tsv_file:
    writer = csv.writer(tsv_file, delimiter="\t")
    for row in processed_table.table:
        # Extract text from each cell and write the row
        writer.writerow([cell.text for cell in row])

print(f"✅ Table successfully saved to {tsv_path}")
```

執行腳本會將每列印到主控台（如果你喜歡），並寫入一個乾淨的 TSV 檔案，任何試算表程式都能開啟。

### 快速驗證

```python
# Print the TSV to the console for a sanity check
for row in processed_table.table:
    print("\t".join(cell.text for cell in row))
```

你應該會看到整齊對齊的欄位，例如：

```
Item	Qty	Price	Total
Apple	10	0.50	5.00
Banana	5	0.30	1.50
```

如果輸出看起來亂碼，請再次檢查影像品質（清晰度、對比度），並考慮調整 OCR 引擎的設定——`engine.set_config(...)` 可讓你調整語言模型與信心門檻。

## 處理常見邊緣案例

| 情況 | 建議解決方案 |
|------|--------------|
| **影像傾斜** | 使用 `Pillow` 的 `Image.rotate` 先行旋轉，再送入 `aocr`。 |
| **對比度低** | 使用直方圖均衡化 (`cv2.equalizeHist`) 提升可讀性。 |
| **儲存格合併** | 在 TSV 後處理時依已知分隔符拆分儲存格，或在可用時使用 `merge_cells=False` 參數。 |
| **多頁 PDF** | 先將每頁轉為影像 (`pdf2image`)，再在迴圈中執行管線。 |

這些調整可讓你的 **ocr table image python** 工作流程在各種來源素材下保持穩定。

## 完整腳本 – 一站式解決方案

以下是完整、可直接執行的腳本，整合了上述所有步驟。將其儲存為 `extract_table.py`，然後執行 `python extract_table.py`。



## 接下來該學什麼？

以下教學涵蓋與本指南密切相關的主題，並在此基礎上延伸。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在自己的專案中探索其他實作方式。

- [使用 Aspose OCR 從影像提取文字 – 步驟說明指南](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [如何使用 Aspose.OCR for .NET 從影像提取表格](/ocr/english/net/text-recognition/recognize-table/)
- [如何透過在 OCR 中預備矩形來提取影像文字](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}