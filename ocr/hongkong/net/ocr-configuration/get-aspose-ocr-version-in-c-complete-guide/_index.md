---
category: general
date: 2026-06-03
description: 使用簡單程式碼片段在 C# 中取得 Aspose OCR 版本。了解如何透過 OcrEngine GetVersion 取得 Aspose
  OCR 函式庫版本。
draft: false
keywords:
- get aspose ocr version
- aspose ocr library
- ocrengine getversion
- c# ocr example
- retrieve aspose version
language: zh-hant
og_description: 快速在 C# 中取得 Aspose OCR 版本。本教學精確示範如何使用 OcrEngine.GetVersion 取得 Aspose
  OCR 函式庫的版本。
og_title: 取得 Aspose OCR 版本於 C# – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-06-03'
  description: Get Aspose OCR version in C# with a simple snippet. Learn how to retrieve
    the Aspose OCR library version using OcrEngine GetVersion.
  headline: Get Aspose OCR Version in C# – Complete Guide
  type: TechArticle
- description: Get Aspose OCR version in C# with a simple snippet. Learn how to retrieve
    the Aspose OCR library version using OcrEngine GetVersion.
  name: Get Aspose OCR Version in C# – Complete Guide
  steps:
  - name: Why this matters
    text: When you install the package, the assembly version on disk may differ from
      the version reported by the library at runtime. Querying the version via code
      ensures you’re reading the exact build that the CLR loaded, which is crucial
      for debugging and for compliance audits.
  - name: Expected output
    text: 'When you run `dotnet run` inside the project folder, you should see something
      similar to:'
  - name: What if `GetVersion()` returns an empty string?
    text: That usually signals a corrupted installation or a missing native dependency.
      Re‑install the NuGet package and verify that the `Aspose.OCR.Native.dll` (or
      the appropriate platform‑specific binary) sits alongside your executable.
  - name: Does the method work on .NET Core 2.0?
    text: Yes, **Aspose OCR** supports .NET Standard 2.0 and higher, so any .NET Core
      version that implements that standard can call `OcrEngine.GetVersion()`. Just
      make sure you reference the correct runtime identifiers (`win-x64`, `linux-x64`,
      etc.) if you’re publishing a self‑contained app.
  - name: Can I retrieve the version without a license file?
    text: Absolutely. `GetVersion()` does **not** require a license; it simply reports
      the library build number. However, if you attempt to perform OCR without a valid
      license, you’ll get a runtime exception. That’s why the `try/catch` in our snippet
      is valuable—it isolates the version check from the OCR exec
  type: HowTo
tags:
- Aspose
- OCR
- C#
- .NET
title: 取得 Aspose OCR 版本於 C# – 完整指南
url: /zh-hant/net/ocr-configuration/get-aspose-ocr-version-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 取得 Aspose OCR 版本（C#） – 完整指南

有沒有想過如何在 .NET 專案中 **取得 Aspose OCR 版本**？也許你在排除版本不符的問題，或只是想記錄在生產環境中執行的確切函式庫版本。無論原因為何，你已經來到正確的地方。

在本教學中，我們將逐步說明一個簡單、獨立的 C# 程式，呼叫 `OcrEngine.GetVersion()` 並印出結果。完成後，你不僅會知道 *如何* 取得版本，還會了解 *為何* 在升級 **Aspose OCR library** 時檢查版本能避免許多麻煩。

## 你將學會

- 將 Aspose.OCR NuGet 套件加入 C# 專案  
- 使用 `OcrEngine.GetVersion()` 方法（**ocrengine getversion** 入口點）  
- 處理可能的例外並驗證輸出  
- 擴充程式碼以應對實務情境，例如記錄或條件功能切換  

不需要任何 OCR 先前經驗——只要具備基本的 C# 與 Visual Studio（或你喜愛的 IDE）知識即可。讓我們開始吧。

---

## 步驟 1：設定專案並取得 Aspose OCR 函式庫

在呼叫任何 OCR 相關 API 之前，你必須在專案中參考 **Aspose OCR library**。

1. 在 Visual Studio 中開啟終端機或套件管理員主控台。  
2. 執行以下指令以安裝最新的穩定版：

```bash
dotnet add package Aspose.OCR
```

> **專業提示：** 若你的目標是 .NET Framework 而非 .NET Core，請使用 NuGet 套件管理員 UI，並選取與執行環境相符的版本。此套件包含我們稍後會使用的 `OcrEngine` 類別。

### 為何這很重要

安裝套件後，磁碟上的組件版本可能與執行時函式庫回報的版本不同。透過程式碼查詢版本可確保讀取到 CLR 載入的確切組建，這對除錯與合規稽核皆相當關鍵。

---

## 步驟 2：撰寫最小程式碼以 **取得 Aspose OCR 版本**

建立一個新的主控台應用程式（`dotnet new console -n OcrVersionDemo`），並將預設的 `Program.cs` 替換為下列程式碼：

```csharp
using System;
using Aspose.OCR;

namespace OcrVersionDemo
{
    class Program
    {
        static void Main()
        {
            try
            {
                // Step 2a: Retrieve the Aspose OCR library version.
                // This is the core of the get aspose ocr version operation.
                string version = OcrEngine.GetVersion();   // e.g., "24.5.7"

                // Step 2b: Display the version information to the console.
                Console.WriteLine($"Aspose OCR version: {version}");
            }
            catch (Exception ex)
            {
                // If something goes wrong (missing DLL, license issue, etc.)
                Console.Error.WriteLine($"Failed to get Aspose OCR version: {ex.Message}");
            }
        }
    }
}
```

**各部分說明**

- `using Aspose.OCR;` 會將 OCR 命名空間匯入，使我們能呼叫 `OcrEngine`。  
- `OcrEngine.GetVersion()` 是 **ocrengine getversion** 的靜態方法，會回傳類似 `"24.5.7"` 的字串。  
- 將呼叫包在 `try/catch` 區塊中，可防止執行時的意外情況——例如目標機器找不到原生二進位檔案。  
- 插值字串 `$"Aspose OCR version: {version}"` 會印出清晰、易讀的訊息。

### 預期輸出

在專案資料夾內執行 `dotnet run` 後，你應該會看到類似以下的輸出：

```
Aspose OCR version: 24.5.7
```

若無法載入函式庫，錯誤分支會輸出簡潔的訊息，協助你快速定位問題。

---

## 步驟 3：驗證版本是否與 NuGet 套件相符

很容易認為已安裝的 NuGet 版本就是執行時使用的版本，但環境差異可能會介入。為了再次確認：

```csharp
// After retrieving the version, compare it to the package metadata.
var assembly = typeof(OcrEngine).Assembly;
var fileVersion = System.Diagnostics.FileVersionInfo.GetVersionInfo(assembly.Location).FileVersion;

Console.WriteLine($"Assembly file version: {fileVersion}");
```

執行此額外程式碼會印出類似以下的結果：

```
Assembly file version: 24.5.7.0
```

若兩個值不相同，可能是從全域組件快取 (GAC) 或先前的建置資料夾載入了較舊的 DLL。此時，請執行 `dotnet clean` 清理方案，然後重新建置。

---

## 步驟 4：將版本檢查寫入正式環境日誌

大多數實務應用程式不只會印到主控台，還會寫入日誌檔或遙測系統。以下是一個使用 `Microsoft.Extensions.Logging` 的簡易範例：

```csharp
using Microsoft.Extensions.Logging;
using Microsoft.Extensions.DependencyInjection;

// Set up a minimal logger.
var serviceProvider = new ServiceCollection()
    .AddLogging(builder => builder.AddConsole())
    .BuildServiceProvider();

var logger = serviceProvider.GetService<ILogger<Program>>();

try
{
    string version = OcrEngine.GetVersion();
    logger.LogInformation("Aspose OCR version: {Version}", version);
}
catch (Exception ex)
{
    logger.LogError(ex, "Unable to retrieve Aspose OCR version");
}
```

現在版本會出現在結構化日誌中，之後可輕鬆依 `{Version}` 進行過濾。當你有多個微服務，各自載入可能不同的 OCR DLL 時，這個模式特別實用。

---

## 常見問題與邊緣情況

### 如果 `GetVersion()` 回傳空字串會怎樣？

通常表示安裝損毀或缺少原生相依性。請重新安裝 NuGet 套件，並確認 `Aspose.OCR.Native.dll`（或相對應平台的二進位檔）與可執行檔位於同一目錄。

### 此方法在 .NET Core 2.0 上能運作嗎？

可以，**Aspose OCR** 支援 .NET Standard 2.0 及以上版本，因此任何實作該標準的 .NET Core 版本皆可呼叫 `OcrEngine.GetVersion()`。若發佈自包含應用程式，請確保參考正確的執行時識別碼（`win‑x64`、`linux‑x64` 等）。

### 可以在沒有授權檔的情況下取得版本嗎？

絕對可以。`GetVersion()` **不需要** 授權檔，只會回報函式庫的建置編號。然而，若在未持有有效授權的情況下執行 OCR，會拋出執行時例外。因此，我們程式碼中的 `try/catch` 很有價值——它將版本檢查與 OCR 執行流程分離。

---

## 完整可執行範例（直接複製貼上）

以下是完整程式碼，可直接放入新的主控台專案。它包含可選的日誌區塊，讓你同時看到主控台輸出與結構化日誌。

```csharp
using System;
using Aspose.OCR;
using Microsoft.Extensions.Logging;
using Microsoft.Extensions.DependencyInjection;

namespace OcrVersionDemo
{
    class Program
    {
        static void Main()
        {
            // Set up a simple console logger.
            var services = new ServiceCollection()
                .AddLogging(builder => builder.AddConsole())
                .BuildServiceProvider();

            var logger = services.GetService<ILogger<Program>>();

            try
            {
                // Retrieve the Aspose OCR library version.
                string version = OcrEngine.GetVersion();   // get aspose ocr version

                // Log and display the version.
                logger.LogInformation("Aspose OCR version: {Version}", version);
                Console.WriteLine($"Aspose OCR version: {version}");

                // Extra verification – compare with assembly file version.
                var assembly = typeof(OcrEngine).Assembly;
                var fileVersion = System.Diagnostics.FileVersionInfo
                    .GetVersionInfo(assembly.Location).FileVersion;
                logger.LogDebug("Assembly file version: {FileVersion}", fileVersion);
                Console.WriteLine($"Assembly file version: {fileVersion}");
            }
            catch (Exception ex)
            {
                logger.LogError(ex, "Failed to get Aspose OCR version");
                Console.Error.WriteLine($"Error: {ex.Message}");
            }
        }
    }
}
```

使用 `dotnet run` 執行，它會顯示兩行確認版本的訊息，若啟用 `LogLevel.Debug`，還會多一行除錯訊息。

---

## 結論

我們已說明在 C# 環境中 **取得 Aspose OCR 版本** 所需的全部步驟——從安裝 **Aspose OCR library**、呼叫 **ocrengine getversion** 方法、處理例外，到將結果寫入正式等級的日誌。掌握這些知識後，你即可可靠地驗證應用程式使用的 OCR 建置版本，避免因版本問題造成的錯誤，並在不費吹灰之力的情況下滿足合規需求。

下一步？試著將此版本檢查與實際的 OCR 呼叫（`OcrEngine` → `RecognizeImage`）結合，並同時記錄版本與辨識結果。你也可以探索其他 Aspose 產品（PDF、Slides、Cells）的 **retrieve aspose version** 模式，讓整個套件保持同步。

祝開發順利，願你的 OCR 流程保持銳利！

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，建立在本篇示範的技巧之上。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在自己的專案中探索替代實作方式。

- [如何使用 Aspose.OCR for .NET 取得 OCR 結果](/ocr/english/net/text-recognition/get-recognition-result/)
- [使用 Aspose.OCR 以語言選擇擷取影像文字（C#）](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [如何在 Aspose.OCR for .NET 中使用 List 批次 OCR 影像](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}