---
date: 2026-04-29
description: 提升 OCR 準確度，學習如何使用 Aspose OCR for .NET 從圖像識別文字，利用拼字檢查與語言支援來校正錯字並自訂字典。
keywords:
- improve ocr accuracy
- recognize text from image
- Aspose OCR spell checking
- custom OCR dictionary
linktitle: 使用圖像拼寫檢查提升 OCR 準確度
second_title: Aspose.OCR .NET API
title: 透過圖像拼寫檢查提升 OCR 準確度
url: /zh-hant/net/ocr-optimization/result-correction-with-spell-checking/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 提升 OCR 準確度：影像中的拼寫檢查

當您使用光學字符辨識 (OCR) 時，最終目標是**提升 OCR 準確度**，使擷取的文字與原始影像完全相符。拼寫錯誤是常見的錯誤來源，尤其在來源影像雜訊較多或使用不常見字型時更是如此。Aspose.OCR for .NET 提供內建的拼寫檢查功能，不僅能校正這些錯誤，還允許您透過自訂字典擴充引擎。在本教學中，您將學習如何使用拼寫檢查提升 OCR 結果，查看前後對照的輸出，並了解如何依照特定語言需求調整校正流程。

## 快速回答
- **拼寫檢查對 OCR 有什麼作用？** 它會自動偵測 OCR 輸出中的拼寫錯誤，並以最有可能的正確詞彙取代。  
- **哪個函式庫提供此功能？** Aspose.OCR for .NET 包含即用型的拼寫檢查 API。  
- **需要網路連線嗎？** 不需要，拼寫檢查引擎完全離線運作。  
- **我可以加入自己的術語嗎？** 可以，您可以提供自訂使用者字典以處理領域特定詞彙。  
- **這如何協助我從影像辨識文字？** 透過校正 OCR 產生的錯誤，最終文字變得乾淨，並可直接用於後續處理。

## OCR 中的拼寫檢查是什麼？
拼寫檢查會檢視 OCR 引擎返回的原始文字，找出與所選語言字典中已知詞彙不匹配的詞彙，並提供或套用校正建議。此步驟對**提升 OCR 準確度**至關重要，尤其在處理掃描文件、收據或表單時，OCR 可能會誤判字元。

## 為何使用 Aspose OCR 語言支援？
Aspose.OCR 內建大量語言套件，並允許您加入額外字典。利用 **aspose ocr language support**，您可以在不編寫自訂解析器的情況下處理多語言文件，並取得語言特定規則，以進一步提升辨識品質。

## 何時提升 OCR 準確度最為重要？
- **法律與合規文件**，單一錯字可能改變含義。  
- **資料抽取流程**，將 OCR 結果輸入分析或 AI 模型。  
- **面向客戶的應用程式**，例如必須即時返回可讀文字的手機掃描器。  

## 前置條件

在深入拼寫檢查的技巧之前，請確保已具備以下前置條件：

- Aspose.OCR for .NET 函式庫：從[發行頁面](https://releases.aspose.com/ocr/net/)下載並安裝 Aspose.OCR 函式庫。  
- 文件目錄：確保您有指定的文件目錄。於程式碼片段中將 `"Your Document Directory"` 替換為實際路徑。

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

## 步驟 5：拼寫錯誤與建議

使用以下程式碼取得拼寫錯誤詞彙清單及建議的校正：

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

使用 Aspose.OCR 函式庫校正特定使用者提供的文字：

```csharp
// Correct user text
Console.WriteLine("recogniition -> " + api.CorrectSpelling("recogniition"));
```

## 步驟 7：使用使用者字典進行校正

透過加入自訂使用者字典，進一步強化校正效果：

```csharp
// Get corrected result with user dictionary
string correctedResultUserDict = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng, dataDir+"dictionary.txt");
Console.WriteLine("AFTER CORRECTION WITH USER DICTIONARY:\n" + correctedResultUserDict);
```

## 常見問題與解決方案

| 問題 | 發生原因 | 解決方法 |
|------|----------|----------|
| 未返回建議 | 語言套件未載入或文字太短。 | 確保 `RecognitionSettings(Language.Eng)` 與來源影像的語言相符，且 OCR 結果包含足夠的字元。 |
| 自訂字典未套用 | 路徑或檔案格式不正確。 | 確認 `dictionary.txt` 存在於指定位置，且每行僅有一個詞。 |
| 拼寫檢查器在大型文件上變慢 | 逐字處理會增加額外負擔。 | 將頁面分批處理，或在 .NET Core 上執行時增加記憶體配置。 |

## 常見問答

**Q1：我可以將 Aspose.OCR 用於英語以外的語言嗎？**  
A1：可以，Aspose.OCR 支援多種語言，請相應調整語言設定。

**Q2：如何將 Aspose.OCR 整合至我的 .NET 專案？**  
A2：請參考[文件說明](https://reference.aspose.com/ocr/net/)以取得詳細的整合步驟。

**Q3：是否提供 Aspose.OCR 的試用版？**  
A3：有，您可透過[免費試用版](https://releases.aspose.com/)探索功能。

**Q4：我可以上傳自訂字典以進行拼寫檢查嗎？**  
A4：當然可以！本教學示範如何使用使用者提供的字典加強校正。

**Q5：我可以在哪裡取得 Aspose.OCR 的支援？**  
A5：請前往[Aspose.OCR 論壇](https://forum.aspose.com/c/ocr/16)尋求社群支援與指導。

---

**最後更新：** 2026-04-29  
**測試環境：** Aspose.OCR for .NET 最新版本  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}