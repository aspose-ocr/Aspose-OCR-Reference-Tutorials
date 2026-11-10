---
category: general
date: 2026-01-15
description: 學習如何使用 Aspose OCR 進行阿拉伯文文字的 OCR 以及印地文文字的識別。此逐步指南向您展示如何有效地從圖像中提取文字並將圖像轉換為文字。
draft: false
keywords:
- how to ocr arabic
- recognize arabic text
- extract text from image
- convert image to text
- recognize hindi text
language: zh-hant
og_description: 如何在單一 C# 程式中 OCR 阿拉伯文字並辨識印地文字。請參考本完整指南，從圖像中擷取文字並將圖像轉換為文字。
og_title: 如何使用 Aspose OCR 進行阿拉伯文與印地文文字辨識
tags:
- Aspose OCR
- C#
- Multilingual OCR
title: 如何使用 Aspose OCR 進行阿拉伯文與印地文文字的 OCR
url: /zh-hant/net/text-recognition/how-to-ocr-arabic-and-hindi-text-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose OCR 進行阿拉伯文與印地文文字辨識

有沒有想過 **如何 OCR 阿拉伯文**（從右至左書寫）同時從收據中擷取印地文字符？你並不孤單。許多開發者在同一工作流程中需要 **辨識阿拉伯文字** 與 **辨識印地文字** 時，常會碰到相同的問題。  

在本教學中，我們將逐步示範一個完整、可執行的 C# 範例，說明如何 **extract text from image** 檔案、**convert image to text**，以及如何使用 Aspose OCR 同時處理阿拉伯文與印地文腳本。沒有模糊的參考——只提供可直接 copy‑paste 的程式碼，並說明每一行的原理。

> **Pro tip:** 如果你從未使用過 Aspose OCR，請先安裝 NuGet 套件 `Aspose.OCR`。在 Visual Studio 中只需點一下即可完成，且會自動下載所有 CPU 辨識所需的原生二進位檔。

---

![how to ocr arabic example](/images/arabic-ocr-sample.png "how to ocr arabic – sample Arabic sign")

*Image alt text:* **how to ocr arabic – sample Arabic sign**  

---

## how to ocr arabic – 環境設定

在開始撰寫程式碼之前，先確保開發環境已就緒。

1. **Target framework** – .NET 6.0 或更新版本。較舊的版本仍能編譯，但會錯過最新的語言功能。  
2. **Package** – 在終端機執行 `dotnet add package Aspose.OCR`，或使用 NuGet 套件管理員 UI。  
3. **Images** – 將兩張範例圖片放在可參照的資料夾，例如 `C:\OCRSamples\arabic_sign.jpg` 與 `C:\OCRSamples\hindi_receipt.png`。阿拉伯文圖片應包含清晰、高對比度的阿拉伯字元；印地文圖片可以是掃描的收據或招牌照片。  

就這樣——不需要額外的設定檔、GPU 驅動，只要一個直接的 CPU‑based OCR 引擎即可。

---

## Recognize Arabic Text – 載入與處理

現在我們實際 **recognize arabic text**。關鍵是告訴引擎預期的語言，否則引擎會預設為拉丁字元，導致輸出雜亂。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

class MultiLangDemo
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine (CPU‑based by default)
        var ocrEngine = new OcrEngine();

        // 2️⃣ Load an image that contains Arabic script
        var arabicImage = OcrImage.FromFile(@"C:\OCRSamples\arabic_sign.jpg");

        // 3️⃣ Recognize the Arabic text – note the Language.Arabic enum
        var arabicResult = ocrEngine.Recognize(arabicImage, Language.Arabic);

        // 4️⃣ Print the result to the console
        System.Console.WriteLine("Arabic: " + arabicResult.Text);
```

**Why this works:**  
* `OcrEngine` 處理所有繁重的工作——前置處理、分割與字元分類。  
* 透過傳入 `Language.Arabic`，我們啟用右至左版面配置引擎與阿拉伯字元集。若不這樣做，引擎會把影像視為左至右的拉丁文字，導致缺少變音符號與斷裂的單詞。  

**Expected output**（實際文字會依圖片而異）：

```
Arabic: مرحبا بكم في متجرنا
```

如果看到空字串，請再次確認影像不是太暗且檔案路徑正確。  

---

## extract text from image – 處理右至左腳本

阿拉伯文並非唯一需要特殊處理的腳本。右至左（RTL）語言在辨識後必須將視覺順序反轉。當你指定 `Language.Arabic` 時，Aspose 會自動完成此步驟，但在未來擴充（例如希伯來文）時仍值得留意。

*Tip:* 當你在 UI 中顯示 OCR 結果時，請確保控制項支援 RTL 呈現；否則文字會顯示為亂碼。

---

## convert image to text – 處理印地文

換個方向，讓我們 **convert image to text** 以辨識印地文收據。流程與阿拉伯文相同，只是改用 `Language.Hindi`。

```csharp
        // 5️⃣ Load the Hindi (Devanagari) image
        var hindiImage = OcrImage.FromFile(@"C:\OCRSamples\hindi_receipt.png");

        // 6️⃣ Recognize Hindi text – Language.Hindi tells the engine to use Devanagari models
        var hindiResult = ocrEngine.Recognize(hindiImage, Language.Hindi);

        // 7️⃣ Output the Hindi OCR result
        System.Console.WriteLine("Hindi: " + hindiResult.Text);
    }
}
```

**Why we reuse the same `ocrEngine` instance:**  
為每種語言建立新引擎會浪費記憶體與初始化時間。Aspose 的引擎對於順序呼叫是執行緒安全的，因此重複使用同一個實例既有效率又整潔。

**Sample console output**（同樣取決於你的圖片）：

```
Hindi: कुल राशि: ₹ 1,250.00
```

如果印地文顯示為雜亂的拉丁字元，可能是忘記設定語言列舉，或是影像解析度過低（<300 dpi）。將影像升級或套用簡單的二值化濾鏡可顯著提升準確度。

---

## recognize hindi text – 常見問題與邊緣案例

即使正確設定語言旗標，仍有一些小陷阱可能讓你卡住：

| Issue | Symptom | Fix |
|-------|---------|-----|
| Low contrast | 許多字元變成「？」或被省略 | Pre‑process with `OcrImage.AdjustContrast(1.5)` |
| Skewed image | 文字呈旋轉狀，OCR 回傳空字串 | Call `ocrEngine.PreprocessImage(arabicImage, ImageProcessingOptions.Rotate)` |
| Mixed languages | 阿拉伯文行後接英文數字 | Run two passes: first with `Language.Arabic`, then with `Language.English` on the same image and concatenate results |
| Large file size | 辨識緩慢或記憶體不足錯誤 | Downscale to max 2000 px width with `OcrImage.Resize(2000, 0)` |

這些技巧可協助你 **extract text from image** 那些未完美掃描的檔案，這在實務專案中相當常見。

---

## Putting It All Together – 完整範例程式

以下是可直接貼到新 Console 專案的完整程式碼。沒有隱藏的相依性、也不需要額外設定——純粹的 C#。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

class MultiLangDemo
{
    static void Main()
    {
        // Initialize the OCR engine (CPU‑based)
        var ocrEngine = new OcrEngine();

        // -------------------- Arabic --------------------
        var arabicPath = @"C:\OCRSamples\arabic_sign.jpg";
        var arabicImage = OcrImage.FromFile(arabicPath);
        var arabicResult = ocrEngine.Recognize(arabicImage, Language.Arabic);
        System.Console.WriteLine("Arabic: " + arabicResult.Text);

        // -------------------- Hindi --------------------
        var hindiPath = @"C:\OCRSamples\hindi_receipt.png";
        var hindiImage = OcrImage.FromFile(hindiPath);
        var hindiResult = ocrEngine.Recognize(hindiImage, Language.Hindi);
        System.Console.WriteLine("Hindi: " + hindiResult.Text);
    }
}
```

**Running the program** 會在主控台印出阿拉伯文與印地文字串，證明你已成功在同一次執行中 **recognize arabic text** 與 **recognize hindi text**。  

---

## Conclusion

現在你已掌握 **how to ocr arabic** 同時處理印地文的完整解法。只要建立單一 `OcrEngine`、載入各自的影像，並傳入對應的 `Language` 列舉，即可 **extract text from image**、**convert image to text**，並同時 **recognize arabic text** 與 **recognize hindi text**，無需額外函式庫。

接下來你可以探索：

* **Batch processing** – 迴圈處理資料夾內的多張圖片，並將結果寫入資料庫。  
* **Post‑processing** – 使用正規表達式清理印地文收據中的貨幣符號。  
* **Hybrid language detection** – 在選擇列舉前，先將原始位圖送入語言辨識模型。  

試試看，調整前置處理步驟，你會看到 OCR 準確度快速提升。若遇到任何怪異情況，請隨時聯絡

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}