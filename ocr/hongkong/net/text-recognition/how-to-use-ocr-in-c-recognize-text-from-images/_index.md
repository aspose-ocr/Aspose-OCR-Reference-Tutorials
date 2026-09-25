---
category: general
date: 2026-02-09
description: 如何在 C# 中使用 OCR 從圖像辨識文字、提取文字，並使用 Aspose OCR 將圖像轉換為文字。完整逐步指南。
draft: false
keywords:
- how to use OCR
- recognize text from image
- extract text from image
- convert image to text
- load image stream
language: zh-hant
og_description: 如何在 C# 中使用 OCR 從圖像識別文字、提取文字，並使用 Aspose OCR 將圖像轉換為文字。完整指南與程式碼。
og_title: 如何在 C# 中使用 OCR – 從圖像辨識文字
tags:
- C#
- Aspose OCR
- Image Processing
title: 如何在 C# 中使用 OCR – 從圖像辨識文字
url: /zh-hant/net/text-recognition/how-to-use-ocr-in-c-recognize-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 OCR – 從圖像辨識文字

有沒有想過 **如何使用 OCR** 把螢幕截圖轉換成可編輯的文字？你並不孤單。許多開發者在需要 *從圖像辨識文字* 時會卡住，卻找不到清晰、可直接執行的範例。  

在本教學中，我們將逐步說明整個流程——載入授權、建立引擎、傳入影像串流，最後取得純文字。完成後，你將能夠 **extract text from image**、**convert image to text**，甚至了解 **load image stream** 處理的細節。

> **你將獲得：** 一個完整、可執行的 C# 程式，使用 Aspose.OCR，包含每一步的說明，以及避免常見陷阱的技巧。

---

## 前置條件

- .NET 6.0 或更新版本（API 亦支援 .NET Framework 4.6 以上）  
- 已安裝 Aspose.OCR for .NET NuGet 套件 (`Aspose.OCR`)  
- 有效的 Aspose OCR 授權檔 (`Aspose.OCR.lic`) – 免費試用版可用，但會加上浮水印。  
- 一張包含清晰、機器可讀文字的影像 (`sample.jpg`)。

> **提示：** 如果你使用 Visual Studio，NuGet 主控台指令為  
> `Install-Package Aspose.OCR -Version 23.10`（請替換為最新版本）。

---

## 如何使用 OCR：載入授權並初始化引擎

首先，你必須告訴 Aspose 你已擁有授權。若跳過此步驟程式仍會執行，但輸出會出現浮水印，且會因試用模式檢查而浪費寶貴的處理時間。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Licensing;

class LicenseExample
{
    static void Main()
    {
        // Step 1 – Load the Aspose OCR license (replace with your .lic file path)
        License ocrLicense = new License();
        ocrLicense.SetLicense(@"C:\Licenses\Aspose.OCR.lic");

        // Step 2 – Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // The rest of the steps follow...
    }
}
```

**為什麼這很重要：** `License` 物件會關閉試用浮水印，並解鎖完整功能，包括更高精度的模型與多語言支援。  

> **專業提示：** 將授權檔放在來源控制系統之外。使用環境變數或安全保管庫在執行時注入路徑。

---

## 步驟 2 – 載入影像串流（以及為何比檔案路徑更好）

當你 *load image stream* 而非直接傳遞檔案路徑時，會獲得彈性：影像可以來自資料庫、Web 請求，或是記憶體中的位元組陣列。  

```csharp
// Step 3 – Load the image you want to recognize
// Using ImageStream.FromFile is the simplest way for local files.
ImageStream imageStream = ImageStream.FromFile(@"C:\Images\sample.jpg");

// Alternative: load from a byte array (e.g., when the image is uploaded via HTTP)
// byte[] imageBytes = ... // get from request
// ImageStream imageStream = ImageStream.FromBytes(imageBytes);
```

**說明：** `ImageStream` 抽象化底層來源，讓 OCR 引擎能統一處理所有資料。若日後改為雲端儲存桶，只需更改 `ImageStream` 的建立方式，其他程式碼則保持不變。

---

## 步驟 3 – 從影像辨識文字

現在進入重點：**recognize text from image**。`OcrEngine.Recognize` 方法會執行 Aspose 隨附的神經網路模型，並回傳包含多項有用屬性的 `OcrResult` 物件。

```csharp
// Step 4 – Run the OCR process on the image
OcrResult ocrResult = ocrEngine.Recognize(imageStream);
```

**`OcrResult` 內包含什麼？**  
- `PlainText` – 包含所有偵測到字元的單一字串。  
- `Words` – 包含文字物件與其邊界框的集合（可用於標示）。  
- `Lines` – 行層級的分組，方便保留段落斷行。

如果只需要原始文字，`PlainText` 是最快的方式。若有更進階的需求（例如在原始影像上疊加結果），可探索 `Words` 與 `Lines`。

---

## 步驟 4 – 顯示或儲存擷取的文字

最後，將辨識出的文字輸出到主控台。在實際應用中，你可能會寫入資料庫、檔案，或透過 API 傳送。

```csharp
// Step 5 – Display the recognized plain text (watermark omitted with a full license)
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.PlainText);
Console.WriteLine("==================");

// Optional: Save to a .txt file
System.IO.File.WriteAllText(@"C:\Output\extracted.txt", ocrResult.PlainText);
```

**預期輸出：**  
如果 `sample.jpg` 包含句子 *“Hello World!”*，你會看到：

```
=== OCR Output ===
Hello World!
==================
```

使用試用授權時，輸出文字的結尾會附加小型 “Aspose OCR Demo” 浮水印。擁有正式授權則會完全消失。

---

## 完整可執行範例（即貼即用）

以下是完整程式碼，已可直接編譯。將路徑替換為你自己的位置，即可執行。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Licensing;

class LicenseExample
{
    static void Main()
    {
        // 1️⃣ Load license – required for production use
        License ocrLicense = new License();
        ocrLicense.SetLicense(@"C:\Licenses\Aspose.OCR.lic");

        // 2️⃣ Create OCR engine – the core processing object
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Load image – you can also use ImageStream.FromBytes for in‑memory data
        ImageStream imageStream = ImageStream.FromFile(@"C:\Images\sample.jpg");

        // 4️⃣ Recognize text – this is where the magic happens
        OcrResult ocrResult = ocrEngine.Recognize(imageStream);

        // 5️⃣ Output the plain text – perfect for further processing
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.PlainText);
        Console.WriteLine("==================");

        // Optional: persist the result
        System.IO.File.WriteAllText(@"C:\Output\extracted.txt", ocrResult.PlainText);
    }
}
```

> **請記得：** 上述程式碼 **extracts text from image** 並 **converts image to text** 只需一次呼叫。無需額外迴圈或手動像素處理——全部由 Aspose 完成。

---

## 常見問題與邊緣情況

### 如果我的影像模糊或低對比度怎麼辦？

Aspose OCR 內建前處理選項（例如 `ocrEngine.ImagePreprocessor`）。你可以在辨識前啟用二值化或去傾斜：

```csharp
ocrEngine.ImagePreprocessor = new ImagePreprocessor
{
    Binarization = true,
    Deskew = true
};
```

### 如何處理多語言？

在引擎上設定 `Language` 屬性：

```csharp
ocrEngine.Language = OcrLanguage.English | OcrLanguage.Spanish;
```

引擎將自動嘗試偵測兩種語言。

### 能否處理 PDF 而非 JPEG？

可以——Aspose OCR 能直接讀取 PDF，但需要先使用 Aspose.PDF 套件將每頁轉為影像，然後再將影像串流傳入 OCR 引擎。

### 大批量處理該怎麼做？

將辨識邏輯包在迴圈中，並重複使用同一個 `OcrEngine` 實例。每張影像都建立新引擎會產生不必要的開銷。

---

## 生產環境 OCR 的專業技巧

- **Cache the license object**：於應用程式啟動時載入一次，而非每次請求都載入。  
- **Reuse `OcrEngine`**：引擎會保留內部緩衝，重複使用可減少 GC 壓力。  
- **Limit image size**：過大的影像（>5 MP）會大幅延長處理時間。若不需要高解析度，請縮小至 150‑300 DPI。  
- **Validate output**：OCR 並非完美，請實作簡易信心度檢查（`ocrResult.Words.Average(w => w.Confidence)`），並將低信心度結果標記為需人工審核。  
- **Thread safety**：`OcrEngine` 並非執行緒安全。請為每個執行緒建立獨立實例，或使用池化模式。

---

## 結論

我們已說明了在 C# 中 **how to use OCR** 的全過程，從載入授權到擷取乾淨、可搜尋的文字。依照上述步驟，你即可 **recognize text from image**、**extract text from image**，並輕鬆 **convert image to text**，同時掌握 **load image stream** 模式，讓程式碼未來能靈活應對各種資料來源。

準備好接受下一個挑戰了嗎？試著加入感興趣區域裁切、整合 Azure Blob Storage，或將 OCR 輸出餵入自然語言處理管線。沒有極限，而你現在已具備堅實的基礎可供構築。

![顯示 OCR 流程圖：載入授權 → 建立引擎 → 載入影像串流 → 辨識 → 輸出文字](image-placeholder.png "如何使用 OCR 從圖像辨識文字")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}