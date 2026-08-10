---
category: general
date: 2026-06-06
description: Python OCR 教學，示範如何辨識影像文字、執行高解析度 OCR 以及使用 GPU 加速的 OCR 來擷取西班牙文文字。
draft: false
keywords:
- python ocr tutorial
- recognize image text
- high resolution ocr
- gpu accelerated ocr
- extract spanish text
language: zh-hant
og_description: Python OCR 教學，帶你一步步認識圖像文字、高解析度 OCR，以及使用 GPU 加速提取西班牙文文字。
og_title: Python OCR 教學 – GPU 加速文字辨識
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Python OCR tutorial showing how to recognize image text, perform high
    resolution OCR and extract Spanish text using GPU accelerated OCR.
  headline: Python OCR Tutorial – Recognize Image Text with GPU Acceleration
  type: TechArticle
- description: Python OCR tutorial showing how to recognize image text, perform high
    resolution OCR and extract Spanish text using GPU accelerated OCR.
  name: Python OCR Tutorial – Recognize Image Text with GPU Acceleration
  steps:
  - name: Prerequisites
    text: '- Python 3.9+ (the code works on 3.10 and newer as well). - A CUDA‑compatible
      GPU (optional but highly recommended). - Basic familiarity with pip and virtual
      environments.'
  - name: 6.1 Fallback When No GPU Is Present
    text: "```python if not torch.cuda.is_available(): # Re‑initialize the reader
      without GPU to avoid hidden errors reader = Reader(lang_list=[\"es\"], gpu=False)
      print(\"\U0001F504 Re‑initialized reader for CPU execution.\") ```"
  - name: 6.2 Down‑sampling Very Large Images
    text: 'If your image is larger than 4000 × 4000 px, you might run out of GPU memory.
      Down‑sample proportionally while preserving DPI:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- GPU
- Spanish
title: Python OCR 教學 – 使用 GPU 加速辨識影像文字
url: /zh-hant/python-java/general/python-ocr-tutorial-recognize-image-text-with-gpu-accelerati/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python OCR 教學 – 使用 GPU 加速辨識影像文字

有沒有想過如何在 Python 程式中 **recognize image text**，而不需要花上數小時調整設定？你並不是唯一有此疑問的人。在本篇 **python ocr tutorial** 中，我們將示範一個乾淨、端對端的方式，從高解析度圖片中擷取西班牙文文字，並加入 GPU 加速，使整個過程快如閃電。

把它想像成一個快速的咖啡休息示範，之後你可以將它擴展成生產等級的工作流程。閱讀完本指南後，你將擁有一個可執行的程式，能執行 **high resolution OCR**、利用支援 CUDA 的 GPU，並輸出你所需的西班牙文字。

## 你將學到什麼

- 如何安裝與匯入支援 GPU 加速的現代 OCR 函式庫。  
- 如何建立 OCR 引擎實例，並設定為西班牙文的 **recognize image text**。  
- 如何啟用 **gpu accelerated OCR**，在高解析度檔案上獲得巨大的速度提升。  
- 如何處理如缺少 CUDA 驅動程式或回退至 CPU 等邊緣情況。  
- 提升準確度的技巧，當你需要從噪點掃描中 **extract spanish text** 時。  

### 先決條件

- Python 3.9+（程式碼在 3.10 及更新版本亦可執行）。  
- 支援 CUDA 的 GPU（非必須，但強烈建議）。  
- 對 pip 與虛擬環境有基本了解。  

如果缺少上述任一項目，教學仍可執行——只要跳過 GPU 步驟，函式庫會自動回退至 CPU。

---

## Python OCR 教學：安裝必要套件

首先，我們需要一個穩固的 OCR 引擎。於本教學中，我們將使用開源的 **`easyocr`** 套件，當偵測到相容裝置時，它會內建 GPU 支援。

```bash
# Create a fresh virtual environment (optional but tidy)
python -m venv ocr-env
source ocr-env/bin/activate   # On Windows use `ocr-env\Scripts\activate`

# Install EasyOCR and its optional torch dependencies
pip install easyocr[torch]   # Installs both CPU and GPU builds of PyTorch
```

> **Pro tip:** 如果你已經安裝了 PyTorch，請確保它與你的 CUDA 版本相符（`pip install torch==2.2.0+cu121 -f https://download.pytorch.org/whl/torch_stable.html`）。版本不匹配是導致「GPU not found」錯誤的常見原因。

---

## 步驟 1：建立 OCR 引擎實例

現在我們啟動引擎。EasyOCR 的主要類別為 `Reader`。建構子接受語言代碼的清單，我們將傳入西班牙語的 `"es"`。

```python
# Step 1: Initialize the OCR reader for Spanish
from easyocr import Reader

# The `gpu` flag tells EasyOCR to try using CUDA if it’s available.
reader = Reader(lang_list=["es"], gpu=True)
```

*Why this matters:* 透過事先宣告語言，引擎只會載入必要的神經網路權重，從而節省記憶體並加速推論——在之後處理 **high resolution OCR** 時特別有用。

## 步驟 2：準備高解析度影像

高解析度影像提供模型更多像素可供處理，通常會轉化為更佳的字元辨識。假設你有一個名為 `high_res_spanish.png`，位於 `samples` 資料夾中的檔案。

```python
import os

# Construct an absolute path – keeps the script portable
image_path = os.path.join("samples", "high_res_spanish.png")

# Quick sanity check – raise a clear error if the file is missing
if not os.path.isfile(image_path):
    raise FileNotFoundError(f"Image not found at {image_path}")
```

如果手頭沒有高解析度樣本，你可以從 Unsplash 下載免費圖片，或使用 Pillow 產生合成影像。關鍵是將 DPI 保持在 300 以上，以獲得最佳效果。

## 步驟 3：啟用 GPU 加速（可選但建議）

當你設定 `gpu=True` 時，EasyOCR 已會嘗試使用 GPU。然而，特別在多 GPU 環境下，驗證實際使用的裝置仍是良好做法。

```python
import torch

# Verify CUDA availability – helpful for debugging
if torch.cuda.is_available():
    print(f"✅ CUDA device detected: {torch.cuda.get_device_name(0)}")
else:
    print("⚠️ No CUDA device found – falling back to CPU. Performance will be slower.")
```

*Why check this?* 若腳本悄悄回退至 CPU，你可能會疑惑為何原本 5 秒的操作突然變成 30 秒。這個小檢查讓行為透明，並使你的 **gpu accelerated OCR** 流程保持可預測。

## 步驟 4：執行高解析度 OCR 並辨識影像文字

現在是有趣的部分——實際讀取文字。EasyOCR 的 `readtext` 方法會回傳一個包含邊界框、辨識字串與信心分數的 tuple 清單。

```python
# Step 4: Run OCR on the high‑resolution image
results = reader.readtext(image_path, detail=1, paragraph=False)

# `results` looks like:
# [
#   ([(x1, y1), (x2, y2), (x3, y3), (x4, y4)], 'Texto reconocido', 0.98),
#   ...
# ]
```

若你只需要純文字而不含座標，請設定 `detail=0`。對於大多數 **recognize image text** 的使用情境，預設值（`detail=1`）已提供足夠的上下文以便之後後處理。

## 步驟 5：擷取西班牙文字並清理輸出

因為我們向 EasyOCR 指定了西班牙語，回傳的字串已是該語言。儘管如此，你可能仍想將它們串接、去除空白，或過濾低信心的偵測結果。

```python
# Step 5: Consolidate high‑confidence Spanish strings
extracted_text = []
for bbox, text, conf in results:
    if conf > 0.85:                # Drop anything below 85 % confidence
        extracted_text.append(text)

# Join everything into a single block – perfect for further NLP tasks
final_text = "\n".join(extracted_text)

print("📝 Extracted Spanish text:")
print(final_text)
```

**What if the confidence is low?** 你可以降低門檻（但可能產生雜訊），或在影像上做前處理（提升對比、二值化或去斜）。在掃描文件上執行 **high resolution OCR** 時，這些技巧相當常見。

## 步驟 6：處理邊緣案例與效能調整

即使是最佳訓練的模型也會在某些情況下失誤。以下提供幾個快速修正，你可以直接貼入腳本中。

### 6.1 無 GPU 時的回退方案

```python
if not torch.cuda.is_available():
    # Re‑initialize the reader without GPU to avoid hidden errors
    reader = Reader(lang_list=["es"], gpu=False)
    print("🔄 Re‑initialized reader for CPU execution.")
```

### 6.2 大尺寸影像的降採樣

如果你的影像大於 4000 × 4000 px，可能會耗盡 GPU 記憶體。請在保留 DPI 的同時按比例降採樣：

```python
from PIL import Image

def resize_if_needed(path, max_dim=3000):
    img = Image.open(path)
    if max(img.size) > max_dim:
        scale = max_dim / max(img.size)
        new_size = (int(img.width * scale), int(img.height * scale))
        img = img.resize(new_size, Image.LANCZOS)
        resized_path = path.replace(".png", "_resized.png")
        img.save(resized_path)
        return resized_path
    return path

image_path = resize_if_needed(image_path)
```

這些程式碼片段可讓腳本更具韌性，無論你是在工作站或是一般筆記型電腦上執行。

## 完整範例程式

將上述步驟整合起來，以下是完整的腳本，你可以直接複製貼上並立即執行：

```python
# python_ocr_tutorial.py
import os
import torch
from PIL import Image
from easyocr import Reader

# ----------------------------------------------------------------------
# Helper: Resize very large images to avoid GPU OOM errors
def resize_if_needed(path, max_dim=3000):
    img = Image.open(path)
    if max(img.size) > max_dim:
        scale = max_dim / max(img.size)
        new_size = (int(img.width * scale), int(img.height * scale))
        img = img.resize(new_size, Image.LANCZOS)
        resized_path = path.replace(".png", "_resized.png")
        img.save(resized_path)
        return resized_path
    return path
# ----------------------------------------------------------------------

# 1️⃣ Verify CUDA availability (optional)
if torch.cuda.is_available():
    print(f"✅ CUDA device detected: {torch.cuda.get_device_name(0)}")
else:
    print("⚠️ No CUDA device – using CPU (expect slower performance).")

# 2️⃣ Initialize the OCR engine for Spanish (GPU if possible)
reader = Reader(lang_list=["es"], gpu=torch.cuda.is_available())

# 3️⃣ Path to the high‑resolution image
image_path = os.path.join("samples", "high_res_spanish.png")
if not os.path.isfile(image_path):
    raise FileNotFoundError(f"Image not found at {image_path}")

# 4️⃣ Resize if the image is gigantic
image_path = resize_if_needed(image_path)

# 5️⃣ Run OCR – this is the core **recognize image text** step
results = reader.readtext(image_path, detail=1, paragraph=False)

# 6️⃣ Filter and concatenate high‑confidence Spanish strings
extracted = []
for bbox, txt, conf in results:
    if conf > 0.85:
        extracted.append(txt)

final_text = "\n".join(extracted)

# 7️⃣ Output the result – **extract spanish text** ready for downstream processing
print("\n📝 Extracted Spanish text:")
print(final_text)
```

**預期輸出（範例）：**



## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，並在此基礎上進一步說明。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通其他 API 功能，並在自己的專案中探索替代實作方式。

- [使用 Aspose OCR 從影像擷取文字 – 步驟指南](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [使用 Aspose.OCR 以語言辨識影像文字的方法](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [在 Aspose.OCR 中辨識頁面矩形以進行文字辨識](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}