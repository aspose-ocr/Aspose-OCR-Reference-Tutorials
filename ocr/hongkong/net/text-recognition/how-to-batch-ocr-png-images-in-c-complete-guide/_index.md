---
category: general
date: 2026-03-17
description: 如何在 C# 中快速批次 OCR PNG 圖像。學習提取 PNG 檔案中的文字、將 PNG 轉換為文字，並使用簡單腳本從資料夾讀取圖像。
draft: false
keywords:
- how to batch OCR
- extract text png
- convert png to text
- read images from directory
language: zh-hant
og_description: 如何在 C# 中使用逐步程式碼批次 OCR PNG 圖片。提取 PNG 檔案文字、將 PNG 轉換為文字，並輕鬆從目錄讀取圖像。
og_title: 如何在 C# 中批量 OCR PNG 圖片 – 完整指南
tags:
- OCR
- C#
- Image Processing
title: 如何在 C# 中批次 OCR PNG 圖像 – 完整指南
url: /zh-hant/net/text-recognition/how-to-batch-ocr-png-images-in-c-complete-guide/
---

produce final content with translations.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中批量 OCR PNG 圖像 – 完整指南

有沒有想過 **如何批量 OCR** 一個充滿螢幕截圖的資料夾，而不必手動開啟每個檔案？你並不是唯一的——開發者常常詢問如何批量 OCR 大量 PNG，特別是當目標是提取文字 PNG 檔案以供後續分析時。  

在本教學中，我們將逐步說明一個可直接執行的 C# 範例，該範例 **提取文字 PNG** 檔案、**將 PNG 轉換為文字**，並向你展示最佳的 **從目錄讀取圖像** 方法。完成後，你將擁有一個腳本，會在每張圖像旁產生相應的 `.txt`，為你節省數小時的手動複製貼上。

## 你將達成的目標

- 初始化一次 OCR 引擎，並在整個批次中重複使用。  
- 在指定資料夾中掃描每個 `*.png`，無需自行撰寫迴圈。  
- 將每個 OCR 結果寫入各自的文字檔，保留原始檔名。  
- 優雅地處理常見的例外情況，如空資料夾或非圖像檔案。

### 前置條件

- .NET 6.0 或更新版本（此程式碼同樣適用於 .NET Core 與 .NET Framework）。  
- 提供 `OcrEngine`、`ImageStream` 與 `OcrResult` 類型的 OCR 函式庫（例如本範例中使用的虛構 **FastOCR** SDK）。  
- 基本的 C# 知識——不需要進階模式。

---

## 如何批量 OCR PNG 圖像 – 概觀

以下是 **完整、可執行的程式**。請隨意將其複製貼上至新的 Console 專案，替換佔位路徑，然後按下 **F5**。

```csharp
using System;
using System.IO;
using System.Linq;
using FastOCR;               // <-- Replace with your actual OCR namespace

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Initialize the OCR engine (language = English)
        // -------------------------------------------------
        var ocrEngine = new OcrEngine();
        ocrEngine.Config.Language = Language.English;

        // -------------------------------------------------
        // Step 2: Locate every PNG file in the input folder
        // -------------------------------------------------
        string inputFolder = @"YOUR_DIRECTORY\images";
        string[] imagePaths = Directory.GetFiles(inputFolder, "*.png");

        if (imagePaths.Length == 0)
        {
            Console.WriteLine("No PNG files found – nothing to process.");
            return;
        }

        // -------------------------------------------------
        // Step 3: Convert file paths to ImageStream objects
        // -------------------------------------------------
        var imageStreams = imagePaths
            .Select(path => ImageStream.FromFile(path))
            .ToList();

        // -------------------------------------------------
        // Step 4: Recognize text in the entire batch
        // -------------------------------------------------
        IReadOnlyList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);

        // -------------------------------------------------
        // Step 5: Write each result to a .txt file next to the image
        // -------------------------------------------------
        string outputFolder = @"YOUR_DIRECTORY\output";
        Directory.CreateDirectory(outputFolder); // ensures the folder exists

        for (int i = 0; i < ocrResults.Count; i++)
        {
            string originalFileName = Path.GetFileNameWithoutExtension(imagePaths[i]);
            string outputPath = Path.Combine(outputFolder, $"{originalFileName}.txt");
            File.WriteAllText(outputPath, ocrResults[i].Text);
            Console.WriteLine($"✅ {originalFileName}.txt created");
        }

        Console.WriteLine("All done! Check the output folder for your text files.");
    }
}
```

> **預期輸出：** 每個 `image01.png` 皆會產生一個 `image01.txt`，內含辨識出的字元。主控台會列出每個寫入的檔案。

![批量 OCR 圖解](how-to-batch-ocr-diagram.png "說明如何使用 C# 批量 OCR PNG 圖像的圖示")

---

## 步驟說明

### 1. 初始化 OCR 引擎 – 流程的核心  

`var ocrEngine = new OcrEngine();` 這行程式碼會建立一個引擎實例，供整個批次重複使用。重複使用引擎是 **關鍵**，因為大多數 OCR 函式庫會在建構時分配大量資源（例如語言模型）。一次初始化即可大幅提升效能——尤其在處理數十或數百張 PNG 時。

> **專業提示：** 若需要非英文語言，請設定 `ocrEngine.Config.Language = Language.Spanish;`（或任何支援的列舉值）。

### 2. 從目錄讀取圖像 – 定位每個 PNG  

`Directory.GetFiles(@"YOUR_DIRECTORY\images", "*.png")` 正好符合次要關鍵字 *從目錄讀取圖像* 的描述。它會回傳絕對路徑陣列，稍後我們會將其傳入 OCR 引擎。  

> **為何不使用 `SearchOption.AllDirectories`？** 若圖像位於子目錄中，可改用 `GetFiles(path, "*.png", SearchOption.AllDirectories)`。但請記得較深層的掃描可能會帶入不需要的檔案，需自行過濾。

### 3. 將檔案路徑轉換為 ImageStream 物件  

大多數 OCR SDK 需要的是串流而非原始路徑。LINQ 表達式 `Select(path => ImageStream.FromFile(path)).ToList()` 會建立一個 **串流清單**，讓批次辨識器一次性使用。此步驟同時確保檔案只開啟一次，降低 I/O 負擔。  

> **例外情況：** 若檔案損毀，`ImageStream.FromFile` 可能拋出例外。若需韌性，請將轉換包在 `try/catch` 中。

### 4. 在整個批次中辨識文字  

`ocrEngine.RecognizeBatch(imageStreams)` 正是 *如何批量 OCR* 的最佳做法。與其對每張圖像迴圈呼叫單圖方法，我們直接將整個集合交給引擎。函式庫在內部可能會平行化處理，於多核心機器上提升速度。  

> **提示：** 若你的 OCR 函式庫未提供批次方法，仍可透過在單圖 `Recognize` 呼叫外層使用 `Parallel.ForEach` 來取得類似效能。

### 5. 寫入每個 OCR 結果 – 將 PNG 轉換為文字  

最後的 `for` 迴圈會將 `ocrResults[i].Text` 寫入與原始 PNG 同名的 `.txt` 檔案。這正是次要關鍵字 *將 PNG 轉換為文字* 所描述的行為。`Path.Combine` 呼叫確保輸出資料夾已存在，並防止路徑遍歷的錯誤。  

> **常見陷阱：** 若未先建立輸出目錄，會拋出 `DirectoryNotFoundException`。使用 `Directory.CreateDirectory(outputFolder);` 可提前解決此問題。

## 處理實務變化

| 情況 | 要更改的地方 | 原因 |
|-----------|----------------|-----|
| **空的輸入資料夾** | 保留早期的 `if (imagePaths.Length == 0)` 防護 | 防止不必要的 OCR 呼叫，並提供友善訊息 |
| **混合檔案類型** | 使用 `Directory.EnumerateFiles(..., "*.*", SearchOption.TopDirectoryOnly).Where(f => f.EndsWith(".png", StringComparison.OrdinalIgnoreCase))` | 確保只處理 PNG，符合 *extract text png* 而不產生錯誤 |
| **大型圖像（> 5 MB）** | 在送入 OCR 前先縮小：`ImageStream.FromFile(path).Resize(1920, 1080)`（若 API 支援） | 減少記憶體壓力，且通常提升辨識準確度 |
| **不同的 OCR 語言** | 設定 `ocrEngine.Config.Language = Language.French;` | 使引擎與來源圖像的語言相符 |

## 常見問題 (FAQ)

**Q: 這能用於 JPEG 或 TIFF 檔案嗎？**  
A: 核心邏輯保持不變，只需將搜尋模式改為 `"*.jpg"` 或 `"*.tif"`，並確保 OCR 函式庫能解碼這些格式。

**Q: 如何在不耗盡記憶體的情況下處理數千張圖像？**  
A: 將批次呼叫改為串流方式——一次處理例如 50 張圖像的區塊，處理完後釋放串流，再載入下一批。

**Q: 我需要 OCR 信心分數。該在哪裡取得？**  
A: 大多數 `OcrResult` 物件都有 `Confidence` 屬性。你可以擴充寫出步驟：

```csharp
var result = ocrResults[i];
string content = $"Confidence: {result.Confidence:P2}\n{result.Text}";
File.WriteAllText(outputPath, content);
```

## 總結

我們剛剛完整說明了在 C# 中 **如何批量 OCR** PNG 圖像的全流程。透過初始化單一引擎、從目錄讀取圖像、將其轉換為串流、辨識整個批次，最後將每個結果寫入文字檔，你現在擁有一套穩固、可投入生產的模式，適用於 **提取文字 PNG**、**將 PNG 轉換為文字** 與 **從目錄讀取圖像** 等任務。

接下來可以怎麼做？嘗試更換 OCR 供應商、加入多執行緒的後處理（例如拼寫檢查），或將 `.txt` 檔案匯入搜尋索引。掌握批次工作流程後，想像空間無限。

有任何想法想分享嗎？留下評論吧，祝 coding 愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}