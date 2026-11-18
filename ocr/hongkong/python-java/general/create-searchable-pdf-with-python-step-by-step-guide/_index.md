---
category: general
date: 2026-05-31
description: 使用 Python OCR 從掃描影像建立可搜尋的 PDF。學習如何將掃描影像 PDF 轉換、將 TIFF 轉為 PDF，並在數分鐘內加入
  OCR 文字層。
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- convert tiff to pdf
- how to run OCR
- add OCR text layer
language: zh-hant
og_description: 即時建立可搜尋的 PDF。本指南示範如何使用單一 Python 程式執行 OCR、將掃描圖像 PDF 轉換，並加入 OCR 文字層。
og_title: 使用 Python 建立可搜尋 PDF – 完整教學
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Create searchable PDF from scanned images using Python OCR. Learn how
    to convert scanned image PDF, convert TIFF to PDF, and add OCR text layer in minutes.
  headline: Create Searchable PDF with Python – Step‑by‑Step Guide
  type: TechArticle
- description: Create searchable PDF from scanned images using Python OCR. Learn how
    to convert scanned image PDF, convert TIFF to PDF, and add OCR text layer in minutes.
  name: Create Searchable PDF with Python – Step‑by‑Step Guide
  steps:
  - name: Expected Output
    text: 'Running the script prints:'
  - name: 1️⃣ Can I process multi‑page PDFs?
    text: Yes. Use `ocr_engine.load_image("file.pdf")` and then loop over each page
      with `ocr_engine.recognize(pdf_save_options, page_number)`. The library will
      automatically generate a multi‑page searchable PDF.
  - name: 2️⃣ What if my source file is a high‑resolution TIFF (300 dpi+)?
    text: 'Higher DPI yields better OCR accuracy but also larger memory usage. If
      you hit a `MemoryError`, downscale the image first:'
  - name: 3️⃣ How do I change the language of the OCR?
    text: 'Set the `language` property on the engine before loading the image:'
  - name: 4️⃣ What if I need to keep the original image quality?
    text: The `PdfSaveOptions` class has a `compression` property. Set it to `PdfCompression.None`
      to preserve the raster data exactly as it was.
  type: HowTo
tags:
- OCR
- Python
- PDF
- Document Automation
title: 使用 Python 建立可搜尋的 PDF – 步驟指南
url: /zh-hant/python-java/general/create-searchable-pdf-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Python 建立可搜尋 PDF – 步驟指南

有沒有想過 **如何從掃描頁面建立可搜尋 PDF**，卻不需要切換好幾個工具？你並不孤單。在許多辦公流程中，掃描的 TIFF 或 JPEG 會被放到共享磁碟，接下來的人只能手動複製貼上文字——既痛苦又容易出錯，還浪費時間。

在本教學中，我們將一步步示範一個乾淨、程式化的解決方案，讓你 **轉換掃描影像 PDF**、**將 TIFF 轉成 PDF**，以及 **加入 OCR 文字層**，一次完成。完成後，你將擁有一支可直接執行 OCR、嵌入隱藏文字，並輸出可搜尋 PDF 的腳本，隨時可以索引、搜尋或自信地分享。

## 需要的環境

- Python 3.9+（任何較新的版本皆可）
- `aspose-ocr` 與 `aspose-pdf` 套件（使用 `pip install aspose-ocr aspose-pdf` 安裝）
- 一個掃描的影像檔（`.tif`、`.png`、`.jpg`，或僅含影像的 PDF 頁面）
- 一點點記憶體（OCR 引擎相當輕量，筆記型電腦也能應付）

> **小技巧：** 若你使用 Windows，最簡單的取得套件方式是以系統管理員身分在 PowerShell 視窗執行上述指令。

```bash
pip install aspose-ocr aspose-pdf
```

現在前置作業已完成，讓我們進入程式碼。

## 步驟 1：建立 OCR 引擎實例 – *create searchable pdf*

首先，我們要啟動 OCR 引擎。它就像大腦，會讀取每個像素並轉換成文字。

```python
from aspose.ocr import OcrEngine

# Initialize the OCR engine – this is the core of the create searchable pdf process
ocr_engine = OcrEngine()
```

> **為什麼這很重要：** 只初始化一次引擎即可降低記憶體使用量。如果在迴圈裡每頁都呼叫 `OcrEngine()`，資源很快就會耗盡。

## 步驟 2：載入掃描影像 – *convert tiff to pdf* & *convert scanned image pdf*

接著，將引擎指向要處理的檔案。API 接受任何點陣圖，所以 TIFF 與 JPEG 同樣適用。

```python
# Load the image you want to OCR. Replace the path with your own file location.
ocr_engine.load_image("YOUR_DIRECTORY/scanned_page.tif")
```

如果你手上有只包含掃描影像的 PDF，也可以使用 `load_image`，Aspose 會自動擷取第一頁。

## 步驟 3：設定 PDF 儲存選項 – *add OCR text layer*

在這裡我們設定最終 PDF 的樣貌。關鍵的旗標是 `create_searchable_pdf`；將它設為 `True` 即告訴函式庫嵌入一層與視覺內容對應的隱形文字層。

```python
from aspose.pdf import PdfSaveOptions

pdf_save_options = PdfSaveOptions()
pdf_save_options.create_searchable_pdf = True   # embed OCR text layer
pdf_save_options.output_path = "YOUR_DIRECTORY/scanned_page_searchable.pdf"
```

> **文字層的作用：** 當你在 Adobe Reader 開啟產生的檔案並嘗試選取文字時，會看到隱藏的字元。搜尋引擎也能索引它們——非常適合合規或保存需求。

## 步驟 4：執行 OCR 並儲存 – *how to run OCR* in a single call

現在魔法發生了。只要一次方法呼叫，就會執行辨識引擎並將可搜尋 PDF 寫入磁碟。

```python
# Run OCR and generate the searchable PDF in one go
ocr_engine.recognize(pdf_save_options)

print("PDF saved as searchable PDF.")
```

`recognize` 方法會回傳一個狀態物件，你可以檢查是否有錯誤，但對於大多數簡單情境，上述單行呼叫已足夠。

### 預期輸出

執行腳本時會印出：

```
PDF saved as searchable PDF.
```

若開啟 `scanned_page_searchable.pdf`，你會發現可以選取文字、複製貼上，甚至使用 `Ctrl+F` 搜尋。這正是 **create searchable pdf** 工作流程的標誌。

## 完整範例腳本

以下是可直接執行的完整腳本。只要把佔位路徑換成實際檔案位置即可。

```python
# ------------------------------------------------------------
# create_searchable_pdf.py – Convert scanned image to searchable PDF
# ------------------------------------------------------------

from aspose.ocr import OcrEngine
from aspose.pdf import PdfSaveOptions

def main():
    # 1️⃣ Initialize OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load image (TIFF, JPEG, PNG, or scanned PDF page)
    image_path = "YOUR_DIRECTORY/scanned_page.tif"
    ocr_engine.load_image(image_path)

    # 3️⃣ Configure PDF output – embed OCR text layer
    pdf_save_options = PdfSaveOptions()
    pdf_save_options.create_searchable_pdf = True
    pdf_save_options.output_path = "YOUR_DIRECTORY/scanned_page_searchable.pdf"

    # 4️⃣ Run OCR and write searchable PDF
    ocr_engine.recognize(pdf_save_options)

    print("PDF saved as searchable PDF.")

if __name__ == "__main__":
    main()
```

將檔案儲存為 `create_searchable_pdf.py` 後執行：

```bash
python create_searchable_pdf.py
```

## 常見問題與特殊情況

### 1️⃣ 可以處理多頁 PDF 嗎？

可以。使用 `ocr_engine.load_image("file.pdf")` 後，搭配 `ocr_engine.recognize(pdf_save_options, page_number)` 於每一頁迴圈。函式庫會自動產生多頁的可搜尋 PDF。

### 2️⃣ 若來源檔案是高解析度 TIFF（300 dpi 以上）怎麼辦？

較高 DPI 能提升 OCR 正確率，但也會佔用更多記憶體。若遭遇 `MemoryError`，請先將影像縮小：

```python
from PIL import Image
img = Image.open(image_path)
img = img.resize((int(img.width * 0.5), int(img.height * 0.5)), Image.ANTIALIAS)
img.save("temp.tif")
ocr_engine.load_image("temp.tif")
```

### 3️⃣ 如何變更 OCR 的語言？

在載入影像前，設定引擎的 `language` 屬性：

```python
ocr_engine.language = "fra"   # French
```

完整的語言代碼清單可參考 Aspose 官方文件。

### 4️⃣ 若我要保留原始影像品質？

`PdfSaveOptions` 類別提供 `compression` 屬性。將其設為 `PdfCompression.None` 即可完整保留點陣資料。

```python
pdf_save_options.compression = "None"
```

## 產品化部署小技巧

- **批次處理：** 將核心邏輯封裝成接受檔案路徑清單的函式，並將每筆成功或失敗寫入 CSV，以作稽核。
- **平行執行：** 使用 `concurrent.futures.ThreadPoolExecutor` 在多核心上同時執行 OCR。記得每個執行緒都需要自己的 `OcrEngine` 實例。
- **安全性：** 若處理機密文件，請在沙盒環境執行腳本，並在處理完畢後立即刪除暫存檔。

## 結論

現在你已掌握如何使用簡潔的 Python 腳本 **建立可搜尋 PDF**，只要初始化 OCR 引擎、載入 TIFF（或任何點陣圖）、設定 `PdfSaveOptions` 以 **add OCR text layer**，最後呼叫 `recognize`，整個 **convert scanned image pdf** 與 **convert TIFF to PDF** 流程即可一次完成、可重複執行。

接下來的步驟是什麼？可以把此腳本與檔案監控程式結合，讓任何新掃描的檔案一放入資料夾就自動變成可搜尋的 PDF。或是嘗試不同的 OCR 語言，以支援多語言檔案庫。只要結合 OCR 與 PDF 產生，想像空間無限。

對 **how to run OCR** 在其他語言或框架有更多疑問嗎？歡迎在下方留言，祝編程愉快！

![掃描影像 → OCR 引擎 → 可搜尋 PDF（create searchable pdf）流程圖](searchable-pdf-flow.png "建立可搜尋 PDF 流程圖")


## 接下來該學什麼？

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}