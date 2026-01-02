---
date: 2026-01-02
description: 學習如何使用 Aspose.OCR for .NET 取得 OCR 字元選項。本指南逐步說明如何在圖像辨識中取得字元備選。
linktitle: Get Choices for Recognized Characters in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: 如何取得圖像辨識中已辨識字元的 OCR 字元選項
url: /zh-hant/net/text-recognition/get-choices-for-recognized-characters/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 取得 OCR 圖像辨識中已辨識字元的候選項目

## 簡介

在現代 .NET 應用程式中釋放光學字元辨識 (OCR) 的威力，並學習 **如何取得每個已辨識符號的 OCR 字元候選項目**。Aspose.OCR for .NET 讓此過程變得簡單，除了提供最佳猜測的文字外，還會給出引擎考慮的替代字元。完成本教學後，您將能將此功能整合至任何 C# 專案，並改善對模糊字形的處理。

## 快速答案
- **「取得 OCR 字元候選項目」是什麼意思？** 它會回傳每個已辨識字形的替代字元清單。  
- **為什麼要使用字元候選項目？** 用於處理不確定的辨識結果、執行後處理，或實作自訂驗證。  
- **事前需要什麼？** .NET 開發環境、Visual Studio，以及 Aspose.OCR for .NET 函式庫。  
- **是否需要授權？** 免費試用可用於測試；正式上線需購買商業授權。  
- **可以在 .NET Core / .NET 6 上執行嗎？** 可以，Aspose.OCR 支援所有現代 .NET 執行環境。

## 什麼是「取得 OCR 字元候選項目」？
當 OCR 引擎分析圖像時，每個像素模式可能對應多個可能的字元。**取得 OCR 字元候選項目** API 會公開這些替代選項，讓開發者自行決定哪個字元最符合當前情境。

## 為什麼使用 Aspose.OCR for .NET？
- **高精準度**，支援多種語言與字型。  
- **易於整合**，提供簡單的 C# API。  
- **可透過 `RecognitionCharactersList` 取得字元替代項目**。  
- **無外部相依** – 可直接在 Windows、Linux 與 macOS 上執行。

## 先決條件

在開始本教學之前，請確保您具備以下條件：

- 具備 C# 與 .NET 開發的基礎知識。  
- 機器上已安裝 Visual Studio。  
- Aspose.OCR for .NET 函式庫，可於 [此處](https://releases.aspose.com/ocr/net/) 下載。

## 匯入命名空間

在您的 C# 專案中，先匯入必要的命名空間：

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## 步驟 1：初始化 Aspose.OCR

先建立 Aspose.OCR 的實例：

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## 步驟 2：指定圖像路徑

設定欲分析圖像的路徑：

```csharp
// Image Path
string fullPath = dataDir + "sample.png";
```

## 步驟 3：辨識圖像

執行圖像辨識程序：

```csharp
// Recognize image           
RecognitionResult result = api.RecognizeImage(fullPath, new RecognitionSettings
{
    // Default or custom settings
});
```

## 取得 OCR 字元候選項目 – 概觀

圖像已完成辨識後，您可以取得 OCR 引擎對每個位置所考慮的字元替代清單。

## 步驟 4：取得已辨識字元的候選項目

取得已辨識字元的候選項目：

```csharp
List<char[]> resultWithChoices = result.RecognitionCharactersList;
```

## 步驟 5：列印結果

顯示辨識文字與候選項目：

```csharp
// Print result
Console.WriteLine($"Text:\n {result.RecognitionText}");
Console.WriteLine("Choices:");
resultWithChoices.ForEach(a => Console.WriteLine($"character: {a[0]} . Choices: {a[1]} {a[2]} {a[3]} {a[4]}"));

Console.WriteLine("GetChoiceForRecognizedCharacters executed successfully");
```

依照應用程式需求重複上述步驟並自行客製化。

## 常見問題與解決方案

- **`RecognitionCharactersList` 為空** – 請確認圖像具備足夠的解析度與對比度。  
- **出現非預期字元** – 調整 `RecognitionSettings`（例如語言、字典）以提升精準度。  
- **效能問題** – 可使用非同步處理或批次辨識多張圖像，以保持 UI 響應。

## 常見問答

### Q1：Aspose.OCR for .NET 是否適用於大規模文件處理？

A1：絕對可以！Aspose.OCR for .NET 專為高效且精準地處理大量文件而設計。

### Q2：我可以在 Web 應用程式中使用 Aspose.OCR for .NET 嗎？

A2：可以，您可以將 Aspose.OCR for .NET 整合至 Web 應用程式，適用於各種開發情境。

### Q3：Aspose.OCR for .NET 有哪些授權方案？

A3：有，您可於 [此處](https://purchase.aspose.com/buy) 了解授權方案並購買。

### Q4：如何取得 Aspose.OCR for .NET 的支援或提問？

A4：請前往 [Aspose.OCR 論壇](https://forum.aspose.com/c/ocr/16) 取得支援、提問並與社群交流。

### Q5：是否提供 Aspose.OCR for .NET 的免費試用？

A5：有，您可於 [此處](https://releases.aspose.com/) 取得免費試用，體驗 Aspose.OCR for .NET 的功能。

## 結論

在本教學中，我們探討了如何使用 Aspose.OCR for .NET **取得 OCR 字元候選項目**。此功能為您的 OCR 能力增添新維度，讓您能更智慧地處理模糊字元並實作更豐富的後處理邏輯。

---

**Last Updated:** 2026-01-02  
**Tested With:** Aspose.OCR 24.11 for .NET  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}