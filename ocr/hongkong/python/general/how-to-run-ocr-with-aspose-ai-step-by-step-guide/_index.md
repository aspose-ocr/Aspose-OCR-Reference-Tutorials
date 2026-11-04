---
category: general
date: 2026-02-09
description: 如何使用 Aspose AI 與 Hugging Face 模型執行 OCR ——學習下載 Hugging Face 模型、校正 OCR
  錯誤及釋放 GPU 記憶體。
draft: false
keywords:
- how to run OCR
- download hugging face model
- free gpu memory
- how to free gpu
- correct OCR errors
language: zh-hant
og_description: 在第一段說明了如何使用 Aspose AI 執行 OCR——了解如何下載 Hugging Face 模型、校正 OCR 錯誤以及釋放
  GPU 記憶體。
og_title: 如何使用 Aspose AI 執行 OCR – 完整指南
tags:
- OCR
- Aspose
- AI
- HuggingFace
title: 如何使用 Aspose AI 執行 OCR – 逐步指南
url: /zh-hant/python/general/how-to-run-ocr-with-aspose-ai-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose AI 執行 OCR – 完整指南

有沒有想過在掃描的發票上 **執行 OCR**，且能取得完美乾淨的數字，而不需要花數小時去修正錯字？你並不孤單。在許多實務專案中，傳統 OCR 引擎輸出的原始文字仍會包含雜散字元、破損的貨幣符號或錯亂的數字——尤其當來源影像噪點較多時。  

好消息是，你可以將大型語言模型（LLM）接到 Aspose OCR，即時下載 Hugging Face 模型，讓 AI 為你潤飾輸出結果。在本教學中，我們將完整示範整個流程，從取得模型（是的，我們會示範如何自動 **download hugging face model**）到完成後釋放 GPU 資源。最終，你將擁有一支可重現的腳本，能 **corrects OCR errors**、在一般 GPU 上快速執行，且會自行清理，避免記憶體浪費。

## 您將學習

- 設定 Aspose AI 從 Hugging Face 取得 **Qwen2.5‑3B‑Instruct‑GGUF** 模型。  
- 在影像檔上執行標準的 Aspose OCR 引擎。  
- 使用自訂的 LLM 提示詞，確保數字與貨幣符號保持完整。  
- 使用內建的 **free gpu memory** 程式釋放 GPU 記憶體。  
- 微調工作流程，以因應多頁 PDF 或低階 GPU 等特殊情況。  

> **先決條件** – Python 3.9+、`aspose-ocr` 套件、首次下載模型時需要網路連線，以及至少 4 GB VRAM 的 GPU（非必要但建議）。若沒有 GPU，腳本會自動改用 CPU 執行剩餘層級。  

---

## 如何執行 OCR 並提升結果

以下是完整、可直接執行的 Python 程式碼。請將其存為 `ocr_with_ai.py`，並將佔位路徑替換成你的檔案路徑。

```python
# ocr_with_ai.py
import aspose.ocr as aocr
from aspose.ocr.ai import AsposeAI, AsposeAIModelConfig

# -------------------------------------------------
# Step 1 – Configure the AI engine (download hugging face model)
# -------------------------------------------------
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",                     # auto‑download if missing
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",               # tiny memory footprint
    gpu_layers=20,                                  # 20 layers on GPU, rest on CPU
    directory_model_path=r"YOUR_DIRECTORY/Models"  # optional custom folder
)
ai = AsposeAI(ai_config)

# -------------------------------------------------
# Step 2 – Load an image and run the classic OCR engine
# -------------------------------------------------
ocr_engine = aocr.OcrEngine()
ocr_engine.load_image(r"YOUR_DIRECTORY/invoice.png")
raw_text = ocr_engine.recognize()   # returns plain‑text string

# -------------------------------------------------
# Step 3 – Register a custom LLM prompt (correct OCR errors)
# -------------------------------------------------
def financial_prompt():
    # Bias the model toward financial terminology
    return {"prompt": "Correct OCR errors, keep numbers and currency symbols intact"}

ai.set_post_processor("llm_correction", financial_prompt)

# -------------------------------------------------
# Step 4 – Let the LLM polish the output
# -------------------------------------------------
corrected_text = ai.run_postprocessor(raw_text)

print("Original :", raw_text)
print("Enhanced :", corrected_text)

# -------------------------------------------------
# Step 5 – Release resources (free gpu memory)
# -------------------------------------------------
ai.free_resources()
```

> **專業提示**：`gpu_layers` 參數讓你決定有多少 transformer 層保留在 GPU 上。若遇到記憶體不足錯誤，可降低此數值，其餘層將在 CPU 上執行——之後仍可使用 `ai.free_resources()` **free gpu memory**。

### 預期輸出

在範例發票上執行此腳本，會得到類似以下的結果：

```
Original : Invoic # 12345 \n Total: $1O0.00\n Date: 2023-07-15
Enhanced : Invoice # 12345
Total: $100.00
Date: 2023-07-15
```

請注意，AI 將 `$1O0.00` 中的「O」修正為正確的零，同時保留美元符號。這正是金融文件中 **correct OCR errors** 的核心。

## 下載 Hugging Face 模型 – 內部運作原理

當你將 `allow_auto_download="true"` 設定為真時，Aspose AI 包裝器會檢查 `directory_model_path`。若該目錄中沒有模型檔案，它會向 Hugging Face Hub 請求，下載 **int8‑quantized** 版的 `Qwen2.5‑3B‑Instruct‑GGUF`，並儲存於本機。此一次性下載通常不超過 2 GB，即使在一般 SSD 上也能輕鬆容納。  

> **為何使用 int8？** 將模型量化至 8 位元可大幅降低記憶體使用量——在你需要 **free gpu memory** 後處理時尤為關鍵。雖然會稍微影響準確度，但對於 OCR 後處理的文字而言，影響可忽略不計。  

如果你想自行託管模型，只需將 `.gguf` 檔案放入 `YOUR_DIRECTORY/Models`，Aspose 便會直接載入，無需再次連線至網路。  

## 如何釋放 GPU – 最佳實踐

GPU 資源在多數工作站上屬於共享資源。腳本結束後若仍保留張量，會導致後續工作出現「CUDA out of memory」錯誤。`ai.free_resources()` 會執行以下三項動作：

1. **釋放底層 transformer** – 所有駐留於 GPU 的權重皆被釋放。  
2. **清除 PyTorch 快取** – 內部會呼叫 `torch.cuda.empty_cache()`。  
3. **刪除暫存檔案** – 下載過程中產生的磁碟快取會被移除。  

如果你同時使用 Aspose AI 與其他 PyTorch 工作負載，也可以手動呼叫 `torch.cuda.empty_cache()`，但內建方法通常已足夠。  

## 步驟說明 (含次要關鍵字的 H2)

### 自動下載 Hugging Face 模型

`AsposeAIModelConfig` 建構子封裝了與 Hugging Face API 互動的複雜性。只要在首次執行腳本時具備網路連線即可。之後模型會存放於 `YOUR_DIRECTORY/Models`，後續執行即可即時啟動。  

### 推論後釋放 GPU 記憶體

若你在長時間運行的服務（例如 Flask API）中使用此功能，請於每次請求結束後呼叫 `ai.free_resources()`。這可防止記憶體泄漏，確保下一個請求能順利重用同一 GPU。  

### 使用自訂提示詞校正 OCR 錯誤

我們的 `financial_prompt` 函式會回傳一個僅含 `prompt` 鍵的字典。你可以依需求調整為任何領域：

```python
def medical_prompt():
    return {"prompt": "Fix OCR mistakes, keep dosage numbers and units unchanged"}
```

將 `ai.set_post_processor(...)` 中的函式名稱替換，即可得到適用於醫療紀錄的 **correct OCR errors** 流程。  

### 如何在多頁 PDF 上執行 OCR

Aspose OCR 原生支援 PDF 處理：

```python
ocr_engine.load_document(r"YOUR_DIRECTORY/multi_page.pdf")
raw_text = ocr_engine.recognize()  # concatenates pages automatically
```

取得原始字串後，同樣的 LLM 後處理器會清理每一頁的文字，無需額外程式碼。  

### 當沒有 GPU 時 – 如何釋放 GPU（即使沒有 GPU）

即使在僅有 CPU 的機器上，呼叫 `ai.free_resources()` 也不會有害，它僅會清除內部快取，仍能釋放 RAM。因此 **how to free gpu** 的建議適用於所有情況：務必自行清理。  

## 常見問題與解決方式

| Issue | Why It Happens | Fix |
|-------|----------------|-----|
| **GPU 記憶體不足** | `gpu_layers` 設定過高，超出顯卡容量 | 將 `gpu_layers` 降至 10 或 5，讓其餘層在 CPU 上執行 |
| **模型無法下載** | 公司防火牆阻擋了對 huggingface.co 的 HTTPS 連線 | 在其他網路手動下載模型，然後將 `directory_model_path` 指向本機資料夾 |
| **數字被破壞** | 提示詞未明確說明要保留數字 | 在提示詞中加入 “preserve all numeric values and currency symbols exactly as they appear” 以明確要求保留所有數值與貨幣符號 |
| **`free_resources` 拋出例外** | 使用較舊的 Aspose OCR 版本 | 升級至最新的 `aspose-ocr` 套件 (pip install --upgrade aspose-ocr) |

## 完整範例回顧

以下再次提供腳本，並加入說明每一行的內嵌註解，供日後參考：

```python
import aspose.ocr as aocr
from aspose.ocr.ai import AsposeAI, AsposeAIModelConfig

# 1️⃣ Configure AI – will auto‑download the model if needed
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20,                     # adjust based on your GPU size
    directory_model_path=r"YOUR_DIRECTORY/Models"
)
ai = AsposeAI(ai_config)               # initialise the engine

# 2️⃣ Run classic OCR on an image (or PDF)
ocr_engine = aocr.OcrEngine()
ocr_engine.load_image(r"YOUR_DIRECTORY/invoice.png")
raw_text = ocr_engine.recognize()      # plain‑text result

# 3️⃣ Define a prompt that tells the LLM to keep numbers intact
def financial_prompt():
    return {"prompt": "Correct OCR errors, keep numbers and currency symbols intact"}

ai.set_post_processor("llm_correction", financial_prompt)

# 4️⃣ Let the LLM clean the text
corrected_text = ai.run_postprocessor(raw_text)

# 5️⃣ Show before/after
print("Original :", raw_text)
print("Enhanced :", corrected_text)

# 6️⃣ Clean up – this frees GPU memory for the next run
ai.free_resources()
```

## 結論

我們已說明如何使用 Aspose **how to run OCR**、按需下載 Hugging Face 模型、設計能 **corrects OCR errors** 的提示詞，並最終 **free gpu memory**，讓你的工作站保持回應。整個流程僅需一個獨立的 Python 檔案——不需外部腳本、手動模型管理，也不會留下 GPU 記憶體佔用。  

接下來的步驟？試著將 `financial_prompt` 換成其他用途的提示詞，例如  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}