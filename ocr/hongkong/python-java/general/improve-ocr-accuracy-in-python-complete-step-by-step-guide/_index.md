---
category: general
date: 2026-05-31
description: 使用 Python 透過影像前處理提升 OCR 準確度。學習如何從影像檔案提取文字、辨識 PNG 圖片中的文字，並提升結果表現。
draft: false
keywords:
- improve OCR accuracy
- preprocess image for OCR
- extract text from image
- recognize text from PNG
- image preprocessing for text
language: zh-hant
og_description: 透過對文字進行影像前處理，在 Python 中提升 OCR 準確度。跟隨本指南，即可輕鬆從影像檔案提取文字，並辨識 PNG 中的文字。
og_title: 提升 Python OCR 準確度 – 完整教學
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Improve OCR accuracy with Python by preprocessing images for OCR. Learn
    how to extract text from image files, recognize text from PNG, and boost results.
  headline: Improve OCR Accuracy in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Improve OCR accuracy with Python by preprocessing images for OCR. Learn
    how to extract text from image files, recognize text from PNG, and boost results.
  name: Improve OCR Accuracy in Python – Complete Step‑by‑Step Guide
  steps:
  - name: Loads the PNG into memory
    text: Loads the PNG into memory
  - name: Applies denoise and deskew based on our settings
    text: Applies denoise and deskew based on our settings
  - name: Runs the neural‑network or classic pattern matcher
    text: Runs the neural‑network or classic pattern matcher
  - name: Packages the output into `recognition_result`
    text: Packages the output into `recognition_result`
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: 提升 Python OCR 準確度 – 完整逐步指南
url: /zh-hant/python-java/general/improve-ocr-accuracy-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 提升 Python OCR 準確度 – 完整逐步指南

有沒有嘗試過 **提升 OCR 準確度**，結果卻得到一堆亂碼？你並不是唯一遇到這種情況的人。大多數開發者在原始影像噪點太多、傾斜或對比度低時，都會卡住。好消息是，只要使用幾個前處理技巧，就能把模糊的螢幕截圖變成乾淨、機器可讀的文字。

在本教學中，我們將示範一個 **為 OCR 前處理影像** 的真實案例，執行辨識引擎，最後 **從影像中擷取文字**（以 PNG 為例）。完成後，你將清楚知道如何 **從 PNG 辨識文字**，並擁有一段可直接套用到任何專案的可重用程式碼片段。

## 你將學到

- 為什麼影像前處理對 OCR 引擎至關重要  
- 哪些前處理模式（去噪、去斜）能帶來最大提升  
- 如何在 Python 中配置 `OcrEngine` 實例  
- 完整、可直接執行的腳本，**從影像中擷取文字**  
- 處理旋轉掃描或低解析度圖片等邊緣案例的技巧  

不需要除 OCR SDK 之外的額外函式庫，只要有 Python 3.8+ 與一張想要讀取的 PNG 影像即可。

---

![Diagram showing steps to improve OCR accuracy in Python](image.png "Improve OCR accuracy workflow")

*Alt text: 展示提升 OCR 準確度工作流程的圖示，說明前處理與辨識步驟。*

## 前置條件

- 已安裝 Python 3.8 或更新版本  
- 取得提供 `OcrEngine`、`OcrEngineSettings` 與 `ImagePreprocessMode` 的 OCR SDK（以下程式碼使用通用 API；如有需要請改為供應商的類別）  
- 一張 PNG 影像（`input.png`），放在可參照的資料夾內  

如果你使用虛擬環境，現在就啟動它——不需要特別的設定，只要執行 `python -m venv venv && source venv/bin/activate` 即可。

---

## 步驟 1：建立 OCR 引擎實例 – 開始提升 OCR 準確度

首先需要一個 OCR 引擎物件。它就像大腦，之後會讀取像素並輸出文字。

```python
# Step 1: Initialise the OCR engine
ocr_engine = OcrEngine()
```

為什麼這很重要：沒有引擎就無法套用任何前處理，原始影像會直接送給辨識器——通常是準確度最差的情況。

---

## 步驟 2：載入目標 PNG – 為 **從 PNG 辨識文字** 做好準備

接著告訴引擎要處理哪個檔案。PNG 為無損格式，已經比 JPEG 多了一點優勢。

```python
# Step 2: Load the image you want to process
ocr_engine.load_image("YOUR_DIRECTORY/input.png")
```

如果影像放在其他位置，只要調整路徑即可。引擎支援任何相容格式，但 PNG 常能保留文字邊緣的細節。

---

## 步驟 3：設定前處理 – 為 OCR 前處理影像

這裡就是魔法發生的地方。我們建立設定物件，開啟去噪以消除斑點，並啟用去斜讓傾斜的文字自動校正。

```python
# Step 3: Prepare preprocessing settings to improve accuracy
preprocess_settings = OcrEngineSettings()
preprocess_settings.preprocess_mode = (
    ImagePreprocessMode.DENOISE | ImagePreprocessMode.DESKEW
)
```

### 為什麼同時使用去噪 + 去斜？

- **去噪**：隨機像素雜訊會干擾模式匹配演算法。移除雜訊可讓字母更銳利。  
- **去斜**：即使只有 2 度的傾斜，也會大幅降低信心分數。去斜會校正基線，讓辨識器更可靠地匹配字型。

如果你的影像特別暗，還可以嘗試加入其他旗標（例如 `ImagePreprocessMode.CONTRAST_ENHANCE`）。SDK 文件通常會列出所有可用模式。

---

## 步驟 4：將設定套用至引擎 – 把前處理綁定到 OCR

把設定物件指派給引擎，讓下一次辨識時會使用我們剛剛定義的轉換。

```python
# Step 4: Apply the settings to the engine
ocr_engine.settings = preprocess_settings
```

若跳過此步驟，引擎會回退到預設（通常是「不做前處理」），導致 **OCR 準確度下降**。

---

## 步驟 5：執行辨識程序 – **從影像中擷取文字**

所有設定完成後，我們終於請引擎執行工作。此呼叫為同步，會回傳包含辨識結果字串的物件。

```python
# Step 5: Run the recognition process
recognition_result = ocr_engine.recognize()
```

在背後，引擎會依序：

1. 將 PNG 載入記憶體  
2. 依設定套用去噪與去斜  
3. 執行神經網路或傳統模式匹配  
4. 把輸出封裝成 `recognition_result`

---

## 步驟 6：輸出辨識文字 – 驗證提升效果

把擷取出的字串印出來。實際應用中，你可能會寫入檔案、資料庫，或傳給其他服務。

```python
# Step 6: Output the recognized text
print(recognition_result.text)
```

### 預期輸出

如果影像內的句子是 “Hello, OCR World!” 則應看到：

```
Hello, OCR World!
```

可以看到文字乾淨整齊——沒有雜訊或斷裂的字元。這正是正確 **影像前處理** 所帶來的效果。

---

## 專業技巧與邊緣案例

| 情境 | 調整方式 | 原因 |
|-----------|----------------|-----|
| 非常低解析度的 PNG（≤ 72 dpi） | 若支援，加入 `ImagePreprocessMode.SUPER_RESOLUTION` | 放大後可提供辨識器更多像素供分析 |
| 文字旋轉 > 5° | 提高去斜容忍度或使用 `Pillow` 先手動旋轉後再送入引擎 | 大角度可能會跳過自動去斜 |
| 背景圖案繁雜 | 開啟 `ImagePreprocessMode.BACKGROUND_REMOVAL` | 去除非文字雜訊，避免誤讀 |
| 多語言文件 | 設定 `ocr_engine.language = "eng+spa"`（或類似） | 引擎會載入正確的字元集，提升整體準確度 |

記住，**提升 OCR 準確度** 並非一刀切；你可能需要針對自己的資料集不斷調整前處理旗標。

---

## 完整腳本 – 直接複製貼上使用

以下是結合所有步驟的完整、可執行範例。將它存為 `improve_ocr_accuracy.py`，再以 `python improve_ocr_accuracy.py` 執行。

```python
"""
Improve OCR Accuracy in Python – Full Example
Author: Your Name (2026)
Requires: OCR SDK providing OcrEngine, OcrEngineSettings, ImagePreprocessMode
"""

# Import the necessary classes from the OCR SDK
from ocr_sdk import OcrEngine, OcrEngineSettings, ImagePreprocessMode

def main():
    # 1️⃣ Initialise the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load the PNG you want to read
    image_path = "YOUR_DIRECTORY/input.png"
    ocr_engine.load_image(image_path)

    # 3️⃣ Configure preprocessing: denoise + deskew
    preprocess_settings = OcrEngineSettings()
    preprocess_settings.preprocess_mode = (
        ImagePreprocessMode.DENOISE | ImagePreprocessMode.DESKEW
    )

    # 4️⃣ Apply the settings
    ocr_engine.settings = preprocess_settings

    # 5️⃣ Run recognition
    recognition_result = ocr_engine.recognize()

    # 6️⃣ Print the extracted text
    print("=== Recognized Text ===")
    print(recognition_result.text)

if __name__ == "__main__":
    main()
```

執行後觀察主控台，你會立即看到 **從影像中擷取文字** 的結果。若輸出不理想，請依照「專業技巧」表格調整 `preprocess_mode` 旗標。

---

## 結論

我們剛剛示範了一套實用配方，透過 Python **提升 OCR 準確度**。只要建立 `OcrEngine`、載入 PNG、**為 OCR 前處理影像**，最後 **從 PNG 辨識文字**，即使來源影像不完美，也能可靠地 **從影像中擷取文字**。

接下來可以嘗試將多張影像放入迴圈處理、把結果寫入 CSV，或測試其他前處理模式（如對比度增強）。相同流程同樣適用於 PDF、掃描收據或手寫筆記——只要換掉輸入來源並調整設定即可。

對特定影像類型有疑問，或想了解如何整合到 Web 服務中？歡迎留言，我們一起探討。祝程式開發順利，OCR 結果永遠清晰無誤！

## 接下來該學什麼？

- [從影像中擷取文字 – Aspose OCR 步驟指南](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [從影像中擷取文字 – Aspose.OCR for .NET OCR 最佳化](/ocr/english/net/ocr-optimization/)
- [如何透過在 OCR 中準備矩形來擷取文字](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}