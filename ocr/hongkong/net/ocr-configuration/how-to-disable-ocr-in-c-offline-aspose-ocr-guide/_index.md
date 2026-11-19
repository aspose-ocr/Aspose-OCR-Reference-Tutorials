---
category: general
date: 2026-04-11
description: 學習如何在 Aspose OCR for C# 中停用 OCR，以離線執行、在無網路情況下從圖像提取文字，並正確載入圖像進行 OCR。
draft: false
keywords:
- how to disable OCR
- extract text from image
- load image for OCR
- offline OCR C#
- Aspose OCR resources
language: zh-hant
og_description: 如何在 Aspose OCR for C# 中停用 OCR 並離線執行，無需網路即可從圖像提取文字，並輕鬆載入圖像進行 OCR。
og_title: 如何在 C# 中停用 OCR – 離線 Aspose OCR 指南
tags:
- C#
- OCR
- Aspose
- Offline Processing
title: 如何在 C# 中停用 OCR – 離線 Aspose OCR 指南
url: /zh-hant/net/ocr-configuration/how-to-disable-ocr-in-c-offline-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中停用 OCR – 離線 Aspose OCR 指南

有沒有想過在需要徹底離線的情況下**如何停用 OCR**？也許你正在開發一個無法依賴網路連線的安全桌面應用程式，或只是想避免意外的下載。無論哪種情況，好消息是 Aspose OCR 允許你關閉自動資源下載，指向本機資料夾，讓所有資源都保留在本地。在本教學中，你還會看到如何**從影像檔案中擷取文字**以及正確**載入影像以進行 OCR**，全程不會出現問題。

我們將逐步示範一個完整、可直接執行的範例，從初始化引擎到輸出辨識出的日文文字。沒有外部文件、沒有隱藏的魔法；只有純粹的 C# 程式碼，你今天就能放入專案中使用。完成後，你將了解為何停用自動下載功能很重要、如何設定資源路徑，以及需要留意哪些陷阱。

## 前置條件

- .NET 6.0（或任何較新的 .NET 版本）已安裝於你的機器上。  
- Aspose.OCR for .NET NuGet 套件（`Install-Package Aspose.OCR`）。  
- 一個已經包含所需語言資源的資料夾（例如日文模型）。  
- 一個想要執行 OCR 的影像檔（`japan_doc.png`）。  

如果缺少語言套件，請從 Aspose 入口網站下載一次，解壓縮到類似 `AsposeOCRResources` 的資料夾，即可完成設定。停用自動下載功能後，將不會再有任何下載發生。

![如何離線停用 OCR](/images/how-to-disable-ocr.png "如何停用 OCR 示意圖")

## 步驟 1 – 建立 OCR 引擎實例  

首先要做的事是實例化 `OcrEngine`。可以把這個物件想像成讀取影像的“大腦”。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class OfflineDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

> **為何重要：** 沒有引擎就無法進行任何設定。此物件保存所有設定，包括告訴函式庫是否可以連上網路的關鍵旗標。

## 步驟 2 – 停用自動資源下載  

預設情況下，Aspose OCR 會即時嘗試下載缺少的語言檔案。為了保持離線，將 `AutoDownloadResources` 開關設為 `false`。

```csharp
        // Step 2: Disable automatic resource download to work offline
        ocrEngine.Settings.AutoDownloadResources = false;
```

> **專業提示：** 關閉此功能不僅確保隱私，還能加快首次辨識的速度，因為引擎不會浪費時間檢查更新。

## 步驟 3 – 指向本機資源資料夾  

現在告訴引擎預先下載好的語言套件所在的位置。這就是在前置條件中設定的路徑。

```csharp
        // Step 3: Point the engine to the folder containing pre‑downloaded resources
        ocrEngine.Settings.ResourcesPath = @"YOUR_DIRECTORY/AsposeOCRResources";
```

> **可能會發生什麼問題？** 若路徑錯誤或缺少必要的語言檔案，引擎會拋出 `ResourceNotFoundException`。請再次確認資料夾名稱正確，且日文模型（`jpn.traineddata`）已存在。

## 步驟 4 – 選取本機語言模型  

選擇實際已在磁碟上的語言模型。在本例中我們使用日文，但你可以將 `Language.Japanese` 替換為任何已下載的其他語言。

```csharp
        // Step 4: Select the language model that is available locally
        ocrEngine.Settings.Language = Language.Japanese;
```

> **特殊情況：** 某些語言需要額外的字典（例如中文）。請確保這些輔助檔案也放在同一資源資料夾內。

## 步驟 5 – 載入影像以進行 OCR  

這裡是我們**載入影像以進行 OCR**的地方。`ImageStream.FromFile` 方法會將檔案讀入 Aspose 可處理的串流。

```csharp
        // Step 5: Load the image you want to recognize
        ImageStream image = ImageStream.FromFile(@"YOUR_DIRECTORY/japan_doc.png");
```

> **提示：** 支援的格式包括 PNG、JPEG、BMP 與 TIFF。若需處理 PDF，請先將每頁轉為影像。

## 步驟 6 – 執行辨識程序  

現在引擎會實際讀取像素，並嘗試將其轉換為文字。

```csharp
        // Step 6: Run the OCR process
        OcrResult ocrResult = ocrEngine.Recognize(image);
```

> **為何此步驟可能較慢：** OCR 需要大量 CPU，尤其是高解析度影像。若在意效能，可考慮在辨識前先縮小影像尺寸。

## 步驟 7 – 輸出擷取的文字  

最後，我們**從影像中擷取文字**並將其印到主控台。

```csharp
        // Step 7: Output the recognized text
        Console.WriteLine(ocrResult.Text);
    }
}
```

執行程式後，應會顯示 `japan_doc.png` 中的日文字符。若設定正確，主控台上會看到一段乾淨的 Unicode 文字區塊。

### 預期輸出

```
これはサンプルの日本語テキストです。
```

（實際輸出會依影像內容而異。）

## 常見陷阱與避免方法  

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **缺少語言檔案** | `AutoDownloadResources` 為 false，導致引擎無法下載檔案。 | 確認 `ResourcesPath` 指向包含 `jpn.traineddata` 的資料夾。 |
| **影像路徑不正確** | `ImageStream.FromFile` 拋出 `FileNotFoundException`。 | 使用絕對路徑或確保工作目錄設定正確。 |
| **不支援的影像格式** | Aspose 只支援特定的影像格式。 | 在呼叫 `FromFile` 前將影像轉為 PNG 或 JPEG。 |
| **大型影像導致記憶體不足** | OCR 會將整張影像載入記憶體。 | 調整影像大小或分割影像，或提升程式的記憶體上限。 |

## 擴充範例  

- **批次處理：** 迭代目錄中的影像，呼叫相同的辨識程式，並將每個結果寫入獨立的 `.txt` 檔案。  
- **不同語言：** 在放置相應資源檔後，將 `Language.Japanese` 替換為 `Language.English`（或其他語言）。  
- **自訂前處理：** 使用 Aspose.Imaging 在 OCR 前進行去斜或提升對比度，以獲得更高的辨識準確度。  

## 結論  

現在你已了解如何在 Aspose OCR for C# 中**停用 OCR**，並完全離線執行。只要將 `AutoDownloadResources` 設為 `false`、指向本機資源資料夾，並正確**載入影像以進行 OCR**，就能可靠地**從影像中擷取文字**，而不會連接到網路。此方式非常適合安全環境、CI 流程或任何網路存取受限的情境。

準備好下一步了嗎？試著處理整個掃描 PDF 資料夾、實驗不同的語言套件，或將 OCR 結果整合至可搜尋的資料庫。你今天建立的離線設定，是任何本地文件處理工作流程的堅實基礎。

祝程式開發順利，如有任何問題，歡迎留下評論！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}