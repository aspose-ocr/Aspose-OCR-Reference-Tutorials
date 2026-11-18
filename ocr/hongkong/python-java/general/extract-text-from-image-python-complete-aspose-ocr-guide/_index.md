---
category: general
date: 2026-05-03
description: 使用 Aspose OCR 於 Python 從圖像提取文字。學習一步一步的 Python OCR 教學，支援混合拉丁文與西里爾文。
draft: false
keywords:
- extract text from image python
- Aspose OCR Python
- image to text conversion
- mixed language OCR
- Python OCR tutorial
language: zh-hant
og_description: 快速使用 Python 從圖像中提取文字。本指南說明如何在 Python 中使用 Aspose OCR 處理混合拉丁文‑西里爾文圖像。
og_title: 使用 Python 從圖像提取文字 – 完整 Aspose OCR 教學
tags:
- OCR
- Python
- Aspose
title: 使用 Python 從圖像提取文字 – 完整的 Aspose OCR 指南
url: /zh-hant/python-java/general/extract-text-from-image-python-complete-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從圖像提取文字 Python – 完整 Aspose OCR 指南

是否曾需要 **extract text from image python** 但不確定哪個函式庫能處理拉丁文與西里爾文混合的字符？你並非唯一遇到此問題的人——開發者在對多語言截圖進行 OCR 時常會卡住這個難題。  

好消息是 Aspose OCR for Python 讓整個流程幾乎毫不費力。在本教學中，我們將逐步說明如何安裝套件、套用授權、載入混合語言的圖像，最後只需幾行程式碼即可取得辨識出的文字。完成後，你將擁有一個可直接執行的腳本，隨時可嵌入任何專案。

## 你將學會

- 如何在虛擬環境中設定 **Aspose OCR Python**。  
- 為何提示語言（如拉丁文與西里爾文）能加快偵測速度。  
- 使用單一函式呼叫即可完成 **extract text from image python** 的完整程式碼。  
- 處理混合語言 OCR 時常見的陷阱以及避免方法。

### 前置條件

- 已在機器上安裝 Python 3.8 或更新版本。  
- Aspose OCR 授權檔 (`Aspose.OCR.Java.lic`)。免費試用可用於測試，但正式授權可移除浮水印。  
- 包含拉丁文與西里爾文字符的 PNG/JPEG 圖像（此處稱為 `mixed_latin_cyrillic.png`）。

只要上述條件皆符合，即可開始——不需要額外框架或龐大相依套件。

---

## 第一步 – Extract Text from Image Python：安裝 Aspose OCR

首先，從 PyPI 取得函式庫，並確保環境能找到授權檔。

```bash
# Create a clean virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate

# Install the Aspose OCR package
pip install asposeocrcloud
```

> **專業提示：** 若遇到權限錯誤，請在 `pip install` 指令後加上 `--user`，或以系統管理員身分執行終端機。

套件安裝完成後，我們將匯入它並將引擎指向授權檔。

```python
import asposeocrcloud as ocr   # the library we just installed

# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Apply your license – replace the path with the actual location of your .lic file
ocr_engine.license = ocr.License()
ocr_engine.license.set_license(r"YOUR_DIRECTORY/Aspose.OCR.Java.lic")
```

為什麼此時需要授權？若未提供授權，引擎會以 **evaluation mode** 運作，會限制頁數並在輸出加入浮水印。提前提供授權可確保之後的 `recognize` 呼叫返回純淨文字。

## 第二步 – 載入含混合拉丁‑西里爾文字的圖像

接著，我們將圖像載入記憶體。Aspose OCR 使用自有的 `Image` 類別，抽象化底層檔案格式。

```python
# Load the image that contains both Latin and Cyrillic characters
input_image = ocr.Image.from_file(r"YOUR_DIRECTORY/mixed_latin_cyrillic.png")
```

如果你在想其他格式是否支援——答案是肯定的，JPEG、BMP、TIFF，甚至 PDF 都受支援。只要更換檔案副檔名，`from_file` 方法即可自動處理。

## 第三步 – 提示語言以加速偵測（可選但有幫助）

當你知道圖像中包含哪些語言時，可提前告訴引擎。此步驟非必須，但能 **顯著縮短處理時間** 並提升混合語言 OCR 的準確度。

```python
# Provide language hints: Latin and Cyrillic
ocr_engine.config.language_hints = ["Latin", "Cyrillic"]
```

提示清單接受 Aspose OCR 支援的任何語言（例如 `"Arabic"`、`"Japanese"`）。若省略此步驟，引擎會嘗試所有內建語言，對大量批次而言會較慢。

## 第四步 – 執行 OCR 引擎並提取文字

現在是關鍵時刻：實際辨識字符。`recognize` 方法會回傳一個 `OcrResult` 物件，內含純文字、信心分數，若需要亦可取得文字框的座標。

```python
# Perform OCR on the loaded image
ocr_result = ocr_engine.recognize(input_image)

# The recognised text is available via the .text attribute
extracted_text = ocr_result.text
```

> **為什麼這樣可行：** Aspose OCR 內部結合了神經網路文字偵測器與語言特定的分類器。將 `Image` 物件直接餵入，即可省去手動前處理（如二值化）的需求。

## 第五步 – 查看提取的文字

最後，將結果印到主控台。實際應用中，你可能會將其寫入檔案、寫入資料庫，或傳給翻譯 API。

```python
print("Recognised text:")
print(extracted_text)
```

執行腳本後，應會看到類似以下的輸出：

```
Recognised text:
Hello мир! This is a test.
```

此輸出證明我們成功 **extract text from image python**，在一次處理中同時辨識拉丁文與西里爾文字符。

## 完整範例程式

以下是完整腳本，可直接複製貼上至名為 `extract_ocr.py` 的檔案。僅需將佔位路徑替換為實際目錄即可。

```python
import asposeocrcloud as ocr   # package installed via pip

# ------------------------------------------------------------
# Step 1 – Initialise engine and apply license
# ------------------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.license = ocr.License()
ocr_engine.license.set_license(r"YOUR_DIRECTORY/Aspose.OCR.Java.lic")   # path to your license file

# ------------------------------------------------------------
# Step 2 – Load the image (mixed Latin‑Cyrillic)
# ------------------------------------------------------------
input_image = ocr.Image.from_file(r"YOUR_DIRECTORY/mixed_latin_cyrillic.png")

# ------------------------------------------------------------
# Step 3 – (Optional) Hint the languages present
# ------------------------------------------------------------
ocr_engine.config.language_hints = ["Latin", "Cyrillic"]

# ------------------------------------------------------------
# Step 4 – Run OCR
# ------------------------------------------------------------
ocr_result = ocr_engine.recognize(input_image)

# ------------------------------------------------------------
# Step 5 – Display the recognised text
# ------------------------------------------------------------
print("Recognised text:")
print(ocr_result.text)
```

儲存檔案，啟動虛擬環境，然後執行：

```bash
python extract_ocr.py
```

你應會看到辨識出的文字被印出，證明腳本全程運作正常。

## 常見問題與特殊情況

**如果圖像模糊怎麼辦？**  
Aspose OCR 內建去斜與降噪功能，但對於嚴重退化的照片，建議先使用 OpenCV 前處理（例如套用高斯模糊與閾值化）。`Image` 類別亦可接受 NumPy 陣列，讓你在呼叫 `recognize` 前串接自訂濾鏡。

**我可以一次處理整個資料夾的圖像嗎？**  
當然可以。將邏輯包在 `for` 迴圈中，將 `from_file` 改為讀取每個檔名，並將結果存入字典。若使用雲端版，請留意 API 的速率限制。

**每種語言需要單獨的授權嗎？**  
不需要，單一 Aspose OCR 授權即可涵蓋所有支援語言。`language_hints` 清單僅為效能提示。

**PDF 輸入怎麼處理？**  
將 `Image.from_file` 改為 `ocr.Image.from_file("document.pdf")`。OCR 引擎會自動將每頁光柵化，並回傳合併後的文字。

## 結論

我們剛示範了一個簡潔、可投入生產的方式，使用 Aspose OCR **extract text from image python**。安裝、授權、載入、提示語言、辨識與顯示這幾個步驟，已涵蓋取得混合拉丁‑西里爾文字可靠結果所需的一切。  

接下來，你可以探索進階主題，例如批次處理的 **image to text conversion**、將輸出結合 **Python OCR tutorial** 用於自然語言處理，或嘗試其他語言提示以處理多語言文件。只要發揮創意，程式碼已在手中，無所不能。  

有其他使用情境或遇到問題嗎？留下評論、分享你的經驗，讓我們持續交流。祝開發順利！  

![Extract text from image python 範例](/images/extract-text-from-image-python.png "顯示 OCR 輸出的螢幕截圖 – extract text from image python")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}