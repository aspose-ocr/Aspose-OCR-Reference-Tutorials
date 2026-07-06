---
category: general
date: 2026-03-05
description: 如何快速使用 Aspose.OCR 進行 OCR，並在幾個簡單步驟中從串流辨識文字。了解完整的 C# 程式碼及串流影像資料的技巧。
draft: false
keywords:
- how to get OCR
- recognize text from stream
- Aspose OCR
- streaming OCR C#
- image chunk processing
language: zh-hant
og_description: 如何在 C# 中使用 Aspose.OCR 取得 OCR 並從串流辨識文字。請跟隨此一步一步的教學，獲得即用的解決方案。
og_title: 如何在 C# 中取得 OCR – 完整串流辨識指南
tags:
- OCR
- C#
- Aspose
title: 如何在 C# 中取得 OCR – 從串流識別文字
url: /zh-hant/net/text-recognition/how-to-get-ocr-in-c-recognize-text-from-stream/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中取得 OCR – 從串流辨識文字

有沒有想過 **如何在 .NET 應用程式中取得 OCR** 而不必先將整張圖片儲存到磁碟？你並不孤單。許多開發者需要 **從串流辨識文字**——例如在處理透過網路、相機即時影像或雲端儲存 API 傳送過來的圖片時。  

在本教學中，我們將逐步說明一個完整、可直接執行的範例，正好展示上述情境。完成後，你將擁有一個獨立的 C# 程式，能建立 Aspose OCR 引擎、將影像資料塊串流傳入，並將擷取的文字輸出至主控台。沒有神祕的外部工具，只有清晰的程式碼與幾個實用技巧。

## 你將學到

- 如何安裝與授權 Aspose.OCR 函式庫。
- 如何使用 `AppendChunk` 方法逐片餵入影像資料。
- 如何啟動與結束辨識流程（`BeginRecognize` / `EndRecognize`）。
- 如何處理常見的邊緣情況，例如資料塊不完整或授權錯誤。
- 輸出結果的樣子以及如何驗證。

### 前置條件

- .NET 6.0 或更新版本（程式碼同樣適用於 .NET Core 與 .NET Framework）。
- 有效的 Aspose OCR 授權檔 (`Aspose.OCR.lic`)。可從 Aspose 官方網站取得免費試用版。
- 具備 C# 基礎，並了解 `async`/`await`（若要從非同步串流讀取），本範例為了說明使用同步存根。

> **為什麼重要：** 串流 OCR 可讓記憶體使用保持低，且在處理大型影像或連續視訊串流時降低延遲。這是一種在即時文件掃描器、行動應用程式與伺服器端處理管線中常見的模式。

## 第一步：設定專案並加入 Aspose.OCR

首先，建立一個新的 Console 專案，並加入 Aspose.OCR 的 NuGet 套件。

```bash
dotnet new console -n StreamOcrDemo
cd StreamOcrDemo
dotnet add package Aspose.OCR
```

> **小技巧：** 若使用 Visual Studio，右鍵點擊專案 → *Manage NuGet Packages* → 搜尋 “Aspose.OCR” 並安裝最新的穩定版。

現在將授權檔加入專案根目錄，並將其 **Copy to Output Directory** 屬性設為 **Copy always**。這樣可確保執行時能找到檔案。

```csharp
// Program.cs – top of the file
using System;
using System.IO;
using Aspose.OCR;
```

## 第二步：初始化 OCR 引擎並套用授權

建立引擎相當簡單，但套用授權 **必須** 在任何辨識呼叫之前完成；否則會受到試用模式的限制。

```csharp
static OcrEngine InitializeOcrEngine()
{
    var engine = new OcrEngine();

    // Load the license – adjust the path if your file lives elsewhere
    string licensePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "Aspose.OCR.lic");
    if (!File.Exists(licensePath))
    {
        Console.Error.WriteLine("License file not found at " + licensePath);
        Environment.Exit(1);
    }

    engine.SetLicense(licensePath);
    return engine;
}
```

> **為什麼這樣做：** 先設定授權可確保之後的所有 API 呼叫皆以完整功能模式執行，避免出現「評估版」浮水印。

## 第三步：模擬串流來源

在真實應用中，你會從 `NetworkStream`、`FileStream` 或相機 SDK 讀取。為了示範，我們會使用一個輔助函式，回傳代表 JPEG 影像資料塊的 byte 陣列。

```csharp
static byte[] GetNextChunk()
{
    // Replace this with your actual streaming logic.
    // Here we simply read the whole file and pretend it’s a single chunk.
    string sampleImagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "sample.jpg");
    if (!File.Exists(sampleImagePath))
    {
        Console.Error.WriteLine("Sample image not found at " + sampleImagePath);
        Environment.Exit(1);
    }

    return File.ReadAllBytes(sampleImagePath);
}
```

> **邊緣情況說明：** 若收到許多小資料塊，可在結束辨識前重複呼叫 `engine.Image.AppendChunk(chunk)`。引擎會在內部緩衝，直到累積足夠資料才開始處理。

## 第四步：逐片餵入影像資料並執行 OCR

現在把所有步驟結合起來。流程如下：

1. `BeginRecognize()` – 告訴引擎即將開始餵入資料。
2. `AppendChunk()` – 加入每個 byte 陣列（可在多個資料塊上迴圈）。
3. `EndRecognize()` – 表示最後一個資料塊已送出，並觸發實際的辨識。

```csharp
static string PerformOcr(OcrEngine engine, byte[] imageChunk)
{
    // Start the recognition session
    engine.BeginRecognize();

    // Feed the image data. If you have multiple chunks, call this in a loop.
    engine.Image.AppendChunk(imageChunk);

    // End the session – the engine now processes the accumulated data.
    engine.EndRecognize();

    // Retrieve the result object; .Text holds the plain string.
    return engine.GetResult().Text;
}
```

## 第五步：在 `Main` 中整合所有程式碼

以下是完整的 `Main` 方法，將所有步驟串接起來，印出辨識文字，並妥善釋放引擎。

```csharp
static void Main(string[] args)
{
    // 1️⃣ Initialize OCR engine with license
    var ocrEngine = InitializeOcrEngine();

    try
    {
        // 2️⃣ Get a chunk of image data (replace with your streaming source)
        byte[] imageChunk = GetNextChunk();

        // 3️⃣ Run OCR on the streamed data
        string recognizedText = PerformOcr(ocrEngine, imageChunk);

        // 4️⃣ Output the result
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(recognizedText);
    }
    catch (Exception ex)
    {
        // Helpful error handling – you’ll often see OCR exceptions when the image is corrupted.
        Console.Error.WriteLine("OCR failed: " + ex.Message);
    }
    finally
    {
        // Release any native resources held by the engine.
        ocrEngine.Dispose();
    }
}
```

### 預期輸出

如果 `sample.jpg` 包含文字 “Hello, World!”，你應該會看到：

```
=== Recognized Text ===
Hello, World!
```

若影像模糊或資料塊不完整，輸出可能為空或出現亂碼——這就是確保最後一塊已送出的重要性。

## 處理多個資料塊（進階）

在真正的串流資料情況下，你可能會收到許多小片段。以下模式示範如何持續迴圈直到來源結束。

```csharp
static string OcrFromStream(OcrEngine engine, Stream source)
{
    engine.BeginRecognize();

    byte[] buffer = new byte[8192]; // 8 KB per read – adjust as needed
    int bytesRead;
    while ((bytesRead = source.Read(buffer, 0, buffer.Length)) > 0)
    {
        // If the last read returned fewer bytes, copy only that many.
        if (bytesRead < buffer.Length)
        {
            byte[] chunk = new byte[bytesRead];
            Array.Copy(buffer, chunk, bytesRead);
            engine.Image.AppendChunk(chunk);
        }
        else
        {
            engine.Image.AppendChunk(buffer);
        }
    }

    engine.EndRecognize();
    return engine.GetResult().Text;
}
```

> **為什麼這有幫助：** 直接從 `NetworkStream` 或 `FileStream` 串流，可避免一次將整張影像載入記憶體，對於大型 PDF 或高解析度照片尤為有利。

## 常見陷阱與避免方式

| 陷阱 | 症狀 | 解決方式 |
|---------|----------|-----|
| 找不到授權 | `SetLicense` 拋出 `FileNotFoundException` | 檢查路徑，並將 *Copy to Output Directory* 設為 *Copy always*。 |
| 結果為空 | 沒有印出文字 | 確保在 `AppendChunk` 之前呼叫 `BeginRecognize`，且在最後一塊之後呼叫 `EndRecognize`。 |
| 記憶體洩漏 | 多次 OCR 呼叫後應用程式變慢 | 在每次使用後釋放 `OcrEngine`，或以正確的 `Dispose` 呼叫重複使用同一實例。 |
| 資料塊損壞 | 出現亂碼 | 驗證資料塊大小；對於 JPEG/PNG，前幾個位元組應為 `0xFF 0xD8` 或 `0x89 0x50`。 |

## 加分項：使用非同步串流

如果來源是 `HttpClient` 回應串流，你可以將迴圈改寫為 `await` 讀取：

```csharp
static async Task<string> OcrFromAsyncStream(OcrEngine engine, Stream asyncSource)
{
    engine.BeginRecognize();

    byte[] buffer = new byte[8192];
    int bytesRead;
    while ((bytesRead = await asyncSource.ReadAsync(buffer, 0, buffer.Length)) > 0)
    {
        if (bytesRead < buffer.Length)
        {
            var chunk = new byte[bytesRead];
            Array.Copy(buffer, chunk, bytesRead);
            engine.Image.AppendChunk(chunk);
        }
        else
        {
            engine.Image.AppendChunk(buffer);
        }
    }

    engine.EndRecognize();
    return engine.GetResult().Text;
}
```

這樣可讓桌面或行動應用程式的 UI 保持回應，並在伺服器上提升吞吐量。

## 結論

現在你已擁有一個 **完整、獨立的解決方案**，可在 C# 中 **取得 OCR** 並 **從串流辨識文字**，使用 Aspose.OCR。教學涵蓋了授權與初始化、餵入影像資料塊、處理邊緣情況，甚至提供非同步變體。

試著執行看看——將 `sample.jpg` 換成即時相機影像、雲端儲存的圖片，或是 multipart HTTP 上傳。熟悉後，可探索語言套件、自訂前處理，或批次處理多個串流等進階功能。

**下一步：**  
- 嘗試先將 PDF 每頁轉為影像，再進行 OCR。  
- 使用 `engine.Config` 針對特定字型調整以提升辨識精度。  
- 結合 Azure Functions 或 AWS Lambda，打造無伺服器的文字抽取管線。

祝程式開發順利，願你的串流永遠清晰，OCR 結果完美無瑕！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}