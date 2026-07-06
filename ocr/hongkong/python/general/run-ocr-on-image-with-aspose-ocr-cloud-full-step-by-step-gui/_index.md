---
category: general
date: 2026-03-28
description: 學習如何在圖像上執行 OCR、自動下載 Hugging Face 模型、清理 OCR 文字，並使用 Aspose OCR Cloud 在
  Python 中配置 LLM 模型。
draft: false
keywords:
- run OCR on image
- download hugging face model
- clean OCR text
- configure LLM model
language: zh-hant
og_description: 在圖像上執行 OCR，並使用自動下載的 Hugging Face 模型清理輸出。本指南說明如何在 Python 中設定 LLM 模型。
og_title: 在圖像上執行 OCR – 完整的 Aspose OCR 雲端教學
tags:
- OCR
- Python
- LLM
- HuggingFace
title: 使用 Aspose OCR Cloud 於圖片執行 OCR – 完整逐步指南
url: /zh-hant/python/general/run-ocr-on-image-with-aspose-ocr-cloud-full-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在圖像上執行 OCR – 完整 Aspose OCR Cloud 教程

有沒有遇過要在圖像檔案上執行 OCR，但原始輸出卻像是一團亂碼？依我之見，最大的痛點其實不是辨識本身，而是後續的清理。幸好，Aspose OCR Cloud 允許你掛接一個 LLM 後處理器，能自動 *清理 OCR 文字*。在本教學中，我們會一步步帶你完成：從 **下載 Hugging Face 模型**、設定 LLM、執行 OCR 引擎，到最後拋光結果。

完成本指南後，你將擁有一個即時可執行的腳本，具備以下功能：

1. 從 Hugging Face 取得緊湊的 Qwen 2.5 模型（會自動下載）。  
2. 設定模型在 GPU 上執行部分網路層，剩餘部分在 CPU 上執行。  
3. 在手寫筆記圖像上執行 OCR 引擎。  
4. 使用 LLM 清理辨識出的文字，產生人類可讀的輸出。

> **先決條件** – Python 3.8+、`asposeocrcloud` 套件、具備至少 4 GB VRAM 的 GPU（非必要但建議），以及首次下載模型時需要的網路連線。

---

## 你需要的東西

- **Aspose OCR Cloud SDK** – 透過 `pip install asposeocrcloud` 安裝。  
- **範例圖像** – 例如 `handwritten_note.jpg`，放在本機資料夾內。  
- **GPU 支援** – 若有支援 CUDA 的 GPU，腳本會將 30 個層級卸載至 GPU；否則會自動回退至 CPU。  
- **寫入權限** – 腳本會將模型快取於 `YOUR_DIRECTORY`，請確保該資料夾已存在。

---

## 第一步 – 設定 LLM 模型（下載 Hugging Face 模型）

首先，我們要告訴 Aspose AI 從哪裡取得模型。`AsposeAIModelConfig` 類別負責自動下載、量化以及 GPU 層級分配。

```python
import asposeocrcloud as ocr
from asposeocrcloud.ai import AsposeAI, AsposeAIModelConfig

# ----------------------------------------------------------------------
# Step 1: Model configuration – this will download the model if it’s missing
# ----------------------------------------------------------------------
model_config = AsposeAIModelConfig(
    allow_auto_download="true",                           # Enables auto‑download
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF", # Repo on Hugging Face
    hugging_face_quantization="int8",                     # Small footprint, fast inference
    gpu_layers=30,                                        # 30 layers on GPU, rest on CPU
    directory_model_path=r"YOUR_DIRECTORY"               # Cache folder (optional)
)
```

**為什麼這很重要** – 量化為 `int8` 能大幅減少記憶體使用（約 4 GB 對比 12 GB）。將模型分割至 GPU 與 CPU，可讓 30 億參數的 LLM 在一般的 RTX 3060 上也能運行。若沒有 GPU，將 `gpu_layers=0`，SDK 會全部在 CPU 上執行。

> **小技巧**：首次執行會下載約 1.5 GB，請預留幾分鐘並確保網路穩定。

---

## 第二步 – 使用模型設定初始化 AI 引擎

接著，我們啟動 Aspose AI 引擎，並將剛剛建立的設定傳入。

```python
# ----------------------------------------------------------------------
# Step 2: Initialise the AI engine – pulls the model if needed
# ----------------------------------------------------------------------
ocr_ai = AsposeAI()
ocr_ai.initialize(model_config)  # This call blocks until the model is ready
```

**背後發生了什麼**？SDK 會檢查 `directory_model_path` 是否已有模型。若找到相符版本，會立即載入；否則會從 Hugging Face 下載 GGUF 檔案、解壓縮，並建構推論管線。

---

## 第三步 – 建立 OCR 引擎並掛接 AI 後處理器

OCR 引擎負責執行文字辨識。掛接 `ocr_ai.run_postprocessor` 後，辨識完成即會自動執行 **清理 OCR 文字**。

```python
# ----------------------------------------------------------------------
# Step 3: Build the OCR engine and bind the LLM post‑processor
# ----------------------------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.set_post_processor(ocr_ai.run_postprocessor, custom_settings=None)
```

**為什麼要使用後處理器？** 原始 OCR 常會出現錯位的換行、誤判的標點或多餘的符號。LLM 能將輸出改寫成完整句子、校正拼寫，甚至推測遺漏的字詞，等於把雜亂的資料轉變為潤飾過的文章。

---

## 第四步 – 在圖像檔案上執行 OCR

所有元件已串接完成，現在把圖像送入引擎吧。

```python
# ----------------------------------------------------------------------
# Step 4: Load the image and run OCR
# ----------------------------------------------------------------------
input_image = ocr.Image.load(r"YOUR_DIRECTORY/handwritten_note.jpg")
raw_result = ocr_engine.recognize(input_image)   # Returns an OcrResult object
```

**邊緣情況**：若圖像過大（> 5 MP），建議先縮小以加速處理。SDK 接受 Pillow 的 `Image` 物件，你可以先用 `PIL.Image.thumbnail()` 進行前置處理。

---

## 第五步 – 讓 AI 清理辨識文字，並同時顯示前後兩版

最後，我們呼叫先前掛接的後處理器。此步驟會展示清理前後的差異。

```python
# ----------------------------------------------------------------------
# Step 5: Clean the OCR output using the LLM and display both results
# ----------------------------------------------------------------------
cleaned_result = ocr_engine.run_postprocessor(raw_result)

print("=== Before AI ===")
print(raw_result.text)

print("\n=== After AI ===")
print(cleaned_result.text)
```

### 預期輸出

```
=== Before AI ===
Th1s 1s a h@ndwr1tt3n n0te.  It c0nta1ns m1st@k3s, l1n3 br3aks, & sp3c!@l ch@r@ct3rs.

=== After AI ===
This is a handwritten note. It contains mistakes, line breaks, and special characters.
```

可以看到 LLM 已經：

- 修正常見的 OCR 誤認（`Th1s` → `This`）。  
- 移除多餘符號（`&` → `and`）。  
- 將換行正規化為完整句子。

---

## 🎨 視覺概覽（在圖像上執行 OCR 工作流程）

![在圖像上執行 OCR 工作流程](run_ocr_on_image_workflow.png "示意圖顯示從模型下載到清理輸出的在圖像上執行 OCR 流程")

上圖概括了完整管線：**下載 Hugging Face 模型 → 設定 LLM → 初始化 AI → OCR 引擎 → AI 後處理器 → 清理 OCR 文字**。

---

## 常見問題與專業小技巧

### 沒有 GPU 該怎麼辦？

在 `AsposeAIModelConfig` 中將 `gpu_layers=0`。模型會全程在 CPU 上執行，雖然較慢但仍可使用。你也可以改用較小的模型（例如 `Qwen/Qwen2.5-1.5B‑Instruct‑GGUF`），以維持合理的推論時間。

### 想之後更換模型要怎麼做？

只要更新 `hugging_face_repo_id` 後重新執行 `ocr_ai.initialize(model_config)`。SDK 會偵測版本變更、下載新模型，並取代快取檔案。

### 可以自訂後處理器的提示語嗎？

可以。將字典傳入 `custom_settings`，其中包含 `prompt_template` 鍵。例如：

```python
custom_prompt = {
    "prompt_template": "Correct the following OCR text and keep line breaks:\n{ocr_text}"
}
ocr_engine.set_post_processor(ocr_ai.run_postprocessor, custom_settings=custom_prompt)
```

### 要把清理後的文字寫入檔案嗎？

一定要。清理完畢後，你可以將結果寫入 `.txt` 或 `.json` 檔，以供後續處理：

```python
with open("cleaned_note.txt", "w", encoding="utf-8") as f:
    f.write(cleaned_result.text)
```

---

## 結論

我們已示範如何使用 Aspose OCR Cloud **在圖像上執行 OCR**，自動 **下載 Hugging Face 模型**、精細 **設定 LLM 模型**，最後透過強大的 LLM 後處理器 **清理 OCR 文字**。整個流程只需一個簡易的 Python 腳本，且同時支援 GPU 與純 CPU 環境。

如果你對此管線已熟悉，可進一步嘗試：

- **不同 LLM** – 如 `meta-llama/Meta-Llama-3-8B‑Instruct‑GGUF`，以取得更大的上下文視窗。  
- **批次處理** – 迴圈遍歷資料夾內多張圖像，將清理結果匯總至 CSV。  
- **自訂提示** – 針對特定領域（法律文件、醫療筆記等）調整 AI 行為。

隨意調整 `gpu_layers` 數值、替換模型，或套用自己的提示語。未來的可能性無限，而你現在手上的程式碼，就是起飛的發射台。

祝開發順利，願你的 OCR 輸出永遠乾淨！ 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}