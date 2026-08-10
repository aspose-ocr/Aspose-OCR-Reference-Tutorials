---
category: general
date: 2026-02-24
description: C# OCR 教學，示範如何使用 Aspose OCR 從圖像中提取文字——為 .NET 開發者提供的完整一步一步指南。
draft: false
keywords:
- c# ocr tutorial
- how to extract text from image
- Aspose OCR C#
- OCR region of interest
- image text extraction C#
language: zh-hant
og_description: C# OCR 教學，示範如何使用 Aspose OCR 從圖像中提取文字——為 .NET 開發者提供的完整、一步一步的指南。
og_title: C# OCR 教學：使用 Aspose OCR 從圖片提取文字
tags:
- C#
- OCR
- Aspose
- Image Processing
title: C# OCR 教學：使用 Aspose OCR 從圖像提取文字
url: /zh-hant/net/text-recognition/c-ocr-tutorial-extract-text-from-images-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr 教學 – 使用 Aspose OCR 從圖像提取文字

有沒有想過如何在 C# 應用程式中從圖像檔案提取文字？你並不是唯一有此疑問的人。在許多實務專案中——例如護照掃描器、發票處理器，甚至簡單的收據讀取器——取得可靠的 OCR 結果是每日的挑戰。  

本 **c# ocr 教學** 會帶你一步步使用 Aspose OCR 的實用解決方案，完整示範 **如何從圖像檔案提取文字**、將掃描限制於感興趣區域，並顯示結果——全部只需幾行程式碼。  

我們會涵蓋你所需的一切：NuGet 套件、必要的 `using` 陳述式、ROI 設定、選項配置，以及對輸出結果的快速檢查。完成後，你將擁有一個可執行的 Console 應用程式，能從護照掃描（或任何你指定的圖像）中擷取姓名。沒有多餘的說明，只有清晰完整的解答，直接複製貼上即可執行。

## 前置條件

- .NET 6+ SDK（或如果你偏好舊版執行環境，可使用 .NET Framework 4.7+）
- Visual Studio 2022 或任何支援 C# 的編輯器
- 具備網路連線以下載 **Aspose.OCR** NuGet 套件
- 一個圖像檔案（例如 `passport_scan.png`），內含可辨識的文字

> **小技巧：** 若在本機測試，請將小尺寸的 PNG 或 JPEG 放入專案內名為 `Images` 的資料夾——這樣路徑較短，程式碼也更整潔。

## 步驟 1：安裝 Aspose OCR 並加入命名空間

首先，我們需要 OCR 函式庫。開啟終端機（或套件管理員主控台）並執行以下指令：

```bash
dotnet add package Aspose.OCR
```

套件安裝完成後，於 `Program.cs` 檔案頂部加入必要的 `using` 指令：

```csharp
using Aspose.OCR;          // Core OCR engine
using System.Drawing;     // Rectangle struct for ROI
```

這兩行程式碼讓你可以使用 `OcrEngine`、`OcrOptions`，以及我們將用來限制掃描區域的 `Rectangle` 類型。

## 步驟 2：建立 OCR Engine 實例

Engine 是此流程的核心。可將其視為讀取像素並轉換為文字的「大腦」。初始化相當簡單：

```csharp
// Step 2: Instantiate the OCR engine – this object does the heavy lifting.
OcrEngine ocrEngine = new OcrEngine();
```

> **為什麼這很重要：** 單一個 `OcrEngine` 可重複使用於多張圖像，能節省記憶體並避免重複的授權檢查。

## 步驟 3：定義感興趣區域 (ROI)

掃描整張高解析度圖像可能會浪費資源，特別是當你已清楚知道文字所在位置（例如護照上的姓名欄位）時。透過指定 **感興趣區域**，即可告訴 Engine 忽略矩形之外的所有內容。

```csharp
// Step 3: Set the ROI – adjust X, Y, Width, Height to match your image layout.
Rectangle regionOfInterest = new Rectangle(150, 300, 800, 200);
```

- **X** 與 **Y** 代表矩形左上角的座標。
- **Width** 與 **Height** 定義矩形的寬度與高度。

如果不確定確切數值，可使用任何圖像編輯器（如 Paint.NET）快速視覺測試，以找出座標位置。

## 步驟 4：設定 OCR 選項並套用 ROI

現在我們將 ROI 綁定至 `OcrOptions` 物件。此物件同時允許調整語言、偵測速度等設定，但在本教學中我們僅保留最基本的設定。

```csharp
// Step 4: Prepare OCR options and assign the ROI we just defined.
OcrOptions ocrOptions = new OcrOptions { Roi = regionOfInterest };
```

> **邊緣情況：** 若省略 ROI，Aspose OCR 會掃描整張圖像，可能導致處理時間增加，且結果中會出現更多雜訊。

## 步驟 5：對圖像執行 OCR Engine

所有設定完成後，就可以正式辨識文字了。提供圖像路徑以及剛才建立的選項。

```csharp
// Step 5: Perform OCR on the target image using the configured options.
OcrResult ocrResult = ocrEngine.RecognizeImage(
    "Images/passport_scan.png", // Adjust this path to your file location
    ocrOptions);
```

此方法會回傳 `OcrResult` 物件，內含擷取的字串、信心分數，甚至每個單字的邊界框（若日後需要）。

## 步驟 6：輸出擷取的文字

最後，將結果顯示出來。在實際應用中，你可能會將其寫入資料庫，但在本教學中只需簡單的 Console 輸出即可。

```csharp
// Step 6: Show the extracted text in the console.
Console.WriteLine("Extracted name: " + ocrResult.Text);
```

執行程式後，應會看到類似以下的輸出：

```
Extracted name: JOHN DOE
```

若輸出為空或雜亂，請再次確認 ROI 座標，並確保來源圖像清晰（高對比、少模糊）。

## 完整範例程式

以下為完整的 `Program.cs` 檔案，可直接編譯。將其存於 Console 專案中，將圖像放入 `Images` 資料夾，然後按 **F5** 執行。

```csharp
using Aspose.OCR;
using System.Drawing;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create an OCR engine instance
            OcrEngine ocrEngine = new OcrEngine();

            // Step 2: Define the region of interest (ROI) where the text is expected
            // (x, y, width, height) – adjust these values for your own image
            Rectangle regionOfInterest = new Rectangle(150, 300, 800, 200);

            // Step 3: Prepare OCR options and assign the ROI
            OcrOptions ocrOptions = new OcrOptions { Roi = regionOfInterest };

            // Step 4: Perform OCR on the target image using the configured options
            OcrResult ocrResult = ocrEngine.RecognizeImage(
                "Images/passport_scan.png",
                ocrOptions);

            // Step 5: Display the extracted text
            Console.WriteLine("Extracted name: " + ocrResult.Text);
        }
    }
}
```

> **預期輸出：**  
> `Extracted name: JOHN DOE`（或任何位於指定 ROI 內的文字）

## 常見問題與邊緣情況

### 如果我的圖像是其他格式呢？

Aspose OCR 支援 PNG、JPEG、BMP、TIFF，甚至 PDF。只要在路徑中更改檔案副檔名，Engine 會自動偵測格式。

### 能否在迴圈中處理多張圖像？

當然可以。`OcrEngine` 可以重複使用：

```csharp
foreach (var file in Directory.GetFiles("Images", "*.png"))
{
    var result = ocrEngine.RecognizeImage(file, ocrOptions);
    Console.WriteLine($"{Path.GetFileName(file)} → {result.Text}");
}
```

### 如何提升非拉丁文字的辨識準確度？

在 `OcrOptions` 上設定 language 屬性：

```csharp
ocrOptions.Language = Language.English; // or Language.Russian, Language.ChineseSimplified, etc.
```

### 如果 ROI 設定錯誤，導致漏掉文字該怎麼辦？

你可以將矩形放大，或直接省略 ROI，讓 Engine 掃描整張圖片。請留意，掃描全圖可能會增加處理時間。

## 專業提示：提升使用體驗

- **快取 Engine：** 為每張圖像建立新的 `OcrEngine` 會產生額外開銷。只要在應用程式執行期間保持單一實例即可。
- **前處理圖像：** 簡單的步驟如轉為灰階或提升對比度，可顯著提升辨識率。
- **處理 null 結果：** 使用前務必檢查 `ocrResult?.Text`，以避免 `NullReferenceException`。
- **授權重要：** 免費版在前 200 個字元後會加入浮水印。若需正式產出，請註冊試用或商業授權。

## 往後步驟

既然你已掌握 **c# ocr 教學** 的基礎，接下來可以探索：

- **批次從圖像提取文字**（大量處理）
- 使用 **Aspose OCR** 偵測表格或結構化資料
- 將 OCR 結果整合至資料庫或 Web API
- 結合 OCR 與 **圖像前處理** 函式庫，如 `OpenCvSharp`

上述主題皆以你剛建立的基礎為出發點，讓你將原始掃描檔轉換為可搜尋、可操作的資料。

---

*準備好投入正式環境了嗎？從我的 GitHub 倉庫取得完整原始碼，為自己的文件調整 ROI，即可看到文字如魔法般顯示。*  

祝開發順利！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}