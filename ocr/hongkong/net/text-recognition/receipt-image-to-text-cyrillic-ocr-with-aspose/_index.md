---
category: general
date: 2026-04-01
description: 學習如何使用 Aspose OCR 將收據圖像轉換為文字。本指南說明如何提取西里爾文字、載入圖像進行 OCR，以及高效辨識西里爾字元。
draft: false
keywords:
- receipt image to text
- extract cyrillic text
- load image for ocr
- recognize cyrillic characters
- create OCR engine
language: zh-hant
og_description: 使用 Aspose OCR 將收據圖像轉換為文字。學習提取西里爾文字、載入圖像進行 OCR，並在 C# 中辨識西里爾字元。
og_title: 收據圖像轉文字 – 使用 Aspose 進行西里爾文 OCR
tags:
- OCR
- C#
- Aspose
- Cyrillic
title: 收據圖像轉文字 – Aspose 的西里爾文 OCR
url: /zh-hant/net/text-recognition/receipt-image-to-text-cyrillic-ocr-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 收據圖像轉文字 – 使用 Aspose 的西里爾文 OCR

有沒有曾經需要把 **receipt image to text** 轉成文字，但所有字元都是西里爾文？你並不是唯一一個為此抓狂的人。在許多零售或會計應用程式中，收據會以俄文、保加利亞文或塞爾維亞文顯示，而你仍然希望得到乾淨、可搜尋的字串。

在本教學中，我們將示範如何 **從收據照片中擷取西里爾文字**、**載入圖像進行 OCR**，以及使用 Aspose OCR 函式庫 **辨識西里爾字元**。完成後，你將擁有一個可直接執行的 C# 程式，會把 OCR 結果寫入 `.txt` 檔案。

## 需要的環境

- **.NET 6**（或任何較新的 .NET 版本）— 這段程式碼同樣支援 .NET Framework 4.7 以上。  
- **Aspose.OCR for .NET** NuGet 套件 — `Install-Package Aspose.OCR`。  
- 一張包含西里爾文字的收據範例圖（例如 `cyrillic_receipt.jpg`）。  
- 開發環境 — Visual Studio、VS Code 或 Rider 都可以。  

不需要額外的原生相依性；Aspose 內建語言模型，會在內部處理繁重的工作。

## receipt image to text – 設定 OCR 引擎

首先，我們必須 **建立 OCR 引擎** 實例，並告訴它我們要辨識的語言。Aspose 讓這件事變得非常簡單：

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;   // language and resource handling
using System.Drawing;      // Image class
using System.IO;

class CyrillicDemo
{
    static void Main()
    {
        // Step 1: Instantiate the OCR engine
        var ocrEngine = new OcrEngine();

        // Step 2: Tell Aspose we want Cyrillic support
        ocrEngine.Language = Language.Cyrillic;

        // Optional: Pre‑load the model if you’ll run offline later
        // ResourceManager.Preload(Language.Cyrillic);
```

> **小技巧：** 預先載入模型可避免程式首次執行時的網路呼叫，對於桌面或嵌入式情境相當方便。

## 如何擷取西里爾文字 – 載入收據圖像

引擎準備好之後，我們需要 **載入圖像進行 OCR**。`System.Drawing.Image` 類別對大多數點陣圖格式都相當適用。

```csharp
        // Step 3: Point to your receipt image
        string imagePath = @"YOUR_DIRECTORY\cyrillic_receipt.jpg";

        // Step 4: Load the image inside a using block (ensures disposal)
        using (var image = Image.FromFile(imagePath))
        {
            // Step 5: Run the OCR process
            var recognitionResult = ocrEngine.Recognize(image);
```

如果找不到檔案，`Image.FromFile` 會拋出 `FileNotFoundException`。在正式環境中，你可能想把整段程式碼包在 `try…catch` 區塊裡。

## 辨識西里爾字元 – 取得文字

`recognitionResult` 物件包含原始文字、信心分數，甚至還有邊界框資訊（若你之後需要的話）。對於簡單的「收據圖像轉文字」轉換，我們只需要把 `Text` 屬性寫入檔案：

```csharp
            // Step 6: Write the extracted text to a .txt file
            string outputPath = @"YOUR_DIRECTORY\cyrillic.txt";
            File.WriteAllText(outputPath, recognitionResult.Text);

            // Quick verification: print to console
            Console.WriteLine("OCR completed. Extracted text:");
            Console.WriteLine(recognitionResult.Text);
        }
    }
}
```

執行程式後，你應該會看到類似以下的輸出：

```
OCR completed. Extracted text:
СЧЕТ № 12345
Дата: 01/04/2026
Товар      Кол-во   Цена
Хлеб       2        30,00
Молоко     1        45,00
Итого:               105,00
```

這就是你想要的 **receipt image to text** 結果。

![收據圖像轉文字範例](receipt-ocr-example.png "收據圖像轉換為文字的範例")

*圖片說明：使用 Aspose OCR 擷取的西里爾字元，展示收據圖像轉文字的結果。*

## 邊緣案例與常見問題

### 若語言模型尚未下載該怎麼辦？

第一次設定 `ocrEngine.Language = Language.Cyrillic;` 時，Aspose 會自動下載所需模型。若機器沒有網路連線，預先載入的步驟會失敗。此時，你可以手動提供模型（請參考 Aspose 文件），或確保裝置能連到 `download.aspose.com`。

### 如何在同一張收據中處理多種語言？

可以傳入以逗號分隔的語言清單：

```csharp
ocrEngine.Language = Language.Cyrillic | Language.English;
```

Aspose 會嘗試同時辨識兩套字元。

### 我的收據模糊不清——如何提升辨識準確度？

Aspose OCR 提供基本的圖像前處理功能：

```csharp
ocrEngine.ImagePreprocessor = new ImagePreprocessor
{
    Sharpen = true,
    Binarize = true,
    Denoise = true
};
```

在呼叫 `Recognize` 之前先執行上述程式碼。

### 大量批次處理該怎麼做？

將辨識迴圈包在 `Parallel.ForEach` 中，並重複使用同一個 `OcrEngine` 實例（模型載入後即為執行緒安全）。若遇到執行緒安全問題，記得對引擎加鎖。

## 完整範例（結合所有步驟）

以下是可直接複製貼上的完整程式碼，已加入可選的預載入與基本錯誤處理：

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;
using System.Drawing;
using System.IO;

class CyrillicDemo
{
    static void Main()
    {
        try
        {
            // Create OCR engine and select Cyrillic language
            var ocrEngine = new OcrEngine();
            ocrEngine.Language = Language.Cyrillic;

            // Optional: preload model for offline use
            // ResourceManager.Preload(Language.Cyrillic);

            // Path to the receipt image
            string imagePath = @"YOUR_DIRECTORY\cyrillic_receipt.jpg";

            // Verify the file exists
            if (!File.Exists(imagePath))
                throw new FileNotFoundException("Receipt image not found.", imagePath);

            using (var image = Image.FromFile(imagePath))
            {
                // Perform OCR
                var result = ocrEngine.Recognize(image);

                // Output path for extracted text
                string outputPath = @"YOUR_DIRECTORY\cyrillic.txt";
                File.WriteAllText(outputPath, result.Text);

                Console.WriteLine("✅ receipt image to text conversion succeeded.");
                Console.WriteLine("Extracted text saved to: " + outputPath);
                Console.WriteLine("\n--- Extracted Text ---\n");
                Console.WriteLine(result.Text);
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine("❌ An error occurred: " + ex.Message);
        }
    }
}
```

在專案資料夾執行 `dotnet run`，即可得到包含 **receipt image to text** 輸出的 `.txt` 檔案。

## 結論

現在你已掌握一套完整、端對端的解決方案，能使用 Aspose OCR 把 **receipt image to text** 轉換為西里爾文字。我們說明了如何 **建立 OCR 引擎**、**載入圖像進行 OCR**、**擷取西里爾文字**，以及在幾行 C# 程式碼內 **辨識西里爾字元**。

接下來的步驟？試著處理整個收據資料夾、使用 `ImagePreprocessor` 提升準確度，或將 OCR 輸出結合資料庫實作自動化記帳。如果需要處理其他字母表，只要交換 `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}