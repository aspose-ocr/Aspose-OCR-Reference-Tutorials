---
category: general
date: 2025-12-27
description: 使用 Aspose OCR 從圖片提取文字並校正 OCR 錯誤。了解如何載入圖片進行 OCR 並快速修正錯誤。
draft: false
keywords:
- extract text from image
- load image for ocr
- how to correct ocr errors
- Aspose OCR Python
- OCR post‑processing
language: zh-hant
og_description: 使用 Aspose OCR 從圖像中提取文字，並即時更正 OCR 錯誤。請依照本教學載入圖像進行 OCR，並清理結果。
og_title: 使用 Aspose OCR 從圖像提取文字 – 完整指南
tags:
- OCR
- Python
- Aspose
- Text Extraction
title: 使用 Aspose OCR 從圖像提取文字 – 逐步指南
url: /zh-hant/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose OCR 從圖像提取文字 – 步驟指南

是否曾需要 **從圖像提取文字**，卻被雜亂的 OCR 輸出搞得頭疼？你並不孤單。在許多自動化專案中——例如發票處理、收據掃描或舊文件數位化——首要障礙就是從圖片取得乾淨、可搜尋的文字。  

在本教學中，我們將逐步示範一個完整且可執行的範例，說明如何 **load image for OCR**、執行辨識，並使用 Aspose 的 AI 驅動拼寫檢查後處理器 **correct OCR errors**。完成後，你將擁有一支腳本，能將發票的 PNG 轉換為精緻、可搜尋的文字，供後續工作流程使用。

## 你將學到

- 如何在 Python 中安裝與匯入 Aspose OCR 與 AI 函式庫。  
- 完整的 **load image for OCR** 程式碼（不需猜測）。  
- 如何執行 OCR 引擎並取得原始字串。  
- 為何 OCR 常會產生錯字，以及內建的拼寫檢查處理器如何自動 **correct OCR errors**。  
- 處理多頁 PDF 或低解析度掃描等邊緣案例的技巧。

> **前置條件：** Python 3.8 以上、有效的 Aspose OCR 授權（或免費試用），以及你想處理的圖像檔案（例如 `invoice.png`）。

## 從圖像提取文字 – 設定 Aspose OCR

在執行任何操作之前，我們需要先安裝正確的套件。Aspose 以可透過 pip 安裝的模組方式提供 OCR 引擎。

```bash
pip install aspose-ocr
```

如果你也需要 AI 後處理器，請安裝配套套件：

```bash
pip install aspose-ocr-ai
```

> **小技巧：** 保持套件為最新版本。撰寫本文時，最新版本為 `aspose-ocr 23.12` 與 `aspose-ocr-ai 23.12`。

一旦套件安裝完成，匯入你將使用的類別：

```python
# Step 1: Import the OCR and AI classes
from aspose.ocr import OcrEngine, AsposeAI
```

> **為什麼這很重要：** 匯入特定類別可保持命名空間整潔，並清楚顯示哪些元件負責辨識，哪些負責後處理。

## 載入圖像以進行 OCR – 準備你的發票 PNG

接下來的合理步驟是將引擎指向你想要讀取的檔案。這時 **load image for OCR** 關鍵字就派上用場了。

```python
# Step 2: Create an OCR engine instance
ocr_engine = OcrEngine()

# Step 3: Load the image you want to process
ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")
```

> **說明：** `OcrEngine()` 會建立一個使用預設設定（英文、auto‑rotation 等）的全新引擎。`load_image()` 方法接受檔案路徑、串流，甚至是位元組陣列——因此你可以從磁碟、網路或記憶體緩衝區提供圖像。

### 載入圖像時的常見陷阱

| 問題 | 徵兆 | 解決方式 |
|-------|---------|-----|
| 低 DPI（<300） | 字元亂碼、數字缺失 | 在載入前將影像重新取樣至 300 dpi 或更高 |
| 顏色模式不正確（CMYK） | 字形錯誤 | 使用 Pillow 轉換為 RGB (`Image.convert("RGB")`) |
| 多頁 PDF | 僅處理第一頁 | 將每頁轉為圖像並逐頁處理 |

## 執行 OCR 並取得原始文字

現在引擎已知道圖片所在位置，我們即可讀取它。

```python
# Step 4: Perform OCR to extract raw text
raw_text = ocr_engine.recognize()
print("Raw OCR output:")
print(raw_text)
```

`recognize()` 呼叫會回傳純 Python 字串。在許多實務情境中，輸出可能包含多餘的空格、誤讀的字元或斷裂的換行——尤其是使用緊縮字體的收據。

> **為什麼先捕獲 raw_text：** 它提供一個基準，讓你之後能與清理過的版本比較，對除錯或稽核很有幫助。

## 如何校正 OCR 錯誤 – 使用 Aspose AI 拼寫檢查

Aspose 提供一個輕量級的 AI 包裝器，可對原始輸出執行拼寫檢查後處理器。這直接回應了 **how to correct OCR errors** 的問題。

```python
# Step 5: Initialise the AI post‑processor and choose a spell‑check processor
ai_processor = AsposeAI()
ai_processor.set_post_processor("spell_check")
```

如果你的使用情境需要，你可以將 `"spell_check"` 替換為其他處理器，例如 `"grammar_check"` 或 `"named_entity_recognition"`。

```python
# Step 6: Clean the OCR output using the selected post‑processor
clean_text = ai_processor.run_postprocessor(raw_text)

# Step 7: Output the corrected text
print("\nCorrected OCR output:")
print(clean_text)
```

### 拼寫檢查在背後的運作原理

1. **Tokenisation** – 將原始字串切分為單詞與標點符號。  
2. **Dictionary Lookup** – 將每個 token 與英文詞典（或你提供的自訂詞典）比對。  
3. **Contextual Scoring** – 使用小型語言模型判斷校正是否符合上下文。  
4. **Replacement** – 回傳套用最可能校正後的新字串。

> **邊緣情況：** 如果來源語言不是英文，建立 `AsposeAI()` 時請傳入相應的語言代碼（例如 `AsposeAI(language="fr")`）。

## 驗證與使用清理過的文字

此時你會有兩個變數：`raw_text`（直接的 OCR 輸出）與 `clean_text`（拼寫檢查後的版本）。保留哪一個取決於你的後續需求。

```python
# Example: Save the cleaned text to a .txt file for later indexing
with open("invoice_extracted.txt", "w", encoding="utf-8") as f:
    f.write(clean_text)

print("\n✅ Cleaned text saved to invoice_extracted.txt")
```

> 如果你將結果輸入搜尋引擎、資料庫或機器學習模型，請始終使用 **cleaned** 版本——否則會將 OCR 噪聲傳播至整個流程。

## 完整可執行範例

以下是完整腳本，你可以直接複製貼上成名為 `extract_invoice.py` 的檔案。假設你已安裝上述兩個 Aspose 套件，且圖像位於 `YOUR_DIRECTORY/invoice.png`。

```python
# extract_invoice.py
# -------------------------------------------------------------
# Complete example: extract text from image and correct OCR errors
# -------------------------------------------------------------

# 1️⃣ Import required classes
from aspose.ocr import OcrEngine, AsposeAI

# 2️⃣ Create OCR engine and load the target image
ocr_engine = OcrEngine()
ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")

# 3️⃣ Run OCR – get raw text
raw_text = ocr_engine.recognize()
print("Raw OCR output:")
print(raw_text)

# 4️⃣ Initialise AI spell‑check post‑processor
ai_processor = AsposeAI()
ai_processor.set_post_processor("spell_check")

# 5️⃣ Clean the OCR output
clean_text = ai_processor.run_postprocessor(raw_text)

# 6️⃣ Show the corrected result
print("\nCorrected OCR output:")
print(clean_text)

# 7️⃣ Persist the cleaned text for later use
with open("invoice_extracted.txt", "w", encoding="utf-8") as out_file:
    out_file.write(clean_text)

print("\n✅ Cleaned text saved to invoice_extracted.txt")
```

執行後，你會先看到原始輸出，接著是較整潔的版本，且同資料夾內會產生名為 `invoice_extracted.txt` 的檔案。

```bash
python extract_invoice.py
```

## 常見問題 (FAQ)

**Q: 這能用於 PDF 嗎？**  
A: 不能直接使用。請將每頁 PDF 轉為圖像（例如使用 `pdf2image`），再對產生的 PNG 逐一執行腳本。

**Q: 我的語言不是英文——還能使用拼寫檢查嗎？**  
A: 可以。將想要的語言代碼傳給 `AsposeAI(language="de")`（德文）、`"es"`（西班牙文）等。

**Q: 如果 OCR 引擎誤判表格佈局該怎麼辦？**  
A: Aspose OCR 提供 `set_layout_analysis(True)` 旗標。啟用後可提升表格偵測，但可能增加處理時間。

**Q: 如何處理極大量的批次？**  
A: 將核心邏輯封裝成函式，並使用執行緒池或 async IO 於多核心或多機器上平行處理。

## 總結

我們已示範如何使用 Aspose OCR **extract text from image**、如何 **load image for OCR**，以及使用內建 AI 拼寫檢查最直接的 **correct OCR errors** 方法。完整可執行的腳本展示了從載入發票 PNG 到儲存乾淨、可搜尋的 `.txt` 檔案的端到端流程。

歡迎自行嘗試：將拼寫檢查換成文法校正、將輸出餵入 NLP 分類器，或整合至更大的文件管理系統。只要擁有可靠、校正過的文字，應用無限可能。

對 OCR、Aspose 或 Python 自動化有更多疑問嗎？在下方留言，我們會回覆。祝編程愉快！ 

![從圖像提取文字範例](extract_text_image.png "使用 Aspose OCR 從圖像提取文字")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}