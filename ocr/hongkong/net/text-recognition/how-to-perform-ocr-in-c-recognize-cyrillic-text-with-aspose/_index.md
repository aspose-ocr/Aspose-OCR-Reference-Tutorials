---
category: general
date: 2025-12-30
description: 如何在 C# 中快速執行 OCR。學習從圖像提取文字、將圖像轉換為文字，並使用 Aspose OCR 識別西里爾文字。
draft: false
keywords:
- how to perform OCR
- extract text from image
- convert image to text
- recognize cyrillic text
- process image with OCR
language: zh-hant
og_description: 如何在 C# 中使用 Aspose 執行 OCR。本教程展示如何從圖像中提取文字、將圖像轉換為文字，以及識別西里爾字元。
og_title: 如何在 C# 中執行 OCR – 完整指南
tags:
- OCR
- C#
- Aspose
title: 如何在 C# 中執行 OCR – 使用 Aspose 識別西里爾文字
url: /zh-hant/net/text-recognition/how-to-perform-ocr-in-c-recognize-cyrillic-text-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中執行 OCR – 使用 Aspose 識別西里爾文字

有沒有想過 **如何執行 OCR** 於包含西里爾字母的圖片上？你並不孤單。許多開發者在需要從圖像檔案中擷取文字時會卡關，尤其當語言不是拉丁字母時。好消息是？使用 Aspose OCR，你只需幾行 C# 程式碼即可 **process image with OCR**，並取得乾淨、可搜尋的文字。

在本指南中，我們將逐步說明完整工作流程：從安裝 Aspose OCR 函式庫、載入西里爾語言模型，到最後 **extracting text from image** 並將結果印到主控台。完成後，你將能夠 **convert image to text** 且 **recognize cyrillic text**，毫不費力。

## 需要的條件

- .NET 6.0 或更新版本（此程式碼同樣適用於 .NET Core 與 .NET Framework）
- 有效的 Aspose OCR 授權或免費試用版（免費版在開發階段功能完整）
- 含有西里爾字元的圖像檔案（例如 `cyrillic_sample.png`）
- 放置 Aspose 提供之語言模組的資料夾（稍後會將引擎指向此資料夾）

就這樣——除了 Aspose OCR 之外不需要額外的 NuGet 套件，也沒有龐大的相依性。

## 步驟 1 – 安裝 Aspose OCR 並準備資源

首先，你需要將 Aspose OCR 套件加入專案。開啟終端機並執行：

```bash
dotnet add package Aspose.OCR
```

套件安裝完成後，從 Aspose 官方網站下載 **OCR language modules**，並解壓至你自行選擇的資料夾，例如 `C:\Aspose\ocr-modules`。稍後我們會將此資料夾指定給引擎，以便找到西里爾模型。

> **小技巧：** 請將模組資料夾放在解決方案目錄之外，以免不小心將大型二進位檔提交至原始碼管理。

## 步驟 2 – 建立最小化主控台應用程式

現在，我們來設定一個小型的主控台應用程式，以 **process image with OCR**。如果尚未有專案，請先建立新專案：

```bash
dotnet new console -n CyrillicOcrDemo
cd CyrillicOcrDemo
```

開啟 `Program.cs`，將其內容取代為以下完整可執行範例。每一行皆有註解，讓你清楚了解其用途。

```csharp
// ------------------------------------------------------------
// How to Perform OCR – Complete C# Example using Aspose OCR
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize the OCR engine.
        var ocrEngine = new OcrEngine();

        // 2️⃣ Tell the engine where the language modules live.
        //    Replace the path with the actual location on your machine.
        ocrEngine.ResourcesPath = @"C:\Aspose\ocr-modules";

        // 3️⃣ Load the Cyrillic language model explicitly.
        //    This ensures the engine knows how to read Cyrillic glyphs.
        ocrEngine.LoadLanguage(LanguageModel.Cyrillic);

        // 4️⃣ Perform OCR on the target image.
        //    The method returns an OcrResult object that holds the text.
        var ocrResult = ocrEngine.Recognize(@"C:\Aspose\cyrillic_sample.png");

        // 5️⃣ Output the recognized text to the console.
        Console.WriteLine("=== Recognized Cyrillic Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**每個步驟的重要性**

- **Initialize the OCR engine** – 這會建立處理所有圖像分析的核心物件。
- **ResourcesPath** – Aspose 將語言資料與核心 DLL 分離；指向該資料夾讓引擎載入正確的字典。
- **LoadLanguage(Cyrillic)** – 若未呼叫此方法，引擎會預設為英文，會導致西里爾字元亂碼。
- **Recognize(...)** – 這才是真正的 **convert image to text** 動作。它會讀取位圖、執行神經網路，並回傳結果。
- **Console.WriteLine** – 最後我們 **extract text from image** 並顯示於主控台，以證明 OCR 成功。

## 步驟 3 – 執行應用程式並驗證輸出

編譯並執行程式：

```bash
dotnet run
```

若設定正確，你應該會看到類似以下的結果：

```
=== Recognized Cyrillic Text ===
Привет, мир! Это пример текста на кириллице.
```

該行即為 OCR 引擎從 `cyrillic_sample.png` 取得的完整文字。於實務上，你可以將此字串存入資料庫、送入搜尋索引，或即時翻譯。

### 常見問題與避免方式

| 問題 | 原因 | 解決方式 |
|-------|--------|-----|
| **Empty output** | 找不到語言模組或 `ResourcesPath` 錯誤。 | 再次確認資料夾路徑，並確保 Cyrillic `.bin` 檔案存在。 |
| **Garbage characters** | 語言模型錯誤（預設為英文）。 | 在 `Recognize` 前呼叫 `LoadLanguage(LanguageModel.Cyrillic)`。 |
| **File not found** | 圖像路徑拼寫錯誤。 | 使用絕對路徑或搭配 `AppContext.BaseDirectory` 使用 `Path.Combine`。 |
| **Performance lag** | 大型圖像以全解析度處理。 | 在 OCR 前將圖像寬度調整至 ≤ 1024 px；Aspose 提供 `Resize` 方法。 |

## 步驟 4 – 擴充範例：批次處理

通常你需要對多個檔案 **process image with OCR**。以下是一段快速程式碼，會遍歷目錄、對每個 PNG 執行 OCR，並將結果寫入文字檔。

```csharp
using System.IO;

// Assume ocrEngine is already configured as in the previous example.
string inputFolder = @"C:\Aspose\Samples";
string outputFolder = @"C:\Aspose\Results";

foreach (var filePath in Directory.GetFiles(inputFolder, "*.png"))
{
    var result = ocrEngine.Recognize(filePath);
    string fileName = Path.GetFileNameWithoutExtension(filePath);
    string outPath = Path.Combine(outputFolder, $"{fileName}.txt");
    File.WriteAllText(outPath, result.Text);
    Console.WriteLine($"Processed {fileName} → {outPath}");
}
```

## 步驟 5 – 當你需要超出西里爾語的支援時

Aspose OCR 支援數十種語言（阿拉伯語、印地語、中文等）。若要切換語言，只需更換列舉值：

```csharp
ocrEngine.LoadLanguage(LanguageModel.Arabic);
```

甚至可以同時載入多種語言：

```csharp
ocrEngine.LoadLanguages(LanguageModel.Cyrillic, LanguageModel.English);
```

此彈性讓相同程式碼可 **convert image to text** 用於多語言檔案庫。

## 完整可執行範例（直接複製貼上）

以下為完整程式碼，可直接放入 `Program.cs`。內容完整——只需將佔位路徑換成自己的即可。

```csharp
// ------------------------------------------------------------
// How to Perform OCR – Full End‑to‑End Example
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Initialize the OCR engine.
        var ocrEngine = new OcrEngine();

        // Point to the folder containing language modules.
        ocrEngine.ResourcesPath = @"C:\Aspose\ocr-modules";

        // Load Cyrillic language model.
        ocrEngine.LoadLanguage(LanguageModel.Cyrillic);

        // Recognize text from a Cyrillic image.
        var ocrResult = ocrEngine.Recognize(@"C:\Aspose\cyrillic_sample.png");

        // Output the result.
        Console.WriteLine("=== Recognized Cyrillic Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

執行後，你會在主控台看到完整的西里爾字串——證明你已掌握 **how to perform OCR** 在 C# 中的使用方法。

## 結論

我們已說明如何使用 Aspose OCR 在含有西里爾字元的圖像上 **how to perform OCR**。從安裝函式庫、載入正確語言模型，到單張或批次 **extract text from image**，你現在擁有任何文字擷取專案的堅實基礎。

接下來的步驟？嘗試將語言模型換成 **recognize cyrillic text** 搭配英文，測試不同圖像格式，或將輸出串接至翻譯 API。只要能可靠地 **convert image to text**，就沒有做不到的。

對於邊緣案例（例如低解析度掃描或雜訊背景）有疑問嗎？在下方留言，我們祝你編程愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}