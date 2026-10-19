---
date: 2026-02-25
description: 學習如何在 C# 中使用 Aspose.OCR for .NET 提取圖片文字。本分步指南展示多語言 OCR、語言選擇及實用技巧。
linktitle: Extract image text C# with language selection using Aspose.OCR
second_title: Aspose.OCR .NET API
title: 使用 Aspose.OCR 在 C# 中提取圖像文字並選擇語言
url: /zh-hant/net/ocr-configuration/ocr-operation-with-language-selection/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.OCR 進行語言選擇的 C# 圖像文字提取

## 介紹

如果您需要在 .NET 應用程式中 **提取圖像文字 C#**，Aspose.OCR for .NET 提供快速、精確且具語言感知的解決方案。本教學將示範一個真實案例，說明如何使用語言選擇進行 OCR 圖像辨識，讓您只需幾行程式碼即可從圖像中提取多語言文字。完成後，您將了解如何輕鬆將 OCR 整合至 C# 專案，以及為何此方式是生產環境的可靠選擇。

## 快速回答
- **Aspose.OCR 的功能是什麼？** 它能辨識圖像中的印刷文字與手寫文字，並回傳提取出的文字。  
- **可以選擇語言嗎？** 可以 – 您可以指定任何支援的語言，如英文、德文、西班牙文、中文等。  
- **開發階段需要授權嗎？** 免費試用可用於評估；正式上線需購買授權。  
- **支援哪些 .NET 版本？** .NET Framework 4.5 以上、.NET Core 3.1 以上、.NET 5/6 以上。  
- **傾斜校正會自動執行嗎？** 您可以啟用 `AutoSkew`，並微調 `SkewAngle` 設定。  

## 什麼是「extract image text C#」？

在 C# 中提取圖像文字指的是使用函式庫讀取圖像（PNG、JPEG、TIFF 等）的視覺內容，並將其轉換為可搜尋、可編輯的文字。Aspose.OCR 在本機提供此功能，無需將資料傳送至外部服務，確保工作流程的安全與合規。

## 為何選擇 Aspose.OCR 進行 OCR 任務？

- **高精度**，適用於多種字型與圖像品質。  
- **內建語言選擇**，免除外部語言套件的需求。  
- **簡易 API**，可無縫整合至現有 C# 專案，讓 **extract image text C#** 變得直觀。  
- **無外部相依** – 全部在本機執行，資料安全有保障。  

## 前置條件

在開始撰寫程式碼之前，請先確保具備以下條件：

- Aspose.OCR for .NET：請確認已安裝 Aspose.OCR 函式庫。您可從 [Aspose.OCR for .NET 下載頁面](https://releases.aspose.com/ocr/net/) 取得。  
- 開發環境：建立一個可執行的 .NET 應用程式。若尚未設定，請參考 [文件說明](https://reference.aspose.com/ocr/net/) 取得詳細步驟。  

## 匯入命名空間

在 .NET 應用程式中，先匯入必要的命名空間：

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## 步驟 1：初始化 Aspose.OCR

先建立 Aspose.OCR 類別的實例，為後續的 OCR 功能做好準備。

```csharp
// ExStart:1
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## 步驟 2：指定圖像路徑

接著，定義要執行 OCR 的圖像路徑，確保程式能存取該圖像。

```csharp
// Image Path
string fullPath = dataDir + "sample.png";
```

## 步驟 3：使用語言選擇辨識圖像

現在執行核心的 OCR 操作。利用 Aspose.OCR 函式庫辨識指定圖像的文字，並透過語言選擇等設定微調 **extract image text C#** 的流程。

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

OCR 完成後，列印並顯示結果，包括辨識文字、區域、警告訊息以及 JSON 表示。

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

## 常見問題與技巧

- **語言選擇不正確** – 若輸出文字呈現亂碼，請再次確認 `Language` 屬性與來源圖像的語言相符。  
- **圖像傾斜** – 啟用 `AutoSkew` 或手動調整 `SkewAngle`，可提升斜掃描圖像的辨識精度。  
- **大型檔案** – 可將大圖分塊處理，或在送入 `RecognizeImage` 前降低解析度，以節省記憶體。  

## 常見問答

**Q: Aspose.OCR 是否適用於多語言文字辨識？**  
A: 是，Aspose.OCR 支援多種語言，能靈活應對多語言 OCR 任務。

**Q: 我可以針對特定圖像特性微調 OCR 設定嗎？**  
A: 當然可以！調整傾斜角度、行辨識、區域偵測等參數，即可優化不同情境的 OCR 效果。

**Q: 我該去哪裡取得更多支援或參與社群討論？**  
A: 前往 [Aspose.OCR 論壇](https://forum.aspose.com/c/ocr/16) 與社群交流取得支援。

**Q: 有免費試用版嗎？**  
A: 有，請探索 [免費試用](https://releases.aspose.com/) 體驗 Aspose.OCR 的功能。

**Q: 我要如何購買 Aspose.OCR for .NET？**  
A: 前往 [購買頁面](https://purchase.aspose.com/buy) 完成購買。

## 結論

恭喜您！您已學會如何使用 Aspose.OCR for .NET 以語言選擇方式 **提取圖像文字 C#**。本教學示範了如何設定 OCR 引擎、選擇適當語言以及處理結果，為在應用程式中建置多語言文字提取功能奠定了堅實基礎。

---

**最後更新：** 2026-02-25  
**測試版本：** Aspose.OCR 24.11 for .NET  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}