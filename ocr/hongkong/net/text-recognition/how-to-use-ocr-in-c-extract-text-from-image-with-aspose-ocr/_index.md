---
category: general
date: 2026-02-24
description: 如何在 C# 中使用 OCR 從圖像檔案提取文字。學習將 PNG 轉換為文字、非同步讀取圖像，並處理常見陷阱。
draft: false
keywords:
- how to use OCR
- extract text from image
- convert png to text
- how to extract text
- how to read image
language: zh-hant
og_description: 如何在 C# 中使用 OCR 從圖片擷取文字。本指南逐步示範使用 Aspose 進行非同步 OCR，涵蓋轉換、錯誤處理及最佳實踐。
og_title: 在 C# 中使用 OCR 完整指南
tags:
- OCR
- C#
- Aspose
title: 如何在 C# 中使用 OCR – 使用 Aspose OCR 從圖像提取文字
url: /zh-hant/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 OCR – 從圖像提取文字

有沒有想過 **how to use OCR** 從圖片中提取文字而不需要手動輸入？你並不孤單。許多開發者在需要 *extract text from image* 檔案（如 PNG）時會卡住，而一般的複製貼上方法根本無法解決。  

在本教學中，我們將逐步說明一個完整的非同步解決方案，使用 Aspose.OCR 函式庫 **converts PNG to text**。完成後，你將清楚了解如何讀取圖像檔案、處理錯誤，並將結果整合到自己的應用程式中。  

我們會涵蓋從設定 NuGet 套件到微調 OCR 引擎以提升準確度的所有內容，並提供在圖像不夠清晰時的處理技巧。無需追尋文件連結——所有資訊都在此處。

## 需要的環境

- .NET 6.0 或更新版本（此程式碼同樣適用於 .NET Core 與 .NET Framework）  
- Visual Studio 2022（或任何你偏好的 IDE）  
- **Aspose.OCR** NuGet 套件（`Install-Package Aspose.OCR`）  
- 一個你想處理的圖像檔案（PNG、JPG、BMP）——我們稱之為 `input.png`

就這樣。如果你已勾選以上項目，即可開始。

![顯示 OCR 工作流程的圖示 – 如何使用 OCR 從圖像提取文字](/images/ocr-workflow.png)

## 步驟 1：安裝 Aspose.OCR 並加入命名空間

首先，將函式庫加入你的專案。打開套件管理員主控台並執行以下指令：

```powershell
Install-Package Aspose.OCR
```

接著，在 C# 檔案的最上方加入必要的命名空間：

```csharp
using Aspose.OCR;
using System;
using System.Threading.Tasks;
```

> **Pro tip:** 如果你使用 .NET 6 最小化 API，可以將這些 `using` 陳述式放在全域檔案中，避免在多個類別中重複寫入。

### 為什麼這很重要

`Aspose.OCR` 命名空間讓你可以使用 `OcrEngine`，這個核心類別負責讀取圖像。若沒有它，你必須自行編寫像素分析程式碼，會陷入巨大的坑洞。加入命名空間可讓程式碼保持整潔，並告訴編譯器在何處尋找你將使用的型別。

## 步驟 2：建立非同步 OCR 引擎

我們會將 OCR 呼叫包在 `async` 方法中，讓 UI 保持回應，且伺服器端程式碼能夠擴展。以下是一個主控台應用程式的骨架：

```csharp
class AsyncExample
{
    static async Task Main()
    {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Recognize text from the image asynchronously
        OcrResult ocrResult = await ocrEngine.RecognizeImageAsync("YOUR_DIRECTORY/input.png");

        // Output the extracted text
        Console.WriteLine(ocrResult.Text);
    }
}
```

### 說明

- **`OcrEngine ocrEngine = new OcrEngine();`** – 使用預設設定建立引擎實例。之後你可以微調語言、偵測模式或前處理濾鏡。  
- **`await ocrEngine.RecognizeImageAsync(...)`** – 這個非同步方法會回傳 `Task<OcrResult>`。await 它可在 OCR 背景執行時釋放執行緒。  
- **`ocrResult.Text`** – 引擎能讀取的所有內容的純文字表示。這就是 *how to extract text* 從圖像的核心。

## 步驟 3：微調引擎以提升準確度

開箱即用的 OCR 在乾淨且高對比度的圖像上表現良好，但實際情況的圖片常常需要額外協助。你可以在呼叫 `RecognizeImageAsync` 前調整一些屬性：

```csharp
// Set language (English is default, but you can add more)
ocrEngine.Language = OcrLanguage.English;

// Enable automatic image preprocessing (deskew, despeckle)
ocrEngine.ImagePreprocessingOptions = ImagePreprocessingOptions.Auto;

// If you only need numbers, restrict the character set
ocrEngine.Characters = "0123456789";
```

### 何時使用這些設定

- **低品質掃描** – 開啟 `ImagePreprocessingOptions.Auto` 讓 Aspose 清除雜訊。  
- **多語言 PDF** – 將 `Language` 改為 `OcrLanguage.French`，或使用位元遮罩結合多種語言。  
- **表單欄位** – 限制 `Characters` 為數字或大寫字母，以減少誤判。

## 步驟 4：優雅地處理錯誤

OCR 並非魔法；若檔案遺失、損毀或格式不支援，可能會失敗。將非同步呼叫包在 try/catch 區塊中：

```csharp
try
{
    OcrResult ocrResult = await ocrEngine.RecognizeImageAsync("YOUR_DIRECTORY/input.png");
    Console.WriteLine("Extracted Text:");
    Console.WriteLine(ocrResult.Text);
}
catch (FileNotFoundException ex)
{
    Console.Error.WriteLine($"File not found: {ex.Message}");
}
catch (OcrException ex)
{
    Console.Error.WriteLine($"OCR failed: {ex.Message}");
}
```

### 為什麼這有幫助

提供清晰的錯誤訊息可加速除錯並提升最終使用者體驗。與其出現通用崩潰，倒不如顯示有用的提示，告訴你是要檢查路徑、檔案格式，或是 OCR 引擎的設定。

## 步驟 5：整合完整範例 – 完整可執行範例

以下是一個完整、可直接執行的主控台程式，示範 **how to use OCR**、套用前處理並處理錯誤。將它複製貼上到新的 `.csproj` 後按 F5 執行。

```csharp
using Aspose.OCR;
using System;
using System.IO;
using System.Threading.Tasks;

class AsyncOcrDemo
{
    static async Task Main()
    {
        // 1️⃣  Initialize the OCR engine with optional tweaks
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English,
            ImagePreprocessingOptions = ImagePreprocessingOptions.Auto
        };

        // 2️⃣  Define the path to the image you want to read
        string imagePath = Path.Combine(Environment.CurrentDirectory, "input.png");

        // 3️⃣  Perform the async recognition inside a safe try/catch
        try
        {
            OcrResult result = await ocrEngine.RecognizeImageAsync(imagePath);
            Console.WriteLine("\n--- Extracted Text ---\n");
            Console.WriteLine(result.Text);
            Console.WriteLine("\n--- End of Output ---\n");
        }
        catch (FileNotFoundException fnf)
        {
            Console.Error.WriteLine($"❌ Image not found: {fnf.Message}");
        }
        catch (OcrException ocrEx)
        {
            Console.Error.WriteLine($"❌ OCR processing error: {ocrEx.Message}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"❌ Unexpected error: {ex.Message}");
        }
    }
}
```

**預期輸出**（假設 `input.png` 包含「Hello World」這句話）：

```
--- Extracted Text ---

Hello World

--- End of Output ---
```

如果圖像模糊，可能會出現多餘字元或遺漏文字——這時 Step 3 的前處理選項就顯得非常關鍵。

## 步驟 6：擴充解決方案 – 從 PNG 轉為 PDF 或文字檔

有時你需要 **convert PNG to text**，再將結果存成 `.txt` 或嵌入 PDF 報告。以下是一段快速程式碼，將 OCR 輸出寫入檔案：

```csharp
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.txt");
await File.WriteAllTextAsync(outputPath, result.Text);
Console.WriteLine($"✅ Text saved to {outputPath}");
```

或者，若你使用 Aspose.PDF 產生 PDF：

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// ... after OCR result is obtained
Document pdfDoc = new Document();
Page page = pdfDoc.Pages.Add();
TextFragment fragment = new TextFragment(result.Text);
page.Paragraphs.Add(fragment);
pdfDoc.Save("Result.pdf");
Console.WriteLine("✅ PDF created with extracted text.");
```

這些擴充示範了 **how to read image** 資料如何供給後續流程——報告產生、搜尋索引，甚至餵入語言模型。

## 常見問題與特殊情況

| Question | Answer |
|----------|--------|
| *支援哪些圖像格式？* | Aspose.OCR 支援 PNG、JPEG、BMP、TIFF 與 GIF。若有 PDF，請先將其頁面轉為圖像。 |
| *我可以平行處理多張圖像嗎？* | 可以——將每個 `RecognizeImageAsync` 呼叫包在各自的 task 中，並使用 `Task.WhenAll`。但需留意記憶體使用量。 |
| *如果 OCR 回傳空文字怎麼辦？* | 檢查圖像品質：低對比度或旋轉的文字常會失敗。可啟用 `ImagePreprocessingOptions.Deskew`，或在 OCR 前手動旋轉圖像。 |
| *圖像大小有上限嗎？* | 大型圖像（>10 MP）可能導致 `OutOfMemoryException`。在辨識前請將其縮小至合理解析度（例如 300 DPI）。 |
| *使用 Aspose.OCR 是否需要授權？* | 開發模式可使用臨時授權，但正式環境需購買授權以移除評估水印。 |

## 效能建議

- **重複使用 `OcrEngine` 實例** 以進行批次處理；每張圖像重新建立引擎會增加開銷。  
- **關閉未使用的語言** 以加速偵測——每多一種語言都會增加少量處理成本。  
- **在背景執行緒上執行 OCR**（如前所示），可讓桌面或 Web 應用程式的 UI 執行緒保持流暢。

## 結論

我們已完整說明在 C# 中 **how to use OCR** 的全流程：安裝 Aspose.OCR、撰寫非同步方法、為噪點圖像微調設定、處理錯誤以及儲存結果。現在你擁有可靠的方式來 *extract text from image* 檔案、*convert PNG to text*，甚至將文字輸入其他工作流程，如 PDF 產生。  

準備好接受下一個挑戰了嗎？試著將 OCR 輸出寫入可搜尋的 Azure Cognitive Search 索引，或透過在引擎中加入 `OcrLanguage.Spanish | OcrLanguage.French` 來實驗多語言 OCR。只要了解 **how to read image** 資料的程式寫法，便能無所限制。  

*如果你覺得本指南對你有幫助，請在 GitHub 上給予星標，與同事分享，或在下方留言分享你的 OCR 小技巧。祝開發愉快！*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}