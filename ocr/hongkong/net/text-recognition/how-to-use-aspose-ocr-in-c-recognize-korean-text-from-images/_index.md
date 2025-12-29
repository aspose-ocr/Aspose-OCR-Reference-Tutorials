---
category: general
date: 2025-12-29
description: 如何使用 Aspose OCR 轉換圖像文字並提取韓文文字。逐步指南，於 C# 中提取圖像文字並辨識韓文。
draft: false
keywords:
- how to use aspose
- convert image text
- extract text image
- extract korean text
- recognize korean text
language: zh-hant
og_description: 學習如何使用 Aspose OCR 轉換圖像文字、提取韓文文字，並透過完整的 C# 範例從圖片中辨識韓文文字。
og_title: 如何使用 Aspose OCR – 在 C# 中識別韓文文字
tags:
- Aspose
- OCR
- C#
- Image Processing
title: 如何在 C# 中使用 Aspose OCR – 從圖片辨識韓文文字
url: /zh-hant/net/text-recognition/how-to-use-aspose-ocr-in-c-recognize-korean-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 Aspose OCR – 從圖像辨識韓文文字

有沒有想過 **如何使用 Aspose** 從照片中提取韓文字符？也許你有街道標誌的螢幕截圖、掃描的收據，或是需要轉換成可搜尋文字的 meme。好消息是 Aspose OCR 讓這件事變得輕而易舉，你不必與低階的影像處理技巧糾纏。

在本教學中，我們將逐步說明一個 **完整、可執行的範例**，展示如何使用 Aspose OCR 函式庫 **convert image text**、**extract text image**，以及特別 **extract Korean text**。完成後，你將擁有一個在主控台輸出辨識出韓文字串的應用程式，並了解每一行程式碼的意義。

## 需要的環境

- **.NET 6+**（任何近期的 .NET SDK 都可使用 – Visual Studio、Rider，或 `dotnet` CLI）
- **Aspose.OCR for .NET** NuGet 套件  
  ```bash
  dotnet add package Aspose.OCR
  ```
- 包含韓文字元的圖像檔（例如 `korean_sign.jpg`）。
- 一點 C# 基礎知識 – 若你已寫過「Hello World」程式，即可開始。

> **小技巧：** Aspose OCR 內建支援超過 50 種語言。我們將重點放在韓文，因為其 Hangul 文字常讓一般 OCR 引擎卡關。

## 步驟 1 – 安裝並參考 Aspose OCR

首先，將函式庫加入你的專案。上方的 NuGet 指令已完成大部分工作，但若你偏好使用 UI，只要在 NuGet 套件管理員中搜尋 *Aspose.OCR* 即可。

```csharp
// No code needed here – the package reference is enough.
// The using directives below will bring the types into scope.
using Aspose.OCR;
using Aspose.OCR.Models;
```

> **為什麼重要：** `using` 陳述式讓你可以使用 `OcrEngine`、`Language` 以及 `Image` 輔助類別。若缺少它們，編譯器會因未知類型而報錯。

## 步驟 2 – 載入要處理的圖像

Aspose OCR 使用自有的 `Image` 包裝類別，可讀取 JPEG、PNG、BMP 以及其他多種格式。將它指向包含韓文文字的檔案即可。

```csharp
// Step 2: Load the image containing Korean characters
var imagePath = Path.Combine(Environment.CurrentDirectory, "korean_sign.jpg");
var image = Image.Load(imagePath);
```

如果檔案不在可執行檔同一資料夾，請相應調整路徑。`Image.Load` 呼叫會 **convert image text** 成 OCR 引擎可理解的內部表示。

![how to use aspose OCR example](/images/aspose-ocr-korean.png "how to use aspose OCR to recognize Korean text")

*圖片說明文字： “how to use aspose OCR example showing a Korean street sign.”*

## 步驟 3 – 為韓文設定 OCR 引擎

引擎必須知道要辨識哪種語言；否則會預設為英文，導致無法辨識 Hangul 字元。

```csharp
// Step 3: Create and configure the OCR engine
var ocrEngine = new OcrEngine
{
    // Tell Aspose we want to recognize Korean (Hangul)
    Language = Language.Korean
};
```

> **為什麼重要：** 設定 `Language = Language.Korean` 讓引擎載入韓文語言套件，顯著提升 Hangul 字形的辨識精度。若省略此步驟，常會得到亂碼輸出。

## 步驟 4 – 執行辨識程序

現在我們真正請求 Aspose 讀取圖像。`Recognize` 方法會回傳一個 `OcrResult` 物件，內含擷取的字串與信心分數。

```csharp
// Step 4: Run OCR on the loaded image
OcrResult ocrResult = ocrEngine.Recognize(image);
```

如果需要從較大的照片（例如包含多個 UI 元素的螢幕截圖）**extract text image**，可以先使用 `image.Crop(...)` 裁切感興趣的區域，再呼叫 `Recognize`。當你只關注圖片的特定部分時，這個技巧非常實用。

## 步驟 5 – 輸出辨識出的韓文文字

最後，顯示結果。在實務應用中，你可能會將其存入資料庫或傳送至翻譯 API，但在本教學中，使用主控台輸出即可保持簡潔。

```csharp
// Step 5: Print the recognized Korean text
Console.WriteLine("Recognized Korean text:");
Console.WriteLine(ocrResult.Text);
```

### 預期輸出

```
Recognized Korean text:
서울특별시 강남구 테헤란로 123
```

當然，你實際的輸出會反映 `korean_sign.jpg` 中的韓文字元。

## 完整範例程式

以下是 **完整程式**，可直接複製貼上至新的主控台專案（`dotnet new console`）。請確保圖像檔與編譯後的 `.exe` 同目錄，或自行調整路徑。

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // 1️⃣ Install Aspose.OCR via NuGet before running this code.

        // 2️⃣ Load the image that contains Korean text.
        var imagePath = Path.Combine(Environment.CurrentDirectory, "korean_sign.jpg");
        var image = Image.Load(imagePath);

        // 3️⃣ Create the OCR engine and set it to recognize Korean.
        var ocrEngine = new OcrEngine
        {
            Language = Language.Korean   // 👈 This enables Hangul support.
        };

        // 4️⃣ Run the OCR process.
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // 5️⃣ Output the extracted Korean string.
        Console.WriteLine("Recognized Korean text:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

使用 `dotnet run` 執行程式，即可在主控台看到韓文字元顯示。

## 常見問題與邊緣情況

### 如果 OCR 回傳亂碼該怎麼辦？

- **檢查語言設定。** 忘記設定 `Language.Korean` 是最常見的錯誤。
- **提升影像品質。** 更清晰的圖像、更高 DPI 與適當光線可提升辨識精度。
- **前置處理影像。** Aspose OCR 提供內建濾鏡（`image.Binarize()`、`image.Deskew()`）可清理噪點掃描。

### 我可以批次 **convert image text** 嗎？

當然可以。將上述步驟包在 `foreach` 迴圈中，遍歷資料夾內的圖像。以下是一段快速範例：

```csharp
foreach (var file in Directory.GetFiles(@"C:\KoreanImages", "*.jpg"))
{
    var img = Image.Load(file);
    var result = ocrEngine.Recognize(img);
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), result.Text);
}
```

此腳本會 **extract text image** 每個檔案，並在同目錄產生相對應的 `.txt` 檔案。

### 如何處理同一圖像中的多語言？

若將 `Language = Language.Auto`，Aspose OCR 可自動偵測語言。但自動偵測可能較慢且精度略低於明確指定語言。若已知圖像同時包含韓文與英文，可分兩次辨識——先以 `Language.Korean`，再以 `Language.English`，最後將結果串接。

## 生產環境 OCR 的建議

- **快取 OcrEngine。** 為每個請求建立新引擎會增加開銷。若大量處理圖像，請使用單例。
- **限制圖像尺寸。** 大圖會佔用記憶體；在送入引擎前將寬度縮小至約 1500 px。
- **處理例外狀況。** 將 `Recognize` 呼叫包在 try/catch 中，以優雅地處理損壞的檔案。

## 結論

我們剛剛說明了 **如何使用 Aspose** 來 **convert image text**、**extract text image**，以及特別 **extract Korean text**，只需幾行 C# 程式碼。步驟相當簡單：

1. 安裝 Aspose OCR。  
2. 載入圖像。  
3. 為韓文設定引擎。  
4. 執行 `Recognize`。  
5. 輸出結果。

現在你可以將此程式碼片段嵌入更大的工作流程——批次處理、文件歸檔，甚至即時翻譯應用。想更進一步？可嘗試加入 Aspose 的 `Image.Preprocess()` 方法、測試不同語言，或將輸出與 Azure Cognitive Services 結合進行翻譯。

對 **recognize Korean text** 或其他 Aspose 功能有更多疑問嗎？歡迎留言，祝編程愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}