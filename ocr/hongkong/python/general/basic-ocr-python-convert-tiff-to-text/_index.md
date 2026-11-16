---
category: general
date: 2026-03-18
description: 基本 OCR Python 教學展示如何將 TIFF 轉換為文字、載入影像 OCR、設定 GPU 層，並使用 Aspose AI 修正前導零。
draft: false
keywords:
- basic ocr python
- convert tiff to text
- load image ocr
- set gpu layers
- fix leading zeroes
language: zh-hant
og_description: 基本 OCR Python 教學會指導你將 TIFF 檔案轉換為乾淨文字、載入圖像、設定 GPU 層級，以及修正前導零。
og_title: 基本 OCR Python – 將 TIFF 轉換為文字
tags:
- OCR
- Python
- AI
- Aspose
title: 基本 OCR Python – 將 TIFF 轉換為文字
url: /zh-hant/python/general/basic-ocr-python-convert-tiff-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# basic ocr python – 使用 AI 後處理將 TIFF 轉換為文字

想要在掃描文件上執行 **basic ocr python** 嗎？本教學將示範如何使用 Aspose OCR 與 AI 後處理器，將 TIFF 檔案轉換為乾淨、可搜尋的文字。  

如果你曾因 **convert TIFF to text** 時，原始輸出充斥錯字或奇怪符號而苦惱，別擔心。我們也會說明如何 **load image OCR**、調整引擎以 **set GPU layers**，以及如何 **fix leading zeroes**（常見於發票編號的前置零）。


## What You’ll Learn

- 如何為列印文件初始化 Aspose OCR 引擎。  
- 從 TIFF 檔案 **load image OCR** 並取得原始文字的完整步驟。  
- 設定 AI 模型、自動下載，並 **setting GPU layers** 以提升推論速度。  
- 加入內建拼寫檢查以及自訂函式來 **fix leading zeroes**。  
- 清理 OCR 結果並正確釋放資源。  

完成本教學後，你將擁有一支可重複使用的 Python 腳本，能將任何 TIFF 轉換為精緻、可搜尋的文字——不需要手動複製貼上。

### Prerequisites

- 已在機器上安裝 Python 3.8+。  
- `aspose-ocr` 套件（`pip install aspose-ocr`）。  
- 可選：若想 **set GPU layers**，需具備至少 4 GB VRAM 的 GPU；否則程式會自動回退至 CPU。

---

## basic ocr python – load image and recognize text

我們首先要做的事是 **load image OCR**，讓引擎能讀取像素。Aspose 的 `OcrEngine` 支援多種格式，但此處聚焦於最常用於掃描發票的 TIFF。

```python
import aspose.ocr as ocr

# Initialise the OCR engine for printed documents
ocr_engine = ocr.OcrEngine()
ocr_engine.set_recognition_mode(ocr.RecognitionMode.PRINTED)   # use HANDWRITTEN for handwritten docs

# Load the TIFF file – replace with your own path
ocr_engine.load_image("YOUR_DIRECTORY/input.tif")
```

> **Pro tip:** 若處理 multi‑page TIFF，Aspose 會自動依序處理每一頁，無需額外迴圈。

圖片載入完成後，讓我們執行一次基本的辨識。

```python
# Perform basic OCR and capture the raw string
raw_text = ocr_engine.recognize()
print("Raw OCR:", raw_text)
```

你會看到類似以下的結果：

```
Raw OCR: Inv0ce N0: 0123AB4
Total Amt: $1,200.00
Date: 2024-07-15
```

注意字母前面的 *zeroes* 嗎？這是典型的 OCR 產物，我們稍後會清除它。

![basic ocr python workflow](/images/ocr-workflow.png "basic ocr python workflow diagram")

---

## Step 2: Convert TIFF to text – prepare the AI post‑processor

原始 OCR 雖有用，但大多數生產環境需要更精緻的版本。Aspose 提供的 `AsposeAI` 包裝器能從 Hugging Face 下載模型、在 GPU 上執行，並自動套用拼寫檢查。

```python
from aspose.ocr.ai import AsposeAI, AsposeAIModelConfig

# Configure the AI model – we’ll download Qwen2.5‑3B‑Instruct automatically
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",
    directory_model_path="YOUR_DIRECTORY/ocr_ai_models",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=25          # <-- this is where we **set GPU layers**
)

ocr_ai = AsposeAI(ai_config)
```

### Why `set GPU layers` matters

`gpu_layers` 參數告訴底層 GGUF 模型要在 GPU 上保留多少個 transformer 層。層數越多 → 推論更快，但 VRAM 用量也會提升。若使用一般筆記型電腦，可將數值降至 `10`，或直接省略以使用 CPU。

---

## Step 3: Apply spellcheck and **fix leading zeroes**

Aspose AI 內建拼寫檢查器，可捕捉大多數英文錯字。然而，領域特有的修正（例如將發票代碼前的 `0` 轉成 `O`）需要自訂後處理器。

```python
# Enable the built‑in spell‑check
ocr_ai.set_post_processor("spellcheck")

# Custom function to replace a leading zero before three capital letters
def invoice_fix(txt: str) -> str:
    import re
    # Example: "0ABC" -> "OABC"
    return re.sub(r"\b0([A-Z]{3})\b", r"O\1", txt)

# Register the custom fix – it runs after spellcheck
ocr_ai.set_post_processor(invoice_fix)
```

> **Why this works:** 正則表達式會尋找字邊界 (`\b`)、一個零，接著恰好三個大寫英文字母，然後把零替換成字母 “O”。你可以依需求擴充模式（例如 `0[0-9]{2}` 用於誤讀的數字）。

---

## Step 4: Clean the OCR result with the AI post‑processor

現在把所有步驟結合起來：**basic ocr python** 取得的原始字串、拼寫檢查，以及零字元修正。`run_postprocessor` 方法會回傳已清理好的版本，供下游系統使用。

```python
cleaned_text = ocr_ai.run_postprocessor(raw_text)
print("\nCleaned OCR:", cleaned_text)
```

後處理器的典型輸出：

```
Cleaned OCR: Invoice No: O123AB4
Total Amt: $1,200.00
Date: 2024-07-15
```

可以看到前置零已變成 `O`，常見的拼寫錯誤也已修正。此文字現在適合用於搜尋引擎索引或資料抽取流程。

---

## Step 5: Release AI resources – keep your GPU happy

若在長時間服務中執行多筆 OCR 任務，建議在完成後釋放模型的 GPU 記憶體。

```python
ocr_ai.free_resources()
```

忽略此步驟可能導致後續呼叫出現「out‑of‑memory」錯誤，尤其在 **set GPU layers** 設定較高時更為明顯。

---

## Optional Variations & Edge Cases

| Situation | What to change |
|-----------|----------------|
| **Handwritten documents** | Use `ocr_engine.set_recognition_mode(ocr.RecognitionMode.HANDWRITTEN)` instead of `PRINTED`. |
| **No GPU available** | Set `gpu_layers=0` or omit the argument; the model will run on CPU (slower but safe). |
| **Different language** | Swap the Hugging Face repo ID to a language‑specific model, e.g., `microsoft/Florence-2-base`. |
| **Batch processing** | Wrap the steps in a `for file in glob("*.tif"):` loop and accumulate results in a list or CSV. |
| **More complex zero patterns** | Extend `invoice_fix` with additional regexes, such as `r"\b0+([A-Z]{2,})\b"` for multiple leading zeroes. |

---

## Conclusion

我們剛完成一條 **basic ocr python** 流程：載入 TIFF、擷取原始文字，然後使用 AI 模型在 **setting GPU layers** 下進行效能優化與清理。自訂後處理器示範了如何 **fix leading zeroes**，這個細節常被忽略卻可能破壞下游分析。

歡迎自行實驗：嘗試不同的量化方式（如 `float16` 提升精度）、換用領域專屬字典的拼寫檢查，或串接多個自訂修正。整體模式不變——load、recognize、configure AI、post‑process、clean up。

**Next steps** 可能包括：

- 將清理後的輸出整合至資料庫或 Elasticsearch 索引。  
- 用相同方式 **convert TIFF to text** 處理多語言 PDF。  
- 使用 Flask 或 FastAPI 建置 UI，讓非技術使用者能上傳檔案並即時取得清理過的文字。  

祝開發順利，願你的 OCR 結果永遠清晰且零字元全無！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}