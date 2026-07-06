---
category: general
date: 2026-02-27
description: 如何在 C# 中啟用 OCR 以將 PDF 轉換為文字。了解如何使用 Aspose OCR 從多語言 PDF 中提取文字。
draft: false
keywords:
- how to enable ocr
- convert pdf to text
- how to extract text
- how to recognize pdf
- recognize pdf text c#
language: zh-hant
og_description: 如何在 C# 中啟用 OCR 並將 PDF 轉換為文字。逐步指南，使用 Aspose OCR 提取與辨識 PDF 文字。
og_title: 如何在 C# 中啟用 OCR – 將 PDF 轉換為文字
tags:
- OCR
- C#
- PDF
- Aspose
title: 如何在 C# 中啟用 OCR – 輕鬆將 PDF 轉換為文字
url: /zh-hant/net/ocr-configuration/how-to-enable-ocr-in-c-convert-pdf-to-text-easily/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中啟用 OCR – 輕鬆將 PDF 轉換為文字

如何在 C# 中啟用 OCR 是許多開發者在需要從 PDF 中提取文字時常問的問題。如果你曾經盯著掃描過的發票，心想 *「要怎麼在不重新打字的情況下抽取文字？」*，那麼你來對地方了。在本教學中，我們將一步步示範完整、可直接執行的解決方案，不僅說明 **如何啟用 OCR**，還示範 **如何將 PDF 轉換為文字**、**如何從多語言文件中抽取文字**，以及 **如何使用 C# 識別 PDF** 內容。

我們將使用 Aspose.OCR 函式庫，它內建支援數十種語言，讓你不必為英文、阿拉伯文、日文或其他文字腳本分別準備引擎。完成本指南後，你將擁有一個 **recognizes PDF text C#** 的單一方法，能將結果印到主控台，且可直接嵌入任何 .NET 專案。

## 前置條件 – 開始前需要的項目

- .NET 6.0 SDK 或更新版本（此程式碼同樣支援 .NET Core 與 .NET Framework）
- Visual Studio 2022（或任意你偏好的編輯器）
- **Aspose.OCR for .NET** 的授權或免費試用版 – 可從 Aspose 官方網站取得臨時金鑰
- 一個包含多種語言的範例 PDF（我們稱之為 `multilang.pdf`）

如果缺少上述任一項目，請從 Microsoft 官網下載 SDK，並安裝 NuGet 套件：

```bash
dotnet add package Aspose.OCR
```

設定完成。準備好了嗎？讓我們開始吧。

## 如何在 C# 中啟用 OCR – 設定與配置

首先要做的事就是建立 OCR 引擎的實例，並告訴它預期會使用哪些語言。這就是 **如何啟用 OCR** 的關鍵步驟，為後續流程提供基礎。

```csharp
using Aspose.OCR;
using System;

public class OcrDemo
{
    public static void Main()
    {
        // Step 1: Instantiate the OCR engine
        var ocrEngine = new OcrEngine();

        // Step 2: Enable the languages you need (English, Arabic, Japanese)
        ocrEngine.Language = OcrLanguage.English |
                             OcrLanguage.Arabic |
                             OcrLanguage.Japanese;

        // Step 3: Recognize text from the PDF file
        string recognizedText = ocrEngine.RecognizeFromFile("YOUR_DIRECTORY/multilang.pdf");

        // Step 4: Output the extracted text
        Console.WriteLine(recognizedText);
    }
}
```

**為什麼這很重要：** 透過明確設定 `Language` 屬性，你可指引引擎載入正確的字元模型，從而大幅提升準確度，尤其是混合腳本的 PDF。若省略此步驟（或保留預設值），引擎將自行猜測，往往會產生亂碼。

> **小技巧：** 若你的文件只包含單一語言，請將旗標限制於該語言，可提升最高 30 % 的處理速度。

### 圖片 – 啟用 OCR 的視覺概覽  
![Screenshot of OCR engine configuration showing how to enable OCR in C#](/images/enable-ocr-csharp.png)

*Alt text: 使用 Aspose.OCR 在 C# 中啟用 OCR 的示意圖。*

## 使用 Aspose OCR 將 PDF 轉換為文字

現在 **如何啟用 OCR** 已完成，接下來談談實際的轉換。`RecognizeFromFile` 方法負責大部分工作：它會開啟 PDF、對每一頁執行 OCR，最後回傳包含所有抽取字元的單一字串。

### 背後的運作流程？

1. **頁面光柵化** – 每一頁 PDF 會被轉成位圖，因為 OCR 只能處理影像。
2. **語言模型選擇** – 依據先前設定的旗標，引擎挑選對應的神經網路。
3. **文字行偵測** – 引擎找出文字行，即使文字有傾斜也能偵測。
4. **字元解碼** – 最後將像素圖樣映射為 Unicode 字元。

由於此方法回傳純文字字串，你只需要一行程式碼即可 **convert PDF to text**。若需要更細緻的控制（例如逐頁處理），可在迴圈中呼叫 `RecognizeFromStream`。

## 如何從多語言 PDF 中抽取文字

假設你的 PDF 包含英文標題、阿拉伯文正文與日文註腳。前面示範的程式碼已能處理此情境，但你可能想知道 **如何只抽取特定語言的文字**。

只要使用簡單的字串操作或正規表達式即可過濾結果。以下範例示範如何只取出英文部分：

```csharp
using System.Text.RegularExpressions;

// After recognizing the whole document...
string allText = ocrEngine.RecognizeFromFile("YOUR_DIRECTORY/multilang.pdf");

// Regex to keep only ASCII characters (roughly English)
string englishOnly = Regex.Replace(allText, @"[^\u0000-\u007F]+", string.Empty);

Console.WriteLine("English extracted:");
Console.WriteLine(englishOnly);
```

**為什麼要過濾？** 在許多商業工作流程中，只需要拉丁文字段落作為索引，其他語言則另行保存。此模式展示了 **how to extract text** 的高效做法，且不需再次執行 OCR。

## 如何識別 PDF – 處理邊緣案例

即使是最好的 OCR 引擎，也會在某些 PDF 上卡關。以下列出常見問題與解決方式：

| 問題 | 症狀 | 解決方案 |
|------|------|----------|
| 低解析度掃描 (<150 dpi) | 缺字、文字亂碼 | 使用 `ocrEngine.ImageProcessingOptions.Dpi = 300;` 先行前處理 PDF |
| 頁面旋轉 | 文字呈側向 | 設定 `ocrEngine.PageSegmentationMode = PageSegmentationMode.AutoRotate;` |
| 受密碼保護的 PDF | `RecognizeFromFile` 拋出例外 | 傳入密碼：`ocrEngine.RecognizeFromFile(path, "myPassword");` |
| 超大型檔案 (>100 頁) | 記憶體不足導致當機 | 分批處理：一次載入 10 頁並串接結果 |

加入上述調整後，你的解決方案即可 **recognizes PDF** 內容，無論檔案有何怪癖，都能穩定運作。

```csharp
// Example of handling low‑resolution and rotation
ocrEngine.ImageProcessingOptions.Dpi = 300;
ocrEngine.PageSegmentationMode = PageSegmentationMode.AutoRotate;
```

## Recognize PDF Text C# – 完整可執行範例

將所有步驟整合，以下是一個可直接貼到 Console 應用程式的完整程式碼。它示範了 **how to enable OCR**、**convert PDF to text**、**extract specific language portions**，以及 **handle common edge cases**。

```csharp
using Aspose.OCR;
using System;
using System.Text.RegularExpressions;

namespace PdfOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create OCR engine instance
            var ocrEngine = new OcrEngine();

            // 2️⃣ Enable languages (English, Arabic, Japanese)
            ocrEngine.Language = OcrLanguage.English |
                                 OcrLanguage.Arabic |
                                 OcrLanguage.Japanese;

            // Optional: improve accuracy for low‑res PDFs
            ocrEngine.ImageProcessingOptions.Dpi = 300;
            ocrEngine.PageSegmentationMode = PageSegmentationMode.AutoRotate;

            // 3️⃣ Path to your multi‑language PDF
            string pdfPath = @"C:\Docs\multilang.pdf";

            // 4️⃣ Recognize all text
            string fullText = ocrEngine.RecognizeFromFile(pdfPath);
            Console.WriteLine("=== Full extracted text ===");
            Console.WriteLine(fullText);
            Console.WriteLine();

            // 5️⃣ Extract only English (as an example of how to extract text)
            string englishOnly = Regex.Replace(fullText, @"[^\u0000-\u007F]+", string.Empty);
            Console.WriteLine("=== English‑only excerpt ===");
            Console.WriteLine(englishOnly);
        }
    }
}
```

**預期輸出**（為簡潔起見已截斷）：

```
=== Full extracted text ===
Welcome to our report…
مرحبا بكم في تقريرنا…
ようこそ、私たちのレポートへ…

=== English‑only excerpt ===
Welcome to our report...
```

執行程式，指向你的 PDF，即可在主控台看到完整的多語言文字與過濾後的英文片段。

## 常見問題（快速解答）

- **這能在 .NET Framework 4.7 上運行嗎？**  
  可以。Aspose.OCR 的 NuGet 套件目標為 .NET Standard 2.0，兼容 .NET Core 與 .NET Framework。

- **如果我要 OCR 圖片而不是 PDF，該怎麼做？**  
  使用 `ocrEngine.RecognizeFromImage("image.png")`。語言旗標仍然適用，仍然是 **how to enable OCR** 的一步。

- **我可以把輸出寫入 .txt 檔嗎？**  
  完全可以。將 `Console.WriteLine(fullText);` 改為 `File.WriteAllText("output.txt", fullText);` 即可。

- **有辦法取得信心分數嗎？**  
  Aspose.OCR 會回傳 `OcrResult` 物件，你可以從中讀取每個單字的 `Confidence`。請參考 API 文件 `RecognizeFromFile(..., out OcrResult result)`。

## 結論

我們已說明 **how to enable OCR** 在 C# 中的做法，展示了 **convert PDF to text**、**how to extract text** 從特定語言段落，以及 **how to recognize PDF** 的可靠實作。上方完整、可執行的程式碼為你提供了將 OCR 整合至任何 .NET 應用的堅實基礎——無論是文件管理系統、自動化發票處理器，或是多語言搜尋索引。

接下來的步驟？嘗試加入中文或韓文的語言旗標、實驗 `ImageProcessingOptions` 以處理噪點掃描，或將抽取的文字導入自然語言處理管線。所有這些延伸都仍然依賴同一核心概念：在一開始正確 **how to enable OCR**。

祝開發順利，願你的 PDF 永遠可搜尋！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}