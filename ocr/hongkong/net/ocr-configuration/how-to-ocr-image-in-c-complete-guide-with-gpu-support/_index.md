---
category: general
date: 2026-01-09
description: 學習如何使用 Aspose.OCR 進行圖像 OCR 並提取圖像文字。包括將掃描文件轉換、啟用 GPU 以及使用 OCR 讀取圖像的步驟。
draft: false
keywords:
- how to ocr image
- extract image text
- convert scanned document
- how to enable gpu
- read image with ocr
language: zh-hant
og_description: 如何使用 Aspose.OCR 快速進行圖像 OCR。跟隨本步驟教學，提取圖像文字、轉換掃描文件，並啟用 GPU。
og_title: 如何在 C# 中進行圖像 OCR – GPU 加速指南
tags:
- OCR
- C#
- Aspose
- Image Processing
title: 如何在 C# 中對圖像進行光學字符辨識 – 完整的 GPU 支援指南
url: /zh-hant/net/ocr-configuration/how-to-ocr-image-in-c-complete-guide-with-gpu-support/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中進行影像 OCR – 完整指南（支援 GPU）

你是否曾好奇 **how to OCR image** 檔案如何直接從 .NET 應用程式中讀取？你並非唯一有此需求的開發者——開發者經常需要從 PDF、TIFF 與相片中擷取文字，尤其是處理大量掃描文件時。好消息是？使用 Aspose.OCR，你只需幾行程式碼即可 **extract image text**，甚至可以 **enable GPU** 加速以提升處理速度。

在本教學中，我們將逐步說明你需要了解的所有內容：從安裝函式庫、初始化具 GPU 後備機制的 OCR 引擎，到最終 **read image with OCR** 並顯示結果。完成後，你將能夠 **convert scanned document** 影像轉換為可編輯的字串——無需外部服務。

---

## 需要的條件

- **.NET 6.0** 或更新版本（此程式碼同樣適用於 .NET Core 與 .NET Framework）。
- 一個 **license** 給 Aspose.OCR 或暫時的評估金鑰（免費試用可用於測試）。
- 你想要處理的影像檔案——最好是高解析度的 TIFF 或 PNG。
- （可選）具備 GPU 的機器，如果你想看到效能提升；否則引擎會自動回退至 CPU。

具備上述前置條件，即可專注於實際的 OCR 工作流程，而不會在之後卡關。

---

## 步驟 1：安裝 Aspose.OCR NuGet 套件

首先，將 Aspose.OCR 函式庫加入你的專案。於解決方案資料夾開啟終端機並執行：

```bash
dotnet add package Aspose.OCR
```

或者，若你使用 Visual Studio 的 NuGet UI，只需搜尋 **Aspose.OCR** 並點擊安裝。此單一指令會下載所有必要的 DLL，包括可用時的原生 GPU 二進位檔。

> **專業提示：** 保持套件為最新版本。新版本通常會包含語言模型的改進與更好的 GPU 支援。

---

## 步驟 2：匯入必要的命名空間  

套件安裝完成後，將相關的命名空間引入範圍。這一步即是我們在程式碼中開始 **how to OCR image** 的地方。

```csharp
// Step 2: Import required namespaces
using Aspose.OCR;
using Aspose.OCR.Settings;
```

這兩行程式碼讓你可以存取 `OcrEngine` 類別以及可切換 GPU 使用的設定物件。若缺少它們，編譯器將無法辨識 `OcrEngine` 是什麼。

---

## 步驟 3：初始化 OCR 引擎並啟用 GPU  

如果你曾想過 **how to enable GPU** 用於 OCR，這就是答案。我們建立 `OcrEngineSettings` 實例，將 `UseGpu` 旗標打開，並將其傳入引擎建構子。引擎會自動偵測是否有相容的 GPU；若無，則回退至 CPU——因此不需要額外的錯誤處理。

```csharp
// Step 3: Initialize the OCR engine with GPU support (falls back to CPU if unavailable)
var ocrSettings = new OcrEngineSettings { UseGpu = true };
var ocrEngine   = new OcrEngine(ocrSettings);
```

為什麼要啟用 GPU？對於大型影像——例如多頁 TIFF 或高解析度掃描，處理時間可從數秒縮短至毫秒等級。若你在建構批次處理管線，這樣的效能提升會快速累積。

---

## 步驟 4：對目標影像執行 OCR  

這裡才是真正 **read image with OCR** 的地方。提供檔案路徑給引擎，即可取得辨識後的文字字串。此方式支援 Aspose 所支援的任何點陣圖格式（PNG、JPEG、TIFF、BMP 等）。

```csharp
// Step 4: Perform OCR on the target image file
string imagePath = @"C:\Images\large-document.tif";
string recognizedText = ocrEngine.RecognizeImage(imagePath);
```

若你需要 **convert scanned document** 頁面逐一處理，只要迴圈檔名並對每個檔案呼叫 `RecognizeImage` 即可。此方法為執行緒安全，你甚至可以在多核心 CPU 上平行化工作負載。

---

## 步驟 5：顯示或儲存擷取的文字  

最後，我們輸出結果。在主控台應用程式中，`Console.WriteLine` 即可完成。實務上，你可能會將文字寫入資料庫、JSON 檔，或送入搜尋索引。

```csharp
// Step 5: Display the extracted text
Console.WriteLine(recognizedText);
```

上述程式碼會印出原始的 OCR 輸出。你會看到換行、偶爾的錯誤辨識，甚至少量雜訊字元——這在 OCR 中屬於正常現象。若有需要，可透過後處理（例如正規表達式清理）來整理結果。

> **注意：** Aspose.OCR 亦支援語言特定的字典。若你處理非英文文字，請在呼叫 `RecognizeImage` 前適當設定 `ocrEngine.Settings.Language`。

---

## 完整範例  

將上述步驟整合起來，以下是一個可直接複製貼上至新主控台專案的完整程式：

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class Program
{
    static void Main()
    {
        // Initialize OCR engine with GPU support
        var ocrSettings = new OcrEngineSettings { UseGpu = true };
        var ocrEngine   = new OcrEngine(ocrSettings);

        // Path to the image you want to process
        string imagePath = @"C:\Images\large-document.tif";

        // Perform OCR
        string recognizedText = ocrEngine.RecognizeImage(imagePath);

        // Output the result
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(recognizedText);
    }
}
```

**預期輸出**（為簡潔起見已截斷）：

```
=== OCR Result ===
This is a sample scanned document.
It contains several lines of text that have been
converted from image to editable characters.
...
```

執行程式後，你應該會在主控台視窗看到擷取的文字。若 GPU 可用，處理時間將明顯比僅使用 CPU 的機器更短。

---

## 常見陷阱與避免方式  

| Issue | Why It Happens | Fix |
|-------|----------------|-----|
| **雜訊字元** | 低解析度來源或背景噪點。 | 在 OCR 前先前處理影像（提升 DPI、套用二值化）。 |
| **GPU 未使用** | 未安裝相容的 CUDA 驅動程式。 | 檢查驅動版本，或將 `UseGpu = false` 強制使用 CPU。 |
| **大型 TIFF 記憶體不足** | 一次載入整個檔案。 | 使用 `OcrEngineSettings.MaxMemoryUsage` 限制佔用，或逐頁處理。 |
| **語言偵測錯誤** | 預設語言為英文。 | 在呼叫 `RecognizeImage` 前設定 `ocrEngine.Settings.Language = Language.YourLanguage;`。 |

---

## 擴充解決方案  

既然你已能 **extract image text**，接下來可能想要：

- **Convert scanned document** PDF 轉換為可搜尋的 PDF，方法是嵌入 OCR 層。
- 將結果儲存於 **Azure Cognitive Search** 索引，以便快速檢索。
- 若需要多語言支援，將 OCR 輸出串接至 **translation API**。
- 使用 **Aspose.OCR** 的 `GetBoundingBoxes` 方法，找出每個單詞在影像上的位置——對於遮蔽工具相當便利。

所有這些擴充功能皆基於我們先前討論的核心原則：初始化引擎、提供影像，然後讀取文字。

---

## 結論  

我們已完整示範了在 C# 中使用 Aspose.OCR 進行 **how to OCR image** 的端對端範例。透過安裝 NuGet 套件、匯入正確的命名空間、啟用 GPU（或回退至 CPU），以及呼叫 `RecognizeImage`，你即可可靠地 **extract image text**、**convert scanned document** 頁面，並在任何 .NET 應用程式中 **read image with OCR**。

試著在幾張自己的掃描檔上執行——嘗試不同的影像格式、切換 GPU 旗標，觀察效能變化。當你準備好時，可探索語言字典或邊界框提取等進階功能，讓你的解決方案更聰明。

祝程式開發順利，願你的 OCR 流程快速、精確且無煩惱！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}