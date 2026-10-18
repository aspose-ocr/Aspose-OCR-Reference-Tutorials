---
category: general
date: 2026-06-22
description: 使用 Aspose OCR 在 Python 中辨識 PNG 檔案的文字。學習批次 OCR 圖片並設定 GPU 層以加速處理。
draft: false
keywords:
- recognize text from png
- batch ocr images
- set gpu layers
- Aspose OCR Python
- GPU acceleration OCR
language: zh-hant
og_description: 使用 Aspose OCR 在 Python 中辨識 PNG 檔案的文字。本指南說明如何批次執行 OCR 圖像並設定 GPU 層以提升速度。
og_title: 從 PNG 識別文字 – Aspose OCR 逐步教學
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: recognize text from png files using Aspose OCR in Python. Learn batch
    OCR images and set GPU layers for fast processing.
  headline: recognize text from png – Complete Guide with Aspose OCR & AI
  type: TechArticle
- description: recognize text from png files using Aspose OCR in Python. Learn batch
    OCR images and set GPU layers for fast processing.
  name: recognize text from png – Complete Guide with Aspose OCR & AI
  steps:
  - name: '**Model download fails** – Ensure your environment can reach `https://huggingface.co`.
      A corporate proxy may need configuration (`https_proxy` env var).'
    text: '**Model download fails** – Ensure your environment can reach `https://huggingface.co`.
      A corporate proxy may need configuration (`https_proxy` env var).'
  - name: '**GPU not detected** – Verify that the `torch` library (installed as a
      dependency) sees the GPU: `import torch; print(torch.cuda.is_available())`.
      If it returns `False`, install the CUDA‑compatible PyTorch wheel.'
    text: '**GPU not detected** – Verify that the `torch` library (installed as a
      dependency) sees the GPU: `import torch; print(torch.cuda.is_available())`.
      If it returns `False`, install the CUDA‑compatible PyTorch wheel.'
  - name: '**Incorrect image path** – `Path.glob("*.png")` is case‑sensitive on Linux.
      Use `*.PNG` or `*.png` accordingly, or add `pathlib.Path(...).rglob("*.[pP][nN][gG]")`
      for safety.'
    text: '**Incorrect image path** – `Path.glob("*.png")` is case‑sensitive on Linux.
      Use `*.PNG` or `*.png` accordingly, or add `pathlib.Path(...).rglob("*.[pP][nN][gG]")`
      for safety.'
  - name: '**Post‑processor over‑corrects** – The simple replace may turn legitimate
      “0” characters into “o”. Test on a representative sample and adjust the logic
      as needed.'
    text: '**Post‑processor over‑corrects** – The simple replace may turn legitimate
      “0” characters into “o”. Test on a representative sample and adjust the logic
      as needed.'
  type: HowTo
tags:
- OCR
- Python
- AsposeAI
title: 從 PNG 識別文字 – Aspose OCR 與 AI 完整指南
url: /zh-hant/python/general/recognize-text-from-png-complete-guide-with-aspose-ocr-ai/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從 PNG 識別文字 – 完整功能的 Aspose OCR 與 AI 教程

有沒有曾經想 **從 png 識別文字**，卻被繁雜的設定細節卡住？你並不孤單。無論是數位化收據、掃描表格，或是將螢幕截圖轉成可搜尋的文字，掌握 Python 中的批次 OCR 圖片處理都能為你省下大量時間。

在本指南中，我們將一步步示範一個可直接執行的範例，不僅 **從 png 識別文字**，還會示範如何 **設定 GPU 層數** 以獲得顯著的速度提升。完成後，你將擁有一個自包含的腳本、每一步的清晰說明，以及可直接複製貼上的實用小技巧。

## 本教學涵蓋內容

- 安裝 Aspose OCR 與 Aspose AI Python 套件  
- 以自動下載方式從 Hugging Face 設定 AI 模型  
- 製作簡易的後處理器，修正最常見的 OCR 錯字  
- 執行 **批次 OCR 圖片**，遍歷整個 PNG 資料夾  
- 使用 **設定 GPU 層數** 以發揮顯示卡效能  
- 安全釋放資源，完成後清理  

不需要外部服務，也沒有隱藏的魔法——只有純粹的 Python 程式碼，你可以直接放入 `.py` 檔案執行。

![Diagram of recognize text from png workflow](workflow.png){alt="從 PNG 識別文字工作流程圖"}

## 前置需求

| Requirement | Why it matters |
|-------------|----------------|
| Python 3.8+ | Aspose AI 的 wheel 針對較新版本的直譯器 |
| 支援 CUDA 的 GPU（可選） | 若想 **設定 GPU 層數** 以加速時必須 |
| 首次執行時需有網路連線 | 模型會自動從 Hugging Face 下載 |
| 已安裝 `pip` | 用於取得 Aspose 套件 |

如果你已具備上述條件，太好了——可以直接開始。如果還缺少，以下的安裝步驟會協助你補齊。

---

## 步驟 1：安裝 Aspose OCR 與 Aspose AI 套件

先從 PyPI 取得函式庫。下列指令會一次安裝 OCR 引擎與 AI 輔助套件。

```bash
pip install aspose-ocr aspose-ai
```

*小技巧*：使用虛擬環境（`python -m venv .venv`）可以讓套件與全域 Python 安裝隔離。

---

## 步驟 2：建立並設定 Aspose AI 實例

AI 元件為 OCR 引擎提供「智慧」模式。我們會指向 `Qwen/Qwen2.5-3B-Instruct-GGUF` 模型，若缺少則自動下載，並 **設定 GPU 層數** 為 30（之後可自行調整）。

```python
from aspose_ai import AsposeAI, AsposeAIModelConfig

# Initialize the AI wrapper
ai = AsposeAI()

# Build a model configuration
model_cfg = AsposeAIModelConfig(
    allow_auto_download="true",                     # Grab the model automatically
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",               # Smaller footprint, still accurate
    directory_model_path="YOUR_DIRECTORY/ai_models", # Where the model will live
    gpu_layers=30                                   # <-- set gpu layers for GPU acceleration
)

# Apply the configuration and spin up the model
ai.initialize(model_cfg)
```

**為什麼這很重要：**  
- `allow_auto_download` 省去手動下載約 2 GB 模型的步驟。  
- `gpu_layers=30` 告訴底層 transformer 前 30 層在 GPU 上執行，若有相容的 GPU，推論時間會大幅縮短。  
- 使用 `int8` 量化可在不犧牲太多準確度的前提下降低記憶體使用。

---

## 步驟 3：定義簡易的後處理器以清理 OCR 錯誤

OCR 並非完美，特別是低解析度的 PNG。快速的解法是取代常被誤讀的字元。以下函式會把「0」換成「o」以及「1」換成「l」，這是我們在掃描發票時常見的情況。

```python
def fix_common_errors(text, **_):
    """
    Post‑processor that corrects typical OCR mis‑recognitions.
    Feel free to extend this with regexes or custom dictionaries.
    """
    return text.replace("0", "o").replace("1", "l")
```

接下來會把這個函式綁定到 AI 實例，讓每次辨識結果都自動通過後處理。

---

## 步驟 4：綁定後處理器與 OCR 引擎

現在把所有元件串起來：OCR 引擎、AI 模型與後處理器。

```python
import ocr  # Aspose OCR module

# Attach the post‑processor
ai.set_post_processor(fix_common_errors, {})

# Spin up the OCR engine and bind the AI
engine = ocr.OcrEngine()
engine.set_ai(ai)
```

**底層發生了什麼？**  
`OcrEngine` 會把繁重的運算交給你先前設定好的 AI 模型。模型回傳原始文字後，Aspose 會呼叫 `fix_common_errors` 進行清理，然後才把結果交給使用者。

---

## 步驟 5：批次 OCR 圖片 – 處理資料夾內的每個 PNG

以下程式碼是本教學的核心：遍歷目錄、載入每個 `.png`、執行 OCR，並印出清理後的結果。這是執行 **批次 OCR 圖片** 的標準做法。

```python
from pathlib import Path

# Replace with the folder that holds your PNG files
image_folder = Path("YOUR_DIRECTORY")

# Iterate over every PNG file in the folder
for img_path in image_folder.glob("*.png"):
    # Load the image into the engine
    engine.load_image(str(img_path))

    # Perform recognition
    result = engine.recognize()

    # Output the filename and the extracted text
    print(f"[{img_path.name}] → {result.text}")
```

**預期輸出**（收據範例）：

```
[receipt_001.png] → Total amount: $23.45
[receipt_002.png] → Item: Coffee, Price: $3.50
```

若你有數十或數百個檔案，這段迴圈會依序處理，且會重複使用同一個 AI 實例，避免重複載入模型的開銷。

---

## 步驟 6：清理 – 釋放資源並關閉引擎

完成後，釋放 GPU 記憶體與其他原生資源是良好慣例。Aspose 提供了明確的方法來做到這點。

```python
# Release the AI model and any GPU buffers
ai.free_resources()

# Dispose of the OCR engine to close native handles
engine.dispose()
```

若省略此步驟，GPU 記憶體可能會遺留，導致下次執行腳本時出現記憶體不足的錯誤。

---

## 加分項：依硬體調整 GPU 層數

先前設定的 `gpu_layers` 值對多數現代 GPU 來說是個不錯的平衡點，但你可能需要依實際情況調整：

| GPU 記憶體 (GB) | 推薦 `gpu_layers` |
|-----------------|-------------------|
| 4 GB 或以下      | 10‑15             |
| 6‑8 GB          | 20‑30             |
| 12 GB 以上      | 35‑45（或更高）   |

若超出 GPU 記憶體，引擎會自動將剩餘層退回 CPU 執行，雖然會變慢但不會當機。可使用 `nvidia‑smi` 監控使用情形，盡情實驗。

---

## 常見陷阱與避免方式

1. **模型下載失敗** – 確認環境能連到 `https://huggingface.co`。公司內部代理可能需要設定 `https_proxy` 環境變數。  
2. **GPU 未偵測到** – 檢查 `torch`（作為依賴安裝）是否看到 GPU：`import torch; print(torch.cuda.is_available())`。若回傳 `False`，請安裝相容 CUDA 的 PyTorch wheel。  
3. **圖像路徑錯誤** – `Path.glob("*.png")` 在 Linux 上區分大小寫。可改用 `*.PNG` 或 `*.png`，或使用 `pathlib.Path(...).rglob("*.[pP][nN][gG]")` 以兼容大小寫。  
4. **後處理器過度修正** – 簡單的取代可能會把真正的「0」變成「o」。請在具代表性的樣本上測試，並依需求調整邏輯。

---

## 完整可執行範例（直接複製貼上）

```python
# recognize_text_from_png_batch.py
# -------------------------------------------------
# Author: Your Name
# Date:   2026‑06‑22
# -------------------------------------------------
from pathlib import Path
import ocr                      # Aspose OCR module
from aspose_ai import AsposeAI, AsposeAIModelConfig

# ----- Step 1: AI configuration -----
ai = AsposeAI()
model_cfg = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    directory_model_path="YOUR_DIRECTORY/ai_models",
    gpu_layers=30               # <-- set gpu layers
)
ai.initialize(model_cfg)

# ----- Step 2: Post‑processor -----
def fix_common_errors(text, **_):
    """Replace typical OCR mis‑reads."""
    return text.replace("0", "o").replace("1", "l")

ai.set_post_processor(fix_common_errors, {})

# ----- Step 3: OCR engine -----
engine = ocr.OcrEngine()
engine.set_ai(ai)

# ----- Step 4: Batch processing -----
image_folder = Path("YOUR_DIRECTORY")
for img_path in image_folder.glob("*.png"):
    engine.load_image(str(img_path))
    result = engine.recognize()
    print(f"[{img_path.name}] → {result.text}")

# ----- Step 5: Cleanup -----
ai.free_resources()
engine.dispose()
```

執行方式：

```bash
python recognize_text_from_png_batch.py
```

執行後，你應該會看到每個 PNG 檔名以及對應的擷取文字，與前面示範的結果一致。

---

## 結論

我們已完整示範如何使用 Aspose OCR 與 Aspose AI 在 Python 中 **從 png 識別文字**，並將步驟整合成一個可直接投入生產環境的腳本。透過此腳本，你可以輕鬆實現 **批次 OCR 圖片**，而且藉由 `set gpu layers` 進一步提升效能。

## 接下來該學什麼？

以下教學與本篇內容緊密相關，能幫助你進一步掌握 API 功能或探索其他實作方式：

- [如何在 Aspose.OCR for .NET 中使用 List 進行批次 OCR 圖片](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [在資料夾上執行 OCR 操作以擷取圖像文字](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [使用 Aspose.OCR 依語言 OCR 圖像文字](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}