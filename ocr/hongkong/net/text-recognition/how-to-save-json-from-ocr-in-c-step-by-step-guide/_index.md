---
category: general
date: 2026-02-19
description: 如何在 C# 中將 OCR 輸出儲存為 JSON – 學習從圖像提取文字、在 C# 中寫入 JSON 檔案，以及使用 Aspose OCR
  將圖像轉換為 JSON。
draft: false
keywords:
- how to save json
- extract text from image
- write json file c#
- convert image to json
- c# ocr tutorial
language: zh-hant
og_description: 在 C# 中將 OCR 結果儲存為 JSON 非常簡單。跟隨本教學，從圖像提取文字並以 C# 風格寫入 JSON 檔案。
og_title: 如何在 C# 中從 OCR 儲存 JSON – 完整指南
tags:
- C#
- OCR
- JSON
title: 如何在 C# 中從 OCR 儲存 JSON – 步驟指南
url: /zh-hant/net/text-recognition/how-to-save-json-from-ocr-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中從 OCR 保存 JSON – 完整教學

在 C# 中從 OCR 結果保存 json 是將掃描文件轉換為結構化資料的常見需求。在本指南中，你將看到如何從影像提取文字、轉換為 json，最後以 C# 方式寫入 json 檔案——不囉嗦，僅提供可運作的解決方案。

有沒有試過用掃描器讀取收據，結果只得到一張模糊的圖片，無法搜尋？這就是許多開發者在需要從影像中提取資料時遇到的問題。閱讀完本文後，你將擁有一個小型主控台應用程式，能讀取影像、使用 Aspose OCR 抽取文字，並保存一個乾淨的 json 檔案，供任何下游服務使用。

我們會涵蓋所有內容：所需的 NuGet 套件、完整可執行且註解豐富的程式碼、常見陷阱，以及快速驗證輸出的方式。無需事先具備 OCR 經驗——只要對 C# 與 .NET 有基本了解即可。

## 前置條件

- .NET 6 SDK 或更新版本（程式碼目標為 .NET 6，但亦可在 .NET 5+ 上執行）
- Visual Studio 2022、VS Code，或任何你喜歡的編輯器
- 想要處理的影像檔案（`input.png`）
- 需要有網路連線以下載 **Aspose.OCR** NuGet 套件

如果缺少上述任一項，請立即取得；否則之後會浪費時間。  

> **小技巧：** Aspose OCR 提供免費試用金鑰——非常適合在未購買授權的情況下進行實驗。

## 步驟 1：安裝 Aspose OCR NuGet 套件

首先，加入負責繁重工作的函式庫。於專案資料夾開啟終端機並執行：

```bash
dotnet add package Aspose.OCR
```

此單一指令會下載最新的 Aspose OCR 二進位檔，並在你的 `.csproj` 中加入參考。  

> **為何此步驟重要：** 若未安裝套件，`OcrEngine` 類別根本不存在，會導致編譯時錯誤。

套件安裝完成後，讓我們建立主控台應用程式的骨架。

## 步驟 2：設定專案結構

如果尚未建立，請先建立新的主控台專案：

```bash
dotnet new console -n JsonExportOcr
cd JsonExportOcr
```

在 `Program.cs` 中將預設內容替換為以下完整範例。我們稍後會逐行說明，但先備好檔案可避免複製貼上時遺漏大括號。

## 步驟 3：初始化 OCR 引擎（從影像提取文字）

第一行真正的程式碼會建立 OCR 引擎，並指示其偵測英文字符。你也可以改成 `Language.Spanish` 或其他支援的語言，但英文是最常見的情況。

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;
using System;
using System.IO;

class JsonExport
{
    static void Main()
    {
        // Step 3.1: Create an OCR engine and set the language to English
        OcrEngine ocrEngine = new OcrEngine { Language = Language.English };

        // Step 3.2: Recognize text from the input image
        // Replace the path with where your image actually lives
        string inputPath = @"YOUR_DIRECTORY/input.png";
        if (!File.Exists(inputPath))
        {
            Console.WriteLine($"Input file not found: {inputPath}");
            return;
        }

        OcrResult ocrResult = ocrEngine.RecognizeImage(inputPath);
```

**發生了什麼？**  
- `OcrEngine` 為 Aspose OCR 的入口點。  
- 設定 `Language` 可提升準確度，因為引擎會套用語言特定的啟發式演算法。  
- `RecognizeImage` 會回傳 `OcrResult` 物件，內含所有辨識出的文字、信心分數與邊界框。

若影像遺失或損壞，防護條件會印出友善訊息並中止執行——此小檢查可避免日後出現令人困惑的 null 參考錯誤。

## 步驟 4：將 OCR 結果轉換為 JSON（將影像轉為 JSON）

Aspose OCR 附帶一個名為 `JsonResultWriter` 的輔助工具。它會將 `OcrResult` 序列化為乾淨的 JSON 字串，結構與 REST API 的回傳相似。

```csharp
        // Step 4: Convert the OCR result to a JSON string
        string jsonResult = JsonResultWriter.Write(ocrResult);
```

**為何使用 `JsonResultWriter`？**  
- 它會自動處理複雜物件（例如巢狀的 `Word` 集合）。  
- 你不必自行撰寫序列化程式，避免遺漏諸如信心百分比等細節欄位。

此時 `jsonResult` 大致會是以下這樣（為了易讀性已做格式化）：

```json
{
  "PageCount": 1,
  "Pages": [
    {
      "PageNumber": 1,
      "Words": [
        {
          "Text": "Hello",
          "Confidence": 0.98,
          "BoundingBox": { "X": 10, "Y": 20, "Width": 50, "Height": 15 }
        },
        // … more words …
      ]
    }
  ]
}
```

你可以將該片段貼到 JSON 檢視器中以探索結構。  

> **邊緣情況：** 若影像包含多頁，JSON 會包含 `Pages` 陣列——請確保下游使用者能處理此結構。

## 步驟 5：將 JSON 寫入磁碟（如何保存 JSON）

現在進入教學核心：**如何保存 json** 到磁碟檔案。 .NET 的 `File` 類別讓這只需要一行程式碼，但我們會加入少量錯誤處理以提升穩定性。

```csharp
        // Step 5: Write the JSON string to an output file
        string outputPath = @"YOUR_DIRECTORY/output.json";
        try
        {
            File.WriteAllText(outputPath, jsonResult);
            Console.WriteLine($"JSON saved to {outputPath}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Failed to write JSON: {ex.Message}");
        }
```

這就是最終回答 *如何保存 json* 的時刻——檔案會被建立，若已存在則會覆寫，且會在主控台顯示清晰訊息確認成功。

## 步驟 6：驗證結果

程式執行完畢後，於任意編輯器（VS Code、Notepad++ 或甚至瀏覽器）開啟 `output.json`。你應該會看到格式良好的 JSON，呈現 OCR 輸出。若發現空的 `"Words": []` 陣列，請再次檢查影像品質——OCR 在低對比或噪點過多時表現不佳。

你也可以在命令列執行快速的完整性檢查：

```bash
dotnet run
```

應該會看到：

```
JSON saved to YOUR_DIRECTORY/output.json
```

若出現錯誤，主控台會告知是輸入檔案遺失或寫入操作失敗。

## 完整可執行範例

以下是 **完整** 程式碼，你可以直接複製貼上到 `Program.cs`。將 `YOUR_DIRECTORY` 替換為包含 `input.png` 的資料夾路徑。除此之外不需要其他檔案。

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;
using System;
using System.IO;

class JsonExport
{
    static void Main()
    {
        // Step 3: Initialize OCR engine (extract text from image)
        OcrEngine ocrEngine = new OcrEngine { Language = Language.English };

        // Define file paths
        string inputPath = @"YOUR_DIRECTORY/input.png";
        string outputPath = @"YOUR_DIRECTORY/output.json";

        // Validate input image exists
        if (!File.Exists(inputPath))
        {
            Console.WriteLine($"Input file not found: {inputPath}");
            return;
        }

        // Recognize text
        OcrResult ocrResult = ocrEngine.RecognizeImage(inputPath);

        // Convert OCR result to JSON (convert image to json)
        string jsonResult = JsonResultWriter.Write(ocrResult);

        // Write JSON to disk (how to save json)
        try
        {
            File.WriteAllText(outputPath, jsonResult);
            Console.WriteLine($"JSON saved to {outputPath}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Failed to write JSON: {ex.Message}");
        }
    }
}
```

執行程式，開啟產生的檔案，即完成一個展示 **如何從影像保存 json** 的 **c# ocr 教學**。

## 常見陷阱與技巧（寫入 JSON 檔案 C#）

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **空的 `Words` 陣列** | 影像過暗或解析度太低 | 前置處理影像（提升對比、使用較高 DPI） |
| **`File.WriteAllText` 拋出 UnauthorizedAccessException** | 嘗試寫入唯讀資料夾 | 選擇可寫入的目錄（例如 `%TEMP%` 或你的專案資料夾） |
| **缺少 NuGet 套件** | 忘記執行 `dotnet add package Aspose.OCR` | 重新執行指令並重新建置 |
| **JSON 為單行** | `WriteAllText` 直接寫入未格式化的字串 | 若有相應的 overload，使用 `JsonResultWriter.Write(ocrResult, true)`，或將輸出透過 `JsonSerializer` 並設定 `WriteIndented = true` |

這些快速檢查可讓你的 **write json file c#** 工作流程順暢，避免出現令人沮喪的「什麼都沒發生」情況。

## 往後步驟（從影像提取文字與更多）

現在你已了解 **如何保存 json**，接下來可能想要：

- **儲存**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}