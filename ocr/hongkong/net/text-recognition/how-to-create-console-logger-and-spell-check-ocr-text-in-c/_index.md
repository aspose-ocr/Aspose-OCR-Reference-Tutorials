---
category: general
date: 2026-08-18
description: 學習如何在 C# 中建立主控台記錄器，並使用 Aspose AI 透過拼寫檢查後處理器校正 OCR 文字。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create console logger
- correct ocr text
- spell check ocr
language: zh-hant
lastmod: 2026-08-18
og_description: 在 C# 中建立控制台記錄器，並使用 Aspose AI 校正 OCR 文字。按照本完整指南，為您的 OCR 流程添加拼字檢查後處理器。
og_image_alt: Illustration of creating a console logger in C# code editor
og_title: 建立控制台日誌記錄器與 OCR 文字拼寫檢查（C#）—一步一步指南
schemas:
- author: Aspose
  dateModified: '2026-08-18'
  description: Learn how to create console logger in C# and use Aspose AI to correct
    OCR text with a spell‑check post‑processor.
  headline: How to create console logger and spell‑check OCR text in C#
  type: TechArticle
tags:
- C#
- OCR
- AI
- logging
title: 如何在 C# 中建立主控台記錄器並對 OCR 文字進行拼字檢查
url: /zh-hant/net/text-recognition/how-to-create-console-logger-and-spell-check-ocr-text-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中建立主控台記錄器並拼寫檢查 OCR 文字

如果您需要 **建立主控台記錄器** 以在處理掃描文件時輸出診斷資訊，本指南將提供完整解決方案。完成本教學後，您將能使用 Aspose AI SDK 內建的拼寫檢查後處理器 **校正 OCR 文字**。

OCR 結果常會留下拼寫錯誤，影響後續分析。加入拼寫檢查步驟可確保文字乾淨，適合進行索引、翻譯或資料抽取。以下章節將一步步說明從記錄器建立到最終驗證的所有必要步驟。

## 前置條件

在開始之前，請確保您已具備：

* .NET 6.0 或更新版本  
* Visual Studio 2022（或任何相容 C# 的 IDE）  
* 已於專案中加入 Aspose.AI NuGet 套件 (`dotnet add package Aspose.AI`)  

不需要額外的外部服務，因為 Aspose AI 模型可自動下載。

## 步驟 1：建立主控台記錄器以供診斷

記錄器會捕捉執行時資訊，讓您更容易排除模型載入或後處理器執行的問題。`ILogger` 介面讓您在不更改其他程式碼的情況下切換實作。

```csharp
// Step 1: (Optional) Create a logger for diagnostic output
ILogger logger = new ConsoleLogger();   // set to null if logging is not needed
```

`ConsoleLogger` 會將每筆日誌寫入標準輸出串流。使用介面可保持程式碼可測試，未來也能輕鬆換成檔案或雲端記錄器。

## 步驟 2：設定 AI 模型以啟用自動下載

Aspose AI 能在需要時自動下載必要的模型檔案。指定本機資料夾可避免重複的網路流量，並讓您掌控儲存位置。

```csharp
// Step 2: Configure the AI model – enable automatic download and specify a local folder
AsposeAIModelConfig modelConfig = new AsposeAIModelConfig
{
    AllowAutoDownload = true,
    DirectoryModelPath = "YOUR_DIRECTORY"
};
```

`AllowAutoDownload` 會確保 SDK 在第一次執行時取得模型。`DirectoryModelPath` 指向您機器上的永久位置，對 CI 流程特別有用。

## 步驟 3：以記錄器初始化 AsposeAI 引擎

將記錄器傳入引擎，可將診斷輸出與每個內部操作（包括模型載入與後處理器執行）關聯起來。

```csharp
// Step 3: Initialise the AsposeAI engine with the logger
AsposeAI ai = new AsposeAI(logger);
```

`AsposeAI` 建構子接受 `ILogger` 實例。如果在步驟 1 中傳入 `null`，引擎將靜默執行。

## 步驟 4：建立內建的拼寫檢查後處理器

Aspose AI 提供即用的拼寫檢查元件，可直接作用於 OCR 結果。建立此元件不需要任何額外設定。

```csharp
// Step 4: Create the built‑in spell‑check post‑processor
SpellCheckAIProcessor spellChecker = new SpellCheckAIProcessor();
```

`SpellCheckAIProcessor` 實作 `IAIProcessor` 介面，因而能與模型設定一起註冊。

## 步驟 5：將拼寫檢查處理器與模型設定一起註冊

將處理器綁定至引擎，可確保 OCR 結果自動流經拼寫檢查階段。

```csharp
// Step 5: Register the spell‑check processor together with the model configuration
ai.SetPostProcessor(spellChecker, modelConfig);
```

`SetPostProcessor` 會把 `spellChecker` 綁定到 `modelConfig`。之後呼叫 `RunPostprocessor` 時，引擎會使用已下載的模型執行拼寫檢查邏輯。

## 步驟 6：對先前取得的 OCR 結果執行後處理器

假設您已將 OCR 輸出存於變數 `ocrResult`，呼叫後處理器即可取得校正後的文字。

```csharp
// Step 6: Execute the post‑processor on previously obtained OCR results (variable `ocrResult`)
ai.RunPostprocessor(ocrResult);
```

`RunPostprocessor` 會處理 `ocrResult` 的每一頁。拼寫檢查演算法會分析辨識字串、套用語言特定字典，並產生校正版本。

## 步驟 7：取得並顯示校正後的文字

處理完成後，`SpellCheckAIProcessor` 會保留清理過的結果。您可以將其取出並輸出至主控台。

```csharp
// Step 7: Retrieve and display the corrected text
Console.WriteLine("CORRECTED RESULT\n");
Console.WriteLine(spellChecker.GetResult()[0].RecognitionText);
```

`GetResult()` 的第一個元素對應 OCR 文件的第一頁。若處理多頁檔案，請遍歷集合以顯示每頁的校正文字。

## 步驟 8：完成後釋放資源

釋放 `AsposeAI` 實例可釋放非受控資源並關閉任何開啟的檔案句柄。

```csharp
// Clean up resources when finished
ai.Dispose();
```

對實作 `IDisposable` 的物件呼叫 `Dispose` 是最佳實踐，特別是在使用原生函式庫時。

## 預期輸出

程式成功執行時，您會看到類似以下的輸出：

```
CORRECTED RESULT

The quick brown fox jumps over the lazy dog.
```

上述文字顯示原始 OCR 輸入，已由拼寫檢查後處理器修正拼寫錯誤。

## 常見問題與邊緣情況

**如果 OCR 結果為空會怎樣？**  
後處理器會優雅地處理空頁，回傳空字串，不會拋出例外。

**可以使用自訂字典嗎？**  
`SpellCheckAIProcessor` 提供可選的 `CustomDictionaryPath` 屬性。若需領域專用詞彙，請在呼叫 `SetPostProcessor` 前設定此屬性。

**主控台記錄器是否具備執行緒安全性？**  
`ConsoleLogger` 寫入 `Console.Out`，由 .NET 執行階段同步。若有高吞吐量需求，可改用具備緩衝機制的記錄器。

**如果需要同時處理大量文件該怎麼做？**  
每個執行緒建立獨立的 `AsposeAI` 實例，或使用執行緒安全的池化模式。共用單一實例可能導致競爭條件，因為內部模型狀態不是執行緒本地的。

## 結論

您現在已了解如何在 C# 中 **建立主控台記錄器**，並整合 **拼寫檢查 OCR** 後處理器以 **校正 OCR 文字**。完整工作流程——從記錄器初始化、模型設定、處理到資源釋放——涵蓋了建構穩健 OCR 校正管線的所有關鍵步驟。

接下來，您可以考慮為此管線加入其他後處理器，例如語言偵測或實體抽取。亦可嘗試使用 Serilog 等進階記錄框架，以捕捉更豐富的診斷資料。祝開發順利！

## 接下來該學什麼？

以下教學與本指南技術緊密相關，提供完整範例程式碼與逐步說明，協助您掌握更多 API 功能並探索替代實作方式：

- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Create Searchable PDF with Aspose OCR Batch Processing – C# Guide](/ocr/english/net/ocr-optimization/create-searchable-pdf-with-batch-ocr-c-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}