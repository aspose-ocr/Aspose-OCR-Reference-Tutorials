---
category: general
date: 2026-04-01
description: 使用 Aspose OCR 在 C# 中建立可搜尋的 PDF – 學習如何將掃描的 PDF 轉換、為 PDF 添加 OCR，並啟用 GPU
  加速以獲得快速結果。
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- convert pdf to searchable
- add OCR to pdf
- enable GPU acceleration
language: zh-hant
og_description: 在 C# 中快速建立可搜尋 PDF——將掃描 PDF 轉換、為 PDF 加入 OCR，並啟用 GPU 加速以實現高效能處理。
og_title: 在 C# 中使用 Aspose OCR 建立可搜尋的 PDF
tags:
- Aspose OCR
- C#
- PDF processing
title: 使用 Aspose OCR 在 C# 中建立可搜尋的 PDF
url: /zh-hant/net/ocr-optimization/create-searchable-pdf-with-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose OCR 在 C# 中建立可搜尋的 PDF

是否曾需要從一堆掃描文件建立 **可搜尋的 PDF** 檔案？你並非唯一面臨此問題的使用者——許多團隊都在努力將僅含影像的 PDF 轉換成可文字搜尋的資產。好消息是？使用 Aspose OCR，你只需幾行 C# 程式碼即可 **將掃描的 PDF 轉換** 為完整可搜尋的版本。在本指南中，我們將逐步說明整個流程，從為 PDF 加入 OCR 到可選的 **啟用 GPU 加速** 以提升速度。

我們還會示範如何 **將 PDF 轉換為可搜尋** 格式，討論為何你可能想要 **為 PDF 加入 OCR**，以及提供處理大量批次的實用技巧。完成後，你將擁有一個即時可執行的主控台應用程式，產生的可搜尋 PDF 可直接放入任何文件管理系統。

---

## 需要的條件

- **.NET 6.0** 或更新版本（API 也支援 .NET Framework，但 .NET 6+ 為最佳選擇）。
- **Aspose.OCR for .NET** NuGet 套件（`Install-Package Aspose.OCR`）。
- 一個掃描的 PDF 檔案（僅含影像）作為輸入。
- 可選：具備 CUDA® 的 GPU 相容機器，若想 **啟用 GPU 加速**。

就這樣——不需要大型 OCR 引擎，也不需外部服務。所有操作皆在本機執行。

---

## 建立可搜尋 PDF – 步驟概覽

以下是我們將遵循的高階流程：

1. **初始化 OCR 引擎** – 告訴 Aspose 要辨識的語言以及是否使用 GPU。
2. **指定引擎的掃描 PDF** – 定義輸入與輸出路徑。
3. **執行轉換** – Aspose 完成繁重工作並寫入可搜尋的 PDF。
4. **驗證結果** – 開啟輸出檔案並嘗試文字搜尋。

每個步驟都有獨立章節，讓你可挑選最相關的部分。

---

## 將掃描的 PDF 轉換為可搜尋 PDF

首先，你需要建立 `OcrEngine` 的實例。此物件是執行核心，負責讀取 PDF 內的點陣圖並擷取文字。

```csharp
using Aspose.OCR;
using System;

class PdfSearchableDemo
{
    static void Main()
    {
        // Step 1: Create and configure the OCR engine
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.English,
            // Optional: enable GPU for faster processing
            UseGpuAcceleration = true
        };

        // Step 2: Specify the input scanned PDF and the output searchable PDF paths
        string sourcePdfPath = @"C:\Docs\input.pdf";
        string searchablePdfPath = @"C:\Docs\output.pdf";

        // Step 3: Convert the scanned PDF into a searchable PDF
        ocrEngine.ConvertToSearchablePdf(sourcePdfPath, searchablePdfPath);

        // Step 4: Notify the user where the searchable PDF was saved
        Console.WriteLine("Searchable PDF created at: " + searchablePdfPath);
    }
}
```

**為什麼這樣可行：** `ConvertToSearchablePdf` 會逐頁讀取，對點陣內容執行 OCR，然後在原始影像後嵌入隱形文字層。結果與原始掃描文件外觀相同，但現在可以複製、選取與搜尋文字。

---

## 使用 Aspose 為 PDF 加入 OCR

如果你已經有 PDF，只想 **為 PDF 加入 OCR** 而不轉換整個檔案，可以呼叫相同的方法——Aspose 會將此操作視為「加入 OCR」。上方程式碼已完成此功能，以下提供一個快速變體，示範如何在迴圈中處理多個檔案：

```csharp
string[] pdfFiles = Directory.GetFiles(@"C:\Docs\Scanned", "*.pdf");
foreach (var file in pdfFiles)
{
    string output = Path.Combine(@"C:\Docs\Searchable", Path.GetFileNameWithoutExtension(file) + "_searchable.pdf");
    ocrEngine.ConvertToSearchablePdf(file, output);
    Console.WriteLine($"Processed {Path.GetFileName(file)} → {Path.GetFileName(output)}");
}
```

**提示：** 整批處理時保留同一個 `OcrEngine` 實例。每次重新建立會增加不必要的開銷，尤其在 **啟用 GPU 加速** 時更是如此。

---

## 為更快的 OCR 啟用 GPU 加速

GPU 加速可為大量批次節省數分鐘。Aspose OCR 於底層使用 NVIDIA CUDA，只需切換布林旗標即可：

```csharp
ocrEngine.UseGpuAcceleration = true; // set to false if no compatible GPU
```

**何時使用：** 若處理的 PDF 大於 10 MB 或超過數十個檔案，GPU 通常可提升 2‑3 倍速度。若在沒有 CUDA 相容 GPU 的一般筆記型電腦上，請保留 `false`——函式庫會自動回退至 CPU。

**常見陷阱：** 忘記安裝正確的 CUDA 驅動版本會導致執行時例外 (`CudaException`)。請確保你的驅動版本與 Aspose 所需相符（請參閱 NuGet 頁面的發行說明）。

---

## 完整範例（結合所有步驟）

以下是一個獨立的主控台應用程式範例，你可以直接複製貼上至新的 .NET 專案。它包含實用註解、錯誤處理，以及最終驗證步驟，會印出處理的頁數。

```csharp
using Aspose.OCR;
using System;
using System.IO;

class PdfSearchableDemo
{
    static void Main()
    {
        try
        {
            // 1️⃣ Initialize OCR engine – English language, GPU on if available
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.English,
                UseGpuAcceleration = true // set to false on non‑GPU machines
            };

            // 2️⃣ Define input and output paths
            string sourcePdfPath = @"C:\Docs\input.pdf";
            string searchablePdfPath = @"C:\Docs\output.pdf";

            // 3️⃣ Perform the conversion – this creates a searchable PDF
            ocrEngine.ConvertToSearchablePdf(sourcePdfPath, searchablePdfPath);

            // 4️⃣ Simple verification – count pages in the new file
            int pageCount = new Aspose.Pdf.Facades.PdfFileInfo(searchablePdfPath).NumberOfPages;
            Console.WriteLine($"✅ Searchable PDF created at: {searchablePdfPath}");
            Console.WriteLine($"📄 The new file contains {pageCount} pages.");

            // 5️⃣ Optional: open the file automatically (Windows only)
            // System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo(searchablePdfPath) { UseShellExecute = true });
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"❌ Oops! Something went wrong: {ex.Message}");
        }
    }
}
```

**預期輸出**

```
✅ Searchable PDF created at: C:\Docs\output.pdf
📄 The new file contains 12 pages.
```

在任何 PDF 檢視器中開啟 `output.pdf`，並嘗試輸入掃描影像中出現的字詞。若文字被標示，即表示你已成功 **建立可搜尋的 PDF**。

---

## 常見問題與專業提示

| Issue | Why it Happens | How to Fix / Avoid |
|-------|----------------|--------------------|
| **未偵測到 GPU** | 缺少或不相容的 CUDA 驅動。 | 安裝 Aspose 發行說明中列出的驅動版本；如需回退，將 `UseGpuAcceleration = false` 設為 false。 |
| **語言設定錯誤** | OCR 預設為英文；其他語言需明確設定。 | 在轉換前設定 `Language = Language.Spanish`（或任何支援的列舉）。 |
| **大型 PDF 造成 OutOfMemory** | 引擎會將整頁載入記憶體。 | 使用 `ocrEngine.PageRange = new PageRange(1, 5)` 將 PDF 分批處理。 |
| **輸出檔案損毀** | 目標資料夾缺乏寫入權限。 | 以提升的權限執行應用程式或選擇可寫入的路徑。 |
| **文字層無法搜尋** | 檢視器快取了舊版本。 | 重新整理 PDF 檢視器或重新開啟檔案。 |

**專業提示：** 當同時處理掃描 PDF 與原生 PDF 時，請在執行 OCR 前檢查每頁的 `HasText` 旗標（`PdfPageInfo.HasText`）。這可節省 CPU 資源，避免對已可搜尋的頁面重複 OCR。

---

## 以程式方式驗證結果（可選）

若想自動化驗證，Aspose.PDF 可擷取隱藏文字：

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Load the searchable PDF
Document doc = new Document(searchablePdfPath);
TextAbsorber absorber = new TextAbsorber();
doc.Pages.Accept(absorber);
string extracted = absorber.Text;

// Simple check – does the word "Invoice" appear?
if (extracted.Contains("Invoice"))
    Console.WriteLine("✅ OCR succeeded – 'Invoice' found.");
else
    Console.WriteLine("⚠️ OCR may have missed some text.");
```

此程式碼片段證明你確實 **將 PDF 轉換為可搜尋** 格式，而非僅在影像上疊加。

---

## 圖片範例

![建立可搜尋 PDF 輸出範例](https://example.com/images/searchable-pdf.png "使用 Aspose OCR 建立可搜尋 PDF")

*Alt text:* **create searchable pdf** 範例，顯示前（掃描）與後（可搜尋）視圖。

---

## 後續步驟與相關主題

- **批次處理：** 將「為 PDF 加入 OCR」章節中的迴圈包裝成 Windows Service 或 Azure Function，以執行夜間作業。
- **進階語言支援：** 探索 `ocrEngine.Language = Language.Multilingual`，以處理包含多種文字的文件。
- **OCR 後清理：** 使用 Aspose.PDF 的 `TextFragmentAbsorber` 來校正常見 OCR 錯誤（例如「0」與「O」）。
- **Security

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}