---
category: general
date: 2026-07-05
description: 如何使用 Aspose AI 列出模型、啟用自動下載，並在 Python 中下載 Hugging Face 模型。跟隨本一步一步教學設定快取，立即開始使用
  Aspose AI。
draft: false
keywords:
- how to list models
- enable auto download
- download hugging face model
- how to use aspose
- how to set cache
language: zh-hant
og_description: 如何使用 Aspose AI 列出模型、啟用自動下載並下載 Hugging Face 模型。學習設定快取，幾分鐘內即可使用 Aspose
  AI。
og_title: 如何使用 Aspose AI 列出模型 – 完整教學
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: How to list models with Aspose AI, enable auto download, and download
    Hugging Face model in Python. Follow this step‑by‑step tutorial to set up cache
    and start using Aspose AI today.
  headline: How to list models with Aspose AI – Complete Guide
  type: TechArticle
- description: How to list models with Aspose AI, enable auto download, and download
    Hugging Face model in Python. Follow this step‑by‑step tutorial to set up cache
    and start using Aspose AI today.
  name: How to list models with Aspose AI – Complete Guide
  steps:
  - name: Create an `AsposeAI` object and a `AsposeAIModelConfig`.
    text: Create an `AsposeAI` object and a `AsposeAIModelConfig`.
  - name: Set `allow_auto_download = "true"` and point `directory_model_path` to a
      folder you control.
    text: Set `allow_auto_download = "true"` and point `directory_model_path` to a
      folder you control.
  - name: Initialise the AI, then call `list_local()` to see exactly what’s cached.
    text: Initialise the AI, then call `list_local()` to see exactly what’s cached.
  - name: Use the listed model name for inference, and you’re ready to build real‑world
      applications.
    text: Use the listed model name for inference, and you’re ready to build real‑world
      applications.
  type: HowTo
tags:
- Aspose
- Python
- LLM
- Model Management
title: 如何使用 Aspose AI 列出模型 – 完整指南
url: /zh-hant/python/general/how-to-list-models-with-aspose-ai-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose AI 列出模型 – 完整指南

如何使用 Aspose AI 列出模型是當你開始在 Python 中試驗大型語言模型時會立即冒出的問題。在本教學中，我們將一步步說明如何啟用 **auto download**、設定本機快取，並直接從 Hugging Face 下載模型——讓你不必手動搜尋檔案即可快速上手。

如果你曾經好奇 *「如何使用 Aspose 進行 OCR‑驅動的 AI？」* 或 *「設定模型檔案快取的最簡方法是什麼？」*，那麼這裡正是你的答案。完成後，你將擁有一個完整的腳本，能列出本機所有已儲存的模型、自動下載缺少的模型，並清楚顯示檔案在磁碟上的實際位置。

---

## 您需要的條件

- Python 3.9 或更新版本（此函式庫使用需要較新直譯器的型別提示）
- 具備 `pip` 安裝 **Aspose OCR** 套件 (`aocr`) 的權限。  
  ```bash
  pip install aocr
  ```
- 首次從 Hugging Face 下載時需要網際網路連線。
- 一個用來存放模型快取的資料夾（例如 `./model_cache`）。

就這樣——不需要額外的 Docker 容器，也不需要在乾淨的 Python 環境之外建立龐大的虛擬環境。

---

## ## 如何使用 Aspose AI 列出模型

本指南的核心在於能 **list models**，即列出 Aspose AI 在本機快取的模型。一旦快取設定完成，函式庫即可枚舉它所知道的所有模型，讓除錯與版本管理變得輕而易舉。

```python
import aocr

# 1️⃣ Create an Aspose AI instance
ai = aocr.AsposeAI()

# 2️⃣ Configure the model cache and auto‑download behavior
cfg = aocr.AsposeAIModelConfig()
cfg.allow_auto_download = "true"                     # ← enable auto download
cfg.directory_model_path = r"./model_cache"          # ← how to set cache
cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"

# 3️⃣ Initialise the AI with the config we just built
ai.initialize(cfg)

# 4️⃣ List the models that are already cached locally
print("🗂️ Models cached at:", ai.get_local_path())
print("📦 Available models:", ai.list_local())
```

**為什麼這樣會有效：**  
- `AsposeAI()` 會建立與底層推論引擎溝通的高階入口點。  
- `AsposeAIModelConfig()` 保存所有可調整的參數；將 `allow_auto_download` 設為 `"true"` 會告訴函式庫自動從你指定的倉庫下載缺失的檔案。  
- `directory_model_path` 是 *快取目錄*——所有下載的二進位檔案都會放在此處。  
- `initialize()` 會套用設定，若快取為空則執行首次下載。  
- 最後，`list_local()` 會掃描快取資料夾並回傳模型識別碼的 Python list，我們將其列印出來。

### 預期輸出（首次執行）

```
🗂️ Models cached at: ./model_cache
📦 Available models: ['Qwen2.5-3B-Instruct-GGUF']
```

若再次執行腳本，函式庫會跳過下載，直接列出已存在的模型，證明 **設定快取** 在後續執行時確實能節省時間。

---

## ## 為缺少的模型啟用 auto download

在多個專案間切換時，你常會需要使用不同的模型。手動從 Hugging Face 逐一下載相當繁瑣。啟用 auto download 後，Aspose AI 會自動處理下載工作。

```python
cfg.allow_auto_download = "true"
```

> **專業小技巧：** 僅在開發或 CI 環境中將 `allow_auto_download` 設為 `"true"`。在正式環境中建議鎖定快取，以避免不預期的網路流量。

若日後想關閉此功能，只需在再次呼叫 `initialize()` 前將旗標設為 `"false"` 即可。

---

## ## 即時下載 Hugging Face 模型

以下程式碼

```python
cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
```

告訴 Aspose AI 從哪個遠端倉庫取得模型。函式庫支援任何提供 GGUF 檔案的公開 Hugging Face 模型。想換其他模型嗎？只要替換倉庫 ID 即可：

```python
cfg.hugging_face_repo_id = "mistralai/Mistral-7B-Instruct-v0.2"
```

執行腳本時，Aspose AI 會檢查快取：

- **若模型已存在**，會立即載入。  
- **若模型不存在**，auto‑download 旗標會觸發下載，將檔案存於 `directory_model_path`，並立即註冊供使用。

此方式省去許多教學中常見的「先下載再執行」兩步驟。

---

## ## 列出模型後如何使用 Aspose AI

僅列出模型只是第一步。取得模型後即可開始推論：

```python
# Assume the model we just listed is the one we want to use
model_name = ai.list_local()[0]

# Create a simple prompt
prompt = "Explain the difference between supervised and unsupervised learning."

# Run inference
response = ai.run_inference(model_name, prompt)

print("🤖 Model response:", response)
```

**為什麼這很重要：**  
- `run_inference()` 抽象化了分詞、批次處理與 GPU 管理。  
- 只要傳入從 `list_local()` 取得的 *模型名稱*，即可保證推論呼叫對應到磁碟上正確的檔案。

---

## ## 為多個專案設定快取位置

若同時維護多個專案，建議為每個專案配置獨立的快取資料夾。`directory_model_path` 欄位僅是普通字串，故可動態組合路徑：

```python
import os

project_name = "sentiment_analysis"
cache_root   = "./model_cache"
cfg.directory_model_path = os.path.join(cache_root, project_name)
```

如此每個專案都會得到獨立的子資料夾（例如 `./model_cache/sentiment_analysis`），避免版本衝突，且清理工作更為簡單。

---

## ## 常見陷阱與避免方式

| 症狀 | 可能原因 | 解決方式 |
|------|----------|----------|
| **`PermissionError` when accessing cache** | 快取資料夾被其他使用者擁有（在共享伺服器上常見） | 手動建立資料夾並設定正確權限：`mkdir -p ./model_cache && chmod 775 ./model_cache` |
| **Model never appears in `list_local()`** | `allow_auto_download` 設為 `"false"`，且模型尚未快取 | 暫時開啟旗標，執行一次後若需要再關閉 |
| **Unexpected model version** | 兩個不同的倉庫使用相同名稱但內容不同 | 固定完整的 repo ID（含 tag/commit），或在首次成功下載後關閉 auto‑download 以鎖定快取 |
| **Out‑of‑memory errors** | 大型 GGUF 檔案在記憶體/顯存不足的機器上執行 | 改用較小的模型（例如 `Qwen2.5-1.5B`），或將 `cfg.device = "cpu"` 強制使用 CPU 推論 |

---

## ## 完整腳本（可直接複製貼上）

以下是結合上述所有概念的完整範例。將其儲存為 `list_models_demo.py`，然後以 `python list_models_demo.py` 執行。

```python
# list_models_demo.py
import os
import aocr

def main():
    # ------------------------------------------------------------------
    # 1️⃣ Create the Aspose AI instance
    # ------------------------------------------------------------------
    ai = aocr.AsposeAI()

    # ------------------------------------------------------------------
    # 2️⃣ Build configuration: enable auto download, set cache path,
    #    and point at a Hugging Face repo
    # ------------------------------------------------------------------
    cfg = aocr.AsposeAIModelConfig()
    cfg.allow_auto_download = "true"                               # enable auto download
    cfg.directory_model_path = os.path.abspath("./model_cache")   # how to set cache
    cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"

    # ------------------------------------------------------------------
    # 3️⃣ Initialise the AI with the configuration
    # ------------------------------------------------------------------
    ai.initialize(cfg)

    # ------------------------------------------------------------------
    # 4️⃣ Verify cache location and list all locally available models
    # ------------------------------------------------------------------
    print("🗂️ Models cached at:", ai.get_local_path())
    print("📦 Available models:", ai.list_local())

    # ------------------------------------------------------------------
    # 5️⃣ (Optional) Run a quick inference using the first listed model
    # ------------------------------------------------------------------
    if ai.list_local():
        model_name = ai.list_local()[0]
        prompt = "Give a short summary of the Python GIL."
        response = ai.run_inference(model_name, prompt)
        print("\n🤖 Model response:", response)

if __name__ == "__main__":
    main()
```

**執行後** 會產生與前述範例相似的輸出，並附上模型的簡短回應。隨意更換提示文字即可——這是測試模型在 **如何列出模型** 後是否真正可用的最快方式。

---

## ## 小結

我們已完整說明如何使用 Aspose AI **列出模型**，包括啟用 **auto download**、設定永久 **快取**，以及即時從 **Hugging Face** 取得模型。重點如下：

1. 建立 `AsposeAI` 物件與 `AsposeAIModelConfig`。  
2. 將 `allow_auto_download = "true"`，並將 `directory_model_path` 指向自行管理的資料夾。  
3. 初始化 AI，然後呼叫 `list_local()` 查看已快取的模型。  
4. 使用列出的模型名稱進行推論，即可開發實際應用。

---

## 接下來該做什麼？

- **嘗試不同模型** – 將 `cfg.hugging_face_repo_id` 換成其他倉庫，觀察列表如何變化。  
- **微調快取**（此段落原文未完，請自行補充相關說明）

## 接下來應該學什麼？

以下教學與本指南緊密相關，提供完整的程式碼範例與逐步說明，協助你掌握更多 API 功能並在專案中探索其他實作方式。

- [如何在 Aspose.OCR for .NET 中使用 List 批次處理 OCR 圖片](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [如何在 Java 中設定 Aspose OCR 授權並驗證](/ocr/english/java/ocr-basics/set-license/)
- [如何使用 Aspose.OCR for .NET 從影像中擷取文字](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}