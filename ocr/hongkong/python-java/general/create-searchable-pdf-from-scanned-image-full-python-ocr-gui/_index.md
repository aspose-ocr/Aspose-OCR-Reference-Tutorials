---
category: general
date: 2026-07-05
description: 使用 Python 建立可搜尋的 PDF。了解如何對掃描的 PNG 進行 OCR、將掃描的影像 PDF 轉換，並在數分鐘內獲得可搜尋的 PDF。
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- how to ocr pdf
- ocr recognition example
- convert png searchable pdf
language: zh-hant
og_description: 快速建立可搜尋的 PDF。本指南說明如何對 PNG 進行 OCR、將掃描圖像 PDF 轉換，並使用 Python 產生可搜尋的 PDF。
og_title: 從掃描圖像建立可搜尋的 PDF – Python OCR 教學
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Create searchable PDF with Python. Learn how to OCR a scanned PNG,
    convert scanned image PDF, and get a searchable PDF in minutes.
  headline: Create Searchable PDF from Scanned Image – Full Python OCR Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF
- Automation
title: 從掃描圖像建立可搜尋 PDF – 完整 Python OCR 教學
url: /zh-hant/python-java/general/create-searchable-pdf-from-scanned-image-full-python-ocr-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從掃描圖像建立可搜尋 PDF – 完整 Python OCR 指南

你有沒有想過如何在不付高價軟件的情況下，從掃描圖片**建立可搜尋的 PDF**？你並不孤單。在許多辦公室，PDF 只是一張平面圖像——難以搜尋、無法複製貼上，且在合規審計時是個噩夢。好消息是？只要幾行 Python 程式碼，就能把那個靜態 PNG 轉換成完整可搜尋的 PDF，且過程比你想像的更簡單。

在本教學中，我們將逐步說明完整的**OCR 識別範例**，涵蓋從安裝正確的函式庫到寫入最終 PDF 檔案的全部步驟。完成後，你將清楚知道如何**轉換掃描圖像 PDF**檔案、如何以程式方式**how to ocr pdf**，並擁有一個可重複使用的腳本，隨時可放入任何專案。

## 你將學到什麼

- 安裝與設定 Python OCR 函式庫（我們將使用 `pytesseract` 與 `pdf2image`）。
- 初始化 OCR 引擎並設定語言。
- 載入掃描的 PNG（或任何影像）並執行 OCR。
- 將 OCR 結果轉換為**可搜尋的 PDF**（位元組陣列）並儲存。
- 處理多頁文件、不同語言以及常見陷阱的技巧。

不需要任何 OCR 經驗——只要有可運作的 Python 3 環境與一點好奇心。

---

## 建立可搜尋 PDF – 概觀

Below is a high‑level flowchart of the steps we’ll implement.  

![建立可搜尋 PDF 工作流程圖](https://example.com/flowchart.png "建立可搜尋 PDF 工作流程圖")

*Alt text: 建立可搜尋 PDF 工作流程圖，顯示引擎初始化、影像載入、OCR 識別、PDF 轉換與檔案寫入。*

## 步驟 1：初始化 OCR 引擎 (how to ocr pdf)

為什麼我們需要先初始化？OCR 引擎是將像素模式解讀為文字的“大腦”。透過建立引擎實例並明確設定語言，我們告訴函式庫應預期哪種字母表，這會大幅提升準確度。

```python
import pytesseract
from pdf2image import convert_from_path
from PIL import Image
import io

# Ensure Tesseract is on your PATH or provide the executable location
pytesseract.pytesseract.tesseract_cmd = r"/usr/local/bin/tesseract"  # adjust as needed

# Define the language – ENGLISH is the default, but you can add more (e.g., 'fra' for French)
ocr_language = "eng"
```

**小技巧：**如果需要對多語言文件進行 OCR，請為 Tesseract 安裝相應的語言套件，並將類似 `"eng+spa"` 的清單傳遞給 `ocr_language`。

## 步驟 2：載入掃描圖像 (convert scanned image pdf)

接下來的關鍵是將影像資料載入 Python。無論是單一 PNG 或多頁 TIFF，`PIL.Image` 類別都能開啟它。如果你是從已包含掃描圖像的 PDF 開始，`pdf2image` 會為我們將每一頁轉換成影像。

```python
# Path to the scanned image (PNG, JPG, TIFF, etc.)
image_path = "YOUR_DIRECTORY/scanned_agreement.png"

# Open the image using Pillow
image = Image.open(image_path)

# If you were starting from a scanned PDF, you could do:
# pages = convert_from_path("scanned.pdf", dpi=300)
# image = pages[0]  # just take the first page for this example
```

**為什麼重要：**將影像載入為 Pillow 物件可讓我們取得其原始像素資料，這是 OCR 引擎所需的。若跳過此步驟直接傳入原始位元組，會導致錯誤。

## 步驟 3：對影像執行 OCR 識別 (ocr recognition example)

現在是有趣的部分——讓引擎讀取文字。`pytesseract.image_to_pdf_or_hocr` 會回傳已包含隱形文字層的 PDF 位元串流，這正是我們製作**可搜尋 PDF**所需的。

```python
# Run OCR and ask for a PDF output (includes the hidden text layer)
pdf_bytes = pytesseract.image_to_pdf_or_hocr(
    image,
    lang=ocr_language,
    extension='pdf'  # returns PDF bytes
)

# pdf_bytes is a binary blob that can be saved directly to disk
```

**邊緣情況：**如果影像對比度低，考慮在 OCR 前先套用簡單的閾值處理：

```python
# Convert to grayscale and increase contrast
gray = image.convert('L')
threshold = gray.point(lambda x: 0 if x < 128 else 255, '1')
pdf_bytes = pytesseract.image_to_pdf_or_hocr(threshold, lang=ocr_language, extension='pdf')
```

這個微小的前處理步驟可以顯著提升準確度。

## 步驟 4：將 PDF 位元寫入檔案 (convert png searchable pdf)

OCR 函式庫提供給我們一個位元組陣列——可視為 PDF 檔案的原始內容。我們現在只需要將這些位元寫入磁碟。

```python
output_path = "YOUR_DIRECTORY/agreement_searchable.pdf"

with open(output_path, "wb") as f:
    f.write(pdf_bytes)

print(f"✅ Searchable PDF created at: {output_path}")
```

**你會看到：**在任何 PDF 檢視器中開啟產生的檔案，搜尋原始影像中確實出現的字詞。高亮應直接跳到該位置，證明隱形文字層確實有效。

## 步驟 5：擴充至多頁文件 (convert scanned image pdf)

現實中的合約常常跨越多頁。若要**convert scanned image pdf**包含多頁的檔案，需對每一頁迴圈、執行 OCR，並將產生的 PDF 合併。

```python
def ocr_image_to_pdf(image_obj, lang="eng"):
    """Helper that returns PDF bytes for a single image."""
    return pytesseract.image_to_pdf_or_hocr(image_obj, lang=lang, extension='pdf')

def merge_pdfs(pdf_bytes_list):
    """Combine multiple PDF byte streams into one."""
    from PyPDF2 import PdfMerger
    merger = PdfMerger()
    for i, pdf_bytes in enumerate(pdf_bytes_list):
        merger.append(io.BytesIO(pdf_bytes))
    output = io.BytesIO()
    merger.write(output)
    merger.close()
    return output.getvalue()

# Example: convert a multi‑page scanned PDF to searchable PDF
pages = convert_from_path("YOUR_DIRECTORY/scanned_contract.pdf", dpi=300)
pdf_parts = [ocr_image_to_pdf(p, lang=ocr_language) for p in pages]
final_pdf = merge_pdfs(pdf_parts)

with open("YOUR_DIRECTORY/contract_searchable.pdf", "wb") as f:
    f.write(final_pdf)

print("✅ Multi‑page searchable PDF created.")
```

**為什麼要合併？**每次呼叫 `image_to_pdf_or_hocr` 都會產生獨立的 PDF。合併它們可確保最終文件保留原始頁面順序。

## 常見陷阱與解決方法

| 症狀 | 可能原因 | 解決方法 |
|---------|--------------|-----|
| 開啟 PDF 後無法搜尋文字 | Tesseract 未偵測到任何字元（輸出為空） | 檢查影像品質、提升 DPI，或套用前處理（對比度、二值化）。 |
| 亂碼（例如 �） | 語言套件錯誤或缺少字型 | 安裝正確的語言資料（`tesseract‑lang‑eng`），並確保 `ocr_language` 相符。 |
| PDF 檔案尺寸過大（單頁影像 >10 MB） | 使用無損 PNG 作為來源；OCR 會加入全解析度影像 | 在 OCR 前縮小影像（A4 使用 `image.thumbnail((1240, 1754))`）。 |
| 腳本在 Windows 上因找不到 “tesseract.exe” 而崩潰 | Tesseract 可執行檔未在 PATH 中 | 加入 `pytesseract.pytesseract.tesseract_cmd = r"C:\\Program Files\\Tesseract-OCR\\tesseract.exe"`（依實際路徑調整）。 |

## 完整、可直接執行的腳本

把所有步驟整合起來，以下是一個可直接複製貼上並執行的單一檔案：

```python
#!/usr/bin/env python3
"""
create_searchable_pdf.py
A complete example that converts a scanned PNG (or PDF) into a searchable PDF using Tesseract OCR.
"""

import io
import sys
from pathlib import Path

import pytesseract
from pdf2image import convert_from_path
from PIL import Image
from PyPDF2 import PdfMerger

# -------------------- Configuration --------------------
# Adjust these paths for your environment
TESSERACT_CMD = r"/usr/local/bin/tesseract"   # macOS/Linux
# TESSERACT_CMD = r"C:\\Program Files\\Tesseract-OCR\\tesseract.exe"  # Windows
OCR_LANGUAGE = "eng"                         # Add '+spa' for Spanish, etc.
INPUT_PATH = Path("YOUR_DIRECTORY/scanned_agreement.png")
OUTPUT_PATH = Path("YOUR_DIRECTORY/agreement_searchable.pdf")
# -------------------------------------------------------

# Point pytesseract at the executable
pytesseract.pytesseract.tesseract_cmd = TESSERACT_CMD

def load_image(path: Path) -> Image.Image:
    """Load an image from disk; supports PNG, JPG, TIFF."""
    if not path.is_file():
        sys.exit(f"❌ File not found: {path}")
    return Image.open(path)

def ocr_to_pdf_bytes(img: Image.Image, lang: str = OCR_LANGUAGE) -> bytes:
    """Run OCR on a Pillow image and return PDF bytes with hidden text."""
    return pytesseract.image_to_pdf_or_hocr(img, lang=lang, extension='pdf')

def write_pdf(data: bytes, dest: Path):
    """Write PDF byte stream to a file."""
    dest.parent.mkdir(parents=True, exist_ok=True)
    with open(dest, "wb") as f:
        f.write(data)
    print(f"✅ Searchable PDF saved to {dest}")

def main():
    # Load the scanned image
    image = load_image(INPUT_PATH)

    # Optional: improve contrast for low‑quality scans
    # image = image.convert('L').point(lambda x: 0 if x < 128 else 255, '1')

    # OCR → PDF bytes
    pdf_bytes = ocr_to_pdf_bytes(image)

    # Save the result
    write_pdf(pdf_bytes, OUTPUT_PATH)

if __name__ == "__main__":
    main()
```

將其儲存為 `create_searchable_pdf.py`，將佔位符替換為實際路徑，然後執行：

```bash
python create_searchable_pdf.py
```

你應該會看到

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，建立在本篇示範的技術之上。每個資源皆提供完整可運作的程式碼範例與逐步說明，協助你精通更多 API 功能，並在自己的專案中探索替代實作方式。

- [如何在 .NET 使用 Aspose.OCR 進行 OCR PDF](/ocr/english/net/text-recognition/recognize-pdf/)
- [將影像轉換為 PDF C# – 儲存多頁 OCR 結果](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [在 Aspose.OCR for Java 中 OCR 識別 PDF 文件](/ocr/hongkong/java/ocr-operations/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}