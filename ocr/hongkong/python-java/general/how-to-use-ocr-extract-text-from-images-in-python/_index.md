---
category: general
date: 2026-03-18
description: 如何使用 OCR 從圖像中提取文字 – 快速指南，教你從 PNG 檔案辨識文字及載入圖像以進行 OCR。
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from png
- how to extract text
- load image for OCR
language: zh-hant
og_description: 如何使用 OCR 從圖像中提取文字 – 學習從 PNG 識別文字、載入圖像進行 OCR，並使用簡單的 Python 腳本提取文字。
og_title: 如何使用 OCR：在 Python 中從圖片提取文字
tags:
- OCR
- Python
- Image Processing
title: 如何使用 OCR：在 Python 中從圖像提取文字
url: /zh-hant/python-java/general/how-to-use-ocr-extract-text-from-images-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 OCR：在 Python 中從圖像提取文字

有沒有想過在截圖或掃描收據雜亂時 **如何使用 OCR**？你並不孤單——開發者經常需要從圖片中提取可讀文字，尤其是來自手機應用程式或網上上傳的 PNG。於本教學，我們將逐步示範一個完整且可執行的範例，說明如何 **從圖像檔案提取文字**、**從 PNG 資產辨識文字**，甚至 **載入圖像以供 OCR**，只需幾行 Python 程式碼。

我們會從安裝正確的函式庫說起，直到處理多語言文件，最後你將能精確知道如何 *從任何圖像中提取文字*。不會有模糊的說明，只有清晰的逐步解決方案，讓你直接複製貼上並執行。

## 你將學到什麼

1. 設定輕量級 OCR 引擎（不需要大型相依套件）。  
2. 將圖像檔案（特別是 PNG）載入引擎。  
3. 啟用自動語言偵測，使引擎能處理多語言內容。  
4. 執行辨識程序並取得純文字結果。  
5. 微調工作流程以因應缺少檔案或不支援格式等邊緣情況。  

如果你對基本的 Python 已經熟悉，就可以直接開始。不需要先前的 OCR 經驗，雖然快速瀏覽函式庫文件總是有幫助的。

---

![如何在 PNG 圖像上使用 OCR](placeholder.png "如何在 PNG 圖像上使用 OCR – 步驟指南")

## 如何使用 OCR – 載入圖像並辨識文字 {#how-to-use-ocr}

### 步驟 1：安裝 OCR 函式庫

首先，你需要一個提供 `OcrEngine` 類別的 Python 套件。為了本教學，我們將使用虛構但具說明性的 **SimpleOCR** 套件，你可以透過 pip 安裝：

```bash
pip install simple-ocr
```

> **專業提示：** 若你在虛擬環境中工作（強烈建議），請在執行安裝指令前先啟動它。這樣可以讓你的專案相依性保持整潔。

### 步驟 2：匯入引擎並建立實例

建立引擎就像呼叫其建構子一樣簡單。把引擎想像成之後會處理你提供的圖像的「大腦」。

```python
# Step 2: Import and instantiate the OCR engine
from simple_ocr import OcrEngine

# Create a fresh engine instance – this allocates internal buffers
engine = OcrEngine()
```

為什麼每次都要建立新實例？因為需要隔離。全新的引擎可確保先前執行遺留下的狀態不會污染本次辨識，這在批次處理大量檔案時尤為重要。

### 步驟 3：載入要處理的圖像

現在我們真的要 **載入圖像以供 OCR**。`setImageFromFile` 方法接受任意點陣圖的路徑；我們將指向名為 `mixed_doc.png` 的 PNG。

```python
# Step 3: Load the PNG image you want to read
image_path = "YOUR_DIRECTORY/mixed_doc.png"
engine.setImageFromFile(image_path)
```

如果找不到檔案，`SimpleOCR` 會拋出明確的 `FileNotFoundError`。你可以捕獲它以提供友善的錯誤訊息：

```python
try:
    engine.setImageFromFile(image_path)
except FileNotFoundError:
    print(f"❗️ Unable to locate '{image_path}'. Check the path and try again.")
    raise
```

### 步驟 4：啟用自動語言偵測

大多數現代 OCR 引擎都內建語言套件。傳入 `"multilingual"` 後，我們告訴引擎自動偵測文字並自動選擇正確的語言模型。例如，當你的 PNG 同時包含英文與西班牙文時，這特別方便。

```python
# Step 4: Turn on auto‑language detection (covers all installed packs)
engine.setLanguage("multilingual")
```

如果事先知道語言，你可以將 `"multilingual"` 換成特定語系代碼，例如 `"eng"` 或 `"spa"`，以加快處理速度。

### 步驟 5：執行辨識程序

繁重的工作就在此進行。`recognize()` 會掃描圖像、套用分割、執行神經網路，並在內部建立文字緩衝區。

```python
# Step 5: Execute OCR – this may take a moment for large images
engine.recognize()
```

在背後，引擎會執行：

- **前處理**（去斜、二值化）  
- **版面分析**（偵測欄位、表格）  
- **字元分類**（使用深度學習模型）  

所有這些都已抽象化，這也是為什麼你只需要一行程式碼。

### 步驟 6：取得並印出辨識文字

最後，我們取得結果物件並抽取純文字字串。這就是實際 **從圖像提取文字** 的部分。

```python
# Step 6: Get the OCR result and display the plain text
result = engine.getResult()
text = result.getText()
print("📝 Recognized Text:\n")
print(text)
```

**預期輸出**（為簡潔起見已截斷）：

```
📝 Recognized Text:

Invoice #12345
Date: 2026‑03‑15
Total: $89.99
Thank you for your purchase!
```

如果圖像中沒有可辨識的字元，`text` 會是空字串。你可以針對此情況做防護：

```python
if not text.strip():
    print("⚠️ No text detected – try a higher‑resolution image or adjust preprocessing.")
```

---

## 從圖像提取文字 – 處理常見邊緣情況

### 單一檔案中的多語言

當文件混合多種語言時，`"multilingual"` 設定通常能正確處理。然而，若發現辨識錯誤，你可以手動指定備援語言清單：

```python
engine.setLanguage(["eng", "spa", "fra"])  # English, Spanish, French
```

### 非 PNG 格式

雖然我們的重點是 **從 PNG 辨識文字**，`SimpleOCR` 仍支援 JPEG、BMP 與 TIFF。只要在 `setImageFromFile` 中更改檔案副檔名即可。對於 TIFF 堆疊，可能需要選取特定頁面：

```python
engine.setImageFromFile("scanned.tif", page=0)  # first page only
```

### 大檔案與記憶體使用量

如果你在處理千兆像素的掃描圖，建議在 OCR 前先調整大小：

```python
from PIL import Image

with Image.open(image_path) as img:
    img.thumbnail((2000, 2000))  # keep aspect ratio, max 2000px
    img.save("temp_resized.png")
engine.setImageFromFile("temp_resized.png")
```

調整大小可減少記憶體壓力，同時保留足夠的細節以確保辨識準確。

### 偵錯載入失敗

有時圖像肉眼看起來正常，但內部已損毀。啟用詳細日誌以觀察引擎看到的內容：

```python
engine.enableDebug(True)   # prints internal steps to stdout
engine.recognize()
```

---

## 完整、可直接執行的腳本

以下是將所有步驟整合的完整程式。將它複製到名為 `ocr_demo.py` 的檔案中，調整 `YOUR_DIRECTORY` 佔位符，然後執行 `python ocr_demo.py`。

```python
# ocr_demo.py
# Full example showing how to use OCR to extract text from a PNG image.
# Requires: pip install simple-ocr pillow

from simple_ocr import OcrEngine
import os
from PIL import Image

def main():
    # 1️⃣ Create the OCR engine
    engine = OcrEngine()

    # 2️⃣ Define the image path – change this to your actual file location
    image_path = os.path.join("YOUR_DIRECTORY", "mixed_doc.png")

    # 3️⃣ Load the image (with a safety net for missing files)
    try:
        engine.setImageFromFile(image_path)
    except FileNotFoundError:
        print(f"❗️ Cannot find image at '{image_path}'. Exiting.")
        return

    # Optional: resize large images to keep memory usage low
    # (uncomment if you deal with huge scans)
    # with Image.open(image_path) as img:
    #     img.thumbnail((2000, 2000))
    #     resized_path = "temp_resized.png"
    #     img.save(resized_path)
    #     engine.setImageFromFile(resized_path)

    # 4️⃣ Enable automatic language detection (covers all installed packs)
    engine.setLanguage("multilingual")

    # 5️⃣ Run the OCR engine
    engine.recognize()

    # 6️⃣ Retrieve and print the recognized text
    result = engine.getResult()
    text = result.getText()

    if text.strip():
        print("\n📝 Recognized Text:\n")
        print(text)
    else:
        print("⚠️ No recognizable text found. Try a clearer image or adjust preprocessing.")

if __name__ == "__main__":
    main()
```

執行此腳本應會輸出 `mixed_doc.png` 內部的純文字版本。隨意將檔案換成其他圖片——**如何提取文字**的方式相同。

---

## 結論

我們剛剛示範了在 Python 中 **如何使用 OCR** 以 **從圖像檔案提取文字**，特別聚焦於 **從 PNG 資產辨識文字** 以及實作 **載入圖像以供 OCR** 的步驟。上述程式碼是一個獨立的解決方案：安裝套件、提供檔案、啟用多語言偵測、執行引擎，然後取得結果。

從此你可以：

- 將腳本整合到接受使用者上傳的 Web 服務中。  
- 批次處理已轉換成 PNG 的 PDF 資料夾。  
- 加入後處理（例如正規表達式清理、拼寫檢查）以提升準確度。

請記住，OCR 的品質取決於圖像清晰度、正確的語言套件，有時還需要一些前處理——因此請多加實驗

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}