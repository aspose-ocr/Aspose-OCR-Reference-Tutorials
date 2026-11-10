---
category: general
date: 2026-05-03
description: 如何使用 Aspose OCR 與 AI 拼寫檢查批次處理圖片。學習從圖片提取文字、套用拼寫檢查、使用免費 AI 資源及校正 OCR 錯誤。
draft: false
keywords:
- how to batch ocr
- extract text from images
- free ai resources
- apply spell check
- correct ocr errors
language: zh-hant
og_description: 如何使用 Aspose OCR 與 AI 拼寫檢查批次處理圖片文字辨識。跟隨一步一步的指南，從圖片中提取文字、套用拼寫檢查、使用免費
  AI 資源，並校正 OCR 錯誤。
og_title: 如何使用 Aspose OCR 進行批次 OCR – 完整 Python 教學
tags:
- OCR
- Python
- AI
- Aspose
title: 如何使用 Aspose OCR 進行批次 OCR – 完整 Python 指南
url: /zh-hant/python/general/how-to-batch-ocr-with-aspose-ocr-full-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose OCR 進行批次 OCR – 完整 Python 教學

有沒有想過 **如何批次 OCR** 整個資料夾的掃描 PDF 或相片，而不必為每個檔案寫一個獨立腳本？你並不孤單。在許多實務工作流程中，你需要 **從影像中擷取文字**、修正拼寫錯誤，最後釋放已分配的 AI 資源。本教學將一步步示範如何使用 Aspose OCR（輕量級 AI 後處理器）以及幾行 Python 程式碼完成這些工作。

我們會說明如何初始化 OCR 引擎、掛接 AI 拼寫檢查器、遍歷圖片目錄，並在最後清理模型。完成後，你將擁有一個可直接執行的腳本，能 **自動校正 OCR 錯誤** 並釋放 **免費的 AI 資源**，讓 GPU 保持順暢。

## 需要的環境

- Python 3.9+（程式碼使用型別提示，但在較早的 3.x 版本亦可執行）
- `asposeocr` 套件（`pip install asposeocr`）– 提供 OCR 引擎
- 取得 Hugging Face 模型 `bartowski/Qwen2.5-3B-Instruct-GGUF`（會自動下載）
- 具備至少數 GB VRAM 的 GPU（腳本預設 `gpu_layers = 30`，如有需要可降低）

不需要外部服務，也不需要付費 API – 全部在本機執行。

---

## 步驟 1：設定 OCR 引擎 – **如何有效率地批次 OCR**

在處理上千張圖片之前，我們需要一個穩固的 OCR 引擎。Aspose OCR 讓我們在一次呼叫中選擇語言與辨識模式。

```python
# Step 1: Initialize the OCR engine for English plain‑text output
def init_ocr() -> aocr.OcrEngine:
    ocr_engine = aocr.OcrEngine()
    ocr_engine.language = aocr.Language.English          # English language pack
    ocr_engine.recognize_mode = aocr.RecognitionMode.Plain  # Returns raw string, no layout
    return ocr_engine
```

**為什麼這很重要：** 將 `recognize_mode` 設為 `Plain` 可讓輸出保持輕量，這在之後要執行拼寫檢查時非常理想。若需要版面資訊，可改為 `Layout`，但會增加不必要的負擔，對批次作業而言不太適合。

> **小技巧：** 若要處理多語言掃描，可傳入類似 `ocr_engine.language = [aocr.Language.English, aocr.Language.Spanish]` 的清單。

---

## 步驟 2：初始化 AI 後處理器 – **對 OCR 輸出套用拼寫檢查**

Aspose AI 內建可自行掛載的後處理器，我們從 Hugging Face 下載量化版 Qwen 2.5 模型，並將拼寫檢查流程掛上。

```python
# Step 2: Configure and start the AI post‑processor
def init_ai() -> aocr.ai.AsposeAI:
    model_cfg = AsposeAIModelConfig()
    model_cfg.allow_auto_download = "true"
    model_cfg.hugging_face_repo_id = "bartowski/Qwen2.5-3B-Instruct-GGUF"
    model_cfg.hugging_face_quantization = "q4_k_m"
    model_cfg.gpu_layers = 30          # Adjust based on your GPU memory
    ai_processor = AsposeAI()
    ai_processor.initialize(model_cfg)

    # Attach the built‑in spell‑check post‑processor
    ai_processor.set_post_processor(ai_processor.postprocessor_spell_check, {})
    return ai_processor
```

**為什麼這很重要：** 模型已量化為 `q4_k_m`，可大幅降低記憶體使用量，同時仍保有不錯的語言理解能力。呼叫 `set_post_processor` 後，Aspose AI 會自動在任何傳入的字串上執行 **apply spell check** 步驟。

> **注意：** 若 GPU 無法支援 30 層，請將數值降至 15 或甚至 5 – 腳本仍能運作，只是速度會稍慢。

---

## 步驟 3：對單張圖片執行 OCR 並 **校正 OCR 錯誤**

OCR 引擎與 AI 拼寫檢查器都準備好後，我們將它們結合。此函式會載入圖片、擷取原始文字，然後使用 AI 後處理器進行清理。

```python
# Step 3: OCR an image and run the spell‑check post‑processor
def ocr_and_correct(image_path: str,
                    ocr_engine: aocr.OcrEngine,
                    ai_processor: aocr.ai.AsposeAI) -> str:
    image = aocr.Image.load(image_path)               # Load any supported format
    raw_text = ocr_engine.recognize(image)           # Plain string from OCR
    corrected_text = ai_processor.run_postprocessor(raw_text)
    return corrected_text
```

**為什麼這很重要：** 直接把原始 OCR 文字送入 AI 模型，即可完成 **校正 OCR 錯誤** 的工作，無需自行撰寫正則表達式或自訂字典。模型具備上下文感知能力，能把 “recieve” 修正為 “receive”，甚至更微妙的錯誤。

---

## 步驟 4：**大量擷取影像文字** – 真正的批次迴圈

這裡就是 **如何批次 OCR** 發揮威力的地方。我們遍歷目錄、略過不支援的檔案，並將每個校正後的結果寫入 `.txt` 檔。

```python
# Step 4: Process an entire folder of images
if __name__ == "__main__":
    # Initialize once – reuse for every file
    ocr_engine = init_ocr()
    ai_processor = init_ai()

    input_dir = "YOUR_DIRECTORY/input_images"
    output_dir = "YOUR_DIRECTORY/output_text"
    os.makedirs(output_dir, exist_ok=True)

    for file_name in os.listdir(input_dir):
        # Only handle common image extensions
        if not file_name.lower().endswith(('.png', '.jpg', '.jpeg', '.tif', '.tiff')):
            continue

        image_path = os.path.join(input_dir, file_name)
        corrected = ocr_and_correct(image_path, ocr_engine, ai_processor)

        txt_path = os.path.join(output_dir,
                                os.path.splitext(file_name)[0] + ".txt")
        with open(txt_path, "w", encoding="utf-8") as txt_file:
            txt_file.write(corrected)

        print(f"Processed {file_name}")

    # Step 5: Release **free AI resources** after the batch finishes
    ai_processor.free_resources()
```

### 預期輸出

若影像內的句子為 *“The quick brown fox jumps over the lazzy dog.”*，產生的文字檔會顯示：

```
The quick brown fox jumps over the lazy dog.
```

可以看到雙「z」已自動更正 – 這就是 AI 拼寫檢查的效果。

**為什麼這很重要：** 我們只 **建立一次** OCR 與 AI 物件，並重複使用，避免每處理一個檔案就重新載入模型。這是以規模化方式 **如何批次 OCR** 最有效的做法。

---

## 步驟 5：清理 – 正確 **釋放 AI 資源**

作業結束後，呼叫 `free_resources()` 會釋放 GPU 記憶體、CUDA 內容以及模型產生的暫存檔。

```python
# Step 5: Explicitly free GPU and model memory
ai_processor.free_resources()
```

若省略此步驟，GPU 可能會留下未釋放的記憶體，導致後續 Python 程式當機或耗盡 VRAM。把它想成批次工作中的「關燈」程序。

---

## 常見問題與額外技巧

| 問題 | 觀察現象 | 解決方式 |
|------|----------|----------|
| **記憶體不足** | GPU 在處理數十張圖片後崩潰 | 降低 `gpu_layers`，或改用 CPU（`model_cfg.gpu_layers = 0`） |
| **缺少語言套件** | OCR 回傳空字串 | 確認 `asposeocr` 版本已包含英文語言資料；必要時重新安裝 |
| **非影像檔案** | 腳本在偶發的 `.pdf` 上當機 | `if not file_name.lower().endswith(...)` 判斷已自動跳過 |
| **拼寫檢查未套用** | 輸出與原始 OCR 完全相同 | 確認在迴圈前已呼叫 `ai_processor.set_post_processor` |
| **批次速度慢** | 每張圖片耗時 >5 秒 | 第一次執行後將 `model_cfg.allow_auto_download = "false"`，避免每次都重新下載模型 |

**小技巧：** 若要 **擷取影像文字** 的語言不是英文，只需將 `ocr_engine.language` 改成對應的列舉值（例如 `aocr.Language.French`）。同樣的 AI 後處理器仍會執行拼寫檢查，但若想取得最佳效果，建議使用相同語言的模型。

---

## 重點回顧與後續步驟

我們已完整說明 **如何批次 OCR** 的全流程：

1. **初始化** 只輸出純文字的 OCR 引擎（英文）。  
2. **設定** AI 拼寫檢查模型，並將其綁定為後處理器。  
3. **執行** OCR，讓 AI **自動校正 OCR 錯誤**。  
4. **遍歷** 目錄，以批次方式 **擷取影像文字**。  
5. **釋放** AI 資源，結束工作。

接下來你可以：

- 將校正後的文字送入下游 NLP 流程（情感分析、實體抽取等）。  
- 以 `ai_processor.set_post_processor(your_custom_func, {})` 替換拼寫檢查，改為自訂摘要器。  
- 若 GPU 能同時處理多條串流，可使用 `concurrent.futures.ThreadPoolExecutor` 平行化資料夾迴圈。

---

## 結語

批次 OCR 不必是繁重的工作。結合 Aspose OCR 與輕量級 AI 模型，你即可得到一個 **一站式解決方案**，同時 **擷取影像文字**、**套用拼寫檢查**、**校正 OCR 錯誤**，並 **乾淨地釋放 AI 資源**。先在測試資料夾上跑跑腳本，依硬體調整 GPU 層數，即可在數分鐘內建置上線級別的流水線。

對模型微調、PDF 處理或整合至 Web 服務有任何疑問？歡迎在下方留言或於 GitHub 私訊我。祝開發順利，願你的 OCR 永遠精準！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}