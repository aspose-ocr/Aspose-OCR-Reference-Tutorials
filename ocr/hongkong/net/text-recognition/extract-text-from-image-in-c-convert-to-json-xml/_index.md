---
category: general
date: 2026-04-26
description: 使用 Aspose.OCR 在 C# 中從圖像提取文字，並在幾分鐘內學會將圖像轉換為 JSON 與 XML 格式。
draft: false
keywords:
- extract text from image
- convert image to json
- convert image to xml
- Aspose OCR C#
- image to JSON C#
- image to XML C#
language: zh-hant
og_description: 使用 Aspose.OCR 在 C# 中從圖像擷取文字。一步一步學習如何即時將結果轉換為 JSON 與 XML。
og_title: 在 C# 中從圖像提取文字 – 轉換為 JSON 與 XML
tags:
- OCR
- C#
- Aspose
- JSON
- XML
title: 在 C# 中從圖片提取文字 – 轉換為 JSON 與 XML
url: /zh-hant/net/text-recognition/extract-text-from-image-in-c-convert-to-json-xml/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從圖片中提取文字（C#） – 轉換為 JSON 與 XML

是否曾在 .NET 專案中需要 **從圖片中提取文字**，卻卡在「到底要怎樣取得資料？」這一步？你並不孤單。在許多實務應用中——例如發票處理、收據掃描或證件驗證——從圖片中抽取原始字元是第一個且關鍵的步驟。  

好消息是？使用 Aspose.OCR 只需幾行程式碼，即可即時 **將圖片轉換為 JSON** 或 **將圖片轉換為 XML**，供下游系統使用。本指南將逐步說明完整、可直接執行的程式碼，解釋每個部分的意義，並提供避免常見陷阱的小技巧。

---

## 需要的條件

- **.NET 6+**（任何近期的 SDK 都可使用；範例以 .NET 6 為目標）
- **Aspose.OCR for .NET** NuGet 套件  
  ```bash
  dotnet add package Aspose.OCR
  ```
- 一個包含可列印文字的影像檔（PNG、JPG 等），此處以 `invoice.png` 為例。
- 程式碼編輯器——Visual Studio、VS Code 或 Rider——隨你喜好。

就這樣。無需額外的 OCR 引擎，亦不需外部服務，只要一個 NuGet 套件即可。

---

## 步驟 1：設定 OCR 引擎 – 如何從圖片中提取文字

首先，我們建立 `OcrEngine` 實例並指向影像檔。此步驟是基礎；若未正確載入影像，引擎將無法辨識任何內容。

```csharp
using Aspose.OCR;
using System.IO;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Load the image you want to process
// Replace YOUR_DIRECTORY with the actual folder path
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/invoice.png");

// Optional: verify the image was loaded
if (ocrEngine.Image == null)
{
    throw new FileNotFoundException("Image not found. Check the path and filename.");
}
```

**為何重要：**  
- `OcrEngine` 封裝了所有低階的影像前處理（二值化、去斜）。  
- 透過 `ImageStream.FromFile` 載入影像可確保引擎讀取到精確的位元組，保留 DPI 與色彩深度——這兩者皆會影響辨識準確度。

> **專業提示：** 若來源影像是以串流形式（例如透過 Web API 上傳），請使用 `ImageStream.FromStream(yourStream)` 取代 `FromFile`。

---

## 步驟 2：告訴引擎預期的語言 – 精確提取圖片文字

Aspose.OCR 支援多種字母。指定正確的語言可縮小字元集合，提升辨識準確度。

```csharp
// Set the language; Latin covers English, French, German, etc.
ocrEngine.Language = Language.Latin;
```

**原因：**  
設定 `Language.Latin` 後，OCR 引擎會忽略西里爾文或亞洲字形，減少誤判。若日後需處理多語言文件，可改用 `Language.Multilingual` 或結合多種語言。

---

## 步驟 3：執行辨識程序 – 一次呼叫即可提取圖片文字

現在開始實際辨識文字。`Recognize` 方法會回傳 `RecognitionResult` 物件，內含原始文字、信心分數，甚至版面配置資料。

```csharp
// Perform OCR
RecognitionResult recognitionResult = ocrEngine.Recognize();

// Quick sanity check
if (recognitionResult == null || string.IsNullOrWhiteSpace(recognitionResult.Text))
{
    Console.WriteLine("No text was detected. Verify the image quality.");
    return;
}

// Print the raw extracted text to the console
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(recognitionResult.Text);
```

**為何這樣做：**  
只需呼叫一次 `Recognize` 即可，因為引擎在內部已完成前處理、分割與字元分類。`Text` 屬性會提供純文字字串，適合用於日誌或快速驗證。

---

## 步驟 4：將結果轉換為 JSON – 輕鬆將圖片轉為 JSON

許多現代服務偏好 JSON 資料。Aspose.OCR 提供便利的 `ToJson` 方法，將完整的 `RecognitionResult` 序列化，包括信心值與邊界框。

```csharp
// Serialize the result to JSON
string jsonResult = recognitionResult.ToJson();

// Save the JSON to a file
File.WriteAllText("YOUR_DIRECTORY/invoice.json", jsonResult);

Console.WriteLine("JSON file saved at YOUR_DIRECTORY/invoice.json");
```

**為何可能需要 JSON：**  
- **相容性：** 前端應用程式（React、Angular）可直接使用此 JSON。  
- **除錯：** JSON 包含每個字元的信心值，讓你能標記低信心的詞彙以供人工審核。

> **特殊情況：** 若下游系統僅需純文字，可擷取 `recognitionResult.Text`，再自行包裝成自訂的 JSON 物件，而非使用完整的 Aspose 負載。

---

## 步驟 5：將結果轉換為 XML – 為舊有系統將圖片轉為 XML

部分企業仍依賴 XML 結構進行資料交換。`ToXml` 方法與 `ToJson` 類似，但輸出 XML。

```csharp
// Serialize the result to XML
string xmlResult = recognitionResult.ToXml();

// Save the XML to a file
File.WriteAllText("YOUR_DIRECTORY/invoice.xml", xmlResult);

Console.WriteLine("XML file saved at YOUR_DIRECTORY/invoice.xml");
```

**為何使用 XML：**  
- **結構驗證：** 你可以定義符合 Aspose 輸出結構的 XSD，確保合約符合性。  
- **整合性：** 舊版 ERP 或文件管理系統通常內建 XML 解析功能。

---

## 完整範例程式 – 一站式程式碼

以下為完整程式，將所有步驟串接起來。將其複製貼上至新的主控台專案（`dotnet new console`）後執行。

```csharp
using Aspose.OCR;
using System;
using System.IO;

namespace ImageOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Initialize OCR engine and load the image
            // -------------------------------------------------
            OcrEngine ocrEngine = new OcrEngine();
            // Adjust the path to point at your PNG/JPG file
            string imagePath = "YOUR_DIRECTORY/invoice.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            if (ocrEngine.Image == null)
            {
                Console.WriteLine($"Unable to load image at {imagePath}");
                return;
            }

            // -------------------------------------------------
            // Step 2: Specify language (Latin for most European scripts)
            // -------------------------------------------------
            ocrEngine.Language = Language.Latin;

            // -------------------------------------------------
            // Step 3: Run OCR and get the result
            // -------------------------------------------------
            RecognitionResult result = ocrEngine.Recognize();

            if (result == null || string.IsNullOrWhiteSpace(result.Text))
            {
                Console.WriteLine("No text detected – check image quality or language setting.");
                return;
            }

            Console.WriteLine("=== Extracted Text ===");
            Console.WriteLine(result.Text);
            Console.WriteLine();

            // -------------------------------------------------
            // Step 4: Convert to JSON (convert image to json)
            // -------------------------------------------------
            string json = result.ToJson();
            string jsonPath = "YOUR_DIRECTORY/invoice.json";
            File.WriteAllText(jsonPath, json);
            Console.WriteLine($"JSON output written to {jsonPath}");

            // -------------------------------------------------
            // Step 5: Convert to XML (convert image to xml)
            // -------------------------------------------------
            string xml = result.ToXml();
            string xmlPath = "YOUR_DIRECTORY/invoice.xml";
            File.WriteAllText(xmlPath, xml);
            Console.WriteLine($"XML output written to {xmlPath}");
        }
    }
}
```

**預期輸出（主控台）：**

```
=== Extracted Text ===
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
...

JSON file saved at YOUR_DIRECTORY/invoice.json
XML file saved at YOUR_DIRECTORY/invoice.xml
```

JSON 與 XML 檔案將包含更豐富的結構，例如：

```json
{
  "Text": "Invoice #12345\nDate: 2024‑03‑15\nTotal: $1,250.00",
  "Confidence": 0.96,
  "Blocks": [
    { "Text": "Invoice #12345", "Confidence": 0.98, "Rectangle": { "X": 12, "Y": 30, "Width": 200, "Height": 20 } },
    ...
  ]
}
```

```xml
<RecognitionResult>
  <Text>Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00</Text>
  <Confidence>0.96</Confidence>
  <Blocks>
    <Block>
      <Text>Invoice #12345</Text>
      <Confidence>0.98</Confidence>
      <Rectangle X="12" Y="30" Width="200" Height="20"/>
    </Block>
    ...
  </Blocks>
</RecognitionResult>
```

---

## 常見問題與特殊情況

### 若影像模糊或旋轉該怎麼辦？

Aspose.OCR 會自動校正大多數影像的傾斜，但在極端情況下，你可能需要先以 `ocrEngine.Image = ImageProcessor.Deskew(ocrEngine.Image)` 進行前處理。加入少量對比度提升（`ImageProcessor.AdjustContrast`）亦可提升信心分數。

### 我可以從 PDF 中提取文字嗎？

可以——先將每頁 PDF 轉為影像（例如使用 Aspose.PDF 或免費的 PDFium 等函式庫），再將這些影像投入相同的 OCR 流程。

### 如何在同一文件中處理多種語言？

設定 `ocrEngine.Language = Language.Multilingual;` 或結合特定語言：

```csharp
ocrEngine.Language = Language.English | Language.French | Language.German;
```

請留意，較廣泛的語言集合可能會

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}