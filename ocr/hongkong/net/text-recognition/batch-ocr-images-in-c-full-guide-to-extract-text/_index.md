---
category: general
date: 2026-02-24
description: 使用 Aspose.OCR 於 C# 快速批量 OCR 圖像。了解如何從目錄讀取檔案、辨識圖像中的文字，並在幾個步驟內將圖像轉換為文字。
draft: false
keywords:
- batch OCR images
- extract text from images
- read files from directory
- recognize text from image
- convert image to text
language: zh-hant
og_description: 批次 OCR 圖像於 C# 使用 Aspose.OCR。本教學示範如何從目錄讀取檔案、辨識圖像文字，並高效地將圖像轉換為文字。
og_title: 批量 OCR 圖像（C#）– 完整逐步指南
tags:
- C#
- OCR
- Aspose
title: 在 C# 中批量 OCR 圖像 – 完整的文字提取指南
url: /zh-hant/net/text-recognition/batch-ocr-images-in-c-full-guide-to-extract-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 批次 OCR 圖像於 C# – 完整文字提取指南

是否曾需要**批次 OCR 圖像**卻不知從何開始？你並不孤單——許多開發者在首次嘗試**大量從圖像提取文字**時都會卡關。好消息是，只要幾行 C# 程式碼結合 Aspose.OCR，即可把整個資料夾的圖片快速轉換成整齊的 `.txt` 檔案。

在本教學中，我們將逐步說明完整流程：從目錄讀取檔案、將每張圖片送入 OCR 引擎，最後**將圖像轉換為文字**檔案，讓你可以進行索引、搜尋或輸入後續的資料流程。完成後，你將擁有一個可自行執行的主控台應用程式，能直接嵌入任何 .NET 解決方案中。

## 需求條件

- **.NET 6+**（範例以 .NET 6 編譯，但任何較新的版本皆可使用）
- **Aspose.OCR** NuGet 套件 (`Install-Package Aspose.OCR`)
- 欲處理的圖像檔案資料夾（如 `.png`、`.jpg` 等）
- Visual Studio、Rider 或你喜愛的編輯器

不需要額外的設定檔或外部服務——只要純粹的 C# 程式碼即可在本機執行。

## 批次 OCR 圖像 – 建立專案

首先，建立一個新的主控台專案：

```bash
dotnet new console -n BatchOcrDemo
cd BatchOcrDemo
dotnet add package Aspose.OCR
```

此指令會產生最小化的專案結構並下載 OCR 函式庫。還原完成後，即可加入核心程式碼。

### 從目錄讀取檔案

我們需要告訴程式來源圖像所在位置以及產生的文字檔要存放在哪裡。使用 `System.IO` 可輕鬆完成此步驟。

```csharp
using System;
using System.IO;
using Aspose.OCR;

class BatchExample
{
    static void Main()
    {
        // 1️⃣ Define input and output folders
        string inputFolder  = @"C:\Images\ToProcess";   // <-- change to your source folder
        string outputFolder = @"C:\Images\OcrResults"; // <-- change to your target folder

        // 2️⃣ Ensure the output folder exists
        Directory.CreateDirectory(outputFolder);
```

> **此步驟的重要性：** 若輸出目錄不存在，程式在寫入 `.txt` 檔時會拋出例外。`CreateDirectory` 為冪等操作——若資料夾已存在則不會有任何動作，因此每次執行都安全呼叫。

### 從圖像辨識文字並將圖像轉換為文字

現在我們啟動 OCR 引擎，並對找到的每個檔案進行迴圈。此迴圈使用 `Directory.GetFiles` 搭配萬用字元 (`*.*`) 以取得*所有*檔案，若需要可將過濾條件改為 `*.png` 或 `*.jpg`。

```csharp
        // 3️⃣ Initialise the OCR engine
        var ocrEngine = new OcrEngine();

        // 4️⃣ Process each image file in the input folder
        foreach (var imagePath in Directory.GetFiles(inputFolder, "*.*", SearchOption.TopDirectoryOnly))
        {
            // 5️⃣ Recognise text from the current image
            var ocrResult = ocrEngine.RecognizeImage(imagePath);

            // 6️⃣ Save the recognised text to a .txt file in the output folder
            string textFilePath = Path.Combine(
                outputFolder,
                Path.GetFileNameWithoutExtension(imagePath) + ".txt");

            File.WriteAllText(textFilePath, ocrResult.Text);
        }

        Console.WriteLine("✅ All images processed. Check the output folder!");
    }
}
```

**這段程式碼在做什麼？**  
- `ocrEngine.RecognizeImage(imagePath)` 讀取位圖、執行 OCR 演算法，並回傳 `OcrResult` 物件。  
- `ocrResult.Text` 包含引擎所辨識出的純文字內容。  
- `File.WriteAllText` 會建立新檔（或覆寫既有檔案），寫入擷取出的文字。

這就是完整的 **批次 OCR 圖像** 流程，程式碼不超過 30 行。

## 專業提示與邊緣情況

| 情況 | 建議 |
|-----------|----------------|
| 圖像檔案過大（> 5 MB） | 先將寬度縮放至約 1500 px，以加快辨識速度且不失準確度。 |
| 需要支援 PDF | 先將每頁 PDF 轉為圖像（例如使用 `Aspose.PDF`），再交給相同的迴圈處理。 |
| 有些檔案不是圖像（例如 `.txt`） | 加入簡易過濾：`if (!imagePath.EndsWith(".png") && !imagePath.EndsWith(".jpg")) continue;` |
| 想要多語言支援 | 在迴圈前設定 `ocrEngine.Language = Language.English | Language.Spanish;` |
| 需要進度回報 | 在 foreach 內寫入 `Console.WriteLine($"Processing {Path.GetFileName(imagePath)}...");` |

> **專業提示：** 將 OCR 呼叫包在 `try/catch` 中。偶爾損壞的圖像會導致 `RecognizeImage` 拋出例外，處理後可避免整批作業中斷。

## 預期輸出

程式執行完畢後，`outputFolder` 內會為每個原始圖像產生對應的 `.txt` 檔案：

```
C:\Images\OcrResults\invoice1.txt
C:\Images\OcrResults\receipt_2024-01-15.txt
C:\Images\OcrResults\signage.png.txt   <-- note the .txt extension
```

每個檔案皆保存引擎擷取的原始文字，例如：

```
Invoice #12345
Date: 01/15/2024
Total: $1,250.00
Thank you for your business!
```

現在你可以將這些檔案匯入搜尋索引、執行情感分析，或僅作為合規保存。

## 常見問題

**Q: 這在 Linux 上能運作嗎？**  
A: 當然可以。Aspose.OCR 為跨平台套件，且此處使用的 `System.IO` API 與作業系統無關。只需調整資料夾路徑（例如 `/home/user/images`）。

**Q: 如果需要**遞迴讀取目錄中的檔案**該怎麼做？**  
A: 將 `SearchOption.TopDirectoryOnly` 改為 `SearchOption.AllDirectories`。請留意較深層資料夾的權限問題。

**Q: OCR 的準確度如何？**  
A: 準確度受圖像品質、字型與語言影響。為獲得最佳效果，請使用高解析度掃描且背景乾淨。亦可調整 `ocrEngine.Config` 以啟用去斜或降噪功能。

## 結語

你剛剛學會如何在 C# 中使用 Aspose.OCR **批次 OCR 圖像**，從讀取目錄檔案、**從圖像辨識文字**，到最終 **將圖像轉換為文字** 檔案，以供儲存或後續處理。上述完整可執行的範例應可直接使用，而提示部分則提供了擴充或自訂解決方案的藍圖。

下一步？可嘗試使用 WinForms 或 WPF 加入簡易 UI、將輸出整合至 Azure Cognitive Search，或測試 Aspose.OCR 支援的其他語言。掌握核心迴圈後，想像空間無限。

祝開發順利，願你的 OCR 批次處理無錯誤！  

![Diagram of batch OCR images process](batch-ocr-images-diagram.png "Batch OCR images workflow")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}