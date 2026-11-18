---
category: general
date: 2026-04-26
description: 如何對 OCR 結果進行後處理並提取帶坐標的文字。學習使用結構化輸出和 AI 校正的逐步解決方案。
draft: false
keywords:
- how to post‑process OCR
- extract text with coordinates
- OCR structured output
- AI post‑processing OCR
- bounding box OCR
language: zh-hant
og_description: 如何後處理 OCR 結果並提取帶座標的文字。請跟隨本完整教學，獲得可靠的工作流程。
og_title: 如何進行 OCR 後處理 – 完整指南
tags:
- OCR
- Python
- AI
- Text Extraction
title: 如何對 OCR 進行後處理 — 使用 Python 提取帶座標的文字
url: /zh-hant/python/general/how-to-post-process-ocr-extract-text-with-coordinates-in-pyt/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何後處理 OCR – 在 Python 中提取帶座標的文字

有沒有曾經需要 **如何後處理 OCR** 結果，因為原始輸出雜訊太多或對齊不正確？你並不是唯一遇到這種情況的人。在許多實際專案中——發票掃描、收據數位化，甚至增強 AR 體驗——OCR 引擎會給你原始文字，但你仍需清理它們並追蹤每個字在頁面上的位置。這時結合結構化輸出模式與 AI 驅動的後處理器就能大顯身手。

在本教學中，我們將逐步說明一個完整且可執行的 Python 流程，**從影像中提取帶座標的文字**，執行 AI 基礎的校正步驟，並列印每個字以及其 (x, y) 位置。沒有缺少的匯入，也沒有模糊的「請參考文件」捷徑——只是一個可直接放入你專案的獨立解決方案。

> **小技巧：** 如果你使用的是其他 OCR 函式庫，請尋找「structured」或「layout」模式；概念保持不變。

---

## 前置條件

在深入之前，請確保你已具備以下條件：

| 需求 | 為何重要 |
|-------------|----------------|
| Python 3.9+ | 現代語法與型別提示 |
| `ocr` library that supports `OutputMode.STRUCTURED` (e.g., a fictional `myocr`) | 用於取得邊界框資料 |
| An AI post‑processing module (could be OpenAI, HuggingFace, or a custom model) | 提升 OCR 後的準確度 |
| An image file (`input.png`) in your working directory | 我們將讀取的來源 |

如果上述項目對你來說陌生，只需使用 `pip install myocr ai‑postproc` 安裝佔位套件。以下程式碼也包含備用存根，讓你在沒有實際函式庫的情況下測試流程。

## 步驟 1：為 OCR 引擎啟用結構化輸出模式  

我們首先要告訴 OCR 引擎提供的不僅是純文字。結構化輸出會回傳每個字以及其邊界框與信心分數，這對於之後的 **提取帶座標的文字** 至關重要。

```python
# step1_structured_output.py
import myocr as ocr  # fictional OCR library

# Initialize the engine (replace with your actual init code)
engine = ocr.Engine()

# Switch to structured mode – this makes the engine emit word‑level data
engine.set_output_mode(ocr.OutputMode.STRUCTURED)

print("✅ Structured output mode enabled")
```

*為何重要：* 若未使用結構化模式，你只能得到一長串文字，且會失去在影像上疊加文字或供下游版面分析所需的空間資訊。

## 步驟 2：辨識影像並擷取文字、框框與信心分數  

現在我們將影像送入引擎。結果是一個物件，內含一系列字物件，每個字物件提供 `text`、`x`、`y`、`width`、`height` 與 `confidence`。

```python
# step2_recognize.py
from pathlib import Path

# Path to your image
image_path = Path("YOUR_DIRECTORY/input.png")

# Perform OCR – returns a StructuredResult with .words collection
structured_result = engine.recognize_image(str(image_path))

print(f"🔎 Detected {len(structured_result.words)} words")
```

*邊緣情況：* 若影像為空或無法讀取，`structured_result.words` 會是空列表。建議先檢查並妥善處理此情況。

## 步驟 3：在保留位置的同時執行 AI 基礎的後處理  

即使是最佳的 OCR 引擎也會出錯——例如「O」與「0」混淆或缺少變音符號。針對特定領域文字訓練的 AI 模型能校正這些錯誤。關鍵是，我們保留原始座標，使空間版面保持完整。

```python
# step3_ai_postprocess.py
import ai_postproc as ai  # placeholder for your AI module

# The AI post‑processor expects the structured result and returns a new one
corrected_result = ai.run_postprocessor(structured_result)

print("🤖 AI post‑processing complete")
```

*為何保留座標：* 許多下游任務（例如 PDF 產生、AR 標註）依賴精確的放置。AI 僅修改 `text` 欄位，`x`、`y`、`width`、`height` 保持不變。

## 步驟 4：遍歷校正後的文字並顯示其座標  

最後，我們遍歷校正後的文字，將每個字與其左上角 `(x, y)` 一起印出。這即達成 **提取帶座標的文字** 目標。

```python
# step4_display.py
for recognized_word in corrected_result.words:
    # Using f‑string for clean formatting
    print(f"{recognized_word.text} (x:{recognized_word.x}, y:{recognized_word.y})")
```

**預期輸出（範例）：**

```
Invoice (x:45, y:112)
Number (x:120, y:112)
12345 (x:190, y:112)
Total (x:45, y:250)
$ (x:120, y:250)
199.99 (x:130, y:250)
```

每一行顯示校正後的文字以及其在原始影像上的精確位置。

## 完整可執行範例  

以下是一個將所有步驟串接的單一腳本。你可以直接複製貼上，依實際使用的函式庫調整匯入語句，然後直接執行。

```python
# ocr_postprocess_demo.py
"""
Complete demo: how to post‑process OCR and extract text with coordinates.
Works with any OCR library exposing a structured output mode and an AI post‑processor.
"""

import sys
from pathlib import Path

# ----------------------------------------------------------------------
# 1️⃣ Imports – replace these with your real packages
# ----------------------------------------------------------------------
try:
    import myocr as ocr               # OCR engine with structured output
    import ai_postproc as ai          # AI correction module
except ImportError:  # Fallback stubs for quick testing
    class DummyWord:
        def __init__(self, text, x, y, w, h, conf):
            self.text = text
            self.x = x
            self.y = y
            self.width = w
            self.height = h
            self.confidence = conf

    class DummyResult:
        def __init__(self, words):
            self.words = words

    class StubEngine:
        class OutputMode:
            STRUCTURED = "structured"

        def set_output_mode(self, mode):
            print(f"[Stub] set_output_mode({mode})")

        def recognize_image(self, path):
            # Very simple fake OCR output
            sample = [
                DummyWord("Invoice", 45, 112, 60, 20, 0.98),
                DummyWord("Number", 120, 112, 55, 20, 0.96),
                DummyWord("12345", 190, 112, 40, 20, 0.97),
                DummyWord("Total", 45, 250, 50, 20, 0.99),
                DummyWord("$", 120, 250, 10, 20, 0.95),
                DummyWord("199.99", 130, 250, 55, 20, 0.94),
            ]
            return DummyResult(sample)

    class StubAI:
        @staticmethod
        def run_postprocessor(structured_result):
            # Pretend we corrected "12345" to "12346"
            for w in structured_result.words:
                if w.text == "12345":
                    w.text = "12346"
            return structured_result

    engine = StubEngine()
    ai = StubAI

# ----------------------------------------------------------------------
# 2️⃣ Enable structured output
# ----------------------------------------------------------------------
engine.set_output_mode(ocr.Engine.OutputMode.STRUCTURED)

# ----------------------------------------------------------------------
# 3️⃣ Recognize image
# ----------------------------------------------------------------------
image_path = Path("YOUR_DIRECTORY/input.png")
if not image_path.is_file():
    print(f"⚠️  Image not found at {image_path}. Using stub data.")
structured_result = engine.recognize_image(str(image_path))

# ----------------------------------------------------------------------
# 4️⃣ AI post‑processing
# ----------------------------------------------------------------------
corrected_result = ai.run_postprocessor(structured_result)

# ----------------------------------------------------------------------
# 5️⃣ Display results
# ----------------------------------------------------------------------
print("\n🗒️  Final OCR output with coordinates:")
for word in corrected_result.words:
    print(f"{word.text} (x:{word.x}, y:{word.y})")
```

**執行腳本**

```bash
python ocr_postprocess_demo.py
```

若已安裝真實函式庫，腳本會處理你的 `input.png`。否則，存根實作讓你在不需任何外部依賴的情況下看到預期的流程與輸出。

## 常見問題 (FAQ)

| 問題 | 答案 |
|----------|--------|
| *這能在 Tesseract 上使用嗎？* | Tesseract 本身不直接提供結構化模式，但像 `pytesseract.image_to_data` 這樣的封裝會回傳邊界框，你可以將其餵入相同的 AI 後處理器。 |
| *如果我需要右下角而不是左上角怎麼辦？* | 每個字物件也提供 `width` 與 `height`。計算 `x2 = x + width` 與 `y2 = y + height` 即可取得相對的角落。 |
| *我可以批次處理多張影像嗎？* | 當然可以。將步驟包在 `for image_path in Path("folder").glob("*.png"):` 迴圈中，並為每個檔案收集結果。 |
| *我要如何選擇校正用的 AI 模型？* | 對於一般文字，可使用在 OCR 錯誤上微調的輕量 GPT‑2。若是特定領域資料（例如醫療處方），則可在噪聲‑乾淨配對資料上訓練序列對序列模型。 |
| *AI 校正後信心分數仍有用嗎？* | 仍可保留原始信心分數以供除錯，但若模型支援，AI 也可能輸出自己的信心分數。 |

## 邊緣情況與最佳實踐  

1. **空的或損毀的影像** – 在繼續之前務必確認 `structured_result.words` 非空。  
2. **非拉丁文字** – 確保 OCR 引擎已為目標語言設定；AI 後處理器也必須在相同文字上訓練。  
3. **效能** – AI 校正可能成本高。若會重複使用同一影像，請快取結果，或以非同步方式執行 AI 步驟。  
4. **座標系統** – OCR 函式庫可能使用不同的原點（左上或左下）。在 PDF 或畫布上疊加時請相應調整。  

## 結論  

現在你已掌握一套完整、可靠的 **如何後處理 OCR** 與 **提取帶座標的文字** 的流程。透過啟用結構化輸出、將結果送入 AI 校正層，並保留原始邊界框，你可以將雜訊多的 OCR 掃描轉換為乾淨且具空間感的文字，供 PDF 產生、資料輸入自動化或擴增實境標註等下游任務使用。

準備好進一步了嗎？試著將存根 AI 換成 OpenAI `gpt‑4o‑mini` 呼叫，或將此流程整合至 FastAPI 中。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}