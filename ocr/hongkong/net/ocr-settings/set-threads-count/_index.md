---
date: 2025-12-25
description: 在 .NET 中釋放 OCR 效率，透過 Aspose.OCR 設定執行緒數量提升 OCR 準確度。加快速度與精準度。
linktitle: Set Threads Count to Improve OCR Accuracy
second_title: Aspose.OCR .NET API
title: 設定執行緒數量以提升 .NET 中的 OCR 準確度
url: /zh-hant/net/ocr-settings/set-threads-count/
weight: 11
---

{{< blocks/products/pf/main-container >}}
{{< /blocks/products/pf/tutorial-page-section >}}
{{< blocks/products/pf/main-wrap-class >}}

# 設定執行緒數量以提升 OCR 準確度

## 介紹

歡迎來到 Aspose.OCR for .NET 的世界，這裡最先進的光學字符識別（OCR）技術與您 .NET 應用程式的無縫整合相結合。在本教學中，您將學習 **如何設定執行緒數量** 以 **提升 OCR 準確度**，同時保持處理速度快且資源友好。

## 快速解答
- **ThreadsCount 有什麼作用？** 它告訴 Aspose.OCR 在圖像分析期間使用多少平行執行緒。  
- **為什麼要手動設定？** 調整執行緒數量可以在多核心機器上 **提升 OCR 準確度**，並避免 CPU 節流。  
- **預設行為？** 設為 `0` 時，Aspose.OCR 會自動計算最佳執行緒數量。  
- **常見範圍？** 1 – 8 個執行緒適用於大多數桌面情境；較高的數值對多核心伺服器有益。  
- **先決條件？** .NET（Framework 4.5+ 或 .NET Core 3.1+）、Aspose.OCR for .NET，以及一張範例圖像。

## 什麼是 OCR 中的執行緒數量？

執行緒數量決定 Aspose.OCR 在辨識文字時會分配多少個同時處理單元。更多的執行緒可以加速大批量處理，且在與 CPU 資源適當平衡時，透過減少逾時與記憶體壓力，**提升 OCR 準確度**。

## 為什麼設定執行緒數量可以提升 OCR 準確度？

- **更佳的資源利用率：** 將執行緒數量與 CPU 核心匹配，可防止 OCR 引擎資源不足或過度佔用。  
- **降低延遲：** 平行處理縮短每張圖像在辨識流程中的時間，讓演算法有更多時間套用完整的準確模型。  
- **可擴展性：** 在伺服器端情境中，您可以微調執行緒池，以處理大量同時請求而不犧牲精度。

## 先決條件

在開始之前，請確保您已具備以下項目：

- 已安裝 Aspose.OCR for .NET。若尚未下載，您可以在 **[此處](https://releases.aspose.com/ocr/net/)** 取得。  
- 一張範例圖像放置於您的文件目錄中（例如 `sample.png`）。

## 匯入命名空間

首先，在您的 .NET 專案中加入必要的命名空間：

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

## 步驟 1：初始化 Aspose.OCR 實例

建立一個 `AsposeOcr` 物件，並指向保存圖像的資料夾：

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## 步驟 2：使用自訂執行緒數量辨識圖像

現在告訴 OCR 引擎使用多少執行緒。將 `ThreadsCount` 設為大於 0 的值，即可直接控制，並能在高負載工作中 **提升 OCR 準確度**。

```csharp
// Recognize image
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings
{
    ThreadsCount = 2 // 0 - means auto calculate
});
```

## 步驟 3：顯示辨識文字

最後，將辨識出的文字輸出至主控台或您偏好的任何其他 UI 元件）：

```csharp
// Display the recognized text
Console.WriteLine(result.RecognitionText);
```

## 常見問題與技巧

| 問題 | 發生原因 | 解決方案 |
|------|----------|----------|
| **執行緒過多導致高 CPU 使用率** | 每個執行緒都在爭奪相同的核心。 | 先將 `ThreadsCount = Environment.ProcessorCount / 2` 作為起點，並根據監控結果調整。 |
| **在大型圖像上辨識失敗** | 多個平行執行緒造成記憶體壓力。 | 減少 `ThreadsCount` 或增加可用記憶體。 |
| **意外的低準確度** | 自動計算的執行緒數量可能對您的硬體而言過低。 | 手動設定較高的 `ThreadsCount` 並測試輸出。 |

## 常見問答

### Q1：我可以將執行緒數量設為 0 以自動計算嗎？

**A：** 當然可以！將 `ThreadsCount` 設為 `0`，Aspose.OCR 會自動判斷當前環境的最佳執行緒數量。

### Q2：我如何取得 Aspose.OCR for .NET 的臨時授權？

**A：** 前往 **[此連結](https://purchase.aspose.com/temporary-license/)** 取得測試用的臨時授權。

### Q3：我可以在哪裡找到 Aspose.OCR for .NET 的完整文件？

**A：** 請參考 **[文件](https://reference.aspose.com/ocr/net/)** 以取得 Aspose.OCR 的詳細說明。

### Q4：Aspose.OCR for .NET 是否提供免費試用？

**A：** 是的，您可在 **[此處](https://releases.aspose.com/)** 探索免費試用。

### Q5：需要協助或想與社群聯繫？

**A：** 前往 **[Aspose.OCR 論壇](https://forum.aspose.com/c/ocr/16)** 取得支援並與社群互動。

## 結論

設定 **執行緒數量** 是在您的 .NET 應用程式中 **提升 OCR 準確度** 與效能的簡單且強大方法。嘗試不同的數值，監控 CPU 與記憶體使用情況，選擇能在速度與精確度之間取得最佳平衡的配置。

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
{{< /blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

---

**最後更新：** 2025-12-25  
**測試環境：** Aspose.OCR 24.11 for .NET  
**作者：** Aspose  

---