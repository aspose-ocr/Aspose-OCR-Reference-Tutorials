---
category: general
date: 2026-07-05
description: 使用 Python OCR 從圖像提取文字。學習如何辨識圖像文字、載入圖像進行 OCR，以及僅用幾行程式碼設定 OCR 語言。
draft: false
keywords:
- extract text from image
- how to recognize text from image
- load image for ocr
- create ocr engine python
- set ocr language
language: zh-hant
og_description: 使用 Python OCR 從圖像提取文字。本指南說明如何辨識圖像中的文字、載入圖像進行 OCR、以 Python 方式建立 OCR
  引擎，以及設定 OCR 語言。
og_title: 在 Python 中從圖像提取文字 – 快速辨識文字
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract text from image using Python OCR. Learn how to recognize text
    from image, load image for OCR, and set OCR language in just a few lines.
  headline: Extract Text from Image in Python – Recognize Text Fast
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: 在 Python 中從圖像提取文字 – 快速辨識文字
url: /zh-hant/python-java/general/extract-text-from-image-in-python-recognize-text-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從圖像中提取文字（Python） – 快速辨識文字

有沒有曾經需要**從圖像中提取文字**，卻不知道該選哪個函式庫？如果你曾經問過自己*如何在不使用外部工具的情況下辨識圖像文字*，那麼你來對地方了。在本教學中，我們會啟動一個小型 OCR 引擎，指向一張圖片，並把文字抽取出來——僅此而已。

我們會一步步說明：**create OCR engine python**、**set OCR language**、**load image for OCR**、非同步觸發辨識，最後讀取結果。完成後，你將擁有一個獨立的腳本，可直接放入任何專案，無論是文件數位化工具或是讀取 meme 的聊天機器人。

## 你需要的環境

- Python 3.8+（此程式碼亦可在 3.10 及更新版本執行）  
- `ocr` 套件（Tesseract 的輕量封裝 – 使用 `pip install ocr` 或你偏好的分支安裝）  
- 含有可辨識文字的圖像檔案（`.jpg`、`.png` 等）  
- 稍微等一下非同步部分（很快的，保證）

就這樣——沒有大型相依套件，亦不需要原生編譯。如果你的系統已安裝 Tesseract，`ocr` 包裝器會自動偵測到它。

## 步驟 1：建立 OCR 引擎 – 抽取的核心

首先，你需要一個能與底層 OCR 引擎溝通的 engine 物件。可以把它想像成之後處理圖片的「大腦」。

```python
import ocr

# Step 1: Instantiate the OCR engine
engine = ocr.OcrEngine()
```

*為什麼這很重要*：沒有 engine，就無法設定語言或使用非同步功能。`OcrEngine` 類別將底層對 Tesseract 的指令列呼叫抽象化，提供乾淨的 Python API。

## 步驟 2：設定 OCR 語言 – 告訴引擎預期的文字

如果文件是英文，你可以保留預設值，但最好明確設定。這同時示範了如何**set OCR language**給其他語系。

```python
# Step 2: Explicitly set the language to English
engine.language = ocr.Language.ENGLISH
```

> **小技巧**：對於多語言 PDF，你可以傳入類似 `[ocr.Language.ENGLISH, ocr.Language.FRENCH]` 的清單。引擎會自動嘗試這兩種語言。

## 步驟 3：載入 OCR 圖像 – 將圖片載入記憶體

現在我們真的要**load image for OCR**。此封裝支援延遲載入，檔案會在引擎需要時才讀取。

```python
# Step 3: Load the image you want to process
image_path = "YOUR_DIRECTORY/large_document.jpg"
image = ocr.Image.load(image_path)
```

*邊緣情況*：若圖片過大（超過 5 MB），建議先調整尺寸以加速辨識。可使用 Pillow 完成：

```python
from PIL import Image as PilImage

pil_img = PilImage.open(image_path)
pil_img.thumbnail((2000, 2000))          # keep aspect ratio, max 2000px
pil_img.save("resized.jpg")
image = ocr.Image.load("resized.jpg")
```

## 步驟 4：啟動非同步辨識 – 避免阻塞應用程式

執行 OCR 可能需要一兩秒，特別是大型掃描時。`recognize_async` 方法會回傳一個 future，你之後可以輪詢，讓你在 OCR 背景執行時**同時執行其他工作**。

```python
# Step 4: Start the recognition asynchronously
future = engine.recognize_async(image)

# While OCR works, we can do something else
print("Processing other tasks while OCR runs...")
# Example placeholder work
for i in range(3):
    print(f"Task {i+1} done.")
```

為什麼要使用非同步？在 Web 伺服器上，你不希望單一請求卡住整個工作池。future 物件讓你掌控：可以在非同步程式碼中 `await`，或只在真正需要結果時才阻塞。

## 步驟 5：取得結果 – 僅在必要時阻塞

當你最終需要文字時，呼叫 `future.get()`。此呼叫**僅在此處阻塞**，代表程式其餘部分會保持回應，直到 OCR 完成。

```python
# Step 5: Get the recognized text (blocks here)
result = future.get()   # blocks only at this point
```

如果你在 `asyncio` 迴圈中，也可以改用 `await future` – 此封裝支援兩種寫法。

## 步驟 6：使用辨識出的文字 – 資料已就緒

現在你已取得 `result` 物件，取得純文字非常簡單。讓我們印出來，同時示範如何寫入檔案。

```python
# Step 6: Output the OCR result
print("OCR completed:")
print(result.text)

# Optional: save to a .txt file
with open("extracted.txt", "w", encoding="utf-8") as f:
    f.write(result.text)
```

**預期輸出**（為簡潔起見已截斷）：

```
OCR completed:
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
```

若圖片不含文字，`result.text` 會是空字串——請優雅地處理此情況。

## 完整範例 – 一步完成所有步驟

以下是完整、可直接執行的程式。複製貼上，調整 `image_path`，即可使用。

```python
import ocr
from PIL import Image as PilImage

# -------------------------------------------------
# 1️⃣ Create OCR engine
engine = ocr.OcrEngine()

# 2️⃣ Set language (English)
engine.language = ocr.Language.ENGLISH

# 3️⃣ Load image (optional resize for large files)
original_path = "YOUR_DIRECTORY/large_document.jpg"
pil_img = PilImage.open(original_path)
pil_img.thumbnail((2000, 2000))          # keep aspect ratio
pil_img.save("resized.jpg")
image = ocr.Image.load("resized.jpg")

# 4️⃣ Start async recognition
future = engine.recognize_async(image)
print("Processing other tasks while OCR runs...")
for i in range(3):
    print(f"Task {i+1} done.")

# 5️⃣ Wait for result
result = future.get()

# 6️⃣ Use the text
print("OCR completed:")
print(result.text)
with open("extracted.txt", "w", encoding="utf-8") as f:
    f.write(result.text)
```

> **注意**：將 `"YOUR_DIRECTORY/large_document.jpg"` 替換為實際的圖像路徑。只要 Tesseract 已安裝且在你的 `PATH` 中可被找到，此腳本即可在 Windows、macOS 與 Linux 上執行。

## 常見陷阱與避免方法

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **雜訊字元** | 語言設定錯誤或缺少語言資料檔案。 | 確保 `engine.language` 與文字相符，且相應的 `.traineddata` 檔案存在於 Tesseract 的 `tessdata` 資料夾中。 |
| **大圖像效能緩慢** | OCR 的運算量大致與像素數量成正比。 | 在送入引擎前先調整尺寸或降採樣（參考 Pillow 範例）。 |
| **Future 永不完成** | 圖像檔案損毀或無法讀取。 | 將 `future.get()` 包在 try/except 區塊，並在辨識前驗證 `image.is_valid()`。 |
| **Unicode 丟失** |  |  |

## 接下來該學什麼？

以下教學涵蓋與本指南密切相關的主題，並以此為基礎。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在自己的專案中探索其他實作方式。

- [使用 Aspose OCR 從圖像提取文字 – 步驟指南](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [將圖像轉換為文字 – 從 URL 執行 OCR](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [從圖像提取文字 – 使用 Aspose OCR 於 .NET 的 OCR 最佳化](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}