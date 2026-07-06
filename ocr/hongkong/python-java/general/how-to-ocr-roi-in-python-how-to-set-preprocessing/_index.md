---
category: general
date: 2026-03-28
description: 如何在 Python 中對 ROI 進行 OCR – 了解如何設定前處理選項，以從特定圖像區域精確提取文字。
draft: false
keywords:
- how to OCR ROI
- how to set preprocessing
- Aspose OCR Python
- ROI extraction
- image preprocessing OCR
language: zh-hant
og_description: 如何在 Python 中對 ROI 進行 OCR – 本指南示範如何設定前處理，以可靠地從指定的圖像區域提取文字。
og_title: 如何在 Python 中對 ROI 進行 OCR – 如何設定前置處理
tags:
- OCR
- Python
- Aspose
title: 如何在 Python 中對 ROI 進行 OCR – 如何設定前置處理
url: /zh-hant/python-java/general/how-to-ocr-roi-in-python-how-to-set-preprocessing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中 OCR ROI – 如何設定前處理

有沒有想過 **如何在嘈雜的發票圖像中 OCR ROI**，卻不必把整頁載入記憶體？你並不是唯一有此疑問的人。在許多實務專案中，我們只需要少數欄位——客戶名稱、地址、總金額——因此掃描整份文件實在是大材小用。

好消息是？使用 Aspose OCR，你可以告訴引擎 **要找哪裡**，甚至先把圖像清理乾淨。這篇教學將一步步說明 **如何設定前處理** 選項、定義感興趣區域（ROI），並只用幾行 Python 取得乾淨的文字。

閱讀完本指南後，你將擁有一個可直接執行的腳本，能從任何發票、收據或表單中抽取特定區塊。無需額外工具，只要 Aspose OCR 加上一點 Python 邏輯即可。

---

## 需求條件

- **Python 3.8+**（程式碼在任何近期版本皆可執行）  
- **Aspose OCR for Python via .NET** – 以 `pip install aspose-ocr` 安裝  
- 一張範例圖（例如 `invoice.png`），放在可參照的資料夾內  
- 具備基本的 Python 函式與物件導向語法概念  

如果你已備妥上述條件，太好了——直接進入程式碼吧。

---

![如何 OCR ROI 示意圖](ocr-roi.png "如何 OCR ROI 範例圖")

*Alt text: 顯示發票圖像上 ROI 方框的如何 OCR ROI 示意圖*

---

## 第一步 – 初始化 OCR 引擎（How to OCR ROI）

在告訴引擎 **要找哪裡** 之前，我們需要先建立 OCR 處理器的實例。這個物件會保存所有設定，並執行辨識工作。

```python
import aspose.ocr as aocr
import aspose.storage as storage

# Create the engine – this is the entry point for all OCR work
ocr_engine = aocr.OcrEngine()
```

*為什麼重要*：`OcrEngine` 類別負責繁重的工作（字型偵測、版面分析等）。只建立一次引擎即可避免對每張圖像重新初始化大量資源，從而提升效能。

---

## 第二步 – 載入來源圖像（How to OCR ROI）

Aspose Storage 讓載入圖像變得非常簡單。只要指向檔案路徑，即可取得可供處理的 `Image` 物件。

```python
# Replace YOUR_DIRECTORY with the actual path where invoice.png lives
source_image = storage.Image.load("YOUR_DIRECTORY/invoice.png")
```

*小技巧*：若你是使用串流（例如透過 Web API 上傳的圖像），可以將 `BytesIO` 物件傳給 `Image.load`，而非檔案路徑。

---

## 第三步 – 定義感興趣區域（ROIs）

現在我們要回答核心問題 **how to OCR ROI**：告訴引擎我們關心的資料所在的精確矩形。每個 ROI 以左上角座標 (`x`, `y`) 以及尺寸 (`width`, `height`) 定義。

```python
from aspose.ocr import Roi

# Each tuple is (x, y, width, height) in pixels
regions_of_interest = [
    Roi(50, 120, 400, 60),   # Customer name block
    Roi(50, 200, 400, 80)    # Address block
]
```

*為什麼要使用 ROI？*  
- **速度** – 引擎會跳過圖像中不相關的部分。  
- **準確度** – 專注於小範圍，可避免其他雜訊干擾辨識器。  
- **彈性** – 可依需求加入任意數量的 ROI；引擎會依相同順序回傳結果清單。

---

## 第四步 – 如何設定前處理以提升 OCR 準確度

掃描器或手機直接拍攝的圖像常常會出現傾斜、對比低或光線不均。Aspose OCR 提供 `PreprocessingOptions` 物件，讓你在辨識前啟用常見的修正功能。

```python
from aspose.ocr import PreprocessingOptions

preprocessing_options = PreprocessingOptions()
preprocessing_options.deskew = True          # Auto‑rotate tilted text
preprocessing_options.binarize = True        # Convert to black‑white for clarity
preprocessing_options.contrast = 1.5         # Boost contrast (1.0 = no change)
```

*這樣做的好處*：  
- **Deskew** 會去除使字形模糊的傾斜。  
- **Binarize** 會降低顏色雜訊，將圖像轉為乾淨的二值圖。  
- **Contrast** 會放大淡淡的筆劃，對於褪色的收據特別有用。

你可以自行實驗這些旗標——關閉其中一項，觀察輸出是否改變。這就是 **how to set preprocessing** 的精髓。

---

## 第五步 – 僅在已定義的 ROI 內執行 OCR

當引擎、圖像、ROI 以及前處理都備妥後，就可以呼叫 `recognize`。此方法會回傳一個 `OcrResult` 物件，其中的 `regions` 集合與我們提供的 ROI 順序相對應。

```python
ocr_result = ocr_engine.recognize(
    source_image,
    rois=regions_of_interest,
    preprocessing=preprocessing_options
)
```

*背後原理*：引擎會依序裁切每個 ROI，套用前處理管線，然後在清理過的片段上執行辨識模型。因為我們傳入的是清單，結果會保留相同順序，讓後續處理變得直觀。

---

## 第六步 – 讀取並使用抽取出的文字（How to OCR ROI）

最後，遍歷 `regions` 清單，將辨識出的字串印出或儲存。`Region` 物件提供 `text` 屬性，內含 Unicode 結果。

```python
for idx, region in enumerate(ocr_result.regions, start=1):
    print(f"Region {idx} text:")
    print(region.text)
    print("-" * 40)
```

**預期輸出（範例）**：

```
Region 1 text:
John Doe
----------------------------------------
Region 2 text:
123 Maple Street
Springfield, IL 62704
----------------------------------------
```

如果文字看起來亂碼，請回顧 **how to set preprocessing**：或許需要提升 `contrast`，或對彩色標誌關閉 `binarize`。

---

## 常見問題與進階小技巧

| 問題 | 為何會發生 | 解決方式（How to Set Preprocessing） |
|------|------------|--------------------------------------|
| 傾斜文字變成亂碼 | `deskew` 未啟用或圖像旋轉過度 | 設定 `preprocessing_options.deskew = True` |
| 數字變成點或雜訊 | 對比過低或二值化過度 | 降低 `contrast`（例如 `1.2`）或將 `binarize = False` |
| ROI 座標少了幾個像素 | DPI 不同或掃描器比例不同 | 使用工具（如 Paint.NET）測量精確像素，或在每個 ROI 加上小幅邊界（`+5` 像素） |
| 某區域回傳空結果 | ROI 超出圖像範圍 | 檢查圖像尺寸：`source_image.width`, `source_image.height` |

---

## 延伸應用（How to OCR ROI in Different Scenarios）

- **動態 ROI**：若發票版面多變，可先執行一次全頁 OCR，找出關鍵字（例如 “Customer:”、 “Address:”），再即時計算 ROI。  
- **批次處理**：將上述步驟封裝成函式，對資料夾內的多張圖像迴圈處理。記得重複使用同一個 `ocr_engine` 實例，以降低記憶體使用。  
- **匯出 JSON**：與其直接印出，不如建立字典並使用 `json.dumps` 序列化；這樣可輕鬆串接 ERP 系統等下游應用。

```python
import json

def extract_invoice_fields(image_path):
    img = storage.Image.load(image_path)
    result = ocr_engine.recognize(
        img,
        rois=regions_of_interest,
        preprocessing=preprocessing_options
    )
    data = {f"field_{i+1}": r.text.strip() for i, r in enumerate(result.regions)}
    return data

print(json.dumps(extract_invoice_fields("invoice.png"), indent=2))
```

---

## 結論

現在你已掌握一個完整、可直接執行的範例，示範 **how to OCR ROI** 同時 **how to set preprocessing** 以取得最佳準確度。透過限制引擎只處理你關心的矩形，並在辨識前先清理圖像，你能得到更快、更乾淨的結果——非常適合發票自動化、表單數位化，或任何只需要頁面局部資訊的情境。

準備好下一步了嗎？試著為不同文件類型調整 ROI 座標，或探索額外的前處理旗標，如 `sharpen` 或 `noise_reduction`。Aspose OCR 的彈性讓你可以針對幾乎任何圖像品質自行調整管線。

若遇到問題，請檢查主控台輸出是否有空的區域，並重新檢視前處理設定。祝程式開發順利，OCR 準確率節節高升！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}