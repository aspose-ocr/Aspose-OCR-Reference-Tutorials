---
category: general
date: 2026-04-26
description: 使用 Aspose OCR 在 Python 中從圖片提取文字。了解如何提取文字、將圖片轉換為文字，以及載入圖片進行 OCR，支援多語言。
draft: false
keywords:
- extract text from image
- how to extract text
- convert image to text
- load image for ocr
- multilingual ocr python
language: zh-hant
og_description: 即時從圖像提取文字。本指南示範如何提取文字、將圖像轉換為文字，以及使用 Aspose OCR 在 Python 中載入圖像進行 OCR。
og_title: 使用 Python 從圖片提取文字 – 完整多語言 OCR 教程
tags:
- OCR
- Python
- Aspose
title: 使用 Python 從圖像提取文字 – 多語言 OCR 指南
url: /zh-hant/python-java/general/extract-text-from-image-with-python-multilingual-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Python 從圖像中提取文字 – 多語言 OCR 指南

是否曾需要**從圖像中提取文字**，卻不確定哪個函式庫能處理混合語言的頁面？你並不孤單。在許多實務應用中——例如發票處理、社交媒體監控或多語言文件歸檔——你會遇到同時包含拉丁字母與西里爾字母的圖片。

好消息是？使用 Aspose OCR for Python，你可以在幾行程式碼內**提取文字**、**將圖像轉換為文字**，以及**載入圖像進行 OCR**，同時讓引擎自動偵測語言。在本教學中，我們將逐步示範完整、可執行的範例，說明每一步的原因，並涵蓋你在實作過程中可能遇到的幾個邊緣案例。

> **學習成果**  
> * 一個可直接執行的腳本，能從混合語言的 PNG 中提取文字。  
> * 了解如何在 Python 中設定多語言 OCR。  
> * 處理大型檔案、不同圖像格式以及除錯常見問題的技巧。  

## 前置條件

- Python 3.8 或更新版本（程式碼使用 f‑strings）。  
- 已安裝 `asposeocr` 套件（`pip install asposeocr`）。  
- 一個圖像檔案（例如 `mixed_lang.png`），其中包含多種文字系統。  
- 具備 Python 匯入與物件導向 API 的基本概念。  

不需要繁重的相依套件，也不需外部服務——只要一次 pip 安裝，即可開始使用。

---

## 步驟 1 – 安裝與匯入 Aspose OCR 函式庫  

在我們能**載入圖像進行 OCR**之前，需要先安裝函式庫本身。此套件內含核心 OCR 引擎與輕量級的圖像載入器。

```python
# Install the package (run once in your environment)
# pip install asposeocr

# Import the required classes
import asposeocr as aocr
from asposeocr import OcrEngine, OcrConfig, Language
```

*為什麼這很重要*：匯入特定類別可保持命名空間整潔，讓後續程式碼更易讀。如果只匯入 `asposeocr`，則每次呼叫都必須加上前綴（`aocr.OcrEngine()`），會顯得雜亂。

## 步驟 2 – 建立 OCR 引擎並啟用多語言偵測  

Aspose OCR 能自動推測圖像中出現的語言。將 `Language.AUTO` 設為偵測模式，可涵蓋拉丁文、西里爾文、阿拉伯文等多種語言。

```python
# Initialize the OCR engine
ocr_engine = OcrEngine()

# Enable automatic language detection (covers Latin, Cyrillic, etc.)
ocr_engine.config.language = Language.AUTO
```

*小技巧*：若事先知道語言，可指定 `Language.ENGLISH` 或 `Language.RUSSIAN` 以略提升效能。但對於真正的混合文件，使用 `AUTO` 是最安全的選擇。

## 步驟 3 – 載入要處理的圖像  

這裡就是我們**載入圖像進行 OCR**的地方。Aspose 支援 PNG、JPEG、BMP、TIFF，甚至可將 PDF 頁面視為圖像載入。

```python
# Path to the image containing mixed‑language text
image_file_path = "YOUR_DIRECTORY/mixed_lang.png"

# Load the image into the OCR engine
ocr_engine.image = aocr.Image.load(image_file_path)
```

> **提示**：若圖像大小超過 2 MB，建議先行調整尺寸。大型圖像會增加記憶體使用，且可能拖慢偵測步驟。

## 步驟 4 – 執行 OCR 程序並取得結果  

呼叫 `process()` 會完成繁重的工作：文字偵測、版面分析與語言解碼。

```python
# Execute the OCR operation
ocr_result = ocr_engine.process()
```

回傳的 `ocr_result` 物件包含多個實用屬性：

| Property | Description |
|----------|-------------|
| `text` | 辨識出的純文字字串（最常使用的欄位）。 |
| `confidence` | 整體信心水平（0‑100）。 |
| `lines` | `OcrLine` 物件的列表，包含位置資訊（對 PDF 特別有用）。 |

## 步驟 5 – 顯示提取的文字  

最後，我們將輸出列印到螢幕。實際應用中，你可能會將結果寫入資料庫，或傳遞給翻譯 API。

```python
print("Recognized Text:")
print(ocr_result.text)
```

**預期輸出**（混合語言圖像的範例）：

```
Recognized Text:
Hello world!
Привет мир!
```

如果看到亂碼，請確認圖像未損毀，且使用的是最新版本的 `asposeocr`（本文撰寫時為 v23.7）。

## 步驟 6 – 完整腳本（可直接複製貼上）  

將所有步驟整合在一起，可避免「程式碼從哪裡開始？」的困惑。將此檔案另存為 `multilingual_ocr.py`，並於命令列執行。

```python
# multilingual_ocr.py
# -------------------------------------------------
# Complete example: extract text from image (multilingual)
# -------------------------------------------------

import asposeocr as aocr
from asposeocr import OcrEngine, Language

def extract_text(image_path: str) -> str:
    """
    Loads an image, runs Aspose OCR with auto language detection,
    and returns the recognized text.
    """
    engine = OcrEngine()
    engine.config.language = Language.AUTO
    engine.image = aocr.Image.load(image_path)
    result = engine.process()
    return result.text

if __name__ == "__main__":
    # Adjust this path to point at your own image file
    img_path = "YOUR_DIRECTORY/mixed_lang.png"
    text = extract_text(img_path)
    print("Recognized Text:")
    print(text)
```

執行指令：

```bash
python multilingual_ocr.py
```

你應該會在主控台看到提取的字串。就這樣——只需幾行程式碼即可**將圖像轉換為文字**。

## 常見問題與邊緣案例處理  

### 如果圖像中包含手寫文字呢？

Aspose OCR 針對印刷文字進行最佳化。手寫文字通常需要專用模型（例如 Azure Read 或 Google Vision）。仍可嘗試 `Language.AUTO`，但預期信心較低。

### 如何提升噪點掃描的辨識準確度？

1. 先行前處理圖像（二值化、去斑點）。  
2. 將 DPI 提升至至少 300 ppi 再送入引擎。  
3. 若圖像傾斜，明確設定 `ocr_engine.config.deskew = True`。

```python
ocr_engine.config.deskew = True
```

### 能否直接從 PDF 提取文字，而不先轉換為圖像？

可以——Aspose OCR 能直接開啟 PDF 頁面：

```python
ocr_engine.image = aocr.Image.load("document.pdf", page_number=1)
```

只要記得每一頁在內部都會被視為圖像處理，因此相同的品質考量仍然適用。

## 結論  

現在你已擁有一套完整、端到端的流程，能使用 Aspose OCR 在 Python 中**從圖像中提取文字**，並支援多語言。此腳本示範了如何**載入圖像進行 OCR**、**將圖像轉換為文字**，以及處理最常見的陷阱。

從此你可以：

- 將此功能整合至接受使用者上傳的 Web 服務。  
- 將提取的文字與語言偵測函式庫結合，以導向正確的翻譯引擎。  
- 嘗試調整 `ocr_engine.config` 選項（例如 `max_recognition_time`、`text_orientation`）以微調效能。

祝程式開發順利，願你的 OCR 流程永遠精確！  

---  

![提取多語言文字的螢幕截圖 – 從圖像提取文字範例](image-placeholder.png "從圖像提取文字範例")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}