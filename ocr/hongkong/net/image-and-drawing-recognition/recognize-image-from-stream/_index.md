---
date: 2026-04-12
description: 學習如何使用 Aspose OCR for .NET 從串流執行圖像文字擷取。此逐步範例展示簡易的 OCR 文字擷取。
keywords:
- image text extraction
- image to memorystream
- ocr png file
- image stream ocr
- read image stream c#
linktitle: 於 OCR 圖像辨識中從串流辨識圖像
second_title: Aspose.OCR .NET API
title: 如何使用 Aspose OCR 從串流執行圖像文字提取
url: /zh-hant/net/image-and-drawing-recognition/recognize-image-from-stream/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose OCR 從串流執行影像文字擷取

Welcome to the world of **image text extraction** with **Aspose.OCR for .NET**. In this tutorial you’ll see how to read an image stream, run OCR on a PNG file, and pull the recognized text into your C# application. Whether you’re building a document‑processing pipeline, a data‑entry automation tool, or just experimenting with OCR, the steps below will get you from a raw image to searchable text in minutes.

## 快速解答
- **本教學示範什麼？** 使用 Aspose OCR 從作為串流提供的影像中擷取文字。  
- **主要關鍵字是什麼？** *image text extraction*（於整篇指南中使用）。  
- **開發是否需要授權？** 免費試用可用於測試；正式上線需購買商業授權。  
- **能直接處理 PNG 檔案嗎？** 可以 – Aspose OCR 可直接處理 **ocr png file** 格式，無需額外轉換。  
- **支援哪些 .NET 版本？** .NET Framework 4.5+、.NET Core 3.1+、.NET 5/6/7。

## 什麼是影像文字擷取？
影像文字擷取（亦稱 OCR）會將影像中的視覺字符轉換為可編輯、可搜尋的文字。使用 Aspose OCR，您可以提供包含任何支援影像（PNG、JPEG、BMP 等）的 `MemoryStream`，並在一次呼叫中取得辨識後的字串。

## 為何選擇 Aspose OCR 進行影像文字擷取？
- **廣泛語言支援** – 開箱即支援數十種語言。  
- **簡易 API** – 只需幾行 C# 程式碼，即可將 **image to memorystream** 轉換為可讀文字。  
- **高準確度** – 先進演算法能處理雜訊掃描與低解析度 PNG。  
- **跨平台** – 可於 Windows、Linux、macOS 上執行 .NET Core。

## 前置條件

Before we start, make sure you have:

- 已安裝 Aspose.OCR for .NET（從 [Aspose.OCR for .NET Documentation](https://reference.aspose.com/ocr/net/) 下載）。  
- 一個範例影像檔（例如 **sample.png**），放置於程式碼可參照的資料夾中。

## 匯入命名空間

Add the required namespaces to your C# file:

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

## 步驟說明

### 步驟 1：設定文件目錄
```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";
```
將 **"Your Document Directory"** 替換為實際包含 *sample.png* 的資料夾路徑。

### 步驟 2：初始化 Aspose OCR 引擎
```csharp
// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```
建立 `AsposeOcr` 物件即可取得所有 OCR 方法的存取權。

### 步驟 3：讀取影像串流並辨識文字
```csharp
// Recognize image
using (MemoryStream ms = new MemoryStream())
using (FileStream file = new FileStream(dataDir + "sample.png", FileMode.Open, FileAccess.Read))
{
    file.CopyTo(ms);
    result = api.RecognizeImage(ms);
}
```
此處我們開啟 **sample.png**，將其位元組複製至 `MemoryStream`，再將該串流傳遞給 `RecognizeImage`。此範例示範了 **image stream ocr** 與 **read image stream c#** 的單一流程。

### 步驟 4：顯示辨識結果文字
```csharp
// Display the recognized text
Console.WriteLine(result);
```
OCR 結果會印出至主控台；您亦可將其儲存至資料庫或檔案中。

### 步驟 5：確認執行成功
```csharp
Console.WriteLine("RecognizeImageFromStream executed successfully");
```
簡單的確認訊息可讓您知道程序已順利完成，且未拋出例外。

## 常見問題與解決方案

| 問題 | 解決方案 |
|-------|----------|
| *結果為空* | 檢查影像路徑，確保檔案可讀，並確認影像中有清晰的高對比度文字。 |
| *不支援的影像格式* | 在呼叫 `RecognizeImage` 前，將來源轉換為 PNG 或 JPEG。 |
| *授權例外* | 於開發期間套用臨時授權，或於正式環境購買完整授權（見下文）。 |

## 常見問答

**問：Aspose.OCR 能處理多種語言嗎？**  
**答：** 可以，Aspose.OCR 支援多種語言，適用於全球化的 OCR 專案。

**問：是否有可使用的試用版？**  
**答：** 當然！您可前往 [此處](https://releases.aspose.com/) 取得 Aspose.OCR for .NET 的免費試用。

**問：遇到問題時該向何處尋求協助？**  
**答：** 請前往 [Aspose.OCR 論壇](https://forum.aspose.com/c/ocr/16) 獲得社群與專家支援。

**問：如何取得測試用的臨時授權？**  
**答：** 可於 [此處](https://purchase.aspose.com/temporary-license/) 取得測試用臨時授權。

**問：哪裡可以購買永久授權？**  
**答：** 若要將 Aspose.OCR 加入正式環境，請前往 [購買頁面](https://purchase.aspose.com/buy)。

## 結論

您現在已掌握使用 Aspose OCR for .NET 從串流執行 **影像文字擷取**。簡潔的 API 只需幾行程式碼，即可將任何支援的影像（例如 **ocr png file**）轉換為可搜尋的文字。請嘗試不同的影像來源、語言套件與進階設定，以微調 OCR 輸出，符合您的特定情境。

---

**最後更新：** 2026-04-12  
**測試版本：** Aspose.OCR 24.12 for .NET  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}