---
category: general
date: 2026-04-06
description: 如何在 C# 中使用 OCR 從 JPG 圖像提取純文字，包括西里爾字元。學習載入圖像進行 OCR、辨識 JPG 文字並獲得可靠的結果。
draft: false
keywords:
- how to use OCR
- extract plain text
- extract cyrillic text
- recognize text jpg
- load image for OCR
language: zh-hant
og_description: 如何在 C# 中使用 OCR 從 JPG 檔案提取純文字。本指南示範如何載入影像以進行 OCR、辨識 JPG 文字，以及處理西里爾文字。
og_title: 如何在 C# 中使用 OCR – 從圖像中提取純文字
tags:
- C#
- OCR
- Aspose
- Image Processing
title: 如何在 C# 中使用 OCR – 從圖像提取純文字
url: /zh-hant/net/text-recognition/how-to-use-ocr-in-c-extract-plain-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 OCR – 從圖像提取純文字

有沒有想過在 .NET 專案中 **如何使用 OCR**，卻不必與原生函式庫糾纏？也許你有一個掃描收據的資料夾、幾張帶有西里爾文字說明的螢幕截圖，或只是想快速從 JPEG 中提取文字進行分析。好消息是 Aspose OCR 讓整個流程變得輕而易舉。

在本教學中，我們將逐步示範一個完整、可執行的範例，說明 **如何使用 OCR** 來 **從 JPEG 圖像提取純文字**、**載入圖像以供 OCR**，甚至在來源語言不是拉丁字母時 **提取西里爾文字**。完成後，你將擁有一個小型主控台應用程式，直接在主控台印出辨識結果——不需要額外檔案，也不會產生神祕的副作用。

> **你將獲得**  
> * 可直接複製貼上到 Visual Studio 的一步步教學。  
> * 為何每一行程式碼重要的說明，而不只是它做了什麼。  
> * 處理大圖、 多語言以及常見陷阱的技巧。

## 前置條件

在開始之前，請確保你已具備：

* .NET 6 SDK 或更新版本（此程式碼同樣支援 .NET Core 與 .NET Framework）。  
* Visual Studio 2022（或任何你慣用的編輯器）。  
* 第一次執行範例時需要有網路連線——Aspose OCR 會即時下載語言套件。  

如果缺少 Aspose OCR NuGet 套件，我們會在第一步說明如何取得。

## 步驟 1 – 透過 NuGet 安裝 Aspose OCR（以及為何重要）

**載入圖像以供 OCR** 的步驟必須等到程式庫安裝完成後才能執行。使用 NuGet 能確保取得最新、已修補安全性的二進位檔，並自動帶入所有必要的相依性。

```bash
dotnet add package Aspose.OCR
```

*為何這很重要*：Aspose OCR 只隨附一個極小的核心 DLL，語言資料會在你需要時才下載。這樣可以讓應用程式保持輕量，避免打包大量未使用的語言檔案。

## 步驟 2 – 初始化 OCR 引擎（**如何使用 OCR** 的核心）

建立 `OcrEngine` 實例是 **如何使用 OCR** 的第一行關鍵程式碼。引擎預設為「即時下載」模式，意味著第一次請求特定語言時會自動下載相應的語言套件。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Step 2: Create the engine – it will fetch language data when needed.
var ocrEngine = new OcrEngine();
```

> **小技巧**：如果你身處企業代理伺服器後，請在第一次辨識呼叫前設定 `OcrEngine.Proxy`，以確保下載順利完成。

## 步驟 3 – 選擇語言 – 需要時 **提取西里爾文字**

Aspose OCR 支援數十種文字系統。若要 **提取西里爾文字**，只需將 `Language` 屬性設為 `OcrLanguage.Cyrillic`。首次執行此行程式碼時，西里爾模組（約 5 MB）會從 Aspose 的 CDN 下載。

```csharp
// Step 3: Tell the engine which language to look for.
// This will automatically download the Cyrillic language pack on first use.
ocrEngine.Language = OcrLanguage.Cyrillic;
```

如果你的圖像只包含拉丁字元，可以將 `Cyrillic` 換成 `English`。相同的寫法同樣適用於任何受支援的語言。

## 步驟 4 – **載入圖像以供 OCR** – 從磁碟或串流

現在我們真正 **載入圖像以供 OCR**。`System.Drawing.Image` 類別能處理大多數常見格式（JPG、PNG、BMP）。若在非 Windows 平台上執行，可考慮改用 `ImageSharp`，但本教學使用內建類型已足夠。

```csharp
using System.Drawing;

// Step 4: Load the picture that holds the text.
using var image = Image.FromFile(@"C:\Images\cyrillic_sample.jpg");
```

> **為何這很重要**：在 `using` 區塊內載入圖像，可確保非受控的 GDI+ 資源即時釋放，避免長時間執行的服務發生記憶體泄漏。

## 步驟 5 – **辨識 JPEG 文字** – 執行 OCR 程序

在引擎設定完成且圖像已載入後，我們終於 **辨識 JPEG 文字**。`Recognize` 方法會回傳一個 `OcrResult`，其中包含純文字字串、信心分數，甚至在需要時的邊界框資訊。

```csharp
// Step 5: Perform the recognition.
var ocrResult = ocrEngine.Recognize(image);
```

若想微調辨識精度，可調整 `ocrEngine.Config`（例如啟用 `AutoRotate` 或設定 `TextOrientation`）。對於大多數簡單情境，預設值已相當不錯。

## 步驟 6 – **提取純文字** – 顯示結果

**如何使用 OCR** 的最後一步是從 `ocrResult` 取出辨識出的字串並加以處理。此處我們直接寫入主控台，同時示範如何 **提取純文字** 從結果物件。

```csharp
// Step 6: Output the plain text to the console.
Console.WriteLine("=== Recognized Text ===");
Console.WriteLine(ocrResult.Text);
```

### 預期輸出

若 `cyrillic_sample.jpg` 內的文字為「Привет мир」（Hello world），應會看到：

```
=== Recognized Text ===
Привет мир
```

若圖像模糊或文字過小，輸出可能會有錯誤；你可以檢查 `ocrResult.Confidence` 以決定是否需要使用更高解析度的來源重新嘗試。

## 完整、可直接執行的範例

以下是完整程式碼。將它貼到新建的 Console App 專案（`dotnet new console`）中執行。除了指向的圖像檔外，無需其他檔案。

```csharp
// ---------------------------------------------------------------
// How to Use OCR in C# – Complete Example
// ---------------------------------------------------------------
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // 1️⃣ Install Aspose.OCR via NuGet first (dotnet add package Aspose.OCR)

        // 2️⃣ Initialize the OCR engine – on‑demand language download.
        var ocrEngine = new OcrEngine();

        // 3️⃣ Select Cyrillic to **extract Cyrillic text**.
        ocrEngine.Language = OcrLanguage.Cyrillic;

        // 4️⃣ **Load image for OCR** – change the path to your own file.
        using var image = Image.FromFile(@"YOUR_DIRECTORY\cyrillic_sample.jpg");

        // 5️⃣ **Recognize text jpg** – run the engine.
        var ocrResult = ocrEngine.Recognize(image);

        // 6️⃣ **Extract plain text** – display it.
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

> **注意**：將 `YOUR_DIRECTORY\cyrillic_sample.jpg` 替換為實際的 JPEG 檔案路徑。

## 常見問題與進階情境

### 若要 **辨識 JPEG 文字** 時改用串流而非檔案，該怎麼做？

直接將 `MemoryStream` 傳入：

```csharp
using var ms = new MemoryStream(File.ReadAllBytes("myImage.jpg"));
using var img = Image.FromStream(ms);
var result = ocrEngine.Recognize(img);
```

### 如何同時處理圖像中的多種語言？

將 `ocrEngine.Language` 設為 `OcrLanguage.Multilingual`。引擎會自動偵測每種文字系統，非常適合收據同時包含英文與西里爾文的情況。

```csharp
ocrEngine.Language = OcrLanguage.Multilingual;
```

### 我的圖像非常大（超過 5 MP），會不會卡住？

大型圖像會增加記憶體使用量並減慢辨識速度。先行縮小尺寸能有效改善效能：

```csharp
var resized = new Bitmap(image, new Size(image.Width / 2, image.Height / 2));
var result = ocrEngine.Recognize(resized);
```

### 能取得每行文字的信心分數嗎？

可以——`ocrResult.Lines` 包含每行的 `Confidence`。遍歷這些資訊即可過濾低信心的結果。

```csharp
foreach (var line in ocrResult.Lines)
{
    if (line.Confidence > 0.8)
        Console.WriteLine(line.Text);
}
```

## 生產環境 OCR 的專業建議

* **快取語言套件**——首次下載可能需要數秒，請將檔案存放於固定資料夾，並設定 `ocrEngine.LanguageDataPath` 以重複使用。  
* **批次處理**——對多張圖像重複使用同一個 `OcrEngine` 實例；為每個檔案重新建立引擎會增加不必要的開銷。  
* **錯誤處理**——將 `Recognize` 呼叫包在 try/catch 中。Aspose 會拋出 `OcrException` 以回報損毀的圖像或不支援的格式。  
* **日誌記錄**——記錄 `ocrResult.Confidence`，之後可用來稽核哪些頁面需要人工審核。

## 結論

我們剛剛示範了 **如何在 C# 中使用 OCR** 來 **從 JPEG 提取純文字**，說明了 **載入圖像以供 OCR** 的步驟，展示了 **辨識 JPEG 文字** 的流程，甚至成功 **提取西里爾文字**。此範例功能完整、僅需一個 NuGet 套件，且可擴充至多語言文件、批次作業或即時掃描情境。

準備好接受下一個挑戰了嗎？試著將語言換成阿拉伯文、實驗 `AutoRotate` 旗標，或把輸出整合至搜尋索引。可能性無限。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}