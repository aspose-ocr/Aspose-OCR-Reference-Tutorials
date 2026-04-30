---
category: general
date: 2026-04-29
description: 使用 Python 對圖像執行 OCR，自動下載 HuggingFace 模型，並在清理 OCR 文字的同時有效釋放 GPU 記憶體。
draft: false
keywords:
- perform OCR on image
- download HuggingFace model python
- release GPU memory python
- clean OCR text python
language: zh-hant
og_description: 學習如何在 Python 中對影像執行 OCR、自动下載 HuggingFace 模型、清理文字並釋放 GPU 記憶體。
og_title: 使用 Python 對圖像執行 OCR – 逐步指南
tags:
- OCR
- Python
- Aspose
- HuggingFace
title: 使用 Python 進行圖像 OCR – 完整指南
url: /zh-hant/python/general/perform-ocr-on-image-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Python 中對圖像執行 OCR – 完整指南

是否曾需要**對圖像執行 OCR**但在模型下載或 GPU 記憶體清理階段卡住？你並非唯一——許多開發者在首次嘗試將光學字符識別與大型語言模型結合時都會碰到這個問題。  

在本教學中，我們將逐步說明一個完整的端到端解決方案，該方案**在 Python 中下載 HuggingFace 模型**、執行 Aspose OCR、清理原始輸出，最後**釋放 Python 可回收的 GPU 記憶體**。完成後，你將擁有一個可直接執行的腳本，將掃描的 PNG 轉換為精緻且可搜尋的文字。

> **你將獲得：** 完整、可執行的程式碼範例、每個步驟重要性的說明、避免常見陷阱的技巧，以及如何為自己的專案微調管線的概覽。

---

## 需求環境

- Python 3.9 或更新版本（範例在 3.11 上測試）  
- `aspose-ocr` 套件（透過 `pip install aspose-ocr` 安裝）  
- 需要網路連線以下載 **在 Python 中下載 HuggingFace 模型** 步驟  
- 如果想要加速，請使用相容 CUDA 的 GPU（非必須但建議）  

不需要額外的系統層級相依性；Aspose OCR 引擎已捆綁所有必要的元件。

![對圖像執行 OCR 範例](image.png "使用 Aspose OCR 與 LLM 後處理器執行 OCR 的範例")

*圖片說明文字：“對圖像執行 OCR – Aspose OCR 在 AI 清理前後的輸出”*

---

## 執行 OCR 步驟概覽

以下我們將工作流程拆分為邏輯區塊。每個區塊都有自己的標題，讓 AI 助手能快速跳至你感興趣的部分，搜尋引擎也能索引相關關鍵字。

### 1. 在 Python 中下載 HuggingFace 模型

我們首先需要取得一個語言模型，作為原始 OCR 輸出的後處理器。Aspose OCR 附帶一個名為 `AsposeAI` 的輔助類別，能自動從 HuggingFace hub 下載模型。

```python
import aspose.ocr as aocr
from aspose.ocr import AsposeAI, AsposeAIModelConfig, OcrEngine

# Configure the model – it will auto‑download the first time you run it
model_config = AsposeAIModelConfig(
    allow_auto_download="true",                     # <-- enables auto‑download
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",               # smaller footprint on GPU
    gpu_layers=20,                                  # how many layers stay on GPU
    directory_model_path=r"YOUR_DIRECTORY"         # where the model files live
)
```

**為什麼這很重要：**  
- **在 Python 中下載 HuggingFace 模型** – 你可以避免手動處理 zip 檔或令牌驗證。  
- 使用 `int8` 量化可將模型縮減至原始大小約四分之一，這在之後需要**釋放 Python GPU 記憶體**時至關重要。

> **專業提示：** 將 `directory_model_path` 放在 SSD 上以加快載入速度。  

---

### 2. 初始化 AI 輔助工具並啟用拼寫檢查

現在我們建立 `AsposeAI` 實例並附加拼寫校正後處理器。這就是 **在 Python 中清理 OCR 文字** 魔法的開始。

```python
# Initialise the AI helper
ai_helper = AsposeAI()
ai_helper.set_post_processor(
    processor="spell_corrector",
    custom_settings={"max_edits": 2}   # allows up to two character edits per word
)
```

**說明：**  
拼寫校正器會檢查 OCR 引擎的每個 token，並根據 `max_edits` 提出編輯建議。這個小調整即可將 “rec0gn1tion” 轉為 “recognition”，而不需要大型語言模型。

---

### 3. 將 AI 輔助工具掛接至 OCR 引擎

Aspose 在 23.4 版中引入了一個新方法，允許你直接將 AI 引擎插入 OCR 流程。

```python
# Initialise the OCR engine and attach the AI helper
ocr_engine = OcrEngine()
ocr_engine.set_ai_engine(ai_helper)   # new in v23.4
```

**為什麼這麼做：**  
提前接入 AI 輔助工具後，OCR 引擎可以選擇性地使用模型進行即時改進（例如版面偵測）。同時保持程式碼整潔——之後不需要額外的後處理迴圈。

---

### 4. 對掃描圖像執行 OCR

以下是實際**對圖像執行 OCR**的核心步驟。將 `YOUR_DIRECTORY/input.png` 替換為你自己的掃描檔案路徑。

```python
image_path = r"YOUR_DIRECTORY/input.png"
ocr_result = ocr_engine.recognize(image_path)

print("Raw OCR text:")
print(ocr_result.text)
```

典型的原始輸出可能在奇怪的位置出現換行、錯誤辨識的字元或雜散符號。這就是為什麼需要下一步。

**預期的原始輸出（範例）：**

```
Th1s 1s 4n ex4mpl3 0f r4w OCR t3xt.
It c0ntains numb3rs 123 and s0me m1stakes.
```

---

### 5. 使用 AI 後處理器在 Python 中清理 OCR 文字

現在讓 AI 清理這些雜訊。這就是 **在 Python 中清理 OCR 文字** 流程的核心。

```python
cleaned_result = ocr_engine.run_postprocessor(ocr_result)

print("\nAI‑enhanced text:")
print(cleaned_result.text)
```

**你將看到的結果：**

```
This is an example of raw OCR text.
It contains numbers 123 and some mistakes.
```

請注意拼寫校正器將 “Th1s” 修正為 “This”，並移除雜散的 “4n”。模型同時會正規化空格，這在之後將文字輸入下游 NLP 流程時常是個痛點。

---

### 6. 在 Python 中釋放 GPU 記憶體 – 清理步驟

完成後，釋放 GPU 資源是良好實踐，特別是當你在長時間服務中執行多個 OCR 任務時。

```python
# Release resources – crucial for GPU memory
ai_helper.free_resources()
ocr_engine.dispose()
```

**背後發生的事：**  
`free_resources()` 從 GPU 卸載模型，將記憶體歸還給 CUDA 驅動程式。`dispose()` 關閉 OCR 引擎的內部緩衝區。若省略這些呼叫，僅在處理少量圖像後就可能出現記憶體不足錯誤。

> **請記住：** 若打算在迴圈中批次處理，請在每個批次後呼叫清理，或在最後才釋放 `ai_helper`，以避免過早釋放。

---

## 加分項：為不同情境微調管線

### 調整模型量化

如果你擁有強大的 GPU（例如 RTX 4090）且想要更高的準確度，請將 `hugging_face_quantization` 改為 `"fp16"`，並將 `gpu_layers` 提升至 `30`。這會消耗更多記憶體，因此需要在每個批次後更積極地**釋放 Python GPU 記憶體**。

### 使用自訂拼寫檢查器

你可以將內建的 `spell_corrector` 替換為自訂的後處理器，以執行領域特定的校正（例如醫學術語）。只需實作所需介面，並將其名稱傳遞給 `set_post_processor` 即可。

### 批次處理多張圖像

將 OCR 步驟包在 `for` 迴圈中，將 `cleaned_result.text` 收集到列表，若 GPU 記憶體足夠，則僅在迴圈結束後呼叫 `ai_helper.free_resources()`。這可減少重複載入模型的開銷。

---

## 結論

我們剛剛示範了如何在 Python 中**對圖像執行 OCR**，自動**下載 HuggingFace 模型**、**清理 OCR 文字**，並在完成後安全**釋放 GPU 記憶體**。完整腳本已可直接複製貼上，說明則提供了將其套用至更大型專案的信心。

接下來的步驟？嘗試將 Qwen 2.5 模型換成更大的 LLaMA 變種，實驗不同的後處理器，或將清理後的輸出整合至可搜尋的 Elasticsearch 索引。可能性無窮，而你已擁有堅實的基礎可供構建。

祝編程愉快，願你的 OCR 管線永遠乾淨且記憶體友好！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}