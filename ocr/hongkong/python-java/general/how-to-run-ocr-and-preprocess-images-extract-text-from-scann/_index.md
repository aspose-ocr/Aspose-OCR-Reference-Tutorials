---
category: general
date: 2026-04-26
description: 如何對掃描表格執行 OCR，學習如何預處理圖像以減少雜訊，並快速從圖像中提取文字。
draft: false
keywords:
- how to run OCR
- how to preprocess image
- extract text from image
- how to extract text
- how to reduce noise
language: zh-hant
og_description: 如何在掃描文件上執行 OCR，預處理圖像、降低噪點，並高效提取文字。
og_title: 如何執行 OCR 與圖像前處理 – 快速指南
tags:
- OCR
- image processing
- Python
title: 如何執行 OCR 及圖像預處理 – 從掃描表格提取文字
url: /zh-hant/python-java/general/how-to-run-ocr-and-preprocess-images-extract-text-from-scann/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何執行 OCR – 完整的圖像文字提取指南

有沒有想過 **如何執行 OCR** 在雜亂的掃描表格上，並取得乾淨、可搜尋的文字？你並非唯一有此疑問的人。在許多實務專案中，原始影像充斥斑點、光線不均以及其他會讓即時 OCR 表現不佳的因素。  

好消息是？只需幾行 Python 程式碼加上一條聰明的前處理流程，即可大幅提升辨識準確度、**降低雜訊**，並抽取出你需要的精確文字。在本教學中，我們會逐步說明每個步驟——從載入圖片到印出最終字串——讓你得到一段可直接套用的程式碼，能夠應用於發票、收據或任何掃描文件。

## 你將建立的功能

- 一個與底層 OCR 函式庫互動的 `OcrEngine` 實例。  
- 一條前處理鏈，**二值化**影像並套用 **中值模糊** 以平滑斑點。  
- 一個簡單的 `process()` 呼叫，回傳包含 `text`（即抽取字串）的物件。  

完成後，你將擁有一個獨立的腳本，能在任何影像檔上執行，並立即在主控台顯示抽取出的文字。

## 前置條件

- Python 3.9+（此處使用的語法符合最新穩定版）。  
- 虛構的 `aocr` 套件——可視為 Tesseract 或其他現代 OCR 引擎的輕量包裝。使用 `pip install aocr` 安裝。  
- 一張掃描圖像（`scanned_form.jpg`），放在可供參照的資料夾中。  

如果你使用的是實際的 OCR 函式庫，例如 `pytesseract`，只要將 `OcrEngine` 換成相應的類別，其他程式碼皆保持不變。

![](how-to-run-ocr-example.png "how to run OCR example showing a scanned form and extracted text")

*Alt text: 在掃描文件上執行 OCR 並檢視抽取文字的示例。*

---

## 步驟 1：如何執行 OCR – 初始化引擎

在引擎能讀取任何內容之前，我們必須先建立實例。把 `OcrEngine` 想像成之後會解讀視覺資料的大腦。

```python
# Step 1: Create an OCR engine instance
ocr_engine = OcrEngine()
```

> **為什麼這很重要：** 建立引擎實例會設定內部模型、載入語言套件，並準備執行環境。若跳過此步驟，之後呼叫 `process()` 時通常會出現 `NoneType` 錯誤。

---

## 步驟 2：如何前處理影像 – 載入掃描表單

大腦已就緒，我們將圖片餵入。影像可以是 `aocr.Image` 支援的任何格式。

```python
# Step 2: Load the image you want to recognize
ocr_engine.image = aocr.Image.load("YOUR_DIRECTORY/scanned_form.jpg")
```

> **專業提示：** 開發時使用絕對路徑，可避免腳本在不同工作目錄執行時出現「找不到檔案」的意外。

---

## 步驟 3：如何降低雜訊 – 套用二值化與中值模糊

原始掃描常會有雜散點、背景不均或淡淡陰影。兩個經典技巧——**二值化**與**中值模糊**——能在不犧牲字元邊緣的前提下清理影像。

```python
# Step 3: Pre‑process the image to improve recognition accuracy
# • Binarize converts the image to black‑and‑white using a threshold
# • Median blur reduces noise while preserving edges
ocr_engine.image = ocr_engine.image.apply_filters(
    aocr.ImageFilters.binarize(threshold=180),
    aocr.ImageFilters.median_blur(radius=2)
)
```

### 深入探討

- **二值化**：`threshold=180` 參數告訴演算法「亮度高於 180 的像素變成白色，其他則變成黑色」。若掃描過暗或過亮，可調整此數值。  
- **中值模糊**：半徑 `2` 表示濾波器會檢視 5×5 像素的視窗，並以中位數取代中心像素。此方式可平滑孤立斑點，同時保留字母筆畫。  

> **邊緣情況：** 若文件有彩色標記，簡單的二值閾值可能會將其抹除。此時可考慮改用 `aocr.ImageFilters.adaptive_threshold()`——它會在影像上局部調整閾值。

---

## 步驟 4：如何抽取文字 – 執行 OCR 程序

取得乾淨的影像後，我們終於讓引擎發揮魔法。

```python
# Step 4: Run the OCR process on the prepared image
ocr_result = ocr_engine.process()
```

> **背後發生什麼？** 引擎會在像素矩陣上運行神經網路（或傳統的模式匹配器），將每個辨識出的字形轉換為 Unicode 字元，並組合成行與段落。

---

## 步驟 5：如何抽取文字 – 輸出結果

`ocr_result` 物件提供方便的 `text` 屬性。讓我們看看得到什麼。

```python
# Step 5: Print the extracted text
print(ocr_result.text)
```

### 預期輸出

如果掃描的表單內容為：

```
Name: Jane Doe
Date: 2024-04-24
Amount: $123.45
```

你應該會看到類似以下的結果：

```
Name: Jane Doe
Date: 2024-04-24
Amount: $123.45
```

請注意，前處理步驟消除了原本會把 “Amount” 變成 “Am0unt” 的雜散點。這正是 **在 OCR 前降低雜訊** 的威力所在。

---

## 常見問題與解決方法

| 症狀 | 可能原因 | 快速解決方案 |
|---------|--------------|-----------|
| 亂碼（例如 “@#%”） | 影像過暗或過亮 | 微調 `binarize()` 中的 `threshold`；嘗試 `adaptive_threshold`。 |
| 遺漏文字 | 雜訊仍然存在 | 增加 `median_blur` 的 `radius`，或加入 `gaussian_blur` 濾鏡。 |
| 語言錯誤（例如英文字母變成中文） | 載入了錯誤的語言套件 | 在建立 `OcrEngine()` 時傳入 `language="eng"`（若函式庫支援）。 |
| 大型檔案處理緩慢 | 解析度過高 | 先縮小影像：在二值化前使用 `aocr.ImageFilters.resize(width=1200)`。 |

---

## 更進一步 – 後續步驟與相關主題

- **批次處理**：將上述邏輯包在迴圈中，以自動處理數十個檔案。  
- **結構化輸出**：使用正規表達式於 `ocr_result.text` 取得日期、金額等欄位。  
- **替代函式庫**：將 `aocr` 換成 `pytesseract`——程式碼僅在引擎初始化步驟有所變化。  
- **如何為 PDF 前處理影像**：將每頁 PDF 轉為影像，然後套用相同的流程。  

這些延伸功能可讓你將解決方案從單一表單擴展至企業級的文件擷取管線。

---

## 結論

我們已完整說明 **如何執行 OCR**，展示 **如何前處理影像** 以 **降低雜訊**，並以乾淨、可重現的腳本示範 **如何從影像抽取文字**。關鍵是什麼？只要使用二值化與中值模糊這兩個簡單濾鏡，即可將雜訊掃描轉為可靠的資料來源，為你節省大量手動清理的時間。

把腳本套用到自己的文件上，調整閾值，觀察準確度提升。當你準備好時，可探索批次處理或將輸出整合至資料庫，以建立可搜尋的檔案庫。祝編程愉快，願你的 OCR 永遠精準！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}