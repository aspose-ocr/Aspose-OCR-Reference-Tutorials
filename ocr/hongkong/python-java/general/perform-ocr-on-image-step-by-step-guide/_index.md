---
category: general
date: 2026-03-18
description: 快速對圖像執行光學字符辨識，提取文字。了解如何載入圖像進行 OCR、建立 OCR 引擎，並透過語言選項提升辨識準確度。
draft: false
keywords:
- perform OCR on image
- extract text from image
- improve OCR accuracy
- load image for OCR
- create OCR engine
language: zh-hant
og_description: 使用本詳細指南對圖像執行 OCR。學習如何載入圖像進行 OCR、建立 OCR 引擎，並提升 OCR 準確度，以獲得可靠的文字提取。
og_title: 在圖像上執行 OCR – 完整程式設計教學
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: 對圖像執行 OCR – 步驟指南
url: /zh-hant/python-java/general/perform-ocr-on-image-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在圖像上執行 OCR – 完整程式教學

曾經需要**在圖像上執行 OCR**，但不確定該選擇哪個函式庫或如何取得可靠的結果嗎？你並不孤單。在本指南中，我們將逐步說明取得**從圖像中提取文字**所需的一切，從載入圖片到微調語言選項，讓你在每個步驟都能**提升 OCR 準確度**。

我們將說明如何**載入圖像以進行 OCR**、如何**建立 OCR 引擎**，以及每個設定為何重要。完成後，你將擁有一個可直接執行的腳本，會印出辨識出的文字，且能了解每行程式背後的「原因」——不會只給你模糊的「請參考文件」捷徑。讓我們開始吧。

## 需要的環境

- Python 3.8+（程式碼使用 f‑strings 與型別提示）
- 假想的 `ocr_lib` 套件 – 使用 `pip install ocr_lib` 安裝
- 包含清晰印刷文字的圖像檔案（例如 `lab_report.png`）
- 基本的文字編輯器或 IDE（VS Code、PyCharm，或任何你喜歡的）

如果你已經具備上述條件，太好了——已經可以開始。如果還沒有，請從 python.org 下載 Python，並執行 pip 指令；只需要一分鐘。

![在圖像上執行 OCR 範例 – 顯示提取文字的樣本輸出](/images/ocr-example.png)

*Alt text: 在圖像上執行 OCR – 顯示提取文字的樣本輸出.*

## 第一步：建立 OCR 引擎 – 如何在 Python 中**建立 OCR 引擎**

在任何辨識發生之前，函式庫需要一個保存設定與執行階段狀態的引擎物件。可以把引擎想像成整個操作的“大腦”。

```python
# step_1_create_engine.py
from ocr_lib import OcrEngine, LanguageOptions, OcrResult

def build_engine() -> OcrEngine:
    """
    Initialize and return a fresh OcrEngine instance.
    Creating the engine once and reusing it is more efficient than
    instantiating it inside a loop.
    """
    engine = OcrEngine()
    return engine
```

**為什麼這很重要：** 及早實例化引擎可以讓你之後附加語言選項，且它會快取內部模型，以加快後續呼叫的速度。

## 第二步：載入圖像以進行 OCR – 正確的**載入圖像以進行 OCR**方式

既然已經有了引擎，我們必須給它要讀取的圖像。`setImageFromFile` 方法接受檔案系統路徑；該路徑可以是絕對路徑或相對於腳本工作目錄的路徑。

```python
# step_2_load_image.py
def load_image(engine: OcrEngine, image_path: str) -> None:
    """
    Attach an image file to the engine.
    Raises FileNotFoundError if the file does not exist.
    """
    engine.setImageFromFile(image_path)
```

**小技巧：** 使用絕對路徑或 `os.path.join`，可避免腳本在不同資料夾執行時出現「找不到檔案」的情況。

```python
import os

image_file = os.path.join("YOUR_DIRECTORY", "lab_report.png")
load_image(my_engine, image_file)
```

## 第三步：提升 OCR 準確度 – 微調**語言選項**以**提升 OCR 準確度**

開箱即用的 OCR 雖然能運作，但領域特定的詞彙（例如實驗室術語）常會讓它出錯。透過提供自訂字典與黑名單，可減少例如把「0」誤辨為「O」之類的錯誤辨識。

```python
# step_3_language_options.py
def configure_language(engine: OcrEngine) -> None:
    """
    Set up language options to help the engine recognize domain‑specific terms
    and ignore characters that are frequently misread.
    """
    language_opts = LanguageOptions()
    # Add terms that appear often in laboratory reports
    language_opts.setDictionary(["HPLC", "UV‑VIS", "chromatogram"])
    # Blacklist characters that cause confusion
    language_opts.setBlacklist(["0", "O", "l", "1"])
    engine.setLanguageOptions(language_opts)
```

**為什麼這有幫助：** 字典告訴 OCR 模型「HPLC」是一個有效的詞彙，避免模型將其拆成無意義的字串。黑名單則指示模型將模糊的符號視為噪音，從而直接**提升 OCR 準確度**。

## 第四步：在圖像上執行 OCR – 核心的**在圖像上執行 OCR**呼叫

引擎已就緒且圖像已載入，現在是實際辨識文字的時候。此步驟會回傳一個 `OcrResult` 物件，你可以查詢原始文字、信心分數或邊界框等資訊。

```python
# step_4_recognize.py
def recognize_text(engine: OcrEngine) -> OcrResult:
    """
    Run the OCR process. This may take a few seconds depending on image size.
    Returns an OcrResult that contains the extracted string and metadata.
    """
    result = engine.recognize()
    return result
```

如果圖像模糊，結果中的信心分數會較低。這時應在送入引擎前先對圖像進行前處理（例如提升對比度）。

## 第五步：從圖像中提取文字 – 取得最終字串

最後，我們向 `OcrResult` 索取文字表示。`getText()` 方法會回傳純文字字串，已可直接用於後續處理（儲存至檔案、寫入資料庫等）。

```python
# step_5_output.py
def print_result(result: OcrResult) -> None:
    """
    Output the recognized text to the console.
    You could also write it to a file with open('output.txt', 'w') …
    """
    extracted = result.getText()
    print("=== OCR Output Start ===")
    print(extracted)
    print("=== OCR Output End ===")
```

**預期輸出：** 假設 `lab_report.png` 包含一個簡單的表格，可能會看到類似以下內容：

```
=== OCR Output Start ===
Sample ID: 00123
Method: HPLC
Result: 5.67 mg/L
=== OCR Output End ===
```

這就是**從圖像中提取文字**的部分完成了。

## 完整範例 – 整合所有步驟

以下是一個完整腳本，將前面各段落的程式碼串接起來。你可以將它複製貼上至 `run_ocr.py`，然後執行 `python run_ocr.py`。

```python
# run_ocr.py
import os
from ocr_lib import OcrEngine, LanguageOptions, OcrResult

def build_engine() -> OcrEngine:
    engine = OcrEngine()
    return engine

def load_image(engine: OcrEngine, image_path: str) -> None:
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")
    engine.setImageFromFile(image_path)

def configure_language(engine: OcrEngine) -> None:
    language_opts = LanguageOptions()
    language_opts.setDictionary(["HPLC", "UV‑VIS", "chromatogram"])
    language_opts.setBlacklist(["0", "O", "l", "1"])
    engine.setLanguageOptions(language_opts)

def recognize_text(engine: OcrEngine) -> OcrResult:
    return engine.recognize()

def print_result(result: OcrResult) -> None:
    extracted = result.getText()
    print("\n=== OCR Output Start ===")
    print(extracted)
    print("=== OCR Output End ===\n")

def main() -> None:
    # 1️⃣ Create the OCR engine
    ocr_engine = build_engine()

    # 2️⃣ Load the image you want to process
    image_file = os.path.join("YOUR_DIRECTORY", "lab_report.png")
    load_image(ocr_engine, image_file)

    # 3️⃣ Apply language tweaks to **improve OCR accuracy**
    configure_language(ocr_engine)

    # 4️⃣ **Perform OCR on image** – this is the heavy lifting
    ocr_result = recognize_text(ocr_engine)

    # 5️⃣ **Extract text from image** and show it
    print_result(ocr_result)

if __name__ == "__main__":
    main()
```

### 快速驗證清單

| ✅ | 項目 |
|---|------|
| ✔️ | 已建立引擎（`create OCR engine`） |
| ✔️ | 已載入圖像（`load image for OCR`） |
| ✔️ | 已設定語言選項（`improve OCR accuracy`） |
| ✔️ | 已執行 OCR（`perform OCR on image`） |
| ✔️ | 已提取文字（`extract text from image`） |

執行腳本並觀察主控台。如果看到包含報告內容的「OCR Output」區塊，表示你已成功**在圖像上執行 OCR**。

## 常見問題與避免方法

| 問題 | 發生原因 | 解決方法 |
|------|----------|----------|
| **Blurry input** | OCR 模型無法辨識字符 | 使用 OpenCV 前處理：`cv2.GaussianBlur` 或提升 DPI |
| **Wrong language** | 預設語言可能不是英文 | 在 `recognize()` 前呼叫 `engine.setLanguage("eng")` |
| **Missing dictionary terms** | 領域特定詞彙會變成亂碼 | 如第 3 步所示，使用 `setDictionary` 加入詞彙 |
| **Blacklisted characters cause

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}