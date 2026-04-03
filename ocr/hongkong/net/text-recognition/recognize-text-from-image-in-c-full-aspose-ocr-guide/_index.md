---
category: general
date: 2026-04-03
description: 使用 Aspose OCR 在 C# 中辨識圖像文字。學習載入圖像進行 OCR、從圖像提取文字、在 C# 中寫入 JSON 檔案，以及對
  PNG 進行 OCR。
draft: false
keywords:
- recognize text from image
- write json file c#
- load image for ocr
- extract text from image
- perform ocr on png
language: zh-hant
og_description: 在 C# 中使用 Aspose OCR 辨識圖像文字。逐步教學：載入圖像進行 OCR、從圖像擷取文字、在 C# 中寫入 JSON 檔案，以及對
  PNG 進行 OCR。
og_title: 在 C# 中辨識圖像文字 – 完整 Aspose OCR 教學
tags:
- OCR
- C#
- Aspose
title: 在 C# 中從圖像辨識文字 – 完整 Aspose OCR 指南
url: /zh-hant/net/text-recognition/recognize-text-from-image-in-c-full-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中辨識影像文字 – 完整 Aspose OCR 教學

曾經需要 **辨識影像文字**，卻不確定該選哪個函式庫嗎？也許你手上有一批掃描過的收據、PNG 截圖，或是手寫筆記，想要將它們轉換成可搜尋的資料。好消息是：使用 Aspose.OCR 只要幾行 C# 程式碼，就能完成，而且還會產生一個整齊的 JSON 檔案，方便匯入其他系統。

在本教學中，我們將逐步說明如何載入影像進行 OCR、從影像中擷取文字、將結果序列化為 JSON 檔案，最後處理 PNG 檔而不費吹灰之力。完成後，你將擁有一個可直接執行的主控台應用程式，能 **辨識影像文字** 並將結果寫入 *output.json*。

## 需要的環境

- .NET 6.0 或更新版本（此程式碼亦可於 .NET Framework 上執行）
- Aspose.OCR NuGet 套件（`Install-Package Aspose.OCR`）
- 想要處理的 PNG（或任何支援的格式）檔案
- Visual Studio、VS Code，或任何你慣用的 C# 編輯器

不需要額外的第三方函式庫——只需 Aspose OCR 引擎以及內建的 `System.Text.Json` 序列化程式。

## 步驟 1：使用 Aspose OCR 辨識影像文字

首先，你需要建立一個 `OcrEngine` 實例。這個物件在背後負責大量運算。

```csharp
using Aspose.OCR;
using System.Drawing;
using System.IO;
using System.Text.Json;

class JsonExportDemo
{
    static void Main()
    {
        // Initialize the OCR engine – this is where the magic starts.
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image for OCR – replace the path with your own file.
        Image sourceImage = Image.FromFile(@"YOUR_DIRECTORY/input.png");

        // Perform OCR on the loaded image and get a structured result.
        OcrResult ocrResult = ocrEngine.RecognizeToResult(sourceImage);

        // Serialize the result into a nicely indented JSON string.
        string json = JsonSerializer.Serialize(
            ocrResult,
            new JsonSerializerOptions { WriteIndented = true });

        // Write JSON file C# – this will create output.json next to your exe.
        File.WriteAllText(@"YOUR_DIRECTORY/output.json", json);
    }
}
```

**為什麼這很重要：** 只建立一次 `OcrEngine` 並重複使用，比每個檔案都重新建立引擎更有效率。`RecognizeToResult` 會回傳一個 `OcrResult` 物件，已包含擷取的文字、信心分數以及邊框座標——非常適合後續處理。

## 步驟 2：載入影像以進行 OCR – 處理不同格式

Aspose OCR 能讀取 PNG、JPEG、BMP 以及其他多種格式。如果你處理的 PNG 含有透明度，建議先將其展平，以免出現意外的空白。

```csharp
// Optional: flatten PNG with transparency to a white background.
if (sourceImage.RawFormat.Equals(System.Drawing.Imaging.ImageFormat.Png))
{
    Bitmap flat = new Bitmap(sourceImage.Width, sourceImage.Height);
    using (Graphics g = Graphics.FromImage(flat))
    {
        g.Clear(Color.White);
        g.DrawImage(sourceImage, 0, 0);
    }
    sourceImage = flat;
}
```

**小技巧：** 請務必確認影像尺寸合理（例如寬度 > 50 px）。過小的影像會導致 OCR 引擎遺漏字元，進而產生低信心分數。

## 步驟 3：在 C# 中寫入 JSON 檔案 – 讓輸出易於使用

`System.Text.Json` 序列化程式速度快且內建，但若需要自訂轉換器，也可以改用 `Newtonsoft.Json`。上例已設定 `WriteIndented = true`，因此產生的檔案具可讀性。

```csharp
// Expected output (truncated):
{
  "Text": "Hello World",
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Text": "Hello World",
          "Confidence": 0.98,
          "BoundingBox": { "X": 10, "Y": 20, "Width": 120, "Height": 30 }
        }
      ]
    }
  ]
}
```

將 OCR 資料以 JSON 形式保存，可輕鬆匯入資料庫、透過 HTTP 傳送，或供機器學習管線使用。

## 步驟 4：驗證結果 – 快速檢查

程式執行完畢後，開啟 `output.json`，尋找 `"Text"` 欄位。若其內容符合預期，即表示已成功 **從影像擷取文字**。若信心分數偏低，請考慮對影像做前處理（例如提升對比或套用二值化閾值）。

```csharp
Console.WriteLine($"Extracted text: {ocrResult.Text}");
Console.WriteLine($"Overall confidence: {ocrResult.Confidence:P2}");
```

執行主控台程式時會輸出類似以下內容：

```
Extracted text: Hello World
Overall confidence: 98.00%
```

這表示 OCR 已如預期般正常運作。

## 常見陷阱與邊緣案例

| Issue | Why it Happens | How to Fix |
|-------|----------------|------------|
| **空白輸出** | 圖片過暗或使用不支援的色彩空間 | 轉換為灰階、提升亮度，或將 PNG 展平（參見步驟 2） |
| **雜訊字元** | DPI 太低（< 72）或噪點過多 | 放大影像或在傳入 `RecognizeToResult` 前套用去噪濾鏡 |
| **大型檔案導致記憶體壓力** | 將多百萬像素的 PNG 載入 `Bitmap` 會佔用大量 RAM | 分批處理影像或在保持可讀性的前提下縮小尺寸 |
| **JSON 序列化錯誤** | `OcrResult` 含有循環參照（可能性低） | 使用 `JsonSerializerOptions { ReferenceHandler = ReferenceHandler.IgnoreCycles }` |

## 加分項目：在批次迴圈中對 PNG 執行 OCR

如果資料夾中有大量 PNG 檔案，你可以擴充示範程式以逐一處理它們：

```csharp
string[] pngFiles = Directory.GetFiles(@"YOUR_DIRECTORY", "*.png");
foreach (var file in pngFiles)
{
    Image img = Image.FromFile(file);
    OcrResult res = ocrEngine.RecognizeToResult(img);
    string outPath = Path.ChangeExtension(file, ".json");
    File.WriteAllText(outPath, JsonSerializer.Serialize(res, new JsonSerializerOptions { WriteIndented = true }));
    Console.WriteLine($"Processed {Path.GetFileName(file)} → {Path.GetFileName(outPath)}");
}
```

現在程式會一次性 **對 PNG 檔案執行 OCR**，並為每張影像產生對應的 JSON 檔案。

## 結論

你剛剛學會如何在 C# 中使用 Aspose OCR **辨識影像文字**、**載入影像以進行 OCR**、**從影像擷取文字**，以及 **在 C# 中寫入 JSON 檔案** 以儲存結果。完整且可執行的範例涵蓋了所有關鍵步驟，說明了每個環節的重要性，甚至示範了 PNG 特有的處理技巧。

接下來可以嘗試將 JSON 匯入搜尋索引、結合語言偵測，或整合到即時處理上傳檔案的 Web API 中。若你的需求涉及手寫文字，也可以探索 Aspose 提供的手寫辨識功能。

對於邊緣案例或效能調校有任何疑問嗎？歡迎在下方留言——祝開發愉快！ 

![辨識影像文字示範](/images/ocr-demo.png "說明 Aspose OCR 如何辨識影像文字的圖示")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}