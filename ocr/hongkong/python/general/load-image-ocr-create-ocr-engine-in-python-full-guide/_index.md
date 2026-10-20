---
category: general
date: 2026-01-12
description: 使用 Python 快速載入圖像 OCR。學習如何建立 OCR 引擎、處理錯誤，以及在一步一步的教學中提取文字。
draft: false
keywords:
- load image OCR
- create OCR engine
- OCR error handling
- Python OCR tutorial
- image preprocessing OCR
language: zh-hant
og_description: 使用簡易 OCR 引擎在 Python 中載入圖像 OCR。本指南展示錯誤處理、最佳實踐以及完整程式碼。
og_title: 載入圖像 OCR – 用 Python 建立 OCR 引擎
tags:
- OCR
- Python
- Image Processing
title: 載入圖像 OCR – 使用 Python 建立 OCR 引擎 – 完整指南
url: /zh-hant/python/general/load-image-ocr-create-ocr-engine-in-python-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 載入影像 OCR – 在 Python 中建立 OCR 引擎

有沒有曾經需要 **載入影像 OCR**，卻不知從何開始？也許你嘗試過某個函式庫，卻收到難以理解的例外，心想「接下來怎麼辦？」你並不孤單。在本教學中，我們將一步步說明如何從頭建立 OCR 引擎、安全載入影像，並處理檔案遺失或損毀時不可避免的錯誤。

完成本指南後，你將擁有一個完整可執行的腳本，能 **建立 OCR 引擎**、載入影像、檢查錯誤，甚至輸出擷取的文字。沒有模糊的外部文件參考——只是一個完整、可直接執行的範例，今天就能放入你的專案中使用。

## 需要的環境

- Python 3.9 或更新版本（我們使用的語法在 3.x 版本中皆為標準）  
- 假設的 `ocr` 套件（使用 `pip install ocr‑lib` 安裝——請改為你實際使用的函式庫）  
- 一個資料夾，內含幾張測試影像（其中一張存在，另一張刻意缺少）  

就這樣。沒有繁重的相依套件，也沒有複雜的建置步驟。讓我們開始吧。

## 步驟 1：建立 OCR 引擎 – 設定核心物件

在你能 **載入影像 OCR** 之前，需要先建立一個能與底層 OCR 引擎溝通的引擎實例。可以把它想像成電視的遙控器；沒有它就無法換頻道。

```python
# step_1_create_engine.py
import ocr

def init_engine():
    """
    Initializes and returns an OCR engine instance.
    This is where we 'create OCR engine' for the rest of the tutorial.
    """
    try:
        engine = ocr.OcrEngine()
        print("✅ OCR engine created successfully.")
        return engine
    except ocr.OcrException as e:
        # If the library itself fails to initialise, we bail out early.
        print(f"❌ Failed to create OCR engine (code {e.code}): {e.message}")
        raise
```

**為什麼這很重要：**  
只建立一次引擎並重複使用，可避免在每張影像上載入原生函式庫的額外開銷。它同時將設定（語言套件、DPI 參數等）集中管理，讓你只需在一處調整即可。

## 步驟 2：載入影像 OCR – 使用例外處理的安全載入

現在已有引擎，接下來的合理步驟就是提供影像給它。最簡單的方式是呼叫 `engine.load_image(path)`。然而，實務程式碼必須預測檔案遺失、不支援的格式或權限問題。

```python
# step_2_load_with_exception.py
def load_image_with_exception(engine, path):
    """
    Attempts to load an image using a try/except block.
    Demonstrates the classic 'load image OCR' pattern with Python exceptions.
    """
    try:
        engine.load_image(path)
        print(f"✅ Image loaded: {path}")
    except ocr.OcrException as ex:
        # The OCR library packages its own error codes.
        print(f"❌ Failed to load image (code {ex.code}): {ex.message}")
        # Optionally re‑raise or handle gracefully.
```

**專業提示：**  
如果你預期會處理大量影像，請將呼叫包在迴圈中，並將失敗紀錄寫入 CSV 以供日後分析。即使單一檔案出錯，也能保持整個流程的穩定性。

## 步驟 3：載入影像 OCR – 使用引擎內建的錯誤 API

某些 OCR 函式庫提供非例外式的錯誤取得方法。當你想在緊密迴圈中避免 Python 例外帶來的效能損耗時，這非常有用。

```python
# step_3_load_with_error_api.py
def load_image_with_error_api(engine, path):
    """
    Loads an image and then checks the engine's internal error state.
    This pattern complements the exception approach and shows another way
    to 'load image OCR' safely.
    """
    engine.load_image(path)           # No try/except here.
    load_error = engine.get_last_error()
    if load_error:
        print(f"❌ Load error: {load_error.message} (code {load_error.code})")
    else:
        print(f"✅ Image loaded without error: {path}")
```

**何時適合使用此方式：**  
如果你每分鐘要處理上千張影像，避免例外可以省下寶貴的毫秒。錯誤 API 讓你在每次呼叫後進行輕量的狀態檢查。

## 步驟 4：擷取文字 – 你來此的真正目的

載入影像只是故事的一半。成功載入後，你通常會想取得 OCR 文字。以下是一個簡潔的輔助函式，負責擷取文字並印出。

```python
# step_4_extract_text.py
def extract_text(engine):
    """
    Retrieves OCR results from the previously loaded image.
    Returns a string; empty string indicates no text found.
    """
    try:
        result = engine.recognize()
        text = result.text
        if text:
            print("📝 Extracted Text:")
            print(text)
        else:
            print("⚠️ No text detected in the image.")
        return text
    except ocr.OcrException as e:
        print(f"❌ OCR failed (code {e.code}): {e.message}")
        return ""
```

**為什麼它會運作：**  
`engine.recognize()` 是大多數 OCR SDK 的標準呼叫。它會回傳一個結果物件，包含原始字串、信心分數與邊界框。本教學中我們保持簡單，只顯示純文字。

## 步驟 5：整合所有步驟 – 完整可執行腳本

以下是最終腳本，將所有部件串接起來。將其儲存為 `load_image_ocr_demo.py`，然後在命令列執行。

```python
# load_image_ocr_demo.py
import os
import ocr

def init_engine():
    try:
        engine = ocr.OcrEngine()
        print("✅ OCR engine created.")
        return engine
    except ocr.OcrException as e:
        print(f"❌ Could not create OCR engine (code {e.code}): {e.message}")
        raise

def load_image_with_exception(engine, path):
    try:
        engine.load_image(path)
        print(f"✅ Loaded image via exception method: {path}")
    except ocr.OcrException as ex:
        print(f"❌ Exception while loading '{path}': {ex.message}")

def load_image_with_error_api(engine, path):
    engine.load_image(path)
    err = engine.get_last_error()
    if err:
        print(f"❌ Error API reported for '{path}': {err.message}")
    else:
        print(f"✅ Loaded image via error API: {path}")

def extract_text(engine):
    try:
        result = engine.recognize()
        txt = result.text
        if txt:
            print("📝 OCR Result:")
            print(txt)
        else:
            print("⚠️ No recognizable text.")
        return txt
    except ocr.OcrException as e:
        print(f"❌ Recognition error: {e.message}")
        return ""

def main():
    # 1️⃣ Create the OCR engine
    engine = init_engine()

    # Paths – adjust to your environment
    existing_img = os.path.join("samples", "document.png")
    missing_img = os.path.join("samples", "nonexistent.png")

    # 2️⃣ Load a valid image using exception handling
    load_image_with_exception(engine, existing_img)
    extract_text(engine)

    # 3️⃣ Attempt to load a missing image using the error API
    load_image_with_error_api(engine, missing_img)

if __name__ == "__main__":
    main()
```

**預期輸出（當 `document.png` 存在時）：**

```
✅ OCR engine created.
✅ Loaded image via exception method: samples/document.png
📝 OCR Result:
[Here you’ll see the extracted text from the image]

✅ Loaded image via error API: samples/nonexistent.png
❌ Error API reported for 'samples/nonexistent.png': File not found
```

如果影像遺失，腳本會優雅地回報問題，而不會當機——這正是生產環境所需要的。

## 常見陷阱與專業提示

- **檔案路徑怪癖：** Windows 使用反斜線 (`\`) 可能被解讀為跳脫字元。請使用原始字串 (`r"C:\\path\\file.png"`) 或如範例所示的 `os.path.join`。  
- **不支援的格式：** 大多數 OCR 引擎（如 Tesseract）支援 PNG、JPEG、TIFF。若提供 BMP，會回傳錯誤碼。請先使用 Pillow（`Image.save(..., format="PNG")`）轉換後再載入。  
- **記憶體洩漏：** 重複使用同一引擎雖然有效率，但完成後別忘了呼叫 `engine.close()`（或相應的函式），尤其在長時間執行的服務中。  
- **批次處理：** 將載入與擷取步驟包在針對目錄的 `for` 迴圈中。將每個錯誤記錄到獨立檔案，這樣除錯大型資料集就不會痛苦。

## 視覺概覽

![載入影像 OCR 圖示，展示引擎建立、錯誤處理與文字擷取](load_image_ocr_diagram.png "載入影像 OCR 工作流程")

*替代文字：載入影像 OCR 圖示說明建立 OCR 引擎、載入影像、處理錯誤與擷取文字的步驟。*

## 結論

我們剛剛已說明如何在 Python 中可靠地 **載入影像 OCR** 同時 **建立 OCR 引擎**。從初始化引擎、以例外與函式庫的錯誤 API 處理遺失檔案，到最終擷取辨識文字，完整腳本已可直接嵌入任何專案。

請記住：穩健的 OCR 不僅取決於你選擇的函式庫，更在於優雅的錯誤處理、合理的資源管理與清晰的日誌。透過本教學示範的模式，你可以從單張影像示範擴展到生產等級的批次管線，而不必重新發明輪子。

### 接下來？

- 嘗試 **影像前處理**（對比度提升、去斜）以提升準確度。  
- 將佔位的 `ocr` 套件換成 Tesseract、EasyOCR 或雲端服務，並相應調整 `init_engine` 函式。  
- 將 OCR 輸出整合至資料庫或搜尋索引，以支援文件檢索的使用情境。  

有任何問題或遇到奇怪的邊緣案例嗎？歡迎在下方留言，祝編程愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}