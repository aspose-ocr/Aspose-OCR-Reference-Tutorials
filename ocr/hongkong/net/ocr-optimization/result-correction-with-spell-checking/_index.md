---
date: 2025-12-25
description: 利用 Aspose OCR for .NET 提升 OCR 準確度，透過拼寫檢查與語言支援校正錯字，並自訂字典，以實現零錯誤的文字辨識。
linktitle: Improve OCR Accuracy with Spell Checking in Images
second_title: Aspose.OCR .NET API
title: 透過圖像拼寫檢查提升 OCR 準確度
url: /zh-hant/net/ocr-optimization/result-correction-with-spell-checking/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 提升圖像 OCR 準確度的拼寫檢查

## 介紹

當您使用光學字元辨識（OCR）時，最終目標是 **提升 OCR 準確度**，讓擷取出的文字與原始圖像完美對應。拼寫錯誤是常見的錯誤來源，尤其在來源圖像雜訊較多或使用不常見字型時更為明顯。Aspose.OCR for .NET 提供內建的拼寫檢查功能，不僅能自動校正這些錯誤，還允許您透過自訂字典擴充引擎。於本教學中，您將學會如何利用拼寫檢查提升 OCR 結果，觀察前後對照的輸出，並了解如何依照特定語言需求客製化校正流程。

## 快速解答
- **拼寫檢查對 OCR 有什麼作用？** 它會自動偵測 OCR 輸出中的拼寫錯誤，並以最有可能的正確詞彙取代。  
- **哪個函式庫提供此功能？** Aspose.OCR for .NET 包含即用型的拼寫檢查 API。  
- **需要網路連線嗎？** 不需要，拼寫檢查引擎完全離線運作。  
- **可以加入自訂術語嗎？** 可以，您可以提供自訂使用者字典以處理領域專用詞彙。  
- **支援哪些語言？** 請參閱「aspose ocr language support」章節了解詳情。

## OCR 中的拼寫檢查是什麼？

拼寫檢查會檢視 OCR 引擎回傳的原始文字，找出未在所選語言字典中出現的詞彙，並提供或直接套用修正。此步驟對 **提升 OCR 準確度** 至關重要，特別是在處理掃描文件、收據或表單時，OCR 常會誤判字元。

## 為什麼使用 Aspose OCR 語言支援？

Aspose.OCR 內建豐富的語言套件，且允許您自行插入額外字典。善用 **aspose ocr language support** 意味著您可以無需自行撰寫解析器，即可處理多語言文件，並取得語言特有規則以進一步提升辨識品質。

## 前置條件

在進入拼寫檢查的魔法之前，請先確保具備以下條件：

- Aspose.OCR for .NET 函式庫：從[發行頁面](https://releases.aspose.com/ocr/net/)下載並安裝 Aspose.OCR 函式庫。

- 文件目錄：確保您有指定的文件目錄。將程式碼片段中的 `"Your Document Directory"` 替換為實際路徑。

## 匯入命名空間

先在您的 .NET 專案中匯入必要的命名空間：

```csharp
using System;
using Aspose.OCR.SpellChecker;
using System.Collections.Generic;
```

## 步驟 1：初始化 Aspose.OCR

建立 Aspose.OCR 的實例，以啟動 OCR 流程。

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## 步驟 2：辨識圖像

接著使用 Aspose.OCR 辨識圖像中的文字。以下程式碼示範此過程：

```csharp
// Recognize image
RecognitionResult result = api.RecognizeImage(dataDir + "sample_bad.png", new RecognitionSettings(Language.Eng));
```

## 步驟 3：校正前

取得未校正的 OCR 結果，以便與校正後的結果做比較。

```csharp
// Get result
Console.WriteLine("BEFORE CORRECTION:\n" + result.RecognitionText);
```

## 步驟 4：校正後

套用拼寫檢查取得校正結果。下列程式碼片段說明此步驟：

```csharp
// Get corrected result
string correctedResult = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng);
Console.WriteLine("AFTER CORRECTION:\n" + correctedResult);
```

## 步驟 5：拼寫錯誤與建議

使用以下程式碼取得拼寫錯誤清單及建議的修正詞：

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

利用 Aspose.OCR 函式庫校正特定的使用者提供文字：

```csharp
// Correct user text
Console.WriteLine("recogniition -> " + api.CorrectSpelling("recogniition"));
```

## 步驟 7：使用使用者字典進行校正

透過自訂使用者字典進一步強化校正效果：

```csharp
// Get corrected result with user dictionary
string correctedResultUserDict = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng, dataDir+"dictionary.txt");
Console.WriteLine("AFTER CORRECTION WITH USER DICTIONARY:\n" + correctedResultUserDict);
```

## 常見問題與解決方案

| 問題 | 為何發生 | 解決方法 |
|------|----------|----------|
| 未返回建議 | 語言包未載入或文字過短。 | 確保 `RecognitionSettings(Language.Eng)` 與來源圖像的語言相符，且 OCR 結果包含足夠的字元。 |
| 自訂字典未套用 | 路徑或檔案格式不正確。 | 驗證 `dictionary.txt` 是否存在於指定位置，且每行僅有一個單詞。 |
| 拼寫檢查在大型文件上變慢 | 逐字處理增加了開銷。 | 將頁面分批處理，或在 .NET Core 上增加記憶體配置。 |

## 常見問答

### Q1：我可以將 Aspose.OCR 用於英語以外的語言嗎？

A1：可以，Aspose.OCR 支援多種語言。請依需求調整語言設定。

### Q2：如何將 Aspose.OCR 整合到我的 .NET 專案中？

A2：請參考[文件說明](https://reference.aspose.com/ocr/net/)取得詳細的整合步驟。

### Q3：是否提供 Aspose.OCR 的試用版？

A3：可以，您可透過[免費試用版](https://releases.aspose.com/)探索功能。

### Q4：我可以上傳自訂字典用於拼寫檢查嗎？

A4：當然可以！本教學示範了如何使用使用者提供的字典來增強校正。

### Q5：我可以在哪裡取得 Aspose.OCR 的支援？

A5：請前往[Aspose.OCR 論壇](https://forum.aspose.com/c/ocr/16)尋求社群支援與指導。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**最後更新：** 2025-12-25  
**測試環境：** Aspose.OCR for .NET latest version  
**作者：** Aspose