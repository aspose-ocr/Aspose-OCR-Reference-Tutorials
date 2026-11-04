---
category: general
date: 2026-06-06
description: 使用 Python OCR 在幾分鐘內從圖片中提取文字。探索多語言圖片 OCR、自動偵測語言的 OCR，以及如何準確提取 OCR 文字。
draft: false
keywords:
- extract text from image
- how to extract OCR text
- multilingual image OCR
- detect language OCR
- auto detect language OCR
language: zh-hant
og_description: 使用 Python OCR 快速從圖像中提取文字。學習多語言圖像 OCR、自動偵測語言 OCR，以及一步步提取 OCR 文字的方法。
og_title: 使用 Python OCR 從圖片提取文字 – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Extract text from image with Python OCR in minutes. Discover multilingual
    image OCR, auto detect language OCR, and how to extract OCR text accurately.
  headline: Extract Text from Image Using Python OCR – Complete Guide
  type: TechArticle
- description: Extract text from image with Python OCR in minutes. Discover multilingual
    image OCR, auto detect language OCR, and how to extract OCR text accurately.
  name: Extract Text from Image Using Python OCR – Complete Guide
  steps:
  - name: '**Low‑resolution images** – OCR accuracy drops sharply below 150 dpi. Upscale
      or request a higher‑resolution scan.'
    text: '**Low‑resolution images** – OCR accuracy drops sharply below 150 dpi. Upscale
      or request a higher‑resolution scan.'
  - name: '**Noise and compression artifacts** – Apply a simple threshold filter (`opencv`
      or `Pillow`) before feeding the image to the engine.'
    text: '**Noise and compression artifacts** – Apply a simple threshold filter (`opencv`
      or `Pillow`) before feeding the image to the engine.'
  - name: '**Mixed scripts on one page** – Some engines struggle with simultaneous
      Latin and CJK characters. Split the page into regions and run separate recognitions
      if needed.'
    text: '**Mixed scripts on one page** – Some engines struggle with simultaneous
      Latin and CJK characters. Split the page into regions and run separate recognitions
      if needed.'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- Multilingual
title: 使用 Python OCR 從圖像提取文字 – 完整指南
url: /zh-hant/python-java/general/extract-text-from-image-using-python-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從圖像中提取文字的 Python OCR 完整指南

是否曾需要 **從圖像中提取文字**，卻不確定哪個函式庫能自動處理多語言？你並不孤單——開發者在面對國際文件、收據或掃描傳單時，常會問 *如何提取 OCR 文字*。在本教學中，我們將示範一個實用的 Python 範例，不僅能從圖像中提取文字，還能 **即時偵測語言**，讓多語言圖像 OCR 變得輕而易舉。

我們會從安裝 OCR 套件、啟用 **自動偵測語言 OCR**、在範例圖片上執行引擎，最後印出偵測到的語言與提取的字串。完成後，你將擁有一段可重複使用的程式碼，無論是建構翻譯管線或資料擷取服務，都能直接套用。

## 從圖像中提取文字 – 環境設定

在開始撰寫程式碼之前，請先確保你的工作站符合以下最低需求：

- Python 3.8 或更新版本（此函式庫使用型別提示，舊版會被忽略）
- `pip` 進行套件管理
- 至少包含兩種不同語言文字的圖像檔（例如 English + Spanish）

你還需要支援此示範的 OCR 函式庫。為了本教學的目的，我們使用虛構的 `ocr` 套件，它的介面類似 Tesseract、EasyOCR 等常見工具，但提供更乾淨的 Python API。

```bash
# Install the OCR package and its optional image dependencies
pip install ocr[image]
```

> **小技巧：** 若遇到權限錯誤，可在指令前加上 `python -m`，或使用虛擬環境——這樣可以保持全域 site‑packages 的整潔。

## 建立 OCR 引擎實例

函式庫安裝完成後，第一步是 **建立 OCR 引擎實例**。可以把引擎想像成一部可在輸入圖像前先行設定的智慧掃描器。

```python
import ocr

# Step 1: Initialize the OCR engine
engine = ocr.OcrEngine()
```

為什麼要先實例化引擎，而不是直接呼叫靜態方法？引擎物件會保存設定狀態（例如語言偏好），讓你在處理多張圖像時可以重複使用，免除每次重新初始化的開銷。

## 啟用自動偵測語言 OCR

大多數 OCR 工具都需要手動指定語言代碼——`eng` 代表英文、`spa` 代表西班牙文，依此類推。手動猜測語言會失去 **多語言圖像 OCR** 工作流程的意義。幸好，`ocr` 套件提供 *自動偵測語言 OCR* 模式，會在背景自動檢查圖像並選擇最適合的語言模型。

```python
# Step 2: Turn on automatic language detection
engine.set_recognition_language(ocr.Language.AUTO_DETECT)
```

以這種方式啟用 **偵測語言 OCR**，就不必維護長長的語言代碼清單。引擎會嘗試匹配圖像中出現的文字系統——拉丁、斯拉夫、漢字等——並自動載入相應模型。

## 執行多語言圖像 OCR

引擎已就緒，現在可以真正 **從圖像中提取文字**。`recognize_image` 方法接受檔案路徑，回傳一個結果物件，內含原始文字與偵測到的語言。

```python
# Step 3: Run OCR on a multilingual image
image_path = "YOUR_DIRECTORY/multilang_page.png"
result = engine.recognize_image(image_path)
```

如果你想知道 *如何從 PDF 提取 OCR 文字*，只要改用 `recognize_pdf` 方法即可。底層的偵測邏輯相同，仍能受惠於 **自動偵測語言 OCR** 功能。

## 顯示偵測語言與提取文字

最後，我們把引擎發現的資訊輸出。結果物件提供 `detected_language`（如 `en`、`es` 的 BCP‑47 標籤）以及 `text`（原始 OCR 輸出）。

```python
# Step 4: Show the language and the extracted string
print(f"Detected language: {result.detected_language}")
print("Extracted text:")
print(result.text)
```

在範例圖像上執行腳本，應會得到類似以下的結果：

```
Detected language: en
Extracted text:
Welcome to our multilingual brochure.
¡Bienvenidos a nuestro folleto multilingüe!
```

可以看到，引擎正確辨識出英文為主要語言，同時也捕捉到西班牙文行——這正是 **多語言圖像 OCR** 解決方案所應具備的表現。

### 假如偵測失敗？

當圖像模糊或文字系統過於罕見時，OCR 引擎可能會退回預設語言（通常是英文）。此時你可以強制指定語言清單：

```python
engine.set_recognition_language([ocr.Language.ENGLISH, ocr.Language.SPANISH])
```

但請記得，強制指定語言會失去 **自動偵測語言 OCR** 的便利性，僅在已知語言子集時使用。

## 常見陷阱與可靠提取 OCR 文字的方法

即使有自動偵測，仍有幾個常見問題可能卡住你：

1. **低解析度圖像** – 當解析度低於 150 dpi 時，OCR 準確度會急劇下降。請升級圖像或要求更高解析度的掃描。
2. **噪點與壓縮雜訊** – 在送入引擎前，先使用簡單的二值化濾鏡（`opencv` 或 `Pillow`）清理圖像。
3. **單頁混合文字系統** – 部分引擎在同時處理拉丁與中日韓字符時表現不佳。必要時可將頁面切割成多個區塊，分別辨識。

解決上述問題後，**從圖像中提取文字** 的品質會大幅提升，特別是面對真實世界的多語言文件時。

## 完整可執行範例

以下是結合前述所有步驟的完整腳本。將其存為 `multilingual_ocr.py`，然後在命令列執行。

```python
import ocr

def main():
    # Initialize engine with auto language detection
    engine = ocr.OcrEngine()
    engine.set_recognition_language(ocr.Language.AUTO_DETECT)

    # Path to your multilingual image
    image_path = "YOUR_DIRECTORY/multilang_page.png"

    # Perform OCR
    result = engine.recognize_image(image_path)

    # Output results
    print(f"Detected language: {result.detected_language}")
    print("Extracted text:")
    print(result.text)

if __name__ == "__main__":
    main()
```

**預期輸出**（假設範例圖像同時包含英文與西班牙文）：

```
Detected language: en
Extracted text:
Welcome to our multilingual brochure.
¡Bienvenidos a nuestro folleto multilingüe!
```

隨意將 `multilang_page.png` 換成任何含有其他語言文字的圖片——得益於 **自動偵測語言 OCR**，腳本仍會回傳合理的語言標籤與對應文字。

![Extract text from image example](https://example.com/ocr-sample.png "Extract text from image")

## 結論

現在你已掌握 **如何從圖像中提取 OCR 文字**、如何啟用 **自動偵測語言 OCR**，以及如何以最少程式碼處理 **多語言圖像 OCR** 情境。只要建立 OCR 引擎實例、開啟自動語言偵測，並呼叫 `recognize_image`，就能可靠地取得語言標識與原始文字。

接下來可以嘗試將提取的字串送入翻譯 API、存入可搜尋的資料庫，或把多頁合併成單一 PDF 報告。你也可以實驗不同的 OCR 後端（Tesseract、EasyOCR、Google Vision），只要保持相同的高階工作流程——感謝一致的 **偵測語言 OCR** 介面。

若遇到任何怪異情況，請回顧「常見陷阱」章節或微調圖像前處理步驟。祝開發順利，願你的下一個專案充滿正確偵測、完美提取的文字！

## 接下來該學什麼？

以下教學與本指南的技術緊密相關，能幫助你進一步掌握 API 功能，並在自己的專案中探索其他實作方式：

- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [recognize text image with Aspose OCR for multiple languages](/ocr/english/net/ocr-settings/working-with-different-languages/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}