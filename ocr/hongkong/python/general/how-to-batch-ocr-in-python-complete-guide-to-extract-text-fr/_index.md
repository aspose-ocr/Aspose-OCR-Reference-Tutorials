---
category: general
date: 2026-06-28
description: 如何在 Python 中批量執行 OCR——從圖像提取文字，並使用批量 OCR 處理將掃描頁面轉換為文字。
draft: false
keywords:
- how to batch OCR
- extract text from images
- convert scanned pages to text
- batch OCR processing
language: zh-hant
og_description: 學習如何在 Python 中批次進行 OCR、從圖片提取文字，並透過高效的批次 OCR 處理將掃描頁面轉換為文字。
og_title: 如何在 Python 中批次 OCR – 一步一步指南
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: How to batch OCR in Python—extract text from images and convert scanned
    pages to text using batch OCR processing.
  headline: How to Batch OCR in Python – Complete Guide to Extract Text from Images
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: 如何在 Python 中批量執行 OCR – 完整指南：從圖像提取文字
url: /zh-hant/python/general/how-to-batch-ocr-in-python-complete-guide-to-extract-text-fr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中批量 OCR – 從圖像提取文字的完整指南

如果你在想 **如何在 Python 中批量 OCR**，恭喜你來對地方了。本教學會示範一個快速方法，讓你 **從圖像提取文字** 並 **將掃描頁面轉換成文字**，只需使用單一 OCR 引擎實例。再也不需要一個檔案接著一個檔案手動複製貼上——讓程式碼幫你完成繁重的工作。

我們會一步步說明所有必備內容：安裝函式庫、載入整個資料夾的掃描檔、執行批次 OCR 處理，以及優雅地處理結果。完成後，你將擁有一支可重複使用的腳本，能在數秒內把一堆 PNG 或 JPEG 轉成可搜尋的文字檔。

## 你需要的條件

在開始之前，請確保你已具備：

* 已安裝 Python 3.9+（程式碼在 3.8 也能執行，但 3.9+ 提供最新的型別提示功能）。
* 現代的 OCR 函式庫——此處我們使用 **Aspose.OCR for Python via .NET**，它會公開原始片段中使用的 `OcrEngine` 類別。  
  ```bash
  pip install aspose-ocr
  ```
* 一個放有掃描頁面的資料夾（`page1.png`、`page2.png` …）。只要 Pillow 能開啟的格式都行，PDF、TIFF 或 BMP 也沒問題。
* 一點好奇心——如果你從未自動化過「圖像轉文字」，現在就能體會批次 OCR 為何是顛覆性的利器。

> **小技巧：** 若你偏好純 Python 函式庫，只要把 `OcrEngine` 換成 `pytesseract.image_to_string` 即可。其餘邏輯保持不變。

## 如何在 Python 中批量 OCR – 步驟說明

以下是完整、可直接執行的腳本。每一行都有註解，讓你了解 *為什麼* 需要這段程式碼，而不只是 *它做了什麼*。

```python
# batch_ocr.py
import os
from aspose.ocr import OcrEngine, Image  # Aspose OCR library
from typing import List

def load_images(folder: str) -> List[Image]:
    """
    Scan a directory and return a list of Aspose.Image objects.
    Supports PNG, JPEG, BMP, and TIFF out of the box.
    """
    supported_ext = {".png", ".jpg", ".jpeg", ".bmp", ".tif", ".tiff"}
    images = []
    for filename in sorted(os.listdir(folder)):
        _, ext = os.path.splitext(filename)
        if ext.lower() in supported_ext:
            path = os.path.join(folder, filename)
            try:
                img = Image.from_file(path)
                images.append(img)
            except Exception as e:
                print(f"⚠️  Could not load {filename}: {e}")
    return images

def batch_ocr_process(images: List[Image]) -> List[str]:
    """
    Perform OCR on the whole batch at once.
    Returns a list of recognized strings, one per image.
    """
    engine = OcrEngine()          # Step 1: create an OCR engine instance
    # The recognize_batch method is optimized for bulk work.
    return engine.recognize_batch(images)

def save_results(texts: List[str], output_folder: str):
    """
    Write each page's text to a separate .txt file.
    """
    os.makedirs(output_folder, exist_ok=True)
    for idx, page_text in enumerate(texts, start=1):
        out_path = os.path.join(output_folder, f"page_{idx}.txt")
        with open(out_path, "w", encoding="utf-8") as f:
            f.write(page_text)
        print(f"✅  Saved page {idx} → {out_path}")

def main():
    # -----------------------------------------------------------------
    # 1️⃣ Load the images you want to process
    # -----------------------------------------------------------------
    image_folder = "YOUR_DIRECTORY"          # <-- replace with your path
    images = load_images(image_folder)

    if not images:
        print("❌  No supported images found. Exiting.")
        return

    # -----------------------------------------------------------------
    # 2️⃣ Perform OCR on the whole batch at once
    # -----------------------------------------------------------------
    print(f"🔎  Running batch OCR on {len(images)} images...")
    page_texts = batch_ocr_process(images)

    # -----------------------------------------------------------------
    # 3️⃣ Output the recognized text for each page
    # -----------------------------------------------------------------
    for i, txt in enumerate(page_texts, start=1):
        print(f"\n--- Page {i} ---")
        print(txt[:200] + ("…" if len(txt) > 200 else ""))  # preview first 200 chars

    # -----------------------------------------------------------------
    # 4️⃣ (Optional) Save each page's text to a file
    # -----------------------------------------------------------------
    save_results(page_texts, "ocr_output")

if __name__ == "__main__":
    main()
```

### 預期輸出

對含有三個 PNG 掃描檔的資料夾執行腳本，會產生類似以下的結果：

```
🔎  Running batch OCR on 3 images...

--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit…

--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore…

--- Page 3 ---
Ut enim ad minim veniam, quis nostrud exercitation ullamco…
✅  Saved page 1 → ocr_output/page_1.txt
✅  Saved page 2 → ocr_output/page_2.txt
✅  Saved page 3 → ocr_output/page_3.txt
```

預覽會顯示每頁的前 200 個字元，完整文字則儲存在 `ocr_output` 目錄下。

## 使用單一引擎提取圖像文字

為什麼只 **建立一個** `OcrEngine` 並重複使用？建立引擎的成本相當高，因為它需要載入語言套件與原生 DLL。共享同一個實例於批次作業時，你可以：

* **節省記憶體** – 只會在 RAM 中保留一套資源。
* **提升速度** – 引擎保持熱態，避免重複初始化。
* **維持一致性** – 相同的辨識設定會套用到每一頁，這對於 **從圖像提取文字**、且版面相同的情況尤為重要。

如果需要調整辨識設定（例如開啟拼寫檢查或變更語言），請在呼叫 `recognize_batch` 之前完成。之後的所有頁面都會自動繼承這些設定。

## 高效將掃描頁面轉換成文字

解決 **將掃描頁面轉換成文字** 的核心在於 `engine.recognize_batch(images)`。函式庫會在背景執行緒池中逐一處理每張圖像，讓多核心機器幾乎呈線性擴充。需要留意的要點包括：

* **圖像品質很重要** – 300 dpi 以上可獲得最佳結果。若掃描檔解析度過低，可先用 Pillow 進行升頻再送入引擎。
* **彩色 vs. 灰階** – OCR 引擎通常在 8 位元灰階圖像上較快。你可以加入前置處理步驟：  
  ```python
  img = Image.from_file(path).convert_to_grayscale()
  ```
* **語言支援** – Aspose.OCR 支援超過 40 種語言。若非英文，請在批次呼叫前設定 `engine.language = "eng"` 或 `"fra"` 等對應語言代碼。

## 批次 OCR 處理最佳實踐

雖然上述程式碼已相當簡潔，實務上大量批次 OCR 常需要額外的安全措施：

| Concern | Recommended Approach |
|---------|----------------------|
| **Large batches ( > 500 files )** | Split into chunks of 100–200 images to keep memory footprints modest. |
| **Corrupt or unsupported files** | The `load_images` helper already catches exceptions and logs a warning; you can also write a fallback to skip or move bad files. |
| **Progress monitoring** | Wrap `recognize_batch` in a loop that yields after each image if the library exposes per‑image callbacks. |
| **Post‑processing** | Run a spell‑check or regex cleanup on the resulting strings to improve downstream searchability. |
| **Parallelism** | If you have a multi‑node setup, distribute folders across workers and merge the `.txt` outputs at the end. |

這些技巧可協助你將 **批次 OCR 處理** 從少量頁面擴展至上千頁，而不會讓腳本當機。

## 常見問題

**Q: 可以直接對 PDF 使用嗎？**  
A: 絕對可以。先將每一頁 PDF 轉成圖像（例如使用 `pdf2image`），再把產生的圖像清單傳給 `recognize_batch`。其餘流程保持不變。

## 接下來該學什麼？

以下教學與本指南緊密相關，能進一步深化你對 API 功能的掌握，並探索在實務專案中的其他實作方式：

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [How to Extract Text from ZIP Archives Using Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}