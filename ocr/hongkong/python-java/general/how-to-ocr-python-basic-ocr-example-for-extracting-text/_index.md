---
category: general
date: 2026-04-26
description: 如何在 Python 中使用 OCR：學習從圖像提取文字並使用基本 OCR 範例讀取 TIFF 檔案。附上快速可執行的程式碼。
draft: false
keywords:
- how to ocr python
- extract text from image
- read tiff file python
- basic ocr example
- convert scanned image text
language: zh-hant
og_description: 如何在 Python 中使用 OCR：一步一步的指南，展示如何從圖像提取文字、在 Python 中讀取 TIFF 檔案，以及使用簡單、可執行的腳本將掃描圖像文字轉換。
og_title: 如何在 Python 中進行 OCR – 基本 OCR 範例：提取文字
tags:
- OCR
- Python
- Image Processing
title: 如何使用 Python OCR – 基本 OCR 範例：提取文字
url: /zh-hant/python-java/general/how-to-ocr-python-basic-ocr-example-for-extracting-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Python 進行 OCR – 基本 OCR 範例：提取文字

有沒有想過 **如何使用 Python 進行 OCR**，當你桌上擺著一個掃描好的 TIFF 檔時？你並不是唯一一個盯著一堆影像檔，問自己「要怎樣把裡面的文字取出來？」的使用者。好消息是，只要有合適的函式庫和幾個清晰的步驟，將圖片轉成純文字其實輕而易舉。

在本教學中，我們會一步步示範一個 **基本 OCR 範例**，讀取 TIFF 檔、擷取文字，並將結果印到主控台。完成後，你將清楚知道如何 **從影像檔提取文字**、如何處理 TIFF 格式的特殊情況，以及在需要 **將掃描影像文字轉換** 成更有用的形式時該如何調整。沒有隱藏的魔法——只有直接可複製、可立即執行的 Python 程式碼。

## 需要的前置條件

在開始之前，請確保你已具備：

- 已安裝 Python 3.9 以上（建議使用最新穩定版）。
- 可透過 pip 安裝的 OCR 函式庫。本教學使用虛構的 `aocr` 套件，模擬 Tesseract 等常見工具；之後你可以改成 `pytesseract` 或 `easyocr`。
- 一個想要處理的 TIFF 影像——將它命名為 `input.tiff`，放在程式碼會參照的資料夾內。
- 基本的指令列操作知識（僅用於安裝套件）。

就這樣。沒有大型依賴、沒有 Docker 容器，只要幾行程式碼即可。

## 步驟 1 – 安裝與匯入相依套件（how to ocr python）

首先，取得 OCR 套件。打開終端機並執行：

```bash
pip install aocr
```

如果你想使用真實的函式庫，只要把 `aocr` 換成 `pytesseract`，並另行安裝 Tesseract 引擎即可。

接著匯入我們需要的模組。`pathlib` 中的 `Path` 類別讓我們能以跨平台的方式處理檔案路徑。

```python
# Step 1: Import the Path class for handling file paths
from pathlib import Path

# Import the OCR engine and image loader from the chosen library
from aocr import OcrEngine, Image
```

*為什麼使用 `Path`？* 因為它抽象化了斜線（`/` 與 `\`）的差異，讓你在拼接目錄時不必擔心底層作業系統。這個小細節常常能避免日後把腳本搬到 CI 伺服器時的頭痛。

## 步驟 2 – 建立 OCR 引擎實例（basic ocr example）

接下來，啟動 OCR 引擎。把 `OcrEngine` 想成會閱讀圖片並輸出字元的「大腦」。

```python
# Step 2: Create an instance of the OCR engine
ocr_engine = OcrEngine()
```

大多數 OCR 函式庫都允許在此調整語言、DPI 或信心門檻。對於這個 **基本 OCR 範例** 我們直接使用預設值，之後若需處理多語言文件，可自行探索 `ocr_engine.config`。

## 步驟 3 – 載入 TIFF 影像（read tiff file python）

這裡就是 **read tiff file python** 的關鍵。TIFF 可能包含多頁，但 `Image.load` 預設只抓取第一頁——對單頁掃描來說正好。

```python
# Step 3: Load the image you want to recognize
# Using a generic placeholder path makes it easy to adapt the example
ocr_engine.image = Image.load(Path("YOUR_DIRECTORY/input.tiff"))
```

把 `"YOUR_DIRECTORY"` 替換成實際存放 `input.tiff` 的資料夾路徑。若不確定腳本的執行目錄，`Path.cwd()` 會印出目前工作目錄，方便除錯路徑問題。

## 步驟 4 – 執行 OCR 處理（extract text from image）

現在魔法發生了。呼叫 `process()` 會把影像送入 OCR 流程，並回傳一個結果物件。

```python
# Step 4: Run the OCR process to extract text from the image
ocr_result = ocr_engine.process()
```

在背後，引擎可能會先將影像轉成灰階、套用二值化，然後送入神經網路。這些步驟你不需要自行管理，函式庫已為你抽象化。

## 步驟 5 – 印出辨識結果（convert scanned image text）

最後，將文字輸出。實務上你可能會寫入檔案或資料庫，但在範例中直接印出最為簡潔。

```python
# Step 5: Print the recognized text to the console
print(ocr_result.text)
```

執行腳本後，預期會看到類似以下的輸出：

```
Hello, world!
This is a sample scanned document.
```

如果結果雜亂，請再次確認原始影像是否清晰，以及 OCR 語言設定是否與文字相符。

## 完整可執行腳本

將上述所有片段組合起來，即得到完整、可直接執行的程式：

```python
# Full script: how to ocr python – basic OCR example

from pathlib import Path
from aocr import OcrEngine, Image  # Replace with your OCR library if needed

def main():
    # Initialize the OCR engine
    ocr_engine = OcrEngine()

    # Load the TIFF image (adjust the path as needed)
    image_path = Path("YOUR_DIRECTORY/input.tiff")
    if not image_path.is_file():
        raise FileNotFoundError(f"Could not find {image_path}. Make sure the file exists.")
    
    ocr_engine.image = Image.load(image_path)

    # Perform OCR
    ocr_result = ocr_engine.process()

    # Output the extracted text
    print("=== OCR Output ===")
    print(ocr_result.text)

if __name__ == "__main__":
    main()
```

### 預期輸出

```
=== OCR Output ===
Your scanned document’s text appears here, line by line.
```

若你需要 **將掃描影像文字轉換** 成可搜尋的 PDF，只要把 `ocr_result.text` 丟給像 `reportlab` 這樣的 PDF 產生器即可——但那又是另一篇完整教學。

## 常見問題與進階小技巧

- **低解析度掃描**：OCR 在 150 DPI 以下表現不佳。若 TIFF 模糊，可先使用 Pillow (`Image.open(...).resize(...)`) 進行升採樣。
- **多頁文件**：對多頁 TIFF，可遍歷 `Image.load_multi_page()`（若函式庫支援）並將結果串接。
- **語言支援**：多數引擎預設英文。若要辨識西班牙文，可設定 `ocr_engine.language = "spa"`。
- **空白處理**：OCR 常會產生多餘的換行。使用 `str.splitlines()` 或正規表達式清理輸出。
- **效能**：大量處理時，建議重複使用同一個 `OcrEngine` 實例，而非每個檔案都重新建立。

## 延伸範例

既然已掌握 **如何使用 Python 進行 OCR** 單張影像的技巧，接下來可以嘗試以下方向：

1. **批次處理** – 迴圈走訪資料夾中的所有 TIFF，將每個結果寫入 `.txt` 檔。
2. **結合 Pandas** – 把擷取的文字與中繼資料一起存入 DataFrame，方便後續分析。
3. **混合應用** – 結合 OCR 與 NLP 函式庫（如 `spaCy`）抽取發票中的實體（姓名、日期、金額）等資訊。
4. **支援其他檔案格式** – 把 `Image.load` 換成 `Image.from_bytes`，處理來自 API 或資料庫的影像資料。

以上皆以 **從影像檔提取文字** 與 **將掃描影像文字轉換** 成機器可理解的形式為核心概念。

## 結語

我們已完整示範一個 **基本 OCR 範例**，說明了 **如何使用 Python 進行 OCR**、**如何讀取 TIFF 檔** 以及 **如何從影像檔提取文字**，整個流程只需幾行程式碼。腳本自包含、具備錯誤處理，並直接印出結果，是任何需要將掃描文件轉成可編輯文字的專案的堅實基礎。

歡迎自行實驗——換掉 OCR 後端、微調前處理，或把輸出接到下游工作流程。只要能可靠地 **將掃描影像文字轉換** 成可搜尋、可分析的資料，未來的可能性就無限。

有關特殊情境、語言套件或效能調校的問題嗎？歡迎在下方留言，祝開發順利！

![how to ocr python example](/images/ocr-python-example.png "Screenshot of how to ocr python script output")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}