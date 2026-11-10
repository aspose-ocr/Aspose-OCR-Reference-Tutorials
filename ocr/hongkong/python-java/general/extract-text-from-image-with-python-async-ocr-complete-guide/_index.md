---
category: general
date: 2026-05-03
description: 使用 Python 的非同步 OCR 從圖像提取文字。了解如何將 tif 轉換為文字、載入圖像進行 OCR，以及高效辨識圖像中的文字。
draft: false
keywords:
- extract text from image
- convert tif to text
- load image for ocr
- extract image text
- recognize text from image
language: zh-hant
og_description: 使用 Python 非同步 OCR 從圖像提取文字。本指南展示如何將 tif 轉換為文字、載入圖像進行 OCR，以及辨識圖像中的文字。
og_title: 使用 Python 非同步 OCR 從圖像提取文字 – 完整指南
tags:
- OCR
- Python
- AsyncIO
title: 使用 Python 非同步 OCR 從圖像提取文字 – 完整指南
url: /zh-hant/python-java/general/extract-text-from-image-with-python-async-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Python Async OCR 從圖像提取文字 – 完整指南

需要 **快速從圖像提取文字** 嗎？使用 Python 的 async OCR，只需幾行程式碼即可完成。無論你面對的是巨大的 .tif 掃描檔，還是少量的 JPEG，本教學都會示範如何將 tif 轉換成文字、載入圖像進行 OCR，最後在不阻塞事件迴圈的情況下辨識圖像文字。

事實上，大多數開發者會先選擇同步函式庫，結果 UI 卡住，等引擎處理完像素才恢復。在本指南中，我們將改用 Aspose OCR Cloud 的非同步 API，讓你的應用保持回應。完成後，你將擁有一個可直接執行的腳本，能從任何支援的圖像格式中抽取文字，並了解每一步背後的原理。

## 你將學到

- 如何為 Python 設定 Aspose OCR Cloud SDK。
- **載入圖像進行 OCR** 並啟動非同步辨識任務的完整程式碼。
- 處理大型 .tif 檔案與授權細節的技巧。
- 即使服務回傳錯誤，也能安全 **抽取圖像文字** 的方法。
- 一個完整、可直接複製貼上的範例，讓你立即在專案中使用。

> **先決條件**：Python 3.8+ 與 Aspose OCR Cloud 授權檔 (`Aspose.OCR.Java.lic`)。不需要其他第三方套件。

---

![extract text from image workflow](workflow.png){: .align-center alt="從圖像提取文字工作流程"}

## 從圖像提取文字 – Async OCR 概觀

在深入程式碼之前，先說明整體流程。當你呼叫 `recognize_async` 時，SDK 會將圖像上傳至 Aspose 雲端，啟動背景工作，並回傳一個 `Task` 物件。等待該任務完成後會得到一個 `OcrResult`，其中包含圖像的純文字表示。由於呼叫是非同步的，你可以同時發起多個工作——非常適合批次處理大量掃描文件。

### 為什麼使用 Async？

- **非阻塞 I/O** – 事件迴圈仍可處理其他工作（例如回應 HTTP 請求）。
- **可擴展性** – 同時啟動數十個辨識任務；雲端負責繁重計算。
- **回應速度** – UI 應用程式在等待 OCR 引擎時不會凍結。

了解了「為什麼」之後，接下來說明 **如何**。

## 使用 Aspose OCR 將 TIF 轉換成文字

常見的卡關點是以為每個 OCR 函式庫都原生支援 .tif。Aspose 支援，但仍需提供 `Image` 物件。SDK 會抽象化格式，你只要指向檔案路徑即可。

```python
import asyncio
import asposeocrcloud as ocr

async def async_ocr(image_path: str) -> str:
    """
    Asynchronously extract text from the given image file.
    
    Parameters
    ----------
    image_path: str
        Path to the image (e.g., a .tif, .png, or .jpg file).

    Returns
    -------
    str
        The plain‑text OCR result.
    """
    # 1️⃣ Create the OCR engine and apply the license
    ocr_engine = ocr.OcrEngine()
    # The License class reads the .lic file; adjust the path if needed.
    ocr_engine.license = ocr.License().set_license("Aspose.OCR.Java.lic")

    # 2️⃣ Load the image for OCR – this works for TIF, PNG, JPEG, etc.
    ocr_image = ocr.Image.from_file(image_path)

    # 3️⃣ Start the asynchronous recognition task
    recognition_task = ocr_engine.recognize_async(ocr_image)

    # 4️⃣ Await the task and retrieve the extracted text
    ocr_result = await recognition_task
    return ocr_result.text
```

**關鍵程式碼說明**

- `ocr_engine.license = ...` – 若未提供有效授權，雲端會回傳 403 錯誤。請確保 `.lic` 檔案在腳本工作目錄可被存取。
- `ocr.Image.from_file(image_path)` – 此步驟 **載入圖像進行 OCR**；SDK 會自動偵測格式，無需事先將 .tif 轉換。
- `recognize_async` – 回傳可與 coroutine 配合的 task。若有批次需求，可在 `gather` 呼叫中同時啟動多個。

> **專業提示**：若處理的是 GB 級的 TIFF，建議先將其切分為單頁。Aspose 的 `Image.from_file` 可接受頁碼索引，減少記憶體壓力。

## 非同步辨識圖像文字

以下示範在一般腳本中如何呼叫此函式。`asyncio.run` 是在未處於事件迴圈（例如純 CLI 工具）時，啟動 coroutine 的最簡方式。

```python
if __name__ == "__main__":
    # Replace with the actual path to your large TIF file.
    tif_path = "YOUR_DIRECTORY/large_image.tif"

    # Execute the coroutine and capture the output.
    extracted_text = asyncio.run(async_ocr(tif_path))

    # Print the result – this is the final step of **extracting text from image**.
    print("=== OCR Result ===")
    print(extracted_text)
```

**執行結果說明**

對於清晰的高解析度掃描，腳本通常會回傳多行字串，與印刷頁面內容相符。若圖像雜訊較多，Aspose 仍會嘗試清理，但可能出現亂碼。此時可在送給 OCR 引擎前，先使用 OpenCV 進行前處理（例如二值化）。

### 優雅地處理錯誤

```python
try:
    extracted_text = asyncio.run(async_ocr(tif_path))
except ocr.OcrException as exc:
    print(f"⚠️ OCR failed: {exc}")
    # Fallback: you could retry, log, or switch to a different service.
else:
    print(extracted_text)
```

捕捉 `OcrException` 可避免雲端回傳錯誤時程式崩潰——這是新手常因忽略網路抖動而遇到的問題。

## 載入圖像進行 OCR – 實用技巧

1. **檔案路徑 vs. 位元組** – SDK 接受檔案路徑，也支援從 `bytes` 物件載入（`ocr.Image.from_bytes`），適用於圖像已在記憶體中（例如從 S3 或資料庫取得）。
2. **支援格式** – 除 .tif 外，Aspose 亦支援 PDF、BMP、GIF，甚至多頁 TIFF。直接使用 `Image.from_file("doc.pdf")` 即可 OCR PDF。
3. **效能** – 批次作業時，重複使用同一個 `OcrEngine` 實例；為每個檔案重新建立引擎會增加不必要的開銷。

## 完整可執行範例（一步到位腳本）

以下為完整、可直接執行的腳本，已整合授權、錯誤處理與簡易命令列參數解析。複製貼上、調整授權路徑，即可使用。

```python
# full_async_ocr.py
import asyncio
import argparse
import asposeocrcloud as ocr
import sys
from pathlib import Path

async def async_ocr(image_path: Path) -> str:
    """Extract text from an image file asynchronously."""
    engine = ocr.OcrEngine()
    # Adjust this if your .lic file lives elsewhere
    license_path = Path("Aspose.OCR.Java.lic")
    if not license_path.is_file():
        sys.exit("❌ License file not found. Place Aspose.OCR.Java.lic beside the script.")
    engine.license = ocr.License().set_license(str(license_path))

    # Load the image (supports TIFF, PNG, JPEG, PDF, etc.)
    image = ocr.Image.from_file(str(image_path))

    # Fire off the async recognition
    task = engine.recognize_async(image)

    # Await and return the plain text
    result = await task
    return result.text

def parse_args():
    parser = argparse.ArgumentParser(
        description="Extract text from image using Aspose OCR async API."
    )
    parser.add_argument(
        "image",
        type=Path,
        help="Path to the image file (e.g., .tif, .png, .jpg, .pdf)."
    )
    return parser.parse_args()

def main():
    args = parse_args()
    if not args.image.is_file():
        sys.exit(f"❌ File not found: {args.image}")

    try:
        text = asyncio.run(async_ocr(args.image))
    except ocr.OcrException as e:
        sys.exit(f"⚠️ OCR failed: {e}")

    print("\n=== Extracted Text ===\n")
    print(text)

if __name__ == "__main__":
    main()
```

**預期輸出**

```
=== Extracted Text ===

Lorem ipsum dolor sit amet,
consectetur adipiscing elit.
...
```

若圖像僅包含一段文字，主控台會顯示相同的行並保留換行。對於多頁 TIFF，SDK 會依序串接各頁內容。

## 常見問題 (FAQ)

**Q: 這能在其他 async 框架（例如 FastAPI）中使用嗎？**  
A: 完全可以。只要把 `asyncio.run` 換成在端點內 `await async_ocr(path)`，FastAPI 會自行管理事件迴圈。

**Q: 若一次需要處理上百個檔案，該怎麼做？**  
A: 使用 `asyncio.gather`：

```python
tasks = [async_ocr(p) for p in list_of_paths]
results = await asyncio.gather(*tasks, return_exceptions=True)
```

**Q: 能否從受密碼保護的 PDF 抽取文字？**  
A: 直接不行。必須先解鎖 PDF（例如使用 `pikepdf`），再將解密後的位元組傳給 `ocr.Image.from_bytes`。

**Q: 如何處理非英文語言？**  
A: 在辨識前設定語言：

```python
engine.language = "spa"   # Spanish ISO code
```

Aspose 支援超過 60 種語言，請參考文件取得正確的語言代碼。

## 結論

現在你已擁有一套完整的 **從圖像提取文字** 解決方案，結合 Python 的 `asyncio` 與 Aspose OCR Cloud 的非同步 API。依照上述步驟，你可以 **將 tif 轉換成文字**、**載入圖像進行 OCR**，以及 **非阻塞地辨識圖像文字**——無論是命令列工具或高流量的 Web 服務，都相當適用。

接下來要做什麼？試著批次處理整個資料夾的掃描檔、調整語言設定，或將 OCR 輸出串接至下游的 NLP 流程。未來的可能性無限。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}