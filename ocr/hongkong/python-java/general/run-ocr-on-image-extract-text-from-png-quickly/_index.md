---
category: general
date: 2026-03-18
description: 對圖像執行 OCR，從 PNG 中提取文字並產生可搜尋的 PDF。了解如何辨識文字圖像，並在數分鐘內將 PNG 轉換為 PDF。
draft: false
keywords:
- run OCR on image
- extract text from png
- recognize text image
- generate searchable pdf
- convert png to pdf
language: zh-hant
og_description: 執行 OCR 於圖像以從 PNG 提取文字，辨識文字圖像，並產生可搜尋的 PDF。請跟隨此一步一步的指南。
og_title: 對圖像執行 OCR – 快速從 PNG 提取文字
tags:
- OCR
- Python
- Image Processing
title: 在圖像上執行 OCR – 快速從 PNG 提取文字
url: /zh-hant/python-java/general/run-ocr-on-image-extract-text-from-png-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在圖像上執行 OCR – 快速從 PNG 提取文字

有沒有過想 **在圖像上執行 OCR** 卻不知道從哪裡開始的時候？也許你手上有一個已掃描的文章 `article.png`，只想取得純文字，或是需要一個可搜尋的 PDF 來做歸檔。無論哪種情況，你都來對地方了。本教學將一步步說明如何從 PNG 提取文字、辨識文字圖像，甚至把 PNG 轉成可搜尋的 PDF——只需要幾行程式碼。

> **你將得到：** 一個完整、可直接執行的腳本，能載入 PNG、執行 OCR、儲存 hOCR 輸出，並可選擇產生可搜尋的 PDF。沒有缺少的 import，沒有「請參考文件」的死路——只要把這段自包含的解決方案直接放入你的專案即可使用。

## 前置條件

在開始之前，請確保你已具備：

- **Python 3.8+**（此語法在任何近期版本皆可執行）
- 你正在使用的 **`ocr_engine`** 函式庫（範例假設有一個 `OcrEngine` 類別；若使用 Tesseract、EasyOCR 等，請自行替換）
- 想要處理的 PNG 圖片（例如放在可參照的資料夾中的 `article.png`）
- 對輸出目錄的寫入權限

如果底層使用 Tesseract，請先安裝：

```bash
# Ubuntu/Debian
sudo apt-get install tesseract-ocr

# macOS (Homebrew)
brew install tesseract
```

接著安裝 Python 包裝器：

```bash
pip install pytesseract Pillow
```

*Pro tip:* 定期更新 OCR 函式庫——新語言包與效能優化會不斷推出。

## 在圖像上執行 OCR – 步驟指南

以下是 **完整腳本**。直接複製貼上成 `run_ocr.py`，再以 `python run_ocr.py` 執行即可。

```python
# run_ocr.py
import os
from pathlib import Path

# Import the OCR engine – replace with your actual import if different
# For Tesseract via pytesseract you would use: import pytesseract
# Here we assume a generic OcrEngine class that matches the example
from ocr_engine import OcrEngine  # <-- adjust as needed

def main():
    # ------------------------------------------------------------------
    # Step 1: Create an OCR engine instance
    # ------------------------------------------------------------------
    ocr_engine = OcrEngine()
    # Why this matters: the engine holds configuration (language, DPI, etc.)
    # You can tweak ocr_engine.setLanguage('eng') or similar before proceeding.

    # ------------------------------------------------------------------
    # Step 2: Load the image you want to process
    # ------------------------------------------------------------------
    image_path = Path("YOUR_DIRECTORY/article.png")
    if not image_path.is_file():
        raise FileNotFoundError(f"Image not found: {image_path}")
    ocr_engine.setImageFromFile(str(image_path))

    # ------------------------------------------------------------------
    # Step 3: Choose the export format
    # ------------------------------------------------------------------
    # hOCR preserves layout (bounding boxes, fonts) – perfect for searchable PDFs.
    # Other options: "txt", "pdf", "pdfa"
    ocr_engine.setExportFormat("hocr")

    # ------------------------------------------------------------------
    # Step 4: Run the recognition process
    # ------------------------------------------------------------------
    ocr_result = ocr_engine.recognize()
    # The result object gives us access to the raw OCR text, hOCR, etc.

    # ------------------------------------------------------------------
    # Step 5: Write the HOCR output to a file
    # ------------------------------------------------------------------
    output_path = Path("YOUR_DIRECTORY/article.hocr")
    with open(output_path, "w", encoding="utf-8") as output_file:
        output_file.write(ocr_result.getExportedContent())
    print(f"✅ HOCR saved to {output_path}")

    # ------------------------------------------------------------------
    # Optional: Generate a searchable PDF from the HOCR
    # ------------------------------------------------------------------
    # Many OCR engines can bundle the original image with the hOCR to produce
    # a PDF that you can search. If your engine supports it, uncomment:
    # ocr_engine.setExportFormat("pdf")
    # pdf_result = ocr_engine.recognize()
    # pdf_path = Path("YOUR_DIRECTORY/article_searchable.pdf")
    # with open(pdf_path, "wb") as pdf_file:
    #     pdf_file.write(pdf_result.getExportedContent())
    # print(f"📄 Searchable PDF created at {pdf_path}")

if __name__ == "__main__":
    main()
```

### 腳本功能說明（簡明說明）

1. **Instantiate** OCR 引擎，以便控制其設定。
2. **Load** PNG 檔案（`article.png`）。若檔案不存在，腳本會提前中止，避免之後出現神祕的 `NoneType` 錯誤。
3. **Select** `hocr` 為匯出格式。此格式保留原始版面配置，對於之後轉成可搜尋 PDF 相當重要。
4. **Run** 辨識引擎；繁重的運算就在這裡完成。
5. **Write** hOCR XML 到 `article.hocr`。此時你已擁有機器可讀的文字與座標資訊。
6. *(Optional)* 切換成 `"pdf"`，再額外執行一步即可產生可搜尋的 PDF。

**預期輸出** 為 UTF‑8 編碼的 `.hocr` 檔案，內容大致如下（為簡潔起見已裁切）：

```xml
<div class='ocr_page' id='page_1' title='image "article.png"; bbox 0 0 2480 3508; ppageno 0'>
  <div class='ocr_carea' id='block_1_1' title="bbox 100 100 2400 3400">
    <p class='ocr_par' id='par_1' title="bbox 100 100 2400 200">
      <span class='ocr_line' id='line_1' title="bbox 100 100 2400 150; baseline 0 -5">
        <span class='ocrx_word' id='word_1' title="bbox 100 100 300 150; x_wconf 96">This</span>
        <span class='ocrx_word' id='word_2' title="bbox 310 100 500 150; x_wconf 92">is</span>
        …
```

若取消註解 PDF 區段，還會產生 `article_searchable.pdf`，可在任何 PDF 閱讀器中使用 **Ctrl + F** 立即搜尋關鍵字。

![在圖像上執行 OCR 範例輸出](example.png "在圖像上執行 OCR – hOCR 與 PDF 結果")

## 使用 OcrEngine 從 PNG 提取文字

如果只需要純文字（不需要版面或 PDF），可以直接跳過 hOCR 步驟：

```python
ocr_engine.setExportFormat("txt")
text_result = ocr_engine.recognize()
plain_text = text_result.getExportedContent()
print("📝 Extracted text:\n", plain_text)
```

*為什麼選擇純文字？* 輕量、適合建立索引，且能順利串接下游的 NLP 流程。

## 識別文字圖像並產生可搜尋 PDF

產生可搜尋 PDF 需要兩個步驟：

1. **Run OCR** 使用 `hocr`（如上所示）取得版面資訊。
2. **Combine** 原始 PNG 與 hOCR，透過引擎的 PDF 匯出功能合成 PDF。

大多數現代 OCR 函式庫（Tesseract、ABBYY、Google Vision）皆提供 `pdf` 匯出，正好完成上述工作。主腳本中 *Optional* 區塊的程式碼即示範此模式。若你的函式庫沒有內建 PDF 匯出功能，也可以使用 **`pdf2image`** + **`reportlab`** 手動把圖像與 hOCR 合併——有需要的話請告訴我，我會再提供簡易範例。

## 使用 OCR 輸出將 PNG 轉換為 PDF

有時只想要一個 **純 PDF**（僅包含圖像，沒有可搜尋層），更為簡單：

```python
from PIL import Image

png_path = Path("YOUR_DIRECTORY/article.png")
pdf_path = Path("YOUR_DIRECTORY/article.pdf")

# Pillow can convert directly:
Image.open(png_path).convert("RGB").save(pdf_path, "PDF", resolution=100.0)
print(f"📄 PNG converted to PDF at {pdf_path}")
```

若同時需要可搜尋版本，可把此步驟與 OCR 步驟結合；若僅作為視覺備份，則直接使用此 PDF 即可。

## 常見問題與技巧

| 問題 | 為何會發生 | 快速解決方案 |
|------|------------|--------------|
| **模糊或低解析度 PNG** | OCR 準確度在低於約 300 DPI 時會急速下降。 | 在送入引擎前使用 `Image.resize((width*2, height*2), Image.LANCZOS)` 進行放大。 |
| **語言設定錯誤** | 引擎預設為英文，非英文字符會變成亂碼。 | 在 `recognize()` 前呼叫 `ocr_engine.setLanguage('deu')`（或其他 ISO 語言碼）。 |
| **缺少 hOCR 輸出** | 若未呼叫 `setExportFormat`，部分引擎會預設輸出純文字。 | 確認 `setExportFormat("hocr")` **在** `recognize()` **之前** 執行。 |
| **檔案權限錯誤** | 嘗試寫入唯讀資料夾。 | 改用專案內的路徑，或先執行 `os.makedirs(..., exist_ok=True)`。 |
| **大型 PDF 造成記憶體激增** | PDF 匯出會一次將整張圖像載入記憶體。 | 分批處理頁面或使用串流式 PDF 寫入器。 |

*Pro tip:* 先在小樣本圖像上測試，再批次處理上千張，能省下大量除錯時間。

## 總結

現在你已掌握 **在圖像上執行 OCR**、**從 PNG 提取文字**、**辨識文字圖像** 以供後續任務使用、**產生可搜尋 PDF**，以及 **將 PNG 轉成 PDF** 的完整流程。提供的腳本是一個即拿即用的完整範例，選項化的區塊讓你可以依需求自行調整工作流程。

### 接下來做什麼？

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}