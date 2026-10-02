---
category: general
date: 2026-01-12
description: 如何使用 Aspose OCR 以及輕量級 Hugging Face 模型對發票圖像執行 OCR 並提取文字。學習下載模型、校正 OCR
  錯誤，以及對圖像進行 OCR。
draft: false
keywords:
- how to run OCR
- extract text from invoice
- download hugging face model
- correct OCR errors
- perform OCR on image
language: zh-hant
og_description: 如何在發票圖像上執行 OCR，提取文字，並使用 Hugging Face LLM 修正錯誤。遵循此完整指南，獲得完美結果。
og_title: 如何在發票圖像上執行 OCR – 完整教學
tags:
- OCR
- Python
- AI post‑processing
- Hugging Face
title: 如何在發票圖像上執行 OCR – 完整逐步指南
url: /zh-hant/python/general/how-to-run-ocr-on-invoice-images-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在發票圖像上執行 OCR – 完整逐步指南

有沒有想過 **如何在掃描的發票上執行 OCR**，並獲得乾淨、可搜尋的文字，而不需要花數小時清理？你並非唯一。 在許多實務專案中，原始 OCR 輸出充斥著辨識錯誤——例如把 “O” 誤認為 “0”、把 “l” 誤認為 “1”，甚至整個單詞亂碼。 好消息是？只要幾行 Python 程式碼，你不僅可以 **perform OCR on image** 檔案，還能使用 Hugging Face 的輕量模型自動 **correct OCR errors**。

在本教學中，我們將逐步說明所有必備知識：從載入發票圖像、擷取原始文字、下載量化模型，到優化結果，使你最終得到完美的文字稿，適合後續處理。完成後，你將能在單一、可重複執行的腳本中 **extract text from invoice** PDF 或 PNG。

## 前置條件與設定

| 需求 | 重要原因 |
|-------------|----------------|
| Python 3.9+ | 現代語法與型別提示 |
| `aspose-ocr` package | 提供範例中使用的 `ocr.OcrEngine` |
| `aspose-ai` package | 提供 `AsposeAI` 後處理器 |
| Access to a GPU (optional) | 加速 LLM 層；若無 GPU 亦可使用 CPU 正常運作 |
| Internet connection (first run) | 需要自動 **download Hugging Face model** |

您可以使用以下指令安裝所需的函式庫：

```bash
pip install aspose-ocr aspose-ai
```

> **專業提示：** 若您打算在 GPU 上執行 LLM，請安裝支援 CUDA 的 `torch`（`pip install torch --extra-index-url https://download.pytorch.org/whl/cu118`）。

環境就緒後，讓我們進入程式碼。

---

## 步驟 1 – 初始化 OCR 引擎並載入發票圖像

第一件事是建立 Aspose OCR 引擎的實例，並指向要處理的檔案。此步驟是 **how to run OCR** 在任何圖像上的基礎。

```python
import ocr  # Aspose OCR package

# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Load the invoice you want to read
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")
```

> **為什麼重要：** `load_image` 支援 PNG、JPEG、TIFF，甚至 PDF 頁面，讓您無論何種格式皆可 **perform OCR on image**。

## 步驟 2 – 執行基本 OCR 以擷取原始文字

圖像載入後，引擎即可產生原始文字稿。此輸出常常雜訊較多，因此我們稍後會執行校正步驟。

```python
# Perform the OCR scan
raw_result = ocr_engine.recognize()

# Show what the engine saw
print("Raw OCR:", raw_result.text)
```

典型的原始輸出可能如下：

```
Raw OCR: Inv0ice No: 12345
Date: 2023/07/15
Total Am0unt: $1,200.00
```

請注意零 (`0`) 出現在本應為字母 “O” 的位置嗎？這正是我們稍後要修正的錯誤類型。

## 步驟 3 – 使用輕量 LLM 設定 AI 後處理器

現在我們引入一個 **download Hugging Face model**，其體積足以在一般硬體上執行，同時又足夠強大以理解發票語言。範例使用 Qwen 2.5 3B‑Instruct GGUF 模型，經 `int8` 量化以降低記憶體佔用。

```python
from aspose_ai import AsposeAI, AsposeAIModelConfig

# Define model configuration
model_config = AsposeAIModelConfig(
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",          # reduces size dramatically
    gpu_layers=20,                             # use GPU for the first 20 layers if available
    allow_auto_download="true"                # pulls the model on first run
)

# Initialise the AI processor and attach the post‑processor
ai_processor = AsposeAI()
ai_processor.set_post_processor("llm_correction", model_config)
```

> **為什麼選擇此模型？** `int8` 量化將檔案縮減至約 1.2 GB，讓大多數筆記型電腦都能負荷。GPU 層可加速推論，若未偵測到 GPU，程式會自動回退至 CPU。

## 步驟 4 – 在原始 OCR 結果上執行 LLM 基礎的校正

模型就緒後，我們將原始文字送入後處理器。LLM 會重新寫入文字稿，修正常見的 OCR 錯誤並正規化數字。

```python
# Apply AI correction
corrected_result = ai_processor.run_postprocessor(raw_result)

# Display the cleaned output
print("AI‑corrected:", corrected_result.text)
```

預期的清理後輸出：

```
AI‑corrected: Invoice No: 12345
Date: 2023/07/15
Total Amount: $1,200.00
```

你可以看到零已恢復為字母 “O”，而 “Am0unt” 也變成了 “Amount”。這正是 **correct OCR errors** 的核心自動化步驟。

## 步驟 5 – 釋放資源與清理

大型語言模型會佔用 GPU 記憶體，完成後釋放資源是良好實踐。

```python
# Free the model and any GPU buffers
ai_processor.free_resources()
```

如果你打算批次處理大量發票，可以在腳本最後一次性釋放模型，而非每次都釋放。

## 完整範例

將所有步驟整合，以下是一個可直接存為 `.py` 並執行的單一腳本：

```python
# ------------------------------------------------------------
# How to Run OCR on Invoice Images – End‑to‑End Example
# ------------------------------------------------------------
import ocr
from aspose_ai import AsposeAI, AsposeAIModelConfig

def main():
    # 1️⃣ Initialise OCR engine
    ocr_engine = ocr.OcrEngine()
    ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")

    # 2️⃣ Capture raw OCR text
    raw_result = ocr_engine.recognize()
    print("Raw OCR:", raw_result.text)

    # 3️⃣ Configure lightweight LLM from Hugging Face
    model_cfg = AsposeAIModelConfig(
        hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
        hugging_face_quantization="int8",
        gpu_layers=20,
        allow_auto_download="true"
    )
    ai = AsposeAI()
    ai.set_post_processor("llm_correction", model_cfg)

    # 4️⃣ Run AI correction
    corrected = ai.run_postprocessor(raw_result)
    print("AI‑corrected:", corrected.text)

    # 5️⃣ Clean up
    ai.free_resources()

if __name__ == "__main__":
    main()
```

執行腳本後，應產生與前述 “AI‑corrected” 區塊相似的輸出。隨意將圖像路徑換成其他 **invoice** 或 **receipt**，即可批量 **extract text from invoice** 檔案。

## 常見問題與邊緣案例

### 如果我沒有 GPU 該怎麼辦？

`gpu_layers` 參數為可選。將其設為 `0` 或直接省略，模型將完全在 CPU 上執行。預期推論較慢——在現代筆記型電腦上每頁約需 2–3 秒。

### 我的發票是多頁 PDF。該如何處理？

先將每頁轉為單獨的圖像（例如使用 `pdf2image`），再以相同腳本迴圈處理各頁。OCR 引擎可獨立處理每張圖像，LLM 亦會校正每段文字。

```python
from pdf2image import convert_from_path

pages = convert_from_path("invoice.pdf", dpi=300)
for i, page_img in enumerate(pages):
    ocr_engine.load_image(page_img)
    # …run steps 2‑4…
```

### 模型下載在防火牆後失敗？

可自行從 Hugging Face 模型中心下載模型，解壓至本機資料夾，並將 `hugging_face_repo_id` 指向該本機路徑：

```python
model_cfg = AsposeAIModelConfig(
    hugging_face_repo_id="/local/path/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20,
    allow_auto_download="false"
)
```

### 校正的準確度如何？

對於一般英文發票，LLM 能修正超過 95 % 的常見 OCR 誤辨。複雜的手寫筆記仍可能需要人工校對。

## 生產環境的技巧與竅門

- **Batch processing：** 將步驟 2‑4 包裝成函式，傳入檔案路徑清單。重複使用同一個 `AsposeAI` 實例以避免重新載入模型。  
- **Logging：** 用 Python 的 `logging` 模組取代 `print`，同時記錄原始與校正後的輸出，以利稽核。  
- **Error handling：** 使用 `try/except` 包圍 OCR 呼叫。若圖像處理失敗，記錄檔名後繼續執行。  
- **Performance tuning：** 嘗試調整 `gpu_layers`。更多 GPU 層可加速推論，但會增加 VRAM 用量。

## 結論

我們已完整說明 **how to run OCR** 在發票圖像上的全流程，示範了 **perform OCR on image**、**download Hugging Face model** 與 **correct OCR errors** 的自動化步驟。完整腳本展示了一個實用的工作流程，能直接嵌入任何基於 Python 的自動化管線。

接下來的步驟？可嘗試將管線延伸至 **extract key fields**（發票號碼、日期、總金額），使用正規表達式從校正後文字中抽取，或將清理後的結果寫入資料庫以供搜尋。若需要其他語言或領域的知識，也可以實驗 Hugging Face 上的其他輕量 LLM。

祝編程愉快，願您的 OCR 結果永遠清晰如水晶！

![如何在發票圖像上執行 OCR](ocr_invoice_example.png "如何在發票上執行 OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}