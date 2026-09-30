---
category: general
date: 2026-01-07
description: 如何執行 OCR 並從圖像中提取文字以進行發票處理。學習提升 OCR 準確度、載入圖像進行 OCR，以及高效處理發票 OCR。
draft: false
keywords:
- how to run ocr
- extract text from image
- improve ocr accuracy
- load image for ocr
- process invoice ocr
language: zh-hant
og_description: 一步一步教你在發票上執行 OCR。從圖像提取文字、提升 OCR 準確度，並使用 Aspose AI 載入圖像進行 OCR。
og_title: 如何在發票上執行 OCR – 完整 Python 指南
tags:
- OCR
- Python
- Image Processing
title: 如何在發票上執行 OCR – 使用 Python 從圖像提取文字
url: /zh-hant/python/general/how-to-run-ocr-on-invoices-extract-text-from-image-with-pyth/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在發票上執行 OCR – 使用 Python 從圖像提取文字

你是否曾好奇 **如何執行 OCR** 於掃描的發票並取得乾淨、可搜尋的文字？你並不孤單。許多開發者在原始 OCR 輸出充斥拼寫錯誤、斷裂的換行以及缺少標點時卡住了。在本教學中，我們將逐步說明一個全端解決方案，不僅 **從圖像提取文字**，還透過 Aspose AI 模型的後處理 **提升 OCR 準確度**。

你將會看到如何 **載入圖像以進行 OCR**、執行內建引擎，然後套用輕量級拼寫檢查，使結果可直接用於後續分析。完成後，你將擁有一個可重複使用的腳本，能夠嵌入任何發票處理流程中。

> **你需要的條件**  
> * Python 3.9 或更新版本  
> * `aspose-ocr` 與 `aspose-ai` 套件（透過 `pip` 安裝）  
> * 發票圖像（PNG、JPEG 或 TIFF）— 我們將使用 `sample_invoice.png` 作為範例  
> * 可選：具備至少 4 GB VRAM 的 GPU，以加速模型推論（腳本亦可在 CPU 上執行）

---

## 步驟 1：安裝必要套件並設定環境

在我們能夠 **載入圖像以進行 OCR** 之前，必須確保所需的函式庫已安裝。Aspose OCR 引擎附帶簡易的 Python 包裝器，而 AI 後處理則依賴 Hugging Face 的量化模型。

```bash
# Install Aspose OCR and AI packages
pip install aspose-ocr aspose-ai
```

> **專業提示：** 若你打算使用 GPU 加速，請安裝支援 CUDA 的 `torch`（`pip install torch --extra-index-url https://download.pytorch.org/whl/cu121`）。

---

## 步驟 2：載入發票圖像

載入圖像相當簡單，但值得說明為何我們會明確將路徑設為原始字串 (`r"..."`)。這可避免在 Windows 路徑上因轉義字元而產生的意外錯誤。

```python
import aspose.ocr as ocr

# Define the path to your invoice image
image_path = r"YOUR_DIRECTORY/sample_invoice.png"

# Initialize the OCR engine and attach the image
engine = ocr.OcrEngine()
engine.image = ocr.Image.load(image_path)
```

*為何重要：* 使用 `ocr.Image.load` 可確保圖像依照 Aspose 的最佳預設進行前置處理（二值化、去斜），這已在任何 AI 處理之前 **提升 OCR 準確度**。

---

## 步驟 3：執行內建 OCR 引擎

現在我們真正 **執行 OCR** 並擷取原始文字。此步驟展示了使用原始 OCR 時常見的輸出——通常充斥著雜亂的換行與偶發的拼寫錯誤。

```python
# Perform OCR
engine.recognize()
raw_text = engine.recognized_text

print("Raw OCR output:")
print(raw_text)
```

**典型的原始輸出**（為簡潔起見已截斷）：

```
INVOICE NO: 2023‑00123
Date: 06/15/2023
Bill To:
Acme Corp
123 Main St
...
Total Due: $1,250.00
```

你可能會發現「Invoice」被寫成「Invo1ce」或缺少標點。這時 AI 後處理就會介入。

---

## 步驟 4：設定 Aspose AI 模型

我們將使用的 AI 模型是 **Qwen2.5‑3B‑Instruct‑GGUF**，這是一個輕量級指令微調的大型語言模型，能在中階 GPU 上順暢運行。以下設定告訴 Aspose 從哪裡取得模型、在 GPU 上保留多少層，以及處理長段落的上下文大小。

```python
from aspose.ai import AsposeAI, AsposeAIModelConfig

model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="q4_k_m",
    gpu_layers=30,               # 30 layers on GPU, remainder on CPU
    context_size=4096            # larger context for long paragraphs
)

ai = AsposeAI()
ai.initialize(model_config)   # you could also pass `model_config` to the constructor
```

> **為何使用此設定？**  
> * `gpu_layers=30` 在速度與記憶體之間取得平衡——大部分推論在 GPU 上執行，剩餘層則留在 CPU 以避免 OOM 錯誤。  
> * `context_size=4096` 確保模型一次能看到整張發票，避免截斷重要欄位。

---

## 步驟 5：建立簡易拼寫檢查後處理器

我們會將 AI 呼叫包裝在一個名為 `simple_spell_check` 的小函式中。提示語特意簡潔：「Correct spelling and punctuation:」後接原始 OCR 文字。模型會回傳整理過的版本。

```python
def simple_spell_check(text):
    prompt = f"Correct spelling and punctuation:\n{text}"
    return ai.run_prompt(prompt)

# Register the post‑processor with the AI instance
ai.set_post_processor(simple_spell_check, None)
```

**運作方式：** `ai.run_prompt` 將提示傳送給本機載入的 LLM，然後回傳一個包含校正拼寫、正確標點以及更自然換行布局的單一字串。

---

## 步驟 6：將後處理器套用於原始 OCR 文字

現在魔法發生了。我們將原始 OCR 輸入送入後處理器，並印出強化後的結果。

```python
enhanced_text = ai.run_postprocessor(raw_text)

print("\nAI‑enhanced OCR output:")
print(enhanced_text)
```

**範例強化後的輸出**：

```
Invoice No: 2023‑00123
Date: 06/15/2023
Bill To:
Acme Corp
123 Main St
...
Total Due: $1,250.00
```

請留意「Invoice」拼寫已更正、冒號使用正確，且換行一致——正是可靠後續解析所需的結果。

---

## 步驟 7：清理資源

OCR 引擎與 AI 模型皆會分配原生資源。完成後釋放它們是良好慣例，特別是在長時間執行的服務中。

```python
ai.free_resources()
engine.dispose()
```

---

## 完整腳本 – 可直接貼上使用

以下是完整且可執行的腳本，將所有步驟串接起來。將其儲存為 `invoice_ocr.py`，將 `YOUR_DIRECTORY` 替換為放置發票圖像的資料夾路徑，然後以 `python invoice_ocr.py` 執行。

```python
# invoice_ocr.py
import aspose.ocr as ocr
from aspose.ai import AsposeAI, AsposeAIModelConfig

# -------------------------------------------------
# Step 1: Load the image to be processed
# -------------------------------------------------
image_path = r"YOUR_DIRECTORY/sample_invoice.png"
engine = ocr.OcrEngine()
engine.image = ocr.Image.load(image_path)

# -------------------------------------------------
# Step 2: Run the built‑in OCR engine and obtain raw text
# -------------------------------------------------
engine.recognize()
raw_text = engine.recognized_text
print("Raw OCR output:")
print(raw_text)

# -------------------------------------------------
# Step 3: Configure the Aspose AI model for post‑processing
# -------------------------------------------------
model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="q4_k_m",
    gpu_layers=30,
    context_size=4096
)

ai = AsposeAI()
ai.initialize(model_config)   # alternatively, pass config to the constructor

# -------------------------------------------------
# Step 4: Define a simple spell‑check post‑processor
# -------------------------------------------------
def simple_spell_check(text):
    prompt = f"Correct spelling and punctuation:\n{text}"
    return ai.run_prompt(prompt)

ai.set_post_processor(simple_spell_check, None)

# -------------------------------------------------
# Step 5: Apply the post‑processor to the raw OCR text
# -------------------------------------------------
enhanced_text = ai.run_postprocessor(raw_text)
print("\nAI‑enhanced OCR output:")
print(enhanced_text)

# -------------------------------------------------
# Step 6: Release resources
# -------------------------------------------------
ai.free_resources()
engine.dispose()
```

執行腳本後，你會同時看到雜訊較多的原始 OCR 輸出與已潤飾、**提升 OCR 準確度** 的版本並列顯示。

---

## 常見問題與邊緣案例

### 1. 如果我的發票圖像是多頁 PDF 該怎麼辦？

Aspose OCR 能直接載入 PDF 頁面。將載入圖像的程式碼行改為：

```python
engine.image = ocr.Image.load("invoice.pdf", page_index=0)  # 0‑based page number
```

遍歷 `page_index` 以順序處理每一頁。

### 2. 我的 GPU 記憶體不足——可以只使用 CPU 嗎？

當然可以。於 `AsposeAIModelConfig` 中將 `gpu_layers=0`。模型將完全在 CPU 上執行，速度較慢但對低階硬體較安全。

### 3. 如何處理非英文發票？

將模型倉庫 ID 換成特定語言的模型，例如 `"mistralai/Mistral-7B-Instruct-v0.2"` 以支援多語言。其餘流程保持不變。

### 4. 我可以串接多個後處理器嗎（例如格式化日期、抽取總金額）？

可以。`ai.set_post_processor` 接受一系列可呼叫的函式。例如：

```python
def extract_totals(text):
    # simple regex to pull monetary values
    import re
    totals = re.findall(r"\$\d+(?:,\d{3})*(?:\.\d{2})?", text)
    return "\n".join(totals)

ai.set_post_processor([simple_spell_check, extract_totals], None)
```

輸出將先經過拼寫檢查，之後再抽取總金額。

---

## 效能技巧與最佳實踐

| Tip | Why it Helps |
|-----|---------------|
| **批次處理多張發票** – 將它們載入列表並在迴圈中處理。 | 減少 Python 直譯器的開銷，且保持 AI 模型在記憶體中熱啟動。 |
| **快取模型** – 避免在 Web 服務中重複呼叫 `initialize`。 | 模型載入可能需約 30 秒；快取可即時回應。 |
| **在 OCR 前將大型圖像縮放至 1500 像素寬**。 | 較小的圖像可加速 OCR 與 AI 推論，同時不犧牲準確度。 |
| **在正式環境設定 `allow_auto_download="false"`** – 隨部署一起提供模型。 | 確保啟動時間可預測，避免網路問題。 |

---

## 結論

我們已說明如何在發票上 **執行 OCR**，從載入圖像到使用 AI 驅動的拼寫檢查潤飾結果。依循這些步驟，你可以可靠地 **從圖像提取文字**、**提升 OCR 準確度**，並在任何基於 Python 的工作流程中無縫 **處理發票 OCR**。

試著使用不同版面的發票——或許是手寫收據或掃描的合約。相同的管線只需微調即可適應，證明了結構良好的 OCR + AI 組合是任何文件自動化專案的多功能工具。

如果你覺得本指南對你有幫助，請考慮與同事分享或為託管 Aspose 套件的倉庫加星。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}