---
date: 2026-05-24
description: 了解如何透過在 Aspose.OCR for .NET 中設定允許的字元來提升 OCR，從而實現精確的數字辨識與更快的處理速度。請跟隨一步一步的指南。
keywords:
- how to improve ocr
- set allowed characters
- recognize digits
- improve ocr accuracy
- extract serial numbers
linktitle: 如何提升 OCR – 使用 Aspose.OCR for .NET 設定允許的字元
schemas:
- author: Aspose
  dateModified: '2026-05-24'
  description: Learn how to improve OCR by setting allowed characters with Aspose.OCR
    for .NET, enabling accurate digit recognition and faster processing. Follow a
    step‑by‑step guide.
  headline: How to Improve OCR – Set Allowed Characters with Aspose.OCR for .NET
  type: TechArticle
- description: Learn how to improve OCR by setting allowed characters with Aspose.OCR
    for .NET, enabling accurate digit recognition and faster processing. Follow a
    step‑by‑step guide.
  name: How to Improve OCR – Set Allowed Characters with Aspose.OCR for .NET
  steps:
  - name: Set the path to your image folder
    text: Define the folder that contains the sample images you want to process.
  - name: Initialize Aspose.OCR with a digit‑only whitelist
    text: '`AllowedCharacters` is a property that sets the whitelist of characters
      the OCR engine may recognize.'
  - name: Recognize a single line containing digits
    text: The `RecognizeLine` method scans the image and returns the best‑matching
      line that conforms to the whitelist.
  - name: Output the recognized digits
    text: Write the result to the console (or log) so you can verify the output instantly.
  - name: Use `RecognitionSettings` for more control
    text: '`RecognitionSettings` allows you to customize OCR parameters such as DPI,
      language packs, and processing mode.'
  - name: Confirm successful execution
    text: By following these steps, you’ve learned **how to improve OCR** accuracy
      by limiting the character set, and you can now reliably extract digit strings
      from images using Aspose.OCR for .NET.
  type: HowTo
- questions:
  - answer: It limits OCR to a predefined whitelist, dramatically increasing accuracy
      for targeted data sets.
    question: What does “specify allowed characters OCR” do?
  - answer: Any combination you need—digits (`0‑9`), uppercase letters, custom symbols,
      or a mix like “ABC‑123”.
    question: Which characters can I allow?
  - answer: Whitelisting reduces false recognitions by up to 70 % and speeds up processing
      by 30 % on average.
    question: Why limit characters?
  - answer: A free trial works for development; a commercial license is required for
      production deployments.
    question: Do I need a license?
  - answer: .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.
    question: Which .NET versions are supported?
  type: FAQPage
second_title: Aspose.OCR .NET API
title: 如何提升 OCR – 使用 Aspose.OCR for .NET 設定允許的字元
url: /zh-hant/net/ocr-settings/specify-allowed-characters/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何提升 OCR – 使用 Aspose.OCR for .NET 設定允許的字元

在本教學中，您將學會 **如何透過指定允許的字元** 來提升 Aspose.OCR for .NET 的 OCR 結果。將 OCR 引擎限制在已知的白名單（例如僅限數字）可提升準確度、縮短處理時間，並排除不需要的符號。無論是擷取序號、發票編號或電表讀數，以下步驟皆可在數分鐘內完成此技巧的應用。

## 快速解答
- **「指定允許字元 OCR」的作用是什麼？** 它將 OCR 限制在預先定義的白名單上，顯著提升針對特定資料集的準確度。  
- **我可以允許哪些字元？** 任何您需要的組合——數字 (`0‑9`)、大寫字母、自訂符號，或像「ABC‑123」這樣的混合。  
- **為什麼要限制字元？** 白名單可將錯誤辨識率降低最高 70 %，同時平均提升處理速度 30 %。  
- **需要授權嗎？** 免費試用可用於開發；商業授權則需於正式上線時取得。  
- **支援哪些 .NET 版本？** .NET Framework 4.5+、.NET Core 3.1+、.NET 5/6/7。  
- **可以與語言套件結合使用嗎？** 可以——將白名單與語言套件搭配，即可處理多語系的數字字串。

## 什麼是「指定允許字元 OCR」？

**直接回答：** 指定允許字元即告訴 Aspose.OCR 只接受您列出的字元，忽略所有不符合的視覺模式，讓引擎僅回傳白名單內的結果。此聚焦方式可消除雜訊、提升信心分數，並減少後續處理的工作量，同時加速辨識流程。

## 為何使用 Aspose.OCR 來辨識數字影像？

**直接回答：** Aspose.OCR 內建的 `AllowedCharacters` 功能只需一行程式碼即可辨識僅含數字的影像，在低解析度掃描下可達到 95 % 的準確率，且不需額外過濾邏輯。此函式庫支援超過 30 種語言，能在每頁低於 2 秒的時間內處理 500 頁影像批次，且完全離線執行，非常適合高吞吐量、內部部署的情境，如公用事業表計讀取或發票編號擷取。

## 前置條件

在開始之前，請確保您已具備：

- 基本的 .NET 開發經驗。  
- **Aspose.OCR for .NET** 函式庫 – 從官方網站 **[此處](https://releases.aspose.com/ocr/net/)** 下載。  
- Visual Studio 2019+（或任何相容的 .NET IDE）。  

## 匯入命名空間

以下命名空間可讓您存取 OCR 引擎及其設定：

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

## 如何透過指定允許字元來提升 OCR？

`AsposeOcr` 為 Aspose.OCR 函式庫提供的主要 OCR 引擎類別。  
`RecognizeLine` 會從影像中處理單行文字並回傳辨識結果。

**直接回答：** 載入影像、以僅限數字的白名單（`"0123456789"`）建立 `AsposeOcr` 實例、呼叫 `RecognizeLine`（多行則使用 `Recognize`），最後從結果的 `Text` 屬性取得文字。此三步流程可在一般 300 dpi 影像下於一秒內產出乾淨的數字字串。

### 步驟 1：設定影像資料夾的路徑

定義包含您要處理的樣本影像的資料夾。

```csharp
string dataDir = "Your Document Directory";
```

### 步驟 2：以僅限數字的白名單初始化 Aspose.OCR

`AllowedCharacters` 為屬性，可設定 OCR 引擎允許辨識的字元白名單。

```csharp
AsposeOcr api = new AsposeOcr("0123456789");
```

### 步驟 3：辨識包含數字的單行文字

`RecognizeLine` 方法會掃描影像，回傳符合白名單的最佳匹配行。

```csharp
string result = api.RecognizeLine(dataDir + "0001460985.Jpeg");
```

### 步驟 4：輸出辨識出的數字

將結果寫入主控台（或日誌），即可即時驗證輸出。

```csharp
Console.WriteLine(result);
```

### 步驟 5：使用 `RecognitionSettings` 取得更多控制

`RecognitionSettings` 允許您自訂 DPI、語言套件、處理模式等 OCR 參數。

```csharp
AsposeOcr api2 = new AsposeOcr();
RecognitionResult result2 = api2.RecognizeImage(dataDir + "0001460985.Jpeg", 
    new RecognitionSettings { 
        AllowedCharacters = CharactersAllowedType.DIGITS,
        RecognizeSingleLine = true
    });
```

### 步驟 6：顯示第二種情境的結果

```csharp
Console.WriteLine(result2.RecognitionText);
```

### 步驟 7：確認執行成功

```csharp
Console.WriteLine("SpecifyAllowedCharacters executed successfully");
```

透過上述步驟，您已學會 **如何透過限制字元集** 來提升 OCR 準確度，現在可以可靠地使用 Aspose.OCR for .NET 從影像中擷取數字字串。

## 常見問題與除錯

- **結果為空白：** 確認影像對比度清晰且背景噪點最少；建議最低 300 dpi。  
- **出現非預期字元：** 再次檢查白名單字串，額外的空格或不可見字元會破壞過濾。  
- **找不到檔案：** 確認 `dataDir` 指向正確資料夾，且檔名符合大小寫敏感的檔案系統。  
- **效能下降：** 大批次處理時，請重複使用同一個 `AsposeOcr` 實例，而非每張影像都重新建立。

## 常見問答

### Q1：Aspose.OCR for .NET 是否適合新手與有經驗的開發者？
**A：** 絕對適合。API 提供單行程式碼的快速設定，也提供進階的 `RecognitionSettings` 供進階使用者客製化，涵蓋所有技術層級。

### Q2：在使用允許字元白名單時，能同時辨識多語系字元嗎？
**A：** 可以。載入相應的語言套件（例如 `ocrEngine.LoadLanguage("en")`），再結合如 `"0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ"` 的白名單，即可處理多語系的數字字串。

### Q3：Aspose.OCR for .NET 的更新頻率如何？
**A：** 大約每 6‑8 週發布一次新版本，加入語言支援、效能優化與錯誤修正。最新資訊請參考 [文件說明](https://reference.aspose.com/ocr/net/)。

### Q4：是否提供免費試用？
**A：** 有——可下載 **[免費試用版](https://releases.aspose.com/)** 以評估全部功能。正式上線須購買商業授權。

### Q5：我可以在哪裡取得社群協助或官方支援？
**A：** 加入活躍的 **[Aspose.OCR 論壇](https://forum.aspose.com/c/ocr/16)**，在那裡您可以提問、分享程式碼片段，並獲得 Aspose 工程師的指導。

---

**最後更新：** 2026-05-24  
**測試環境：** Aspose.OCR 24.11 for .NET  
**作者：** Aspose

## 相關教學

- [OCR Image Recognition Settings - Specify Ignored Characters](/ocr/net/ocr-settings/specify-ignored-characters/)
- [Preprocess Image OCR with Aspose.OCR Filters for .NET](/ocr/net/ocr-optimization/preprocessing-filters-for-image/)
- [How to Set Threshold Value in OCR Image Recognition](/ocr/net/ocr-settings/set-threshold-value/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}