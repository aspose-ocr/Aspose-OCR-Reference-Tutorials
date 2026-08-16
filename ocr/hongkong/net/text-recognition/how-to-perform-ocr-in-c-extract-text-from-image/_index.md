---
category: general
date: 2026-04-03
description: 學習如何在 C# 中執行 OCR，並使用 Aspose OCR 從圖像中提取文字，並提供俄文拼寫檢查。
draft: false
keywords:
- how to perform OCR
- extract text from image
- convert image to text
- how to spell check
- ocr russian language
language: zh-hant
og_description: 學習如何在 C# 中執行 OCR，使用 Aspose OCR 從圖像提取文字，並支援俄文拼寫檢查。
og_title: 如何在 C# 中執行 OCR – 從圖像擷取文字
tags:
- OCR
- C#
- Aspose
- SpellCheck
title: 如何在 C# 中執行 OCR – 從圖像擷取文字
url: /zh-hant/net/text-recognition/how-to-perform-ocr-in-c-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中執行 OCR – 從圖像提取文字

有沒有想過 **how to perform OCR** 在手寫筆記的相片上？也許你手上有掃描的收據、外語招牌，或是無法直接複製貼上的 PDF 頁面。好消息是，只要幾行 C# 程式碼加上 Aspose OCR 套件，就能把圖片瞬間變成可編輯的文字。

在本教學中，我們不只會示範 **how to perform OCR**，還會一步步說明 **extract text from image**、**convert image to text**，甚至在處理俄文文件時 **how to spell check** 結果。聽起來很多？別急，我們會逐段拆解說明。

## 你將學會

完成本教學後，你將能夠：

* 為俄文語系設定 Aspose OCR。  
* 載入圖片檔案並執行光學字元辨識，以 **extract text from image**。  
* 使用內建的拼字檢查器自動校正錯字——解答 “**how to spell check**” OCR 輸出的最佳方案。  
* 將清理過的字串印出到主控台，方便後續處理或儲存。

**先備條件** – 你需要：

* .NET 6.0 或更新版本（程式碼同樣支援 .NET Framework 4.8）。  
* 有效的 Aspose OCR 授權或暫時的評估金鑰。  
* 含有俄文文字的圖片檔（示範用檔名為 `russian_note.jpg`）。  

如果上述任何項目你不熟悉，也沒關係。以下步驟會提供完整的 NuGet 安裝指令，程式碼亦為自包含。

![how to perform OCR example](/images/ocr-demo.png "how to perform OCR in C# example")

## Step 1 – Install Aspose OCR and Add Namespaces

首先，你必須取得程式庫。於專案資料夾的終端機執行：

```bash
dotnet add package Aspose.OCR
```

此指令會下載最新的穩定版（截至 2026 年 4 月為 22.9）。套件還原完成後，於 C# 檔案最上方加入必要的 `using` 陳述式：

```csharp
using Aspose.OCR;
using Aspose.OCR.SpellCheck;
using System.Drawing;
```

*Pro tip:* 若使用 Visual Studio，IDE 會在你輸入第一個類別名稱時自動建議加入這些 `using`。

## Step 2 – Initialise the OCR Engine for Russian Language

**how to perform OCR** 的第一步是建立 `OcrEngine` 實例。透過指定 `OcrLanguage.Russian`，我們告訴引擎載入西里爾字元集與語系專屬的啟發式演算法。

```csharp
// Step 2: Initialise OCR engine for Russian
OcrEngine ocrEngine = new OcrEngine
{
    Language = OcrLanguage.Russian   // Enables Russian language support
};
```

為什麼這麼重要？若未設定語系，引擎預設使用英文，會把許多西里爾字元誤判為雜訊，導致輸出變形。明確設定語系可大幅提升辨識準確度。

## Step 3 – Load the Image and **Convert Image to Text**

接著把圖片載入記憶體。`Image.FromFile` 支援大多數常見格式（JPG、PNG、BMP）。載入後呼叫 `Recognize` 以 **convert image to text**。

```csharp
// Step 3: Load the image that contains Russian text
Image sourceImage = Image.FromFile(@"YOUR_DIRECTORY/russian_note.jpg");

// Step 4: Perform OCR – this is the core “how to perform OCR” call
string rawText = ocrEngine.Recognize(sourceImage);
```

此時 `rawText` 變數已包含原始 OCR 結果，仍可能有錯字或辨識錯誤。你可以將它印出來觀察引擎捕捉到的內容：

```csharp
Console.WriteLine("Raw OCR output:");
Console.WriteLine(rawText);
```

## Step 4 – **How to Spell Check** the OCR Result

俄文 OCR 常會因低解析度掃描而產生雜訊。Aspose 提供的 `SpellChecker` 類別內建俄文詞典，使用方式如下：

```csharp
// Step 5: Initialise the spell checker
SpellChecker spellChecker = new SpellChecker();

// Step 6: Correct spelling mistakes in the recognized text
string correctedText = spellChecker.CheckAndCorrect(rawText, OcrLanguage.Russian);
```

`CheckAndCorrect` 方法會回傳一個新字串，將錯字替換為最可能的正確詞彙，同時保留標點符號，避免出現一長串無斷的文字。

*Edge case:* 若 OCR 輸出為空（例如整張圖是全白），`CheckAndCorrect` 只會回傳空字串。若你打算將結果寫入檔案，建議先檢查此情況。

## Step 5 – Display the Cleaned‑Up Result

最後，我們把校正後的字串輸出。實務上可能會寫入資料庫、JSON API，或是 Word 文件；此示範僅以主控台顯示為例：

```csharp
// Step 7: Show the corrected result
Console.WriteLine("\nCorrected text:");
Console.WriteLine(correctedText);
```

執行程式後，你應該會看到類似以下的結果：

```
Raw OCR output:
Привeт мир! Этo тeкcт c русcкoй оcнoвнoй.

Corrected text:
Привет мир! Это текст с русской основой.
```

可以注意到拼字檢查器把 “Привeт”（混用拉丁字母 e）修正為正確的西里爾字 “Привет”。這就是 **how to spell check** OCR 輸出的魔法。

## Full Working Example

以下為完整、可直接執行的程式碼範例，將上述所有步驟串接起來。複製貼上至新的主控台專案後，按 **F5** 即可執行。

```csharp
using Aspose.OCR;
using Aspose.OCR.SpellCheck;
using System.Drawing;

class SpellCheckDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine configured for Russian language
        OcrEngine ocrEngine = new OcrEngine { Language = OcrLanguage.Russian };

        // Step 2: Load the image that contains the text to be recognized
        Image sourceImage = Image.FromFile(@"YOUR_DIRECTORY/russian_note.jpg");

        // Step 3: Perform OCR to extract raw text from the image
        string rawText = ocrEngine.Recognize(sourceImage);

        // Optional: Show raw OCR output
        System.Console.WriteLine("Raw OCR output:");
        System.Console.WriteLine(rawText);

        // Step 4: Initialise the spell checker
        SpellChecker spellChecker = new SpellChecker();

        // Step 5: Correct spelling mistakes in the recognized text
        string correctedText = spellChecker.CheckAndCorrect(rawText, OcrLanguage.Russian);

        // Step 6: Display the corrected result
        System.Console.WriteLine("\nCorrected text:");
        System.Console.WriteLine(correctedText);
    }
}
```

### 預期輸出

使用清晰且高解析度的俄文手寫照片執行程式，通常會得到一段可讀的句子。若照片模糊，仍可能出現部分錯誤字詞，但拼字檢查器會自動平滑大多數明顯的錯誤。

## Common Pitfalls & Tips

| Issue | Why it Happens | How to Fix / Avoid |
|-------|----------------|--------------------|
| **Garbage characters** | 解析度過低或背景雜訊太多 | 在送入 `Recognize` 前先前處理圖片（提升對比、調整至 ≥300 dpi）。 |
| **Empty output** | 檔案路徑錯誤或格式不支援 | 確認路徑正確，並在 `Image.FromFile` 加上 `try/catch` 以捕捉例外。 |
| **Spell checker misses errors** | 詞典未收錄罕見詞彙 | 透過 `spellChecker.AddUserDictionary("mywords.txt")` 載入自訂詞典。 |
| **Performance lag on large batches** | OCR 為 CPU 密集型工作 | 使用背景執行緒或 `Parallel.ForEach` 處理多張圖片。 |
| **License exception** | 評估版逾期使用 | 購買授權後於建立 `OcrEngine` 前呼叫 `License license = new License(); license.SetLicense("Aspose.Total.lic");`。 |

## Next Steps – Going Beyond Simple OCR

掌握 **how to perform OCR** 後，你可以進一步探索以下延伸應用：

* **Batch processing** – 迴圈處理資料夾內所有圖片，並將每張校正後的文字寫入 `.txt` 檔。  
* **PDF conversion** – 使用 Aspose PDF 將抽取的文字嵌入可搜尋的 PDF 中。  
* **Language detection** – 若需同時支援多種語言，可先檢查 OCR 結果再動態切換 `OcrLanguage`。  
* **Integration with Azure Cognitive Services** – 將 Aspose 的結果與 Microsoft OCR API 做比對，實作混合式解決方案。

上述所有主題皆自然涉及次要關鍵字 **extract text from image**、**convert image to text** 與 **how to spell check**，因此

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}