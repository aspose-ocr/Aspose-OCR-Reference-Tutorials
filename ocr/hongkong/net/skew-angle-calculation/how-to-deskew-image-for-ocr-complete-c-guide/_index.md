---
category: general
date: 2026-01-06
description: 學習如何校正圖像傾斜、去除噪點，並使用 Aspose OCR 提取文字。一步一步的指南亦會示範如何載入圖像進行 OCR。
draft: false
keywords:
- how to deskew image
- how to extract text
- how to remove noise
- recognize text from image
- load image for ocr
language: zh-hant
og_description: 學習如何校正圖像傾斜、去除雜訊，並使用 Aspose OCR 提取文字。分步指南亦會示範如何載入圖像以進行 OCR。
og_title: 如何校正影像傾斜以進行 OCR – 完整 C# 指南
tags:
- OCR
- C#
- Image Processing
title: 如何校正影像傾斜以進行 OCR – 完整 C# 指南
url: /zh-hant/net/skew-angle-calculation/how-to-deskew-image-for-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何校正影像以進行 OCR – 完整 C# 指南

曾經想過在將影像檔案送入 OCR 引擎之前，**如何校正影像**嗎？你並不孤單——大多數開發者在掃描的照片稍微傾斜、雜訊過多或根本難以閱讀時，都會遇到相同的障礙。好消息是？使用 Aspose OCR，你可以在幾行 C# 程式碼中將影像校正、清理，然後擷取文字。

在本教學中，我們將逐步說明 **如何擷取文字**、**如何去除雜訊**，以及當然的 **如何校正影像**，讓 OCR 結果精準無誤。最後，你還會了解 **如何載入影像以供 OCR**，並取得乾淨、可搜尋的字串，直接供應用程式使用。

---

## 您需要的條件

- **Aspose.OCR for .NET** (v23.12 或更新版本)。NuGet 套件名稱為 `Aspose.OCR`。
- .NET 6+（任何近期的執行環境皆可）。
- 一張已傾斜或有斑點的範例影像，例如 `skewed_photo.jpg`。
- Visual Studio、Rider，或你慣用的編輯器。

不需要額外的原生函式庫——Aspose 於程式內部處理所有工作。

## 步驟 1 – 設定 OCR 引擎（從影像辨識文字）

在我們能 **載入影像以供 OCR** 之前，需要先建立引擎實例並指定要辨識的語言。

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Create the OCR engine and tell it we’re reading English text.
OcrEngine ocrEngine = new OcrEngine
{
    Language = OcrLanguage.English
};
```

**為什麼這很重要：** `OcrEngine` 是整個流程的核心。提前設定 `Language` 可確保辨識演算法使用正確的字元集，從而大幅提升準確度。

## 步驟 2 – 載入您的影像（載入影像以供 OCR）

現在把引擎指向磁碟上的檔案。許多教學在此處就停下來了，但我們也會討論常見的陷阱。

```csharp
// Load the image you want to process.
ocrEngine.Image = ImageStream.FromFile(@"C:\Images\skewed_photo.jpg");
```

> **專業提示：** 測試時使用絕對路徑，之後再改成相對路徑或嵌入資源以供正式環境使用。同時，請確保影像為支援的格式（JPEG、PNG、BMP、TIFF）。若收到「Unsupported format」錯誤，請再次檢查檔案副檔名與 MIME 類型。

## 步驟 3 – 前處理：校正與去斑點（如何校正影像 & 如何去除雜訊）

傾斜的文件是 OCR 的經典噩夢。Aspose 提供 `DeskewFilter`，可自動偵測至可設定的最大角度並校正。再搭配 `DespeckleFilter` 清除鹽與胡椒雜訊。

```csharp
// 1️⃣ Deskew – correct rotation up to 15° (adjust as needed)
ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 15 });

// 2️⃣ Despeckle – reduce noise; Strength 1‑5 (3 is moderate)
ocrEngine.Filters.Add(new DespeckleFilter { Strength = 3 });
```

### Deskew Filter 的運作原理
此過濾器會掃描影像中的主要文字基線，計算傾斜角度，並相應旋轉位圖。若影像已經水平，過濾器不會執行任何操作——因此可安全地加入任何處理流程。

### Despeckle Filter 的效用
雜訊常以孤立的暗點或亮點出現。去斑點演算法使用中值濾波，保留邊緣（如字形筆畫），同時平滑斑點。過高的強度會模糊細節，建議先以 `Strength = 3` 為起點，依來源素材調整。

> **旁註：** 若影像的旋轉角度超過 15°，請提高 `MaxAngle`。若文件是倒置掃描，可能需要在 Deskew Filter 前先自行旋轉一次 (`Image.Rotate(angle)`)。

## 步驟 4 – 執行辨識（從影像辨識文字）

完成前處理後，我們最終請引擎讀取文字。

```csharp
if (ocrEngine.Recognize())
{
    // The recognized text is now stored in ocrEngine.Text
    Console.WriteLine("=== Extracted Text ===");
    Console.WriteLine(ocrEngine.Text);
}
else
{
    Console.WriteLine("Recognition failed – check the image quality.");
}
```

### 內部運作流程
1. **二值化：** 將影像轉為黑白，提高對比度。
2. **分割：** 把位圖切分為行、詞與字元。
3. **分類：** 將每個字元與已訓練模型（英文字母、數字、標點）比對。
4. **後處理：** 套用語言規則（例如拼字檢查）提升可讀性。

因為我們已 **校正了影像** 並 **去除雜訊**，每個階段都能取得較乾淨的資料，從而減少錯誤辨識的機會。

## 步驟 5 – 驗證與清理輸出（如何有效擷取文字）

原始字串可能包含多餘的換行或空格。快速清理即可讓資料適合後續處理。

```csharp
string raw = ocrEngine.Text;

// Trim leading/trailing whitespace and collapse multiple newlines.
string cleaned = System.Text.RegularExpressions.Regex
    .Replace(raw, @"\s+", " ")
    .Trim();

Console.WriteLine("\n=== Cleaned Text ===");
Console.WriteLine(cleaned);
```

**為什麼要清理？** 許多 OCR 函式庫會保留原始版面配置，對 PDF 很有用，但對純文字管線卻會產生噪音。正規化空白字元可確保你能將結果存入資料庫或送入搜尋索引，而不需額外處理。

## 完整範例程式

以下是可直接複製貼上的完整程式，將所有步驟串接在一起。存為 `Program.cs`，加入 Aspose.OCR NuGet 套件後執行。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English
        };

        // 2️⃣ Load the image you want to process
        //    (this demonstrates how to load image for OCR)
        ocrEngine.Image = ImageStream.FromFile(@"C:\Images\skewed_photo.jpg");

        // 3️⃣ Add preprocessing filters
        //    - Deskew up to 15° (how to deskew image)
        //    - Despeckle with moderate strength (how to remove noise)
        ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 15 });
        ocrEngine.Filters.Add(new DespeckleFilter { Strength = 3 });

        // 4️⃣ Perform recognition (recognize text from image)
        if (ocrEngine.Recognize())
        {
            // 5️⃣ Output raw and cleaned text (how to extract text)
            Console.WriteLine("=== Raw OCR Output ===");
            Console.WriteLine(ocrEngine.Text);

            string cleaned = System.Text.RegularExpressions.Regex
                .Replace(ocrEngine.Text, @"\s+", " ")
                .Trim();

            Console.WriteLine("\n=== Cleaned OCR Output ===");
            Console.WriteLine(cleaned);
        }
        else
        {
            Console.WriteLine("OCR failed – verify the image path and quality.");
        }
    }
}
```

**預期輸出**（假設範例影像內含「Hello World」這句話）：

```
=== Raw OCR Output ===
Hello World

=== Cleaned OCR Output ===
Hello World
```

若影像嚴重傾斜，加入 `DeskewFilter` 前的原始輸出會出現亂碼；加入過濾器後，文字變得清晰可讀——正是我們想要達成的效果。

## 常見問題與特殊情況

| 問題 | 解答 |
|----------|--------|
| *如果我的影像旋轉角度超過 15°，該怎麼辦？* | 在 `DeskewFilter` 中提升 `MaxAngle`。最高可設定至 45°，但極端角度可能仍需先手動旋轉 (`Image.Rotate(angle)`)。 |
| *去斑點後 OCR 仍遺漏字母。* | 嘗試提升 `Strength`（4‑5），或在去斑點前加入 `ContrastFilter`。 |
| *可以直接處理 PDF 嗎？* | 可以——使用 `PdfDocument` 將每頁渲染為影像，然後將每個位圖送入相同的管線。 |
| *引擎是否支援多執行緒？* | 請為每個執行緒建立獨立的 `OcrEngine`；此類別本身未保證為執行緒安全。 |
| *如何處理多語言文件？* | 設定 `ocrEngine.Language = OcrLanguage.Multilingual`，或依頁面切換語言。 |

## 生產環境 OCR 的最佳實踐

1. **批次處理：** 迴圈讀取資料夾內的影像，重複使用同一個 `OcrEngine` 實例以降低開銷。  
2. **日誌記錄：** 當 `Recognize()` 回傳 false 時，檢查 `ocrEngine.LastError`，通常會指示不支援的格式或檔案損毀。  
3. **效能考量：** 校正步驟最耗 CPU。若確定影像已水平，可省略此過濾器。  
4. **記憶體管理：** 使用完 `ImageStream` 後務必呼叫 `ocrEngine.Image.Dispose()`，避免長時間服務產生記憶體泄漏。  

## 結論

我們已說明 **如何校正影像**、**如何去除雜訊**、**如何載入影像以供 OCR**，以及 **如何擷取文字**，全部使用 Aspose OCR 於 C# 實作。透過 `DeskewFilter` 與 `DespeckleFilter` 前置處理，可大幅提升 `Recognize()` 回傳乾淨、可搜尋字串的機率。

從第一行程式碼到最終清理的輸出，步驟簡單明瞭，卻足以應付真實世界的需求——無論你在建置文件歸檔服務、收據掃描行動應用，或是批次處理後端系統。

準備好迎接下一個挑戰了嗎？試著加入 **語言偵測** 步驟，或實驗 **自訂 OCR 字典**，提升特定產業詞彙的辨識率。天際無限，而你已擁有堅實的基礎可供構築。

祝程式開發順利，願你的影像永遠保持完美水平！

![校正後文件的示意圖](deskewed_example.png "如何校正影像")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}