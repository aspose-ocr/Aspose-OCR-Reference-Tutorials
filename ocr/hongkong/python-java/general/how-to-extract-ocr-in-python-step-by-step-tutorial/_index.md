---
category: general
date: 2026-04-26
description: 如何使用 Python 從圖像提取 OCR – 一個 Python OCR 範例，展示如何載入圖像進行 OCR 並從收據中提取文字。
draft: false
keywords:
- how to extract ocr
- python ocr example
- extract text from receipt
- load image for ocr
- how to use OCR
language: zh-hant
og_description: 如何使用 Python 從圖像中提取 OCR。學習 Python OCR 範例，載入圖像進行 OCR，並在數分鐘內從收據中提取文字。
og_title: 如何在 Python 中提取 OCR – 完整指南
tags:
- OCR
- Python
- Image Processing
title: 如何在 Python 中提取 OCR – 步驟教學
url: /zh-hant/python-java/general/how-to-extract-ocr-in-python-step-by-step-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中提取 OCR – 完整指南

有沒有想過 **how to extract ocr** 從模糊的收據或掃描的發票？你並不是唯一的——開發者在需要乾淨、機器可讀的文字時，常常卡住。好消息是，只要幾行 Python 程式碼，就能把收據的照片轉換成高信心、可搜尋的文字。

在本教學中，我們將逐步示範一個 **python ocr example**，展示 **how to load image for ocr**，執行引擎，並僅保留符合 85 % 信心門檻的字元。完成後，你將能夠 **extract text from receipt** 圖片，而不必四處搜尋文件或猜測 API 參數。

## 需要的環境

- Python 3.9 或更新版本（我們使用的語法在 3.8+ 亦可運作）
- `aocr` 套件（或任何提供 `OcrEngine` 類別的 OCR 函式庫）。使用以下指令安裝：

```bash
pip install aocr
```

- 一張範例收據圖片（`receipt.png`），放在可參照的資料夾中。
- 文字編輯器或 IDE——如 VS Code、PyCharm，甚至簡易的 Notebook 都可。

就這樣。沒有笨重的框架，亦無外部服務，僅僅是純粹的 Python。

![高信心 OCR 結果 – how to extract ocr from a receipt](/images/ocr-high-confidence.png)

*圖片說明：使用 Python OCR how to extract ocr from a receipt*

## 第一步 – 建立 OCR 引擎實例 (how to extract ocr)

我們首先要啟動一個 OCR 引擎。可以把它想像成會為我們讀取像素的“大腦”。

```python
# Step 1: Initialize the OCR engine
from aocr import OcrEngine

ocr_engine = OcrEngine()
```

**Why?** 建立 `OcrEngine` 會得到一個全新的設定物件。之後你可以調整語言模型、DPI 設定或前處理步驟——全部不需要觸碰核心處理迴圈。

## 第二步 – 載入 OCR 圖片

接著我們將引擎指向要分析的圖片。這時 **load image for ocr** 關鍵字就會派上用場。

```python
# Step 2: Load the receipt image
image_path = "YOUR_DIRECTORY/receipt.png"
ocr_engine.image = OcrEngine.Image.load(image_path)
```

> **Pro tip:** 如果你的圖片位於其他目錄，請使用 `os.path.join` 來建立跨平台的路徑。

**Why load the image this way?** `Image.load` 輔助函式會將檔案讀入引擎能理解的格式，會自動處理常見的格式（PNG、JPEG、TIFF）。若跳過此步驟或直接傳入原始位元組，將拋出 `ValueError`。

## 第三步 – 執行 OCR 程序

現在我們真正執行 OCR。`process` 方法會回傳一個豐富的結果物件，內含辨識出的符號、信心分數與邊界框。

```python
# Step 3: Execute OCR and capture the result
ocr_result = ocr_engine.process()
```

**What does `ocr_result` contain?** 在大多數函式庫中，它包含：

- `text`：原始的串接字串。
- `symbol_confidences`：`(char, confidence)` 元組的列表。
- `boxes`：每個字元的座標（對視覺除錯很有幫助）。

取得每個字元的信心分數對於下一步至關重要。

## 第四步 – 只保留高信心符號 (≥ 85 %)

收據常會有污漬、淡印或背景噪音。過濾掉低信心的符號，我們可以大幅提升後續解析的品質。

```python
# Step 4: Filter out low‑confidence characters
high_confidence_text = ''.join(
    char for char, confidence in ocr_result.symbol_confidences
    if confidence >= 0.85
)
```

**Why 85 %?** 實務上，約 0.85 的門檻能在大多數印刷收據中取得召回率與精確度的平衡。若發現缺少數字，可降低門檻；若出現亂碼，則提高門檻。

## 第五步 – 輸出高信心的擷取文字

最後，我們列印（或儲存）已清理的字串。這就是我們 **extract text from receipt** 工作流程的核心。

```python
# Step 5: Show the cleaned result
print("High‑confidence text:", high_confidence_text)
```

典型的輸出如下：

```
High‑confidence text: Store XYZ
Date: 2024‑04‑22
Total: $23.45
```

現在你可以將此字串輸入 CSV 寫入器、資料庫，或任何後續的分析管線。

## 完整、可直接執行的腳本

以下是完整的程式碼片段，你可以直接複製貼上至 `ocr_receipt.py` 並立即執行。

```python
# ocr_receipt.py
# A complete python ocr example that extracts high‑confidence text from a receipt.

from aocr import OcrEngine

def main():
    # 1️⃣ Create the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load the image you want to analyze
    image_path = "YOUR_DIRECTORY/receipt.png"
    ocr_engine.image = OcrEngine.Image.load(image_path)

    # 3️⃣ Run the OCR process
    ocr_result = ocr_engine.process()

    # 4️⃣ Keep only symbols with confidence ≥ 85%
    high_confidence_text = ''.join(
        char for char, confidence in ocr_result.symbol_confidences
        if confidence >= 0.85
    )

    # 5️⃣ Output the result
    print("High‑confidence text:", high_confidence_text)

if __name__ == "__main__":
    main()
```

儲存檔案，確認 `receipt.png` 存在，然後執行：

```bash
python ocr_receipt.py
```

你應該會在主控台看到已清理的收據文字。

## 邊緣案例與假設情境

| Situation | Suggested Fix |
|-----------|----------------|
| **Very low confidence across the board** | 預先處理圖片：提升對比、轉為灰階，或套用去噪濾波 (`cv2.GaussianBlur`)。 |
| **Non‑Latin characters** | 傳入語言模型至 `OcrEngine`（例如 `ocr_engine.language = "spa"` 以支援西班牙文）。 |
| **Multiple receipts in one image** | 先對整張圖片執行 OCR，然後使用偵測 `\n\n+`（雙換行）的正規表達式分割結果。 |
| **Need the raw OCR text as well** | 保留 `ocr_result.text` 與過濾後的版本一起以供除錯。 |

## 常見陷阱（以及如何避免）

- **忘記安裝套件** – 必須先成功執行 `pip install aocr` 才能匯入。
- **在 Windows 使用錯誤的路徑分隔符**（`\` 與 `/`）。請使用 `os.path.join`。
- **未經測試就硬編碼信心門檻**——先在幾張收據上快速視覺檢查。
- **忽略 Unicode 正規化**——有些收據含特殊破折號；若要儲存輸出，請執行 `unicodedata.normalize('NFKC', text)`。

## 下一步 – 超越基礎應用

既然你已了解如何 **how to extract ocr** 單張收據的資料，接下來可能想要：

1. **批次處理收據資料夾** – 迴圈遍歷所有 PNG/JPG 檔案，將每個結果寫入 CSV。
2. **整合資料庫** – 將 `high_confidence_text` 存入 SQLite，以便快速查詢。
3. **套用自然語言解析** – 使用正規表達式或 `dateutil` 抽取日期、總金額與稅額。
4. **嘗試其他函式庫** – 若需多語言支援或更高準確度，可使用 `pytesseract`、`easyocr`，或雲端服務（Google Vision、Azure OCR）。

上述每個主題自然會涵蓋我們的次要關鍵字：*python ocr example*、*extract text from receipt*、*load image for ocr* 與 *how to use OCR*。

## 結論

我們剛剛完整示範了一個 **python ocr example**，說明如何 **how to extract ocr** 收據圖片的文字，過濾低信心符號，並輸出乾淨的結果。步驟簡單、程式碼自足，且此方法足夠彈性，可套用於更大型的專案。

試著用自己的收據跑一遍，調整信心門檻，然後再擴展至批次處理。若遇到奇怪情況——例如淡淡的商標或不常見的字型——請記得上述的邊緣案例建議。祝編程愉快，願你的 OCR 流程永遠精準！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}