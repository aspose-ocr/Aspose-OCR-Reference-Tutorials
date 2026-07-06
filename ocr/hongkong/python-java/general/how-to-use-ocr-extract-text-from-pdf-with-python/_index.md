---
category: general
date: 2026-04-26
description: 如何在掃描 PDF 上使用 OCR、從 PDF 提取文字、對 PDF 執行 OCR，並在幾個步驟內將掃描 PDF 轉換為可搜尋檔案。
draft: false
keywords:
- how to use OCR
- extract text from pdf
- run OCR on pdf
- convert scanned pdf
- load pdf as image
language: zh-hant
og_description: 如何在 Python 中使用 OCR：學習如何從 PDF 提取文字、對 PDF 執行 OCR，並將掃描版 PDF 轉換為可搜尋的文件。
og_title: 如何使用 OCR – 從 PDF 提取文字的快速指南
tags:
- OCR
- Python
- PDF
- Text Extraction
title: 如何使用 OCR – 用 Python 從 PDF 提取文字
url: /zh-hant/python-java/general/how-to-use-ocr-extract-text-from-pdf-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 OCR – 使用 Python 從 PDF 提取文字

有沒有想過 **如何使用 OCR** 從掃描的合約、收據或電子書中抽取文字？你並不孤單。在許多實務專案中，收到的 PDF 只是一張影像，若沒有 OCR，就無法搜尋、索引或分析其內容。

在本教學中，我們將逐步示範一個完整、可執行的範例，說明 **如何使用 OCR**、**從 PDF 抽取文字**，以及為什麼你可能想 **將掃描的 PDF** 轉換成可搜尋的文件。還會介紹 **將 PDF 載入為影像** 的微妙技巧，讓 OCR 引擎能清晰看到每一頁。

> **快速預覽：** 完成後，你將擁有一支腳本，能載入多頁 PDF、對每一頁執行 OCR，並印出辨識出的文字——不需要任何外部服務。

## 需要的環境

- Python 3.9+（任何較新的版本皆可）
- `aocr` 套件（或任何提供 `OcrEngine` 與 `Image.load` 的相容 OCR 函式庫）
- 一個你想處理的掃描 PDF 檔案（例如 `contract.pdf`）
- 适量的記憶體（約 200 MB 內可處理 100 頁的 PDF，通常足夠）

如果尚未安裝 OCR 函式庫，請執行：

```bash
pip install aocr
```

> **小技巧：** 使用虛擬環境來保持相依套件的整潔。

## 步驟 1：將 PDF 載入為影像 – 拼圖的第一塊

在執行任何 OCR 之前，必須先把 PDF 轉成影像。這正是次要關鍵字 **load pdf as image** 發揮作用的地方。

```python
# Step 1: Create an OCR engine instance
ocr_engine = OcrEngine()

# Step 2: Load the PDF file as a multi‑page image
ocr_engine.image = aocr.Image.load("YOUR_DIRECTORY/contract.pdf")
```

*為什麼重要：* `aocr.Image.load` 會在內部將每一頁 PDF 光柵化為位圖，讓 OCR 引擎能夠理解。若直接將原始 PDF 傳入，引擎會拋出錯誤，因為它期待的是像素資料，而非向量資料。

> **注意：** 路徑可以是絕對或相對。請確保檔案可讀取，否則會遇到 `FileNotFoundError`。

## 步驟 2：對 PDF 執行 OCR – 把像素變成字元

現在 PDF 已經是影像，我們終於可以 **對 PDF 執行 OCR**。以下程式碼一次處理所有頁面：

```python
# Step 3: Run OCR on every page of the document
page_results = ocr_engine.process_all_pages()
```

*底層在做什麼？* `process_all_pages` 會遍歷光柵化的頁面，套用 OCR 模型，並回傳每頁的結果物件列表。每個結果都包含辨識出的文字、信心分數，以及（若需要）邊界框資訊。

## 步驟 3：從 PDF 抽取文字 – 把字串拉出來

取得 OCR 結果後，抽取純文字變得非常簡單。我們會遍歷每頁並印出結果，示範次要關鍵字 **extract text from pdf**。

```python
# Step 4: Iterate through the results and output the recognized text
for page_number, page_result in enumerate(page_results, start=1):
    print(f"--- Page {page_number} ---")
    print(page_result.text)
```

**預期輸出**（為簡潔起見已截斷）：

```
--- Page 1 ---
This Agreement is made on the 1st day of January...
--- Page 2 ---
Section 2.1: Definitions...
```

如果你需要將文字合併成單一字串，只要這樣串接即可：

```python
full_text = "\n".join(r.text for r in page_results)
```

現在，你已成功 **從 PDF 抽取文字**，且是透過 OCR 完成的。

## 步驟 4：將掃描的 PDF 轉換 – 讓它可搜尋

許多下游工具（如 Elasticsearch 或 SharePoint）期待的是可搜尋的 PDF，而非純文字檔。你可以將 OCR 輸出嵌回原始 PDF，實際上 **將掃描的 PDF** 轉換成可搜尋的版本。

```python
# Optional: Create a searchable PDF
searchable_pdf_path = "YOUR_DIRECTORY/contract_searchable.pdf"
ocr_engine.save_searchable_pdf(searchable_pdf_path)
print(f"Searchable PDF saved to {searchable_pdf_path}")
```

*為什麼要這麼做？* 可搜尋的 PDF 保留原始版面與影像，同時允許文字選取與索引，對人與機器皆是雙贏。

## 常見陷阱與邊緣案例

### 大於記憶體的多頁 PDF

如果 PDF 有上百頁，一次載入全部可能會耗盡記憶體。`aocr` 函式庫支援延遲載入：

```python
ocr_engine.image = aocr.Image.load("bigfile.pdf", lazy=True)
```

接著逐頁處理：

```python
for page in ocr_engine.image.iter_pages():
    result = ocr_engine.process_page(page)
    print(result.text)
```

### 低品質掃描

模糊或低對比度的掃描會大幅降低 OCR 準確度。將影像送入引擎前，建議先做前處理：

```python
from aocr import preprocess

# Improve contrast and denoise
clean_image = preprocess.enhance(ocr_engine.image, contrast=1.5, denoise=True)
ocr_engine.image = clean_image
```

### 語言支援

預設情況下引擎假設使用英文。若要 **對 PDF 執行 OCR** 並使用其他語言，請設定語言代碼：

```python
ocr_engine.language = "spa"  # Spanish
```

確保已安裝對應的語言模型。

## 完整可執行範例

將所有步驟整合起來，以下是一支可直接存為 `ocr_pdf.py` 並立即執行的腳本：

```python
# ocr_pdf.py
from aocr import OcrEngine, Image, preprocess

def main(pdf_path: str, output_path: str = None):
    # Initialize OCR engine
    ocr_engine = OcrEngine()

    # Load PDF as image (lazy loading for large files)
    ocr_engine.image = Image.load(pdf_path, lazy=False)

    # Optional preprocessing – improves accuracy on noisy scans
    ocr_engine.image = preprocess.enhance(ocr_engine.image, contrast=1.4, denoise=True)

    # Run OCR on all pages
    page_results = ocr_engine.process_all_pages()

    # Print extracted text
    for i, result in enumerate(page_results, start=1):
        print(f"--- Page {i} ---")
        print(result.text)

    # If a searchable PDF is desired
    if output_path:
        ocr_engine.save_searchable_pdf(output_path)
        print(f"Searchable PDF saved to {output_path}")

if __name__ == "__main__":
    import argparse
    parser = argparse.ArgumentParser(description="Extract text from a scanned PDF using OCR.")
    parser.add_argument("pdf", help="Path to the input scanned PDF")
    parser.add_argument("-o", "--output", help="Path to save searchable PDF (optional)")
    args = parser.parse_args()
    main(args.pdf, args.output)
```

執行方式如下：

```bash
python ocr_pdf.py YOUR_DIRECTORY/contract.pdf -o YOUR_DIRECTORY/contract_searchable.pdf
```

執行後，你會在主控台看到文字輸出；若提供 `-o` 參數，則會在原始檔旁產生可搜尋的 PDF。

## 小技巧與最佳實踐

- **批次處理：** 若要一次處理數十份 PDF，將上述邏輯包在迴圈中，並記錄每個檔案的成功或失敗。
- **信心過濾：** 每個 `page_result` 都包含信心指標。對信心低的頁面進行捨棄或標記，以便手動檢查。
- **平行處理：** 若 CPU 有多核心，可考慮使用 `concurrent.futures` 進行平行頁面處理——但要留意記憶體使用量。
- **版本鎖定：** `aocr` API 可能會變動。請在 `requirements.txt` 中鎖定版本（例如 `aocr==2.3.1`），以避免破壞性更新。

## 結論

我們已完整說明 **如何使用 OCR** 來 **從 PDF 抽取文字**、**對 PDF 執行 OCR**、**將 PDF 載入為影像**，甚至 **將掃描的 PDF** 轉換成可搜尋的格式。程式碼已備妥，說明同時涵蓋 *什麼* 與 *為什麼*，讓你在任何處理影像型 PDF 的專案中，都能套用這套可重用的模式。

接下來可以嘗試把抽出的文字送入自然語言處理管線，或使用 Elasticsearch 索引可搜尋的 PDF，亦或實驗不同的 OCR 後端（如 Tesseract 或 Azure Computer Vision）。只要有想法，工具就在你手邊。

祝編程愉快，願你的 PDF 永遠可搜尋！

![how to use OCR example](/images/ocr_workflow.png "how to use OCR")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}