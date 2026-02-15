---
description: 學習如何使用 Aspose.OCR for .NET 指定允許的 OCR 字元，並有效辨識數字圖像。跟隨一步一步的指南，將 OCR 限制僅辨識數字。
linktitle: Specify Allowed Characters OCR – Using Aspose.OCR for .NET
second_title: Aspose.OCR .NET API
title: 指定允許字元 OCR – 使用 Aspose.OCR for .NET
url: /zh-hant/net/ocr-settings/specify-allowed-characters/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 指定允許字元 OCR – 使用 Aspose.OCR for .NET

在本教學中，您將學習如何使用 Aspose.OCR for .NET **specify allowed characters ocr**，以限制 OCR 輸出僅包含您需要的字元。當您需要 **recognize digits image** 檔案（例如序號、發票編號或類似條碼的字串）時，這特別方便。我們將逐步說明設定、程式碼以及幾個實務情境，讓您立即套用此技巧。

## 快速解答
- **What does “specify allowed characters ocr” do?** 它會將 OCR 限制在預先定義的字元集合中，提高針對性資料的辨識準確度。  
- **Which characters can I allow?** 您可以允許任何需要的組合——數字、字母或自訂符號（例如 “0123456789”）。  
- **Why limit characters?** 限制字元可減少錯誤辨識，且在已知預期字元集時加快處理速度。  
- **Do I need a license?** 開發時可使用免費試用版；正式上線則需購買商業授權。  
- **Which .NET versions are supported?** .NET Framework 4.5+、.NET Core 3.1+、.NET 5/6/7 均受支援。

## 「specify allowed characters ocr」是什麼？
當 OCR 掃描影像時，會嘗試將每個視覺模式對應到完整的可能字元表。透過 **specify allowed characters ocr**，您可告訴引擎忽略白名單之外的所有字元，從而大幅提升在受限資料集上的辨識準確度。

## 為何使用 Aspose.OCR 來辨識 digits image？
Aspose.OCR 為 .NET 開發者提供簡潔、流暢的 API。其內建的 `AllowedCharacters` 選項讓您在僅需數字的情境下，無需自行撰寫後處理程式碼。這非常適用於：
- 讀取儀表讀數、發票號碼或產品代碼。  
- 驗證從掃描表單取得的使用者輸入資料。  
- 加速批次處理，因為字元集事先已知。

## 前置條件

在深入程式碼之前，請確保您已具備：

- 具備 .NET 開發的實務知識。  
- **Aspose.OCR for .NET** 函式庫。您可從 [here](https://releases.aspose.com/ocr/net/) 下載。  
- Visual Studio（或任何您偏好的 .NET IDE）。  

## 匯入命名空間

在您的 .NET 專案中，匯入必要的命名空間以使用 Aspose.OCR 功能：

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

現在，讓我們將本教學分解為一系列完整的步驟：

## 如何指定允許字元 OCR – 步驟說明

### 步驟 1：設定影像資料夾的路徑

首先，定義您的範例影像儲存位置。

```csharp
string dataDir = "Your Document Directory";
```

### 步驟 2：以僅限數字的白名單初始化 Aspose.OCR

建立 `AsposeOcr` 實例，並傳入您想允許的字元——此例為全部數字。

```csharp
AsposeOcr api = new AsposeOcr("0123456789");
```

### 步驟 3：辨識包含數字的單行文字

使用 `RecognizeLine` 方法，從僅含數字的影像中擷取文字。

```csharp
string result = api.RecognizeLine(dataDir + "0001460985.Jpeg");
```

### 步驟 4：輸出辨識出的數字

將結果印至主控台，以便驗證輸出。

```csharp
Console.WriteLine(result);
```

### 步驟 5：使用 RecognitionSettings 取得更多控制

若需更細緻的控制（例如強制單行辨識），可使用接受 `RecognitionSettings` 的重載方法。

```csharp
AsposeOcr api2 = new AsposeOcr();
RecognitionResult result2 = api2.RecognizeImage(dataDir + "0001460985.Jpeg", 
    new RecognitionSettings { 
        AllowedCharacters = CharactersAllowedType.DIGITS,
        RecognizeSingleLine = true
    });
```

### 步驟 6：顯示第二個案例的結果

```csharp
Console.WriteLine(result2.RecognitionText);
```

### 步驟 7：確認執行成功

```csharp
Console.WriteLine("SpecifyAllowedCharacters executed successfully");
```

透過上述步驟，您已學會如何 **specify allowed characters ocr**，並使用 Aspose.OCR for .NET 高效地 **recognize digits image** 內容。

## 常見問題與除錯
- **Empty result:** 確保影像品質足夠（對比清晰、雜訊最少）。  
- **Wrong characters returned:** 再次確認白名單字串與您預期的字元完全相符。  
- **File not found:** 確認 `dataDir` 指向正確的資料夾，且檔名大小寫正確。  

## 常見問答

### Q1: Aspose.OCR for .NET 是否適合新手與有經驗的開發者？
**A:** 當然！此 API 設計直觀，適合新手使用，同時也提供進階選項給進階使用者。

### Q2: 我可以使用 Aspose.OCR for .NET 辨識多語言的字元嗎？
**A:** 可以，Aspose.OCR 支援多種語言。您可將語言套件與 allowed‑characters 功能結合，以應對多語言情境。

### Q3: Aspose.OCR for .NET 多久會更新一次？
**A:** 會定期發布更新，新增功能、提升準確度並確保相容性。請參考 [documentation](https://reference.aspose.com/ocr/net/) 取得最新版本資訊。

### Q4: 是否提供 Aspose.OCR for .NET 的免費試用？
**A:** 有，您可下載 [free trial](https://releases.aspose.com/) 以體驗功能。

### Q5: 我該去哪裡尋求協助或與社群聯繫？
**A:** 前往 [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) 提問、分享經驗，並獲得 Aspose 工程師與其他開發者的協助。

---

**最後更新：** 2026-02-15  
**測試環境：** Aspose.OCR 24.11 for .NET  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}