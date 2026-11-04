---
category: general
date: 2026-01-12
description: 學習如何在 Python 中對 PDF 進行 OCR，快速將 PDF 轉為可搜尋。使用 Aspose OCR 轉換掃描 PDF、提取文字
  PDF，並對掃描 PDF 進行 OCR。
draft: false
keywords:
- how to ocr pdf
- make pdf searchable
- convert scanned pdf
- extract text pdf
- ocr scanned pdf python
language: zh-hant
og_description: 如何在 Python 中進行 PDF OCR？本分步教學將示範如何將掃描版 PDF 轉換為可搜尋的 PDF，並使用 Aspose OCR
  提取文字。
og_title: 如何 OCR PDF 並使其可搜尋 – Python 指南
tags:
- OCR
- Python
- PDF processing
title: 如何對 PDF 進行 OCR 並使其可搜尋 – Python 指南
url: /zh-hant/python-java/general/how-to-ocr-pdf-and-make-it-searchable-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Python OCR PDF 並使其可搜尋

有沒有想過 **如何 OCR PDF** 而不必花大錢購買商業軟體？你並不孤單。許多開發者在需要將掃描的合約、發票或任何影像型 PDF 轉換成可搜尋的文件時，都會卡關。好消息是，只要幾行 Python 程式碼加上 Aspose OCR，就能在數分鐘內將掃描 PDF 轉換、提取文字 PDF，最終產生可搜尋的 PDF。

在本教學中，我們會一步步說明所有必備內容：從安裝函式庫、設定語言、處理掃描 PDF，到將結果儲存為同時包含原始影像與隱藏文字層的可搜尋 PDF。完成後，你將擁有一個可直接套用於任何專案的可重用腳本——不需要手動複製貼上。

---

## 需要的條件

- **Python 3.8+**（程式碼在 3.9、3.10 以及更新版本皆可執行）
- 有效的 **Aspose OCR for Python** 授權（免費試用版足以進行測試）
- 一個掃描的 PDF 檔案（例如 `scanned_contract.pdf`），你想要讓它可搜尋
- 基本的命令列與虛擬環境使用經驗（非必須，但建議）

> **專業提示：** 若尚未取得授權，可前往 Aspose 官網申請 30 天試用；試用版在開發階段功能完整。

---

## 如何使用 Aspose OCR OCR PDF（H2 主要關鍵字）

第一步是取得正確的套件。Aspose OCR 提供簡潔的高階 API，將底層影像處理細節抽象化。

```bash
# Create a virtual environment (optional but tidy)
python -m venv venv
source venv/bin/activate   # On Windows use `venv\Scripts\activate`

# Install the Aspose OCR package
pip install aspose-ocr
```

套件安裝完成後，即可開始撰寫腳本。

```python
# Step 1: Import the Aspose OCR module
import asposeocr as ocr

# Step 2: Create an OCR engine instance and set the recognition language
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

> **為什麼要設定語言？**  
> OCR 的準確度高度依賴語言模型。明確告訴引擎預期的文字為英文，可減少誤判並加快處理速度。

---

## 步驟 2：將掃描 PDF 轉換為可搜尋 PDF

引擎就緒後，指向你的掃描文件。`process_pdf` 方法會回傳一個 `PdfResult` 物件，內含原始影像資料與辨識出的文字。

```python
# Step 3: Process the scanned PDF to extract text
input_pdf_path = "YOUR_DIRECTORY/scanned_contract.pdf"
pdf_result = ocr_engine.process_pdf(input_pdf_path)
```

如果需要 **批次轉換掃描 PDF**，只要對資料夾進行迴圈，對每個檔案呼叫 `process_pdf` 即可。引擎會自動處理多頁 PDF。

---

## 步驟 3：將結果儲存為可搜尋 PDF（Make PDF Searchable）

最後一步是將可搜尋版本寫入磁碟。Aspose OCR 只需一行程式碼：

```python
# Step 4: Define the output path for the searchable PDF
searchable_pdf_path = "YOUR_DIRECTORY/contract_searchable.pdf"

# Step 5: Save the result as a searchable PDF (image + hidden text layer)
pdf_result.save_as_searchable_pdf(searchable_pdf_path)
```

當你在任何 PDF 閱讀器中開啟 `contract_searchable.pdf` 時，會看到原始掃描影像，但現在可以 **搜尋任何 OCR 引擎辨識出的字詞**。隱藏的文字層對肉眼不可見，卻能被完整索引。

---

### 完整腳本 – 可直接執行

以下是完整、可執行的範例。將它複製貼上至名為 `make_searchable.py` 的檔案，並依照你的環境調整路徑。

```python
# make_searchable.py
# -------------------------------------------------
# Complete script to OCR a scanned PDF and make it searchable
# -------------------------------------------------

import os
import asposeocr as ocr

def ocr_to_searchable(input_path: str, output_path: str, language=ocr.Language.ENGLISH):
    """
    Convert a scanned PDF into a searchable PDF.
    
    Parameters
    ----------
    input_path : str
        Path to the scanned PDF file.
    output_path : str
        Destination path for the searchable PDF.
    language : ocr.Language, optional
        OCR language model (default is English).
    """
    if not os.path.isfile(input_path):
        raise FileNotFoundError(f"Input file not found: {input_path}")

    # Initialize OCR engine
    engine = ocr.OcrEngine()
    engine.language = language

    # Process the PDF (extracts images + hidden text)
    result = engine.process_pdf(input_path)

    # Save as searchable PDF
    result.save_as_searchable_pdf(output_path)
    print(f"✅ Searchable PDF saved to: {output_path}")

if __name__ == "__main__":
    # Example usage – replace with your actual file locations
    INPUT_PDF = "YOUR_DIRECTORY/scanned_contract.pdf"
    OUTPUT_PDF = "YOUR_DIRECTORY/contract_searchable.pdf"
    ocr_to_searchable(INPUT_PDF, OUTPUT_PDF)
```

**預期輸出：**  
執行腳本後會印出確認訊息，並產生 `contract_searchable.pdf`。開啟檔案，按 `Ctrl + F`，輸入原始掃描影像中出現的任意字詞，即可立即看到匹配結果。

---

## 常見問題與特殊情況

### 1. 若 PDF 包含多種語言該怎麼辦？

可以將語言列表傳給引擎：

```python
engine.language = [ocr.Language.ENGLISH, ocr.Language.SPANISH]
```

Aspose OCR 會嘗試同時辨識同一頁面的多種語言。

### 2. 如何處理低解析度的掃描？

若來源影像低於 150 dpi，OCR 準確度可能下降。可先使用 `pdfimages` 抽取頁面，利用 Pillow 放大影像，然後再將高解析度的影像送入 `process_pdf`。

### 3. 是否能只提取純文字而不產生可搜尋 PDF？

當然可以。`PdfResult` 物件提供 `text` 屬性：

```python
plain_text = pdf_result.text
print(plain_text[:500])  # preview first 500 characters
```

這正符合 **extract text pdf** 的需求，僅取得原始字元。

### 4. 有沒有辦法批次處理整個資料夾？

有——只要將 `ocr_to_searchable` 函式包在簡單的迴圈中：

```python
import glob

for src in glob.glob("scans/*.pdf"):
    dst = src.replace("scans/", "searchable/").replace(".pdf", "_searchable.pdf")
    ocr_to_searchable(src, dst)
```

如此即可一次指令 **批次轉換掃描 pdf**。

---

## 效能小技巧

- **重複使用引擎**：每個檔案都重新建立 `OcrEngine` 會增加額外開銷。建議只建立一次，於多次呼叫間重複使用。
- **平行處理**：對於大量批次，可考慮 Python 的 `concurrent.futures.ThreadPoolExecutor`——Aspose OCR 在唯讀操作下是執行緒安全的。
- **記憶體管理**：若處理數百頁的大型 PDF，於每個檔案處理完畢後呼叫 `gc.collect()` 以釋放記憶體。

---

## 結論

我們已說明 **如何在 Python 中 OCR PDF**，將掃描檔轉換為 **可搜尋 PDF**，並示範如何直接 **extract text PDF**。使用 Aspose OCR，你即可獲得支援多頁文件、多語言與高準確度辨識的可靠引擎，且只需幾行程式碼。

不妨先在自己的合約、發票或存檔的研究論文上試試看。掌握基礎後，可進一步探索進階功能——如自訂字典、影像前處理，或將輸出整合至 Elasticsearch 等全文檢索索引。

對 **ocr scanned pdf python** 有更多疑問或需要協助排除掃描問題？歡迎在下方留言，祝開發順利！

--- 

![how to ocr pdf example](image-placeholder.png){alt="how to ocr pdf example"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}