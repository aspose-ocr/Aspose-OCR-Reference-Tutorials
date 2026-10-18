---
category: general
date: 2026-03-23
description: 使用 Aspose OCR 快速從表單提取文字。了解如何在指定區域識別文字，並使用完整的 C# 範例處理圖像的 OCR 部分。
draft: false
keywords:
- extract text from form
- recognize text in area
- ocr part of image
- Aspose OCR C#
- region based OCR
language: zh-hant
og_description: 使用 Aspose OCR 從表單提取文字。本教學示範如何在特定區域辨識文字，並在 C# 中處理影像的 OCR 部分。
og_title: 使用 Aspose OCR 從表單提取文字 – 完整指南
tags:
- C#
- OCR
- Aspose
- Image Processing
title: 使用 Aspose OCR 從表單提取文字 – 步驟指南
url: /zh-hant/net/text-recognition/extract-text-from-form-with-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose OCR 從表單提取文字 – 步驟指南

是否曾經需要 **從表單提取文字**，卻發現整頁雜訊太多？您並非唯一的開發者——大家常常要處理 PDF、掃描發票或手寫問卷，而實際上只關心其中一個欄位。好消息是，您可以指示 Aspose OCR 只看您在意的區塊，忽略其餘部分。

在本指南中，我們將示範如何 **在掃描表單的特定區域辨識文字**、抽取所需值，且不影響圖像的其他部分。完成後，您將擁有一個可直接執行的 C# 程式，僅處理您關注的 **圖像 OCR 部分**，且不需呼叫任何外部服務。

## 本教學您將學到

- 一個完整、可執行的 C# 主控台應用程式，能從表單圖像抽取欄位。  
- 為何針對矩形區域進行辨識能提升速度與準確度的清晰說明。  
- 處理空白結果、不同 DPI 設定與多頁表單的技巧。  
- 快速檢查清單，讓您在數分鐘內將程式碼套用到自己的專案。

**先備條件** – 您需要 .NET 6 或更新版本、Visual Studio 2022（或任意您喜歡的 IDE），以及首次執行時能連網以下載 Aspose.OCR NuGet 套件。除此之外不需要其他函式庫。

---

## 從表單提取文字 – 建立專案

在撰寫程式碼之前，先確保開發環境已就緒。以下步驟刻意保持簡潔，因為真正的魔法發生在 OCR 引擎實例化之後。

1. **建立新的主控台專案**  
   ```bash
   dotnet new console -n FormOcrDemo
   cd FormOcrDemo
   ```

2. **透過 NuGet 加入 Aspose.OCR**  
   ```bash
   dotnet add package Aspose.OCR
   ```

3. **將掃描好的表單複製到專案資料夾**，並重新命名為 `form.png`。  
   （若您的檔案是 PDF，請先將需要的頁面匯出為 PNG——Aspose OCR 最適合處理點陣圖。）

完成以上三步即可。接下來的教學皆假設這些步驟已完成。

![extract text from form example](form-region.png "extract text from form example")

*Image alt text: extract text from form example showing a highlighted region on a scanned document.*

---

## 在區域內辨識文字 – 定義感興趣區域

為什麼要使用矩形？想像您有一份 2 MB 的完整報稅表掃描檔。對整張圖執行 OCR 會浪費 CPU 時間，且可能因無關欄位產生誤判。將範圍縮小到正好包含目標值的座標，您可以：

- **縮短處理時間**，大型圖像可減少最高 80 % 的運算。  
- **提升辨識準確度**，因為引擎會忽略干擾圖形。  
- **簡化後續處理**——您清楚知道會得到什麼文字。

矩形由四個數字定義：`x`、`y`、`width`、`height`。這些值以像素為單位，從圖像左上角開始測量。若不確定欄位位置，可在 Paint 中開啟圖像，將滑鼠移至左上角讀取 X/Y 值，然後拖曳測量寬度與高度。

---

## 圖像 OCR 部分 – 載入表單並設定引擎

現在已確定區域，接下來說明引擎本身。`OcrEngine` 是 Aspose OCR 的核心。它會自動偵測語言、校正傾斜，並回傳純文字字串。您也可以調整屬性（如 `Resolution` 或 `Language`），若表單使用非拉丁文字。對於大多數英文表單，預設值已足夠。

以下是 **完整、獨立的程式**，將所有步驟整合。直接貼到 `Program.cs` 後，按 **F5** 即可執行。

```csharp
using Aspose.OCR;
using System;
using System.Drawing; // for Rectangle

class RegionExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Create the OCR engine (using ensures disposal)
        // -------------------------------------------------
        using (OcrEngine ocrEngine = new OcrEngine())
        {
            // -------------------------------------------------
            // Step 2: Load the image that contains the form
            // -------------------------------------------------
            // ImageStream.FromFile reads the file into Aspose's internal format
            // Replace "YOUR_DIRECTORY/form.png" with the actual path if needed
            ocrEngine.Image = ImageStream.FromFile("form.png");

            // -------------------------------------------------
            // Step 3: Define the region that holds the desired field
            // -------------------------------------------------
            // (x, y, width, height) – adjust these numbers for your form
            Rectangle regionOfInterest = new Rectangle(120, 350, 400, 80);

            // -------------------------------------------------
            // Step 4: Recognize text only inside the defined region
            // -------------------------------------------------
            bool success = ocrEngine.Recognize(regionOfInterest);
            string recognizedText = success ? ocrEngine.Text.Trim() : string.Empty;

            // -------------------------------------------------
            // Step 5: Display the extracted field value
            // -------------------------------------------------
            Console.WriteLine("Field value: " + (string.IsNullOrEmpty(recognizedText)
                ? "[No text detected]"
                : recognizedText));
        }

        // Keep the console window open when debugging
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

### 預期輸出

若矩形正確框住顯示「Invoice # 12345」的欄位，主控台會印出：

```
Field value: Invoice # 12345
```

若區域為空或 OCR 失敗，則會顯示：

```
Field value: [No text detected]
```

---

## 步驟說明 – 程式碼逐行解析

以下將程式分割成易於理解的片段，說明每行 **為何** 這麼寫，並指出可能需要自行調整的地方。

### 步驟 1：透過 NuGet 安裝 Aspose.OCR *(H3)*

```bash
dotnet add package Aspose.OCR
```

*為什麼？* NuGet 套件內含原生 OCR 引擎、語言資料檔以及輕量的 .NET 包裝層。若未安裝，`OcrEngine` 類別根本不存在。

### 步驟 2：初始化 OcrEngine *(H3)*

```csharp
using (OcrEngine ocrEngine = new OcrEngine())
```

*為什麼使用 `using`？* `OcrEngine` 會佔用非受控資源（原生 DLL、影像緩衝區）。`using` 陳述式可確保在使用完畢後釋放，避免長時間服務產生記憶體泄漏。

### 步驟 3：載入表單影像 *(H3)*

```csharp
ocrEngine.Image = ImageStream.FromFile("form.png");
```

*為什麼使用 `ImageStream`？* 它抽象化檔案 I/O，並自動將常見格式（PNG、JPEG、TIFF）轉換為 Aspose OCR 所需的內部位圖表示。

### 步驟 4：指定要抽取文字的區域 *(H3)*

```csharp
Rectangle regionOfInterest = new Rectangle(120, 350, 400, 80);
```

*為什麼使用 `Rectangle`？* OCR 引擎接受 `System.Drawing.Rectangle`。四個參數讓您精準定位目標欄位，將其餘頁面排除。

*小技巧：* 若需支援多個欄位，可將每個矩形存入 `Dictionary<string, Rectangle>`，再以迴圈逐一處理。

### 步驟 5：執行辨識並取得結果 *(H3)*

```csharp
bool success = ocrEngine.Recognize(regionOfInterest);
string recognizedText = success ? ocrEngine.Text.Trim() : string.Empty;
```

*為什麼要檢查 `success`？* OCR 可能因影像模糊、語言不支援或區域為空等原因失敗。檢查布林值可避免使用過期資料。

### 步驟 6：處理例外情況與常見陷阱 *(H3)*

- **不同 DPI**：若掃描解析度低於 150 DPI，請在呼叫 `Recognize` 前提升 `ocrEngine.Image.DpiX` 與 `ocrEngine.Image.DpiY`。  
- **多頁文件**：對於多頁 PDF，先將每頁匯出為單獨 PNG，然後對每頁套用相同的矩形邏輯。  
- **非英文文字**：在辨識前設定 `ocrEngine.Language = Language.Thai;`（或其他支援語言）。  
- **降噪**：`ocrEngine.Image.Filters.Add(new GaussianBlurFilter(1.2f));` 可改善顆粒感較高的掃描圖。

---

## 延伸應用 – 真實情境變化

### 從同一表單抽取多個欄位

若需要同時取得「姓名」「日期」與「金額」，可建立集合：

```csharp
var fields = new Dictionary<string, Rectangle>
{
    { "Name",   new Rectangle(50, 200, 300, 60) },
    { "Date",   new Rectangle(400, 200, 200, 60) },
    { "Amount", new Rectangle(650, 200, 250, 60) }
};

foreach (var kvp in fields)
{
    bool ok = ocrEngine.Recognize(kvp.Value);
    Console.WriteLine($"{kvp.Key}: {(ok ? ocrEngine.Text.Trim() : "[Not found]")}");
}
```

### 與資料庫整合

抽取完畢後，您可能想將結果寫入 SQL Server：

```csharp
using (var conn = new SqlConnection(connectionString))
{
    conn.Open();
    var cmd = new SqlCommand(
        "INSERT INTO FormResults (FieldName, FieldValue) VALUES (@name, @value)", conn);
    cmd.Parameters.AddWithValue("@name", "InvoiceNumber");
    cmd.Parameters.AddWithValue("@value", recognizedText);
    cmd.ExecuteNonQuery();
}
```

### 在伺服器上自動化執行

若打算將此程式作為背景服務執行，請將邏輯封裝於 `async` 方法，並使用 `Task.Run` 以保持 UI 響應。別忘了設定 `ocrEngine.ParallelProcessing = true;` 以利用多核心加速。

---

## 結論

現在您已掌握使用 Aspose OCR 從表單圖像 **提取文字** 的完整、可投入生產環境的解決方案。只要聚焦於特定矩形區域，即可有效降低資源消耗、提升辨識正確率。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}