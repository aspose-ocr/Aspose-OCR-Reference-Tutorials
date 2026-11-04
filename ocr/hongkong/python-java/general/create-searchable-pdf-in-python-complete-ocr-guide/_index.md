---
category: general
date: 2026-06-22
description: 使用 OCR 在 Python 中建立可搜尋 PDF – 學習如何將影像轉換為 PDF、辨識文字 PDF，並自動化工作流程。
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- ocr image to pdf
- recognize text pdf
- python ocr pdf
language: zh-hant
og_description: 使用 OCR 在 Python 中建立可搜尋的 PDF。跟隨本一步一步教學，將影像轉換為 PDF、辨識文字 PDF，並自動化文件處理。
og_title: 在 Python 中建立可搜尋的 PDF – 完整 OCR 指南
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Create searchable PDF in Python using OCR – learn how to convert image
    to PDF, recognize text PDF, and automate your workflow.
  headline: Create searchable PDF in Python – Complete OCR Guide
  type: TechArticle
- description: Create searchable PDF in Python using OCR – learn how to convert image
    to PDF, recognize text PDF, and automate your workflow.
  name: Create searchable PDF in Python – Complete OCR Guide
  steps:
  - name: Initialise the OCR engine
    text: The first thing you do is spin up an `OcrEngine` object. Think of it as
      turning on a scanner that’s ready to read your image.
  - name: Load the image you want to convert
    text: Next we feed the engine with an image stream. The `ImageStream.from_file`
      helper reads the file and wraps it in a format the OCR engine understands.
  - name: Tell the engine to output a searchable PDF
    text: By default many OCR SDKs output plain text. We need to switch the output
      format to PDF so the resulting file is both visual and searchable.
  - name: Prepare an in‑memory stream for the PDF data
    text: Instead of writing directly to disk, we capture the PDF in a `MemoryStream`.
      This keeps I/O fast and lets you pipe the bytes elsewhere (e.g., upload to S3)
      if you wish.
  - name: Run the recognition and write the PDF
    text: Now the heavy lifting happens. The `recognize` call reads the image, runs
      OCR, and streams the searchable PDF into `pdf_stream`.
  - name: Save the generated PDF to a file
    text: Finally, we dump the bytes from the memory stream onto disk. The resulting
      file can be opened in Adobe Reader, Preview, or any PDF viewer with full‑text
      search.
  type: HowTo
tags:
- OCR
- Python
- PDF
title: 使用 Python 建立可搜尋 PDF – 完整 OCR 指南
url: /zh-hant/python-java/general/create-searchable-pdf-in-python-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Python 中建立可搜尋的 PDF – 完整 OCR 指南

有沒有需要從掃描的合約 **create searchable PDF**，但不知從何開始？你並不孤單——許多開發者在首次嘗試將點陣圖影像轉換為可文字搜尋的文件時，都會碰到相同的障礙。好消息是，只要使用一個小小的 Python 程式碼，你就可以 **convert image to PDF**，讓 OCR 引擎辨識每個字，最終得到一個完美可搜尋的檔案。

在本教學中，我們將逐步說明整個流程，從安裝正確的函式庫到處理多頁文件等邊緣情況。完成後，你將能夠 **ocr image to pdf**、**recognize text pdf**，並將此工作流程整合到更大的自動化管線中。

## 需要的條件

在深入之前，請確保你的機器上已具備以下項目：

| Requirement | Why it matters |
|-------------|----------------|
| Python 3.8 or newer | 現代語法與更好的型別提示 |
| `ocr` Python package (or any compatible OCR SDK) | 提供 `OcrEngine`、`ImageStream` 與 PDF 輸出 |
| A scanned image (JPEG, PNG, or TIFF) | 你要轉換的來源影像 |
| Write access to a folder for the output PDF | 以便儲存產生的檔案 |

如果尚未安裝 SDK，請執行以下指令：

```bash
pip install ocr-sdk   # replace with the actual package name
```

> **專業提示：** 使用虛擬環境 (`python -m venv .venv`) 以保持相依套件整潔。

## 工作流程概覽

1. **Create an OCR engine instance** – 進行辨識的核心引擎。  
2. **Load the image** 你想要處理的影像。  
3. **Configure the engine** 以輸出可搜尋的 PDF 而非純文字。  
4. **Prepare an in‑memory stream** 用於保存 PDF 位元組的記憶體串流。  
5. **Run the recognition** – 引擎讀取影像、提取文字，並寫入 PDF。  
6. **Persist the PDF to disk** 以便於任何檢視器開啟。

以上就是六行程式碼完成的全部流程。接下來讓我們逐步拆解每個步驟。

---

## 建立可搜尋的 PDF – 步驟式 Python OCR 教學

### 步驟 1：初始化 OCR 引擎

首先，你需要建立一個 `OcrEngine` 物件。可以把它想像成開啟一台已準備好讀取影像的掃描器。

```python
import ocr

# Initialise the OCR engine – this is where all the magic begins
engine = ocr.OcrEngine()
```

> **為什麼重要：** 建立引擎實例會分配內部緩衝區並載入語言資料。若跳過此步驟，稍後在設定影像時會出現 `NoneType` 錯誤。

### 步驟 2：載入欲轉換的影像

接著，我們將影像串流提供給引擎。`ImageStream.from_file` 輔助函式會讀取檔案，並將其包裝成 OCR 引擎可理解的格式。

```python
# Load the source image – replace the path with your own file
image_path = "YOUR_DIRECTORY/contract.jpg"
engine.set_image(ocr.ImageStream.from_file(image_path))
```

> **邊緣情況：** 若來源是多頁 TIFF，請改用 `ocr.MultiPageImageStream.from_file`。引擎會自動將每一頁視為獨立的 PDF 頁面。

### 步驟 3：告訴引擎輸出可搜尋的 PDF

預設情況下，許多 OCR SDK 會輸出純文字。我們需要將輸出格式切換為 PDF，讓產生的檔案同時具備視覺呈現與可搜尋性。

```python
# Configure the engine to produce a searchable PDF
engine.get_settings().set_output_format(ocr.OutputFormat.PDF)
```

> **底層運作原理是什麼？** 引擎現在會在點陣圖後方嵌入一層隱形文字層，讓你能像在原生 PDF 中一樣搜尋文字。

### 步驟 4：為 PDF 資料準備記憶體串流

我們不直接寫入磁碟，而是將 PDF 捕獲到 `MemoryStream` 中。這樣可提升 I/O 效能，且若需要也能將位元組傳送至其他地方（例如上傳至 S3）。

```python
# Create a memory buffer that will receive the PDF bytes
pdf_stream = ocr.MemoryStream()
```

### 步驟 5：執行辨識並寫入 PDF

現在開始執行繁重的工作。`recognize` 呼叫會讀取影像、執行 OCR，並將可搜尋的 PDF 串流至 `pdf_stream`。

```python
# Perform OCR and write the searchable PDF into the memory stream
engine.recognize(pdf_stream)
```

> **常見陷阱：** 若忘記呼叫 `engine.recognize`，`pdf_stream` 會是空的，嘗試儲存時會拋出 `ValueError`。若需確認已產生資料，請務必檢查 `pdf_stream.length`。

### 步驟 6：將產生的 PDF 儲存至檔案

最後，我們將記憶體串流中的位元組寫入磁碟。產生的檔案可在 Adobe Reader、Preview 或任何具備全文搜尋功能的 PDF 檢視器中開啟。

```python
output_path = "YOUR_DIRECTORY/contract_searchable.pdf"

# Write the PDF bytes to a file
with open(output_path, "wb") as f:
    f.write(pdf_stream.to_bytes())
print(f"✅ Searchable PDF saved to {output_path}")
```

> **你會看到的結果：** 開啟 PDF，按下 `Ctrl+F`，輸入原始掃描中出現的字詞，即可立即看到檢視器將其標示。這正是 **searchable PDF** 的特徵。

## 轉換影像為 PDF – 調整設定以獲得最佳效果

如果你的主要目標僅是 **convert image to PDF** 而不需要 OCR，你可以跳過第 3 步，將輸出格式設定為 `ocr.OutputFormat.IMAGE_PDF`。引擎會將點陣圖嵌入為 PDF 頁面，且不會有隱形文字層。

```python
engine.get_settings().set_output_format(ocr.OutputFormat.IMAGE_PDF)
```

當你需要忠實的視覺複製品但不在乎可搜尋性時，可使用此模式——例如僅作為存檔用途且不需要 OCR 的情況。

## 辨識文字 PDF – 添加語言套件與 DPI 控制

為了獲得更完善的 **recognize text PDF** 體驗，請考慮以下可選的調整：

```python
settings = engine.get_settings()
settings.set_language("eng+spa")          # English + Spanish support
settings.set_dpi(300)                     # Higher DPI improves accuracy
settings.enable_auto_rotate(True)         # Auto‑rotate skewed scans
```

> **為什麼要調整 DPI？** 較高的解析度提供 OCR 引擎更多像素可供分析，降低低品質掃描的誤辨率。

## Python OCR PDF – 整合至更大型的管線

現在你已能在幾行程式碼內完成 **python ocr pdf**，不妨將此邏輯嵌入 Flask API 中：

```python
from flask import Flask, request, send_file
import io, ocr

app = Flask(__name__)

@app.route("/upload", methods=["POST"])
def upload():
    file = request.files["image"]
    engine = ocr.OcrEngine()
    engine.set_image(ocr.ImageStream.from_bytes(file.read()))
    engine.get_settings().set_output_format(ocr.OutputFormat.PDF)
    pdf_stream = ocr.MemoryStream()
    engine.recognize(pdf_stream)

    return send_file(
        io.BytesIO(pdf_stream.to_bytes()),
        mimetype="application/pdf",
        as_attachment=True,
        download_name="searchable.pdf"
    )
```

這個小型端點允許客戶端 POST 影像並即時取得 **searchable PDF**——非常適合 SaaS 文件處理服務。

## 常見陷阱：當你 **ocr image to pdf** 時

| 症狀 | 可能原因 | 解決方法 |
|------|----------|----------|
| PDF 頁面空白 | 影像未載入（`engine.set_image` 使用錯誤路徑） | 確認路徑，並使用 `os.path.abspath` |
| 無可搜尋文字 | 輸出格式仍為 `IMAGE_PDF` | 明確呼叫 `set_output_format(ocr.OutputFormat.PDF)` |
| 文字亂碼 | 語言套件錯誤 | 使用 `settings.set_language("eng")` 載入正確語言 |
| 大型檔案處理緩慢 | 在高解析度影像上使用預設 DPI (72) | 將 DPI 提升至 300，或將頁面逐一批次處理 |

## 完整、可執行範例（可直接複製貼上）

```python
import ocr

def create_searchable_pdf(image_path: str, output_path: str) -> None:
    """
    Convert a scanned image to a searchable PDF using the ocr SDK.
    """
    # 1️⃣ Initialise engine
    engine = ocr.OcrEngine()

    # 2️⃣ Load image
    engine.set_image(ocr.ImageStream.from_file(image_path))

    # 3️⃣ Set output to searchable PDF
    engine.get_settings().set_output_format(ocr.OutputFormat.PDF)

    # Optional: improve accuracy
    settings = engine.get_settings()
    settings.set_language("eng")   # adjust as needed
    settings.set_dpi(300)

    # 4️⃣ Prepare in‑memory stream
    pdf_stream = ocr.MemoryStream()

    # 5️⃣ Run OCR
    engine.recognize(pdf_stream)

    # 6️⃣ Persist PDF
    with open(output_path, "wb") as f:
        f.write(pdf_stream.to_bytes())
    print(f"✅ Searchable PDF created at: {output_path}")

if __name__ == "__main__":
    create_searchable_pdf(
        image_path="YOUR_DIRECTORY/contract.jpg",
        output_path="YOUR_DIRECTORY/contract_searchable.pdf"
    )
```

執行腳本，開啟產生的 PDF，並搜尋原始掃描中確實出現的字詞。若一切順利，你就已掌握使用 Python **create searchable pdf** 的技巧。

## 結論

我們已說明使用 Python OCR 函式庫建立 **create searchable PDF** 檔案所需的全部步驟：初始化引擎、載入影像、設定 PDF 輸出、串流結果，最後儲存至磁碟。你也看到如何 **convert image to PDF**，以及微調 **

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，並在此基礎上延伸。每個資源皆提供完整可執行的程式碼範例與步驟說明，協助你精通更多 API 功能，並在自己的專案中探索替代實作方式。

- [辨識 PDF 文字 – 使用 Aspose.OCR for Java 的 OCR 操作](/ocr/english/java/ocr-operations/)
- [如何在 .NET 使用 Aspose.OCR 進行 PDF OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [將影像轉換為 PDF C# – 儲存多頁 OCR 結果](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}