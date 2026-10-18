---
category: general
date: 2026-03-26
description: 學習如何校正圖像傾斜、辨識圖像文字，並建立影像前置處理流程以去除掃描噪點，將掃描圖像轉換為文字。
draft: false
keywords:
- how to deskew image
- recognize text from image
- image preprocessing pipeline
- remove noise from scan
- convert scanned image to text
language: zh-hant
og_description: 如何校正影像，將傾斜的掃描檔轉換為可搜尋的文字。請依照本指南辨識影像文字、去除掃描雜訊，並將掃描影像轉換為文字。
og_title: 如何校正圖像傾斜 – 逐步 OCR 指南
tags:
- OCR
- image-processing
- Python
title: 如何校正圖像傾斜 – OCR 完整指南
url: /zh-hant/python-java/general/how-to-deskew-image-complete-guide-with-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何校正影像傾斜 – 完整 OCR 指南

有沒有想過 **如何校正影像傾斜**，尤其是從廉價掃描器掃出的文件？你並不孤單。頁面歪斜看起來不專業，更重要的是，傾斜會讓任何 OCR 引擎在 **從影像辨識文字** 時出錯。

在本教學中，我們將一步步說明完整的 **影像前處理流程**，包括校正、二值化與去噪，最後交給 OCR 引擎，讓你 **將掃描影像轉換成文字**，省去繁雜的步驟。全程使用純 Python 以及一個小型函式庫完成繁重工作。

## 需要的環境

- Python 3.9+（程式碼在 3.10 及更新版本皆可執行）
- `ocr` 套件（使用 `pip install ocr‑toolkit` 安裝 – 請以實際套件名稱為主）
- 一張明顯傾斜的 JPEG 或 PNG 掃描檔（例如 `skewed_scan.jpg`）
- 對每個前處理步驟的作用有一點好奇心

就這些。除非你之後想更深入，否則不需要 OpenCV 等大型依賴。

## 步驟 1：載入掃描影像

首先要把檔案讀入記憶體。這一步看似簡單，卻是關鍵——路徑錯誤會導致整個流程失敗。

```python
# Step 1: Load the scanned image
image_path = "YOUR_DIRECTORY/skewed_scan.jpg"
original_image = ocr.Imaging.Image.load(image_path)
```

> **為什麼要這樣做？**  
> 載入影像後，我們會得到一個可操作的物件，供 `ocr.ImagePreprocessor` 使用。若跳過此步，後續管線將無法取得實際的像素資料。

## 如何校正影像傾斜並為 OCR 做好準備

現在影像已在手，接下來要把它旋正。`deskew()` 方法會估算傾斜角度，並將圖片旋回水平。

```python
# Step 2: Create an image preprocessor and correct the orientation
preprocessor = ocr.ImagePreprocessor()
preprocessor.deskew()
```

> **小技巧：** 若你的掃描只稍微偏離（≤ 3°），預設演算法通常已相當精準。角度過大時可能需要調整內部參數，請參考函式庫文件中 `max_angle` 的說明。

## 二值化影像 – 轉成黑白

OCR 引擎喜歡高對比度的輸入。將圖片轉為二值（黑白）可去除細微的灰階，避免干擾字元辨識。

```python
# Step 3: Convert the image to a binary (black‑and‑white) representation
preprocessor.binarize(threshold=128)
```

> **發生了什麼事？**  
> 像素值大於 128 的會變成白色，其他則變成黑色。若掃描檔特別暗或特別亮，可自行調整閾值。

## 去除掃描雜訊（在 OCR 前）

即使影像已校正，仍可能有斑點、塵埃或壓縮產生的雜訊。這些小斑點是 OCR 引擎的天敵。

```python
# Step 4: Reduce noise to improve OCR accuracy
preprocessor.denoise(radius=1)
```

> **為什麼要去噪？**  
> 雜訊會產生偽邊緣，讓 OCR 誤認為是字元。大多數掃描使用小半徑即可，若文件非常顆粒化，可適度增大半徑。

## 套用影像前處理管線

所有設定已完成——現在把管線套用到原始影像上。

```python
# Step 5: Apply the preprocessing pipeline to the loaded image
processed_image = preprocessor.apply(original_image)
```

> **結果：** `processed_image` 為已清理、校正、對比度提升的位圖，隨時可以進行文字抽取。

## 使用 OCR 引擎辨識影像文字

正式讀取文字。先初始化 OCR 引擎，將處理好的影像送入，最後取得原始字串。

```python
# Step 6: Initialise the OCR engine and provide the processed image
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(processed_image)

# Step 7: Recognise text and output the result
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

> **預期輸出**（範例）：

```
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

如果看到亂碼，請再次確認校正步驟或嘗試不同的 `threshold` 值。

## 建立完整的影像前處理管線 – 完整腳本

把所有步驟整合起來，以下是一個可直接存成 `.py` 並執行的完整腳本：

```python
import ocr  # Replace with the actual import path of your OCR library

# -------------------------------------------------
# 1️⃣ Load the scanned image
# -------------------------------------------------
image_path = "YOUR_DIRECTORY/skewed_scan.jpg"
original_image = ocr.Imaging.Image.load(image_path)

# -------------------------------------------------
# 2️⃣ Deskew – how to deskew image
# -------------------------------------------------
preprocessor = ocr.ImagePreprocessor()
preprocessor.deskew()

# -------------------------------------------------
# 3️⃣ Binarize – convert to black‑and‑white
# -------------------------------------------------
preprocessor.binarize(threshold=128)

# -------------------------------------------------
# 4️⃣ Denoise – remove noise from scan
# -------------------------------------------------
preprocessor.denoise(radius=1)

# -------------------------------------------------
# 5️⃣ Apply the pipeline
# -------------------------------------------------
processed_image = preprocessor.apply(original_image)

# -------------------------------------------------
# 6️⃣ OCR – recognize text from image
# -------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(processed_image)

# -------------------------------------------------
# 7️⃣ Output – convert scanned image to text
# -------------------------------------------------
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

> **提示：** 若要批次處理多個檔案，可將整段程式包在函式 `def ocr_from_file(path): …` 中。

## 常見問題與例外情況

- **如果影像本來就已經正立呢？**  
  `deskew()` 會偵測到接近零度的角度，直接跳過旋轉，故可放心對每個檔案都執行此步。

- **我的掃描是彩色的——要保留嗎？**  
  大多數 OCR 任務不需要彩色資訊。二值化會將其去除，提升處理速度並降低記憶體佔用。

- **可以串接多個前處理步驟嗎？**  
  當然可以。`ImagePreprocessor` 類別設計即支援管線，你可以在呼叫 `apply()` 前加入 `sharpen()`、`contrast_enhance()` 或自訂濾鏡。

- **OCR 輸出有多餘的換行——怎麼處理？**  
  可使用 `text.replace("\n", " ").strip()` 進行後處理，或改用 Tesseract 的 `--psm` 模式進行更進階的版面分析。

## 往下走

現在你已掌握 **如何校正影像傾斜**，並擁有穩固的 **影像前處理管線**，可以進一步探索：

- 將 **從影像辨識文字** 整合到 Flask API，實現即時文件上傳。
- 使用管線 **去除歷史文件的雜訊**，保護珍貴文獻。
- 大規模批次處理上千頁，並使用 `pdfminer` 或 `PyMuPDF` 輸出可搜尋的 PDF。

盡情嘗試不同的閾值、去噪半徑，或改換 OCR 後端（如 Tesseract）以支援多語言。基本流程不變：校正 → 清理 → 讀取。

---

*祝編程愉快！若有任何問題，歡迎在下方留言，我會很樂意協助你微調管線。*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}