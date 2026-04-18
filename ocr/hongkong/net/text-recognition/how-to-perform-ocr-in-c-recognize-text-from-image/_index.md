---
category: general
date: 2026-04-17
description: 學習如何在 C# 中執行 OCR，識別圖像中的文字，從 jpg 提取文字，並快速將圖像轉換為文字。
draft: false
keywords:
- how to perform OCR
- recognize text from image
- extract text from jpg
- convert image to text
- how to extract text
language: zh-hant
og_description: 如何在 C# 中執行 OCR？本指南將教你如何從圖像中辨識文字、從 JPG 提取文字，並在數分鐘內將圖像轉換為文字。
og_title: 如何在 C# 中執行 OCR – 從圖像辨識文字
tags:
- OCR
- C#
- Aspose
title: 如何在 C# 中執行 OCR – 從圖像辨識文字
url: /zh-hant/net/text-recognition/how-to-perform-ocr-in-c-recognize-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中執行 OCR – 從圖像辨識文字

有沒有想過 **how to perform OCR**（如何執行 OCR）在從掃描器或手機取得的圖片上？在許多專案中，你需要 **recognize text from image**（從圖像辨識文字）檔案——無論是收據、手寫筆記，或是轉成 JPEG 的 PDF 頁面。好消息是，使用 Aspose.OCR 只需幾行 C# 程式碼，就能 **extract text from jpg**（從 jpg 檔案提取文字）並 **convert image to text**（將圖像轉換為文字）。

在本教學中，我們將逐步說明完整流程，從安裝函式庫到處理缺少語言等 edge‑cases（邊緣情況）。完成後，你將清楚知道 **how to perform OCR**，並擁有一個可直接執行的程式，會將擷取的字串印到主控台。沒有模糊的「請參閱文件」捷徑——只有完整、獨立的解決方案。

## 需要的環境

- **.NET 6+**（此程式碼亦可在 .NET Framework 上執行，但 .NET 6 為目前的 LTS）
- **Aspose.OCR for .NET** NuGet 套件 – 使用 `dotnet add package Aspose.OCR` 安裝
- 想要測試的圖像檔案（JPEG、PNG、BMP）– 我們稱之為 `input.jpg`
- 任意你喜歡的 IDE（Visual Studio、Rider、VS Code）

就這樣。沒有額外設定、沒有外部服務，也沒有隱藏步驟。

## 步驟 1：安裝 Aspose.OCR 並加入參考

首先，將 OCR 函式庫加入你的專案。於專案資料夾開啟終端機並執行：

```bash
dotnet add package Aspose.OCR
```

此指令會取得最新的穩定版（截至 2026 年 4 月為 **23.9.0**），並更新你的 `.csproj`。之後，在檔案頂部加入 using 指令：

```csharp
using Aspose.OCR;
```

> **Pro tip:** 如果你使用 Visual Studio，NuGet 套件管理員 UI 同樣適用——只要搜尋 *Aspose.OCR* 即可。

## 步驟 2：載入要辨識的圖像

現在需要告訴 OCR 引擎要讀取哪張圖片。Aspose 提供方便的 `OcrImage.FromFile` 方法，支援大多數常見格式。

```csharp
// Step 2: Load the image you want to recognize
var ocrImage = OcrImage.FromFile(@"YOUR_DIRECTORY/input.jpg");
```

將 `YOUR_DIRECTORY` 替換為實際路徑，或將圖像放在執行檔旁並使用相對路徑。如果檔案不存在，該方法會拋出 `FileNotFoundException`，可於稍後捕捉。

## 步驟 3：建立 OCR 引擎（平台感知）

Aspose.OCR 會自動為執行中的作業系統（Windows、Linux、macOS）選擇最佳底層引擎。於 `using` 區塊內建立可確保正確釋放資源。

```csharp
// Step 3: Create the OCR engine (auto‑selects best engine for the platform)
using var ocrEngine = new OcrEngine();
```

為什麼要使用 `using`？引擎會持有原生資源（例如非受管記憶體），必須釋放。若忘記處置，特別是在迴圈中處理大量圖像時，會導致記憶體泄漏。

## 步驟 4：（可選）設定語言 – 預設為英文

如果圖像內的文字為英文，可跳過此步驟，因為預設即為 `OcrLanguage.English`。若為其他語言，只需指派相對應的 enum 值即可。

```csharp
// Step 4: (Optional) Specify the language – English is the default
ocrEngine.Language = OcrLanguage.English;
```

> **Did you know?** Aspose.OCR 支援超過 30 種語言，包括阿拉伯語、中文與俄文。切換語言只要更改 enum 即可。

## 步驟 5：執行辨識程序

呼叫 `Recognize` 會完成繁重的工作——像素分析、字元分割與字典查詢皆在底層自動執行。

```csharp
// Step 5: Run the recognition process on the loaded image
var ocrResult = ocrEngine.Recognize(ocrImage);
```

若引擎找不到任何文字，`ocrResult.Text` 會是空字串。你可能需要在繼續之前檢查 `ocrResult.HasText`（布林值）。

## 步驟 6：取得並顯示純文字結果

最後，擷取字串並寫入主控台。這就是實際 **convert image to text**（將圖像轉換為文字）的地方。

```csharp
// Step 6: Retrieve the plain‑text result and display it
string recognizedText = ocrResult.Text;
Console.WriteLine("Recognized text:");
Console.WriteLine(recognizedText);
```

輸出會類似以下內容：

```
Recognized text:
Invoice #12345
Date: 04/15/2026
Total: $256.78
```

## 完整可執行範例

以下是完整程式碼，可直接貼到新建的主控台應用程式（`dotnet new console`）中。內含最常見問題的錯誤處理。

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        try
        {
            // 1️⃣ Load the image you want to recognize
            var ocrImage = OcrImage.FromFile(@"YOUR_DIRECTORY/input.jpg");

            // 2️⃣ Create the OCR engine (auto‑selects best engine for the platform)
            using var ocrEngine = new OcrEngine();

            // 3️⃣ (Optional) Set language – English is default
            ocrEngine.Language = OcrLanguage.English;

            // 4️⃣ Run the recognition process
            var ocrResult = ocrEngine.Recognize(ocrImage);

            // 5️⃣ Check if any text was found
            if (!ocrResult.HasText || string.IsNullOrWhiteSpace(ocrResult.Text))
            {
                Console.WriteLine("No text could be extracted from the image.");
                return;
            }

            // 6️⃣ Retrieve and display the plain‑text result
            string recognizedText = ocrResult.Text;
            Console.WriteLine("Recognized text:");
            Console.WriteLine(recognizedText);
        }
        catch (FileNotFoundException)
        {
            Console.WriteLine("The specified image file was not found. Double‑check the path.");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"An unexpected error occurred: {ex.Message}");
        }
    }
}
```

> **Expected output:** 主控台會印出 OCR 引擎偵測到的精確字元。若來源圖像清晰且高解析度，準確率通常超過 95 %。

## 處理常見邊緣情況

### 1️⃣ 多語言圖像  
若有雙語收據，將 `ocrEngine.Language` 設為 `OcrLanguage.Multilingual`。引擎會自動嘗試偵測每種語言。

```csharp
ocrEngine.Language = OcrLanguage.Multilingual;
```

### 2️⃣ 低解析度或傾斜圖像  
在送入 Aspose 前先前處理圖像（旋轉、調整大小、提升對比度）。函式庫提供 `OcrImage` 方法，如 `Resize` 與 `Rotate`。

```csharp
ocrImage = ocrImage.Rotate(0.0); // placeholder – replace with actual angle if needed
```

### 3️⃣ 大批量處理  
處理數十個檔案時，重複使用同一個 `OcrEngine` 實例，而非每次迴圈都新建。完成批次後記得釋放它。

```csharp
using var batchEngine = new OcrEngine();
foreach (var file in Directory.GetFiles(@"images", "*.jpg"))
{
    var img = OcrImage.FromFile(file);
    var result = batchEngine.Recognize(img);
    // handle result…
}
```

### 4️⃣ Linux 容器的記憶體限制  
若在記憶體受限的 Docker 容器中執行，請設定 `ocrEngine.MaxMemoryUsage`（若 API 提供此屬性）以避免 OOM 異常。

## 專業技巧與注意事項

- **File Encoding:** 回傳的字串為 UTF‑16（.NET 中的 `string`）。若需以 UTF‑8 寫入檔案，請使用 `Encoding.UTF8.GetBytes(recognizedText)`。
- **Performance:** 單張圖像時，引擎初始化的開銷可忽略不計。大量工作時，僅初始化一次（參見批次範例）即可減少約 30 % 的處理時間。
- **Debugging:** 若 OCR 結果呈現亂碼，檢查 `ocrResult.Words`（各字詞物件的集合）以查看信心分數。信心低通常表示圖像模糊。
- **License:** Aspose.OCR 在未授權的評估模式下仍可使用，但會在輸出文字加上浮水印。於正式環境請註冊授權檔案（`Aspose.OCR.lic`）。

## 視覺概覽

![在 C# 中執行 OCR 範例](ocr-example.png "在 C# 中執行 OCR 範例")

*此螢幕截圖顯示執行範例程式碼後的完整主控台輸出。*

## 結論

現在你已掌握使用 Aspose.OCR 在 C# 中 **how to perform OCR** 的完整知識，且能自信地 **recognize text from image** 檔案、**extract text from jpg**，以及 **convert image to text**，以供後續任何處理。此範例涵蓋必要步驟，說明每個環節的原因，並暗示多語言支援與批次處理等進階情境。

接下來可以怎麼做？嘗試將 JPEG 換成 PNG、實驗 `OcrLanguage.Multilingual`，或將擷取的文字導入自然語言處理管線。只要能將圖片轉成可搜尋、可編輯的字串，可能性無限。

有任何問題或遇到困難嗎？在下方留言，我們祝你寫程式愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}