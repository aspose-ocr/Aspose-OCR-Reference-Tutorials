---
category: general
date: 2026-05-03
description: Python OCR 教學，示範如何載入 PNG 圖像檔案、辨識圖像文字，並提供免費 AI 資源以進行批量 OCR 處理。
draft: false
keywords:
- python ocr tutorial
- batch ocr processing
- free ai resources
- load png image
- recognize text from image
language: zh-hant
og_description: Python OCR 教學將指導你如何載入 PNG 圖像、從圖像中辨識文字，以及處理免費 AI 資源以進行批次 OCR 處理。
og_title: Python OCR 教學 – 使用免費 AI 資源快速批次 OCR
tags:
- OCR
- Python
- AI
title: Python OCR 教學 – 批量 OCR 處理變得簡單
url: /zh-hant/python/general/python-ocr-tutorial-batch-ocr-processing-made-easy/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python OCR 教學 – 批次 OCR 處理變得簡單

有沒有需要一個 **python ocr tutorial**，真的可以讓你一次處理數十個 PNG 檔案而不抓狂？你並不孤單。在許多實務專案中，你必須 **load png image** 檔案，將它們送入引擎，然後在完成後清理 AI 資源。

在本指南中，我們將一步步走過一個完整、可直接執行的範例，說明如何 **recognize text from image** 檔案、批次處理，並釋放底層 AI 記憶體。最後，你會得到一個可直接放入任何專案的自包含腳本——沒有多餘的贅述，只有必要的核心。

## 需要的條件

- Python 3.10 或更新版本（此處使用的語法依賴 f‑strings 與 type hints）  
- 一個提供 `engine.recognize` 方法的 OCR 套件——示範中我們假設有一個虛構的 `aocr` 套件，你也可以改用 Tesseract、EasyOCR 等。  
- 文章中程式碼片段所示的 `ai` 輔助模組（負責模型初始化與資源清理）  
- 一個放有欲處理 PNG 檔案的資料夾  

如果你尚未安裝 `aocr` 或 `ai`，可以使用下方的「可選 Stubs」來模擬——請參考最後的說明。

## 步驟 1：初始化 AI 引擎（Free AI Resources）

在將任何影像送入 OCR 流程之前，必須先讓底層模型就緒。只初始化一次即可節省記憶體並加速批次作業。

```python
# step_1_initialize.py
import ai                # hypothetical helper that wraps the AI model
import aocr               # OCR library

def init_engine(config_path: str = "config.yaml"):
    """
    Initialize the AI engine if it hasn't been set up yet.
    This uses free AI resources – the engine will be released later.
    """
    if not ai.is_initialized():
        ai.initialize(config_path)   # auto‑initialize with the provided configuration
    else:
        print("Engine already initialized.")
```

**為什麼這很重要：**  
若對每張影像都重複呼叫 `ai.initialize`，會不斷分配 GPU 記憶體，最終導致腳本崩潰。透過檢查 `ai.is_initialized()`，我們保證只分配一次——這就是「Free AI Resources」的原則。

## 步驟 2：載入 PNG 影像檔案以進行批次 OCR 處理

現在我們收集所有要進行 OCR 的 PNG 檔案。使用 `pathlib` 可讓程式碼保持跨平台。

```python
# step_2_load_images.py
from pathlib import Path
from typing import List

def collect_png_paths(directory: str) -> List[Path]:
    """
    Scan `directory` and return a list of Path objects pointing to PNG files.
    """
    base_path = Path(directory)
    if not base_path.is_dir():
        raise NotADirectoryError(f"'{directory}' is not a valid folder.")
    
    png_files = sorted(base_path.glob("*.png"))
    if not png_files:
        raise FileNotFoundError("No PNG images found in the specified directory.")
    
    print(f"Found {len(png_files)} PNG image(s) to process.")
    return png_files
```

**邊緣情況：**  
如果資料夾中有非 PNG 檔案（例如 JPEG），會被忽略，避免 `engine.recognize` 因不支援的格式而失敗。

## 步驟 3：對每張影像執行 OCR 並進行後處理

在引擎就緒且檔案清單準備好之後，我們可以逐一迭代影像，取得原始文字，並交給後處理器清理常見的 OCR 雜訊（例如多餘的換行）。

```python
# step_3_ocr_batch.py
import aocr
import ai
from pathlib import Path
from typing import List

def ocr_batch(image_paths: List[Path]) -> List[str]:
    """
    Perform OCR on each PNG image and return a list of cleaned strings.
    """
    results = []
    for image_path in image_paths:
        # Load the image – aocr.Image.load abstracts away Pillow/OpenCV details
        img = aocr.Image.load(str(image_path))
        
        # Recognize raw text
        raw_text = engine.recognize(img)
        
        # Refine the raw OCR output using the AI post‑processor
        cleaned_text = ai.run_postprocessor(raw_text)
        results.append(cleaned_text)
        
        print(f"Processed {image_path.name}: {len(cleaned_text)} characters extracted.")
    
    return results
```

**為什麼要將載入與辨識分開：**  
`aocr.Image.load` 可能採用延遲解碼，對大型批次更快。將載入步驟寫得明確，也方便日後改用其他影像函式庫（例如處理 JPEG 或 TIFF）時直接替換。

## 步驟 4：清理 – 在批次結束後釋放 AI 資源

批次處理完成後，我們必須釋放模型，以免記憶體泄漏，特別是在有 GPU 的機器上。

```python
# step_4_cleanup.py
import ai

def release_resources():
    """
    Free any allocated AI resources. Safe to call multiple times.
    """
    if ai.is_initialized():
        ai.free_resources()
        print("AI resources have been released.")
    else:
        print("No AI resources were allocated.")
```

## 完整腳本 – 把四個步驟串起來

以下是一個單一檔案，將上述四個步驟整合成完整工作流程。將其存為 `batch_ocr.py`，然後在命令列執行。

```python
# batch_ocr.py
"""
Python OCR tutorial – end‑to‑end batch OCR processing.
Loads PNG images, runs OCR, post‑processes results, and frees AI resources.
"""

import sys
from pathlib import Path
import ai
import aocr

# ----------------------------------------------------------------------
# Helper functions (copied from the steps above)
# ----------------------------------------------------------------------
def init_engine(cfg: str = "config.yaml"):
    if not ai.is_initialized():
        ai.initialize(cfg)
    else:
        print("Engine already initialized.")

def collect_png_paths(directory: str):
    base_path = Path(directory)
    if not base_path.is_dir():
        raise NotADirectoryError(f"'{directory}' is not a valid folder.")
    png_files = sorted(base_path.glob("*.png"))
    if not png_files:
        raise FileNotFoundError("No PNG images found in the specified directory.")
    print(f"Found {len(png_files)} PNG image(s) to process.")
    return png_files

def ocr_batch(image_paths):
    results = []
    for image_path in image_paths:
        img = aocr.Image.load(str(image_path))
        raw_text = engine.recognize(img)
        cleaned_text = ai.run_postprocessor(raw_text)
        results.append(cleaned_text)
        print(f"Processed {image_path.name}: {len(cleaned_text)} characters.")
    return results

def release_resources():
    if ai.is_initialized():
        ai.free_resources()
        print("AI resources released.")
    else:
        print("No resources to release.")

# ----------------------------------------------------------------------
# Main execution block
# ----------------------------------------------------------------------
if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python batch_ocr.py <directory-with-png>")
        sys.exit(1)

    image_dir = sys.argv[1]

    try:
        init_engine()
        png_paths = collect_png_paths(image_dir)
        texts = ocr_batch(png_paths)

        # Optional: write results to a single text file
        output_file = Path("ocr_results.txt")
        with output_file.open("w", encoding="utf-8") as f:
            for path, txt in zip(png_paths, texts):
                f.write(f"--- {path.name} ---\n")
                f.write(txt + "\n\n")
        print(f"All results saved to {output_file.resolve()}")
    finally:
        release_resources()
```

### 預期輸出

對包含三個 PNG 的資料夾執行腳本時，可能會印出：

```
Engine already initialized.
Found 3 PNG image(s) to process.
Processed invoice1.png: 452 characters.
Processed receipt2.png: 317 characters.
Processed flyer3.png: 689 characters.
All results saved to /home/user/ocr_results.txt
AI resources released.
```

`ocr_results.txt` 檔案會為每張影像加入清晰的分隔符，並寫入清理過的 OCR 文字。

## 可選 Stubs（若沒有真實的 aocr 與 ai 套件）

如果你只想測試流程，而不想安裝大型 OCR 套件，可以建立最小的模擬模組：

```python
# aocr/__init__.py
class Image:
    @staticmethod
    def load(path):
        return f"ImageObject({path})"

def dummy_recognize(image):
    return "Raw OCR output for " + str(image)

engine = type("Engine", (), {"recognize": dummy_recognize})()
```

```python
# ai/__init__.py
_state = {"initialized": False}

def is_initialized():
    return _state["initialized"]

def initialize(cfg):
    print(f"Initializing AI engine with {cfg}")
    _state["initialized"] = True

def run_postprocessor(text):
    # Very naive cleanup: strip extra spaces
    return " ".join(text.split())

def free_resources():
    print("Freeing AI resources")
    _state["initialized"] = False
```

將這兩個資料夾放在 `batch_ocr.py` 同一目錄下，腳本即可執行，並印出模擬結果。

## 專業小技巧與常見陷阱

- **記憶體峰值**：若處理成千上萬張高解析度 PNG，建議在 OCR 前先縮小尺寸。`aocr.Image.load` 通常接受 `max_size` 參數。  
- **Unicode 處理**：務必以 `encoding="utf-8"` 開啟輸出檔案；OCR 引擎可能會產生非 ASCII 字元。  
- **平行處理**：對於 CPU‑bound 的 OCR，可以將 `ocr_batch` 包在 `concurrent.futures.ThreadPoolExecutor` 中執行。但記得只保留單一 `ai` 實例——若每個執行緒都呼叫 `ai.initialize`，會破壞「Free AI Resources」的目標。  
- **錯誤韌性**：將每張影像的迴圈包在 `try/except` 中，避免單一損壞的 PNG 中斷整個批次。

## 結語

現在你已掌握一個 **python ocr tutorial**，示範如何 **load png image** 檔案、執行 **batch OCR processing**，以及負責任地管理 **Free AI Resources**。完整、可執行的範例清楚說明了如何 **recognize text from image** 物件並在之後清理資源，讓你可以直接複製貼上到自己的專案中，而不必再尋找缺失的部份。

準備好下一步了嗎？試著將這裡的 stub `aocr` 與 `ai` 模組換成真實的庫，例如 `pytesseract` 或 `torchvision`。你也可以擴充腳本，輸出 JSON、寫入資料庫，或整合雲端儲存桶。可能性無限——祝你寫程式開心！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}