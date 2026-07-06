---
category: general
date: 2026-03-13
description: 如何在 C# 中使用 OcrEngine 執行 OCR 並從圖片中擷取文字。學習快速將圖片轉換為文字的完整步驟指南。
draft: false
keywords:
- how to perform OCR
- extract text from image
- convert image to text
- read text from picture
- how to extract text
language: zh-hant
og_description: 如何在 C# 中執行 OCR？本指南將向您展示如何從圖片中提取文字、將圖片轉換為文字，以及使用 OcrEngine 讀取圖片內的文字。
og_title: 如何在 C# 中執行 OCR – 從圖片中提取文字
tags:
- OCR
- C#
- Image Processing
title: 如何在 C# 中執行 OCR – 從圖像提取文字
url: /zh-hant/net/text-recognition/how-to-perform-ocr-in-c-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中執行 OCR – 從圖像提取文字

在 C# 中執行 OCR 是開發人員常見的問題，特別是需要**從圖片檔案讀取文字**時。本指南將帶領你使用 `OcrEngine` 函式庫從圖像提取文字，僅需幾行程式碼即可將圖片轉換為可搜尋的字串。  

如果你曾盯著掃描的發票、手寫筆記或螢幕截圖，並想著 *「我要怎樣提取文字？」*，那麼你來對地方了。我們也會提及將圖像轉換為文字以進行批次處理，讓你能自動化整個工作流程。

---

## 你需要的條件

- **.NET 6.0 或更新版本**（我們使用的 API 可在 .NET Standard 2.0+ 上運作）
- **OcrEngine** NuGet 套件（或任何相容的 OCR 函式庫，只要提供 `Language`、`Image`、`Recognize` 與 `Text` 屬性）
- 範例圖像檔案，例如 `hindi_page.jpg`，放在程式碼可參考的資料夾中
- 基本的 C# 語法了解 – 不需要進階技巧

就這樣。無需外部服務、無需 API 金鑰，只要本地函式庫即可完成繁重的工作。

---

## 步驟式實作

以下我們將流程拆解為邏輯區塊。每個章節都有清晰的標題、簡短的程式碼片段，以及說明**為何**此步驟重要——不僅僅是**做什麼**。

### 如何執行 OCR – 核心步驟

整體流程可概括為五個動作：

1. **Create** OCR 引擎實例
2. **Select** 要辨識的語言
3. **Load** 含有文字的圖像
4. **Run** 辨識演算法
5. **Read** 提取出的文字

這是骨架；以下章節將為其填充細節。

---

### 從圖像提取文字 – 建立引擎

首先，我們需要一個能與 OCR 引擎溝通的物件。

```csharp
using System;
using OcrLibrary;   // Replace with the actual namespace of your OCR package

// Step 1: Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();
```

*Why this matters:* 實例化 `OcrEngine` 會分配所有內部緩衝區，並載入影像分析所需的原生 DLL。若跳過此步驟，之後將無法呼叫辨識器。

> **Pro tip:** 若你打算連續處理多張圖像，請保持相同的 `ocrEngine` 實例存活。它會重複使用語言模型，提升後續呼叫的速度。

---

### 將圖像轉換為文字 – 選擇語言

OCR 的準確度高度依賴所使用的語言模型。對於印地語、泰米爾語或任何其他文字，請相應設定 `Language` 屬性。

```csharp
// Step 2: Select the language of the text to recognize (e.g., Hindi)
ocrEngine.Language = Language.Hindi;   // You can also use Language.Tamil, Language.English, etc.
```

*Why this matters:* 引擎會使用特定語言的字元集與統計模型。提供錯誤的語言常會產生亂碼，尤其是非拉丁文字。

> **Edge case:** 若需要多語言支援，部分函式庫允許設定備援語言清單，例如 `ocrEngine.Language = Language.Multilingual;`。

---

### 從圖片讀取文字 – 載入來源圖像

現在我們將引擎指向包含可視文字的檔案。

```csharp
// Step 3: Load the image that contains the text
ocrEngine.Image = ImageStream.FromFile(@"C:\OCR\Samples\hindi_page.jpg");
```

*Why this matters:* `ImageStream.FromFile` 會將原始檔案轉換為 OCR 核心能理解的位圖格式。提供損毀或不支援的格式（例如 SVG）會拋出例外。

> **Watch out:** 大圖像可能佔用大量記憶體。若處理高解析度掃描，請考慮在傳入引擎前使用 `Image.Resize` 進行縮小。

---

### 將圖像轉換為文字 – 執行辨識

引擎已就緒且圖像已載入，我們終於呼叫 OCR 程序。

```csharp
// Step 4: Perform the OCR operation
ocrEngine.Recognize();
```

*Why this matters:* `Recognize` 會觸發一系列內部步驟——前處理、分割、字元分類與後處理。此呼叫為阻塞式，表示執行緒會等待文字完成後才繼續。

> **Performance note:** 在一般桌面電腦上，辨識 300 dpi 的頁面耗時 < 1 秒。若在伺服器上執行，建議將其放入背景工作，以免 UI 卡住。

---

### 如何提取文字 – 取得結果

辨識完成後，引擎會將純文字輸出存於 `Text` 屬性。

```csharp
// Step 5: Output the recognized text
Console.WriteLine(ocrEngine.Text);
```

*Why this matters:* `Text` 屬性提供乾淨的 UTF‑8 字串，你可以寫入檔案、寫入資料庫，或傳遞給後續的 NLP 流程。

> **Expected output:** 以範例的印地語頁面為例，你可能會看到類似以下內容  
> `यह एक उदाहरण पाठ है जो OCR द्वारा पहचाना गया है।`  
> （實際輸出取決於圖像品質與語言模型。）

---

## 真實專案的其他考量

以下列出一些在生產環境中**從圖像提取文字**時可能遇到的「假如」情境。

### 在迴圈中處理多張圖像

若需為數十個檔案**將圖像轉換為文字**，可將步驟包在 `foreach` 迴圈中，並重複使用相同的 `ocrEngine`：

```csharp
string[] files = Directory.GetFiles(@"C:\OCR\Batch\", "*.jpg");
foreach (var file in files)
{
    ocrEngine.Image = ImageStream.FromFile(file);
    ocrEngine.Recognize();
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), ocrEngine.Text);
}
```

### 處理低品質掃描

- **Pre‑process** 使用二值化 (`Image.Binarize()`)、除噪或去斜。
- **Increase DPI** 掃描時提升 DPI（300 dpi 為安全基準）。
- **Choose a language model** 以支援該文字的連字（例如印地語的 Devanagari）。

### 從網路讀取圖片文字

當圖像來自 URL 時，請先下載至記憶體串流：

```csharp
using (HttpClient client = new())
{
    byte[] data = await client.GetByteArrayAsync(imageUrl);
    using var ms = new MemoryStream(data);
    ocrEngine.Image = ImageStream.FromStream(ms);
    ocrEngine.Recognize();
    Console.WriteLine(ocrEngine.Text);
}
```

### 執行緒安全與平行處理

大多數 OCR 函式庫預設**不**具備執行緒安全性。若計畫同時**從圖片讀取文字**，請為每個執行緒建立獨立的 `OcrEngine` 實例，或使用生產者‑消費者佇列來序列化存取。

---

## 完整範例程式

將所有步驟整合起來，以下是一個可直接執行的 Console 應用程式，示範**如何執行 OCR**、**從圖像提取文字**以及**從圖片讀取文字**的完整流程。

```csharp
using System;
using OcrLibrary;               // Adjust to your OCR library's namespace
using System.IO;

class Program
{
    static void Main()
    {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Choose the language (Hindi in this case)
        ocrEngine.Language = Language.Hindi;

        // Load the image file
        string imagePath = @"C:\OCR\Samples\hindi_page.jpg";
        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"Image not found: {imagePath}");
            return;
        }

        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // Run the recognition process
        ocrEngine.Recognize();

        // Output the extracted text
        string result = ocrEngine.Text;
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(result);

        // Optional: Save to a .txt file
        string txtPath = Path.ChangeExtension(imagePath, ".txt");
        File.WriteAllText(txtPath, result);
        Console.WriteLine($"Text saved to {txtPath}");
    }
}
```

**預期結果：** 主控台會印出從 `hindi_page.jpg` 提取的印地語句子，並確認文字檔已建立。若圖像清晰，輸出將與原始印刷文字幾乎相同。

---

## 結論

現在你已掌握在 C# 中從頭到尾**執行 OCR**的方式，了解如何**從圖像提取文字**、**將圖像轉換為文字**以及**從圖片讀取文字**，只需使用簡單的 `OcrEngine` 工作流程。這五步驟—建立、設定語言、載入、辨識、讀取—涵蓋大多數使用情境，額外的技巧則協助你處理批次作業、低品質掃描與網路來源。

準備好接受下一個挑戰了嗎？試著將語言切換為英文、將 PDF 頁面渲染為圖像，或將 OCR 輸出串接至搜尋索引管線。只要掌握了 C# 中 OCR 的基礎，便可無所限制。

有任何問題或遇到難以辨識的圖像嗎？在下方留言，我們一起排除故障。祝開發愉快！  

![如何執行 OCR 範例](images/ocr-example.png "如何執行 OCR 範例")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}