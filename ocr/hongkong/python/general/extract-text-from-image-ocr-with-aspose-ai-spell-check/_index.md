---
category: general
date: 2026-05-03
description: 使用 Aspose OCR 與 AI 拼寫檢查從圖片提取文字。了解如何對圖片進行 OCR、載入圖片以進行 OCR、從發票中辨識文字以及釋放
  GPU 資源。
draft: false
keywords:
- extract text from image
- how to ocr image
- load image for ocr
- release gpu resources
- recognize text from invoice
language: zh-hant
og_description: 使用 Aspose OCR 與 AI 拼寫檢查從圖片提取文字。逐步指南，涵蓋如何對圖片進行 OCR、載入圖片以進行 OCR，以及釋放
  GPU 資源。
og_title: 從圖片提取文字 – 完整 OCR 與拼寫檢查指南
tags:
- OCR
- Aspose
- AI
- Python
title: 從圖片提取文字 – 結合 Aspose AI 拼寫檢查的 OCR
url: /zh-hant/python/general/extract-text-from-image-ocr-with-aspose-ai-spell-check/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從圖像提取文字 – 完整 OCR 與拼寫檢查指南

是否曾需要 **從圖像提取文字**，卻不確定哪個函式庫能同時提供速度與準確度？你並不孤單。在許多實務專案中——例如發票處理、收據數位化或合約掃描——從圖片取得乾淨、可搜尋的文字是第一道關卡。

好消息是，Aspose OCR 搭配輕量級的 Aspose AI 模型，只需幾行 Python 程式碼即可完成這項工作。在本教學中，我們將一步步說明 **如何 OCR 圖像**、正確載入圖片、執行內建的拼寫檢查後處理，最後 **釋放 GPU 資源**，讓你的應用程式保持記憶體友好。

閱讀完本指南後，你將能 **辨識發票圖像中的文字**、自動校正常見的 OCR 錯誤，並在下一批次處理前保持 GPU 整潔。

---

## 需要的環境

- Python 3.9 或更新版本（程式碼使用型別提示，但在較早的 3.x 版本亦可執行）
- `aspose-ocr` 與 `aspose-ai` 套件（透過 `pip install aspose-ocr aspose-ai` 安裝）
- 支援 CUDA 的 GPU 為可選項目；若未偵測到 GPU，腳本會自動回退至 CPU。
- 範例圖片，例如 `sample_invoice.png`，放置於可參照的資料夾中。

不需要大型機器學習框架，也不需要龐大的模型下載——只要一個小型的 Q4‑K‑M 量化模型，即可在大多數 GPU 上順暢運行。

---

## 第一步：初始化 OCR 引擎 – 從圖像提取文字

首先建立 `OcrEngine` 實例，並告訴它預期的語言。此處選擇英文，並要求純文字輸出，這對後續處理最為理想。

```python
import aocr  # Aspose OCR package
import aspose.ai as ai  # Aspose AI package

# Initialise the OCR engine
ocr_engine = aocr.OcrEngine()
ocr_engine.language = aocr.Language.English            # Choose any supported language
ocr_engine.recognize_mode = aocr.RecognitionMode.Plain  # Plain text makes post‑processing easier
```

**為什麼這很重要：** 設定語言會縮小字元集，提升辨識準確度。純文字模式會去除版面資訊，當你只想從圖像提取文字時，這正是你需要的。

---

## 第二步：載入圖像以供 OCR – 如何 OCR 圖像

接著將實際的圖片提供給引擎。`Image.load` 輔助函式支援常見格式（PNG、JPEG、TIFF），並抽象化檔案 I/O 的細節。

```python
# Load the input image – this is the "load image for OCR" step
input_image = aocr.Image.load("YOUR_DIRECTORY/sample_invoice.png")
raw_text = ocr_engine.recognize(input_image)  # Returns the recognised text as a string
```

**小技巧：** 若來源圖片尺寸過大，建議先將其縮小後再送入引擎；較小的尺寸可減少 GPU 記憶體使用，同時不會明顯影響辨識品質。

---

## 第三步：設定 Aspose AI 模型 – 辨識發票文字

Aspose AI 內建一個可自動下載的微型 GGUF 模型。範例使用 `Qwen2.5‑3B‑Instruct‑GGUF` 儲存庫，量化為 `q4_k_m`。我們同時指示執行環境在 GPU 上配置 20 層，以在速度與 VRAM 使用之間取得平衡。

```python
# Model configuration – auto‑download a small Q4‑K‑M quantised model
model_config = ai.AsposeAIModelConfig()
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "bartowski/Qwen2.5-3B-Instruct-GGUF"
model_config.hugging_face_quantization = "q4_k_m"
model_config.gpu_layers = 20  # Use 20 GPU layers when a GPU is available
```

**背後原理：** 量化模型在磁碟上約 1.5 GB，遠小於完整精度模型，卻仍保有足夠的語言細節，足以偵測典型的 OCR 拼寫錯誤。

---

## 第四步：初始化 AsposeAI 並掛載拼寫檢查後處理器

Aspose AI 內建即用的拼寫檢查後處理器。將它掛上後，所有 OCR 結果都會自動被清理。

```python
# Initialise AsposeAI and attach the built‑in spell‑check post‑processor
ocr_ai = ai.AsposeAI(model_config)  # Pass the config we just built
ocr_ai.set_post_processor(ocr_ai.postprocessor_spell_check, {})  # Empty dict → default settings
```

**為什麼要使用後處理器？** OCR 引擎常把 “Invoice” 誤讀為 “Invo1ce”，或把 “Total” 誤讀為 “T0tal”。拼寫檢查會使用輕量語言模型對原始字串進行校正，無需自行編寫字典。

---

## 第五步：對 OCR 結果執行拼寫檢查後處理器

所有設定完成後，只要一次呼叫即可取得校正後的文字。我們同時印出原始與清理過的版本，讓你直觀比較改進效果。

```python
# Run the spell‑check post‑processor on the OCR result
corrected_text = ocr_ai.run_postprocessor(raw_text)

print("Original :", raw_text)
print("Corrected:", corrected_text)
```

發票的典型輸出可能如下所示：

```
Original : Invo1ce #12345
Date: 2023/07/15
Total: $1,250.00
...
Corrected: Invoice #12345
Date: 2023/07/15
Total: $1,250.00
...
```

可見 “Invo1ce” 已被正確轉換為 “Invoice”。這就是內建 AI 拼寫檢查的威力。

---

## 第六步：釋放 GPU 資源 – 安全釋放 GPU 資源

如果你在長時間執行的服務（例如每分鐘處理數十張發票的 Web API）中使用此腳本，必須在每個批次後釋放 GPU 上下文，否則會出現記憶體洩漏，最終導致 “CUDA out of memory” 錯誤。

```python
# Release GPU resources – crucial to avoid memory leaks
ocr_ai.free_resources()
```

**專業提示：** 在 `finally` 區塊或 context manager 中呼叫 `free_resources()`，確保即使發生例外也能執行釋放。

---

## 完整範例程式

將上述所有片段組合，即可得到一個可直接放入任何專案的獨立腳本。

```python
# extract_text_from_image.py
import aocr
import aspose.ai as ai

def main():
    # Step 1: Initialise OCR engine
    ocr_engine = aocr.OcrEngine()
    ocr_engine.language = aocr.Language.English
    ocr_engine.recognize_mode = aocr.RecognitionMode.Plain

    # Step 2: Load image for OCR
    input_image = aocr.Image.load("YOUR_DIRECTORY/sample_invoice.png")
    raw_text = ocr_engine.recognize(input_image)

    # Step 3: Configure Aspose AI model
    model_cfg = ai.AsposeAIModelConfig()
    model_cfg.allow_auto_download = "true"
    model_cfg.hugging_face_repo_id = "bartowski/Qwen2.5-3B-Instruct-GGUF"
    model_cfg.hugging_face_quantization = "q4_k_m"
    model_cfg.gpu_layers = 20

    # Step 4: Initialise AI and attach spell‑check
    ocr_ai = ai.AsposeAI(model_cfg)
    ocr_ai.set_post_processor(ocr_ai.postprocessor_spell_check, {})

    # Step 5: Run spell‑check
    corrected_text = ocr_ai.run_postprocessor(raw_text)

    print("Original :", raw_text)
    print("Corrected:", corrected_text)

    # Step 6: Release GPU resources
    ocr_ai.free_resources()

if __name__ == "__main__":
    main()
```

將檔案儲存、調整圖片路徑，然後執行 `python extract_text_from_image.py`。你應該會在主控台看到已清理的發票文字。

---

## 常見問題 (FAQ)

**Q: 這能在只有 CPU 的機器上執行嗎？**  
A: 完全可以。若未偵測到 GPU，Aspose AI 會自動回退至 CPU 執行，雖然速度較慢。你也可以透過設定 `model_cfg.gpu_layers = 0` 強制使用 CPU。

**Q: 若我的發票使用非英文語言，該怎麼辦？**  
A: 將 `ocr_engine.language` 改為相應的列舉值（例如 `aocr.Language.Spanish`）。拼寫檢查模型支援多語言，但使用針對特定語言的模型可能會得到更佳結果。

**Q: 能否在迴圈中處理多張圖片？**  
A: 可以。只要把載入、辨識與後處理步驟放入 `for` 迴圈即可。若重複使用同一個 AI 實例，別忘了在迴圈結束或每個批次後呼叫 `ocr_ai.free_resources()`。

**Q: 模型下載大小是多少？**  
A: 量化的 `q4_k_m` 版本約 1.5 GB。首次執行後會快取於本機，之後的執行即時完成。

---

## 結論

本教學示範了如何使用 Aspose OCR **從圖像提取文字**、設定微型 AI 模型、套用拼寫檢查後處理器，並安全 **釋放 GPU 資源**。整個流程涵蓋從載入圖片到清理資源的全部步驟，為 **辨識發票文字** 場景提供可靠的管線。

接下來的步驟？可以嘗試將拼寫檢查換成自訂的實體抽取模型。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}