---
category: general
date: 2026-01-12
description: 學習如何透過列出本機模型，以清晰的 Python 範例顯示 AsposeAI 的資訊，展示模型名稱、大小及最後使用時間戳記。
draft: false
keywords:
- how to display info
- list local models
- display model name
- show model size
- show last used
language: zh-hant
og_description: 如何顯示 AsposeAI 的資訊：列出本機模型，顯示模型名稱、大小及最後使用時間戳記，並提供完整的 Python 教學示範。
og_title: 如何顯示資訊 – 列出本機模型、名稱、大小、最後使用時間
tags:
- AsposeAI
- Python
- Model Management
title: 如何顯示資訊 – 列出本地模型、名稱、大小、最後使用時間
url: /zh-hant/python/general/how-to-display-info-list-local-models-name-size-last-used/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何顯示資訊 – 列出本機模型、名稱、大小、最後使用時間

有沒有想過 **如何顯示資訊** 從你的 AsposeAI 安裝中，而不必翻閱日誌或使用者介面？你並不是唯一有此疑問的人。在許多資料科學工作流程中，你首先需要的是快速瀏覽機器上有哪些模型、它們的名稱、大小以及最後一次使用的時間。

這正是我們要討論的內容：一段簡潔、端到端的 Python 程式碼，能 **列出本機模型**，接著 **顯示模型名稱**、**顯示模型大小**，以及 **顯示最後使用時間**。不需要額外的函式庫，沒有隱藏的魔法——只使用你已經擁有的 AsposeAI 客戶端。

完成本教學後，你就能把程式碼放入任何腳本中執行，立即取得本機快取模型的整齊表格。它非常適合檢查環境狀態、建立健康儀表板，或僅僅滿足對磁碟上隱藏內容的好奇心。

## Prerequisites

- Python 3.8 或更新版本（範例使用 f‑strings，故最低需 3.6+）
- `asposeai` 套件已安裝（`pip install asposeai`）
- 有效的 AsposeAI 授權或試用金鑰（客戶端會從環境變數或設定檔中取得憑證）

如果你已經確認以上條件，太好了——讓我們開始吧。

## 第一步：如何顯示資訊 – 初始化 AsposeAI 客戶端

在我們能 **列出本機模型** 之前，需要一個能與 AsposeAI 執行環境溝通的客戶端物件。這一步是基礎；若缺少它，後續程式碼會拋出 `NameError`。

```python
# Step 1: Create an instance of the AsposeAI client
# The client automatically reads credentials from the environment
aspose_ai = AsposeAI()
```

*為什麼這很重要*：初始化客戶端會與本機推論引擎建立會話，載入任何必要的原生函式庫。它同時會驗證你的授權是否有效，避免日後查詢模型時出現難以理解的錯誤。

> **專業提示**：如果在 CI 伺服器上執行，請在環境變數中設定 `ASPOSEAI_LICENSE`，讓客戶端能在不需要互動提示的情況下啟動。

## 第二步：列出本機模型 – 取得可用模型

現在客戶端已就緒，我們可以 **列出本機模型**。`list_local()` 方法會回傳一系列物件，每個物件都提供 `name`、`size_mb` 與 `last_used` 等屬性。

```python
# Step 2: Retrieve the list of locally available models
local_models = aspose_ai.list_local()
```

*背後的運作*：`list_local()` 會掃描 AsposeAI 快取模型檔案的目錄（預設為 `~/.asposeai/models`），並建立輕量的中繼資料物件。此過程很快，因為它不會載入模型權重——只會讀取一個小型的 JSON 清單。

如果你想確認某個特定模型是否已快取，這個呼叫是最快的方式。

## 第三步：顯示模型名稱、顯示模型大小與顯示最後使用時間

取得模型清單後，我們最終透過遍歷集合並印出每個屬性來 **顯示資訊**。在這裡，我們會 **顯示模型名稱**、**顯示模型大小**，以及 **顯示最後使用時間**，全部呈現在同一行。

```python
# Step 3: Print each model's name, size (in MB), and last‑used timestamp
print("Available local models:")
print("-" * 50)
for model_info in local_models:
    # Using an f‑string to format the output cleanly
    print(f"{model_info.name} – {model_info.size_mb} MB – last used {model_info.last_used}")
```

**預期輸出**（你的時間戳記會不同）：

```
Available local models:
--------------------------------------------------
gpt‑tiny‑en – 120 MB – last used 2025-11-02 14:23:11
bert‑base‑fr – 420 MB – last used 2025-10-18 09:07:45
whisper‑large‑audio – 1580 MB – last used 2025-09-30 22:41:02
```

*為什麼這樣格式化*：破折號（`–`）用來分隔欄位以提升可讀性，標題列則讓控制台輸出更易掃描。若之後需要機器可讀的格式（CSV、JSON），只要把 `print` 換成 `writer.writerow` 或 `json.dump` 即可。

### 處理例外情況

- **未快取任何模型** – `list_local()` 會回傳空清單。迴圈會直接跳過，只留下標題列。你可能想加入防護機制：

  ```python
  if not local_models:
      print("No local models found. Use aspose_ai.download(...) to fetch one.")
  ```

- **屬性缺失** – 在少數情況下清單可能損壞。存取 `model_info.last_used` 可能拋出 `AttributeError`。若預期會有此類問題，請將印出動作包在 `try/except` 中。

- **大型模型目錄** – 若有數百個模型，建議分頁輸出或寫入檔案，而非直接印到終端機。

## 視覺摘要（可選）

如果你喜歡快速的視覺提示，下圖說明了從客戶端初始化到最終顯示的流程。

![顯示 AsposeAI 客戶端資訊的流程圖](/images/how-to-display-info.png "如何顯示資訊圖示")

*替代文字*：**如何顯示資訊** – AsposeAI 客戶端初始化、模型列舉與資訊顯示的示意圖。

## 完整可執行腳本

將所有步驟整合起來，以下是完整、可直接執行的腳本：

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

"""
How to display info from AsposeAI:
List local models and show each model's name, size, and last‑used timestamp.
"""

from asposeai import AsposeAI

def main():
    # Initialize client
    aspose_ai = AsposeAI()

    # Retrieve local models
    local_models = aspose_ai.list_local()

    # Header
    print("Available local models:")
    print("-" * 50)

    if not local_models:
        print("No local models found. Use aspose_ai.download(...) to fetch one.")
        return

    # Display each model's details
    for model_info in local_models:
        try:
            print(f"{model_info.name} – {model_info.size_mb} MB – last used {model_info.last_used}")
        except AttributeError:
            # Fallback if any attribute is missing
            print(f"{model_info.name} – info incomplete")

if __name__ == "__main__":
    main()
```

將其儲存為 `list_models.py`，設定可執行權限（`chmod +x list_models.py`），然後執行：

```bash
./list_models.py
```

你會看到先前示範的整齊清單。

## 結論

我們已說明如何 **顯示資訊** 從 AsposeAI，透過 **列出本機模型**，再 **顯示模型名稱**、**顯示模型大小** 與 **顯示最後使用時間**。此方法輕量、僅需標準的 `asposeai` 套件，且可直接嵌入任何自動化流程或除錯環節。

接下來你可以：

- 將輸出匯出為 CSV 以供試算表分析（使用 `csv` 模組）。
- 將時間戳記輸入監控儀表板，以提醒過時的模型。
- 將此腳本與 `aspose_ai.download()` 結合，自動更新長時間未使用的模型。

請記住，清晰掌握模型清單可節省時間、減少儲存空間浪費，並讓 AI 服務順暢運作。試跑此腳本，依需求調整格式，讓它成為你工具箱中的必備利器。

祝程式開發順利，願你的模型永遠保持最新！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}