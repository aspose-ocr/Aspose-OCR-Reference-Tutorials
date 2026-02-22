---
category: general
date: 2026-02-22
description: 如何在 Python 中刪除檔案並快速清除模型快取。學習使用 Python 列出目錄檔案、按副檔名篩選檔案，以及安全地刪除檔案。
draft: false
keywords:
- how to delete files
- clear model cache
- list directory files python
- filter files by extension
- delete file python
language: zh-hant
og_description: 如何在 Python 中刪除檔案並清除模型快取。一步一步的指南，涵蓋列出目錄檔案、依副檔名篩選檔案，以及刪除檔案的 Python 方法。
og_title: 如何在 Python 中刪除檔案 – 清除模型快取教學
tags:
- python
- file-system
- automation
title: 如何在 Python 中刪除檔案 – 清除模型快取教學
url: /zh-hant/python/general/how-to-delete-files-in-python-clear-model-cache-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中刪除檔案 – 清除模型快取教學

有沒有想過 **how to delete files** 是什麼時候不再需要，尤其是當它們堆滿模型快取目錄時？你並不孤單；許多開發者在實驗大型語言模型時會遇到這個問題，最終產生大量 *.gguf* 檔案。  

在本指南中，我們將示範一個簡潔、可直接執行的解決方案，不僅教導 **how to delete files**，還說明 **clear model cache**、**list directory files python**、**filter files by extension** 以及 **delete file python**，以安全、跨平台的方式執行。完成後，你將擁有一行程式碼可直接放入任何專案，並附上一些處理邊緣案例的技巧。

![刪除檔案示意圖](https://example.com/clear-cache.png "在 Python 中刪除檔案")

## 如何在 Python 中刪除檔案 – 清除模型快取

### 本教學涵蓋內容
- 取得 AI 函式庫儲存快取模型的路徑。  
- 列出該目錄內的所有項目。  
- 僅選取以 **.gguf** 結尾的檔案（即 *filter files by extension* 步驟）。  
- 刪除這些檔案，同時處理可能的權限錯誤。  

不需要外部相依套件，也不需要花俏的第三方套件——只使用內建的 `os` 模組以及假想的 `ai` SDK 中的一個小幫手。

## 步驟 1：列出目錄檔案（Python）

首先，我們需要了解快取資料夾內的內容。`os.listdir()` 函式會回傳檔名的純列表，非常適合快速盤點。

```python
import os

# Assume `ai.get_local_path()` returns the absolute cache directory.
cache_dir_path = ai.get_local_path()

# Grab every entry – this is the “list directory files python” part.
all_entries = os.listdir(cache_dir_path)
print(f"Found {len(all_entries)} items in cache:")
for entry in all_entries:
    print(" •", entry)
```

**為什麼這很重要：**  
列出目錄可以讓你看清內容。如果跳過此步驟，可能會不小心刪除本不該動的檔案。此外，列印出的結果也能在開始清除檔案前作為 sanity‑check（合理性檢查）。

## 步驟 2：依副檔名過濾檔案

並非所有項目都是模型檔案。我們只想清除 *.gguf* 二進位檔，因此使用 `str.endswith()` 方法來過濾列表。

```python
# Keep only files that end with .gguf – our “filter files by extension” logic.
model_files = [f for f in all_entries if f.lower().endswith(".gguf")]
print(f"\nIdentified {len(model_files)} model file(s) to delete:")
for mf in model_files:
    print(" •", mf)
```

**為什麼要過濾：**  
若不加篩選直接大規模刪除，可能會把日誌、設定檔，甚至使用者資料都刪掉。透過明確檢查副檔名，我們確保 **delete file python** 只會針對預期的檔案。

## 步驟 3：安全地刪除檔案（Python）

現在進入 **how to delete files** 的核心。我們會遍歷 `model_files`，使用 `os.path.join()` 建立絕對路徑，然後呼叫 `os.remove()`。將呼叫包在 `try/except` 區塊中，可在不讓腳本崩潰的情況下回報權限問題。

```python
for file_name in model_files:
    file_path = os.path.join(cache_dir_path, file_name)
    try:
        os.remove(file_path)
        print(f"Removed: {file_name}")
    except PermissionError:
        print(f"⚠️  Permission denied: {file_name}")
    except FileNotFoundError:
        # This could happen if another process already deleted the file.
        print(f"⚠️  Already gone: {file_name}")
    except OSError as e:
        # Catch‑all for unexpected OS errors.
        print(f"❌  Failed to delete {file_name}: {e}")

print("\nOld model files removed.")
```

**你會看到：**  
如果一切順利，主控台會顯示每個檔案為「Removed」。若發生錯誤，則會顯示友善的警告，而非難以理解的回溯資訊。此做法體現了 **delete file python** 的最佳實踐——永遠預測並處理錯誤。

## 加分項：驗證刪除與處理邊緣案例

### 驗證目錄已清空

迴圈結束後，最好再次確認沒有 *.gguf* 檔案遺留。

```python
remaining = [f for f in os.listdir(cache_dir_path) if f.lower().endswith(".gguf")]
if not remaining:
    print("✅  Cache is now clean.")
else:
    print("⚡  Some files survived:", remaining)
```

### 若快取資料夾不存在該怎麼辦？

有時 AI SDK 可能尚未建立快取資料夾。提前做好防護：

```python
if not os.path.isdir(cache_dir_path):
    raise RuntimeError(f"The cache directory does not exist: {cache_dir_path}")
```

### 高效刪除大量檔案

如果要處理上千個模型檔案，可考慮使用 `os.scandir()` 取得更快的迭代器，或直接使用 `pathlib.Path.glob("*.gguf")`。邏輯保持不變，僅是列舉方式不同。

## 完整、可直接執行的腳本

把所有步驟整合起來，以下是完整程式碼片段，你可以直接複製貼上到名為 `clear_model_cache.py` 的檔案中：

```python
import os

# -------------------------------------------------
# Step 0: Obtain the cache directory from the AI SDK
# -------------------------------------------------
cache_dir_path = ai.get_local_path()

# -------------------------------------------------
# Safety check: make sure the directory exists
# -------------------------------------------------
if not os.path.isdir(cache_dir_path):
    raise RuntimeError(f"The cache directory does not exist: {cache_dir_path}")

# -------------------------------------------------
# Step 1: List everything (list directory files python)
# -------------------------------------------------
all_entries = os.listdir(cache_dir_path)

# -------------------------------------------------
# Step 2: Keep only .gguf model files (filter files by extension)
# -------------------------------------------------
model_files = [f for f in all_entries if f.lower().endswith(".gguf")]

# -------------------------------------------------
# Step 3: Delete each model file (delete file python)
# -------------------------------------------------
for file_name in model_files:
    file_path = os.path.join(cache_dir_path, file_name)
    try:
        os.remove(file_path)
        print(f"Removed: {file_name}")
    except PermissionError:
        print(f"⚠️  Permission denied: {file_name}")
    except FileNotFoundError:
        print(f"⚠️  Already gone: {file_name}")
    except OSError as e:
        print(f"❌  Failed to delete {file_name}: {e}")

# -------------------------------------------------
# Bonus: Verify everything is gone
# -------------------------------------------------
remaining = [f for f in os.listdir(cache_dir_path) if f.lower().endswith(".gguf")]
if not remaining:
    print("\n✅  Cache is now clean.")
else:
    print("\n⚡  Some files survived:", remaining)

print("\nOld model files removed.")
```

執行此腳本將會：

1. 定位 AI 模型快取。  
2. 列出每個項目（滿足 **list directory files python** 的需求）。  
3. 過濾 *.gguf* 檔案（**filter files by extension**）。  
4. 安全地刪除每個檔案（**delete file python**）。  
5. 確認快取已清空，讓你安心。

## 結論

我們已說明在 Python 中 **how to delete files**，重點在於清除模型快取。完整解決方案示範了如何 **list directory files python**、套用 **filter files by extension**，以及安全地 **delete file python**，同時處理常見的問題，如權限不足或競爭條件。

接下來的步驟？試著將腳本改寫成支援其他副檔名（例如 `.bin` 或 `.ckpt`），或將其整合到每次模型下載後執行的更大型清理流程中。你也可以探索 `pathlib` 以獲得更物件導向的寫法，或使用 `cron`/`Task Scheduler` 排程腳本，讓工作區自動保持整潔。

對於邊緣案例有疑問，或想了解在 Windows 與 Linux 上的執行情形？歡迎在下方留言，祝清理愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}