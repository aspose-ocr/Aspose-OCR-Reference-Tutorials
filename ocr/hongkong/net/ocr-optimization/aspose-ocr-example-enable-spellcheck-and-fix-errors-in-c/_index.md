---
category: general
date: 2026-03-07
description: Aspose OCR 範例示範如何啟用拼寫檢查、加入自訂字典、載入影像 OCR，並快速修正 OCR 錯誤。
draft: false
keywords:
- aspose ocr example
- how to enable spellcheck
- how to add dictionary
- load image ocr
- how to fix ocr errors
language: zh-hant
og_description: Aspose OCR example that walks you through enabling spellcheck, adding
  a custom dictionary, loading an image for OCR and fixing common OCR errors.
og_title: Aspose OCR 範例 – 啟用拼字檢查並修正錯誤
tags:
- Aspose
- OCR
- C#
- SpellCheck
title: Aspose OCR 範例 – 在 C# 中啟用拼寫檢查並修正錯誤
url: /zh-hant/net/ocr-optimization/aspose-ocr-example-enable-spellcheck-and-fix-errors-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR 示例 – 在 C# 中啟用拼寫檢查並修正錯誤

有沒有曾經需要一個 **Aspose OCR example**，不僅能從圖像讀取文字，還能清除那些惱人的拼寫錯誤？你並不是唯一遇到這種情況的人。在許多實際專案中，原始 OCR 輸出充斥著錯別字，尤其是當來源圖像的字體對比度低或是手寫筆記時。

好消息是？使用 Aspose.OCR 你可以 **enable spellcheck**，加入自己的字典，僅用幾行程式碼就能取得潤飾過的字串。以下將會示範 **how to enable spellcheck**、**how to add a dictionary**，以及 **how to load image OCR**，讓你終於能 **fix OCR errors**，不再抓狂。

在本教學中，我們會涵蓋所有必需的內容——從 NuGet 安裝到完整、可執行的程式，印出校正後的文字。完成後，你將擁有一個可靠的 **Aspose OCR example**，可直接嵌入任何 .NET 專案。

## 前置條件

- .NET 6.0 SDK 或更新版本（此程式碼亦可於 .NET Core 與 .NET Framework 上執行）
- Visual Studio 2022 或任何相容 C# 的 IDE
- 一個圖像檔案（`typed_text.png`），內含清晰、打字的英文文字
- 具備網際網路連線以取得 Aspose.OCR NuGet 套件

不需要其他第三方函式庫。

---

## 步驟 1 – 安裝 Aspose.OCR NuGet 套件（Load Image OCR）

在撰寫任何程式碼之前，我們需要提供 OCR 引擎的函式庫。

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** 若你使用 Visual Studio，右鍵點擊專案 → *Manage NuGet Packages* → 搜尋 **Aspose.OCR** 並點選 *Install*。

安裝套件後即可使用 `OcrEngine`、`ImageStream`，以及稍後會用到的內建拼寫檢查工具。套件就緒後，你就可以 **load image OCR**。

## 步驟 2 – 建立 OCR 引擎實例

建立引擎是任何 **Aspose OCR example** 的第一個具體步驟。可將 `OcrEngine` 想像成分析位圖並輸出文字的大腦。

```csharp
using Aspose.OCR;
using Aspose.OCR.SpellCheck;

// Step 2: Initialize the OCR engine
var ocrEngine = new OcrEngine();
```

`OcrEngine` 的建構子不需要任何參數，讓快速原型開發變得簡潔易用。

## 步驟 3 – 如何啟用拼寫檢查（以及為何重要）

原始 OCR 輸出常出現錯誤辨識的單字，例如將 “the” 誤寫為 “teh”。啟用內建拼寫檢查器可讓 Aspose 自動將這些錯誤替換為最可能的正確拼寫。

```csharp
// Step 3: Turn on spell checking and set the language to English
ocrEngine.Settings.SpellCheck.Enabled = true;
ocrEngine.Settings.SpellCheck.Language = SpellCheckLanguage.English;
```

> **為何要啟用拼寫檢查？**  
> - **Accuracy（準確度）:** 後處理的拼寫檢查可將印刷文件的整體文字準確度提升 10‑15 %。  
> - **User experience（使用者體驗）:** 清晰的文字在將結果輸入搜尋索引或分析管線時，可減少後續清理工作。

## 步驟 4 – 如何加入字典（自訂詞彙）

有時預設字典不認識你的品牌名稱、產品代碼或領域特有術語。這時 **how to add dictionary** 就派上用場了。

```csharp
// Step 4: Add custom words that the spell checker should accept
ocrEngine.Settings.SpellCheck.CustomDictionary.AddWords(new[]
{
    "AsposeOCR",   // our library name
    "OCRify",      // a fictional product
    "CSharpify"    // another custom term
});
```

你可以提供陣列、清單，甚至從檔案讀取大量自訂詞彙。拼寫檢查器將把這些條目視為有效，避免錯誤的校正。

## 步驟 5 – 載入 OCR 圖像（Load Image OCR）

現在引擎已設定完成，我們需要指向要讀取的圖片。`ImageStream.FromFile` 輔助方法抽象化了檔案讀取的細節。

```csharp
// Step 5: Load the image that contains the text to be recognized
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/typed_text.png");
```

> **Tip:** 若你的圖像位於專案的子資料夾，請將其 *Copy to Output Directory* 屬性設為 *Copy always*，以確保執行時路徑正確。

## 步驟 6 – 執行辨識並修正 OCR 錯誤

設定完成後，只要呼叫一次 `Recognize()` 即可執行 OCR 流程、套用拼寫檢查，並將清理後的結果存入 `ocrEngine.Text`。

```csharp
// Step 6: Run OCR and let the spell checker clean the output
ocrEngine.Recognize();

// Step 7: Output the corrected text to the console
Console.WriteLine("Corrected text:");
Console.WriteLine(ocrEngine.Text);
```

### 預期輸出

假設 `typed_text.png` 包含句子 `The quick brown fox jumps over teh lazy dog`，控制台將顯示：

```
Corrected text:
The quick brown fox jumps over the lazy dog
```

請注意 “teh” 已自動校正為 “the”。若你已將 “OCRify” 加入自訂字典且圖像中出現該詞，則引擎會保持原樣不做更動。

---

## 完整可執行範例（可直接複製貼上）

以下是完整程式碼，可直接放入新的 Console 專案。它包含上述所有步驟，並加入少量註解以增進可讀性。

```csharp
// ---------------------------------------------------------------
// Aspose OCR Example – Enable Spellcheck and Fix Errors
// ---------------------------------------------------------------

using System;
using Aspose.OCR;
using Aspose.OCR.SpellCheck;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create the OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Enable spell checking (how to enable spellcheck)
            ocrEngine.Settings.SpellCheck.Enabled = true;
            ocrEngine.Settings.SpellCheck.Language = SpellCheckLanguage.English;

            // 3️⃣ Add custom words (how to add dictionary)
            ocrEngine.Settings.SpellCheck.CustomDictionary.AddWords(new[]
            {
                "AsposeOCR",
                "OCRify",
                "CSharpify"
            });

            // 4️⃣ Load the image (load image OCR)
            // Replace the path with the actual location of your image file
            ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/typed_text.png");

            // 5️⃣ Run OCR – this also fixes common OCR errors (how to fix ocr errors)
            ocrEngine.Recognize();

            // 6️⃣ Show the corrected result
            Console.WriteLine("Corrected text:");
            Console.WriteLine(ocrEngine.Text);
        }
    }
}
```

將此檔案存為 `Program.cs`，執行 `dotnet run`，即可在控制台看到校正後的句子。

---

## 常見問題與邊緣案例

| Question | Answer |
|----------|--------|
| **如果圖像是多頁 PDF 會怎樣？** | Aspose.OCR 能將 PDF 頁面視為圖像處理。使用 `ocrEngine.Image = ImageStream.FromPdf("file.pdf", pageNumber: 1);` 並遍歷各頁。 |
| **我可以將語言改成非英文嗎？** | 當然可以。設定 `ocrEngine.Settings.SpellCheck.Language = SpellCheckLanguage.French;`（或任何支援的語言）。 |
| **我的自訂字典很大——會影響效能嗎？** | 加入數千個詞彙會有少量的前置成本，但因底層使用 hash‑set，查找為 O(1)。若字彙極為龐大，建議在應用程式啟動時一次載入。 |
| **如果 OCR 引擎在損壞的圖像上拋出例外會怎樣？** | 將 `Recognize()` 包在 try‑catch 區塊中，檢查 `ocrEngine.LastError`。也可以先以 `ocrEngine.Image.Width` 與 `Height` 先驗證圖像尺寸。 |
| **生產環境需要授權嗎？** | 免費評估版可用於測試，但商業授權會移除評估水印並解鎖完整效能。 |

---

## 結論

現在你已擁有一個 **complete Aspose OCR example**，示範了 **how to enable spellcheck**、**how to add a dictionary**、**load image OCR**，以及 **how to fix OCR errors**，以乾淨且適合上線的方式完成。透過設定拼寫檢查器並提供自訂詞彙表，即可大幅提升擷取文字的品質，且無需自行撰寫後處理邏輯。

準備好進一步了嗎？試著將語言切換成西班牙文、處理多頁 PDF，或將輸出整合至可搜尋的 Azure Cognitive Search 索引。模式相同——只需調整語言旗標，或擴充自訂字典即可。

如果你覺得本指南有幫助，請在 GitHub 上給個星星，與同事分享，或在下方留下評論。祝編程愉快，願你的 OCR 結果永遠零錯！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}