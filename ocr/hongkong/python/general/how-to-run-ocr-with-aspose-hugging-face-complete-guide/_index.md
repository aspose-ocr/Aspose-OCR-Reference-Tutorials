---
category: general
date: 2026-04-29
description: 學習如何對掃描檔執行 OCR，自動使用 Hugging Face 模型，並在數分鐘內使用 Aspose OCR 辨識掃描文字。
draft: false
keywords:
- how to run OCR
- use hugging face model
- recognize text from scans
- download model automatically
language: zh-hant
og_description: 如何使用 Aspose OCR 於掃描檔執行 OCR，自動下載 Hugging Face 模型，並取得乾淨且有標點的文字。
og_title: 如何使用 Aspose 與 Hugging Face 進行 OCR – 完整指南
tags:
- OCR
- Aspose
- Hugging Face
- Python
title: 如何使用 Aspose 與 Hugging Face 執行 OCR – 完整指南
url: /zh-hant/python/general/how-to-run-ocr-with-aspose-hugging-face-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose 與 Hugging Face 執行 OCR – 完整指南

有沒有想過 **如何在一堆掃描文件上執行 OCR**，卻不需要花上數小時調整設定？你並不孤單。在許多專案中，開發者需要快速 **從掃描中辨識文字**，卻常因模型下載與後處理卡關。

好消息：本教學示範一個即開即用的解決方案，**使用 Hugging Face 模型**，自動下載，並加入標點符號，使輸出看起來像是人類寫的。完成後，你將擁有一支腳本，能處理資料夾內的每張圖片，並在每個掃描檔旁產生乾淨的 `.txt` 檔案。

## 需要的環境

- Python 3.8+（程式碼使用 f‑string，較舊版本無法執行）
- `aspose-ocr` 套件（透過 `pip install aspose-ocr` 安裝）
- 首次下載模型時需要網路連線  
- 一個放置影像掃描檔的資料夾（`.png`、`.jpg` 或 `.tif`）

就這些——不需要額外的二進位檔，也不需要手動調整模型。現在就開始吧。

![如何執行 OCR 示例](https://example.com/ocr-demo.png "如何執行 OCR 示例")

## 步驟 1：匯入 Aspose OCR 類別並設定環境

我們先從 Aspose OCR 函式庫中匯入必要的類別。一次匯入全部可以讓腳本保持整潔，也方便快速發現缺少的相依性。

```python
# Step 1: Import Aspose OCR classes
import os
from aspose.ocr import OcrEngine, AsposeAI, AsposeAIModelConfig
```

*為什麼這很重要*：`OcrEngine` 負責主要的文字辨識工作，而 `AsposeAI` 讓我們能接入大型語言模型，以進行更智慧的後處理。如果省略匯入，後續程式碼根本無法編譯——千萬別忘了。

## 步驟 2：設定支援 GPU 的 Hugging Face 模型  

現在告訴 Aspose 從哪裡取得模型，以及有多少層要在 GPU 上執行。`allow_auto_download="true"` 旗標會自動為你 **下載模型**。

```python
# Step 2: Configure a GPU‑aware AI model (replace with your own model folder)
model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=40,                     # use GPU for faster inference
    directory_model_path=r"YOUR_DIRECTORY/models"
)
```

> **小技巧**：若沒有 GPU，將 `gpu_layers=0`。模型會回退到 CPU，速度較慢但仍可正常運作。

### 為什麼選擇 Hugging Face 模型？

Hugging Face 提供大量即用的 LLM。指向 `Qwen/Qwen2.5-3B-Instruct-GGUF` 後，你會得到一個小型、指令微調的模型，能加入標點、校正空格，甚至修正少量 OCR 錯誤。這正是 **使用 Hugging Face 模型** 的實際效益。

## 步驟 3：初始化 AI 引擎並啟用標點後處理  

AI 引擎不只是用來聊天——在這裡我們掛上 *標點添加器*，把原始 OCR 輸出清理乾淨。

```python
# Step 3: Initialise the AI engine and enable punctuation post‑processing
ai_engine = AsposeAI()
ai_engine.set_post_processor("punctuation_adder", {})
```

*發生了什麼事？* `set_post_processor` 會註冊內建的後處理器，於 OCR 引擎完成後執行。它會把原始字串插入逗號、句號與大寫字母，使最終文字更易閱讀。

## 步驟 4：建立 OCR 引擎並掛上 AI 引擎  

將 AI 引擎連結到 OCR 引擎，我們就得到一個同時能讀取字元與潤飾結果的單一物件。

```python
# Step 4: Create the OCR engine and attach the AI engine
ocr_engine = OcrEngine()
ocr_engine.set_ai_engine(ai_engine)
```

如果跳過此步驟，OCR 仍能運作，但會失去標點增強——輸出會變成一長串沒有標點的文字。

## 步驟 5：處理資料夾內的每張影像  

以下是本教學的核心。我們會遍歷每張影像、執行 OCR、套用後處理，最後把清理過的文字寫入同名的 `.txt` 檔案。

```python
# Step 5: Run OCR on each image in a folder, post‑process the result, and save the text
scans_folder = r"YOUR_DIRECTORY/scans"
for image_file in os.listdir(scans_folder):
    # Filter only supported image types
    if not image_file.lower().endswith(('.png', '.jpg', '.tif')):
        continue

    image_path = os.path.join(scans_folder, image_file)

    # Recognise text from the image
    ocr_result = ocr_engine.recognize(image_path)

    # Apply the punctuation post‑processor
    ocr_result = ocr_engine.run_postprocessor(ocr_result)

    # Show a brief confidence summary
    print(f"{image_file} – confidence {ocr_result.confidence:.2%}")

    # Save the cleaned text next to the source image
    txt_path = image_path + ".txt"
    with open(txt_path, "w", encoding="utf-8") as txt_file:
        txt_file.write(ocr_result.text)
```

### 預期結果

執行腳本時會印出類似以下的資訊：

```
invoice_001.png – confidence 96.73%
receipt_2024.tif – confidence 94.12%
```

每一行會顯示信心分數（快速健康檢查），並產生 `invoice_001.png.txt`、`receipt_2024.tif.txt` 等檔案，內含已加標點、可供人閱讀的文字。

### 邊緣案例與變化

- **非英文掃描**：將 `hugging_face_repo_id` 改為多語言模型（例如 `microsoft/Multilingual-LLM-GGUF`）。
- **大量批次**：將迴圈包在 `concurrent.futures.ThreadPoolExecutor` 中以平行處理，但需留意 GPU 記憶體上限。
- **自訂後處理**：若需要領域特定的清理（例如移除發票號碼），可將 `"punctuation_adder"` 換成自訂腳本。

## 步驟 6：釋放資源  

工作結束後釋放資源可防止記憶體洩漏，特別是當你在長時間服務中執行此程式時。

```python
# Step 6: Release resources
ai_engine.free_resources()
ocr_engine.dispose()
```

忽略此步驟可能會讓 GPU 記憶體卡住，進而影響後續執行。

## 小結：完整的 OCR 流程  

只需幾行程式碼，我們就示範了 **如何在資料夾內的掃描文件上執行 OCR**、**使用會自動下載的 Hugging Face 模型**，以及 **自動加入標點的文字辨識**。完整腳本已可直接複製、調整路徑後執行。

## 後續步驟與相關主題  

- **批次後處理**：探索 `ocr_engine.run_batch_postprocessor` 以加速大量處理。  
- **替代模型**：若需要語音轉文字，可嘗試 `openai/whisper` 系列。  
- **與資料庫整合**：將擷取的文字存入 SQLite 或 Elasticsearch，打造可搜尋的檔案庫。  

盡情實驗吧——換模型、調整 `gpu_layers`，或加入自訂後處理器。Aspose OCR 結合 Hugging Face 模型中心的彈性，讓它成為任何文件數位化專案的多功能基礎。

---

*祝開發順利！若遇到問題，歡迎在下方留言或查閱 Aspose OCR 文件，了解更深入的設定選項。*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}