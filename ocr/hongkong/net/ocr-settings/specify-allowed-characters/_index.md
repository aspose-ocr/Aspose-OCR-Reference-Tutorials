---
date: 2025-12-27
description: 學習如何使用 Aspose.OCR for .NET 進行 OCR 圖像轉文字，指定允許的字元並微調 OCR 識別設定。包括用於辨識數字圖像的程式碼。
linktitle: 'ocr image to text: Specify Allowed Characters in OCR'
second_title: Aspose.OCR .NET API
title: OCR 圖像轉文字：指定 OCR 可接受的字元
url: /zh-hant/net/ocr-settings/specify-allowed-characters/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ocr image to text：指定 OCR 允許的字符

## 簡介

在不斷演變的科技領域中，光學字符辨識（OCR）——或 **ocr image to text** 轉換——已成為一項變革性工具，使機器能夠從圖像中理解文字。Aspose.OCR for .NET 脫穎而出，作為強大的解決方案，為尋求在 .NET 應用程式中實現強大 OCR 功能的開發人員提供無縫整合。

## 快速回答
- **“Specify Allowed Characters” 的作用是什麼？** 它會將 OCR 輸出限制在一組定義好的符號，例如僅限數字。  
- **哪個方法會提取單行文字？** `RecognizeLine` 會返回它偵測到的第一行。  
- **我可以即時變更 OCR 辨識設定嗎？** 可以——使用 `RecognitionSettings` 來調整如 `AllowedCharacters` 等選項。  
- **是否提供試用版？** 當然，請從 Aspose 網站下載免費試用版。  
- **支援哪些 .NET 版本？** 所有現代的 .NET Framework 以及 .NET Core/5/6 版本。

## 先決條件

在深入本教學之前，請確保已具備以下先決條件：

- 具備 .NET 開發的實務知識。  
- Aspose.OCR for .NET 函式庫。您可在[此處](https://releases.aspose.com/ocr/net/)下載。  
- 熟悉 Visual Studio 或其他您偏好的 .NET 開發環境。

## 匯入命名空間

在您的 .NET 專案中，匯入必要的命名空間，以有效利用 Aspose.OCR for .NET 的功能：

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

現在，讓我們將教學分解為一系列完整的步驟：

## 步驟 1：在 ocr image to text 中指定允許的字符

首先，設定文件目錄的路徑：

```csharp
string dataDir = "Your Document Directory";
```

## 步驟 2：使用允許的符號初始化 Aspose.OCR（辨識數字圖像）

建立 `AsposeOcr` 的實例，指定允許的符號。本例中，我們僅允許數字 (0‑9)：

```csharp
AsposeOcr api = new AsposeOcr("0123456789");
```

## 步驟 3：辨識圖像

使用 `AsposeOcr` 實例從圖像中辨識文字：

```csharp
string result = api.RecognizeLine(dataDir + "0001460985.Jpeg");
```

## 步驟 4：顯示辨識文字

將辨識出的文字輸出至主控台：

```csharp
Console.WriteLine(result);
```

## 步驟 5：第二案例 – 使用特定 OCR 辨識設定辨識圖像

初始化另一個 `AsposeOcr` 實例，這次使用更具體的設定，以示範 **ocr recognition settings** 的用法：

```csharp
AsposeOcr api2 = new AsposeOcr();
RecognitionResult result2 = api2.RecognizeImage(dataDir + "0001460985.Jpeg", 
    new RecognitionSettings { 
        AllowedCharacters = CharactersAllowedType.DIGITS,
        RecognizeSingleLine = true
    });
```

## 步驟 6：顯示第二案例的辨識文字

將第二案例的辨識文字輸出至主控台：

```csharp
Console.WriteLine(result2.RecognitionText);
```

## 步驟 7：成功執行

最後，確認 **SpecifyAllowedCharacters** 教學已成功執行：

```csharp
Console.WriteLine("SpecifyAllowedCharacters executed successfully");
```

透過以上步驟，您已解鎖使用 Aspose.OCR for .NET 在 OCR 圖像辨識中 **指定允許的字符** 的功能，從而在僅限數字的情境下實現精確的 **ocr image to text** 轉換。

## 為何使用允許字符過濾？

- **更高的準確度：** 限制字符集可減少錯誤辨識，尤其在噪點較多的圖像中。  
- **效能提升：** OCR 引擎會跳過不相關的字形，加快處理速度。  
- **合規性：** 直接在 OCR 階段強制資料格式（例如發票號碼、序號）

## 常見陷阱與技巧

- **陷阱：** 為允許的字符提供空字串會停用過濾。  
  **技巧：** 必須傳入非空字串，或使用 `CharactersAllowedType` 列舉。  
- **陷阱：** 在多行文件上使用 `RecognizeLine` 可能遺漏資料。  
  **技巧：** 改用 `RecognizeImage` 並將 `RecognizeSingleLine = false`，以提取整頁內容。  
- **陷阱：** 未正確組合目錄路徑可能導致 `FileNotFoundException`。  
  **技巧：** 使用 `Path.Combine(dataDir, "file.jpg")` 以取得跨平台的路徑。

## 常見問題

**Q: Aspose.OCR for .NET 是否適合新手與有經驗的開發人員？**  
A: 當然！API 對新手直觀易用，同時也為進階使用者提供高階設定。

**Q: 我可以使用 Aspose.OCR for .NET 辨識多種語言的字符嗎？**  
A: 可以，Aspose.OCR 支援多種語言，亦可結合語言套件以應對多語言專案。

**Q: Aspose.OCR for .NET 更新頻率如何？**  
A: 會定期發布更新，以配合新的 .NET 版本與 OCR 改進。參閱[文件說明](https://reference.aspose.com/ocr/net/)以取得最新版本。

**Q: 是否提供 Aspose.OCR for .NET 的免費試用？**  
A: 有，您可透過下載[免費試用版](https://releases.aspose.com/)來體驗功能。

**Q: 我該到哪裡尋求協助或與社群聯繫？**  
A: 前往[Aspose.OCR 論壇](https://forum.aspose.com/c/ocr/16)與專家及其他開發者交流。

---

**最後更新：** 2025-12-27  
**測試環境：** Aspose.OCR 24.11 for .NET  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}