---
category: general
date: 2026-02-20
description: 學習如何在 C# 中讀取收據，透過從圖像提取文字並轉換為 JSON。使用 Aspose OCR 的逐步程式碼示例。
draft: false
keywords:
- how to read receipt
- extract text from image
- convert image to json
- load image file c#
- OCR receipt C#
- Aspose OCR tutorial
language: zh-hant
og_description: 了解如何在 C# 中透過載入影像檔案、使用 Aspose OCR 提取文字，並將結果轉換為 JSON 來讀取收據。完整程式碼範例。
og_title: 如何在 C# 中讀取收據 – 提取文字，轉換為 JSON
tags:
- C#
- OCR
- Image Processing
- JSON
title: 如何在 C# 中讀取收據 – 從圖像提取文字的完整指南
url: /zh-hant/net/text-recognition/how-to-read-receipt-in-c-complete-guide-to-extract-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中讀取收據 – 完整指南

有沒有想過**如何程式化讀取收據**圖像？也許你正在開發一個費用追蹤應用程式，需要從雜貨收據的照片中提取項目。依我的經驗，最大痛點是把模糊的 JPEG 轉成可用的結構化資料。好消息是？只要幾行 C# 程式碼加上 Aspose OCR，就能**從圖像中提取文字**，再**將圖像轉換為 JSON**，感覺幾乎是魔法般的。

在本教學中，你將獲得一個即插即用的解決方案，能**載入圖像檔案 C#**、執行 OCR，並輸出詳細的 JSON 資料。無需外部服務，無需繁雜的 REST 呼叫——只要純 .NET 程式碼即可放入任何 console 或 ASP.NET 專案。完成後，你將了解每個步驟的重要性、如何處理常見的邊緣案例（例如非標準收據尺寸），以及 JSON 輸出實際長什麼樣子。

## 需要的條件

- **.NET 6.0 或更新版** – 程式碼使用 `System.Drawing.Common`，支援 Windows、Linux 與 macOS。
- **Aspose.OCR for .NET** – 你可以取得免費試用的 NuGet 套件 (`Aspose.OCR`) 或在有授權時使用授權版。
- 一張 **sample receipt image** (`receipt.jpg`) 放在應用程式可讀取的位置。
- 任意你喜歡的 IDE（Visual Studio、Rider、VS Code）。

就這樣。無需額外設定，亦不需要 API 金鑰。

---

## 步驟 1 – 載入圖像檔案 C#（主要關鍵字實作）

在 OCR 引擎發揮魔法之前，你必須先將圖片載入記憶體。這就是許多開發者常忽略的經典「load image file C#」步驟。

```csharp
using System.Drawing;          // Required for Image
using Aspose.OCR;
using Aspose.OCR.Models;

// Path to your receipt image – adjust as needed
string imagePath = @"C:\Receipts\receipt.jpg";

// Load the image into a System.Drawing.Image object
Image receiptImage = Image.FromFile(imagePath);
```

**為什麼這很重要：**  
`Image.FromFile` 會*一次*讀取檔案並保持檔案句柄開啟，適合快速的 OCR 處理。如果你在迴圈中處理大量收據，建議改用 `Image.FromStream` 以避免鎖定檔案。

> **小技巧：** 若遇到 *FileNotFoundException*，請再次確認路徑並確保圖像真的存在。相對路徑也可使用（`"./receipt.jpg"`），但在正式環境中使用絕對路徑較安全。

---

## 步驟 2 – 建立並設定 OCR 引擎

Aspose OCR 內建即用的 `OcrEngine`。你不需要自行訓練模型；此函式庫已能辨識印刷文字，正好符合大多數收據的字體。

```csharp
// Instantiate the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Optional: tweak recognition settings if your receipts are low‑contrast
ocrEngine.Config.Language = OcrLanguage.English;
ocrEngine.Config.DetectOrientation = true;   // Handles rotated receipts
```

**為什麼要設定這些選項：**  
`DetectOrientation` 讓引擎在收據倒置掃描時自動旋轉圖像。設定語言可縮小字元集，提升準確度——尤其當你只需要英文與數字資料時。

---

## 步驟 3 – 辨識圖像並轉換為 JSON

現在進入有趣的部分：在一次呼叫中同時**從圖像中提取文字**與**將圖像轉換為 JSON**。

```csharp
// Perform OCR and get the result as a JSON string
string jsonResult = ocrEngine.RecognizeToJson(receiptImage);
```

`RecognizeToJson` 方法會回傳一個豐富的 JSON 結構，包含：

- `Text`：純文字的串接結果。
- `Lines`：包含座標的行物件陣列。
- `Words`：每個單字及其信心分數。
- `Regions`：偵測到的文字區塊的邊界框。

如果需要型別化存取，你可以將此 JSON 反序列化為 C# 物件；但在多數情況下直接印出原始 JSON 已足夠。

---

## 步驟 4 – 輸出 JSON（或儲存）

讓我們看看輸出結果，並討論接下來的處理方式。

```csharp
// Write the JSON to the console – perfect for quick debugging
Console.WriteLine(jsonResult);

// Bonus: Save the JSON to a file for later processing
File.WriteAllText("receipt_output.json", jsonResult);
```

### 範例輸出

```json
{
  "Text":"Walmart\n123 Main St\nItem A  $2.99\nItem B  $5.49\nTotal   $8.48",
  "Lines":[
    {"Text":"Walmart","BoundingBox":{"X":10,"Y":15,"Width":200,"Height":30}},
    {"Text":"123 Main St","BoundingBox":{"X":10,"Y":50,"Width":180,"Height":25}},
    {"Text":"Item A  $2.99","BoundingBox":{"X":10,"Y":85,"Width":210,"Height":28}},
    {"Text":"Item B  $5.49","BoundingBox":{"X":10,"Y":120,"Width":210,"Height":28}},
    {"Text":"Total   $8.48","BoundingBox":{"X":10,"Y":155,"Width":210,"Height":30}}
  ],
  "Words":[
    {"Text":"Walmart","Confidence":0.99,"BoundingBox":{...}},
    …
  ]
}
```

**接下來要做什麼？**  
解析 `Lines` 陣列以取得 `Total` 金額，或將 JSON 傳入下游服務以儲存費用項目。由於結果已是 JSON，你可以直接將它接入任何 NoSQL 資料庫、Azure Function 或 Power Automate 流程。

---

## 步驟 5 – 處理常見的邊緣案例

即使是最優秀的 OCR 引擎也會在某些情況下受阻。以下是你在學習**如何讀取收據**圖像時可能遇到的情境。

| 情況 | 修正 / 建議 |
|-----------|----------------------|
| **低解析度收據（≤ 150 dpi）** | 先使用 `Bitmap` 與 `Graphics`（`InterpolationMode.HighQualityBicubic`）將圖像放大。 |
| **旋轉或傾斜的收據** | 保留 `DetectOrientation = true`。若傾斜嚴重，可先以 `Image.RotateFlip` 或使用第三方函式庫如 OpenCV 進行前處理。 |
| **彩色背景（例如收據放在桌面上）** | 在 OCR 前先轉為灰階並提升對比度（`ImageAttributes`）。 |
| **單張照片中有多張收據** | 手動裁切每張收據區域，或使用 `ocrEngine.Config.RecognizeMultipleRegions = true`。 |
| **大型檔案導致 OutOfMemory** | 使用 `using` 陳述式即時釋放 `Image` 物件，或分批處理。 |

```csharp
// Example: simple grayscale conversion
using (Bitmap bmp = new Bitmap(receiptImage))
{
    for (int y = 0; y < bmp.Height; y++)
        for (int x = 0; x < bmp.Width; x++)
        {
            Color c = bmp.GetPixel(x, y);
            int gray = (int)(c.R * 0.3 + c.G * 0.59 + c.B * 0.11);
            bmp.SetPixel(x, y, Color.FromArgb(gray, gray, gray));
        }
    receiptImage = (Image)bmp.Clone();
}
```

---

## 步驟 6 – 完整範例（可直接複製貼上）

以下是可立即編譯的*完整*程式。它包含所有步驟、正確的 `using` 指示詞，以及優雅的錯誤處理。

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace ReceiptReaderDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Load the image file C#
            // -------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY\receipt.jpg";

            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"❌ Image not found: {imagePath}");
                return;
            }

            Image receiptImage;
            try
            {
                receiptImage = Image.FromFile(imagePath);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"⚠️ Failed to load image: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 2️⃣ Create and configure OCR engine
            // -------------------------------------------------
            OcrEngine ocrEngine = new OcrEngine
            {
                Config =
                {
                    Language = OcrLanguage.English,
                    DetectOrientation = true
                }
            };

            // -------------------------------------------------
            // 3️⃣ Recognize and convert to JSON
            // -------------------------------------------------
            string jsonResult;
            try
            {
                jsonResult = ocrEngine.RecognizeToJson(receiptImage);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"🛑 OCR failed: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 4️⃣ Output results
            // -------------------------------------------------
            Console.WriteLine("🗂️ OCR JSON Result:");
            Console.WriteLine(jsonResult);

            // Optionally persist the JSON
            string outputPath = Path.Combine(
                Path.GetDirectoryName(imagePath) ?? ".", "receipt_output.json");
            File.WriteAllText(outputPath, jsonResult);
            Console.WriteLine($"✅ JSON saved to {outputPath}");
        }
    }
}
```

**執行方式：**  
在專案資料夾執行 `dotnet run`。若設定正確，你會在主控台看到 JSON 輸出，且會儲存於收據圖像旁邊。

---

## 結論

我們剛剛完整說明了在 C# 中**如何讀取收據**圖像的全流程。透過載入圖像、設定 Aspose OCR，並呼叫 `RecognizeToJson`，即可**從圖像中提取文字**並**將圖像轉換為 JSON**，幾乎不需要額外樣板程式碼。此方法具備可擴充性——從單筆收據示範到每晚處理數百張收據的批次處理器皆適用。

接下來你可以探索的方向：

- **解析 JSON** 以抽取日期、總金額與項目（使用 `System.Text.Json` 或 `Newtonsoft.Json`）。
- **整合資料庫**（SQL、Cosmos DB）以自動儲存費用紀錄。
- **加入 UI**（WinForms、WPF 或 Blazor），讓使用者可以拖放收據。
- **將 Aspose OCR 替換**為其他引擎（Tesseract、Microsoft Azure OCR），若授權是顧慮——只要保留相同的「load image file C#」模式。

盡情試驗、挑戰，之後再回來複習。如果遇到問題，社群（以及 Aspose 論壇）都是很好的求助管道。祝程式開發順利，享受將紙本收據轉換成乾淨、可搜尋的資料吧！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}