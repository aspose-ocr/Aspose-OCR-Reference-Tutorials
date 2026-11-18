---
category: general
date: 2026-03-26
description: 使用 Aspose OCR 將圖片轉換為文字，並以 Python 方式清理 OCR 文字。了解如何在單一腳本中提取圖片文字並進行後處理。
draft: false
keywords:
- convert image to text
- how to extract image text
- clean ocr text python
- Aspose OCR Python
- AI spell‑checker Python
- post‑process OCR output
language: zh-hant
og_description: 快速將圖像轉換為文字。本指南示範如何使用 Aspose OCR 及 AI 拼寫檢查器，以 Python 風格提取圖像文字並清理 OCR
  文本。
og_title: 使用 Python 將圖像轉換為文字 – 完整教學
tags:
- OCR
- Python
- Aspose
- AI
title: 使用 Python 將圖像轉換為文字 – 完整逐步指南
url: /zh-hant/python/general/convert-image-to-text-with-python-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 將圖像轉換為文字 – 完整 Python 教程

是否曾經需要 **將圖像轉換為文字**，卻總是得到雜亂的結果？你並不孤單。許多開發者在 OCR 輸出充斥拼寫錯誤、雜散符號或錯誤換行時卡住了。好消息是，只需幾行 Python 以及 Aspose OCR，你就能從任何圖像中提取直接的文字 **並** 自動清理它。

在本指南中，我們將示範 **如何提取圖像文字**，然後運行 AI 驅動的拼寫檢查器，以產生精緻、易讀的內容。最後，你將擁有一個從 PNG 檔案直接產生乾淨 `.txt` 檔案的單一腳本——無需手動複製貼上。

> **你將學會**  
> * 安裝並設定 Aspose OCR。  
> * 從圖像檔案辨識文字。  
> * 初始化 Aspose AI 模型以進行拼寫檢查。  
> * 套用後處理器整理 OCR 輸出。  
> * 儲存最終結果並釋放資源。  

所有這些都以 **clean OCR text python** 風格運作——意味著程式碼可直接嵌入任何專案，無需額外包裝。

## 前置條件

在深入之前，請確保你已具備以下條件：

| 需求 | 原因說明 |
|-------------|----------------|
| Python 3.9 or newer | 現代語法與型別提示 |
| `asposeocr` package (`pip install asposeocr`) | 核心 OCR 引擎 |
| Internet access (first run) | 模型自動從 Hugging Face 下載 |
| A PNG/JPEG image you want to read | 輸入來源 |

不需要 GPU，但若有 GPU，AI 模型會自動使用它以加速拼寫檢查。

## 步驟 1：使用 Aspose OCR 將圖像轉換為文字

我們首先需要的是可靠的 OCR 引擎。Aspose OCR 是商業函式庫，但提供慷慨的免費開發層級。以下我們會初始化引擎、將語言設定為英語，並啟用 auto‑skew 校正以處理傾斜掃描。

```python
import asposeocr as ocr

# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.English   # English language pack
ocr_engine.auto_skew = True                  # Auto‑deskew images
```

> **為何啟用 `auto_skew`？**  
> 許多掃描文件並非完全平整。Auto‑skew 會將圖像旋轉適當角度，以提升字符辨識率，進而減少日後需要清理的錯亂文字數量。

現在我們將圖像檔案輸入引擎：

```python
# Recognise text from the input image (replace with your own path)
ocr_result = ocr_engine.recognize_image("YOUR_DIRECTORY/input_image.png")
print("Raw OCR output:")
print(ocr_result.text[:200])  # Show first 200 characters for sanity check
```

`ocr_result.text` 屬性包含從圖片中提取的原始字串。此時你可能會注意到雜散的標點、換行怪異，甚至少量拼寫錯誤——正是我們想要解決的問題。

![convert image to text workflow](image.png){alt="將圖像轉換為文字工作流程圖"}

## 步驟 2：設定 AI 拼寫檢查器（Clean OCR Text Python）

清理 OCR 輸出可以簡單到只使用正則表達式取代，但若要真正可讀的文字，我們將使用 Aspose AI 搭配專門用於拼寫檢查的輕量 LLM。模型會在首次執行腳本時從 Hugging Face 下載，無需手動下載任何檔案。

```python
from asposeocr import AsposeAI, AsposeAIModelConfig

# Model configuration – auto‑download enabled
model_cfg = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="bartowski/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=30                # Use GPU if available, otherwise CPU fallback
)

# Initialise the AI spell‑checker
spell_checker = AsposeAI()
spell_checker.initialize(model_cfg)
spell_checker.set_post_processor("spell_check")
```

**為何選擇此模型？**  
`Qwen2.5‑3B‑Instruct‑GGUF` 是一個緊湊的 30 億參數指令微調模型，能在筆記型電腦 GPU（甚至使用 int8 量化的 CPU）上順暢運行。它足夠快速，可逐行執行拼寫檢查而不會耗盡記憶體。

## 步驟 3：對 OCR 輸出套用拼寫檢查

取得 OCR 文字且 AI 模型已就緒後，我們只需將原始字串送入後處理器。此方法會回傳已清理的版本，你可以直接寫入磁碟。

```python
# Run the spell‑checking post‑processor
corrected_text = spell_checker.run_postprocessor(ocr_result.text)

print("\nCleaned OCR output (first 200 chars):")
print(corrected_text[:200])
```

你會看到的典型改進包括：

* “teh” → “the”  
* “recieve” → “receive”  
* 標點符號後缺少空格 – 自動修正  
* 奇怪的換行被轉換為正確的句子  

如果需要更細緻的控制，你可以將自訂提示傳遞給 `run_postprocessor`，但預設的 “spell_check” 預設值已能滿足大多數情況。

## 步驟 4：將清理後的文字儲存至檔案

現在文字已整潔，我們將其持久化。使用 UTF‑8 可確保任何特殊字元（例如帶重音的字母）得以保留。

```python
output_path = "YOUR_DIRECTORY/output_text.txt"

with open(output_path, "w", encoding="utf-8") as out_file:
    out_file.write(corrected_text)

print(f"\n✅ Processing complete: input_image.png → {output_path}")
```

你可以在任何編輯器中開啟此檔案，會看到一份人類可讀的文件，已準備好進行後續處理——無論是餵入語言模型、建立搜尋索引，或僅僅作為存檔。

## 步驟 5：釋放 AI 資源（良好維護）

Aspose AI 會在記憶體中保留模型權重。完成後釋放它們可防止記憶體洩漏，尤其在長時間執行的服務中。

```python
spell_checker.free_resources()
```

就這樣！整個管線——從圖像到乾淨文字——只需不到 30 行 Python 程式碼。

## 常見問題與邊緣情況

### 如果圖像不是英文呢？

將 `ocr_engine.language` 設為相應的列舉，例如 `ocr.Language.French`。拼寫檢查模型對基本拼寫是語言無關的，但若要取得最佳效果，可能需要多語言模型。

### 我的 GPU 只有 20 層——還能使用此模型嗎？

當然可以。只需將 `gpu_layers` 降至 `20`（或設定為 `0` 以純 CPU 使用）。函式庫會自動在剩餘層數上回退至 CPU。

### 在公司代理伺服器下模型下載失敗？

在執行腳本前，透過環境變數 (`HTTP_PROXY`, `HTTPS_PROXY`) 傳遞代理設定。下載程序會遵守這些設定。

### 我只需要快速的正則表達式清理，而不是 AI？

你可以跳過 AI 步驟，直接執行簡單的清理：

```python
import re
clean = re.sub(r'\s+', ' ', ocr_result.text).strip()
```

但請記住，正則表達式無法修正真正的拼寫錯誤——這需要 AI 來完成。

## 完整可執行腳本

以下是完整、可直接執行的腳本。將 `YOUR_DIRECTORY` 替換為存放圖像及欲輸出檔案的資料夾路徑。

```python
import asposeocr as ocr
from asposeocr import AsposeAI, AsposeAIModelConfig

# -------------------------------------------------
# Step 1 – Initialise OCR engine
# -------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.English
ocr_engine.auto_skew = True

# -------------------------------------------------
# Step 2 – Recognise text from image
# -------------------------------------------------
ocr_result = ocr_engine.recognize_image("YOUR_DIRECTORY/input_image.png")
print("Raw OCR (first 200 chars):")
print(ocr_result.text[:200])

# -------------------------------------------------
# Step 3 – Configure AI spell‑checker
# -------------------------------------------------
model_cfg = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="bartowski/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=30
)

spell_checker = AsposeAI()
spell_checker.initialize(model_cfg)
spell_checker.set_post_processor("spell_check")

# -------------------------------------------------
# Step 4 – Clean the OCR output
# -------------------------------------------------
corrected_text = spell_checker.run_postprocessor(ocr_result.text)
print("\nCleaned OCR (first 200 chars):")
print(corrected_text[:200])

# -------------------------------------------------
# Step 5 – Write to file
# -------------------------------------------------
output_path = "YOUR_DIRECTORY/output_text.txt"
with open(output_path, "w", encoding="utf-8") as out_file:
    out_file.write(corrected_text)

print(f"\nProcessing complete: input_image.png → {output_path}")

# -------------------------------------------------
# Step 6 – Free AI resources
# -------------------------------------------------
spell_checker.free_resources()
```

執行此腳本將產生 `output_text.txt`，其中包含圖像的精緻文字轉錄。

## 結論

我們剛剛示範了使用 Aspose OCR **將圖像轉換為文字**，再以 **clean OCR text python** 風格搭配 AI 拼寫檢查器進行清理的實用方法。此解決方案自成一體，只需單一 Python 檔案，即可在 Windows、macOS 或 Linux 上運作。

如果你想進一步，請考慮：

* **如何從 PDF 提取圖像文字**，先將頁面轉換為圖像。  
* 將清理後的文字餵入摘要模型，以自動生成報告。  
* 將結果儲存於向量資料庫，以進行語意搜尋。

試試看，調整模型參數，讓 OCR‑to‑text 管線成為你資料攝取工具箱的必備利器。祝編程愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}