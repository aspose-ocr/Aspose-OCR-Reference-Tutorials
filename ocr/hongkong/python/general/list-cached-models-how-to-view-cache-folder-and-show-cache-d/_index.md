---
category: general
date: 2026-02-22
description: 學習如何列出已快取的模型，並快速顯示您電腦上的快取目錄。包括查看快取資料夾及管理本機 AI 模型儲存的步驟。
draft: false
keywords:
- list cached models
- show cache directory
- how to view cache folder
- AI model cache
- local model storage
language: zh-hant
og_description: 了解如何列出快取模型、顯示快取目錄以及檢視快取資料夾，只需簡單幾步。附上完整的 Python 範例。
og_title: 列出已快取模型 – 快速指南：查看快取目錄
tags:
- AI
- caching
- Python
- development
title: 列出已快取模型 – 如何檢視快取資料夾及顯示快取目錄
url: /zh-hant/python/general/list-cached-models-how-to-view-cache-folder-and-show-cache-d/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 列出快取模型 – 快速指南：檢視快取目錄

你是否曾好奇如何在工作站上 **list cached models** 而不必在隱蔽的資料夾中搜尋？你並非唯一有此疑問的人。許多開發者在需要確認哪些 AI 模型已經本地儲存時會卡住，尤其當磁碟空間緊張時。好消息是？只要幾行程式碼，你就能同時 **list cached models** 與 **show cache directory**，完整掌握快取資料夾的情況。

在本教學中，我們將逐步說明一個獨立的 Python 腳本，正好完成此功能。完成後，你將知道如何檢視快取資料夾、了解不同作業系統上快取的所在位置，甚至看到每個已下載模型的整齊列印清單。無需外部文件、無需猜測——只要清晰的程式碼與說明，現在即可複製貼上使用。

## 你將學到

- 如何初始化提供快取功能的 AI client（或 stub）。  
- 執行 **list cached models** 與 **show cache directory** 的精確指令。  
- 快取在 Windows、macOS 與 Linux 上的存放位置，讓你可以手動導航。  
- 處理邊緣情況的技巧，例如快取為空或自訂快取路徑。  

**Prerequisites** – 你需要 Python 3.8+ 以及可透過 pip 安裝的 AI client，且該 client 必須實作 `list_local()`、`get_local_path()`，以及可選的 `clear_local()`。如果尚未有此 client，範例會使用一個模擬的 `YourAIClient` 類別，你可以將其替換為真實的 SDK（例如 `openai`、`huggingface_hub` 等）。

準備好了嗎？讓我們開始吧。

## 第一步：設定 AI Client（或 Mock）

如果你已經有 client 物件，請跳過此區塊。否則，建立一個小型的替身來模擬快取介面。即使沒有真實的 SDK，也能讓腳本可執行。

```python
# step_1_client_setup.py
import os
from pathlib import Path

class YourAIClient:
    """
    Minimal mock of an AI client that stores downloaded models in a
    directory called `.ai_cache` inside the user's home folder.
    """
    def __init__(self, cache_dir: Path | None = None):
        # Use a custom path if supplied, otherwise default to ~/.ai_cache
        self.cache_dir = Path(cache_dir) if cache_dir else Path.home() / ".ai_cache"
        self.cache_dir.mkdir(parents=True, exist_ok=True)

    def list_local(self):
        """Return a list of model folder names that exist in the cache."""
        return [p.name for p in self.cache_dir.iterdir() if p.is_dir()]

    def get_local_path(self):
        """Absolute path to the cache directory."""
        return str(self.cache_dir.resolve())

    # Optional helper for demonstration purposes
    def _populate_dummy_models(self, count=3):
        for i in range(1, count + 1):
            (self.cache_dir / f"model_{i}").mkdir(exist_ok=True)

# Initialize the client (replace with real client if you have one)
ai = YourAIClient()
# Populate with dummy data the first time you run the script
if not ai.list_local():
    ai._populate_dummy_models()
```

> **Pro tip:** 如果你已經有真實的 client（例如 `from huggingface_hub import HfApi`），只需將 `YourAIClient()` 呼叫改為 `HfApi()`，並確保 `list_local` 與 `get_local_path` 方法存在或已相應包裝。

## 第二步：**list cached models** – 取得並顯示

現在 client 已就緒，我們可以請它列舉本機上已知的所有項目。這就是我們 **list cached models** 操作的核心。

```python
# step_2_list_models.py
print("Cached models:")
for model_name in ai.list_local():
    print(" -", model_name)
```

**Expected output**（使用第 1 步的虛擬資料）：

```
Cached models:
 - model_1
 - model_2
 - model_3
```

如果快取為空，你只會看到：

```
Cached models:
```

那個空白行表示目前尚未有任何儲存——在編寫清理腳本時相當方便。

## 第三步：**show cache directory** – 快取位於何處？

了解路徑往往是解決問題的一半。不同作業系統會將快取放在不同的預設位置，且部分 SDK 允許透過環境變數覆寫。以下程式碼會印出絕對路徑，讓你可以 `cd` 進入或在檔案總管中開啟。

```python
# step_3_show_path.py
print("\nCache directory:", ai.get_local_path())
```

**Typical output**（在類 Unix 系統上的典型輸出）：

```
Cache directory: /home/youruser/.ai_cache
```

在 Windows 上可能會看到類似以下的輸出：

```
Cache directory: C:\Users\YourUser\.ai_cache
```

現在你已清楚知道在任何平台上 **how to view cache folder**。

## 第四步：整合全部 – 單一可執行腳本

以下是完整、可直接執行的程式，結合了前述三個步驟。將其儲存為 `view_ai_cache.py`，然後執行 `python view_ai_cache.py`。

```python
# view_ai_cache.py
import os
from pathlib import Path

class YourAIClient:
    """Simple mock client exposing cache‑related utilities."""
    def __init__(self, cache_dir: Path | None = None):
        self.cache_dir = Path(cache_dir) if cache_dir else Path.home() / ".ai_cache"
        self.cache_dir.mkdir(parents=True, exist_ok=True)

    def list_local(self):
        return [p.name for p in self.cache_dir.iterdir() if p.is_dir()]

    def get_local_path(self):
        return str(self.cache_dir.resolve())

    def _populate_dummy_models(self, count=3):
        for i in range(1, count + 1):
            (self.cache_dir / f"model_{i}").mkdir(exist_ok=True)

# ----------------------------------------------------------------------
# Main execution block
# ----------------------------------------------------------------------
if __name__ == "__main__":
    # Initialize (replace with real client if available)
    ai = YourAIClient()

    # Populate dummy data only on first run – remove this in production
    if not ai.list_local():
        ai._populate_dummy_models()

    # Step 1: list cached models
    print("Cached models:")
    for model_name in ai.list_local():
        print(" -", model_name)

    # Step 2: show cache directory
    print("\nCache directory:", ai.get_local_path())
```

執行後，你會立即看到已快取模型的清單 **以及** 快取目錄的位置。

## 邊緣情況與變化

| 情況 | 處理方式 |
|-----------|------------|
| **Empty cache** | 腳本會印出 “Cached models:” 但不會有條目。你可以加入條件警告：`if not models: print("⚠️ No models cached yet.")` |
| **Custom cache path** | 建構 client 時傳入路徑：`YourAIClient(cache_dir=Path("/tmp/my_ai_cache"))`。`get_local_path()` 呼叫會顯示該自訂位置。 |
| **Permission errors** | 在受限機器上，client 可能拋出 `PermissionError`。將初始化包在 `try/except` 區塊，並回退到使用者可寫入的目錄。 |
| **Real SDK usage** | 將 `YourAIClient` 替換為實際的 client 類別，並確保方法名稱相符。許多 SDK 會直接提供 `cache_dir` 屬性供讀取。 |

## 管理快取的專業技巧

- **Periodic cleanup:** 如果你經常下載大型模型，請排程 cron 工作，在確認不再需要後呼叫 `shutil.rmtree(ai.get_local_path())` 以清除快取。  
- **Disk usage monitoring:** 在 Linux/macOS 上使用 `du -sh $(ai.get_local_path())`，或在 PowerShell 中使用 `Get-ChildItem -Recurse | Measure-Object -Property Length -Sum` 來監控磁碟使用量。  
- **Versioned folders:** 某些 client 會為每個模型版本建立子資料夾。當你 **list cached models** 時，會看到每個版本作為獨立條目——可利用此方式清除較舊的版本。  

## 視覺概覽

![列出快取模型截圖](https://example.com/images/list-cached-models.png "列出快取模型 – 顯示模型與快取路徑的主控台輸出")

*Alt text:* *列出快取模型 – 主控台輸出顯示已快取模型名稱與快取目錄路徑。*

## 結論

我們已說明了在任何系統上 **list cached models**、**show cache directory**，以及一般性的 **how to view cache folder** 所需的一切。這段簡短腳本展示了完整、可執行的解決方案，說明了每個步驟 **why** 重要，並提供實務使用的技巧。

接下來，你可以探索以程式方式 **how to clear the cache**，或將這些呼叫整合到更大的部署流水線中，以在啟動推論工作前驗證模型可用性。無論哪種方式，你現在都有信心管理本地 AI 模型儲存的基礎。

對特定 AI SDK 有疑問嗎？在下方留言，我們祝你快取愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}