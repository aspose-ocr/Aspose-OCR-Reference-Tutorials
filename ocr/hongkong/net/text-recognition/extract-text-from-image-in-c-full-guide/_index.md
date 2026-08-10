---
category: general
date: 2026-03-23
description: 使用 Aspose OCR 於 C# 從圖像提取文字，並學習如何加入控制台記錄器以獲得即時回饋。
draft: false
keywords:
- extract text from image
- add console logger
language: zh-hant
og_description: 使用 Aspose OCR 從圖像提取文字，並加入控制台日誌以監控過程。一步一步的 C# 教學。
og_title: 在 C# 中從圖像提取文字 – 完整程式設計指南
tags:
- OCR
- C#
- logging
title: 在 C# 中從圖片提取文字 – 完整指南
url: /zh-hant/net/text-recognition/extract-text-from-image-in-c-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從圖像中提取文字（C#） – 完整指南

需要快速且可靠地**從圖像中提取文字**嗎？使用 Aspose OCR，您只需幾行 C# 程式碼即可完成。  
我們還會示範如何**新增主控台記錄器**，讓您即時在終端機上看到 OCR 引擎的執行進度。

想像一下您手上有掃描過的收據、手寫筆記，或是以 PNG 格式保存的 PDF 頁面。您想直接取得原始文字，而不必開啟笨重的 UI。本教學將一步步帶您完成可直接複製貼上的完整解決方案，適用於 .NET 6+ 以及最新的 Aspose OCR 函式庫。

完成本指南後，您將能夠：

* 載入圖像檔案並執行 OCR，以**從圖像中提取文字**資料。  
* 將主控台記錄器掛接至 Aspose AI，讓您看到程式庫在背後的運作情形。  
* 套用內建的拼寫檢查後處理器，清理 OCR 錯誤。

> **先決條件** – 可正常運作的 .NET 開發環境（Visual Studio 2022、VS Code 或 Rider）、.NET 6 SDK 或更新版本，以及 Aspose OCR 授權（或免費試用）。不需要其他第三方套件。

---

## 您需要的項目

| 項目 | 為何重要 |
|------|----------|
| **Aspose.OCR** NuGet package | 提供實際讀取圖像的 `OcrEngine` 類別。 |
| **Aspose.OCR.AI** NuGet package | 提供 `AsposeAI` 後處理框架，包括拼寫檢查。 |
| **Microsoft.Extensions.Logging** (optional) | 提供 `ILogger` 介面，用於**新增主控台記錄器**步驟。 |
| **An input image** (`input.png`) | 作為來源檔案，我們將從中**提取文字**的圖像 (`input.png`)。 |

您可以透過終端機安裝這些套件：

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.AI
dotnet add package Microsoft.Extensions.Logging.Abstractions
```

---

## 步驟 1 – 使用 Aspose OCR 從圖像提取文字

我們首先將圖像交給 OCR 引擎處理。此程式碼負責完成繁重的工作，並回傳可能仍含錯字的原始字串。

```csharp
using Aspose.OCR;
using System;

class OcrDemo
{
    static string PerformOcr(string imagePath)
    {
        // Initialise the OCR engine
        using (OcrEngine ocr = new OcrEngine())
        {
            // Load the image – replace with your own path if needed
            ocr.Image = ImageStream.FromFile(imagePath);

            // Run recognition; if it fails we return an empty string
            if (!ocr.Recognize())
            {
                Console.WriteLine("OCR failed – check the image path and format.");
                return string.Empty;
            }

            // The engine populates the Text property with the recognised characters
            string rawText = ocr.Text;
            Console.WriteLine("Raw OCR output:\n" + rawText);
            return rawText;
        }
    }
}
```

**為何這樣可行：** `OcrEngine` 抽象化了所有低階的圖像前處理（二值化、傾斜校正等）。當 `Recognize()` 回傳 `true` 時，`Text` 屬性已包含最佳猜測的字元。  

> **小技巧：** 若圖像尺寸過大，建議先將較長邊縮小至 ≤ 2000 px 再送入引擎。這可加速處理，同時不會影響準確度。

---

## 步驟 2 – 為即時洞察新增主控台記錄器

現在加入**新增主控台記錄器**的程式碼。記錄不只是除錯工具，還能讓您看到模型下載、AI 處理步驟以及程式庫可能拋出的任何警告。

```csharp
using Microsoft.Extensions.Logging;
using System;

public class ConsoleLogger : ILogger
{
    // Minimal ILogger implementation that writes to the console.
    public IDisposable BeginScope<TState>(TState state) => null;
    public bool IsEnabled(LogLevel logLevel) => true;

    public void Log<TState>(LogLevel logLevel, EventId eventId,
        TState state, Exception exception, Func<TState, Exception, string> formatter)
    {
        Console.WriteLine($"[{logLevel}] {formatter(state, exception)}");
    }
}
```

接著將此記錄器注入 Aspose AI：

```csharp
using Aspose.OCR.AI;
using Aspose.OCR.AI.PostProcessors;

// ...

ILogger consoleLogger = new ConsoleLogger();   // Implements ILogger
AsposeAI ai = new AsposeAI(consoleLogger);
```

**您會看到的情況：** 當拼寫檢查模型自動下載時，主控台會印出類似以下的訊息：

```
[Information] Downloading model to YOUR_DIRECTORY/Models/spellcheck.onnx …
```

這就是**新增主控台記錄器**的好處——您再也不會懷疑背景作業是否成功。

---

## 步驟 3 – 設定與註冊拼寫檢查後處理器

Aspose AI 內建一個方便的拼寫檢查後處理器，可清理常見的 OCR 錯誤（例如 “rec0gn1ze” → “recognize”）。我們將對其進行設定，必要時告訴程式庫模型的存放位置，最後再註冊它。

```csharp
// Create the built‑in spell‑check processor
SpellCheckAIProcessor spellProcessor = new SpellCheckAIProcessor();

// Optional: tell AsposeAI where to keep downloaded models
AsposeAIModelConfig modelConfig = new AsposeAIModelConfig
{
    AllowAutoDownload = true,
    DirectoryModelPath = "YOUR_DIRECTORY/Models"
};

// Register the processor with the AI engine
ai.SetPostProcessor(spellProcessor, modelConfig);
```

**為何可能需要自訂路徑：** 在 CI/CD 流程中，您常會想將模型快取於已知目錄，以避免重複下載。`AllowAutoDownload` 旗標確保模型在第一次執行程式碼時會被自動取得。

---

## 步驟 4 – 在 OCR 結果上執行後處理器

取得 OCR 文字後，並且拼寫檢查處理器已備妥，我們將原始字串交給 `AsposeAI`。引擎會執行模型，處理器則在內部儲存校正後的文字。

```csharp
// Assume ocrResult contains the raw OCR output from Step 1
string ocrResult = PerformOcr("YOUR_DIRECTORY/input.png");

// Run the post‑processor – it expects an IEnumerable<string>
ai.RunPostprocessor(new[] { ocrResult });
```

此呼叫完成後，`spellProcessor` 會持有一系列 `RecognitionResult` 物件，每個物件的 `RecognitionText` 屬性都包含已清理過的文字。

---

## 步驟 5 – 取得並顯示校正後的文字

最後，我們從處理器中取出校正後的字串並印出。這正是您真正感受到 OCR 與**新增主控台記錄器**工作流程雙重效益的時刻。

```csharp
// Grab the first (and only) result
string correctedText = spellProcessor.GetResult()[0].RecognitionText;
Console.WriteLine("\nCorrected OCR output:\n" + correctedText);
```

**預期輸出**（假設圖像中包含 “Aspose OCR demo” 這句話，但有少許 OCR 錯誤）：

```
Raw OCR output:
Asp0se OCR d3mo

[Information] Model downloaded successfully.
[Information] Spell‑check completed.

Corrected OCR output:
Aspose OCR demo
```

可見記錄器已告知模型已就緒，且校正後的行文字乾淨整齊。

---

## 步驟 6 – 清理資源

`AsposeAI` 與 `OcrEngine` 皆實作 `IDisposable`。釋放它們可回收原生記憶體與檔案句柄，對於長時間執行的服務尤為重要。

```csharp
// At the end of Main()
ai.Dispose();   // Releases AI resources
// OcrEngine is already disposed via the using‑statement in PerformOcr()
```

---

## 完整範例程式

以下是完整程式碼，您可以直接複製貼上至新建的主控台專案（`dotnet new console`）。請將 `"YOUR_DIRECTORY"` 替換為您機器上的實際資料夾路徑。

```csharp
using Aspose.OCR;
using Aspose.OCR.AI;
using Aspose.OCR.AI.PostProcessors;
using Microsoft.Extensions.Logging; // optional logger
using System;

class SpellCheckDemo
{
    static void Main()
    {
        // ---------- Step 1: OCR ----------
        string ocrResult = PerformOcr("YOUR_DIRECTORY/input.png");
        if (string.IsNullOrEmpty(ocrResult)) return;

        // ---------- Step 2: Initialise AI with console logger ----------
        ILogger consoleLogger = new ConsoleLogger(); // implements ILogger
        AsposeAI ai = new AsposeAI(consoleLogger);

        // ---------- Step 3: Spell‑check processor ----------
        SpellCheckAIProcessor spellProcessor = new SpellCheckAIProcessor();

        // ---------- Step 4: Model configuration (optional) ----------
        AsposeAIModelConfig modelConfig = new AsposeAIModelConfig
        {
            AllowAutoDownload = true,
            DirectoryModelPath = "YOUR_DIRECTORY/Models"
        };

        // ---------- Step 5: Register and run ----------
        ai.SetPostProcessor(spellProcessor, modelConfig);
        ai.RunPostprocessor(new[] { ocrResult });

        // ---------- Step 6: Show corrected text ----------
        string correctedText = spellProcessor.GetResult()[0].RecognitionText;
        Console.WriteLine("\nCorrected OCR output:\n" + correctedText);

        // ---------- Clean up ----------
        ai.Dispose();
    }

    static string PerformOcr(string imagePath)
    {
        using (OcrEngine ocr = new OcrEngine())
        {
            ocr.Image = ImageStream.FromFile(imagePath);
            if (!ocr.Recognize())
            {
                Console.WriteLine("OCR failed – check the image path and format.");
                return string.Empty;
            }
            string raw = ocr.Text;
            Console.WriteLine("Raw OCR output:\n" + raw);
            return raw;
        }
    }
}

// Minimal console logger implementation
public class ConsoleLogger : ILogger
{
    public IDisposable BeginScope<TState>(TState state) => null;
    public bool

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}