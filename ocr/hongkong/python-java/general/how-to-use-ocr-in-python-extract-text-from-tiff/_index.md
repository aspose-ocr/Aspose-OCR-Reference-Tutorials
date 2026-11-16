---
category: general
date: 2026-07-05
description: 如何在 Python 中使用 OCR 快速將 TIFF 轉換為文字。學習 OCR 套件在 Python 的步驟，從 TIFF 影像提取文字並構建
  Python OCR 引擎。
draft: false
keywords:
- how to use ocr
- ocr library python
- convert tiff to text
- extract text from tiff
- python ocr engine
language: zh-hant
og_description: 如何在 Python 中使用 OCR？本指南將一步一步示範如何使用 Python OCR 引擎與 ocr library（Python
  版）將 TIFF 轉換為文字。
og_title: 如何在 Python 中使用 OCR – 完整的 TIFF 文本提取
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: How to use OCR in Python to convert TIFF to text quickly. Learn the
    ocr library python steps for extracting text from TIFF images and building a python
    OCR engine.
  headline: How to Use OCR in Python – Extract Text from TIFF
  type: TechArticle
- description: How to use OCR in Python to convert TIFF to text quickly. Learn the
    ocr library python steps for extracting text from TIFF images and building a python
    OCR engine.
  name: How to Use OCR in Python – Extract Text from TIFF
  steps:
  - name: '**Chunk the pages** – Instead of `recognize_multi_page`, call `engine.recognize(page)`
      inside a generator that yields one page at a time.'
    text: '**Chunk the pages** – Instead of `recognize_multi_page`, call `engine.recognize(page)`
      inside a generator that yields one page at a time.'
  - name: '**Adjust DPI** – Lowering the image resolution (e.g., from 300 DPI to 200 DPI)
      reduces CPU load while barely affecting accuracy for most printed text.'
    text: '**Adjust DPI** – Lowering the image resolution (e.g., from 300 DPI to 200 DPI)
      reduces CPU load while barely affecting accuracy for most printed text.'
  - name: '**Parallelize** – If your OCR engine is thread‑safe, spawn a `concurrent.futures.ThreadPoolExecutor`
      to run recognition on multiple pages concurrently.'
    text: '**Parallelize** – If your OCR engine is thread‑safe, spawn a `concurrent.futures.ThreadPoolExecutor`
      to run recognition on multiple pages concurrently.'
  type: HowTo
tags:
- OCR
- Python
- TIFF
- Image Processing
title: 如何在 Python 中使用 OCR – 從 TIFF 提取文字
url: /zh-hant/python-java/general/how-to-use-ocr-in-python-extract-text-from-tiff/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中使用 OCR – 從 TIFF 提取文字

有沒有想過 **how to use OCR in Python**（如何在 Python 中使用 OCR）將掃描書籍轉換成可編輯的文字？你並不是唯一遇到這個問題的人——開發者、研究人員和業餘愛好者在處理多頁 TIFF 圖片時都會碰到這個障礙。好消息是？只要使用 **ocr library python**，你就可以啟動一個小型 OCR 引擎，指向 TIFF 檔案，並在幾秒鐘內取得乾淨、可搜尋的文字。

在本教學中，我們將逐步說明你需要的所有步驟：安裝正確的套件、載入多頁 TIFF、執行 OCR 引擎，最後列印每一頁的內容。完成後，你將能夠 **convert TIFF to text** 並 **extract text from TIFF** 檔案，而不必離開 Python 環境。

## 前置條件

- Python 3.9 或更新版本（此範例在 3.11 上測試）
- 最近版本的 `ocr` 套件（或任何相容的 `python ocr engine`）
- 你想處理的多頁 TIFF 檔案（此處稱為 `scanned_book.tif`）
- 基本熟悉 Python 腳本與虛擬環境

不需要繁重的外部工具——只要 pip 與幾行程式碼即可。

## 安裝 OCR Library Python

首先，你需要一個可靠的 OCR 後端。於本指南，我們將使用虛構的 `ocr` 套件，它提供簡易的高階 API，但相同的模式也適用於基於 Tesseract 的封裝，如 `pytesseract` 或商業 SDK。

```bash
# Create a clean virtual environment (optional but recommended)
python -m venv ocr-env
source ocr-env/bin/activate   # Windows: ocr-env\Scripts\activate

# Install the OCR package
pip install ocr
```

> **Pro tip:** 如果你在 Windows 上且套件依賴原生二進位檔，請確保已安裝相應的 Visual C++ 可再發行套件。安裝程式通常會在缺少項目時發出警告。

## 如何在 Python 中使用 OCR 引擎

現在套件已就緒，讓我們啟動 OCR 引擎並指向我們的 TIFF 檔案。以下程式碼片段會建立引擎實例、將語言設定為 English，並為多頁處理做準備。

```python
import ocr

# Step 1: Create an OCR engine and set the language to English
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH   # You can switch to ocr.Language.FRENCH, etc.
```

**為什麼要設定語言？**  
大多數 OCR 引擎會使用語言模型來提升準確度。如果跳過此步驟，引擎會退回使用通用模型，可能會錯誤辨識標點或特殊字元。

## 載入多頁 TIFF 圖像

接下來的步驟是載入掃描文件。`ocr.Image.load` 輔助函式能直接辨識 TIFF 堆疊，回傳一個內部代表每一頁的物件。

```python
# Step 2: Load the multi‑page TIFF image containing the scanned book
tiff_path = "YOUR_DIRECTORY/scanned_book.tif"
tiff_image = ocr.Image.load(tiff_path)
```

> **Edge case:** 如果你的 TIFF 使用壓縮（如 CCITT Group 4、LZW 等），且套件拋出錯誤，請先使用 ImageMagick 轉換為未壓縮版本：
> ```bash
> convert scanned_book.tif -compress none scanned_book_uncompressed.tif
> ```

## 在所有頁面執行 OCR – 轉換 TIFF 為文字

取得影像物件後，引擎即可一次處理所有頁面。此方法會回傳一個列表，列表中的每個元素包含單一頁面的 OCR 結果。

```python
# Step 3: Perform OCR on all pages of the image
page_results = engine.recognize_multi_page(tiff_image)
```

**底層發生了什麼？**  
`recognize_multi_page` 函式會遍歷每個光柵化頁面，執行神經網路辨識，並將純文字輸出與信心分數一起打包。這本質上是一個批次操作，讓你免於手動撰寫迴圈。

## 迭代結果 – 從 TIFF 提取文字

最後，我們顯示辨識出的文字。你可以將輸出寫入個別的 `.txt` 檔案、推送至資料庫，或餵入搜尋索引——依照你的工作流程選擇。

```python
# Step 4: Iterate through the results and display the recognized text for each page
for page_index, result in enumerate(page_results):
    print(f"Page {page_index + 1}:\n{result.text}\n")
```

### 預期輸出

```
Page 1:
Chapter 1
In the beginning...

Page 2:
The quick brown fox jumps over the lazy dog.

Page 3:
...

```

每個 `result.text` 字串包含該頁的原始 OCR 輸出。若需要保留換行，大多數引擎會以 `result.lines` 以字串列表形式提供。

## 處理大型 TIFF 檔案 – 提示與技巧

處理 500 頁的 TIFF 可能會佔用大量記憶體。以下提供幾個讓流程順暢的策略：

1. **Chunk the pages** – 不使用 `recognize_multi_page`，改在產生器中一次產生一頁，呼叫 `engine.recognize(page)`。
2. **Adjust DPI** – 降低影像解析度（例如從 300 DPI 降至 200 DPI）可減少 CPU 負載，且對大多數印刷文字的準確度影響甚微。
3. **Parallelize** – 若你的 OCR 引擎支援執行緒安全，可建立 `concurrent.futures.ThreadPoolExecutor`，同時對多頁進行辨識。

```python
import concurrent.futures

def ocr_page(page):
    return engine.recognize(page).text

with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
    texts = list(executor.map(ocr_page, tiff_image.pages))
```

## 將提取的文字儲存為檔案

大多數實務流程需要永久儲存。以下提供簡潔方式將每頁文字寫入各自的檔案，並保留頁面順序。

```python
import pathlib

output_dir = pathlib.Path("ocr_output")
output_dir.mkdir(exist_ok=True)

for i, result in enumerate(page_results, start=1):
    file_path = output_dir / f"page_{i:03}.txt"
    file_path.write_text(result.text, encoding="utf-8")
    print(f"Saved page {i} to {file_path}")
```

現在你已擁有一個整潔的 `.txt` 檔案目錄，可供索引或進一步的 NLP 處理。

## 圖像預覽 – 以視覺方式使用 OCR 結果

如果你想在原始圖像上看到 OCR 覆蓋層（除錯時很方便），許多函式庫允許繪製邊界框。以下是一個使用 Pillow 的簡易範例：

```python
from PIL import ImageDraw

for page, result in zip(tiff_image.pages, page_results):
    draw = ImageDraw.Draw(page)
    for word in result.words:          # Assume `result.words` gives bounding boxes
        draw.rectangle(word.box, outline="red")
    page.show()   # Opens the annotated page
```

![如何在 Python 中使用 OCR – TIFF 頁面的 OCR 覆蓋](ocr_overlay_example.png)

*替代文字:* 如何在 Python 中使用 OCR – 在 TIFF 頁面上視覺化覆蓋已辨識文字。

## 常見陷阱與避免方法

| 問題 | 發生原因 | 解決方式 |
|-------|----------------|-----|
| 文字亂碼 | 語言模型錯誤 | 將 `engine.language` 設為正確的 enum |
| 缺少頁面 | 不支援的 TIFF 壓縮 | 先將 TIFF 轉為未壓縮格式 |
| 效能緩慢 | 高 DPI + 單執行緒處理 | 降低 DPI 或啟用多執行緒 |
| 輸出為空 | 影像過暗/對比度低 | 使用對比拉伸前處理（`opencv` 或 `Pillow`） |

提前處理這些問題可為你節省大量除錯時間。

## 往後步驟 – 超越基本提取

現在你已掌握 **how to use OCR in Python** 的基礎，建議進一步探索：

- **PDF generation** – 使用 `reportlab` 結合提取的文字，重新建立可搜尋的 PDF。
- **Language detection** – 使用 `langdetect` 自動切換 `engine.language`。
- **Structured data extraction** – 使用正規表達式或 spaCy 從原始文字中抽取日期、姓名或表格等結構化資料。
- **Alternative OCR backends** – 若需多語言支援，可將 `ocr` 換成 `pytesseract` 或 `easyocr`。

上述每個主題皆自然關聯到次要關鍵字 **ocr library python**、**convert tiff to text**、**extract text from tiff** 與 **python ocr engine**，為你提供堅實的基礎以進行更進階的專案。

---

### 結論

我們已從安裝到多頁處理完整說明 **how to use OCR in Python**，示範如何使用簡易的 **python OCR engine** 正確 **convert TIFF to text** 與 **extract text from TIFF**。上述完整可執行的範例應可直接支援大多數標準 TIFF 檔案，且提供的技巧將協助你擴展至更大型文件或將 OCR 整合至更大的流程中。

試著使用自己的掃描書籍、收據或檔案影像來實作，然後探索「往後步驟」中列出的進階想法。祝編程愉快，願你的 OCR 結果始終精確！

## 接下來該學什麼？

以下教學涵蓋與本指南技術密切相關的主題，並提供完整可執行的程式碼範例與逐步說明，協助你精通額外的 API 功能，並在自己的專案中探索替代實作方式。

- [使用 Aspose OCR 從圖像提取文字 – 步驟說明指南](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [如何使用 Aspose.OCR for Java 從 TIFF 提取文字](/ocr/english/java/ocr-operations/recognize-tiff/)
- [如何使用 Aspose OCR 從串流執行圖像文字提取](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}