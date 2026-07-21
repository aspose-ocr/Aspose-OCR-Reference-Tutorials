---
category: general
date: 2026-07-21
description: 使用 C# OCR 從圖像提取文字 – 學習將 PNG 轉換為文字、載入圖像進行 OCR，以及使用 Aspose 識別西里爾文字。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- extract text from image
- convert png to text
- c# ocr example
- load image for ocr
- recognize cyrillic text
language: zh-hant
lastmod: 2026-07-21
og_description: 使用 C# OCR 從圖像提取文字。本指南展示如何將 PNG 轉換為文字、載入圖像進行 OCR，以及使用 Aspose.OCR 識別西里爾文字。
og_image_alt: Screenshot of C# code extracting text from an image using Aspose OCR
og_title: 在 C# 中從影像提取文字 – 完整 OCR 教學
schemas:
- author: Aspose
  dateModified: '2026-07-21'
  description: Extract text from image using C# OCR – learn to convert PNG to text,
    load image for OCR, and recognize Cyrillic text with Aspose.
  headline: Extract Text from Image in C# – Complete OCR Guide
  type: TechArticle
tags:
- OCR
- C#
- Aspose
- Image Processing
- Cyrillic
title: 從圖像中提取文字（C#）– 完整 OCR 指南
url: /zh-hant/net/text-recognition/extract-text-from-image-in-c-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從影像中提取文字（C#） – 完整 OCR 指南

有沒有想過如何在 C# 專案內**從影像中提取文字**檔案，而不必離開開發環境？也許你手上有一堆掃描收據、一組西里爾字母的標示，或只是需要把 PNG 截圖轉成可搜尋的文字。簡而言之，你需要一個可靠的 OCR 引擎，能即時**將 PNG 轉換為文字**。

好消息——Aspose.OCR 只需幾行程式碼就能做到。以下示範一個**C# OCR 範例**，載入影像、執行辨識，並輸出結果，即使來源語言是西里爾文也不例外。

## 本教學涵蓋內容

- 為西里爾文設定 Aspose.OCR 引擎。  
- **從檔案路徑或串流載入影像以供 OCR**。  
- **將 PNG 轉換為文字**，並輸出純文字字串。  
- 處理失敗情況與常見陷阱，確保**辨識西里爾文字**順利。

完成本指南後，你將擁有一個可即刻執行的自包含程式，以及多項讓 OCR 流程更穩定的技巧。

> **先決條件**  
> - .NET 6.0 或更新版本（此程式碼亦支援 .NET Framework 4.7 以上）。  
> - 有效的 Aspose.OCR 授權或 30 天評估金鑰。  
> - 已安裝 `Aspose.OCR` NuGet 套件（`dotnet add package Aspose.OCR`）。  

若缺少上述任一項，請先取得，其他皆不需額外設定。

---

## 從影像中提取文字 – 步驟 1：安裝與初始化 OCR 引擎

首先，我們需要建立 OCR 引擎實例，並告訴它預期的語言。Aspose 支援超過 70 種語言，西里爾文使用 `OcrLanguage.Cyrillic`。

```csharp
using Aspose.OCR;
using System;

// Step 1: Create the engine and set the language to Cyrillic.
OcrEngine engine = new OcrEngine
{
    Language = OcrLanguage.Cyrillic
};
```

> **為什麼要設定語言？**  
> 若引擎自行猜測錯誤的文字腳本，OCR 準確度會急劇下降。明確指定西里爾文可讓引擎*先行縮小*需要考慮的字元集合，從而加快處理速度並減少誤辨。

---

## 將 PNG 轉換為文字 – 步驟 2：載入影像以供 OCR

現在正式**從檔案載入影像以供 OCR**。範例使用 PNG 檔案，然而 Aspose 亦支援 JPEG、BMP、TIFF，甚至 PDF 頁面。

```csharp
// Step 2: Load the PNG you want to convert to text.
engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/sample_cyrillic.png");
```

如果你想使用 `MemoryStream`（例如影像來自 Web 請求），只需將上述程式碼改為：

```csharp
using (var ms = new MemoryStream(File.ReadAllBytes("sample_cyrillic.png")))
{
    engine.Image = ImageStream.FromStream(ms);
}
```

> **小技巧：** 為取得最佳效果，請將影像解析度保持在至少 300 dpi。低解析度的螢幕截圖常會產生雜亂的輸出，尤其是非拉丁字母時。

---

## C# OCR 範例 – 步驟 3：執行辨識

引擎已就緒且影像已載入，實際的 OCR 工作只需一次方法呼叫。

```csharp
// Step 3: Run the recognition engine.
bool success = engine.Recognize();
```

`Recognize()` 方法在找到可辨識文字時會回傳 `true`。若回傳 `false`，則需要調查原因——可能是影像過於模糊，或語言設定不正確。

---

## 辨識西里爾文字 – 步驟 4：取得並使用結果

假設辨識成功，你現在可以**從影像中提取文字**，再依需求儲存至資料庫、送入搜尋索引，或直接顯示。

```csharp
if (success)
{
    // Step 4: Grab the plain text.
    string plainText = engine.Text;
    Console.WriteLine("=== OCR RESULT ===");
    Console.WriteLine(plainText);
}
else
{
    // Step 5: Handle recognition failure gracefully.
    Console.WriteLine("Recognition failed. Check image quality or language settings.");
}
```

### 預期輸出

對清晰的西里爾文 PNG 執行完整程式後，會得到類似以下的結果：

```
=== OCR RESULT ===
Пример текста на кириллице
```

若影像同時包含英文與西里爾文，只要語言設定為 `Cyrillic`（它已內含拉丁子集），Aspose 會同時輸出兩種腳本。

---

## 常見陷阱與專業技巧

| 問題 | 為何會發生 | 解決方法 |
|------|------------|----------|
| **模糊或低解析度 PNG** | OCR 引擎需要清晰的字元邊緣。 | 將影像升級至 300 dpi，或在送給 Aspose 前套用銳化濾鏡。 |
| **語言設定錯誤** | 引擎會嘗試匹配錯誤的文字腳本。 | 永遠將 `engine.Language` 設為預期語言，例如 `OcrLanguage.Cyrillic`。 |
| **大型檔案導致記憶體壓力** | 把巨大的影像載入 `MemoryStream` 可能耗盡堆積空間。 | 使用 `engine.Image = ImageStream.FromFile(path)` 直接在磁碟上處理，或分批處理頁面。 |
| **辨識回傳空字串** | 引擎可能未偵測到任何文字區域。 | 在 `Recognize()` 前呼叫 `engine.SetImageProcessingOptions(new ImageProcessingOptions { DetectTextRegions = true })`。 |

> **專業小技巧：** 若需批次**從影像中提取文字**，可將上述邏輯包在 `Parallel.ForEach` 迴圈中——只要確保每個執行緒自行建立 `OcrEngine` 實例即可，因為引擎本身不支援多執行緒共用。

---

## 延伸範例：多語言與非同步呼叫

上述程式碼為同步範例，且僅聚焦於西里爾文。實務上可能同時需要支援英文與西里爾文。Aspose 允許設定*語言陣列*：

```csharp
engine.Language = OcrLanguage.Cyrillic | OcrLanguage.English;
```

若是需要 UI 不卡頓的應用程式，可改用 `RecognizeAsync()`：

```csharp
await engine.RecognizeAsync();
string result = engine.Text; // same property, now filled after await
```

使用此方式時，請將 `Main` 方法宣告為 `async Task`。

---

## 完整可執行範例

以下提供完整、可直接複製貼上的程式。存為 `Program.cs`、加入 Aspose.OCR NuGet 套件，然後在命令列執行。

```csharp
using Aspose.OCR;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine and set language to Cyrillic.
        OcrEngine engine = new OcrEngine
        {
            Language = OcrLanguage.Cyrillic
        };

        // 2️⃣ Load the PNG you want to convert to text.
        //    Replace the path with your actual file location.
        string imagePath = "YOUR_DIRECTORY/sample_cyrillic.png";

        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"File not found: {imagePath}");
            return;
        }

        engine.Image = ImageStream.FromFile(imagePath);

        // 3️⃣ Perform the recognition.
        bool success = engine.Recognize();

        // 4️⃣ Retrieve and display the result.
        if (success)
        {
            string plainText = engine.Text;
            Console.WriteLine("=== OCR RESULT ===");
            Console.WriteLine(plainText);
        }
        else
        {
            Console.WriteLine("Recognition failed. Verify image quality and language settings.");
        }
    }
}
```

**執行方式：**  

```bash
dotnet run
```

執行後，應在主控台看到提取出的西里爾文字。

---

## 結論

我們已示範一個**C# OCR 範例**，說明如何使用 Aspose.OCR **從影像中提取文字**，尤其是 PNG 轉文字的流程。透過設定語言為西里爾文、正確載入影像，以及妥善處理成功與失敗的情況，你現在已具備穩固的基礎，能應付任何文字提取任務——無論是為搜尋索引將 PNG 轉文字，或是建置多語系文件掃描器。

準備好下一步了嗎？試著把 `OcrLanguage.Cyrillic` 換成 `OcrLanguage.English` 看看差異，或是調整 `ImageProcessingOptions` 以提升雜訊掃描的準確度。若遇到問題，Aspose 官方文件與社群論壇都是深入探索的好資源。

祝程式開發順利，願你的 OCR 結果永遠清晰無比！


## 接下來該學什麼？

以下教學與本指南緊密相關，能進一步擴展本篇示範的技巧。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在專案中探索其他實作方式。

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}