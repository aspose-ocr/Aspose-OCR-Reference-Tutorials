---
date: 2026-04-23
description: 使用 Aspose OCR for .NET 改善 OCR 準確度，透過拼寫檢查、支援 OCR 語言套件以及自訂詞典，提升掃描文件的 OCR
  品質。
keywords:
- improve ocr accuracy
- ocr language pack
- process scanned documents
- boost ocr quality
- ocr spell checking
linktitle: 在圖像中使用拼字檢查提升 OCR 準確度
second_title: Aspose.OCR .NET API
title: 使用圖像拼寫檢查提升 OCR 準確度
url: /zh-hant/net/ocr-optimization/result-correction-with-spell-checking/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 透過影像拼寫檢查提升 OCR 準確度

當您使用光學字符辨識 (OCR) 時，最終目標是 **提升 OCR 準確度**，使擷取的文字與原始影像完美相符。拼寫錯誤、雜訊背景以及不常見的字型都是常見的因素，會降低結果品質。結合 Aspose.OCR 內建的拼寫檢查引擎與其廣泛的 OCR 語言套件，您可以大幅 **提升 OCR 品質**，適用於任何掃描文件。

## 如何透過拼寫檢查提升 OCR 準確度

在本節中，我們將逐步說明完整的工作流程——從載入影像、套用拼寫檢查，到最後使用自訂使用者字典潤飾輸出。您將看到實際的前後對比範例，了解此步驟對掃描文件處理的重要性，並發掘如何充分利用 OCR 拼寫檢查功能的技巧。

## 快速答覆
- **What does spell checking do for OCR?** 它會自動偵測 OCR 輸出中的拼寫錯誤，並以最可能的正確詞彙取代。  
- **Which library provides this feature?** Aspose.OCR for .NET 包含即用型的拼寫檢查 API。  
- **Do I need an internet connection?** 不需要，拼寫檢查引擎完全離線運作。  
- **Can I add my own terminology?** 可以，您可提供自訂使用者字典以處理領域專用詞彙。  
- **What languages are supported?** 請參閱「aspose ocr language support」章節取得詳細資訊。

## 什麼是 OCR 中的拼寫檢查？

拼寫檢查會檢視 OCR 引擎回傳的原始文字，找出與所選語言字典中已知詞彙不匹配的詞彙，並提供或套用修正。此步驟對 **提升 OCR 準確度** 至關重要，尤其在處理掃描文件、收據或表單時，OCR 可能會誤判字元。

## 為何使用 Aspose OCR 語言套件？

Aspose.OCR 內建廣泛的語言套件，且允許您加入額外的字典。利用 **aspose ocr language support**，您可以在不編寫自訂解析器的情況下處理多語言文件，並取得語言特定規則，進一步提升辨識品質。

## 先決條件

在深入拼寫檢查的技巧之前，請確保已具備以下先決條件：

- Aspose.OCR for .NET Library: 從 [release page](https://releases.aspose.com/ocr/net/) 下載並安裝 Aspose.OCR 函式庫。
- Document Directory: 確保您有一個指定的文件目錄。將程式碼片段中的 `"Your Document Directory"` 替換為實際路徑。

## 匯入命名空間

讓我們先在 .NET 專案中匯入必要的命名空間：

```csharp
using System;
using Aspose.OCR.SpellChecker;
using System.Collections.Generic;
```

## 步驟 1：初始化 Aspose.OCR

初始化 Aspose.OCR 實例，以啟動 OCR 程序。

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## 步驟 2：辨識影像

接著，使用 Aspose.OCR 辨識影像中的文字。以下程式碼片段示範此過程：

```csharp
// Recognize image
RecognitionResult result = api.RecognizeImage(dataDir + "sample_bad.png", new RecognitionSettings(Language.Eng));
```

## 步驟 3：校正前

取得校正前的 OCR 結果，以便與校正後的版本比較。

```csharp
// Get result
Console.WriteLine("BEFORE CORRECTION:\n" + result.RecognitionText);
```

## 步驟 4：校正後

套用拼寫檢查以取得校正結果。以下程式碼片段說明此步驟：

```csharp
// Get corrected result
string correctedResult = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng);
Console.WriteLine("AFTER CORRECTION:\n" + correctedResult);
```

## 步驟 5：錯誤拼寫的詞彙與建議

使用以下程式碼取得錯誤拼寫詞彙清單及建議的修正：

```csharp
// Get list of misspelled words with suggestions
List<SpellCheckError> errorsList = result.GetSpellCheckErrorList(SpellCheckLanguage.Eng);
foreach (var word in errorsList)
{
	Console.Write("Word:" + word.Word);
	Console.Write(" StartPosition:" + word.StartPosition);
	Console.WriteLine(" Length:" + word.Length);
	Console.WriteLine("SuggestedWords:");
	foreach (var suggest in word.SuggestedWords)
	{
		Console.Write(suggest.Word + " ");
	}
	Console.WriteLine();
}
```

## 步驟 6：校正使用者文字

使用 Aspose.OCR 函式庫校正特定的使用者提供文字：

```csharp
// Correct user text
Console.WriteLine("recogniition -> " + api.CorrectSpelling("recogniition"));
```

## 步驟 7：使用使用者字典進行校正

透過加入自訂使用者字典，進一步提升校正效果：

```csharp
// Get corrected result with user dictionary
string correctedResultUserDict = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng, dataDir+"dictionary.txt");
Console.WriteLine("AFTER CORRECTION WITH USER DICTIONARY:\n" + correctedResultUserDict);
```

## 提升 OCR 品質的技巧

- **Select the correct OCR language pack** 選擇與來源文件相符的正確 OCR 語言套件。於法文文件使用 `Language.Eng` 會大幅降低準確度。  
- **Pre‑process images** 在送入 OCR 引擎前先**前處理影像**（去斜、去噪、提升對比度）；較乾淨的影像會減少拼寫錯誤。  
- **Maintain a concise user dictionary**—one word per line—維持簡潔的使用者字典——每行一個詞彙——讓拼寫檢查器能快速定位自訂詞彙，避免在大量批次時變慢。  
- **Batch process pages** 處理多頁 PDF 時使用**批次處理頁面**；可減少記憶體佔用並加速拼寫檢查階段。

## 常見問題與解決方案

| Issue | Why It Happens | How to Fix |
|-------|----------------|------------|
| No suggestions returned | 語言套件未載入或文字過短。 | 確保 `RecognitionSettings(Language.Eng)` 與來源影像的語言相符，且 OCR 結果包含足夠的字元。 |
| Custom dictionary not applied | 路徑或檔案格式不正確。 | 確認 `dictionary.txt` 存在於指定位置且每行僅有一個詞彙。 |
| Spell checker slows down large documents | 逐字處理會增加額外負擔。 | 以批次方式處理頁面，或在 .NET Core 上執行時增加記憶體配置。 |

## 常見問與答

### Q1: 我可以將 Aspose.OCR 用於英語以外的語言嗎？

A1: 是的，Aspose.OCR 支援多種語言。請相應調整語言設定。

### Q2: 如何將 Aspose.OCR 整合到我的 .NET 專案中？

A2: 請參考 [documentation](https://reference.aspose.com/ocr/net/) 以取得詳細的整合步驟。

### Q3: Aspose.OCR 有提供試用版嗎？

A3: 是的，您可以透過 [free trial version](https://releases.aspose.com/) 來體驗功能。

### Q4: 我可以上傳自訂字典以進行拼寫檢查嗎？

A4: 當然可以！本教學示範了如何使用使用者提供的字典來加強校正。

### Q5: 我可以從哪裡取得 Aspose.OCR 的支援？

A5: 請前往 [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) 取得社群支援與指導。

---

**最後更新:** 2026-04-23  
**測試環境:** Aspose.OCR for .NET latest version  
**作者:** Aspose

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}