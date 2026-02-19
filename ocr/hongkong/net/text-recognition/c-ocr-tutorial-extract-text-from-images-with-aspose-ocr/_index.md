---
category: general
date: 2026-02-19
description: C# OCR 教學 – 教你如何從圖片中提取文字、讀取圖片文字、將圖片轉換為文字，並在數分鐘內使用 Aspose.OCR 識別圖片文字。
draft: false
keywords:
- c# ocr tutorial
- extract text from image
- read image text
- convert image to text
- recognize image text
language: zh-hant
og_description: C# OCR 教學示範如何從圖片中提取文字、讀取圖片文字、將圖片轉換為文字，並使用 Aspose OCR 識別圖片文字。
og_title: C# OCR 教學 – 使用 Aspose OCR 從圖像提取文字
tags:
- OCR
- C#
- Aspose
title: C# OCR 教學：使用 Aspose OCR 從圖像提取文字
url: /zh-hant/net/text-recognition/c-ocr-tutorial-extract-text-from-images-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – 從圖片中擷取文字 (Aspose OCR)

有沒有想過在純 C# 環境下 **從圖像檔案中擷取文字**？這正是這篇 **c# ocr tutorial** 要解決的問題。只要幾個步驟，你就能學會讀取圖片文字、將圖片轉換成文字，甚至辨識不同語言的圖片文字，全部使用 Aspose.OCR 函式庫。

在本指南中，我們會一步步說明：從安裝 NuGet 套件、處理授權、設定語言，到印出結果。完成後，你將擁有一個可直接執行的 console 應用程式，能把任何圖片（例如掃描的發票或螢幕截圖）轉成可搜尋的文字。

## 需要的環境

- .NET 6.0 SDK 或更新版本（程式碼同樣支援 .NET Framework 4.7+）  
- Visual Studio 2022（或任何你慣用的編輯器）  
- Aspose.OCR 授權檔 *可選* – 函式庫在評估模式下也能運作，但授權會移除浮水印。  
- 一張範例圖片（例如 `cyrillic_sample.jpg`），放在磁碟任意位置。

除此之外不需要其他第三方工具；Aspose.OCR 會在底層處理所有繁重工作。

---

![c# ocr tutorial 範例圖片，顯示西里爾文字](/images/ocr-sample.jpg "c# ocr tutorial – OCR 範例圖片")

## c# ocr tutorial – 設定 Aspose OCR

首先，將 Aspose.OCR 套件加入你的專案：

```bash
dotnet add package Aspose.OCR
```

> **小技巧：** 若使用 Visual Studio，也可以右鍵點擊專案 → **Manage NuGet Packages**，搜尋 *Aspose.OCR*。

### 為什麼授權很重要

Aspose.OCR 在未授權的情況下會以 30 天評估模式執行。`License` 類別只需要指向你的 `.lic` 檔案；設定完成後，引擎就不會在輸出中插入評估頁腳。

```csharp
// Optional: apply your Aspose.OCR license to unlock full features
// new License().SetLicense("Aspose.OCR.lic");
```

如果在開發期間省略這行程式碼，OCR 仍會正常運作，只是擷取的文字裡會出現評估提示。

## 從圖片擷取文字 – 建立 OCR 引擎

任何 **c# ocr tutorial** 的核心都是 `OcrEngine` 物件。它抽象化了整個辨識流程。

```csharp
using Aspose.OCR;
using System;

class Program
{
    static void Main()
    {
        // Step 1: (Optional) Apply your license – see above
        // new License().SetLicense("Aspose.OCR.lic");

        // Step 2: Instantiate the OCR engine
        var ocrEngine = new OcrEngine();

        // Step 3: Choose the language you want to recognize
        // For this demo we use Cyrillic, but you can pick English, Arabic, etc.
        ocrEngine.Language = Language.Cyrillic;

        // Step 4: Run OCR on the target picture
        var result = ocrEngine.RecognizeImage(@"YOUR_DIRECTORY/cyrillic_sample.jpg");

        // Step 5: Output the recognized text to the console
        Console.WriteLine("Recognized text:");
        Console.WriteLine(result.Text);
    }
}
```

### 程式碼實際在做什麼

- **實例化 `OcrEngine`** 會建立一個全新的處理上下文。  
- **設定 `Language`** 告訴 Aspose 期待的字元集；這會大幅提升準確度，因為引擎可以套用語言特定的啟發式演算法。  
- **`RecognizeImage`** 會載入檔案，執行一系列影像前處理（去斜、二值化、除噪），最後交給神經網路辨識器。  
- **`result.Text`** 保存純文字表示——非常適合 **convert image to text** 的情境。

## 讀取圖片文字 – 處理不同檔案類型

Aspose.OCR 不只支援 JPEG，還支援 PNG、BMP、TIFF，甚至 PDF 頁面（作為影像）。如果需要批次處理，只要把呼叫包在簡單的迴圈中：

```csharp
string[] files = Directory.GetFiles(@"YOUR_DIRECTORY", "*.*", SearchOption.TopDirectoryOnly)
                          .Where(f => f.EndsWith(".jpg") || f.EndsWith(".png") || f.EndsWith(".tif"))
                          .ToArray();

foreach (var file in files)
{
    var res = ocrEngine.RecognizeImage(file);
    Console.WriteLine($"--- {Path.GetFileName(file)} ---");
    Console.WriteLine(res.Text);
}
```

### 邊緣情況：空白或損毀的圖片

如果 `RecognizeImage` 收到 null 或無法讀取的檔案，會拋出 `ArgumentException`。加入快速防護讓你的 **c# ocr tutorial** 更加穩健：

```csharp
if (!File.Exists(file))
{
    Console.WriteLine($"File not found: {file}");
    continue;
}
```

## 辨識圖片文字 – 微調以提升準確度

有時預設設定會遺漏少數字元，特別是低對比度的掃描件。Aspose.OCR 提供了幾個可調整的參數：

| 屬性 | 功能說明 | 常見使用情境 |
|------|----------|--------------|
| `ocrEngine.PreprocessingOptions.Deskew` | 旋轉影像以校正傾斜 | 掃描文件 |
| `ocrEngine.PreprocessingOptions.NoiseRemoval` | 去除斑點噪聲 | 老照片 |
| `ocrEngine.Language` | 語言模型（西里爾文、英文等） | 多語言 OCR |

啟用去斜的範例：

```csharp
ocrEngine.PreprocessingOptions.Deskew = true;
```

這些調整可協助你 **extract text from image** 的檔案即使未完全對齊，也能提升 **read image text** 的成功率。

## 預期輸出

將範例程式對 `cyrillic_sample.jpg`（內含「Привет мир」）執行，會得到類似以下結果：

```
Recognized text:
Привет мир
```

如果處於評估模式，還會看到最後一行：

```
--- Evaluation version. Use a licensed copy for production. ---
```

提供有效授權檔後，該行即會消失。

---

## 常見問題與避免方式

1. **語言設定錯誤** – 在西里爾文字上使用 `Language.English` 會得到亂碼。務必依來源文字匹配語言。  
2. **大型圖片** – 處理 10 MP 照片可能較慢。如對速度有需求，可先縮小圖片 (`Bitmap.Resize`) 再辨識。  
3. **缺少相依檔案** – Aspose.OCR 內含原生二進位檔，請確保輸出資料夾內有 `Aspose.OCR.Native.dll`（NuGet 會自動處理，但自訂建置流程可能需要手動複製）。

## 往後的方向 – 超越基礎應用

- **批次轉換**：將前述迴圈結合非同步 `Task.Run`，加速大量資料夾的處理。  
- **匯出為 PDF**：在 **convert image to text** 後，將字串傳給 PDF 產生器（如 Aspose.PDF）以建立可搜尋的 PDF。  
- **整合 Azure Functions**：將 OCR 邏輯封裝成無伺服器端點，即時處理上傳的檔案。

所有這些延伸都圍繞 **extract text from image** 與 **read image text** 的實務應用。

---

## 結論

你已完成一個 **c# ocr tutorial**，示範如何使用 Aspose.OCR 讀取圖片文字、將圖片轉換成文字，以及辨識圖片文字。上述完整可執行的範例涵蓋了從授權、語言選擇到錯誤處理的每一步，讓你可以直接把程式碼放入任何 .NET 專案，即刻開始擷取文字。

歡迎嘗試不同語言、微調前處理選項，或將輸出接入資料庫以建立可搜尋的檔案庫。若遇到問題，Aspose 官方文件是很好的參考，而本篇程式碼在大多數情境下應該能即時運作。

祝開發順利，願你的圖片永遠可讀！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}