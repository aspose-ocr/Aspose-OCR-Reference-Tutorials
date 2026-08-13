---
category: general
date: 2026-03-05
description: 如何在 C# 中使用 OCR 從收據圖像提取文字。學習如何載入圖像進行 OCR，並在數分鐘內辨識收據圖像。
draft: false
keywords:
- how to use OCR
- extract text from receipt
- load image for OCR
- recognize receipt image
language: zh-hant
og_description: 如何在 C# 中使用 OCR 從收據提取文字。跟隨此步驟指引，載入影像進行 OCR，並高效辨識收據圖像。
og_title: 如何在 C# 中使用 OCR – 快速提取收據文字
tags:
- OCR
- C#
- Aspose
- Receipt Processing
title: 如何在 C# 中使用 OCR – 快速從收據提取文字
url: /zh-hant/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-receipts-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 OCR – 快速從收據提取文字

有沒有想過 **如何使用 OCR** 直接從超市收據的相片中提取資料？你並不是唯一有此疑問的人。在許多小型企業應用程式中，瓶頸往往是將模糊的 PNG 轉換成可供實際使用的結構化文字。  

好消息是？只需幾行 C# 程式碼加上 Aspose.OCR，你就能 **load image for OCR**、執行引擎，並在不到一分鐘的時間內 **recognize receipt image**。以下將展示一個完整、可直接執行的範例，並提供大多數教學會略過的技巧。

## 本指南涵蓋內容

* 安裝 Aspose.OCR NuGet 套件。  
* 設定 OCR 引擎 – 正確使用 **如何使用 OCR** 的核心。  
* 載入收據檔案（即 **load image for OCR** 步驟）。  
* 執行辨識程序，並擷取 JSON 與 XML 版面資料。  
* 處理常見問題，例如缺少授權或不支援的影像格式。  

完成後，你將擁有一個獨立的程式，可從放入資料夾的任何收據中提取文字。無需外部服務，亦無隱藏的魔法。

## 前置條件

* .NET 6 SDK 或更新版本（程式碼亦可在 .NET Core 上編譯）。  
* 有效的 Aspose.OCR 授權檔 (`Aspose.OCR.lic`)。若尚未取得，可從 Aspose 申請免費試用。  
* 範例收據影像 – `receipt.png` 可正常使用，任何常見的點陣圖格式皆可。  

如果你已備妥上述項目，太好了 – 讓我們開始吧。

![how to use OCR example](https://example.com/ocr-receipt.png "how to use OCR example")

## 步驟 1：安裝 Aspose.OCR 並建立新專案

首先，你需要能真正執行繁重工作的函式庫。於專案資料夾開啟終端機並執行以下指令：

```bash
dotnet new console -n ReceiptOcrDemo
cd ReceiptOcrDemo
dotnet add package Aspose.OCR
```

該指令會產生一個 console 應用程式，並下載最新的 Aspose.OCR 套件。依我之見，將專案名稱保持簡短可讓產生的路徑更易閱讀，尤其在同時處理多個示範應用程式時。

## 步驟 2：初始化 OCR 引擎 – **如何使用 OCR** 的核心

現在我們要撰寫能回答「**如何使用 OCR** 在 C# 中」的程式碼。開啟 `Program.cs`，將內容替換為下方片段。請留意註解——它們說明了每一行背後的 *原因*，而不僅是 *做什麼*。

```csharp
using System;
using System.IO;
using Aspose.OCR;          // Aspose OCR namespace
using Aspose.OCR.Image;   // For loading images

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Create and configure the OCR engine.
        // -------------------------------------------------
        var ocrEngine = new OcrEngine();

        // Why set a license? Without it the engine runs in evaluation mode,
        // which adds a watermark to the output and limits batch size.
        ocrEngine.SetLicense("Aspose.OCR.lic");

        // -------------------------------------------------
        // 2️⃣ Load the receipt image – this is the **load image for OCR** step.
        // -------------------------------------------------
        // Change the path to point at your own receipt file.
        string imagePath = Path.Combine(
            Environment.CurrentDirectory, "receipt.png");

        // The ImageStream class abstracts file I/O and supports many formats.
        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // -------------------------------------------------
        // 3️⃣ Run the recognition process – this is where we **recognize receipt image**.
        // -------------------------------------------------
        var ocrResult = ocrEngine.Recognize();

        // -------------------------------------------------
        // 4️⃣ Export the layout information as JSON.
        // -------------------------------------------------
        string jsonResult = ocrResult.ToJson();
        File.WriteAllText("receipt.json", jsonResult);
        Console.WriteLine("✅ JSON saved to receipt.json");

        // -------------------------------------------------
        // 5️⃣ Export the same layout information as XML.
        // -------------------------------------------------
        string xmlResult = ocrResult.ToXml();
        File.WriteAllText("receipt.xml", xmlResult);
        Console.WriteLine("✅ XML saved to receipt.xml");

        // -------------------------------------------------
        // 6️⃣ Quick preview – print the plain text to console.
        // -------------------------------------------------
        Console.WriteLine("\n--- Extracted Text ---");
        Console.WriteLine(ocrResult.Text);
    }
}
```

### 為何這樣可行

* **`OcrEngine`** 為入口點；它保存所有日後可能調整的設定（語言、DPI 等）。  
* **`SetLicense`** 會移除評估水印——若你打算發佈程式碼，這是關鍵步驟。  
* **`ImageStream.FromFile`** 完成 **load image for OCR** 的工作，支援 PNG、JPEG、BMP、TIFF 等多種格式。  
* **`Recognize()`** 為實際執行 **recognize receipt image** 的方法。其內部會進行二值化、分割與字元分類。  
* 匯出為 JSON 與 XML 可同時取得人類可讀的資料與機器友好的結構，方便後續解析器使用。

## 步驟 3：執行示範並驗證輸出

編譯並執行：

```bash
dotnet run
```

若設定皆正確，將會看到類似以下的輸出：

```
✅ JSON saved to receipt.json
✅ XML saved to receipt.xml

--- Extracted Text ---
Walmart Supercenter
Date: 03/04/2026
Item    Qty   Price
Milk    2     2.58
Bread   1     1.99
Total   4.57
```

主控台會印出純文字，而 `receipt.json` 與 `receipt.xml` 則包含詳細的版面資訊（座標、信心分數等）。若日後需要將每一行對應至資料庫欄位，這些檔案相當方便。

## 邊緣情況與專業提示

### 1️⃣ 缺少或無效的授權

若 `SetLicense` 失敗，引擎會退回試用模式，輸出會帶有水印。請將呼叫包在 try/catch 中，並記錄友善訊息：

```csharp
try { ocrEngine.SetLicense("Aspose.OCR.lic"); }
catch (Exception ex)
{
    Console.WriteLine("⚠️ License not found – running in trial mode.");
    Console.WriteLine(ex.Message);
}
```

### 2️⃣ 不支援的影像格式

Aspose.OCR 支援大多數點陣圖格式，但若提供 PDF 或多頁 TIFF，必須先將所需頁面轉為影像。`Aspose.PDF` 函式庫可完成此轉換。

### 3️⃣ 大尺寸收據與效能

處理 10 MB 影像可能較慢。請在送入引擎前降低解析度：

```csharp
ocrEngine.Image = ImageStream.FromFile(imagePath).Resize(1024, 0);
```

`Resize` 方法會保持長寬比（高度設定為 `0`），大幅減少檔案大小，同時不會影響一般收據的 OCR 準確度。

### 4️⃣ 語言與字型問題

收據可能包含特殊字元（€, ¥ 等）。若已知語系，請明確設定語言：

```csharp
ocrEngine.Language = Language.English; // or Language.Spanish, etc.
```

對於混合語言的收據，可啟用多語言模式：

```csharp
ocrEngine.Language = Language.English | Language.French;
```

### 5️⃣ 抽取結構化資料

原始文字固然有用，但大多數應用程式需要結構化欄位（日期、總金額、項目）。JSON 版面包含每個單字的 `BoundingBox` 座標，可依下方式後處理：

```csharp
var layout = Newtonsoft.Json.Linq.JObject.Parse(jsonResult);
foreach (var word in layout["Words"])
{
    string text = (string)word["Text"];
    // Simple heuristics: look for "$" or "Total"
}
```

上述片段說明概念；在正式環境中，你可能會使用正規表達式或小型規則引擎。

## 常見問答

**Q: 我可以在 Linux 上執行嗎？**  
A: 當然可以。Aspose.OCR 為跨平台套件，只需在 Linux 主機上安裝 .NET 執行環境，即可使用相同程式碼。

**Q: 若需要每分鐘處理數十張收據該怎麼辦？**  
A: 建立 `Parallel.ForEach` 迴圈，重複使用單一 `OcrEngine` 實例——對於唯讀操作它是執行緒安全的。別忘了處理授權的併發限制。

**Q: 這能處理角度偏斜的手機相片嗎？**  
A: 引擎內建基本的去斜功能，但對於嚴重傾斜的影像，建議先使用影像處理函式庫（例如 OpenCV）進行校正，再交給 OCR。

## 完整可執行範例（直接複製貼上）

以下為完整程式碼，可直接貼入 `Program.cs`。除授權檔與收據影像外，無需其他檔案。

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Image;

class Program
{
    static void Main()
    {
        // Create and configure the OCR engine
        var ocrEngine = new OcrEngine();
        try
        {
            ocrEngine.SetLicense("Aspose.OCR.lic");
        }
        catch (Exception)
        {
            Console.WriteLine("⚠️ Running in trial mode – license not found.");
        }

        // Load the image to be processed (load image for OCR)
        string imagePath = Path.Combine(Environment.CurrentDirectory, "

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}