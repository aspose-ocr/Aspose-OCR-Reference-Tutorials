---
category: general
date: 2026-03-17
description: 學習如何在 C# 中執行 OCR，以提取阿拉伯文字、從圖像辨識文字，並透過完整程式碼範例將圖像轉換為文字。
draft: false
keywords:
- how to perform OCR
- extract arabic text
- recognize text from image
- convert image to text
- extract text from image
language: zh-hant
og_description: 如何在 C# 中執行 OCR？本指南將教你如何提取阿拉伯文、從圖像辨識文字，並在幾個步驟內將圖像轉換為文字。
og_title: 如何在 C# 中執行 OCR – 擷取阿拉伯文字
tags:
- OCR
- C#
- Arabic
- ImageProcessing
title: 如何在 C# 中執行光學字符辨識 – 從圖像中提取阿拉伯文字
url: /zh-hant/net/text-recognition/how-to-perform-ocr-in-c-extract-arabic-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中執行 OCR – 從圖像中擷取阿拉伯文文字

有沒有想過 **如何執行 OCR** 於阿拉伯語發票或掃描文件？你並不孤單——許多開發者在需要從位圖中抽取阿拉伯字元時會卡關。好消息是，只要幾行 C# 程式碼，就能辨識圖像檔案中的文字、將圖像轉換為文字，最終 **擷取阿拉伯文字** 供後續處理使用。

在本教學中，我們將逐步示範一個完整、可執行的範例，說明如何執行 OCR、每個步驟的意義，以及處理從右至左腳本時需要注意的事項。完成後，你將能夠 **從圖像中擷取文字**，支援阿拉伯語、烏爾都語、庫爾德語或任何 OCR 引擎支援的語言。

## 前置條件

- .NET 6.0 或更新版本（程式碼同樣可在 .NET Core 上編譯）  
- 參考提供 `OcrEngine` 的 OCR 函式庫（例如 `MyOcrSdk.dll`）。  
- 包含阿拉伯文字的圖像檔，例如 `invoice_arabic.png`。  
- 具備 C# 主控台應用程式的基本概念。

> **小技巧：** 若手邊沒有 OCR SDK，*MyOcrSdk* 的免費社群版即可用於測試，且支援本教學所使用的語言。

---

## Step 1 – Set Up the Project and Import the OCR Namespace

在 **從圖像中辨識文字** 之前，我們需要先建立專案骨架並加入正確的 `using` 指示。

```csharp
using System;
using MyOcrSdk;          // <-- Replace with the actual namespace of your OCR library
using MyOcrSdk.IO;       // For ImageStream helper class

namespace ArabicOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // The rest of the OCR workflow will go here
        }
    }
}
```

*為什麼這很重要：* 匯入正確的命名空間才能使用 `OcrEngine`、`Language` 與 `ImageStream`。若省略此步驟，編譯時會出現錯誤，對新手相當挫折。

---

## Step 2 – Create an OCR Engine Instance (Primary Keyword Included)

現在我們透過實例化引擎來真正 **執行 OCR**。

```csharp
// Step 2: Create an OCR engine instance
var ocrEngine = new OcrEngine();
```

`OcrEngine` 物件是整個流程的核心；它負責設定、執行繁重的辨識工作，並回傳包含擷取字串的結果物件。可以把它想像成會 **將圖像轉換為文字** 的「大腦」。

---

## Step 3 – Choose the Language for Recognition

阿拉伯語、烏爾都語、庫爾德語…皆屬同一文字系統，我們必須告訴引擎預期的語言，才能大幅提升辨識準確度。

```csharp
// Step 3: Choose the language for recognition (Arabic, Urdu, Kurdish, etc.)
ocrEngine.Config.Language = Language.Arabic;   // You can switch to Language.Urdu, etc.
```

*為什麼這很重要：* OCR 引擎依賴語言模型。選擇正確的模型可減少相似字元的誤辨，尤其是從右至左的腳本。

---

## Step 4 – Load the Image Containing the Text

我們需要一張位圖讓引擎分析。輔助類別 `ImageStream.FromFile` 會抽象化檔案 I/O 的細節。

```csharp
// Step 4: Load the image that contains the text to be recognized
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/invoice_arabic.png");
```

請確保路徑指向 **有效的圖像**。若檔案遺失或損毀，引擎會拋出例外，導致無法成功 **從圖像中擷取文字**。

---

## Step 5 – Run the OCR Process and Retrieve the Result

最後，我們呼叫 `Recognize()` 並顯示擷取出的字串。

```csharp
// Step 5: Perform the OCR operation
var ocrResult = ocrEngine.Recognize();

// Step 6: Display the extracted text
Console.WriteLine("=== Extracted Arabic Text ===");
Console.WriteLine(ocrResult.Text);
```

`ocrResult.Text` 屬性保存了引擎能讀取的純文字表示。大多數情況下，你會看到阿拉伯字元與數字的混合，這非常適合後續的資料庫寫入或翻譯等處理。

### 預期輸出

```
=== Extracted Arabic Text ===
فاتورة رقم: 12345
التاريخ: 2026/03/15
المبلغ: 2500.00 ريال
...
```

如果看到亂碼，請再次確認語言設定，並確保圖像解析度足夠（300 dpi 或以上為理想）。

---

## Full Working Example

以下是 **完整、獨立的程式**，可直接複製貼上到新的主控台專案並立即執行。

```csharp
// Full OCR demo – extracts Arabic text from an image
using System;
using MyOcrSdk;
using MyOcrSdk.IO;

namespace ArabicOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create the OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Set language – Arabic (change to Urdu or Kurdish if needed)
            ocrEngine.Config.Language = Language.Arabic;

            // 3️⃣ Load the source image
            // Replace YOUR_DIRECTORY with the folder that holds your PNG/JPG
            string imagePath = @"YOUR_DIRECTORY/invoice_arabic.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            try
            {
                // 4️⃣ Run OCR
                var result = ocrEngine.Recognize();

                // 5️⃣ Output the text
                Console.WriteLine("=== Extracted Arabic Text ===");
                Console.WriteLine(result.Text);
            }
            catch (Exception ex)
            {
                // Graceful error handling – useful when you need to **extract text from image** in batch jobs
                Console.Error.WriteLine($"OCR failed: {ex.Message}");
            }
        }
    }
}
```

> **注意：** 若你的 OCR SDK 需要授權，請在第 1 步之前先初始化授權（例如 `OcrEngine.SetLicense("YOUR_LICENSE_KEY");`）。此行為為簡潔起見已省略。

---

## Handling Common Edge Cases

| 情況 | 發生原因 | 快速解決方案 |
|-----------|----------------|-----------|
| **模糊或低解析度圖像** | OCR 準確率下降至 70 % 以下 | 以 300 dpi 掃描，或在送入引擎前使用雙三次演算法放大圖像。 |
| **混合語言（阿拉伯語 + 英文）** | 引擎可能在第一個語言區塊後停止 | 啟用多語言模式：`ocrEngine.Config.Language = Language.Arabic | Language.English;` |
| **從右至左顯示問題** | Console 以左至右印出字元，導致阿拉伯文顯示顛倒 | 使用 `Console.OutputEncoding = System.Text.Encoding.UTF8;` 並使用支援 RTL 脚本的終端機。 |
| **大型 PDF 分成多頁** | 記憶體使用激增 | 一次處理一頁：將每頁載入為單獨圖像並重複 OCR 流程。 |
| **特殊符號（貨幣、日期）** | 某些 OCR 模型會將其視為雜訊 | 使用正規表達式後處理 `ocrResult.Text` 以正規化已知模式。 |

---

## Extending the Solution – From OCR to Data Extraction

現在你 **已經會執行 OCR**，或許會想：*擷取到的阿拉伯文字可以怎麼用？* 以下是幾個自然衍生的應用想法：

1. **解析發票** – 使用正規表達式抽取發票號碼、日期與金額。  
2. **串接翻譯 API** – 將阿拉伯字串送至 Azure Translator 或 Google Cloud Translate。  
3. **寫入資料庫** – 把清理過的文字插入 SQL 表格，以供報表使用。  
4. **觸發工作流程** – 結合訊息佇列（例如 RabbitMQ）啟動後續處理。

所有這些情境皆以相同的核心操作為基礎：**將圖像轉換為文字**，然後對結果進行後續處理。

---

## Conclusion

我們已完整說明 **如何在 C# 中執行 OCR** 以 **擷取圖像中的阿拉伯文字**。從專案設定、實例化 `OcrEngine`、設定語言、載入位圖、執行辨識、印出結果，我們也討論了常見的陷阱，並示範如何將基本流程延伸至實務管線。

快試試看——更換圖像路徑、改用烏爾都語，或把輸出接到資料庫。只要能可靠 **從圖像中辨識文字** 並 **將圖像轉換為文字**，未來的可能性就無限。

---

### Related Topics You Might Want to Explore

- **使用 Tesseract OCR（開源替代方案）擷取圖像文字**  
- **大量 OCR 處理**：針對成千上萬的掃描 PDF 進行批次作業  
- **透過影像前處理提升 OCR 準確度**（二值化、除噪）  
- **在 .NET UI 框架（WPF、WinForms）中處理從右至左腳本**  

如果在實作過程中遇到任何問題，或想分享你如何將此模式套用到自己的專案，歡迎留言討論。祝開發順利！

![如何執行 OCR 範例](images/ocr_flow.png "how to perform OCR example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}