---
category: general
date: 2026-03-07
description: 學習如何在 C# 中使用 OCR 從圖像檔案提取文字。本指南展示離線 OCR、將圖像轉換為文字，以及載入圖像進行 OCR。
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from png
- convert image to text
- load image for ocr
language: zh-hant
og_description: 如何在 C# 中使用 OCR 離線提取圖像文字。逐步程式碼、技巧與完整說明，教您將圖像轉換為文字。
og_title: 如何在 C# 中使用 OCR – 完整離線指南
tags:
- OCR
- C#
- Aspose
title: 如何在 C# 中使用 OCR – 離線從圖片提取文字
url: /zh-hant/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-images-offline/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 OCR – 離線從圖像提取文字

有沒有想過 **如何在 .NET 專案中使用 OCR** 而不將資料傳送到雲端？你並不孤單。許多開發人員需要在受保護的工作站上 *從圖像檔案提取文字*，且擔心網路流量會洩露敏感資訊。  

好消息是？使用 Aspose.OCR，你可以完全離線辨識 PNG、JPEG 或 PDF 中的文字。在本教學中，我們將逐步說明如何載入圖像進行 OCR、設定離線模式的引擎，最後只需幾行 C# 程式碼即可 **將圖像轉換為文字**。

在本指南結束時，你將能夠：

* 安裝 Aspose.OCR NuGet 套件。  
* 設定 OCR 引擎以進行離線處理。  
* 載入圖像進行 OCR 並提取其文字內容。  

無需外部服務、無需 API 金鑰——只需純粹的 C# 程式碼，即可在任何 Windows 或 Linux 機器上執行。

---

## 前置條件

在開始之前，請確保你已具備：

* .NET 6.0 SDK 或更新版本（此程式碼同樣支援 .NET Framework 4.7 以上）。  
* Visual Studio 2022、VS Code，或任何支援 C# 的編輯器。  
* **Aspose.OCR** 函式庫的副本——可從 NuGet 取得（`Aspose.OCR`）。  
* 隨函式庫一起提供的 OCR 資源資料夾（`Resources`），內含語言資料檔。  
* 一張範例圖像（例如 `offline_test.png`），放置於已知目錄中。

> **專業提示：** 將資源資料夾放在可執行檔旁邊；這樣可簡化 `ResourcesPath` 的設定。

## 步驟 1：安裝 Aspose.OCR NuGet 套件

首先，將函式庫加入你的專案。於專案資料夾中開啟終端機並執行：

```bash
dotnet add package Aspose.OCR
```

或者，若你偏好使用 Visual Studio 介面，右鍵點選 **Dependencies → Manage NuGet Packages**，搜尋 *Aspose.OCR*，然後點擊 **Install**。

> 安裝套件會自動下載所有必要的二進位檔，無需額外的 DLL。

## 步驟 2：建立並設定 OCR 引擎（如何使用 OCR – 離線模式）

現在我們將實例化 OCR 引擎，並指示它以 **離線** 方式運作。這可確保辨識過程中不會產生任何網路流量。

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

// Initialize the OCR engine
var ocrEngine = new OcrEngine();

// Switch the engine to offline mode – crucial for privacy‑first apps
ocrEngine.Settings.EngineMode = EngineMode.Offline;
```

**為什麼要離線？**  
當 `EngineMode` 設為 `Online` 時，引擎會連線至 Aspose 雲端即時下載語言套件。在受管制的環境（金融、醫療）中，此類流量通常被禁止。強制使用離線模式即可確保所有資料皆留在本機。

## 步驟 3：將引擎指向 OCR 資源資料夾

OCR 引擎需要語言資料（訓練模型）才能辨識字元。請告訴它這些檔案所在的位置：

```csharp
// Replace with the absolute or relative path to your Resources folder
ocrEngine.Settings.ResourcesPath = @"C:\MyProject\Resources";
```

如果不確定資料夾位置，可在 NuGet 套件目錄下找到（`%USERPROFILE%\.nuget\packages\aspose.ocr\*\resources`）。將整個資料夾複製到你的專案中，以便更輕鬆部署。

## 步驟 4：載入圖像以進行 OCR（Load Image for OCR）

你可以將任何支援的位圖提供給引擎。此處我們將載入磁碟上的 PNG 圖像：

```csharp
// Load the image you want to recognize – this is the “load image for OCR” step
ocrEngine.Image = ImageStream.FromFile(@"C:\MyProject\offline_test.png");
```

**提示：** 若需從串流處理圖像（例如透過 API 上傳），請改用 `ImageStream.FromStream(yourStream)`。

## 步驟 5：執行辨識程序並將圖像轉換為文字

所有設定完成後，啟動 OCR。`Recognize()` 方法負責主要的辨識工作，提取出的文字可透過 `Text` 屬性取得。

```csharp
// Perform OCR – this is where the engine reads the pixels and produces text
ocrEngine.Recognize();

// Grab the result – now you have “convert image to text” completed
string extractedText = ocrEngine.Text;
```

## 步驟 6：輸出提取的文字

最後，顯示結果。在主控台應用程式中只需寫入主控台；若是 Web API，則可將字串作為 JSON 回傳。

```csharp
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(extractedText);
```

執行程式後應會印出 `offline_test.png` 的文字內容。例如，若圖像包含字句 *“Hello, World!”*，則會看到：

```
=== OCR Result ===
Hello, World!
```

## 完整範例程式

以下是完整、可直接執行的程式。將其複製貼上至新建的主控台專案（`dotnet new console`），並依你的環境調整路徑。

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Initialize OCR engine
        // -------------------------------------------------
        var ocrEngine = new OcrEngine();

        // -------------------------------------------------
        // Step 2: Set offline mode – no network traffic
        // -------------------------------------------------
        ocrEngine.Settings.EngineMode = EngineMode.Offline;

        // -------------------------------------------------
        // Step 3: Provide path to OCR resource files
        // -------------------------------------------------
        ocrEngine.Settings.ResourcesPath = @"C:\MyProject\Resources";

        // -------------------------------------------------
        // Step 4: Load the image you want to recognize
        // -------------------------------------------------
        ocrEngine.Image = ImageStream.FromFile(@"C:\MyProject\offline_test.png");

        // -------------------------------------------------
        // Step 5: Run recognition and extract text
        // -------------------------------------------------
        ocrEngine.Recognize();
        string extractedText = ocrEngine.Text;

        // -------------------------------------------------
        // Step 6: Show the result
        // -------------------------------------------------
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(extractedText);
    }
}
```

> **預期輸出：** 主控台會印出 PNG 檔案中完整的文字。若圖像模糊，結果可能包含辨識錯誤的字元——請參閱下方的故障排除章節。

## 常見問題與技巧（有效辨識 PNG 文字）

| 問題 | 為什麼會發生 | 如何解決 |
|------|--------------|----------|
| **輸出為空** | ResourcesPath 指向錯誤的資料夾或缺少語言檔案。 | 確認資料夾內含 `eng.traineddata`（或其他語言檔案），並再次檢查路徑字串。 |
| **雜訊字元** | 圖像解析度過低或未進行二值化。 | 預先處理圖像（提升 DPI，使用 `ImageProcessor` 銳化）。 |
| **效能延遲** | 大型圖像以完整解析度處理。 | 在送入 OCR 前將圖像大小調整至最大寬度 2000 px。 |
| **不支援的格式** | 使用了具有不尋常像素格式的 BMP。 | 先將圖像轉為 PNG 或 JPEG（`System.Drawing.Image.Save`）。 |

**專業提示：** 若需辨識多種語言，請在呼叫 `Recognize()` 前設定 `ocrEngine.Settings.Language = Language.English | Language.French;`。

## 常見問答

**問：我可以在 Linux 上使用這段程式碼嗎？**  
當然可以。Aspose.OCR 為跨平台套件，只要確保本機已包含原生函式庫（已隨 NuGet 套件一起打包）。

**問：如果我沒有 Resources 資料夾該怎麼辦？**  
你可以從 Aspose 官方網站下載免費語言套件，或從 NuGet 套件中解壓取得（`.../aspose.ocr/<version>/resources`）。

**問：有辦法取得信心分數嗎？**  
有的。呼叫 `Recognize()` 後，檢查 `ocrEngine.RecognizedWords`——每個單字都包含 `Confidence` 屬性。

## 結論

我們已說明 **如何在 C# 中使用 OCR** 完全離線 *從圖像檔案提取文字*。只要安裝 Aspose.OCR、將 `EngineMode` 設為 `Offline`、指向資源資料夾、載入圖像，並呼叫 `Recognize()`，即可可靠地 **將圖像轉換為文字**，且全程不需連網。

使用上述程式碼，替換成自己的圖像路徑，即可開始開發可搜尋的 PDF、資料輸入自動化或無障礙工具等功能。接下來，你可以探索批次 **辨識 PNG 文字**，或將引擎整合至 ASP.NET Core API，為前端應用提供 OCR 結果。

祝開發順利，盡情嘗試吧——只要正確設定引擎，OCR 的容錯度相當高！

![顯示離線 OCR 工作流程的圖示 – 如何在安全環境中使用 OCR](https://example.com/ocr-workflow.png "如何使用 OCR 圖示")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}