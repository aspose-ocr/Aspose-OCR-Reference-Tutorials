---
category: general
date: 2026-06-28
description: 使用 Python 進行 OCR 前處理，包括自動旋轉、二值化與去噪。使用 OCR 引擎取得結構化的 JSON 輸出。
draft: false
keywords:
- preprocess image for OCR
- auto rotate image OCR
- OCR engine Python
- OCR structured JSON output
- image binarization for OCR
- denoise OCR image
language: zh-hant
og_description: 使用 Python 進行 OCR 前處理，包括自動旋轉、二值化與去噪。學習如何使用 OCR 引擎提取結構化的 JSON。
og_title: 預處理圖像以進行 OCR – 完整 Python 指南
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Preprocess image for OCR with auto‑rotate, binarization and denoising
    in Python. Get structured JSON output using an OCR engine.
  headline: Preprocess Image for OCR – Complete Python Guide
  type: TechArticle
- description: Preprocess image for OCR with auto‑rotate, binarization and denoising
    in Python. Get structured JSON output using an OCR engine.
  name: Preprocess Image for OCR – Complete Python Guide
  steps:
  - name: '**Binarization** – converting the picture to pure black‑and‑white, which
      sharpens character edges.'
    text: '**Binarization** – converting the picture to pure black‑and‑white, which
      sharpens character edges.'
  - name: '**Denoising** – removing speckles that the OCR engine might mistake for
      glyphs.'
    text: '**Denoising** – removing speckles that the OCR engine might mistake for
      glyphs.'
  - name: '**Add language packs** (`engine.set_language(''eng+spa'')`) for multilingual
      documents.'
    text: '**Add language packs** (`engine.set_language(''eng+spa'')`) for multilingual
      documents.'
  - name: '**Integrate with Pandas** to turn the JSON tables into DataFrames for analytics.'
    text: '**Integrate with Pandas** to turn the JSON tables into DataFrames for analytics.'
  - name: '**Run batch processing** by looping over a folder of images and appending
      results to a master JSON file.'
    text: '**Run batch processing** by looping over a folder of images and appending
      results to a master JSON file.'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: OCR 圖像預處理 – 完整 Python 指南
url: /zh-hant/python/general/preprocess-image-for-ocr-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 預處理影像以供 OCR – 完整 Python 指南

有沒有想過如何 **preprocess image for OCR**，讓引擎真的能讀取你所看到的內容？你並不孤單——大多數開發者在掃描文件變得亂碼時，都會碰到同樣的問題。好消息是？只要幾個恰當的步驟——auto‑rotate、binarization 與 denoising——就能把雜亂的照片變成乾淨、機器可讀的文字。

在本教學中，我們將逐步說明一個 **Python** 工作流程，不僅會清理影像，還會回傳結構化的 JSON 檔案。完成後，你將會知道如何為 OCR 進行自動旋轉、套用影像二值化，以及在將影像資料送入 **OCR engine Python** 實例前進行去噪。

## 需要的工具

在深入之前，請確保你的機器上已安裝以下項目：

- Python 3.9+（任何較新版本皆可）
- `Pillow` 用於影像處理（`pip install pillow`）
- `ocrutil` – 一個虛構的工具庫，用於包裝 OCR 引擎（透過 `pip install ocrutil` 安裝）
- 一張示範的斜向影像（`skewed.jpg`），放在可供參考的資料夾中

就這樣——不需要大型框架，也不需要 GPU 加速。只要純粹的 Python 加上幾個好用的函式庫即可。

## 第一步：載入影像 – 為 OCR 做準備

首先，我們需要一個影像物件，讓後續的流程可以處理。

```python
from PIL import Image
import ocrutil

# Load the image you want to process
img_path = "YOUR_DIRECTORY/skewed.jpg"
img = Image.open(img_path)          # Pillow gives us a convenient Image object
print(f"Loaded image size: {img.size}")
```

*為什麼這很重要:* 使用 Pillow 載入影像可確保保留所有原始像素資料，這在之後執行二值化時至關重要。跳過此步驟或使用低品質的載入器可能已經會破壞 OCR 的準確度。

## 第二步：為 OCR 自動旋轉影像（auto rotate image OCR）

手機拍攝的照片常常會傾斜，甚至顛倒。`ocrutil.auto_rotate` 輔助函式會偵測文字基線，並相應地旋轉影像。

```python
# Automatically correct 90°/180° rotation
img = ocrutil.auto_rotate(img)
print("Auto‑rotation applied.")
```

*小技巧:* 如果你知道文件永遠都是正立的，可以跳過此步驟，但在實務上 “auto rotate image OCR” 能為你省下大量手動清理的時間。

## 第三步：預處理影像以供 OCR – 二值化 + 去噪

現在我們進入重點：**preprocess image for OCR**。最有效的兩個技巧是：

1. **Binarization** – 將圖片轉換為純黑白，提升字元邊緣的清晰度。
2. **Denoising** – 移除可能被 OCR 引擎誤認為字形的斑點。

```python
# Apply preprocessing: binarization + denoising
img = ocrutil.preprocess(img)   # Under the hood: thresholding + median filter
print("Preprocessing completed.")
```

如果你在此步驟後檢視影像（例如 `img.show()`），會發現背景與前景的對比度大幅提升——這正是優秀 OCR 引擎所渴求的。

## 第四步：設定 OCR 引擎（OCR engine Python）

取得乾淨的影像後，我們就可以實例化 OCR 引擎。`ocrutil.OcrEngine` 類別封裝了一個流行的開源 OCR 後端（例如 Tesseract），同時提供友善的 Python API。

```python
# Create and configure the OCR engine
engine = ocrutil.OcrEngine()
engine.set_image(img)           # Feed the preprocessed image
print("Engine ready for recognition.")
```

*為什麼這麼做:* 將預處理過的影像提供給 **OCR engine Python** 物件，可確保引擎使用你能提供的最高品質資料，直接提升辨識準確度。

## 第五步：純文字辨識（可選但實用）

有時你只需要原始文字。此步驟為可選，因為本教學的主要目標是結構化輸出，但它對快速驗證結果很有幫助。

```python
# Get plain text (useful for debugging)
plain_text = engine.recognize()
print("Plain‑text output:\n", plain_text[:200])   # Print first 200 chars
```

你會看到一段看起來與原始文件相似的字串，但不含任何版面資訊。如果文字顯示為亂碼，請回到前一步調整預處理參數。

## 第六步：擷取結構化資料並儲存為 JSON（OCR structured JSON output）

現代 OCR 引擎的真正威力在於它們能返回版面資訊——表格、欄位，甚至表單欄位。`engine.recognize_structured()` 正是執行此功能，我們會將結果匯出為整齊的 JSON 檔案。

```python
# Recognize structured data (tables, layout) and export to JSON
structured_result = engine.recognize_structured()
output_path = "YOUR_DIRECTORY/out.json"
ocrutil.save_result(structured_result, output_path)
print(f"Structured OCR result saved to {output_path}")
```

JSON 的片段可能長這樣：

```json
{
  "pages": [
    {
      "blocks": [
        {
          "type": "text",
          "bbox": [12, 34, 560, 120],
          "text": "Invoice #12345"
        },
        {
          "type": "table",
          "bbox": [15, 130, 580, 400],
          "rows": [
            ["Item", "Qty", "Price"],
            ["Widget A", "2", "$19.99"]
          ]
        }
      ]
    }
  ]
}
```

*這樣做的好處:* 你得到一個機器可讀的表示，可直接匯入資料庫、API 或報表工具——不再需要手動複製貼上。

## 加分項：視覺確認（含替代文字的影像）

以下是預處理流程的前後快照。請注意對比度的提升與噪點的消失。

![預處理影像以供 OCR – 原始 vs 清理後](/images/ocr_preprocess_example.png){: .align-center alt="預處理影像 OCR 範例"}

*如果你感到好奇:* 將 `ocrutil.preprocess` 換成自己的 OpenCV 程式，也仍然遵循相同的 **preprocess image for OCR** 原則——先閾值化、再過濾，最後送入。

## 常見陷阱與避免方法

- **Over‑binarizing:** 設定過高的閾值會抹掉淡弱的字元。如果發現字母缺失，請在 `ocrutil.preprocess` 中降低閾值。
- **Wrong DPI:** OCR 引擎假設列印文件的解析度約為 300 dpi。若影像解析度過低，請考慮在預處理前先放大。
- **Skipping auto‑rotate:** 即使是 5 度的傾斜也會影響行偵測。 “auto rotate image OCR” 這一步成本低，能省下後續大量除錯時間。

## 擴充工作流程

現在你已經有了穩固的基礎，接下來可能想要：

1. **Add language packs** (`engine.set_language('eng+spa')`) 以支援多語言文件。  
2. **Integrate with Pandas**，將 JSON 表格轉換為 DataFrame 以進行分析。  
3. **Run batch processing**，透過迴圈處理資料夾內的影像，並將結果附加至主 JSON 檔案。

所有這些擴充仍然依賴核心概念：在呼叫引擎之前先 **preprocess image for OCR**。

## 結論

你剛剛學會了如何在 Python 中 **preprocess image for OCR**——自動旋轉、二值化、去噪，最後將乾淨的影像交給 **OCR engine Python**，它會輸出純文字與豐富的 **OCR structured JSON output**。遵循這些步驟，你將大幅提升辨識率，並取得可直接用於後續處理的資料。

想要更上一層樓嗎？試著將內建的 `ocrutil.preprocess` 換成自訂的 OpenCV 流程，實驗不同的二值化技術，或將 JSON 匯入報表儀表板。沒有極限，而你剛建立的基礎將避免再次因影像品質問題卡關。

祝程式開發順利，願你的 OCR 結果永遠清晰！

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，並以此為基礎。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在自己的專案中探索其他實作方式。

- [使用 Aspose OCR 從影像擷取文字 – 步驟指南](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [從影像擷取文字 – 使用 Aspose.OCR for .NET 進行 OCR 最佳化](/ocr/english/net/ocr-optimization/)
- [如何設定 OCR 影像辨識的閾值](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}