---
category: general
date: 2026-06-03
description: 使用 Aspose.OCR 對圖片執行文字辨識並擷取文字。於單一 C# 示範中學習如何偵測拼寫錯誤並取得拼寫建議。
draft: false
keywords:
- perform OCR on image
- extract text from image
- detect misspelled words
- get spelling suggestions
- how to extract text
language: zh-hant
og_description: 對圖像執行 OCR 以提取文字，然後偵測拼字錯誤並取得拼字建議，使用 Aspose.OCR 於 C#。
og_title: 在影像上執行 OCR 並偵測錯別字（C#）
schemas:
- author: Aspose
  dateModified: '2026-06-03'
  description: Perform OCR on image and extract text from image using Aspose.OCR.
    Learn how to detect misspelled words and get spelling suggestions in a single
    C# demo.
  headline: Perform OCR on Image and Detect Misspelled Words in C#
  type: TechArticle
tags:
- Aspose OCR
- C#
- Spell Checking
title: 在 C# 中對圖像執行 OCR 並偵測拼寫錯誤的字詞
url: /zh-hant/net/text-recognition/perform-ocr-on-image-and-detect-misspelled-words-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中對圖像執行 OCR 並偵測拼寫錯誤

有沒有想過如何 **perform OCR on image** 而不至於抓狂？你並不是唯一的疑問者。無論是數位化舊信件、掃描收據，或是構建智慧文件工作流程，從圖片中提取乾淨文字都是第一道關卡。好消息是，只要使用 Aspose.OCR，你可以在幾分鐘內完成解決方案，且同時 **detect misspelled words** 並 **get spelling suggestions**。

在本教學中，我們將逐步說明一個完整、可直接執行的 C# 主控台應用程式，**extract text from image**、執行英文拼寫檢查，並將每個錯誤與修正建議印出。完成後，你將清楚知道 **how to extract text**、如何呼叫拼寫檢查 API，以及預期的主控台輸出長什麼樣子。

## 你將會建立的功能

- 載入包含錯別字的 bitmap（或 PNG）。  
- 使用 Aspose.OCR **perform OCR on image** 並取得原始字串資料。  
- 初始化內建的英文拼寫檢查器。  
- **Detect misspelled words** 並 **get spelling suggestions**。  
- 在主控台印出整齊的報告。

不需要外部服務，也不需要繁雜的 HTTP 呼叫——只要一個 NuGet 套件與少量程式碼。

## 前置條件

- .NET 6.0 SDK 或更新版本（此程式碼亦可在 .NET Framework 4.7+ 上執行）。  
- Visual Studio 2022（或任何你喜歡的編輯器）。  
- Aspose.OCR for .NET NuGet 套件（`Aspose.OCR`）。  
- 一個圖像檔案（`letter_with_typos.png`），放在專案可參照的路徑下。

如果你從未使用過 Aspose，也別擔心——安裝套件只要執行以下指令：

```bash
dotnet add package Aspose.OCR
```

現在讓我們深入實作。

## 步驟 1：建立專案並安裝 Aspose.OCR

建立一個新的主控台專案，並將 OCR 函式庫加入：

```bash
dotnet new console -n OcrSpellDemo
cd OcrSpellDemo
dotnet add package Aspose.OCR
```

還原完成後，開啟 `Program.cs`。稍後我們會把預設內容換成完整示範程式碼，先說明每個命名空間的用途。

- `Aspose.OCR` – 核心 OCR 引擎與圖像處理。  
- `Aspose.OCR.SpellCheck` – 隨函式庫提供的拼寫檢查工具。  
- `System` – 標準 .NET 基礎類別（例如 `Console`）。

## 步驟 2：載入圖像並 **perform OCR on image**

真正的工作是把圖像送入 OCR 引擎。Aspose.OCR 支援多種格式（PNG、JPEG、TIFF）。以下程式碼負責完成這項重任：

```csharp
// Step 2: Load the image that contains the text to be recognized
var image = OcrImage.FromFile(@"YOUR_DIRECTORY/letter_with_typos.png");

// Step 3: Perform OCR to extract the raw text from the image
var ocrEngine = new OcrEngine();
var ocrResult = ocrEngine.Recognize(image);
```

> **為什麼重要：** `OcrImage.FromFile` 會抽象化像素層面的細節，而 `OcrEngine.Recognize` 會執行訓練好的神經模型，將視覺字形轉換成 Unicode 字元。`ocrResult.Text` 屬性現在就保存了原始字串——正是 **extract text from image** 所需要的資料。  
> 
> > **小技巧：** 若圖像包含多種語言，可在呼叫 `Recognize` 前設定 `ocrEngine.Language = OcrLanguage.Multilingual;`。

## 步驟 3：初始化英文拼寫檢查器

Aspose.OCR 內建的拼寫檢查引擎預設支援英文，只要一行程式即可完成初始化：

```csharp
// Step 4: Initialise the English spell‑checker
var spellChecker = new SpellChecker(OcrLanguage.English);
```

> **為什麼這一步關鍵：** OCR 輸出可能包含辨識錯誤（例如 “l” 與 “1” 混淆）或原始文件本身的錯別字。拼寫檢查器會掃描字串、找出可疑的 token，並提供替代方案。

## 步驟 4：**Detect Misspelled Words** 並 **Get Spelling Suggestions**

將 OCR 取得的文字交給檢查器：

```csharp
// Step 5: Check the recognized text for misspelled words and obtain suggestions
var misspellings = spellChecker.Check(ocrResult.Text);
```

`misspellings` 為一個集合，每筆條目包含錯誤單字以及可能的修正字串陣列。

## 步驟 5：輸出結果

最後，我們遍歷集合並印出易讀的報告：

```csharp
// Step 6: Output each misspelled word together with its suggested corrections
foreach (var entry in misspellings)
{
    Console.WriteLine($"Misspelled: {entry.Word}");
    Console.WriteLine("  Suggestions: " + string.Join(", ", entry.Suggestions));
}
```

### 預期的主控台輸出

假設 `letter_with_typos.png` 內的句子為：

```
Ths is an exampel of a lettter with som misspelled wrds.
```

執行示範程式後會產生類似以下的結果：

```
Misspelled: Ths
  Suggestions: This, Thus, The
Misspelled: exampel
  Suggestions: example, exemplar, exampell
Misspelled: lettter
  Suggestions: letter, litter, lett
Misspelled: som
  Suggestions: some, sum, son
Misspelled: wrds
  Suggestions: words, wards, wryds
```

可以看到每個錯字都配上一組合理的修正建議——這正是建構使用者友好校正 UI 時所需要的。

## 完整可執行範例

以下是 **完整、可直接複製貼上的** 程式。請將 `YOUR_DIRECTORY` 替換成實際的圖像檔案路徑。

```csharp
using Aspose.OCR;
using Aspose.OCR.SpellCheck;
using System;

class SpellCheckDemo
{
    static void Main()
    {
        // Step 1: Load the image that contains the text to be recognized
        var image = OcrImage.FromFile(@"YOUR_DIRECTORY/letter_with_typos.png");

        // Step 2: Perform OCR to extract the raw text from the image
        var ocrEngine = new OcrEngine();
        var ocrResult = ocrEngine.Recognize(image);

        // Step 3: Initialise the English spell‑checker
        var spellChecker = new SpellChecker(OcrLanguage.English);

        // Step 4: Check the recognized text for misspelled words and obtain suggestions
        var misspellings = spellChecker.Check(ocrResult.Text);

        // Step 5: Output each misspelled word together with its suggested corrections
        foreach (var entry in misspellings)
        {
            Console.WriteLine($"Misspelled: {entry.Word}");
            Console.WriteLine("  Suggestions: " + string.Join(", ", entry.Suggestions));
        }

        // Optional: Keep console window open when debugging
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

> **需留意的邊緣情況**  
> - **空白圖像：** 若 OCR 引擎回傳空字串，`spellChecker.Check` 只會回傳空集合——不會當機。  
> - **非英文文字：** 將 `OcrLanguage.English` 換成 `OcrLanguage.French`（或其他支援語言）即可 **detect misspelled words** 於其他語系。  
> - **大型文件：** 若處理多頁 PDF，請對每頁迴圈執行 OCR，然後在拼寫檢查前彙總結果。

## 視覺概覽（圖片替代文字）

![Diagram showing the flow to perform OCR on image, extract text from image, and then detect misspelled words with spelling suggestions](perform-ocr-on-image-flow.png)

*上圖說明端對端流程：圖像 → OCR 引擎 → 原始文字 → 拼寫檢查器 → 建議。*

## 常見問題與進階小技巧

| Question | Answer |
|----------|--------|
| **是否需要網路連線？** | 不需要。Aspose.OCR 完全在本機執行，適合離線或高安全性環境。 |
| **拼寫檢查的準確度如何？** | 使用約 15 萬筆英文單字的字典與模糊匹配，大多數常見錯別字都能被捕捉。 |
| **可以自訂字典嗎？** | 可以。`SpellChecker.AddUserDictionary("custom.txt")` 讓你載入領域專屬詞彙（例如產品名稱）。 |
| **圖像若傾斜該怎麼辦？** | OCR 引擎會自動偵測方向，但對於頑固情況，可手動呼叫 `ocrEngine.ImagePreprocessing.Rotate(angle)` 進行旋轉。 |
| **有沒有方法在 UI 上標示建議？** | 取得 `misspellings` 集合後，可將每個 `entry.Word` 對應回 `ocrResult.Text` 中的位置，並在 RichTextBox 或 WebView 中加底線或高亮。 |

## 結論

我們已示範如何 **perform OCR on image**、**extract text from image**，再 **detect misspelled words** 並 **get spelling suggestions**，全部透過簡潔的 C# 主控台應用程式完成。核心概念很簡單：讓 Aspose.OCR 負責字元辨識，然後利用內建的拼寫檢查器清理輸出。接下來，你可以將此示範擴充為完整的文件處理服務、整合至 Web API，或嵌入桌面編輯器。

準備好進一步挑戰了嗎？試著改用西班牙語、處理多頁 PDF，或打造一個小型 WPF 前端，讓使用者點擊單字接受建議。所有基礎已備妥，只等你持續實驗。

如果在實作過程中遇到問題或有擴充想法，歡迎在下方留言。祝開發順利！

## 接下來該學什麼？

以下教學與本篇內容緊密相關，能進一步深化你的技巧。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助你掌握更多 API 功能與替代實作方式。

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image Using Aspose.OCR .NET](/ocr/english/net/image-and-drawing-recognition/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}