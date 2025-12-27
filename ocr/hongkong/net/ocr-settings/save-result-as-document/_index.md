---
date: 2025-12-27
description: 學習如何使用 Aspose.OCR for .NET 從圖像提取文字、識別圖像中的文字，並將圖像轉換為 PDF 以及其他各種文件格式。
linktitle: Save Result as Document in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: 將影像轉換為 PDF .NET – 在 OCR 影像辨識中將結果儲存為文件
url: /zh-hant/net/ocr-settings/save-result-as-document/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 將圖像轉換為 PDF .NET – 在 OCR 圖像辨識中將結果儲存為文件

## Introduction

歡迎踏入使用 Aspose.OCR for .NET 的光學字元辨識（OCR）精彩世界！在本教學中，您將學會如何 **convert image to PDF .NET**、從圖像中 **extract text from image**，並將 OCR 輸出儲存為可搜尋的文件格式，如 PDF、DOCX、TXT 以及 Excel。無論您需要建立可搜尋的 PDF，或是將 OCR 結果匯出至 Excel，以下步驟都能快速且有效地指引您完成整個流程。

## Quick Answers
- **What does “image to pdf .net” mean?** 它指的是使用 .NET 函式庫（此處為 Aspose.OCR）將圖像檔案轉換成 PDF 文件的過程。  
- **Which formats can I export OCR results to?** 支援直接匯出為 DOCX、TXT、PDF 與 XLSX。  
- **Do I need a license for production use?** 是的，正式環境必須購買商業授權；亦提供免費試用版供評估使用。  
- **Can I extract searchable text from the PDF?** 當然可以——產生的 PDF 為 **ocr to searchable pdf**，可供索引。  
- **What .NET versions are supported?** Aspose.OCR 相容於 .NET Framework 4.5 以上、.NET Core 3.1 以上，以及 .NET 5/6 以上版本。  

## What is “image to pdf .net”?
“Image to PDF .NET” 是指將點陣圖（如 PNG、JPEG、TIFF 等）透過 .NET 程式庫程式化轉換為 PDF 檔案的過程。Aspose.OCR 不僅執行圖像轉換，還會同時進行 OCR，讓您 **recognize text in images**，並將文字嵌入產生的 PDF，使其具備可搜尋功能。

## Why use Aspose.OCR for this task?
- **High accuracy** – 先進的 OCR 引擎，支援多語言與多種字型。  
- **One‑step conversion** – 可同時辨識文字並直接儲存為 PDF、DOCX、TXT 或 Excel，免除額外後處理。  
- **No external dependencies** – 純 .NET 函式庫，無需本機原生二進位檔。  
- **Flexibility** – 輕鬆切換輸出格式，無論是 **creating a document from OCR** 或 **exporting OCR to Excel**，皆可快速完成。

## Prerequisites

在開始 OCR 之旅前，請先確保具備以下前置條件：

- Aspose.OCR for .NET。請確認已安裝 Aspose.OCR 函式庫。您可於 [here](https://releases.aspose.com/ocr/net/) 下載。  

- Document Directory：準備好存放文件的目錄，並在提供的程式碼中相應更新 `dataDir` 變數的路徑。

## Import Namespaces

先匯入必要的命名空間，這些是賦予程式碼 OCR 功能的基礎。

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

接下來，我們將範例分解為多個步驟說明：

## How to Convert Image to PDF .NET Using Aspose.OCR

### Step 1: Initialize Aspose.OCR

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

此步驟負責初始化 Aspose.OCR API。

### Step 2: Recognize Image

```csharp
// Recognize image
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings { });
```

此處使用 Aspose.OCR **recognize text within the specified image**（將 `"sample.png"` 替換為您的圖像檔案）。這就是執行 **extract text from image** 的環節。

### Step 3: Save Result in Different Formats

```csharp
// Save the result in your preferred format
result.Save(RunExamples.GetDataDir_OCR() + "sample.docx", SaveFormat.Docx);
result.Save(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text);
result.Save(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf);
result.Save(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx);
```

依需求自行調整此步驟。Aspose.OCR 允許您 **save the recognized text in various document formats such as DOCX, TXT, PDF, and XLSX**，等同於 **creating a document from OCR** 或 **exporting OCR to Excel**。

### Step 4: Display Success Message

```csharp
Console.WriteLine("SaveResultAsDocument executed successfully");
```

簡單的確認訊息，告知您流程已順利完成。

依循上述步驟，您即可成功運用 Aspose.OCR for .NET 辨識圖像中的文字，並將結果儲存為不同文件格式，包含 **ocr to searchable pdf**。

## Common Issues and Solutions
- **Image not recognized** – 請確保圖像解析度足夠（至少 300 dpi）且為支援格式（PNG、JPEG、TIFF）。  
- **Incorrect language detection** – 傳入 `RecognitionSettings` 物件，並設定正確的 `Language` 屬性（例如 `Language = Language.English`）。  
- **Output file not created** – 檢查 `dataDir` 是否指向有效且可寫入的資料夾，且檔名需唯一。

## Frequently Asked Questions

**Q: Is Aspose.OCR compatible with different image formats?**  
A: Yes, Aspose.OCR supports a wide range of image formats, ensuring flexibility in your OCR tasks.

**Q: Can I customize recognition settings for better accuracy?**  
A: Absolutely! Aspose.OCR provides recognition settings to fine‑tune the OCR process according to your specific requirements.

**Q: Is there a free trial available?**  
A: Yes, you can get started with a free trial [here](https://releases.aspose.com/).

**Q: How can I get temporary licenses for Aspose.OCR?**  
A: Temporary licenses can be obtained [here](https://purchase.aspose.com/temporary-license/).

**Q: Where can I seek help or connect with the community?**  
A: Join the Aspose.OCR community at [Aspose Forum](https://forum.aspose.com/c/ocr/16) for support and discussions.

## Conclusion

總結來說，Aspose.OCR for .NET 為 **image to pdf .net** 轉換、文字抽取與文件產生提供了無限可能。無論是抽取資料、建立可搜尋的 PDF，或是將 OCR 結果匯出至 Excel，Aspose.OCR 都能以直觀的 API 與完整的功能集簡化整個流程。

---

**Last Updated:** 2025-12-27  
**Tested With:** Aspose.OCR 24.11 for .NET  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}