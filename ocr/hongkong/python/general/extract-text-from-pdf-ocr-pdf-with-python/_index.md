---
category: general
date: 2026-04-29
description: 使用 Aspose OCR 於 Python 從 PDF 提取文字。了解批次 OCR PDF 處理、將掃描 PDF 轉換為文字，並處理低可信度頁面。
draft: false
keywords:
- extract text from pdf
- ocr pdf with python
- convert scanned pdf text
- batch ocr pdf processing
language: zh-hant
og_description: 使用 Aspose OCR 於 Python 從 PDF 提取文字。本指南示範批次 OCR PDF 處理、將掃描 PDF 轉換為文字，以及處理低信心結果。
og_title: 從 PDF 提取文字 – 使用 Python 進行 PDF OCR
tags:
- OCR
- Python
- PDF processing
title: 從 PDF 提取文字 – 使用 Python 進行 OCR
url: /zh-hant/python/general/extract-text-from-pdf-ocr-pdf-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從 PDF 提取文字 – 使用 Python 進行 OCR PDF

有沒有曾經需要 **從 PDF 提取文字**，但檔案只是掃描圖像？你並不孤單——許多開發者在嘗試將 PDF 轉換成可搜尋的資料時都會碰到這個問題。好消息是？使用 Aspose OCR for Python，你可以用幾行程式碼將掃描的 PDF 文字轉換，甚至在有數十個檔案需要處理時執行 **批次 OCR PDF 處理**。

在本教學中，我們將逐步說明完整工作流程：設定函式庫、在單一 PDF 上執行 OCR、擴展為批次處理，以及處理低信心分頁讓你知道何時需要人工檢查。完成後，你將擁有一個可直接執行的腳本，能從任何掃描 PDF 中提取文字，並了解每一步背後的原因。

## 您需要的條件

在開始之前，請確保你已具備：

- Python 3.8 或更新版本（程式碼使用 f‑strings，所以 3.6+ 也可運作，但建議使用 3.8+）
- Aspose OCR for Python 授權或免費試用金鑰（可從 Aspose 官方網站取得）
- 一個包含一個或多個欲處理掃描 PDF 的資料夾
- 足夠的磁碟空間以存放產生的 *.txt* 報告

就這樣——不需要繁重的外部相依套件，也不需要 OpenCV 的複雜操作。Aspose OCR 引擎會為你完成繁重的工作。

## 設定環境

首先，從 PyPI 安裝 Aspose OCR 套件：

```bash
pip install aspose-ocr
```

如果你有授權檔案 (`Aspose.OCR.lic`)，請將它放在專案根目錄，並依以下方式啟用：

```python
# Activate Aspose OCR license (optional but removes trial watermark)
from aspose.ocr import License

license = License()
license.set_license("Aspose.OCR.lic")
```

> **專業提示：** 請將授權檔案排除於版本控制之外；將其加入 `.gitignore` 以避免意外外洩。

## 在單一 PDF 上執行 OCR

現在讓我們從單一掃描 PDF 中提取文字。核心步驟如下：

1. 建立一個 `OcrEngine` 實例。
2. 指向 PDF 檔案。
3. 為每一頁取得 `OcrResult`。
4. 將純文字輸出寫入磁碟。
5. 釋放引擎以釋放原生資源。

以下是完整、可執行的腳本：

```python
# Step 1: Import the OCR engine and create an instance
from aspose.ocr import OcrEngine

# Optional: activate license (see previous section)
# from aspose.ocr import License
# License().set_license("Aspose.OCR.lic")

ocr_engine = OcrEngine()

# Step 2: Specify the PDF file to be processed
pdf_file_path = r"YOUR_DIRECTORY/input.pdf"

# Step 3: Extract OCR results – one OcrResult object per page
ocr_pages = ocr_engine.extract_from_pdf(pdf_file_path)

# Step 4: Iterate through the results, show confidence, flag low‑confidence pages, and save the plain text
for ocr_page in ocr_pages:
    print(f"Page {ocr_page.page_number}: confidence {ocr_page.confidence:.2%}")

    # If confidence is below 80 %, flag it for manual review
    if ocr_page.confidence < 0.80:
        print("  Low confidence – consider manual review")

    # Build the output filename
    output_txt = f"YOUR_DIRECTORY/Report_page{ocr_page.page_number}.txt"
    with open(output_txt, "w", encoding="utf-8") as f:
        f.write(ocr_page.text)

# Step 5: Release resources used by the engine
ocr_engine.dispose()
```

**你會看到的結果：** 每一頁腳本會印出類似 `Page 1: confidence 97.45%` 的訊息。若某頁的信心分數低於 80 % 閾值，會顯示警告，提醒你 OCR 可能遺漏了字元。

### 為什麼這樣可行

- **`OcrEngine`** 是連接原生 Aspose OCR 函式庫的入口；它負責從影像前處理到字元辨識的全部工作。
- **`extract_from_pdf`** 會自動將每頁 PDF 光柵化，因此你不必自行將 PDF 轉成影像。
- **信心分數** 讓你能自動化品質檢查——在處理法律或醫療文件等對準確度要求極高的情境時尤為重要。

## 使用 Python 進行批次 OCR PDF 處理

大多數實務專案會處理多於一個檔案。讓我們將單檔腳本擴充為 **批次 OCR PDF 處理** 管線，遍歷目錄、處理每個 PDF，並將結果存入相對應的子資料夾。

```python
import os
from pathlib import Path
from aspose.ocr import OcrEngine

def ocr_pdf_file(pdf_path: Path, output_dir: Path, engine: OcrEngine, confidence_threshold: float = 0.80):
    """Extract text from a single PDF and write per‑page .txt files."""
    ocr_pages = engine.extract_from_pdf(str(pdf_path))
    for page in ocr_pages:
        print(f"{pdf_path.name} – Page {page.page_number}: {page.confidence:.2%}")
        if page.confidence < confidence_threshold:
            print("  ⚠️ Low confidence – manual review may be needed")

        out_file = output_dir / f"{pdf_path.stem}_page{page.page_number}.txt"
        out_file.write_text(page.text, encoding="utf-8")

def batch_ocr_pdf(input_folder: str, output_folder: str):
    """Iterate over all PDFs in input_folder and run OCR."""
    engine = OcrEngine()
    input_path = Path(input_folder)
    output_path = Path(output_folder)
    output_path.mkdir(parents=True, exist_ok=True)

    pdf_files = list(input_path.glob("*.pdf"))
    if not pdf_files:
        print("🚫 No PDF files found in the specified folder.")
        return

    for pdf_file in pdf_files:
        # Create a sub‑folder for each PDF to keep pages organized
        pdf_out_dir = output_path / pdf_file.stem
        pdf_out_dir.mkdir(exist_ok=True)
        ocr_pdf_file(pdf_file, pdf_out_dir, engine)

    # Clean up native resources
    engine.dispose()
    print("✅ Batch OCR completed.")

# Example usage:
if __name__ == "__main__":
    batch_ocr_pdf("YOUR_DIRECTORY/input_pdfs", "YOUR_DIRECTORY/ocr_output")
```

#### 此方式的好處

- **可擴充性：** 此函式一次走訪資料夾，為每個 PDF 建立專屬的輸出子資料夾。當文件數量達到數十甚至上百時，能保持結構整潔。
- **可重用性：** `ocr_pdf_file` 可被其他腳本（例如 Web 服務）呼叫，因為它是一個純函式。
- **錯誤處理：** 若輸入資料夾為空，腳本會印出友善訊息，避免靜默失敗。

## 轉換掃描 PDF 文字 – 處理邊緣情況

雖然上述程式碼能處理大多數 PDF，但你可能會遇到以下幾種特殊情況：

| 情況 | 發生原因 | 緩解方式 |
|-----------|----------------|-----------------|
| **加密的 PDF** | PDF 受密碼保護。 | 將密碼傳遞給 `extract_from_pdf(pdf_path, password="yourPwd")`。 |
| **多語言文件** | Aspose OCR 預設為英文。 | 設定 `ocr_engine.language = "spa"` 以使用西班牙文，或提供語言清單以處理混合語言。 |
| **非常大的 PDF（>500 頁）** | 因為每頁都載入至記憶體，導致記憶體使用量激增。 | 使用 `engine.extract_from_pdf(pdf_path, start_page=1, end_page=100)` 分段處理 PDF，並在迴圈中執行。 |
| **掃描品質差** | 低 DPI 或大量噪點會降低信心分數。 | 使用 `engine.image_preprocessing = True` 進行前處理，或透過 `engine.dpi = 300` 提高 DPI。 |

> **注意：** 開啟影像前處理會顯著增加 CPU 耗時。如果你在執行夜間批次，請安排足夠時間或啟動獨立的工作者。

## 驗證輸出結果

腳本執行完畢後，你會看到類似以下的資料夾結構：

```
ocr_output/
├─ invoice_2023/
│  ├─ invoice_2023_page1.txt
│  ├─ invoice_2023_page2.txt
│  └─ …
└─ contract_A/
   ├─ contract_A_page1.txt
   └─ …
```

打開任一 `.txt` 檔案，你應該會看到乾淨的 UTF‑8 編碼文字，與原始掃描內容相符。若出現亂碼，請再次確認 PDF 的語言設定，並確保機器已安裝正確的字型套件。

## 清理資源

Aspose OCR 依賴原生 DLL，完成工作後務必呼叫 `engine.dispose()`。遺忘此步驟會導致記憶體泄漏，尤其在長時間執行的批次作業中更為嚴重。

```python
# Always the last line of your script
engine.dispose()
```

## 完整端對端範例

將所有步驟整合起來，以下是一個單一

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}