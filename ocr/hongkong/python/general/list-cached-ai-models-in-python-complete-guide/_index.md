---
category: general
date: 2026-06-22
description: 學習如何使用 Python 的 AI SDK 列出已快取的 AI 模型。包括取得模型快取目錄的步驟，以及有效管理本地 AI 模型。
draft: false
keywords:
- list cached ai models
- retrieve model cache directory
- list local ai models
- ai sdk python
- manage ai model cache
language: zh-hant
og_description: 使用 AI SDK 以 Python 列出已快取的 AI 模型。遵循此一步步教學，取得模型快取目錄並處理本機 AI 模型。
og_title: 列出已快取的 AI 模型於 Python – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Learn how to list cached AI models using the AI SDK in Python. Includes
    steps to retrieve model cache directory and manage local AI models efficiently.
  headline: List Cached AI Models in Python – Complete Guide
  type: TechArticle
- description: Learn how to list cached AI models using the AI SDK in Python. Includes
    steps to retrieve model cache directory and manage local AI models efficiently.
  name: List Cached AI Models in Python – Complete Guide
  steps:
  - name: Import the AI SDK
    text: '```python # Step 1: Import the AI SDK (replace with the actual package
      name if different) import ai ```'
  - name: List All Cached Models
    text: '```python # Step 2: List all models that are cached locally cached_models
      = ai.list_local() print("Cached models:", cached_models) ```'
  - name: Retrieve the Model Cache Directory
    text: '```python # Step 3: Retrieve the directory where the model files are stored
      cache_dir = ai.get_local_path() print("Model cache directory:", cache_dir) ```'
  - name: Empty Cache
    text: If `ai.list_local()` returns an empty list, you might wonder whether the
      SDK is misconfigured. Double‑check the environment variable `AI_CACHE_DIR` (or
      the SDK’s config file) to ensure it points to a writable location.
  - name: Permissions Issues
    text: When accessing `ai.get_local_path()`, a `PermissionError` can surface on
      restrictive systems. The fix is usually to run the script with appropriate user
      rights or to adjust the directory’s ACLs.
  - name: Version Mismatches
    text: 'Sometimes the cache contains an older version of a model while your code
      requests a newer one. The SDK will automatically download the newer version,
      but you can pre‑empt this by inspecting the version tag in the list:'
  - name: Cleaning Up Old Models
    text: 'If you need to free up space, you can delete a specific model folder directly:'
  type: HowTo
- questions:
  - answer: Yes. The SDK abstracts away OS‑specific paths, so `ai.get_local_path()`
      returns a valid string on Linux, macOS, and Windows.
    question: Does this work on all operating systems?
  - answer: The built‑in `list_local()` only reports locally stored artifacts. For
      remote registries you’d use `ai.list_remote()` (if your SDK version provides
      it).
    question: Can I list models from a remote cache?
  - answer: 'Replace the import line with the actual package name, e.g., `import myai
      as ai`. All subsequent calls stay the same because the API contract is consistent
      across implementations. --- ## Conclusion You now have a solid, production‑ready
      method to **list cached AI models** using the **AI SDK Python** '
    question: What if the SDK name isn’t `ai`?
  type: FAQPage
tags:
- python
- ai
- sdk
title: Python 中列出快取的 AI 模型 – 完整指南
url: /zh-hant/python/general/list-cached-ai-models-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 列出 Python 中已快取的 AI 模型 – 完整指南

有沒有想過如何在工作站上 **列出已快取的 AI 模型**，而不必在繁雜的資料夾中搜尋？你並不孤單。許多開發者在需要確認哪些模型已經本地儲存時會卡住，尤其是在頻寬受限或離線部署的情況下。在本教學中，你將看到一個快速、直截了當的方式來查詢 AI SDK、列印快取內容，並確切找出這些檔案所在的位置。

我們也會涉及相關主題，如 **取得模型快取目錄**、處理空快取，以及在生產腳本中 **管理 AI 模型快取** 的最佳實踐。完成後，你將擁有一段可直接嵌入任何 Python 專案的完整程式碼片段。

## 前置條件

在深入之前，請確保你已具備：

- 已安裝 Python 3.8 或更新版本。
- 已透過 `pip install ai-sdk` 或貴組織的內部套件庫安裝 AI SDK（`ai` 套件）。
- 具備在命令列執行腳本的基本知識。

不需要額外的函式庫，範例因此保持輕量且可移植。

---

## 列出已快取的 AI 模型 – 快速概覽

首先需要匯入 SDK 並呼叫其輔助函式。SDK 提供兩個方便的方法：

1. `ai.list_local()` – 回傳已快取模型識別碼的 Python list。
2. `ai.get_local_path()` – 回傳這些模型檔案所在的絕對目錄。

兩個呼叫皆為同步執行，若發生錯誤會拋出明確的 `AIError`，使錯誤處理變得直接。

> **為何使用這些函式？**  
> 瞭解已快取模型的完整清單可避免不必要的下載、除錯版本不匹配，並自動清理舊的產物。這是更大 **AI SDK Python** 工作流程中的一小環節，但能為你節省數小時手動搜尋檔案系統的時間。

### 步驟 1：匯入 AI SDK

```python
# Step 1: Import the AI SDK (replace with the actual package name if different)
import ai
```

*為何重要：* 匯入套件會註冊底層的 C 擴充元件，並從環境載入設定檔（例如快取路徑）。若跳過此步驟，當你呼叫任何 SDK 函式時會立刻拋出 `ModuleNotFoundError`。

### 步驟 2：列出所有已快取的模型

```python
# Step 2: List all models that are cached locally
cached_models = ai.list_local()
print("Cached models:", cached_models)
```

**你會看到的結果：** 若已儲存三個模型，輸出可能如下：

```
Cached models: ['gpt-4-mini', 'bert-base-uncased', 'stable-diffusion-v1']
```

若快取為空，則會得到空的清單：

```
Cached models: []
```

> **專業提示：** 若懷疑 SDK 尚未正確初始化，請將呼叫包在 try/except 區塊中。

```python
try:
    cached_models = ai.list_local()
except ai.AIError as e:
    print("Failed to list cached models:", e)
    cached_models = []
```

### 步驟 3：取得模型快取目錄

```python
# Step 3: Retrieve the directory where the model files are stored
cache_dir = ai.get_local_path()
print("Model cache directory:", cache_dir)
```

在類 Unix 系統上的典型輸出：

```
Model cache directory: /home/you/.cache/ai/models
```

在 Windows 上可能會看到類似 `C:\Users\you\AppData\Local\ai\models` 的路徑。了解此路徑在手動 **管理 AI 模型快取** 時至關重要——例如清除舊版本或將檔案複製到共享磁碟。

---

## 視覺總結

![說明如何列出已快取的 AI 模型、取得其名稱並定位快取目錄的圖示](https://example.com/images/list-cached-ai-models.png)

*Alt text:* 圖示說明使用 AI SDK 在 Python 中 **列出已快取的 AI 模型** 的流程。

## 處理邊緣情況與常見陷阱

### 空快取

如果 `ai.list_local()` 回傳空清單，你可能會懷疑 SDK 設定錯誤。請再次確認環境變數 `AI_CACHE_DIR`（或 SDK 的設定檔）指向可寫入的目錄。

```python
if not cached_models:
    print("No models are cached. Consider downloading a model first.")
```

### 權限問題

在存取 `ai.get_local_path()` 時，受限系統可能會拋出 `PermissionError`。通常的解決方式是以適當的使用者權限執行腳本，或調整目錄的 ACL 設定。

### 版本不匹配

有時快取中保存的是舊版模型，而程式碼要求較新版本。SDK 會自動下載較新版本，但你可以透過檢查清單中的版本標籤提前發現此情況：

```python
for model in cached_models:
    if "v2" not in model:
        print(f"Model {model} may be outdated.")
```

### 清理舊模型

若需要釋放空間，可直接刪除特定模型的資料夾：

```python
import shutil, os

def purge_model(model_name):
    path = os.path.join(cache_dir, model_name)
    if os.path.isdir(path):
        shutil.rmtree(path)
        print(f"Purged {model_name} from cache.")
    else:
        print(f"{model_name} not found in cache.")
```

執行 `purge_model('bert-base-uncased')` 會移除該模型並釋放磁碟空間。

## 完整腳本，可直接複製貼上

以下是一個可直接執行的腳本，結合所有步驟、加入基本錯誤處理，並印出友善的摘要。

```python
#!/usr/bin/env python3
"""
Complete example: list cached AI models and show cache directory.
"""

import ai
import os
import sys
import shutil

def main():
    try:
        # Retrieve cached model list
        cached = ai.list_local()
        print("Cached models:", cached)

        # Retrieve cache directory
        cache_dir = ai.get_local_path()
        print("Model cache directory:", cache_dir)

        # Summarize status
        if not cached:
            print("\n⚠️  No models are currently cached.")
        else:
            print("\n✅  Found {} model(s) in cache.".format(len(cached)))

        # Optional: ask user if they want to purge an old model
        if cached:
            to_purge = input("\nEnter a model name to purge (or press Enter to skip): ").strip()
            if to_purge:
                purge_path = os.path.join(cache_dir, to_purge)
                if os.path.isdir(purge_path):
                    shutil.rmtree(purge_path)
                    print(f"🗑️  Purged {to_purge} from cache.")
                else:
                    print(f"❌  Model {to_purge} not found in cache.")
    except ai.AIError as err:
        print("AI SDK error:", err, file=sys.stderr)
        sys.exit(1)
    except Exception as exc:
        print("Unexpected error:", exc, file=sys.stderr)
        sys.exit(1)

if __name__ == "__main__":
    main()
```

**預期輸出（快取有內容時）：**

```
Cached models: ['gpt-4-mini', 'bert-base-uncased', 'stable-diffusion-v1']
Model cache directory: /home/you/.cache/ai/models

✅  Found 3 model(s) in cache.

Enter a model name to purge (or press Enter to skip):
```

使用 `python list_models.py` 執行腳本，即可立即得知磁碟上有哪些模型。

## 常見問題

**Q: 這在所有作業系統上都能運作嗎？**  
A: 可以。SDK 抽象化了作業系統特定的路徑，因此 `ai.get_local_path()` 在 Linux、macOS 與 Windows 上皆會回傳有效字串。

**Q: 我可以列出遠端快取的模型嗎？**  
A: 內建的 `list_local()` 只會回報本地儲存的檔案。若要查詢遠端註冊表，需使用 `ai.list_remote()`（前提是你的 SDK 版本支援此功能）。

**Q: 若 SDK 名稱不是 `ai`，該怎麼辦？**  
A: 將匯入行改為實際的套件名稱，例如 `import myai as ai`。之後的呼叫保持不變，因為 API 合約在各實作間是一致的。

## 結論

現在你已掌握一套穩健、可投入生產環境的方式，使用 **AI SDK Python** 函式庫 **列出已快取的 AI 模型**、取得 **模型快取目錄**，甚至清理舊檔案。此知識可協助你保持環境整潔、避免重複下載，並輕鬆除錯版本問題。

準備好下一步了嗎？試著擴充腳本以自動下載缺少的模型，或將其整合至 CI 流程，在每次建置前驗證快取健康。探索 **管理 AI 模型快取** 的策略，將使你的 AI 應用更快速且更可靠。

祝程式開發順利，願你的快取保持精簡！

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，建立在本篇示範的技巧之上。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在專案中探索替代實作方式。

- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Extract Text from ZIP Archives Using Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}