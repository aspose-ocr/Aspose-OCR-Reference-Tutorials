---
category: general
date: 2026-07-05
description: 學習如何使用 Aspose AI 從 Hugging Face 載入模型，並設定 GPU 層以加快推論速度。完整的 Python 範例以及逐步說明。
draft: false
keywords:
- how to load model from hugging face
- set gpu layers
- Aspose AI configuration
- Python AI inference
- Hugging Face model loading
language: zh-hant
og_description: 如何使用 Aspose AI 從 Hugging Face 載入模型，並設定 GPU 層以獲得最佳效能。請參考此完整指南。
og_title: 如何使用 Aspose AI 從 Hugging Face 載入模型
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Learn how to load model from Hugging Face with Aspose AI and set GPU
    layers for faster inference. Full Python example with step‑by‑step explanation.
  headline: How to Load Model from Hugging Face with Aspose AI
  type: TechArticle
- description: Learn how to load model from Hugging Face with Aspose AI and set GPU
    layers for faster inference. Full Python example with step‑by‑step explanation.
  name: How to Load Model from Hugging Face with Aspose AI
  steps:
  - name: Create the Aspose AI configuration object
    text: '```python import aocr'
  - name: Tell Aspose AI how many layers should live on the GPU
    text: '```python # Step 2: set gpu layers – we’ll run the first 30 layers on the
      GPU cfg.gpu_layers = 30 ```'
  - name: Point to the Hugging Face repository
    text: '```python # Step 3: Specify the Hugging Face repo that holds the model
      cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF" ```'
  - name: Instantiate the Aspose AI engine
    text: '```python # Step 4: Create the engine instance ai = aocr.AsposeAI() ```'
  - name: Initialize the engine with the prepared config
    text: '```python # Step 5: Wire everything together ai.initialize(cfg) ```'
  - name: Verify that the GPU layers are active
    text: '```python # Step 6: Quick sanity check – print the active GPU layer count
      print("GPU layers active:", cfg.gpu_layers) ```'
  - name: Expected Output
    text: '``` GPU layers active: 30'
  type: HowTo
tags:
- Aspose AI
- Hugging Face
- GPU
title: 如何使用 Aspose AI 從 Hugging Face 載入模型
url: /zh-hant/python/general/how-to-load-model-from-hugging-face-with-aspose-ai/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose AI 從 Hugging Face 載入模型

有沒有想過在使用 Aspose AI 時 **如何從 Hugging Face 載入模型**？你並不是唯一有此疑問的人。在許多專案中，最大的阻礙往往是把遠端模型搬到本機 GPU 上，卻又不想抓狂。  

本指南將逐步說明如何從 Hugging Face 載入模型、**設定 GPU 層**，並驗證一切運作正常。完成後，你將擁有一段可重複使用的 Python 程式碼片段，能直接嵌入任何使用 Aspose AI 的應用程式。

> **快速回顧：** 我們會建立一個設定物件，指向 Hugging Face 的倉庫，告訴 Aspose AI 要在 GPU 上執行多少層，最後啟動引擎。沒有神祕，只是清晰的程式碼。

## 前置條件

在深入之前，請確保你已具備：

* Python 3.8 + 已安裝。  
* `aocr` 套件（Aspose OCR/AI）— 透過 `pip install aocr` 安裝。  
* 支援 CUDA 的 GPU（非必須，但強烈建議以提升速度）。  
* 可連網路，以便從 Hugging Face 下載模型。  

如果缺少任何項目，請立即取得——本教學其餘部分皆假設已具備這些條件。

## 如何使用 Aspose AI 從 Hugging Face 載入模型

**如何從 Hugging Face 載入模型** 的核心只需三行簡短程式碼。讓我們逐一說明。

### 步驟 1：建立 Aspose AI 設定物件

```python
import aocr

# Step 1: Build a fresh configuration container
cfg = aocr.AsposeAIModelConfig()
```

*為什麼這很重要：* `AsposeAIModelConfig` 物件是引擎所需資訊的唯一來源——模型路徑、GPU 設定、分詞器選項，樣樣皆在其中。從乾淨的設定開始，可避免前一次執行遺留的隱藏狀態。

### 步驟 2：告訴 Aspose AI GPU 上要使用多少層

```python
# Step 2: set gpu layers – we’ll run the first 30 layers on the GPU
cfg.gpu_layers = 30
```

在此我們 **設定 GPU 層**。Transformer 的前 30 層通常是計算最密集的，將它們卸載到 GPU 可獲得最大的加速，同時將其餘層保留在 CPU，以符合 VRAM 限制。

> **專業提示：** 若遭遇記憶體不足錯誤，請降低此數值（例如 `cfg.gpu_layers = 20`）。相反地，若你擁有強大的 GPU，則可提升至 `40` 或更高。

### 步驟 3：指向 Hugging Face 倉庫

```python
# Step 3: Specify the Hugging Face repo that holds the model
cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
```

這就是 **如何從 Hugging Face 載入模型** 的核心。提供倉庫 ID 後，Aspose AI 會在第一次執行腳本時自動下載模型檔案，並將其快取於本機，之後的執行會直接重複使用。

> **特殊情況：** 某些倉庫需要驗證。若收到 401 錯誤，請建立 Hugging Face token，並設定 `cfg.hugging_face_token = "<YOUR_TOKEN>"`。

### 步驟 4：實例化 Aspose AI 引擎

```python
# Step 4: Create the engine instance
ai = aocr.AsposeAI()
```

引擎是實際執行推論的執行環境。直到呼叫 `initialize` 前，它保持輕量化。

### 步驟 5：使用已準備好的設定初始化引擎

```python
# Step 5: Wire everything together
ai.initialize(cfg)
```

在 `initialize` 期間，Aspose AI 會從倉庫取得模型（若尚未下載），將指定數量的層載入 GPU，並準備好接受提示。

### 步驟 6：驗證 GPU 層已啟用

```python
# Step 6: Quick sanity check – print the active GPU layer count
print("GPU layers active:", cfg.gpu_layers)
```

你應該會看到：

```
GPU layers active: 30
```

若顯示的數字與你設定的相符，即表示已成功 **設定 GPU 層**，模型已可進行推論。

## 完整可執行範例

以下為完整、可直接執行的腳本，將所有步驟整合在一起。將其複製貼上至名為 `load_hf_model.py` 的檔案，然後執行 `python load_hf_model.py`。

```python
import aocr

# ------------------------------------------------------------
# 1️⃣ Create configuration object
# ------------------------------------------------------------
cfg = aocr.AsposeAIModelConfig()

# ------------------------------------------------------------
# 2️⃣ Set how many layers run on the GPU
# ------------------------------------------------------------
cfg.gpu_layers = 30          # adjust based on your GPU memory

# ------------------------------------------------------------
# 3️⃣ Point to the Hugging Face repository
# ------------------------------------------------------------
cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"

# (Optional) If your repo is private, uncomment the line below:
# cfg.hugging_face_token = "hf_XXXXXXXXXXXXXXXXXXXXXXXX"

# ------------------------------------------------------------
# 4️⃣ Create the Aspose AI engine
# ------------------------------------------------------------
ai = aocr.AsposeAI()

# ------------------------------------------------------------
# 5️⃣ Initialize with the config
# ------------------------------------------------------------
ai.initialize(cfg)

# ------------------------------------------------------------
# 6️⃣ Verify GPU layer activation
# ------------------------------------------------------------
print("GPU layers active:", cfg.gpu_layers)

# ------------------------------------------------------------
# 7️⃣ Quick inference test (optional)
# ------------------------------------------------------------
prompt = "Explain the difference between supervised and unsupervised learning."
response = ai.infer(prompt)   # returns a string with the model's answer
print("\nModel response:\n", response)
```

### 預期輸出

```
GPU layers active: 30

Model response:
 Supervised learning uses labeled data...
```

回應的具體文字會因模型版本而異，但腳本應能順利執行完畢且不拋出例外。

## 設定 GPU 層 – 進階技巧

雖然基本的 **set gpu layers** 語句（`cfg.gpu_layers = 30`）適用於大多數情況，但你仍可能遇到以下情形：

| Situation | What to do |
|-----------|------------|
| **VRAM 短缺**（例如 8 GB GPU） | 將 `gpu_layers` 降至 20 或更低。 |
| **多 GPU** | 使用 `cfg.gpu_id = 1` 以指定第二張 GPU，然後將 `gpu_layers` 設為記憶體允許的最高值。 |
| **僅 CPU 後備** | 將 `cfg.gpu_layers = 0`。引擎將完全在 CPU 上執行，速度較慢但較安全。 |
| **混合精度** | 啟用 `cfg.use_fp16 = True` 以在支援的硬體上將記憶體使用量減半。 |

這些調整讓你能在速度與記憶體消耗之間取得最佳平衡。

## 視覺概覽

![說明如何使用 Aspose AI 從 Hugging Face 載入模型以及 GPU 層應用位置的圖示](image.png)

*Alt text:* 圖示說明 **how to load model from Hugging Face** 使用 Aspose AI 的流程以及 GPU 層的應用位置。

## 常見問題

**Q: 我需要手動下載模型嗎？**  
不需要。Aspose AI 會在你提供 repo ID 後自動處理下載。

**Q: 如果模型格式不是 GGUF 該怎麼辦？**  
Aspose AI 目前支援 GGUF 與 ONNX 格式。其他格式需先轉換或使用其他載入器。

**Q: 初始化後可以更改 GPU 層數嗎？**  
不能，除非重新初始化引擎。呼叫 `ai.shutdown()`（若可用），調整 `cfg.gpu_layers`，再執行 `initialize`。

## 下一步

既然你已了解 **how to load model from Hugging Face** 與 **set GPU layers**，接下來可能想要：

* 探索 **batch inference** 以提升吞吐量。  
* 將引擎掛接至 FastAPI 端點，提供即時服務。  
* 嘗試 **quantized models**，在有限的 VRAM 下擠出更高效能。  

上述主題皆建立在剛才的基礎上，轉換過程會相當順暢。

## 結論

我們已完整示範了使用 Aspose AI **how to load model from Hugging Face** 的實作範例，並說明了如何 **set GPU layers** 以獲得最佳效能。此腳本可直接嵌入任何專案，額外的技巧也能幫助你避免常見陷阱。  

快來試試看，

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，並以此為基礎。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在自己的專案中探索其他實作方式。

- [使用 Aspose OCR 從影像擷取文字 – 步驟教學](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [如何在 Java 中設定 Aspose OCR 授權並驗證](/ocr/english/java/ocr-basics/set-license/)
- [使用 Aspose.OCR 以語言辨識影像文字](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}