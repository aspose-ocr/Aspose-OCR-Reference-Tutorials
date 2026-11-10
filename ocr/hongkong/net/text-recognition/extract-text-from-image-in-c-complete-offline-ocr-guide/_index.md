---
category: general
date: 2026-03-18
description: 使用 Aspose OCR 在 C# 中從圖片提取文字。了解如何提取文字、執行 OCR 識別以及在無需網路的情況下識別西里爾文字。
draft: false
keywords:
- extract text from image
- how to extract text
- run OCR recognition
- recognize cyrillic text
- offline OCR with Aspose
language: zh-hant
og_description: 使用 Aspose OCR 從圖像中提取文字。一步一步的指南教您執行 OCR 識別、如何提取文字，以及離線識別西里爾文字。
og_title: 在 C# 中從圖像提取文字 – 離線 OCR 教學
tags:
- C#
- OCR
- Aspose
- Image Processing
title: 在 C# 中從圖像提取文字 – 完整離線 OCR 指南
url: /zh-hant/net/text-recognition/extract-text-from-image-in-c-complete-offline-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從圖像提取文字 – 完整離線 OCR 教學

是否曾需要 **從圖像提取文字**，卻擔心網路延遲或授權限制？你並不孤單。許多開發者在應用必須在受限環境中執行，同時又需要可靠的 OCR 時，常會卡關。好消息是：使用 Aspose OCR，你可以在本機完整執行整個流程，**從圖像提取文字**，完全不需要連線網際網路。

在本教學中，我們將示範一個實作範例，說明 **如何提取文字**、建置離線引擎、**執行 OCR 識別**，甚至 **辨識西里爾文字**。完成後，你將擁有一個可直接執行的 C# 主控台應用程式，會把偵測到的字串直接印在主控台上。

## 你需要的環境

- .NET 6.0 SDK（或任何較新的 .NET 版本）  
- Visual Studio 2022 或 VS Code（依個人喜好）  
- Aspose.OCR for .NET NuGet 套件  
- 一個包含 Aspose OCR 模型檔的資料夾（從 Aspose 入口網站下載一次即可）  
- 一張同時含有英文與西里爾字元的圖像檔（例如 `cyrillic_doc.jpg`）

不需要外部服務，也不會在執行時下載隱藏檔案——所有資源皆存放在本機磁碟。

## 步驟 1：安裝 Aspose.OCR 並準備資源

首先，將 Aspose.OCR NuGet 套件加入你的專案：

```bash
dotnet add package Aspose.OCR
```

接著，在電腦上任意位置建立一個名為 `AsposeOCRResources` 的資料夾，並把從 Aspose 下載的模型檔案複製進去。OCR 引擎會在此目錄尋找語言套件，請確保路徑正確。

> **專業提示：** 將資源資料夾放在 `.csproj` 檔旁邊，可簡化開發期間的路徑處理。

## 步驟 2：建置離線 OCR 引擎

現在，我們要實例化引擎並指向資源資料夾。這一步是讓我們 **離線執行 OCR 識別** 的關鍵。

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;

class OfflineDemo
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Tell the engine where the language models live
        ocrEngine.Settings.ResourcesPath = @"YOUR_DIRECTORY/AsposeOCRResources";

        // 3️⃣ Load the languages you need – English and Cyrillic
        ocrEngine.LoadLanguage(Language.English);
        ocrEngine.LoadLanguage(Language.Cyrillic);
```

為什麼要明確載入語言？因為我們告訴引擎必須保持離線；它不會向 Aspose 伺服器請求缺少的語言套件。如果忘記載入某個語言，該文字會被忽略。

## 步驟 3：將圖像傳入引擎

引擎就緒後，我們提供要處理的圖像。`ImageStream.FromFile` 輔助方法會把檔案讀成 OCR 引擎能理解的格式。

```csharp
        // 4️⃣ Load the target image (make sure the path points to your file)
        ImageStream image = ImageStream.FromFile(@"YOUR_DIRECTORY/cyrillic_doc.jpg");
```

如果圖像很大，建議先縮小尺寸以提升速度與準確度。OCR 引擎在約 300 DPI 時表現最佳。

## 步驟 4：執行辨識程序

呼叫 `Recognize` 便會執行繁重的辨識工作。此方法會回傳一個 `OcrResult` 物件，內含提取的字串、信心分數等資訊。

```csharp
        // 5️⃣ Run the OCR recognition
        OcrResult ocrResult = ocrEngine.Recognize(image);
```

在背後，Aspose 會解析位圖、執行語言專屬的神經網路，並將字元串接起來。因為我們同時載入了英文與西里爾語言套件，混合腳本的文件也能順利處理。

## 步驟 5：顯示提取的文字

最後，我們把結果輸出。實際應用中你可能會把文字寫入資料庫或傳給其他服務，但在此示範只會直接印出。

```csharp
        // 6️⃣ Show the extracted text on the console
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

執行程式後應會看到類似以下的輸出：

```
=== OCR Output ===
This is an English line.
Это строка на кириллице.
```

如果出現亂碼，請再次確認西里爾語言套件已正確放置於資源資料夾，且圖像不過於模糊。

![從圖像提取文字範例](extract_text_image.png "從圖像提取文字")

*圖片說明：從圖像提取文字 – OCR 結果顯示英文與西里爾語行。*

## 常見問題處理

### 缺少語言套件

若拋出「Language data not found」例外，表示引擎找不到模型檔。請檢查 `ResourcesPath`，確保資料夾內有 `english.dat`、`cyrillic.dat`（或同名檔案）。

### 低信心分數

有時 OCR 會對某些字元給予低信心，特別是圖像有噪點時。可透過以下方式提升準確度：

- 在送入引擎前先將圖像轉為灰階  
- 套用中值濾波降低斑點  
- 確保文字水平對齊（必要時旋轉圖像）

### 大尺寸圖像

處理 10 MP 照片可能較慢。建議將寬度最大縮至 2000 px，並保持長寬比；引擎仍能相當準確地捕捉大多數字元。

## 延伸範例

- **批次處理：** 將辨識邏輯包在迴圈中，遍歷資料夾內所有檔案。  
- **輸出格式：** `OcrResult` 也提供 `TextLines` 集合，內含文字框座標，適合在 UI 應用中高亮顯示文字。  
- **其他語言：** 只要呼叫 `LoadLanguage` 並傳入支援的列舉值（例如 `Language.French`），即可加入更多語言。  

所有這些擴充仍遵循 **如何提取文字** 的原則——載入相應語言套件，讓引擎自行完成其餘工作。

## 完整程式碼回顧

以下是可直接複製貼上的完整程式。請將 `YOUR_DIRECTORY` 替換為你機器上的實際路徑。

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;

class OfflineDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Point the engine to the folder that contains OCR model files
        ocrEngine.Settings.ResourcesPath = @"YOUR_DIRECTORY/AsposeOCRResources";

        // Step 3: Load the languages you need (no automatic download will occur)
        ocrEngine.LoadLanguage(Language.English);
        ocrEngine.LoadLanguage(Language.Cyrillic);

        // Step 4: Load the image you want to recognize
        ImageStream image = ImageStream.FromFile(@"YOUR_DIRECTORY/cyrillic_doc.jpg");

        // Step 5: Run the recognition process
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // Step 6: Display the extracted text
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

將此檔案存為 `Program.cs`，執行 `dotnet run`，即可在主控台看到引擎從圖像中抽取的文字。就這樣，你已成功 **離線從圖像提取文字**。

## 結語

我們已完整說明如何使用 Aspose OCR 在完全離線的情境下 **從圖像提取文字**。本指南展示了 **如何提取文字**、**執行 OCR 識別**，以及在不連網的前提下 **辨識西里爾文字** 與英文同時存在的情況。

從安裝 NuGet 套件到處理缺少語言套件等邊緣案例，你現在已具備在任何 .NET 應用中建置 OCR 功能的堅實基礎。

接下來可以嘗試處理 PDF、掃描多頁文件，或將輸出與搜尋索引結合。掌握離線 OCR 後，未來的可能性無限。

祝開發順利，願你的圖像永遠清晰可辨！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}