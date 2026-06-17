---
category: general
date: 2026-02-25
description: 如何在 C# 中快速使用 OCR 從圖像提取文字、載入圖像進行 OCR，並使用 Aspose OCR 設定 OCR 語言。一步一步的指南。
draft: false
keywords:
- how to use OCR
- extract text from image
- load image for OCR
- set OCR language
language: zh-hant
og_description: 學習如何在 C# 中使用 OCR 從圖像提取文字、載入圖像進行 OCR，並使用 Aspose OCR 設定 OCR 語言。完整的非同步範例。
og_title: 如何在 C# 中使用 OCR – 完整非同步指南
tags:
- C#
- Aspose OCR
- async programming
title: 如何在 C# 中使用 OCR – 非同步從圖片提取文字
url: /zh-hant/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image-asynchronously/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 OCR – 非同步從圖像提取文字

是否曾經需要在收據、發票或掃描表格上 **how to use OCR**，卻發現找到的程式碼範例要麼不完整，要麼仍停留在同步的世界？你並非唯一遇到這種情況的人。在許多實際應用中，你希望 **extract text from image** 而不凍結使用者介面，同時也想靈活選擇適合的辨識語言。  

在本教學中，我們將逐步示範一個完整且可執行的範例，向你展示如何 **load image for OCR**、設定 **set OCR language** 選項，並以非同步方式執行辨識。完成後，你將擁有一個獨立的主控台應用程式，能將辨識出的文字印在主控台上，並提供一些處理邊緣案例與擴充解決方案的技巧。

## 前置條件

- .NET 6.0 或更新版本（此程式碼同樣適用於 .NET Core 與 .NET Framework）  
- 已安裝 Aspose.OCR NuGet 套件（`Aspose.OCR`）  
- 放置於可參考資料夾中的範例影像檔（例如 `receipt.jpg`）  
- 基本的 C# 知識 – 不需要任何進階的 async 技巧，只要掌握基礎即可  

如果缺少上述任一項，請使用 `dotnet add package Aspose.OCR` 取得 NuGet 套件，並為測試影像建立一個簡單的資料夾。沒什麼複雜的。

---

## How to Use OCR：逐步實作

以下我們將流程分為四個邏輯步驟。每個步驟都有自己的 H2 標題，且第一個標題會重複主要關鍵字以符合 SEO。

### Step 1 – 初始化 OCR 引擎 (How to Use OCR)

你首先需要的是 `OcrEngine` 的實例。可以把它想像成此操作的核心大腦；它負責保存設定、影像以及結果。

```csharp
using System;
using System.Threading.Tasks;
using Aspose.OCR;
using Aspose.OCR.Enums;

public class AsyncExample
{
    public static async Task RunAsync()
    {
        // Create the OCR engine – this object will manage everything.
        var ocrEngine = new OcrEngine();

        // Next steps will configure it further.
```

**Why this matters:**  
一次建立引擎並重複使用，可在處理大量影像時提升效能。它也提供一個單一位置來設定全域選項，例如語言。

### Step 2 – 設定 OCR 語言 (Set OCR Language Properly)

如果省略語言選擇，Aspose OCR 會預設使用英語，這對收據可能尚可，但對外文文件則不適用。設定語言只需要一行程式碼：

```csharp
        // Set the recognition language to English.
        // You can change OcrLanguage.French, OcrLanguage.Spanish, etc.
        ocrEngine.Config.Language = OcrLanguage.English;
```

**Pro tip:**  
當需要多語言支援時，你可以傳入語言陣列（`OcrLanguage.English | OcrLanguage.French`）。引擎會依序嘗試每種語言，對於混合語言的收據非常方便。

### Step 3 – 載入影像以供 OCR (Load Image for OCR Efficiently)

現在我們將引擎指向要讀取的檔案。Aspose 提供 `ImageStream.FromFile`，它抽象化了底層的串流處理。

```csharp
        // Load the image you want to analyze.
        // Replace the path with the actual location of your image file.
        ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.jpg");
```

**Edge case:**  
如果檔案路徑錯誤或影像格式不支援，`FromFile` 會拋出例外。若你在構建穩健的 UI，請將其包在 try/catch 中。

### Step 4 – 執行非同步辨識 (Extract Text from Image)

這裡就是魔法發生的地方。`RecognizeAsync` 方法會在背景執行緒上執行 OCR，釋放呼叫執行緒——非常適合 UI 或 Web 應用程式。

```csharp
        // Run OCR asynchronously.
        var ocrResult = await ocrEngine.RecognizeAsync();

        // Display the recognized text.
        Console.WriteLine("OCR completed:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**What you’ll see:**  
如果 `receipt.jpg` 包含文字 “Total: $12.34”，主控台輸出將會是：

```
OCR completed:
Total: $12.34
```

**Why async?**  
同步的 OCR 可能會阻塞執行緒數秒，尤其在高解析度影像時更明顯。使用 `await` 可保持應用程式回應性，且與 ASP.NET Core 請求管線相容。

---

## 完整範例

將以下完整程式碼片段複製到新的主控台專案（`dotnet new console`）中並執行。記得將 `YOUR_DIRECTORY/receipt.jpg` 替換為實際影像的路徑。

```csharp
using System;
using System.Threading.Tasks;
using Aspose.OCR;
using Aspose.OCR.Enums;

public class AsyncExample
{
    public static async Task Main(string[] args)
    {
        await RunAsync();
    }

    public static async Task RunAsync()
    {
        // Step 1: Create the OCR engine.
        var ocrEngine = new OcrEngine();

        // Step 2: Set the OCR language (English by default).
        ocrEngine.Config.Language = OcrLanguage.English;

        // Step 3: Load the image you want to process.
        // Ensure the file exists; otherwise an exception is thrown.
        ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.jpg");

        // Step 4: Perform asynchronous OCR recognition.
        var ocrResult = await ocrEngine.RecognizeAsync();

        // Output the recognized text.
        Console.WriteLine("OCR completed:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Expected output**（假設影像包含可辨識的英文文字）：

```
OCR completed:
Your extracted text appears here, line by line.
```

如果看到空字串，請再次確認影像是否清晰，以及語言設定是否與文字相符。

---

## 常見陷阱與避免方法

| 問題 | 發生原因 | 解決方式 |
|-------|----------------|-----|
| **Blank result** | 低解析度影像或語言設定錯誤 | 使用較高解析度的掃描，或將 `ocrEngine.Config.Language` 設為正確的語言 |
| **Exception on `FromFile`** | 路徑錯誤或不支援的格式 | 核對路徑，使用絕對路徑，或先將影像轉換為 PNG/JPEG |
| **Performance lag** | 大量批次同步處理 | 使用 `Task.WhenAll` 平行處理影像，並重複使用單一 `OcrEngine` 實例 |
| **Memory leak** | 自訂載入程式碼未釋放串流 | 依賴 `ImageStream.FromFile` 處理釋放，或在手動載入時使用 `using` 區塊 |

**Bonus tip:**  
如果需要提取結構化資料（例如收據的鍵值對），可考慮使用正規表達式或輕量級的 NLP 函式庫對 `ocrResult.Text` 進行後處理。

---

## 擴充解決方案

現在你已了解 **how to use OCR** 單張影像的使用方式，可能會想問：「如果每晚有數十張收據該怎麼辦？」

- **Batch processing:** 將 `RunAsync` 邏輯包在迴圈中，並將結果收集到清單中。  
- **Parallelism:** 使用 `Parallel.ForEach` 搭配 async 支援（.NET 6 中的 `Parallel.ForEachAsync`）同時執行多個辨識。  
- **Persisting results:** 將 `ocrResult.Text` 儲存至資料庫，或寫入 CSV 供後續分析使用。  

所有這些擴充都仍然依賴我們先前討論的核心步驟：初始化引擎、設定語言、載入影像，以及呼叫 `RecognizeAsync`。

---

## 視覺摘要

![how to use OCR example](/images/ocr-example.png "how to use OCR in C# with Aspose OCR")

*上圖說明了從載入影像到取得辨識文字的流程。*

---

## 結論

我們剛剛走過一個完整、可投入生產的範例，展示了在 C# 中 **how to use OCR** 以 **extract text from image**、**load image for OCR**，以及正確 **set OCR language**——同時透過非同步呼叫保持 UI 的回應性。

只要一個獨立的腳本，你現在就擁有了從圖片、收據或任何掃描文件中提取文字的全部所需。接下來，你可以擴展至批次處理、加入錯誤處理，或將結果整合到更大的工作流程中。

準備好下一步了嗎？試著將 `OcrLanguage.English` 換成其他語言、測試不同的影像格式，或將輸出連結至簡易資料庫。可能性與你需要閱讀的文件一樣廣闊。

有任何問題或卡住了嗎？在下方留下評論，我們祝你寫程式愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}