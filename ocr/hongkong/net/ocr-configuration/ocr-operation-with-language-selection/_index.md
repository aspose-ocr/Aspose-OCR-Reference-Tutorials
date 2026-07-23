---
date: 2026-07-23
description: 了解如何使用 Aspose.OCR 讓 ocr library for .net 提取圖像文字 C#。本指南涵蓋多語言 OCR、語言選擇及實用技巧。
keywords:
- ocr library for .net
- extract image text c#
- Aspose.OCR
- multilingual OCR
lastmod: 2026-07-23
linktitle: 使用 Aspose.OCR 進行語言選擇，提取圖像文字 C#
og_description: ocr library for .net 可使用 Aspose.OCR 提取圖像文字 C#。提供多語言 OCR、語言選擇及一步一步的程式碼範例。
og_image_alt: 'Guide: Extract image text C# using Aspose.OCR OCR library for .NET'
og_title: ocr library for .net – 提取圖像文字 C#
schemas:
- author: Aspose
  dateModified: '2026-07-23'
  description: Learn how the ocr library for .net extracts image text C# using Aspose.OCR.
    This guide covers multilingual OCR, language selection, and practical tips.
  headline: ocr library for .net – Extract image text C#
  type: TechArticle
- questions:
  - answer: Yes, Aspose.OCR supports over 30 languages, providing flexibility for
      multilingual OCR tasks.
    question: Is Aspose.OCR suitable for multilingual text recognition?
  - answer: Absolutely! Adjust parameters like `AutoSkew`, `SkewAngle`, and `LineDetectionMode`
      to optimise results for different scenarios.
    question: Can I fine‑tune OCR settings for specific image characteristics?
  - answer: Visit the [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) for support
      and discussions with the community.
    question: Where can I find additional support or community discussions?
  - answer: Yes, explore the [free trial](https://releases.aspose.com/) to experience
      the capabilities of Aspose.OCR.
    question: Is there a free trial available?
  - answer: To purchase, visit the [purchase page](https://purchase.aspose.com/buy).
    question: How can I purchase Aspose.OCR for .NET?
  type: FAQPage
second_title: Aspose.OCR .NET API
tags:
- ocr library
- Aspose.OCR
- C# OCR
- image text extraction
title: ocr library for .net – 提取圖像文字 C#
url: /zh-hant/net/ocr-configuration/ocr-operation-with-language-selection/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.OCR 進行語言選擇的 C# 圖像文字提取

## 簡介

如果您需要在 .NET 應用程式中 **extract image text C#** 從圖片或 PDF 中提取文字，Aspose.OCR 是一個功能強大的 **ocr library for .net**，提供快速、準確且支援語言感知的辨識。在本教學中，我們將示範一個真實案例，展示具語言選擇的 OCR 圖像辨識，讓您只需幾行程式碼即可從圖像中提取多語言文字。最後，您將了解為何此方法是生產工作負載的可靠選擇，以及將 OCR 整合到 C# 專案中有多麼簡單。

## 快速回答
- **What does Aspose.OCR do?** 它能辨識圖像中的印刷文字與手寫文字，並返回提取的文字。  
- **Can I choose the language?** 是的——您可以指定任何支援的語言，例如 English、German、Spanish、Chinese 等。  
- **Do I need a license for development?** 免費試用可用於評估；正式使用則需購買授權。  
- **Which .NET versions are supported?** 支援 .NET Framework 4.5+、.NET Core 3.1+、.NET 5/6+。  
- **Is skew correction automatic?** 您可以啟用 `AutoSkew` 並微調 `SkewAngle` 設定。  

`AutoSkew` 會自動偵測並校正圖像傾斜。`SkewAngle` 允許手動調整旋轉角度。

## 什麼是「extract image text C#」？

在 C# 中提取圖像文字是指使用函式庫讀取圖像（PNG、JPEG、TIFF 等）的視覺內容，並將其轉換為可搜尋、可編輯的文字。**ocr library for .net** Aspose.OCR 在本機執行此轉換，資料保留於本地，避免呼叫外部服務。

## 為何選擇 Aspose.OCR 進行 OCR 任務？

Aspose.OCR 在標準印刷字體上提供 **95 %+ accuracy**，且在一般 2.5 GHz 伺服器上每分鐘可處理 **up to 300 pages per minute**，使其成為最快的 **ocr library for .net** 解決方案之一。它還內建語言套件，無需第三方資源，且完全離線執行，確保最高安全性。

## 先決條件

在深入程式碼之前，請確保已具備以下先決條件：

- Aspose.OCR for .NET：確保已安裝 Aspose.OCR 函式庫。您可從 [Aspose.OCR for .NET download page](https://releases.aspose.com/ocr/net/) 下載。  
- Development Environment：建立具 .NET 應用程式的開發環境。若尚未完成，請參考 [documentation](https://reference.aspose.com/ocr/net/) 取得詳細說明。

## 匯入命名空間

在 .NET 應用程式中，首先匯入必要的命名空間：

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## 步驟 1：初始化 Aspose.OCR

`OcrEngine` 是 Aspose.OCR 的核心類別，用於對圖像執行光學字元辨識。首先建立此類別的實例，為後續所有 OCR 操作奠定基礎。

```csharp
// ExStart:1
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## 步驟 2：指定圖像路徑

定義要處理之圖像的絕對或相對路徑。路徑必須指向可讀取的檔案，否則引擎會拋出例外。

```csharp
// Image Path
string fullPath = dataDir + "sample.png";
```

## 步驟 3：以語言選擇辨識圖像

`RecognizeImage` 是掃描提供的位圖、套用語言模型並返回包含提取文字的 `RecognitionResult` 物件的方法。透過設定 `Language` 屬性，您告訴引擎使用哪套語言規則，顯著提升非英語內容的辨識準確度。

`Language` 屬性用於選擇要使用的 OCR 語言模型。

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

## 步驟 4：列印與顯示結果

完成 OCR 操作後，您可以取得辨識出的文字、每個單詞的邊界框、任何警告，甚至 JSON 輸出以供後續處理。

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

## 如何使用語言選擇提取 image text C#？

使用 `new OcrEngine()` 載入圖像，並在呼叫 `engine.RecognizeImage(imagePath)` 之前設定 `engine.Language = Language.English`（或任何支援的語言）。此方法會以單一字串返回完整文字，您可將其輸出、儲存或傳遞給其他服務。此兩步驟模式適用於所有支援的語言，且不需外部相依性。

## 常見問題與技巧

- **Incorrect language selection** – 若輸出文字呈現亂碼，請再次確認 `Language` 屬性與來源圖像的語言相符。  
- **Skewed images** – 啟用 `AutoSkew` 或手動調整 `SkewAngle` 以提升傾斜掃描的準確度。  
- **Large files** – 將大型圖像分塊處理或降低解析度後再傳入 `RecognizeImage`，以節省記憶體。  

## 常見問答

**Q: Aspose.OCR 是否適用於多語言文字辨識？**  
A: 是的，Aspose.OCR 支援超過 30 種語言，為多語言 OCR 任務提供彈性。

**Q: 我可以針對特定圖像特徵微調 OCR 設定嗎？**  
A: 當然可以！調整 `AutoSkew`、`SkewAngle`、`LineDetectionMode` 等參數，以優化不同情境的辨識結果。

**Q: 我可以在哪裡找到額外的支援或社群討論？**  
A: 前往 [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) 獲得支援並與社群討論。

**Q: 是否提供免費試用？**  
A: 有的，請探索 [free trial](https://releases.aspose.com/) 體驗 Aspose.OCR 的功能。

**Q: 我該如何購買 Aspose.OCR for .NET？**  
A: 購買請前往 [purchase page](https://purchase.aspose.com/buy)。

## 結論

恭喜！您已學會使用 Aspose.OCR for .NET 透過語言選擇 **how to extract image text C#**。本教學示範了如何設定 OCR 引擎、選擇適當語言以及處理結果，為在應用程式中建構多語言文字提取功能奠定了堅實基礎。

---

**最後更新：** 2026-07-23  
**測試版本：** Aspose.OCR 24.11 for .NET  
**作者：** Aspose  

{{< blocks/products/products-backtop-button >}}

## 相關教學

- [使用 Aspose OCR 進行多語言文字圖像辨識](/ocr/net/ocr-settings/working-with-different-languages/)
- [從圖像提取文字 – 使用 Aspose.OCR 的 OCR 設定](/ocr/net/ocr-settings/)
- [如何使用 Aspose.OCR for .NET 從圖像提取文字](/ocr/net/text-recognition/get-recognition-result/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}