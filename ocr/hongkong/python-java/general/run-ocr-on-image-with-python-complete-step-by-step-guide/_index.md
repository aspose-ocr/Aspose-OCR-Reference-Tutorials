---
category: general
date: 2026-06-06
description: 使用 Python 對圖像執行 OCR，查看信心分數。學習如何過濾低信心字詞、設定閾值以及處理邊緣情況。
draft: false
keywords:
- run OCR on image
- Python OCR tutorial
- OCR confidence threshold
- low‑confidence word detection
- image text extraction
language: zh-hant
og_description: 在 Python 中對圖像執行 OCR，檢查信心分數，並過濾低信心的詞彙。本教學將帶你完成一個完整且可執行的範例。
og_title: 使用 Python 在圖片上執行 OCR – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Run OCR on image using Python and see confidence scores. Learn how
    to filter low‑confidence words, set thresholds, and handle edge cases.
  headline: Run OCR on Image with Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Run OCR on image using Python and see confidence scores. Learn how
    to filter low‑confidence words, set thresholds, and handle edge cases.
  name: Run OCR on Image with Python – Complete Step‑by‑Step Guide
  steps:
  - name: Install and Import the OCR Engine
    text: First, make sure the OCR library is available. **EasyOCR** works out‑of‑the‑box
      for many languages and gives you a confidence score per word.
  - name: Run OCR on the Image
    text: Now we actually **run OCR on image**. The `recognize_image` method from
      the original example is replaced with EasyOCR’s `readtext` call, which returns
      a list of `(bbox, text, confidence)` tuples.
  - name: Summarize Overall Confidence
    text: 'Unlike the earlier snippet that printed a single `confidence` attribute,
      EasyOCR gives a confidence per word. To get an overall sense, we’ll average
      them:'
  - name: List Low‑Confidence Words
    text: Now comes the part that directly answers the “list words whose confidence
      is below the desired threshold” requirement. We’ll set a **OCR confidence threshold**
      of 0.80 (80 %) by default, but you can adjust it.
  - name: Edge Cases & Variations
    text: 1. **Batch Processing** – If you need to **run OCR on image** files in bulk,
      wrap the above logic in a loop that iterates over a directory. 2. **Multiple
      Languages** – Pass a list like `['en', 'fr']` to `easyocr.Reader` and the engine
      will detect both. 3. **Alternative Engines** – Want to try **pyte
  type: HowTo
- questions:
  - answer: Not directly. Convert each PDF page to an image first (e.g., with `pdf2image`)
      and then feed the PNG/JPEG into the script.
    question: Does this work with PDFs?
  - answer: 'Try image preprocessing: increase contrast, remove background noise,
      or rotate the image to a horizontal baseline. EasyOCR also accepts a `contrast_ths`
      parameter you can tweak.'
    question: My confidence numbers are all low—what can I do?
  - answer: Absolutely. After the low‑confidence loop, write `ocr_results` to a `csv.DictWriter`
      where each row contains `text`, `confidence`, and bounding‑box coordinates.
    question: Can I export the results to CSV?
  - answer: 'EasyOCR automatically uses CUDA if a compatible GPU and PyTorch are installed.
      Verify with `torch.cuda.is_available()` before running the script. --- ## Conclusion
      We’ve just **run OCR on image** using Python, inspected the overall confidence,
      and isolated any low‑confidence words that need a {{< /b'
    question: Is there a GPU‑accelerated version?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
title: 使用 Python 在圖片上執行 OCR – 完整逐步教學
url: /zh-hant/python-java/general/run-ocr-on-image-with-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Python 進行圖像 OCR – 完整步驟指南

曾經需要 **對圖像執行 OCR**，卻不確定如何取得可靠的文字嗎？你並不孤單——許多開發者在抽取出的文字顯得搖晃且信心分數成謎時，都會卡在同一個問題上。

在本指南中，我們將直接切入可運作的解決方案：示範如何對圖像執行 OCR、讀取整體信心分數，並挑出任何需要人工審核的低信心字詞。完成後，你將擁有可重複使用的腳本、了解每一行程式碼的意義，並知道如何為自己的專案調整信心閾值。

## 本教學涵蓋內容

我們會一步步走過完整工作流程——從載入圖像到列印出低於 80 % 信心門檻的字詞報告。過程中會討論：

* 選擇穩定的 OCR 引擎（我們將使用 **EasyOCR**，一個熱門的 Python OCR 函式庫）  
* 解析每筆 OCR 結果都會回傳的 `confidence` 屬性  
* 以自訂 **OCR 信心閾值** 篩選字詞  
* 延伸腳本以支援批次處理或改用 **pytesseract** 等其他引擎  

不需要事先具備 OCR 經驗，只要對 Python 有基本認識，且有可執行的環境（建議 Python 3.9+）即可。

準備好把模糊的螢幕截圖變成乾淨、可搜尋的文字了嗎？讓我們開始吧。

---

## ## 如何使用 Python 對圖像執行 OCR

本教學的核心是一段三步驟程式碼，與前面示範的程式相同。以下我們會逐行拆解說明原因，最後提供完整、可直接複製貼上的腳本。

### 步驟 1：安裝與匯入 OCR 引擎

首先，確保已安裝 OCR 函式庫。**EasyOCR** 開箱即支援多種語言，且會為每個字詞提供信心分數。

```bash
pip install easyocr
```

```python
import easyocr  # The engine that will run OCR on image files
import os
```

*為什麼選 EasyOCR？* 它內建已於多樣資料集上訓練的深度學習模型，通常比舊版的 Tesseract 引擎在混合品質圖像上取得更高的信心分數。

> **小技巧：** 若你使用的環境受限（例如極小的 Docker container），`pytesseract` 可能較輕量，但會犧牲 EasyOCR 所提供的現代化準確度。

### 步驟 2：對圖像執行 OCR

現在真正 **對圖像執行 OCR**。原範例的 `recognize_image` 方法改為 EasyOCR 的 `readtext` 呼叫，會回傳 `(bbox, text, confidence)` 三元組的列表。

```python
# Initialize the OCR reader for English (you can add more languages as needed)
reader = easyocr.Reader(['en'])

# Path to the image you want to process
image_path = os.path.join("YOUR_DIRECTORY", "mixed_quality.png")

# Perform OCR – this is the step where we run OCR on image
ocr_results = reader.readtext(image_path, detail=1, paragraph=False)
```

`ocr_results` 中的每筆資料長這樣：

```python
[
    ((x1, y1, x2, y2, x3, y3, x4, y4), "Detected text", 0.92),
    ...
]
```

第三個元素（範例中的 `0.92`）即為 0~1 之間的信心分數。

### 步驟 3：彙總整體信心分數

與前面的程式只印出單一 `confidence` 屬性不同，EasyOCR 為每個字詞提供信心分數。為了快速掌握整體情況，我們會取平均值：

```python
# Extract just the confidence numbers
confidences = [item[2] for item in ocr_results]

# Compute the mean confidence (overall confidence)
overall_confidence = sum(confidences) / len(confidences) if confidences else 0

print(f"Overall confidence: {overall_confidence:.2%}")
```

*為什麼要取平均？* 這能快速檢查健康狀況——若整體信心低於 70 % 左右，可能需要改善圖像（例如提升光線、前處理等）。

### 步驟 4：列出低信心字詞

接下來就是直接回應「列出信心低於設定門檻的字詞」需求的部分。我們預設 **OCR 信心閾值** 為 0.80（80 %），當然你可以自行調整。

```python
# Define the confidence threshold – tweak as needed
THRESHOLD = 0.80

print("\nLow‑confidence words:")
low_confidence_found = False
for bbox, text, conf in ocr_results:
    if conf < THRESHOLD:
        low_confidence_found = True
        print(f"  • '{text}' ({conf:.2%})")
if not low_confidence_found:
    print("  All words meet the confidence threshold.")
```

迴圈會印出每個未達門檻的字詞，並顯示其百分比信心。這正是原本 `for recognized_word in recognition_result.words` 迴圈的等價寫法，只是改用 EasyOCR 的輸出格式。

---

## ## 了解 OCR 信心分數

信心分數並非魔法數字；它是模型對特定轉錄結果的確定程度估計。以下幾點值得留意：

| 情境 | 典型信心分數 | 建議處理方式 |
|-----------|-------------------|------------|
| 清晰、高解析度的掃描 | 0.95 – 1.00 | 不需額外處理 |
| 輕微模糊或光線不均 | 0.80 – 0.94 | 考慮輕度前處理（提升對比） |
| 噪點嚴重、文字旋轉 | < 0.70 | 進行圖像前處理（去斜、去噪）或改用其他 OCR 引擎 |

> **注意：** 某些語言（例如手寫草寫）天生會得到較低分數，請依需求調整閾值。

### 邊緣案例與變化

1. **批次處理** – 若需 **對圖像執行 OCR** 的檔案大量處理，只要把上述邏輯包在遍歷目錄的迴圈中即可。  
2. **多語言** – 傳入 `['en', 'fr']` 給 `easyocr.Reader`，引擎會同時偵測兩種語言。  
3. **替代引擎** – 想試試 **pytesseract**？只要把讀取區塊換成：

   ```python
   import pytesseract
   from PIL import Image

   img = Image.open(image_path)
   raw_text = pytesseract.image_to_string(img, output_type=pytesseract.Output.DICT)
   # raw_text['text'] contains the full string,
   # raw_text['conf'] holds per‑character confidence.
   ```

   之後需要把每個字元的信心聚合成每個字詞的值——稍微多點工作但可行。

4. **前處理技巧** – 使用 OpenCV 濾鏡（`cv2.threshold`、`cv2.GaussianBlur`）可提升噪點掃描的信心分數。  

---

## ## 完整、可直接執行的腳本

以下是完整的 Python 檔案，你只要把它放入專案即可。存為 `ocr_report.py`，然後執行 `python ocr_report.py`。別忘了把圖像路徑改成實際檔案。

```python
#!/usr/bin/env python3
"""
run_ocr_on_image.py

A self‑contained script that:
  1. Runs OCR on an image using EasyOCR.
  2. Prints the overall confidence.
  3. Lists any words whose confidence falls below a configurable threshold.

Author: Your Name
Date: 2026‑06‑06
"""

import os
import easyocr

# --------------------------- Configuration --------------------------- #
IMAGE_DIR = "YOUR_DIRECTORY"          # <-- Change to your folder
IMAGE_NAME = "mixed_quality.png"      # <-- Change to your file name
THRESHOLD = 0.80                       # Confidence threshold (0‑1)

# --------------------------- Helper Functions ----------------------- #
def load_image_path():
    """Construct the absolute path to the target image."""
    return os.path.join(IMAGE_DIR, IMAGE_NAME)

def run_ocr(image_path):
    """Run OCR on the image and return detailed results."""
    reader = easyocr.Reader(['en'])
    return reader.readtext(image_path, detail=1, paragraph=False)

def compute_overall_confidence(results):
    """Return the mean confidence across all detected words."""
    if not results:
        return 0.0
    confidences = [item[2] for item in results]
    return sum(confidences) / len(confidences)

def report_low_confidence_words(results, threshold):
    """Print words whose confidence is below the given threshold."""
    low_conf = [(text, conf) for _, text, conf in results if conf < threshold]
    if not low_conf:
        print("All words meet the confidence threshold.")
    else:
        for text, conf in low_conf:
            print(f"Low‑confidence word: '{text}' ({conf:.2%})")

# --------------------------- Main Execution ------------------------ #
def main():
    image_path = load_image_path()
    if not os.path.isfile(image_path):
        print(f"❌ Image not found: {image_path}")
        return

    # Step 1: Run OCR on image
    ocr_results = run_ocr(image_path)

    # Step 2: Show overall confidence
    overall = compute_overall_confidence(ocr_results)
    print(f"Overall confidence: {overall:.2%}")

    # Step 3: List low‑confidence words
    print("\n--- Low‑confidence words (threshold: {0:.0%}) ---".format(THRESHOLD))
    report_low_confidence_words(ocr_results, THRESHOLD)

if __name__ == "__main__":
    main()
```

**預期輸出**（實際數字會因圖像而異）：

```
Overall confidence: 78.45%

--- Low‑confidence words (threshold: 80%) ---
Low‑confidence word: 'recgnition' (62.13%)
Low‑confidence word: 'imgae' (57.90%)
```

如果所有字詞都通過 80 % 門檻，會看到友善的「All words meet the confidence threshold.」訊息。

---

## ## 常見問題 (FAQ)

**Q: 這能直接處理 PDF 嗎？**  
A: 不能直接。先把每頁 PDF 轉成圖像（例如使用 `pdf2image`），再把產生的 PNG/JPEG 丟給腳本。

**Q: 我的信心分數全部很低，該怎麼辦？**  
A: 嘗試圖像前處理：提升對比、去除背景噪點，或將圖像旋轉至水平基線。EasyOCR 也接受 `contrast_ths` 參數，可自行微調。

**Q: 可以把結果匯出成 CSV 嗎？**  
A: 當然可以。在低信心迴圈之後，使用 `csv.DictWriter` 把 `ocr_results` 寫入 CSV，每列包含 `text`、`confidence` 與邊界框座標。

**Q: 有支援 GPU 加速的版本嗎？**  
A: 若安裝了相容的 GPU 與 PyTorch，EasyOCR 會自動使用 CUDA。執行前可用 `torch.cuda.is_available()` 先確認。

---

## 結論

我們剛剛 **對圖像執行 OCR**，檢視了整體信心，並挑出需要人工檢查的低信心字詞。

## 接下來該學什麼？

以下教學與本指南的技巧密切相關，能幫助你進一步掌握 API 功能，或探索其他實作方式：

- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)
- [How to Use Aspose OCR for JSON Result in Image Recognition](/ocr/english/net/text-recognition/get-result-as-json/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}