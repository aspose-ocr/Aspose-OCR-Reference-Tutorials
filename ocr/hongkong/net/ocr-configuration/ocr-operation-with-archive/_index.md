---
date: 2025-12-19
description: 了解如何使用 Aspose.OCR for .NET 對封存圖像執行光學字符辨識、將圖像轉換為文字，以及從封存檔案中擷取文字。
linktitle: How to Perform OCR on Archive Images with Aspose.OCR for .NET
second_title: Aspose.OCR .NET API
title: 如何使用 Aspose.OCR for .NET 對存檔圖像執行 OCR
url: /zh-hant/net/ocr-configuration/ocr-operation-with-archive/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose.OCR for .NET 執行壓縮檔影像的 OCR

## 介紹

在本完整教學中，您將了解 **如何執行 OCR** 對壓縮檔影像檔使用 Aspose.OCR 函式庫 for .NET。無論您需要 **將影像轉換為文字** 或 **從壓縮檔中擷取文字**，以下逐步指南將帶您完成所有步驟——從設定開發環境到從 ZIP 壓縮檔內的每張影像取得辨識文字。

## 快速解答
- **本教學涵蓋什麼內容？** 使用 Aspose.OCR for .NET 對壓縮檔 (ZIP) 影像執行 OCR。  
- **目標的主要關鍵字是什麼？** *how to perform ocr*。  
- **需要授權嗎？** 免費試用可用於評估；正式上線需購買商業授權。  
- **支援哪些 .NET 版本？** .NET Framework 4.5 以上、.NET Core 3.1 以上、.NET 5/6 以上。  
- **可以自訂辨識設定嗎？** 可以——使用 `RecognitionSettings` 來調整準確度。

## OCR 是什麼以及為何在壓縮檔上使用？

光學字符辨識（OCR）將掃描的影像或 PDF 轉換為可搜尋、可編輯的文字。當影像被打包在壓縮檔（例如 ZIP 檔）中時，一次性抽取並辨識每張圖片可節省時間並降低程式碼複雜度。Aspose.OCR 的 `RecognizeMultipleImages` 方法讓此流程變得簡單。

## 前置條件

- Visual Studio 2019 或更新版本（或任何相容 .NET 的 IDE）。  
- 已安裝 .NET Framework 4.5 以上或 .NET Core 3.1 以上。  
- 取得 Aspose.OCR for .NET 函式庫（下載連結見下方）。  
- 用於正式環境的有效 Aspose.OCR 授權（提供試用版）。

## 匯入命名空間

在您的 .NET 專案中，請確保匯入必要的命名空間，以存取 Aspose.OCR 提供的功能：

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## 下載與安裝 Aspose.OCR for .NET

從發行頁面 **[此處](https://releases.aspose.com/ocr/net/)** 取得最新套件，並依照標準的 NuGet 或手動安裝步驟進行。

## 取得授權

從 **[購買頁面](https://purchase.aspose.com/buy)** 取得授權，或使用 **[免費試用](https://releases.aspose.com/)**。將授權檔案放置於專案根目錄，並依照 Aspose 文件於執行時載入。

## 步驟 1：設定文件目錄

首先初始化文件目錄的路徑：

```csharp
// ExStart:1
// The path to the documents directory.
string dataDir = "Your Document Directory";
// ExEnd:1
```

> **小技巧：** 使用 `Path.Combine` 以處理跨平台路徑。

## 步驟 2：初始化 Aspose.OCR

建立 Aspose.OCR 類別的實例，以啟動 OCR 作業：

```csharp
// ExStart:3
AsposeOcr api = new AsposeOcr();
// ExEnd:3
```

## 步驟 3：指定影像路徑

定義壓縮檔影像的完整路徑（即包含您欲讀取圖片的 ZIP 檔）：

```csharp
// ExStart:4
string fullPath = dataDir + "OCR.zip";
// ExEnd:4
```

## 步驟 4：辨識影像

使用預設或自訂設定對指定的壓縮檔執行 OCR 辨識。此呼叫會自動從 ZIP 中抽取每張影像並執行 OCR：

```csharp
// ExStart:5
RecognitionResult[] result = api.RecognizeMultipleImages(fullPath, new RecognitionSettings
{
   //default or custom settings
});
// ExEnd:5
```

> 您可以調整 `RecognitionSettings` 以提升特定語言或影像品質的準確度。

## 步驟 5：輸出結果

遍歷結果，並列印壓縮檔內每張影像的辨識文字：

```csharp
// ExStart:6
for (int i = 0; i < result.Length; i++)
{
	 Console.WriteLine($"Image: {i}\n Result:\n {result[i].RecognitionText}");
}
// ExEnd:6
```

輸出會顯示每張影像的索引以及對應的擷取字串，實際上 **將影像轉換為文字** 並 **從壓縮檔中擷取文字**。

## 常見問題與故障排除

| 問題 | 原因 | 解決方案 |
|------|------|----------|
| 未返回文字 | 影像品質過低 | 預先處理影像（例如二值化）或調整 `RecognitionSettings.Dpi` |
| 讀取 ZIP 時發生例外 | 壓縮檔路徑無效 | 確認 `fullPath` 指向有效的 `.zip` 檔，且應用程式具有讀取權限 |
| 授權未套用 | 授權檔案遺失或未載入 | 在建立 `AsposeOcr` 實例之前，呼叫 `License license = new License(); license.SetLicense("Aspose.OCR.lic");` |

## 常見問答

**Q: 可以在沒有授權的情況下使用 Aspose.OCR for .NET 嗎？**  
A: 可以，提供免費試用供評估使用，但正式部署需使用授權版本。

**Q: 此函式庫支援受密碼保護的 ZIP 壓縮檔嗎？**  
A: 目前 `RecognizeMultipleImages` 只支援一般的 ZIP 檔。若為加密壓縮檔，請先使用第三方函式庫抽取影像，然後將影像陣列傳給 OCR 引擎。

**Q: 如何提升手寫文字的辨識準確度？**  
A: 開啟 `RecognitionSettings.EnableHandwritingRecognition` 旗標，並提供較高的 DPI 設定（例如 300）。

**Q: 有辦法取得每行辨識的信心分數嗎？**  
A: 每個 `RecognitionResult` 都包含 `Confidence` 屬性，您可以將其記錄或用於過濾低信心的結果。

## 結論

現在您已擁有完整、可投入生產環境的工作流程，能使用 Aspose.OCR for .NET **對壓縮檔影像執行 OCR**、**將影像轉換為文字**，以及 **從壓縮檔中擷取文字**。將此功能整合至您的應用程式，即可實現可搜尋的文件庫、自動化資料輸入，或任何需要大量影像文字擷取的情境。

## 其他資源

- **Aspose.OCR 論壇：** 如需社群支援與進階情境，請造訪 [Aspose.OCR 論壇](https://forum.aspose.com/c/ocr/16)。  
- **臨時授權：** 若需要短期評估，請申請 [臨時授權](https://purchase.aspose.com/temporary-license/)。  
- **官方文件：** 透過檢閱 [文件](https://reference.aspose.com/ocr/net/) 以掌握最新 API 變更。

---

**最後更新時間：** 2025-12-19  
**測試環境：** Aspose.OCR 24.11 for .NET  
**作者：** Aspose

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
