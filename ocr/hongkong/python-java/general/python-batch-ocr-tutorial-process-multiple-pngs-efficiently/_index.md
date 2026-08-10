---
category: general
date: 2026-06-22
description: Python 批次 OCR 教學，示範如何使用 Tesseract 與 pathlib 在 PNG 圖片資料夾上執行多執行緒 OCR。學習在
  Python 中快速批次影像 OCR。
draft: false
keywords:
- python batch ocr tutorial
- multithreaded OCR in Python
- tesseract OCR batch processing
- pathlib image handling
- OCR thread count optimization
language: zh-hant
og_description: Python 批次 OCR 教學會一步步帶領你完成一個完整且可執行的腳本，該腳本使用多執行緒與 Tesseract 處理大量 PNG
  圖片。
og_title: Python 批次 OCR 教學 – 快速多執行緒 PNG 圖像 OCR
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: python batch ocr tutorial showing how to run multithreaded OCR on a
    folder of PNG images using Tesseract and pathlib. Learn fast batch image OCR in
    Python.
  headline: 'python batch ocr tutorial: Process Multiple PNGs Efficiently'
  type: TechArticle
- description: python batch ocr tutorial showing how to run multithreaded OCR on a
    folder of PNG images using Tesseract and pathlib. Learn fast batch image OCR in
    Python.
  name: 'python batch ocr tutorial: Process Multiple PNGs Efficiently'
  steps:
  - name: '**Collects** every PNG with **pathlib image handling**.'
    text: '**Collects** every PNG with **pathlib image handling**.'
  - name: '**Spins up** a **multithreaded OCR in Python** worker pool.'
    text: '**Spins up** a **multithreaded OCR in Python** worker pool.'
  - name: '**Optimizes** the number of threads for your hardware (**OCR thread count
      optimization**).'
    text: '**Optimizes** the number of threads for your hardware (**OCR thread count
      optimization**).'
  - name: '**Writes** each result to a dedicated folder (**tesseract OCR batch processing**).'
    text: '**Writes** each result to a dedicated folder (**tesseract OCR batch processing**).'
  type: HowTo
tags:
- OCR
- Python
- Batch Processing
title: Python 批次 OCR 教學：高效處理多個 PNG 圖片
url: /zh-hant/python-java/general/python-batch-ocr-tutorial-process-multiple-pngs-efficiently/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# python batch ocr tutorial – 快速多執行緒 PNG 圖像 OCR

有沒有想過如何 **python batch ocr tutorial** 在數百張 PNG 截圖中快速完成 OCR，而不讓 CPU 發熱過度？你並不是唯一有此需求的人。無論是數位化掃描表單、從收據中提取文字，或是建立可搜尋的檔案庫，穩定的批次 OCR 流程都能為你節省大量時間。

在本指南中，我們將建立一個小而強大的腳本，收集資料夾中所有 `*.png` 檔案，透過多執行緒處理器將它們交給 Tesseract，並將純文字結果寫入整齊的輸出目錄。無需神祕的函式庫——只需 `pathlib`、`concurrent.futures` 與永遠可靠的 `pytesseract`。完成後，你將擁有一個可以直接複製貼上的 **python batch ocr tutorial**，可用於任何專案。

## 你將學到什麼

- 如何使用 **pathlib image handling** 收集影像檔案  
- 設定 **multithreaded OCR in Python** 工作池  
- 為你的 CPU 核心調整 **OCR thread count optimization**  
- 以清晰的命名規則儲存每個結果，方便之後搜尋  
- 以單一、獨立的腳本執行整個流程  

## 前置條件（先備需求）

| 需求 | 為何重要 |
|------|----------|
| Python 3.9+ | 現代語法（`pathlib`、f‑strings） |
| Tesseract 5.x installed and accessible in `PATH` | `pytesseract` 背後的 OCR 引擎 |
| `pytesseract` (`pip install pytesseract`) | Tesseract 的 Python 包裝器 |
| `Pillow` (`pip install pillow`) | 為 Tesseract 載入影像 |
| A folder of PNG files you want to process | 我們的 **tesseract OCR batch processing** 目標 |

> **Pro tip:** 如果你使用 Windows，請將 `C:\Program Files\Tesseract-OCR` 加入系統 `PATH`，讓 `pytesseract` 能自動找到可執行檔。

---

## 步驟 1 – 收集所有 PNG 圖像（使用 pathlib）

首先，我們需要列出所有要執行 OCR 的影像。`pathlib` 只需一行程式碼即可完成，且能跨作業系統使用。

```python
import pathlib

# Adjust the path to point at your source folder
source_dir = pathlib.Path("YOUR_DIRECTORY/batch_images")
image_files = list(source_dir.glob("*.png"))

print(f"Found {len(image_files)} PNG files to process.")
```

*Why `pathlib`?* 它抽象化了 Windows 的反斜線與 Unix 的斜線差異，讓同一腳本能在任何平台執行。這是本教學中 **pathlib image handling** 的基石。

---

## 步驟 2 – 定義簡易的批次 OCR 處理器類別

以下是一個輕量級的封裝，隱藏了執行緒的樣板程式碼。它與先前看到的偽代碼相同，但已具備完整功能。

```python
import concurrent.futures
import pytesseract
from PIL import Image
import os

class BatchOcrProcessor:
    """Encapsulates multithreaded OCR logic."""

    def __init__(self):
        self.thread_count = os.cpu_count() or 4  # sensible default
        self.output_folder = pathlib.Path("ocr_results")
        self.output_folder.mkdir(parents=True, exist_ok=True)

    def set_thread_count(self, count: int):
        """Adjust the number of worker threads (OCR thread count optimization)."""
        if count < 1:
            raise ValueError("Thread count must be at least 1")
        self.thread_count = count
        print(f"Thread pool size set to {self.thread_count}")

    def set_output_folder(self, folder: str):
        """Where each OCR result will be saved (tesseract OCR batch processing)."""
        self.output_folder = pathlib.Path(folder)
        self.output_folder.mkdir(parents=True, exist_ok=True)
        print(f"Output folder set to {self.output_folder}")

    def _process_single(self, image_path: pathlib.Path):
        """Run OCR on a single image and write the text file."""
        try:
            img = Image.open(image_path)
            text = pytesseract.image_to_string(img)
            out_file = self.output_folder / f"{image_path.stem}.txt"
            out_file.write_text(text, encoding="utf-8")
            return f"✅ {image_path.name} → {out_file.name}"
        except Exception as exc:
            return f"❌ {image_path.name} failed: {exc}"

    def process(self, image_paths):
        """Run OCR on the entire batch using a thread pool."""
        print("🚀 Starting batch OCR...")
        with concurrent.futures.ThreadPoolExecutor(max_workers=self.thread_count) as executor:
            results = list(executor.map(self._process_single, image_paths))
        for line in results:
            print(line)
        print("🏁 Batch OCR completed.")
```

**關鍵選擇說明**

- **ThreadPoolExecutor** 為我們提供真正的多執行緒，適用於 I/O 密集的工作，如讀取檔案與呼叫外部的 Tesseract 執行檔。  
- `set_thread_count` 方法讓你可以嘗試 **OCR thread count optimization**；增加執行緒通常能提升吞吐量，直到 CPU 核心飽和為止。  
- 每張影像會產生一個以原始 PNG 名稱命名的 `.txt` 檔案——非常適合之後的索引或搜尋。

---

## 步驟 3 – 把所有元件串接起來

現在我們建立處理器實例，調整執行緒數量，指定輸出資料夾，最後將影像清單交給它。

```python
if __name__ == "__main__":
    # 1️⃣ Gather PNGs (already done above)
    # 2️⃣ Create processor instance
    ocr_processor = BatchOcrProcessor()

    # 3️⃣ Configure thread pool – feel free to change 8 → your core count
    ocr_processor.set_thread_count(8)   # multithreaded OCR in Python

    # 4️⃣ Choose where results land
    ocr_processor.set_output_folder("YOUR_DIRECTORY/ocr_results")

    # 5️⃣ Run the batch – this call blocks until everything is done
    ocr_processor.process(image_files)

    # 6️⃣ All done – a friendly console message
    print("✅ All images processed. Check the ocr_results folder.")
```

執行腳本後會產生類似以下的輸出：

```
Found 42 PNG files to process.
Thread pool size set to 8
Output folder set to YOUR_DIRECTORY/ocr_results
🚀 Starting batch OCR...
✅ invoice_001.png → invoice_001.txt
✅ receipt_2023-04-15.png → receipt_2023-04-15.txt
...
🏁 Batch OCR completed.
✅ All images processed. Check the ocr_results folder.
```

每個 `.txt` 檔案都包含原始的 OCR 輸出。打開任意檔案，即可看到已提取的文字，可供索引、情感分析或其他後續處理使用。

---

## 步驟 4 – 常見問題與避免方法

| 症狀 | 可能原因 | 解決方法 |
|------|----------|----------|
| 空的 `.txt` 檔案 | Tesseract 找不到語言資料或影像過暗 | 安裝語言套件（`tesseract-ocr-eng`）並預處理影像（提升對比度）。 |
| `UnicodeDecodeError` 讀取結果時發生 | 輸出包含非 UTF‑8 字元 | 以 `encoding="utf-8"` 寫入檔案（程式已如此設定），或使用 `errors="ignore"` 作為快速解決方案。 |
| CPU 急升，卻未提升速度 | 執行緒數量超過實體核心 | 將 `set_thread_count` 降至 `os.cpu_count()` 或更低。 |
| 開啟影像時出現 `FileNotFoundError` | 路徑在 Windows 上含有非 ASCII 字元 | 在字串前加上 `r` 前綴，或直接使用 `pathlib` 物件（如本範例）。 |

---

## 步驟 5 – 延伸教學（後續步驟）

- **Add image preprocessing** 使用 OpenCV（`cv2`）以提升 OCR 準確度（例如去斜、二值化）。  
- **Parallelize across machines** 使用 `multiprocessing` 或簡易任務佇列如 RabbitMQ，將工作分散至多台機器以處理大規模工作負載。  
- **Integrate with a search engine**（Elasticsearch）讓提取的文字即時可搜尋。  
- **Swap Tesseract for a cloud OCR API**（Google Vision、Azure Computer Vision），若需更高的手寫文字辨識精度。

所有這些想法皆建立在你目前擁有的基礎上：一個乾淨、即插即用的 **python batch ocr tutorial**。

---

## 結論

你剛剛完成了一個完整的 **python batch ocr tutorial**，它：

1. **Collects** 每個 PNG，使用 **pathlib image handling**。  
2. **Spins up** 一個 **multithreaded OCR in Python** 工作池。  
3. **Optimizes** 依硬體調整執行緒數量（**OCR thread count optimization**）。  
4. **Writes** 每個結果至專屬資料夾（**tesseract OCR batch processing**）。

此腳本可直接嵌入任何工作流程，無論是處理收據、法律文件，或是大量截圖。你可以調整執行緒數量、加入影像前處理，或將輸出連接至資料庫——隨你決定。

有任何問題嗎？歡迎在下方留言，祝編程愉快！

![python batch ocr tutorial 並行處理多個 PNG 檔案的工作流程圖](/images/python-batch-ocr-workflow.png){.center width=600 alt="python batch ocr tutorial 工作流程"}

---

## 接下來該學什麼？

以下教學涵蓋與本指南密切相關的主題，建立在此處示範的技巧之上。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你掌握更多 API 功能，並在自己的專案中探索替代實作方式。

- [Aspose OCR Tutorial – Optical Character Recognition](/ocr/english/)
- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}