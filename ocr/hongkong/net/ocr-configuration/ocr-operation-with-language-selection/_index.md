---
date: 2025-12-21
description: 學習如何使用 Aspose.OCR for .NET 執行 OCR，並從圖像中擷取文字。此一步一步的指南展示多語言文字辨識與語言選擇。
linktitle: How to Perform OCR with Language Selection in Aspose.OCR
second_title: Aspose.OCR .NET API
title: 如何在 Aspose.OCR 中使用語言選擇執行 OCR
url: /zh-hant/net/ocr-configuration/ocr-operation-with-language-selection/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Aspose.OCR 中執行具語言選擇的 OCR

## Introduction

如果您需要 **how to perform OCR** 圖像並從圖像檔案中提取文字，Aspose.OCR for .NET 提供快速、精確且具語言感知的解決方案。在本教學中，我們將透過一個實際範例示範具語言選擇的 OCR 圖像辨識，讓您只需幾行程式碼即可從圖片中擷取多語言文字。

## Quick Answers
- **What does Aspose.OCR do?** 它會辨識圖像中的印刷文字與手寫文字，並回傳擷取出的文字。  
- **Can I choose the language?** 是的 – 您可以指定任何支援的語言，例如 English、German、Spanish、Chinese 等。  
- **Do I need a license for development?** 免費試用版可用於評估；正式使用則需要授權。  
- **Which .NET versions are supported?** .NET Framework 4.5 以上、.NET Core 3.1 以上、.NET 5/6 以上。  
- **Is skew correction automatic?** 您可以啟用 `AutoSkew`，並微調 `SkewAngle` 設定。

## Why Choose Aspose.OCR for OCR Tasks?

- **High accuracy** 在多種字型與圖像品質下皆具高準確度。  
- **Built‑in language selection** 消除對外部語言套件的需求。  
- **Simple API** 可順利整合至現有的 C# 專案。  
- **No external dependencies** – 所有功能皆在本機執行，確保資料安全。

## Prerequisites

在深入程式碼之前，請確保已具備以下前置條件：

- Aspose.OCR for .NET：確保已安裝 Aspose.OCR 程式庫。您可從 [Aspose.OCR for .NET download page](https://releases.aspose.com/ocr/net/) 下載。  
- Development Environment：建立具 .NET 應用程式的工作環境。若尚未完成，請參考 [documentation](https://reference.aspose.com/ocr/net/) 取得詳細說明。

## Import Namespaces

在您的 .NET 應用程式中，首先匯入必要的命名空間：

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Step 1: Initialize Aspose.OCR

步驟 1：初始化 Aspose.OCR

首先建立 Aspose.OCR 類別的實例，為在應用程式中使用 OCR 功能做好準備。

```csharp
// ExStart:1
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Step 2: Specify Image Path

步驟 2：指定影像路徑

接著，定義要執行 OCR 的影像路徑，確保影像可被應用程式存取。

```csharp
// Image Path
string fullPath = dataDir + "sample.png";
```

## Step 3: Recognize Image with Language Selection

步驟 3：使用語言選擇辨識影像

現在進入核心的 OCR 操作。使用 Aspose.OCR 程式庫辨識指定影像中的文字，並調整辨識設定，包括語言選擇。

```csharp
// Recognize image           
RecognitionResult result = api.RecognizeImage(fullPath, new RecognitionSettings
{
    DetectAreas = true,
    RecognizeSingleLine = false,
    AutoSkew = true,
    SkewAngle = 0.2F,
    Language = Language.Eng, // Choose the language: none, eng, deu, por, spa, fra, ita, cze, dan, dum, est, fin, lav, lit, nor, pol, rum, srp_hrv, slk, slv, swe, chi
});
```

## Step 4: Print and Display Results

步驟 4：列印與顯示結果

OCR 完成後，列印並顯示結果，包括辨識出的文字、區域、警告以及 JSON 表示。

```csharp
// Print result
Console.WriteLine($"Text:\n {result.RecognitionText}");
Console.WriteLine("Areas:");
result.RecognitionAreasText.ForEach(a => Console.WriteLine($"{a}"));
Console.WriteLine("Warnings:");
result.Warnings.ForEach(w => Console.WriteLine($"{w}"));
Console.WriteLine($"JSON: {result.GetJson()}");
// ExEnd:1
```

## Common Issues and Tips

常見問題與技巧

- **Incorrect language selection** – 若輸出文字呈現亂碼，請再次確認 `Language` 屬性與來源影像的語言相符。  
- **Skewed images** – 啟用 `AutoSkew` 或手動調整 `SkewAngle`，以提升斜掃描圖像的辨識準確度。  
- **Large files** – 將大型影像分段處理或降低解析度後再傳入 `RecognizeImage`，以節省記憶體。

## Conclusion

結論

恭喜！您已學會使用 Aspose.OCR for .NET 進行具語言選擇的 **how to perform OCR**。本教學示範了如何從影像檔案中擷取文字、客製化辨識設定，並輕鬆處理多語言內容。

## FAQ's

### Q1: Is Aspose.OCR suitable for multilingual text recognition?

A1：是的，Aspose.OCR 支援多種語言，為多語言 OCR 任務提供彈性。

### Q2: Can I fine‑tune OCR settings for specific image characteristics?

A2：當然可以！調整斜角、行辨識、區域偵測等參數，以優化不同情境下的 OCR 效果。

### Q3: Where can I find additional support or community discussions?

A3：請前往 [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) 獲取支援並與社群討論。

### Q4: Is there a free trial available?

A4：是的，請探索 [free trial](https://releases.aspose.com/) 體驗 Aspose.OCR 的功能。

### Q5: How can I purchase Aspose.OCR for .NET?

A5：購買請前往 [purchase page](https://purchase.aspose.com/buy)。

---

**Last Updated:** 2025-12-21  
**Tested With:** Aspose.OCR 24.11 for .NET  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}