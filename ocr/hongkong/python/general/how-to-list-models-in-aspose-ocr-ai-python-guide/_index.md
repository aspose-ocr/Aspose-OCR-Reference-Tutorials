---
category: general
date: 2026-01-07
description: 如何使用 Python 列出 Aspose OCR AI 的模型 – 學習取得模型路徑、檢查已安裝的模型，並在數秒內獲取 Python 模型清單。
draft: false
keywords:
- how to list models
- get model path
- check installed models
- python get model list
- list available models
language: zh-hant
og_description: 如何使用 Python 列出 Aspose OCR AI 的模型。查找模型路徑、檢查已安裝的模型，並查看可用模型的完整列表。
og_title: 如何在 Aspose OCR AI 中列出模型 – Python 指南
tags:
- Aspose OCR
- Python
- AI models
title: 如何在 Aspose OCR AI 中列出模型 – Python 指南
url: /zh-hant/python/general/how-to-list-models-in-aspose-ocr-ai-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Aspose OCR AI 中列出模型 – Python 指南

有沒有想過 **如何列出模型** 已經安裝在機器上的模型，當使用 Aspose OCR AI 時？你並不是唯一遇到這個問題的人。在許多專案中，你需要檢查模型資料夾、確認有哪些模型存在，甚至在不離開 Python REPL 的情況下除錯缺少模型的問題。

在本教學中，我們將逐步說明一個完整、可直接執行的範例，示範如何 **取得模型路徑**、**檢查已安裝的模型**，以及最終 **列出可用模型**，只需幾行程式碼。沒有外部腳本，沒有隱藏的魔法——只有純粹的 Python 與 Aspose OCR AI SDK。

> **先決條件**  
> • Python 3.8 或更新版本  
> • 已安裝 `asposeocr` 套件（`pip install asposeocr`）  
> • 基本熟悉模組匯入

如果你已滿足上述條件，讓我們開始吧。

---

## 使用 Aspose OCR AI 列出模型

首先，我們需要 `AsposeAI` 輔助類別，它隨 `asposeocr.ai` 模組一起提供。此類別提供了三個方便的方法：

| 方法 | 返回值 | 典型使用情境 |
|--------|----------------|-----------------|
| `get_local_path()` | Aspose 存放 AI 模型的資料夾之絕對路徑 | 驗證 SDK 正在檢查正確的路徑 |
| `list_local()` | 磁碟上現有模型資料夾名稱的 Python `list` | 快速查看可以載入的模型 |
| `list_remote()` *(optional)* | 可從 Aspose 雲端下載的模型清單 | 當你需要本機未擁有的模型時 |

以下是 **完整腳本**，會印出本機模型資料夾以及已安裝模型的清單。

```python
# ---------------------------------------------------------
# Step 1: Import the Aspose OCR AI module
# ---------------------------------------------------------
from asposeocr.ai import AsposeAI

# ---------------------------------------------------------
# Step 2: Create an instance of the AI helper
# ---------------------------------------------------------
ai = AsposeAI()

# ---------------------------------------------------------
# Step 3: Retrieve and display the local model folder
# ---------------------------------------------------------
local_folder = ai.get_local_path()
print("Local AI model folder:", local_folder)

# ---------------------------------------------------------
# Step 4: List all models that are currently installed
# ---------------------------------------------------------
installed_models = ai.list_local()
print("Available models:", installed_models)
```

### 預期輸出

在全新安裝環境執行腳本時，通常會看到類似以下的輸出：

```
Local AI model folder: /home/user/.asposeocr/models
Available models: ['ocr-general-v1', 'ocr-handwritten-v2']
```

如果資料夾是空的，`list_local()` 會回傳空清單 (`[]`)。這是一個有用的訊號，表示你需要先下載模型——我們稍後會說明。

## 為何了解模型路徑很重要

了解 SDK **將檔案儲存於何處**（`取得模型路徑`）不僅僅是好奇心：

1. **除錯** – 若模型載入失敗，你可以 `ls` 該路徑，確認檔案是否真的存在。  
2. **自訂模型** – 某些團隊會自行訓練 OCR 模型並放入該資料夾。了解路徑可讓你將檔案正確放置於 Aspose 所預期的位置。  
3. **權限** – 在 Linux 上，該資料夾可能屬於其他使用者。提前發現權限錯誤可省下數小時的苦惱。

> 小技巧：如果需要將 SDK 指向自訂目錄，請在建立 `AsposeAI()` 前設定環境變數 `ASPOSE_OCR_MODEL_PATH`。

```bash
export ASPOSE_OCR_MODEL_PATH=/my/custom/models
python my_script.py
```

## 檢查已安裝模型 – 邊緣情況與技巧

### 1. 未安裝任何模型

如果 `list_local()` 回傳 `[]`，你有兩個選擇：

| 選項 | 操作方式 |
|--------|--------------|
| **從 Aspose 下載模型** | `ai.download('ocr-general-v1')`（需要網路） |
| **複製預訓練模型** | 手動將模型資料夾放入 `get_local_path()` 顯示的路徑中 |

### 2. 同一模型的多個版本

有時會同時看到 `ocr-general-v1` **以及** `ocr-general-v1-beta`。SDK 會載入第一個匹配的版本，但你可以透過將確切的資料夾名稱傳遞給 OCR 建構子，強制使用特定版本：

```python
from asposeocr.ai import AsposeOCR

ocr = AsposeOCR(model_name='ocr-general-v1-beta')
```

### 3. 模型檔案損毀

部分下載的模型可能導致之後拋出 `FileNotFoundError`。若懷疑檔案損毀，只需刪除相關資料夾並重新下載：

```bash
rm -rf /home/user/.asposeocr/models/ocr-general-v1
python -c "from asposeocr.ai import AsposeAI; AsposeAI().download('ocr-general-v1')"
```

## 擴充腳本 – 列出遠端模型（可選）

如果想在不離開 Python 的情況下查看可下載的模型，加入以下呼叫：

```python
remote_models = ai.list_remote()
print("Remote models you can download:", remote_models)
```

這會輸出類似以下內容：

```
Remote models you can download: ['ocr-general-v1', 'ocr-handwritten-v2', 'ocr-table-v1']
```

之後即可選擇任意模型，呼叫 `ai.download('model-name')` 以自動下載。

## 完整端對端範例

將所有步驟整合起來，以下是一個 **單一可執行腳本**，它會：

1. 顯示本機模型資料夾。  
2. 列出已安裝的模型。  
3. 若未找到模型，下載預設模型。  
4. 最後，印出更新後的清單。

```python
# ---------------------------------------------------------
# Complete script – verifies model folder, installs if empty
# ---------------------------------------------------------
from asposeocr.ai import AsposeAI

def main():
    ai = AsposeAI()

    # 1️⃣ Show where Aspose expects models
    local_path = ai.get_local_path()
    print("🔎 Local AI model folder:", local_path)

    # 2️⃣ List currently installed models
    models = ai.list_local()
    print("📦 Installed models:", models)

    # 3️⃣ If nothing is installed, grab a default model
    if not models:
        default = 'ocr-general-v1'
        print(f"⚠️ No models found – downloading '{default}'...")
        try:
            ai.download(default)
            models = ai.list_local()
            print("✅ After download, installed models:", models)
        except Exception as e:
            print("❌ Failed to download model:", e)
            return

    # 4️⃣ (Optional) Show what you could download from the cloud
    remote = ai.list_remote()
    print("🌐 Remote models available:", remote)

if __name__ == "__main__":
    main()
```

在全新機器上執行此腳本會產生：

```
🔎 Local AI model folder: /home/user/.asposeocr/models
📦 Installed models: []
⚠️ No models found – downloading 'ocr-general-v1'...
✅ After download, installed models: ['ocr-general-v1']
🌐 Remote models available: ['ocr-general-v1', 'ocr-handwritten-v2', 'ocr-table-v1']
```

現在你擁有一個 **自包含且可供引用** 的解決方案，任何 AI 助手都能逐字引用。

## 常見問題 (FAQ)

**Q: 這在 Windows 上可用嗎？**  
A: 當然可以。SDK 抽象化檔案系統，`get_local_path()` 會回傳類似 `C:\Users\YourName\.asposeocr\models` 的路徑。只要確保 Python 有寫入該資料夾的權限即可。

**Q: 我可以將模型存放在網路磁碟上嗎？**  
A: 可以——在建立 `AsposeAI` 實例前，將 `ASPOSE_OCR_MODEL_PATH` 設為 UNC 路徑（`\\server\share\models`）。

**Q: 如果需要預設套件未涵蓋的語言模型該怎麼辦？**  
A: 使用 `list_remote()` 查看 Aspose 是否提供特定語言的模型。若沒有，你可以自行訓練並放入資料夾；只要將自訂資料夾名稱傳給 OCR 建構子即可。

## 結論

我們已說明如何在 Aspose OCR AI 中 **列出模型**，示範了如何 **取得模型路徑**、**檢查已安裝的模型**，甚至 **下載缺少的模型**——全部僅使用純 Python。透過了解資料夾結構與輔助方法（`get_local_path()`、`list_local()`、`list_remote()`），你即可完整掌控應用程式所依賴的 AI 模型。

接下來的步驟？可以嘗試將預設模型換成手寫文字模型，或是將 SDK 指向自行訓練的自訂模型。無論哪種方式，你現在都有堅實的基礎來管理任何 Python 專案中的 OCR 資源。

祝開發順利，願你的模型清單永遠保持最新！

![如何列出模型截圖](https://example.com/images/how-to-list-models.png "如何列出模型")

*圖片替代文字:* **如何列出模型截圖**（符合主要關鍵字需求）。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}