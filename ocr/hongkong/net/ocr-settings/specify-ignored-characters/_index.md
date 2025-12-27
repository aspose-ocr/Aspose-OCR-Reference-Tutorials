---
date: 2025-12-27
description: 探索 Aspose.OCR for .NET 的先進 OCR 語言支援與功能。高效、精準、開發者友好。
linktitle: OCR Language Support – Ignored Characters in Image Recognition
second_title: Aspose.OCR .NET API
title: OCR 語言支援 – 圖像識別中被忽略的字符
url: /zh-hant/net/ocr-settings/specify-ignored-characters/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR 語言支援：在圖像辨識中指定忽略字元

## 簡介

OCR 語言支援是現代文件自動化的基石，讓應用程式能夠從各種字母與符號的圖像中讀取文字。在本教學中，您將學習如何告訴 **Aspose.OCR for .NET** 在辨識過程中忽略特定字元——這是一個在需要更乾淨的輸出或想過濾頁碼、裝飾符號等雜訊時的關鍵技巧。完成本指南後，您將擁有一段可直接執行的程式碼範例，示範此功能的全流程。

## 快速回答
- **「忽略字元」是什麼意思？** OCR 引擎在組成結果字串時會跳過的字元。  
- **為什麼要使用它？** 當某些符號與業務邏輯無關時，可提升辨識準確度。  
- **哪個 API 方法負責此功能？** `RecognitionSettings.IgnoredCharacters`。  
- **可以與語言套件一起使用嗎？** 可以——忽略字元可與您載入的任何語言同時運作。  
- **需要授權嗎？** 生產環境使用需具備臨時或正式授權。

## 先決條件

在深入 Aspose.OCR for .NET 所提供的豐富功能之前，請確保已具備以下條件：

1. Aspose.OCR 安裝  

   確認已成功安裝 Aspose.OCR for .NET。您可於 [download page](https://releases.aspose.com/ocr/net/) 取得相關檔案。

2. 文件目錄設定  

   為文件建立專屬目錄，這對順利執行範例至關重要。請將範例中的 `dataDir` 變數更新為您的文件目錄路徑。

3. 臨時授權（可選）  

   若您以臨時授權探索 Aspose.OCR for .NET，請從 [here](https://purchase.aspose.com/temporary-license/) 取得。

## 匯入命名空間

要開始使用 Aspose.OCR for .NET，您需要匯入必要的命名空間。將以下程式碼加入您的檔案：

```csharp
using System.IO;

using Aspose.OCR;
using System;
```

## 為什麼要指定忽略字元？

在許多實務情境——例如處理發票、收據或多語言表單時，您可能會遇到重複出現但不屬於有效資料的字元（例如作為分隔符的連字號、頁碼或裝飾符號）。告訴 OCR 引擎跳過這些字元，可減少後續處理工作量，並提升下游分析的可靠性。

## 逐步指南

### 步驟 1：設定文件目錄

先指定存放文件的目錄。將 `"Your Document Directory"` 替換為實際的文件路徑。

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";
```

### 步驟 2：初始化 Aspose.OCR

建立 OCR 引擎的實例。此物件將負責所有後續的辨識呼叫。

```csharp
// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

### 步驟 3：使用忽略字元辨識圖像

將圖像檔案與一個列出欲忽略字元的 `RecognitionSettings` 物件一起傳入。以下範例會忽略字元 `a`、`b` 與 `1`。

```csharp
// Recognize image with specified ignored characters
RecognitionResult result = api.RecognizeImage(dataDir + "SpanishOCR.bmp", new RecognitionSettings
{
    IgnoredCharacters = "ab1"
});
```

### 步驟 4：顯示辨識文字

最後，將清理過的文字輸出至主控台或您偏好的其他輸出端。

```csharp
// Display the recognized text
Console.WriteLine(result.RecognitionText);
```

## 常見問題與提示

- **路徑錯誤：** 確認 `dataDir` 以正確的路徑分隔符（`\` 或 `/`）結尾，符合您的作業系統。  
- **語言不支援：** OCR 引擎必須具備來源圖像的語言套件，否則忽略字元不會正確套用。  
- **授權錯誤：** 若出現授權例外，請確認臨時授權檔案已正確引用於專案中。

## 結論

Aspose.OCR for .NET 為開發者提供先進的 OCR 功能，簡化將圖像轉換為可編輯、可搜尋文字的流程。透過本逐步指南，您已學會如何排除不需要的字元，讓 OCR 流程更乾淨、更可靠。請前往 [documentation](https://reference.aspose.com/ocr/net/) 深入了解，發掘 Aspose.OCR 如何提升您的 OCR 專案。

## 常見問題

### Q1: 可以在非營利專案中使用 Aspose.OCR for .NET 嗎？

A1: 可以，Aspose.OCR for .NET 可用於商業與非商業專案。詳情請參閱 [licensing details](https://purchase.aspose.com/buy)。

### Q2: 有免費試用版嗎？

A2: 當然！您可於 [here](https://releases.aspose.com/) 取得免費試用版，先行體驗 Aspose.OCR for .NET 的功能與優勢。

### Q3: 如何取得 Aspose.OCR 的支援？

A3: 如有任何問題或需要協助，請造訪 [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) 與社群交流，或向專家尋求建議。

### Q4: Aspose.OCR 支援哪些語言？

A4: Aspose.OCR 支援多種語言，是執行 OCR 任務的多元選擇。完整語言清單請參考文件說明。

### Q5: 可以購買臨時授權嗎？

A5: 可以，若您需要臨時授權，可於 [here](https://purchase.aspose.com/temporary-license/) 取得，適用於短期使用。

---

**Last Updated:** 2025-12-27  
**Tested With:** Aspose.OCR 23.12 for .NET  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}