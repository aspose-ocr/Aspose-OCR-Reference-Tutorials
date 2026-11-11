---
category: general
date: 2026-03-26
description: 學習如何在 Python 中執行 OCR，並從圖像檔案辨識文字。本指南示範如何從 PNG 提取文字，快速將圖像轉換為文字。
draft: false
keywords:
- how to perform ocr
- recognize text from image
- extract text from png
- ocr tutorial python
- convert image to text
language: zh-hant
og_description: 如何在 Python 中執行 OCR？跟隨本指南，從圖像辨識文字、從 PNG 提取文字，並使用試用授權將圖像轉換為文字。
og_title: 如何在 Python 中進行 OCR – 完整教學
tags:
- OCR
- Python
- Image Processing
title: 如何在 Python 中執行 OCR – 完整逐步教學
url: /zh-hant/python-java/general/how-to-perform-ocr-in-python-complete-step-by-step-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中執行 OCR – 完整逐步教學  

有沒有想過 **如何對剛用手機拍下的圖片執行 OCR**？你並不孤單——全球的開發者都需要一種可靠的方式，從影像檔案中辨識文字，而不必與複雜的原生函式庫糾纏。  

在本教學中，我們將示範一個實作範例，說明 **如何執行 OCR**、**從影像中辨識文字**，以及 **從 PNG 取出文字**，全程使用輕量的 Python 包裝器。完成後，你只需要幾行程式碼就能 **將影像轉換為文字**，而且不必擔心授權問題，因為我們會使用內建的試用模式。

## 你將學會什麼  

* 如何為 OCR 引擎設定試用授權（不需要檔案路徑）。  
* **從影像中辨識文字** 物件的完整呼叫順序。  
* **從 PNG 取出文字** 的方法，以及處理常見問題（例如缺少字型）。  
* 從試用版升級至正式授權時的擴充技巧。  

**先備條件** – 需要 Python 3.8+ 與 `ocr` 套件（可透過 `pip install ocr` 安裝）。不需要其他外部工具。

---  

![如何在 Python 中執行 OCR 範例](https://example.com/ocr-demo.png "如何在 Python 中執行 OCR – 顯示辨識文字")  

*圖片說明：如何在 Python 中執行 OCR – 範例輸出*  

## 步驟 1 – 啟用試用授權（不需檔案路徑）  

在引擎能讀取任何內容之前，需要一個有效的授權。試用模式非常適合實驗與小型專案。

```python
# Step 1: Activate a trial license (no file path needed for trial mode)
import ocr

trial_license = ocr.TrialLicense()
trial_license.apply()
```

*為什麼重要：* 授權物件告訴 OCR 函式庫你正處於沙盒環境。如果省略此步驟，當你呼叫 `recognize()` 時，引擎會拋出 `LicenseError`。  

**小技巧：** 當你升級為付費授權時，將上面的兩行改為 `ocr.License("path/to/your/license.key").apply()`。

## 步驟 2 – 建立 OCR 引擎實例  

試用授權啟動後，我們建立主要的引擎。可以把它想像成會「看」影像並判斷字元位置的「大腦」。

```python
# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()
```

*為什麼重要：* `OcrEngine` 內含語言套件、DPI 設定等組態。之後可以自行調整，但預設已能處理大多數僅含英文的 PNG。

## 步驟 3 – 載入要處理的 PNG  

這一步就是 **從影像中辨識文字**。`ocr.Imaging.Image.load()` 方法支援 PNG、JPEG、BMP 等多種格式。

```python
# Step 3: Load the image you want to recognize
input_image = ocr.Imaging.Image.load("YOUR_DIRECTORY/sample1.png")
ocr_engine.set_image(input_image)
```

*邊緣情況：* 若你的 PNG 使用索引調色盤（螢幕截圖常見），載入器會自動轉換為 24 位元 RGB 緩衝。此轉換會稍微影響效能，但可確保 OCR 結果的正確性。

## 步驟 4 – 執行 OCR 並取得文字  

最後，我們讓引擎執行辨識，然後抓取純文字結果。

```python
# Step 4: Perform OCR and print the recognized text
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

**預期輸出**（以下為簡單圖像「Hello World」的範例）：

```
Hello World
```

若影像包含多行文字，輸出會保留換行，方便直接供 CSV 解析器或 NLP 流程使用。

## 可選：微調以提升準確度  

* **語言套件：** `ocr_engine.set_language("eng")`（預設）或 `"fra"`（法文）。  
* **DPI 調整：** `ocr_engine.set_dpi(300)` 可改善低解析度掃描的結果。  
* **前處理：** 在 `set_image` 前使用二值化閾值 (`ocr.Imaging.Image.threshold()`) 常能在雜訊背景下得到更乾淨的文字。

當你從快速示範升級為每日處理上百檔的 **ocr tutorial python** 時，這些調整相當有用。

## 完整腳本 – 直接複製貼上使用  

以下是結合上述所有步驟的完整可執行腳本。將其存為 `run_ocr.py`，並將 `YOUR_DIRECTORY/sample1.png` 替換為你自己的 PNG 路徑。

```python
# run_ocr.py
# Complete example showing how to perform OCR, recognize text from image,
# and extract text from PNG using the ocr Python package.

import ocr

def main():
    # Activate trial license
    trial_license = ocr.TrialLicense()
    trial_license.apply()

    # Create engine
    ocr_engine = ocr.OcrEngine()

    # Load image (PNG, JPEG, etc.)
    image_path = "YOUR_DIRECTORY/sample1.png"
    input_image = ocr.Imaging.Image.load(image_path)
    ocr_engine.set_image(input_image)

    # Run OCR
    result = ocr_engine.recognize().get_text()
    print("=== Recognized Text ===")
    print(result)

if __name__ == "__main__":
    main()
```

在命令列執行：

```bash
python run_ocr.py
```

執行後應會在終端機印出擷取的文字。若得到空字串，請再次確認影像確實含有清晰、高對比度的文字，且試用授權已正確套用且未出錯。

## 常見問題與注意事項  

* **「支不支援 JPEG？」** – 完全支援。`load()` 方法會自動偵測格式，換成 JPEG 不需要修改程式碼。  
* **「影像如果是旋轉的怎麼辦？」** – 引擎能自動偵測方向，但為取得最佳結果，可在 `set_image` 前使用 `input_image.rotate(90)` 先行旋轉。  
* **「可以在迴圈中處理多張影像嗎？」** – 可以。只要把載入與 `recognize()` 的程式碼搬進 `for` 迴圈，`ocr_engine` 實例即可重複使用，稍微減少開銷。  

## 往後的步驟 – 從示範到正式上線  

既然已掌握 **如何在 Python 中執行 OCR**，可以進一步探討以下主題：

* **批次處理** – 結合 `os.listdir()` 讓程式 **從 PNG 取出文字**，一次處理大量檔案。  
* **與 PDF 整合** – 使用 `pdf2image` 先把 PDF 頁面轉成 PNG，再交給相同的管線。  
* **後處理** – 用正規表達式或模糊比對清理常見的 OCR 錯誤（例如「0」與「O」混淆）。  

以上皆建立在 **將影像轉換為文字** 的核心概念上，讓你的 OCR 工作流程更具彈性與效能。

---  

### TL;DR  

我們已說明在 Python 中 **如何執行 OCR** 的全部步驟：啟用試用授權、建立引擎、載入 PNG、執行辨識、印出結果。只需幾行程式碼，就能 **從影像中辨識文字**、**從 PNG 取出文字**，並 **將影像轉換為文字**，供任何後續應用使用。  

快試試看，調整 DPI 或語言設定，讓引擎幫你完成繁重的工作。祝開發順利！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}