---
category: general
date: 2026-06-06
description: 如何使用 Python 進行 PDF OCR，並從圖像建立可搜尋的 PDF 檔案。學習在數分鐘內加入可搜尋文字並將圖像轉換為 PDF/A。
draft: false
keywords:
- how to ocr pdf
- create searchable pdf
- add searchable text
- ocr image to pdf
- convert image to pdf/a
language: zh-hant
og_description: 一步一步教你 OCR PDF。學習使用簡易 Python 腳本為 PDF 添加可搜尋文字，並將影像轉換為 PDF/A。
og_title: 如何對 PDF 進行 OCR – 快速指南：建立可搜尋的 PDF
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to OCR PDF and create searchable PDF files from images using Python.
    Learn to add searchable text and convert image to PDF/A in minutes.
  headline: How to OCR PDF in Python – Create Searchable PDF from Images
  type: TechArticle
- description: How to OCR PDF and create searchable PDF files from images using Python.
    Learn to add searchable text and convert image to PDF/A in minutes.
  name: How to OCR PDF in Python – Create Searchable PDF from Images
  steps:
  - name: Why this matters
    text: '- **Preserving graphics** means the visual layout (tables, logos, stamps)
      stays exactly as the scanner captured it. - The `result` object typically contains
      a hidden text layer that we’ll later embed into the PDF. - Using `recognize_image`
      instead of `recognize_pdf` avoids an extra conversion step, '
  - name: Why this matters
    text: '- **Searchable PDF**: The output file contains a hidden, selectable text
      layer. You can now Ctrl + F through the document. - **PDF/A compliance**: Some
      organizations (legal, finance) require PDF/A for audit trails; this step satisfies
      that rule automatically. - The method also **adds searchable text'
  - name: Expected output
    text: 'When you run the script, the console prints:'
  type: HowTo
tags:
- OCR
- PDF
- Python
- Automation
title: 如何在 Python 中對 PDF 進行 OCR – 從圖片建立可搜尋的 PDF
url: /zh-hant/python-java/general/how-to-ocr-pdf-in-python-create-searchable-pdf-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何 OCR PDF – 將掃描圖像轉換為可搜尋的 PDF

有沒有想過 **如何 OCR PDF** 檔案，當你手上只有發票或收據的掃描圖像？你並不是唯一有此困惑的人。在許多辦公室，收到的文件往往是平面的 PNG 或 JPEG，而接下來的步驟——讓內容可搜尋——常常像個黑盒子。

好消息是？只要幾行 Python 程式碼，你就能 **建立可搜尋的 PDF** 檔案、**加入可搜尋的文字**，甚至 **將影像轉換為 PDF/A** 以作長期保存。在本教學中，我們會逐步說明每個步驟、解釋其重要性，並提供一段可直接執行的腳本，讓你可以隨時放入任何專案中使用。

> **專業提示：** 同樣的方法也適用於多頁掃描；只需對檔案進行迴圈，引擎會自行處理繁重的工作。

---

## 您需要的環境

在開始之前，請確保您的機器已具備以下項目：

| 需求 | 重要原因 |
|------|----------|
| Python 3.9 或更新版本 | 現代語法與更好的函式庫支援 |
| `pdfium` 為基礎的 OCR 引擎（例如 `pdfocr` 或商業 SDK） | 同時處理影像辨識與 PDF/A 產生 |
| 欲轉換為可搜尋 PDF 的影像檔（PNG、JPEG、TIFF） | 文字的來源 |
| 對輸出資料夾的寫入權限 | 讓腳本能儲存新 PDF |

如果尚未安裝 OCR SDK，請執行以下指令：

```bash
pip install pdfocr   # replace with your vendor's package name
```

就這樣——不需要複雜的系統相依，只要 pip 安裝即可。

---

## 如何 OCR PDF – 概觀

從高層次來看，整個流程包含三個簡單動作：

1. **辨識** 影像內的文字，同時保留原始圖形。  
2. **匯出** OCR 結果與原始影像為 **可搜尋的 PDF/A**（適合長期保存的 PDF 版本）。  
3. **驗證** 產生的檔案是否在原圖上疊加了可選取、可搜尋的文字層。

以下會以程式碼展示每個步驟，並說明指令背後的 *為什麼*。

---

## 步驟 1：從影像辨識文字

首先，我們請 OCR 引擎讀取像素，回傳一個同時包含原始影像與擷取文字的 result 物件。可以把它想成引擎為你「閱讀」發票。

```python
# Step 1: Recognize text from the image and keep the original graphics
result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
```

### 為什麼這很重要

- **保留圖形** 表示視覺版面（表格、商標、印章）會完全如掃描時的樣子保留下來。  
- `result` 物件通常會包含一個隱藏的文字層，我們稍後會把它嵌入 PDF。  
- 使用 `recognize_image` 而非 `recognize_pdf` 可避免額外的轉換步驟，對單頁影像的處理速度更快。

#### 常見變化

- 若你有 **多頁 TIFF**，直接傳入檔案路徑；大多數引擎會把每一頁視為獨立影像。  
- 若 PDF 已經內含影像，可呼叫 `engine.recognize_pdf("file.pdf")`，直接跳過此步驟。

---

## 步驟 2：將 OCR 結果匯出為可搜尋的 PDF/A

現在把步驟 1 取得的 `result` 交給引擎寫入新檔案。此處的關鍵旗標是 *PDF/A*——ISO 標準的長期保存 PDF 版本。

```python
# Step 2: Export the OCR result together with the original image as a searchable PDF/A
result.save_as_pdfa("YOUR_DIRECTORY/invoice_searchable.pdf")
```

### 為什麼這很重要

- **可搜尋的 PDF**：輸出檔案會包含隱藏且可選取的文字層，現在可以使用 Ctrl + F 進行搜尋。  
- **PDF/A 相容**：某些組織（法律、財務）要求使用 PDF/A 作為稽核追蹤，此步驟會自動滿足此規範。  
- 此方法同時 **加入可搜尋文字** 而不會將影像平面化，確保視覺保真度完好。

#### 邊緣情況：需要一般 PDF 而非 PDF/A？

如果不在乎 PDF/A，只要把 `save_as_pdfa` 換成 `save_as_pdf` 即可，其餘工作流程保持不變。

---

## 步驟 3：驗證可搜尋的 PDF

快速的 sanity check 可以避免日後出現神祕的錯誤。用任何 PDF 閱讀器開啟產生的檔案，試著選取文字，並使用搜尋功能。

```python
# Step 3: The file "invoice_searchable.pdf" now contains selectable text layered over the original invoice image
import subprocess, os

pdf_path = "YOUR_DIRECTORY/invoice_searchable.pdf"
if os.path.exists(pdf_path):
    print(f"✅ PDF created successfully: {pdf_path}")
    # Optionally open the file (works on macOS, Windows, Linux with appropriate commands)
    subprocess.run(["open", pdf_path] if os.name == "posix" else ["start", pdf_path], shell=True)
else:
    print("❌ Something went wrong – PDF not found.")
```

### 預期輸出

執行腳本時，主控台會印出：

```
✅ PDF created successfully: YOUR_DIRECTORY/invoice_searchable.pdf
```

開啟檔案後，你應該會看到原始發票影像上覆蓋著淡淡、看不見的文字層。選取任意單字會發現它是可選取的——**這就是剛剛加入的可搜尋文字**。

---

## 為既有 PDF 加入可搜尋文字（加分）

有時候你已經有 PDF，但需要 **加入可搜尋文字**。同樣的引擎可以把 OCR 結果覆蓋到既有 PDF 上：

```python
# Bonus: Add searchable text to an existing PDF file
existing_pdf = engine.load_pdf("YOUR_DIRECTORY/old_scanned.pdf")
ocr_result = engine.recognize_pdf("YOUR_DIRECTORY/old_scanned.pdf")
ocr_result.apply_to(existing_pdf).save_as_pdfa("YOUR_DIRECTORY/old_scanned_searchable.pdf")
```

此處的 `apply_to` 會將隱藏層與原始頁面合併，讓你 **建立可搜尋的 PDF** 而不必重新掃描。

---

## 常見問題與技巧

| 常見問題 | 避免方法 |
|----------|----------|
| **低解析度來源影像** (< 150 dpi) | 放大或要求更高解析度的掃描；解析度低於 150 dpi 時 OCR 準確度會急劇下降。 |
| **缺少語言資料** | 安裝對應的語言套件，例如 `pip install pdfocr[eng,spa]`。 |
| **輸出資料夾無寫入權限** | 以足夠權限執行腳本，或改用其他目錄。 |
| **PDF/A 驗證失敗** | 確認未嵌入不支援的字型或 JavaScript；使用 `save_as_pdfa` 時大多數 SDK 會自動處理。 |

---

## 完整腳本 – 單檔解決方案

以下是一段自包含的腳本，將所有步驟串接在一起。直接複製貼上、替換佔位路徑，即可在數秒內 **將影像轉換為 PDF/A**。

```python
#!/usr/bin/env python3
"""
How to OCR PDF – Complete script to create a searchable PDF/A from an image.
Works with any OCR engine exposing `recognize_image` and `save_as_pdfa`.
"""

import os
import subprocess

# ----------------------------------------------------------------------
# CONFIGURATION – change these paths to match your environment
# ----------------------------------------------------------------------
INPUT_IMAGE = "YOUR_DIRECTORY/invoice.png"
OUTPUT_PDF  = "YOUR_DIRECTORY/invoice_searchable.pdf"

# ----------------------------------------------------------------------
# INITIALIZE THE OCR ENGINE (replace with your SDK's init call)
# ----------------------------------------------------------------------
# Example for a fictional `pdfocr` package:
# from pdfocr import Engine
# engine = Engine(api_key="YOUR_API_KEY")
# If you use a different library, adjust the import and init accordingly.
engine = Engine()  # placeholder – insert real initialization here

def main():
    # Step 1 – Recognize the image
    print(f"🔎 Recognizing text from {INPUT_IMAGE} …")
    result = engine.recognize_image(INPUT_IMAGE)

    # Step 2 – Save as searchable PDF/A
    print(f"💾 Saving searchable PDF/A to {OUTPUT_PDF} …")
    result.save_as_pdfa(OUTPUT_PDF)

    # Step 3 – Verify the file exists
    if os.path.isfile(OUTPUT_PDF):
        print("✅ Success! Searchable PDF/A created.")
        # Open the file for a quick visual check (optional)
        try:
            if os.name == "posix":
                subprocess.run(["open", OUTPUT_PDF])
            else:
                subprocess.run(["start", OUTPUT_PDF], shell=True)
        except Exception:
            pass
    else:
        print("❌ Error: PDF not created.")

if __name__ == "__main__":
    main()
```

**此腳本的功能：**  
1. 載入 OCR 引擎。  
2. 讀取選定的影像並擷取文字。  
3. 寫入 **可搜尋的 PDF/A**，可立即分發或保存。

如需批次處理整個資料夾，只要把 `main` 邏輯包在函式裡，使用 `os.listdir()` 迭代即可，對每個檔案重複上述三個步驟。

---

## 後續步驟與相關主題

既然已掌握 **如何 OCR PDF**，不妨探索以下進階想法：

- **批次處理：** 使用 `concurrent.futures` 同時 OCR 數十張發票。  
- **中繼資料注入：** 為 PDF 加入建立日期或發票編號等中繼資料，方便索引。  
- **混合 PDF：** 結合可搜尋文字與嵌入的原始影像，打造文件的「數位雙生」。  
- **其他輸出格式：** 若下游系統需要可編輯檔案，可匯出為 **DOCX** 或 **HTML**。

上述每項都建基於你剛學會的三個核心概念：辨識、匯出、驗證。

---

## 總結

簡而言之，你現在已掌握 **如何 OCR PDF**：只要三行 Python 程式碼，就能把單純的影像變成 **可搜尋的 PDF/A**。腳本負責繁重的工作、保留原始圖形，並產生符合標準的文件，讓你可以搜尋、保存或分享。

快把它套用在自己的發票、收據或掃描合約上吧。若遇到任何問題，歡迎在下方留言或查閱 SDK 官方文件——那裡通常還有更多範例。祝開發愉快，盡情享受將任何影像即時變為可搜尋的全新能力！

![How to OCR PDF example showing original image and searchable PDF overlay](placeholder.png "How to OCR PDF example")

## 接下來該學什麼？

以下教學與本指南示範的技術緊密相關，提供完整可執行的程式碼範例與逐步說明，協助你掌握更多 API 功能，並在自己的專案中探索替代實作方式。

- [如何在 .NET 使用 Aspose.OCR 進行 OCR PDF](/ocr/english/net/text-recognition/recognize-pdf/)
- [使用 Aspose.OCR for Java 進行 PDF 文字辨識 – OCR 操作](/ocr/english/java/ocr-operations/)
- [C# 影像轉 PDF – 儲存多頁 OCR 結果](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}