---
category: general
date: 2026-07-05
description: 使用 Python 對圖像執行 OCR。學習如何將圖像轉換為文字、載入圖像進行 OCR，並在數分鐘內從圖像中提取西里爾文字。
draft: false
keywords:
- perform OCR on image
- convert image to text python
- load image for OCR
- extract Cyrillic text from image
- recognize Cyrillic text
language: zh-hant
og_description: 在 Python 中執行圖像 OCR。本指南示範如何將圖像轉換為文字、載入圖像以進行 OCR，並快速從圖像中提取西里爾文字。
og_title: 使用 Python 於圖像執行 OCR – 完整教學
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Perform OCR on image using Python. Learn how to convert image to text
    python, load image for OCR and extract Cyrillic text from image in minutes.
  headline: Perform OCR on Image with Python – Complete Step‑by‑Step Guide
  type: TechArticle
tags:
- OCR
- Python
- Cyrillic
title: 使用 Python 進行圖像 OCR – 完整逐步指南
url: /zh-hant/python/general/perform-ocr-on-image-with-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Python 執行影像 OCR – 完整步驟指南

有沒有想過 **在不使用第三方服務的情況下執行影像 OCR**？你並不孤單。無論是護照掃描器、收據數位化工具，或是檔案保存系統，從圖片取得原始文字往往是第一道關卡。

在本教學中，我們將示範一個實務範例，**將影像轉換為文字 python** 風格，說明如何 **載入影像以供 OCR**，最後使用開源的 `aocr` 套件 **從影像中擷取西里爾文字**。完成後，你就能在任何圖片上 **辨識西里爾文字**。

> **學完你會得到：** 一個可直接執行的腳本、每一步的清楚說明，以及處理常見問題（如模糊掃描或字型不符）的技巧。全程不需外部 API，純粹使用 Python。

---

## 前置條件

在開始之前，請確保你已具備：

- 已安裝 Python 3.8 以上版本。
- 熟悉的終端機或命令提示字元。
- `aocr` 套件（可透過 `pip install aocr` 安裝）。
- 含有西里爾字元的影像檔（例如掃描的俄文護照）。

如果以上任一項你不熟悉，別擔心——我們會在後續簡要說明每個步驟。

---

## 第一步：執行影像 OCR – 建立執行環境

首先，我們需要一個乾淨的 Python 環境來安裝 OCR 函式庫。使用虛擬環境可以將相依性隔離，避免版本衝突。

```bash
# Create a virtual environment (optional but recommended)
python -m venv ocr-env
# Activate it (Windows)
ocr-env\Scripts\activate
# Activate it (macOS/Linux)
source ocr-env/bin/activate

# Install the aocr library
pip install aocr
```

**為什麼要這樣做？**  
專屬環境可確保 `aocr` 套件及其原生二進位檔不會干擾其他專案，同時讓可重現性變得容易——其他人只要 clone 你的 repo，執行 `pip install -r requirements.txt` 即可。

> **小技巧：** 使用 `pip freeze > requirements.txt` 冻結相依性，隨時知道使用的版本。

---

## 第二步：載入影像以供 OCR – 匯入與檔案前置

函式庫就緒後，我們需要 **載入影像以供 OCR**。`aocr.Image.from_file` 方法支援大多數常見格式（PNG、JPEG、TIFF）。以下示範如何使用：

```python
import aocr

# Path to the Cyrillic image – replace with your actual file location
image_path = "YOUR_DIRECTORY/rus_passport.png"

# Load the image into an aocr.Image object
cyrillic_image = aocr.Image.from_file(image_path)
```

**這段程式碼在做什麼？**  
`aocr.Image.from_file` 會讀取二進位資料、解碼，並存入 OCR 引擎可辨識的物件。若找不到檔案，Python 會拋出 `FileNotFoundError`，之後可自行捕捉以實作友善的錯誤處理。

> **邊緣案例：** 某些掃描器會輸出多頁 TIFF。此時需要先分割頁面——`aocr` 提供 `Image.from_tiff_pages()` 供使用。

---

## 第三步：設定 OCR 引擎 – 強制辨識西里爾文字

預設情況下，多數 OCR 引擎會自行猜測語言，對非拉丁文字往往產生雜訊。為了 **可靠辨識西里爾文字**，我們必須明確指定語言為 “cyrillic”。

```python
# Create an OCR engine instance
ocr_engine = aocr.OcrEngine()

# Force the engine to use the Cyrillic recognizer
ocr_engine.language = "cyrillic"
```

**為什麼要強制指定語言？**  
西里爾字母與拉丁字母在外觀上有相似之處（例如 “A” 與 “А”）。告訴引擎預期西里爾，可大幅降低誤辨，尤其在低解析度的掃描圖上。

---

## 第四步：執行影像 OCR – 進行文字辨識

影像已載入、引擎已調校完畢，我們終於可以 **執行影像 OCR**。`recognize` 方法會回傳一個 `OcrResult` 物件，內含擷取的文字與信心分數。

```python
# Run the OCR process
ocr_result = ocr_engine.recognize(cyrillic_image)

# Print the raw text
print("Cyrillic text:")
print(ocr_result.text)
```

**`ocr_result` 會提供什麼？**  
- `text`：辨識出的純文字字串。  
- `confidence`：0‑1 之間的浮點數，代表整體信心。  
- `lines`：若需更細部控制，可取得每行物件的列表。

> **常見問題：** *如果文字是倒置的怎麼辦？*  
> `aocr` 能自動旋轉影像，只要在呼叫 `recognize` 前設定 `ocr_engine.auto_rotate = True` 即可。

---

## 第五步：將影像轉換為文字 Python – 後處理輸出

原始字串可能包含多餘的空白或換行符號。為了 **將影像轉換為文字 python** 風格，我們會用簡單的步驟清理它：

```python
import re

# Remove extra whitespace and normalize line breaks
clean_text = re.sub(r'\s+', ' ', ocr_result.text).strip()

print("\nCleaned Cyrillic text:")
print(clean_text)
```

**為什麼要這樣做？**  
清理過的輸出較易投入後續流程——無論是寫入資料庫、送給翻譯 API，或是使用正規表達式搜尋護照號碼，都會更方便。

---

## 第六步：從影像擷取西里爾文字 – 完整整合

把前面的步驟包成一個可重用的函式，讓 **從影像擷取西里爾文字** 只要一行程式碼即可在專案中使用。

```python
def extract_cyrillic_text(image_path: str) -> str:
    """
    Loads an image, forces Cyrillic OCR, and returns cleaned text.
    """
    # Load image
    img = aocr.Image.from_file(image_path)

    # Configure OCR engine for Cyrillic
    engine = aocr.OcrEngine()
    engine.language = "cyrillic"

    # Recognize text
    result = engine.recognize(img)

    # Clean up the output
    cleaned = re.sub(r'\s+', ' ', result.text).strip()
    return cleaned

# Example usage
if __name__ == "__main__":
    path = "YOUR_DIRECTORY/rus_passport.png"
    print("Extracted text:", extract_cyrillic_text(path))
```

**預期結果（範例）：**

```
Extracted text: ПАСПОРТ РФ № 1234567890 ИМЯ ФАМИЛИЯ ДАТА РОЖДЕНИЯ 01.01.1990
```

只要影像清晰且字型與 OCR 模型相符，就能得到近乎完美的文字轉錄。

---

## 故障排除與提示

| 問題 | 可能原因 | 解決方式 |
|------|----------|----------|
| 文字雜亂 | 語言設定錯誤 | 確認 `ocr_engine.language = "cyrillic"` |
| 輸出為空 | 影像過暗或解析度太低 | 使用 `opencv` 前處理提升對比度 |
| 方向錯誤 | 影像旋轉了 90° | 設定 `ocr_engine.auto_rotate = True` |
| 效能緩慢 | 圖片過大（>5 MP） | 在辨識前使用 `aocr.Image.resize(width=1024)` 縮小尺寸 |

---

![perform OCR on image example](ocr_example.png "perform OCR on image example")

*替代文字：*「執行影像 OCR 範例，展示 Python 程式碼從護照掃描圖中擷取西里爾文字。」

---

## 結論

我們已使用純 Python 完成 **執行影像 OCR**，學會如何 **載入影像以供 OCR**，強制引擎 **辨識西里爾文字**，最後透過一個整潔的輔助函式 **從影像擷取西里爾文字**。從安裝 `aocr`、清理結果，到完整的程式碼，只需數十行即可嵌入任何需要 **將影像轉換為文字 python** 的專案。

---

## 接下來可以做什麼？

- **批次處理：** 迴圈遍歷資料夾中的掃描檔，將結果寫入 SQLite。  
- **語言偵測：** 結合 `langdetect` 與 `aocr`，自動在西里爾與拉丁之間切換。  
- **進階前處理：** 使用 `opencv` 去除傾斜、降噪或二值化，以提升辨識準確度。  
- **整合 FastAPI：** 將 `extract_cyrillic_text` 函式以 REST 端點方式提供給 Web 應用。

盡情實驗吧——把語言改成 “latin” 以辨識英文護照，或換成其他 OCR 後端。概念相同，程式碼也足夠彈性可調整。

祝開發順利，願你的影像永遠清晰可辨！

---

## 接下來該學什麼？

以下教學與本篇內容密切相關，能進一步擴展你的技巧。每篇資源皆提供完整可執行的程式碼範例與逐步說明，助你掌握更多 API 功能，並探索替代實作方式。

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}