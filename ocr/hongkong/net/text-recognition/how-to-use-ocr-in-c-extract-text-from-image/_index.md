---
category: general
date: 2026-03-05
description: 如何在 C# 中使用 OCR 從圖像中提取文字。學習將圖像轉換為文字、讀取韓文字符，並快速載入圖像進行 OCR。
draft: false
keywords:
- how to use OCR
- extract text from image
- convert image to text
- read korean characters
- load image for OCR
language: zh-hant
og_description: 如何在 C# 中使用 OCR 並即時從圖像提取文字。本指南展示如何將圖像轉換為文字、讀取韓文字符以及載入圖像以進行 OCR。
og_title: 如何在 C# 中使用 OCR – 從圖片提取文字
tags:
- OCR
- C#
- Aspose
title: 如何在 C# 中使用 OCR – 從圖像提取文字
url: /zh-hant/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 OCR – 從圖像提取文字

有沒有想過在截圖中充滿韓文且需要取得純文字時，**如何使用 OCR**？你並不是唯一為此抓狂的人。在本教學中，我們將逐步示範一個完整、可直接執行的範例，能**從圖像提取文字**、**將圖像轉換為文字**，甚至示範如何使用 Aspose.OCR **讀取韓文字元**。

我們也會說明常被忽略的 **loading image for OCR** 步驟，避免之後出現「找不到檔案」的錯誤。完成後，你將擁有一個可直接放入任何 .NET 專案的獨立程式。

## 需求條件

- .NET 6+（或 .NET Framework 4.7.2 及以上）– 程式碼兩者皆可執行。
- Aspose.OCR for .NET – 可從 Aspose 官方網站取得免費試用版。
- 一張包含韓文的範例圖像 (`korean_doc.png`)。
- 你喜愛的 IDE（Visual Studio、Rider、VS Code – 隨你喜好）。

不需要其他第三方函式庫。

## 步驟 1：設定專案並加入 Aspose.OCR

First, create a new console app:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

Then add the Aspose.OCR NuGet package:

```bash
dotnet add package Aspose.OCR
```

> **小技巧：** 若你有授權檔案，請將其放在專案根目錄；否則免費試用版仍可使用，但會在輸出結果上加上浮水印。

## 步驟 2：如何使用 OCR – 初始化引擎

現在我們開始撰寫 C# 程式碼。當 **how to use OCR** 時，第一件事就是實例化 `OcrEngine`。此物件是函式庫的核心，負責保存之後會用到的所有設定。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // Optional: apply your license to remove trial limitations
            // Replace the path with the actual location of your .lic file
            ocrEngine.SetLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

**為什麼這很重要：** 若沒有正確的引擎實例，就無法設定語言、載入圖像或取得結果。引擎同時管理內部資源，僅建立一次並重複使用比不斷重新建構物件更有效率。

## 步驟 3：選擇語言 – 讀取韓文字元

下一行告訴引擎要辨識哪種語言。因為我們的目標是 **read Korean characters**，所以設定 `OcrLanguage.Korean`。根據需求，你也可以改成阿拉伯語、泰語、古吉拉特語等。

```csharp
            // Step 3: Tell the engine which language to recognize
            ocrEngine.Language = OcrLanguage.Korean; // alternatives: Arabic, Thai, Gujarati, etc.
```

**為什麼重要：** 語言選擇能大幅提升準確度。OCR 引擎會使用特定語言的字典與字元模型；若提供錯誤的語言，輸出可能會變成亂碼。

## 步驟 4：載入圖像以供 OCR – 將圖像轉換為文字

在引擎執行任何工作之前，需要 **load image for OCR**。`ImageStream.FromFile` 方法會將檔案讀取成引擎可理解的格式。

```csharp
            // Step 4: Load the image that contains the text
            ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/korean_doc.png");
```

若圖像位於其他資料夾，只需調整路徑。記得將檔案的 *Build Action* 設為「Copy if newer」，讓執行檔在執行時能找到它。

> **常見陷阱：** 在字串常值中直接使用反斜線 (`\`) 而未進行跳脫，會導致編譯錯誤。請使用雙反斜線 (`\\`) 或逐字字串 (`@"C:\path\file.png"`)。

## 步驟 5：執行 OCR – 從圖像提取文字

現在開始進行繁重的運算。呼叫 `Recognize()` 會執行 OCR 演算法，而 `Text` 屬性則會回傳原始字串。

```csharp
            // Step 5: Run OCR and get the recognized text
            string recognizedText = ocrEngine.Recognize().Text;
```

此時你已 **extracted text from image**，也等同於 **converted image to text**。若原始版面有換行，結果中可能會包含換行字元。

## 步驟 6：顯示結果 – 驗證輸出

最後，將結果印到主控台，以便驗證是否成功。

```csharp
            // Step 6: Output the result to the console
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(recognizedText);
        }
    }
}
```

Run the program:

```bash
dotnet run
```

### 預期輸出

```
=== Recognized Text ===
안녕하세요. 이것은 OCR 테스트 문서입니다.
```

如果看到與圖像相似的韓文字元，恭喜你——已掌握 **how to use OCR** 與 Aspose.OCR！

![如何使用 OCR 範例圖示](image.png)

*圖片說明：如何使用 OCR 範例圖示，展示從載入圖像到印出辨識文字的流程。*

## 邊緣案例與變化

### 1. 處理多頁

如果需要 **extract text from image** 檔案包含多頁（例如 multi‑page TIFF），可對每一頁迴圈，對每個 `ImageStream` 實例呼叫 `Recognize()`。

### 2. 處理低品質掃描

低解析度圖像會影響準確度。在呼叫 `Recognize()` 前，可使用 Aspose 的前處理工具改善圖像：

```csharp
ocrEngine.Image = ImageProcessing.Preprocess(ocrEngine.Image, ImageProcessingOptions.Deskew);
```

### 3. 動態切換語言

假設文件包含多種語言。可在辨識之間變更 `ocrEngine.Language`：

```csharp
ocrEngine.Language = OcrLanguage.English;
string english = ocrEngine.Recognize().Text;

ocrEngine.Language = OcrLanguage.Korean;
string korean = ocrEngine.Recognize().Text;
```

### 4. 將結果儲存至檔案

如果想 **convert image to text** 並儲存，只需將字串寫入 `.txt` 檔案：

```csharp
System.IO.File.WriteAllText("output.txt", recognizedText);
```

## 常見問題

- **執行此程式碼是否需要授權？**  
  不需要。免費試用版可供實驗使用，但會在輸出上加上浮水印。購買授權後可移除浮水印並解鎖完整效能。

- **可以在 Linux 上使用嗎？**  
  當然可以。Aspose.OCR 為跨平台套件，只要確保安裝必要的原生相依性（Linux 上 .NET Core 需要 libgdiplus）。

- **如果我的圖像是以串流而非檔案形式提供呢？**  
  使用 `ImageStream.FromStream(yourStream)` —— API 接受任何 `System.IO.Stream`。

## 結論

我們已一步步說明在 C# 中 **how to use OCR**，以 **extract text from image**、**convert image to text**，並 **read Korean characters**，同時正確 **loading image for OCR**。上述完整可執行的範例應可直接使用，額外的技巧則提供更進階情境的指引。

準備好接受下一個挑戰了嗎？試著換成其他語言、逐頁處理 PDF，或將 OCR 呼叫整合到 Web API，讓使用者上傳圖片即時取得文字結果。可能性無窮，而你現在已具備堅實的基礎。

祝程式開發愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}