---
category: general
date: 2026-04-26
description: 如何在 Python 中批量 OCR 您的文件並從掃描檔案中提取文字。學習使用 OcrEngine 逐步批次處理，輸出 JSON。
draft: false
keywords:
- how to batch OCR
- extract text from scans
- OCR batch processing
- Python OCR automation
- JSON OCR output
language: zh-hant
og_description: 如何批量 OCR 您的掃描檔案，並在單一腳本中提取掃描文字。完整程式碼、技巧與邊緣案例處理。
og_title: 如何批次 OCR – 快速 Python 指南
tags:
- OCR
- Python
- Automation
title: 如何批次 OCR – 高效從掃描檔提取文字
url: /zh-hant/python-java/general/how-to-batch-ocr-extract-text-from-scans-efficiently/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何批量 OCR – 從掃描檔案高效提取文字

有沒有想過 **如何批量 OCR** 那堆掃描的 PDF 而不讓自己抓狂？你並不是唯一有這個疑問的人——開發者常常會問：「一次過要怎樣從掃描檔案提取文字？」好消息是，只要幾行 Python 程式碼，就能把這項繁瑣工作變成順暢、全自動的流程。

在本教學中，我們將一步步示範完整、可直接執行的解決方案，**從掃描檔案提取文字**、將結果儲存為 JSON，並在最後給予簡易的 sanity check。無需外部服務、無需魔法——只要純 Python、`OcrEngine` 類別，以及一點目錄操作。

## 你將學會什麼

- 一個能 **批量 OCR** 任意圖片資料夾的完整腳本。
- 為何每一行程式碼會出現的清楚說明，而不只是它做了什麼。
- 處理空資料夾、非圖片檔案與大型批次的技巧。
- 驗證 JSON 輸出確實包含已提取文字的方法。

### 前置條件（最低需求）

| Requirement | Why it matters |
|-------------|----------------|
| Python 3.8+ | Modern syntax & type hints |
| `OcrEngine` library (or a compatible wrapper) | Core OCR functionality |
| A directory with scanned image files (PNG, JPG, TIFF) | Input data |
| Write permissions for the output folder | Saving JSON results |

如果你已經具備上述條件，太好了——讓我們直接開始吧。

![how to batch OCR workflow](image-placeholder.png){alt="批量 OCR 工作流程"}

## 步驟 1 – 初始化 OCR 引擎（how to batch OCR）

在處理任何檔案之前，我們需要先建立一個 OCR 引擎實例。把它想成會閱讀每張圖片並輸出文字的「大腦」。只初始化一次並在整個批次中重複使用，是最有效率的做法。

```python
# Step 1: Create an OCR engine instance
# The OcrEngine class abstracts the low‑level OCR library (Tesseract, EasyOCR, etc.)
ocr_engine = OcrEngine()
```

> **為什麼要重複使用同一個實例？**  
> 若每個檔案都重新建立引擎，會不斷把龐大的模型載入記憶體，導致批次處理速度急劇下降。單一實例只需在 RAM 中保留模型，即可處理上千張圖片而不會明顯變慢。

## 步驟 2 – 指定掃描檔案所在資料夾（extract text from scans）

你的掃描檔案儲存在磁碟的某個位置。現在告訴腳本它們在哪裡。使用絕對路徑可以避免在不同工作目錄下執行腳本時出現「找不到檔案」的狀況。

```python
import os

# Step 2: Specify the folder that contains scanned images
# Replace YOUR_DIRECTORY with the actual base path on your machine.
input_dir = os.path.abspath("YOUR_DIRECTORY/scans/")
```

> **小技巧：**  
> 若你使用 Windows，`os.path.abspath` 同樣支援正斜線（`/`），因此不必對反斜線進行跳脫。

## 步驟 3 – 設定 JSON 結果的輸出位置

你可能想要一個整潔的資料夾來存放 OCR 結果。把輸出與原始檔案分開，日後清理或將 JSON 匯入其他流程都會更方便。

```python
# Step 3: Specify where the JSON results should be saved
output_dir = os.path.abspath("YOUR_DIRECTORY/json_output/")
os.makedirs(output_dir, exist_ok=True)   # Ensure the folder exists
```

> **為什麼要程式化建立資料夾？**  
> 這樣即使目錄不存在，腳本也不會崩潰；`exist_ok=True` 讓操作具備冪等性——可多次執行腳本而不會產生錯誤。

## 步驟 4 – 執行批次處理（how to batch OCR）

現在進入重點：告訴 `ocr_engine` 逐一走訪 `input_dir` 中的每個檔案、執行 OCR，並把 JSON 寫入 `output_dir`。`format="json"` 參數會指示引擎以結構化的方式序列化結果，方便下游工具使用。

```python
# Step 4: Run batch processing to convert all scans to JSON format
ocr_engine.batch_process(
    input_folder=input_dir,
    output_folder=output_dir,
    format="json"
)
```

### 背後發生了什麼？

1. **檔案探索** – 引擎會遞迴掃描 `input_folder`，自動忽略隱藏檔案。  
2. **檔案驗證** – 只會把支援的影像副檔名（`.png`、`.jpg`、`.tif` 等）送入 OCR 模型。  
3. **OCR 執行** – 每張圖片都會傳給 OCR 引擎，取得文字、信心分數與版面資訊。  
4. **JSON 序列化** – 結果會寫入與原檔名相同、但副檔名為 `.json` 的檔案於 `output_folder`。

> **邊緣案例處理：**  
> - **空資料夾：** 引擎會記錄「No files found」並優雅返回。  
> - **損毀的影像：** 會跳過該檔案，於 `batch_errors.log` 中留下錯誤紀錄，然後繼續執行。  
> - **超大型批次（10k+ 檔案）：** 記憶體使用量仍保持低位，因為每次只處理單一圖片。

## 步驟 5 – 確認轉換已完成

一行簡單的 `print` 陳述式即可在主控台即時回饋。若在正式流水線上，可改為使用 logging 或發送 email 通知。

```python
# Step 5: Inform the user that the batch conversion has finished
print("Batch conversion complete.")
```

當你看到那行訊息時，就可以安全地檢查 `json_output` 資料夾。每個 JSON 檔案大致會長這樣：

```json
{
  "file_name": "invoice_001.png",
  "text": "Invoice #001\nDate: 2024‑12‑01\nTotal: $1,234.56",
  "confidence": 0.97,
  "layout": [
    {"line": 1, "bbox": [10, 20, 200, 40]},
    {"line": 2, "bbox": [10, 50, 180, 70]},
    {"line": 3, "bbox": [10, 80, 150, 100]}
  ]
}
```

接著，你可以把這些 JSON 檔案匯入資料庫、搜尋索引，或任何下游分析工具。

## 常見問題（快速解答）

**Q: 若要處理 PDF 而不是影像該怎麼辦？**  
A: 先把每頁 PDF 轉成影像（例如使用 `pdf2image`），再把產生的 PNG/JPG 放入 `input_dir`。批次 OCR 的邏輯不需要變動。

**Q: 可以把輸出格式改成純文字嗎？**  
A: 當然可以。將 `format="json"` 改成 `format="txt"`，引擎就會產生只包含提取文字的 `.txt` 檔案。

**Q: 我的掃描檔分散在多個子資料夾，腳本會遞迴嗎？**  
A: 會的。`batch_process` 預設會遍歷整個目錄樹。若想要平面輸出，可設定 `flatten=True`（若函式庫支援）或在後處理時自行調整 JSON 檔名。

**Q: 如何處理非拉丁文字？**  
A: 在建立 `OcrEngine` 時加入語言參數，例如 `OcrEngine(lang="spa+eng")`。批次迴圈本身不需要任何修改。

## 專業小技巧與常見陷阱

- **批次大小很重要：** 若發現 CPU 使用率飆升，可在每個檔案之間加入 `time.sleep(0.1)` 以降低負載。  
- **日誌記錄：** 把 `print` 換成 Python 的 `logging` 模組，能取得時間戳記與錯誤等級。  
- **檔名衝突：** 若不同子資料夾內的掃描檔案基礎名稱相同，輸出的 JSON 會互相覆蓋。可在輸出名稱後加上相對路徑的雜湊值以避免衝突。  
- **記憶體洩漏：** 某些 OCR 後端會保留原生資源。腳本結尾若函式庫提供清理方法，請呼叫 `ocr_engine.close()`。

## 完整腳本 – 直接複製貼上使用

```python
import os
from ocr_engine import OcrEngine   # Replace with the actual import path

def main():
    # Step 1: Initialize the OCR engine (how to batch OCR)
    ocr_engine = OcrEngine()

    # Step 2: Directory with scanned images (extract text from scans)
    input_dir = os.path.abspath("YOUR_DIRECTORY/scans/")
    if not os.path.isdir(input_dir):
        raise FileNotFoundError(f"Input folder not found: {input_dir}")

    # Step 3: Destination for JSON results
    output_dir = os.path.abspath("YOUR_DIRECTORY/json_output/")
    os.makedirs(output_dir, exist_ok=True)

    # Step 4: Run the batch OCR process
    ocr_engine.batch_process(
        input_folder=input_dir,
        output_folder=output_dir,
        format="json"
    )

    # Step 5: Confirmation message
    print("Batch conversion complete.")

if __name__ == "__main__":
    main()
```

**預期的主控台輸出**

```
Scanning folder: /home/user/YOUR_DIRECTORY/scans/
Found 42 image files.
Processing file 1/42: invoice_001.png … done.
Processing file 2/42: receipt_2024-03.jpg … done.
…
Batch conversion complete.
```

你可以打開 `json_output` 中的任意檔案，用文字編輯器檢視，或在 Python 中載入：

```python
import json, pathlib

sample = pathlib.Path(output_dir) / "invoice_001.json"
data = json.loads(sample.read_text())
print(data["text"])
```

應該會在主控台印出原始的 OCR 提取文字。

## 結語

我們剛剛完成了 **如何批量 OCR** 整個掃描影像資料夾，並將 **從掃描檔案提取文字** 成為乾淨、機器可讀的 JSON 檔案。整個流程刻意保持簡單：一次設定引擎、指向資料夾，讓函式庫負責繁重的運算。接下來，你可以：

- 把 JSON

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}