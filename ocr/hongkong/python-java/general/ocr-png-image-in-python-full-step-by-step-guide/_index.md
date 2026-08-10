---
category: general
date: 2026-06-06
description: 使用 Python 進行 PNG 圖片 OCR – 學習如何從圖片中提取文字，執行 Python OCR 範例，甚至輕鬆閱讀古希臘文。
draft: false
keywords:
- ocr png image
- extract text from image
- python ocr example
- read ancient greek
- recognize image text
language: zh-hant
og_description: 在 Python 中說明 OCR PNG 圖像。本指南展示如何從圖像中提取文字、執行 Python OCR 範例，並輕鬆閱讀古希臘文。
og_title: OCR PNG 圖片於 Python – 完整教學
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: OCR PNG image with Python – learn how to extract text from image, run
    a python OCR example and even read ancient greek text easily.
  headline: OCR PNG Image in Python – Full Step‑by‑Step Guide
  type: TechArticle
- description: OCR PNG image with Python – learn how to extract text from image, run
    a python OCR example and even read ancient greek text easily.
  name: OCR PNG Image in Python – Full Step‑by‑Step Guide
  steps:
  - name: Prerequisites
    text: '| Requirement | Why it matters | |-------------|----------------| | Python
      3.8+ | Modern syntax and type hints | | `pytesseract` package | Thin wrapper
      around the Tesseract engine | | Tesseract OCR binaries (≥ 5.0) | The actual
      engine that does the heavy lifting | | Greek language data (`grc.trained'
  - name: How do I improve accuracy on a noisy PNG?
    text: '- Convert the image to grayscale: `img = img.convert(''L'')` - Apply a
      binary threshold: `img = img.point(lambda x: 0 if x < 128 else 255, ''1'')`
      - Upscale with `img = img.resize((img.width*2, img.height*2), Image.LANCZOS)`'
  - name: Can I process a whole folder of PNGs?
    text: Absolutely. Wrap the `recognize_image` call in a `for` loop over `Path.glob("*.png")`.
      Store each result in a dictionary or write to a CSV for later analysis.
  - name: What if I need to extract numbers only?
    text: 'Pass a custom **config** string to `image_to_string`:'
  - name: Is there a way to get confidence scores?
    text: Yes—use `pytesseract.image_to_data` which returns a TSV with confidence
      per word. You can filter out low‑confidence tokens before assembling the final
      string.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: 在 Python 中對 PNG 圖像進行 OCR – 完整逐步指南
url: /zh-hant/python-java/general/ocr-png-image-in-python-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python 中的 OCR PNG 圖像 – 完整步驟指南

有沒有想過如何直接在 Python 腳本中 **OCR PNG image** 檔案？也許你有一個充滿掃描古代手稿的資料夾，需要 **extract text from image** 檔案而不必手動逐字輸入。好消息是，你不需要計算機視覺的博士學位——只要幾行程式碼和合適的函式庫，你就能在幾秒鐘內閱讀古希臘文。

在本教學中，我們將逐步說明一個 **python OCR example**，它能辨識 PNG 中的文字、將語言設定為希臘語多音調，並輸出結果。完成後，你將清楚知道如何 **recognize image text**、處理常見問題，並將腳本套用到其他語言或圖像格式。

## 你將學到什麼

- 安裝與設定 Python OCR 函式庫（pytesseract + Tesseract OCR）
- 建立 OCR 引擎實例並載入 PNG 檔案
- 設定辨識語言為希臘語多音調，以便 **read ancient greek**
- 輸出辨識出的文字並排除常見問題
- 擴充腳本以批次處理多個 PNG 或切換至其他語言

### 前置條件

| Requirement | Why it matters |
|-------------|----------------|
| Python 3.8+ | 現代語法與型別提示 |
| `pytesseract` package | Tesseract 引擎的輕量包裝器 |
| Tesseract OCR binaries (≥ 5.0) | 執行實際運算的核心引擎 |
| Greek language data (`grc.traineddata`) | 正確 **read ancient greek** 所必需 |
| A PNG image you want to analyse (e.g., `ancient_greek.png`) | 我們的 **ocr png image** 示範目標 |

你可以使用以下指令安裝 Python 端：

```bash
pip install pytesseract Pillow
```

在 Ubuntu/macOS 上，你需要安裝引擎本身：

```bash
# Ubuntu
sudo apt-get install tesseract-ocr libtesseract-dev

# macOS (Homebrew)
brew install tesseract
```

別忘了下載希臘語多音調的訓練資料：

```bash
wget https://github.com/tesseract-ocr/tessdata/blob/main/greek.traineddata -P /usr/share/tesseract-ocr/4.00/tessdata/
```

*(路徑可能不同；如有需要請調整 `TESSDATA_PREFIX`。)*

---

## OCR PNG 圖像：建立引擎實例

我們首先需要一個與 Tesseract 溝通的物件。在 `pytesseract` 中，透過模組層級的函式存取引擎，但為了清晰，我們會將它包裝在一個小型類別中。這與原始程式碼中看到的「engine」概念相呼應。

```python
from pathlib import Path
from PIL import Image
import pytesseract

class OcrEngine:
    """
    Simple wrapper around pytesseract to keep the API similar to the original example.
    """
    def __init__(self, tess_cmd: str = "tesseract"):
        # You can point pytesseract to a custom binary if you installed it somewhere unusual.
        pytesseract.pytesseract.tesseract_cmd = tess_cmd

    def set_recognition_language(self, language: str):
        """
        Store the language code for later calls.
        Example: 'grc' for Greek polytonic.
        """
        self.lang = language

    def recognize_image(self, image_path: str):
        """
        Open the PNG, run OCR, and return the raw result object.
        """
        img = Image.open(image_path)
        # pytesseract returns a string; we wrap it for consistency with the original code.
        text = pytesseract.image_to_string(img, lang=self.lang)
        return OcrResult(text=text)

class OcrResult:
    """Container for OCR output – mimics the .text attribute used in the example."""
    def __init__(self, text: str):
        self.text = text
```

**為什麼要包裝？**  
- 保持公開 API 與你最初的程式碼片段相同，讓遷移毫無痛感。  
- 允許日後加入日誌或錯誤處理，而不必修改主要流程。  
- 展示良好的 OOP 實踐——讓資深開發者讚賞。

## 從圖像提取文字：設定語言為希臘語多音調

現在我們已有引擎，需要告訴它預期的語言。希臘語多音調使用標準「greek」資料未涵蓋的變音符號，因此我們將 Tesseract 指向 `grc` 訓練檔案。

```python
# Step 2: Set the recognition language to Greek polytonic
engine = OcrEngine()
engine.set_recognition_language("grc")   # 'grc' is the ISO‑639‑2 code for ancient Greek
```

如果你想在其他語言的 **extract text from image** 檔案中使用，只需將 `"grc"` 替換為 `"eng"`（英文）、`"fra"`（法文）等。只要安裝了相應語言，這行指令皆可使用。

## 辨識圖像文字：對 PNG 執行 OCR

設定語言後，我們將 PNG 輸入引擎。原始範例使用硬編碼路徑；我們將改用 `Path` 物件，使其更具彈性。

```python
# Step 3: Recognize text from the image file
image_path = Path("YOUR_DIRECTORY/ancient_greek.png")
ocr_result = engine.recognize_image(str(image_path))
```

**提示與邊緣情況**  
- **File not found** – 將呼叫包在 `try/except FileNotFoundError` 中，以提供友善訊息。  
- **Low‑resolution PNG** – 考慮在 OCR 前使用 Pillow 進行前處理（例如調整大小、二值化）。  
- **Non‑Greek text** – Tesseract 仍會嘗試解碼，但準確度會大幅下降。務必使用相符的語言設定。

## 輸出辨識文字

最後，我們將結果印出。在實際專案中，你可能會寫入資料庫、CSV，或甚至將其送入翻譯流程。

```python
# Step 4: Output the recognized text
print("=== OCR Result ===")
print(ocr_result.text)
```

當你對清晰的古希臘銘文掃描圖執行腳本時，應該會看到類似以下的輸出：

```
=== OCR Result ===
Ἀνδρὸς ἐστὶν ὁ ἥλιος...
```

如果輸出呈現亂碼，請再次確認 **greek.traineddata** 檔案位於正確資料夾，且 PNG 圖像沒有過於雜訊。

## 完整可執行範例（一步到位腳本）

以下是完整、可直接執行的程式。將其儲存為 `ocr_greek.py`，然後執行 `python ocr_greek.py`。

```python
# ocr_greek.py
from pathlib import Path
from PIL import Image
import pytesseract

class OcrEngine:
    def __init__(self, tess_cmd: str = "tesseract"):
        pytesseract.pytesseract.tesseract_cmd = tess_cmd
        self.lang = "eng"  # default fallback

    def set_recognition_language(self, language: str):
        self.lang = language

    def recognize_image(self, image_path: str):
        img = Image.open(image_path)
        text = pytesseract.image_to_string(img, lang=self.lang)
        return OcrResult(text)

class OcrResult:
    def __init__(self, text: str):
        self.text = text

def main():
    # 1️⃣ Create an OCR engine instance
    engine = OcrEngine()

    # 2️⃣ Set the language to Greek polytonic (read ancient greek)
    engine.set_recognition_language("grc")

    # 3️⃣ Path to the PNG you want to analyse
    png_path = Path("YOUR_DIRECTORY/ancient_greek.png")
    if not png_path.is_file():
        raise FileNotFoundError(f"Cannot find image at {png_path}")

    # 4️⃣ Recognize and retrieve the text
    result = engine.recognize_image(str(png_path))

    # 5️⃣ Print the extracted text
    print("=== OCR PNG Image Result ===")
    print(result.text)

if __name__ == "__main__":
    main()
```

**預期輸出**（為簡潔起見已截斷）：

```
=== OCR PNG Image Result ===
Ἀνδρὸς ἐστὶν ὁ ἥλιος·
Καὶ ὁ ἥλιος ἀνατέλλει·
```

如果你看到正確的希臘字元，恭喜你——你已成功在 Python 中執行 **ocr png image** 操作！

## 常見問題與專業技巧

### 如何提升噪點 PNG 的辨識準確度？

- 將圖像轉為灰階：`img = img.convert('L')`
- 套用二元化閾值：`img = img.point(lambda x: 0 if x < 128 else 255, '1')`
- 使用 `img = img.resize((img.width*2, img.height*2), Image.LANCZOS)` 進行放大

這些步驟常能將 **recognize image text** 的噩夢轉變為乾淨的結果。

### 我可以一次處理整個 PNG 資料夾嗎？

當然可以。將 `recognize_image` 呼叫包在 `for` 迴圈中，遍歷 `Path.glob("*.png")`。將每個結果存入字典或寫入 CSV，以供之後分析。

```python
for png in Path("my_folder").glob("*.png"):
    res = engine.recognize_image(str(png))
    print(f"{png.name}: {res.text[:50]}...")
```

### 如果我只需要提取數字呢？

將自訂的 **config** 字串傳遞給 `image_to_string`：

```python
digits = pytesseract.image_to_string(img, lang=self.lang, config='outputbase digits')
```

如此一來，你就能從包含表格、序號或時間戳記的 **extract text from image** 檔案中提取文字。

### 有辦法取得信心分數嗎？

可以——使用 `pytesseract.image_to_data`，它會回傳每個詞的信心分數 TSV。你可以在組合最終字串前過濾掉低信心的詞彙。

## 延伸本教學

既然你已掌握基礎，建議探索以下相關主題：

- **Batch OCR with multiprocessing** – 加速大量 PNG 語料庫的處理。  
- **Hybrid OCR + NLP pipelines** – 自動將提取的古希臘文翻譯成現代英文。  
- **Alternative engines** – 嘗試 `easyocr` 或基於 `opencv` 的方法以因應特定使用情境。  
- **Cloud OCR services** – 使用 Google Vision、Azure Computer Vision 或 AWS Textract 進行無伺服器擴展。

上述每項皆以我們剛剛介紹的核心 **python ocr example** 為基礎，讓你能更自在地深入探索。

## 結論

我們將簡單的程式碼片段轉變為在 Python 中穩健的 **ocr png image** 工作流程。透過建立 `OcrEngine`、設定語言為希臘語多音調、輸入 PNG 並印出結果，你現在已掌握如何 **extract text from image** 檔案、**recognize image text**，甚至 **read ancient greek**。

## 接下來該學什麼？

以下教學涵蓋與本指南密切相關的主題，並以此為基礎。每個資源都提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在自己的專案中探索替代實作方式。

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)
- [recognize text image with Aspose OCR for multiple languages](/ocr/english/net/ocr-settings/working-with-different-languages/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}