---
title: 在 OCR 影像辨識中取得已辨識字元的選擇
linktitle: 在 OCR 影像辨識中取得已辨識字元的選擇
second_title: Aspose.OCR .NET API
description: 使用 Aspose.OCR 增強您的 .NET 應用程序，以實現準確的字元辨識。請依照我們的逐步指南檢索影像辨識中已辨識字元的選擇。
weight: 10
url: /zh-hant/net/text-recognition/get-choices-for-recognized-characters/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 OCR 影像辨識中取得已辨識字元的選擇

## 介紹

在當今的數位時代，釋放光學字元辨識 (OCR) 的力量至關重要，而 Aspose.OCR for .NET 是準確字元辨識的強大解決方案。在本教程中，我們將深入研究一個特定功能：取得已識別字元的選擇。在本指南結束時，您將將此功能無縫整合到您的 .NET 應用程式中。

## 先決條件

在深入學習本教程之前，請確保您具備以下先決條件：

- C# 和 .NET 開發的基礎知識。
- Visual Studio 安裝在您的電腦上。
-  Aspose.OCR for .NET 函式庫，您可以下載[這裡](https://releases.aspose.com/ocr/net/).

## 導入命名空間

在您的 C# 專案中，首先匯入必要的命名空間：

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## 步驟1：初始化Aspose.OCR

首先初始化 Aspose.OCR 的例子：

```csharp
//文檔目錄的路徑。
string dataDir = "Your Document Directory";

//初始化 AsposeOcr 實例
AsposeOcr api = new AsposeOcr();
```

## 第2步：指定影像路徑

設定要分析的影像的路徑：

```csharp
//影像路徑
string fullPath = dataDir + "sample.png";
```

## 第三步：辨識影像

執行影像辨識過程：

```csharp
//辨識影像
RecognitionResult result = api.RecognizeImage(fullPath, new RecognitionSettings
{
    //預設或自訂設定
});
```

## 第 4 步：取得已識別字元的選擇

檢索已識別字元的選擇：

```csharp
List<char[]> resultWithChoices = result.RecognitionCharactersList;
```

## 第 5 步：列印結果

顯示識別文字和選項：

```csharp
//列印結果
Console.WriteLine($"Text:\n {result.RecognitionText}");
Console.WriteLine("Choices:");
resultWithChoices.ForEach(a => Console.WriteLine($"character: {a[0]} . Choices: {a[1]} {a[2]} {a[3]} {a[4]}"));

Console.WriteLine("GetChoiceForRecognizedCharacters executed successfully");
```

重複這些步驟，根據您的應用程式的要求進行自訂。

## 結論

在本教學中，我們探討如何利用 Aspose.OCR for .NET 來取得影像辨識中已辨識字元的選擇。此功能為您的 OCR 功能增添了新的維度，增強了應用程式的多功能性。

## 常見問題解答

### Q1：Aspose.OCR for .NET適合大規模文件處理嗎？

A1：當然！ Aspose.OCR for .NET 旨在高效、準確地處理大量文件。

### Q2：我可以在 Web 應用程式中使用 Aspose.OCR for .NET 嗎？

A2：是的，您可以將 Aspose.OCR for .NET 整合到 Web 應用程式中，使其適用於各種開發場景。

### 問題 3：Aspose.OCR for .NET 有可用的授權選項嗎？

 A3：是的，您可以探索授權選項並進行購買[這裡](https://purchase.aspose.com/buy).

### 問題 4：如何獲得 Aspose.OCR for .NET 的支援或提問？

 A4：訪問[Aspose.OCR 論壇](https://forum.aspose.com/c/ocr/16)獲得支持、提出問題並與社區建立聯繫。

### Q5：Aspose.OCR for .NET 有免費試用版嗎？

 A5：是的，您可以免費試用[這裡](https://releases.aspose.com/)體驗 Aspose.OCR for .NET 的功能。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
