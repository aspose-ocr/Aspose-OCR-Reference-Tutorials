---
title: OCR影像辨識中將結果儲存為文檔
linktitle: OCR影像辨識中將結果儲存為文檔
second_title: Aspose.OCR .NET API
description: 釋放 Aspose.OCR for .NET 的潛能。輕鬆識別圖像中的文字並將結果儲存為各種文件格式。
type: docs
weight: 10
url: /zh-hant/net/ocr-settings/save-result-as-document/
---
## 介紹

歡迎來到 Aspose.OCR for .NET 令人興奮的光學字元辨識 (OCR) 世界！在這個綜合教程中，我們將深入研究使用 Aspose.OCR 識別圖像中文字的複雜性，並示範如何將結果儲存為各種文件格式。

## 先決條件

在我們開始 OCR 之旅之前，請確保您具備以下先決條件：

-  Aspose.OCR for .NET。確保您已安裝 Aspose.OCR 庫。你可以下載它[這裡](https://releases.aspose.com/ocr/net/).

- 文檔目錄：為您的文件指定一個目錄，並更新`dataDir`相應地在提供的程式碼中變數。

## 導入命名空間

首先導入必要的命名空間。這些構建塊將為您的程式碼提供 OCR 功能。

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

現在，讓我們將範例分解為多個步驟：

## 步驟1：初始化Aspose.OCR

```csharp
//文檔目錄的路徑。
string dataDir = "Your Document Directory";

//初始化 AsposeOcr 實例
AsposeOcr api = new AsposeOcr();
```

此步驟透過初始化 Aspose.OCR API 做好準備。

## 第二步：辨識影像

```csharp
//辨識影像
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings { });
```

在這裡，我們使用 Aspose.OCR 來識別指定圖像中的文字（將“sample.png”替換為您的圖像檔案）。

## 步驟 3：以不同格式儲存結果

```csharp
//以您喜歡的格式儲存結果
result.Save(RunExamples.GetDataDir_OCR() + "sample.docx", SaveFormat.Docx);
result.Save(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text);
result.Save(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf);
result.Save(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx);
```

根據您的需求自訂此步驟。 Aspose.OCR 可讓您將識別的文字儲存為各種文件格式，例如 DOCX、TXT、PDF 和 XLSX。

## 步驟4：顯示成功訊息

```csharp
Console.WriteLine("SaveResultAsDocument executed successfully");
```

一則簡單的確認訊息，讓您知道流程已順利完成。

透過執行這些步驟，您已成功利用 Aspose.OCR for .NET 的強大功能來識別圖像中的文字並將結果儲存為不同的文件格式。

## 結論

總之，Aspose.OCR for .NET 為圖像中的文字辨識開啟了一個充滿可能性的世界。無論您是提取資料還是建立可搜尋文檔，Aspose.OCR 都可以透過其直覺的 API 簡化流程。

## 常見問題解答

### Q1. Aspose.OCR 是否相容於不同的影像格式？

A1：是的，Aspose.OCR 支援多種圖像格式，確保您 OCR 任務的靈活性。

### Q2：我可以自訂識別設定以獲得更高的準確度嗎？

A2：當然！ Aspose.OCR 提供識別設置，可根據您的特定要求微調 OCR 過程。

### Q3：有免費試用嗎？

 A3：是的，您可以開始免費試用[這裡](https://releases.aspose.com/).

### Q4：如何取得 Aspose.OCR 的臨時許可證？

 A4：可以獲得臨時許可證[這裡](https://purchase.aspose.com/temporary-license/).

### Q5：我可以在哪裡尋求協助或與社區聯繫？

 A5：加入 Aspose.OCR 社群：[Aspose論壇](https://forum.aspose.com/c/ocr/16)以尋求支持和討論。