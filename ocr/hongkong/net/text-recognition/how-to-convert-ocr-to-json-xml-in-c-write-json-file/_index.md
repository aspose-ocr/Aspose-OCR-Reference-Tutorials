---
category: general
date: 2026-04-01
description: 如何在 C# 中將 OCR 輸出轉換為 JSON 與 XML – 學習從圖像提取文字並使用 Aspose.OCR 寫入 JSON 檔案。
draft: false
keywords:
- how to convert ocr
- extract text from image
- write json file c#
- write xml file c#
- how to extract text
language: zh-hant
og_description: 如何使用 C# 將 OCR 結果轉換為結構化的 JSON 與 XML 檔案。一步步教您從圖像提取文字並寫入 JSON 檔案（C#）。
og_title: 如何在 C# 中將 OCR 轉換為 JSON 與 XML – 寫入 JSON 檔案
tags:
- OCR
- C#
- Aspose
title: 如何在 C# 中將 OCR 轉換為 JSON 與 XML – 寫入 JSON 檔案
url: /zh-hant/net/text-recognition/how-to-convert-ocr-to-json-xml-in-c-write-json-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中將 OCR 轉換為 JSON 與 XML – 寫入 JSON 檔案

**How to convert OCR** 結果成為實際可用的資料，是許多開發者常問的問題。在本教學中，我們將示範如何從影像中擷取文字，將 OCR 輸出轉換成格式化的 JSON 與 XML，然後使用 C# 把這些檔案寫入磁碟。

如果你曾經盯著原始的 OCR 字串想說「一定有更好的儲存方式」，那麼你來對地方了。完成後，你將擁有一個完整、可執行的程式，不僅能 **extract text from image**，還能 **write JSON file C#** 與 **write XML file C#**，輕鬆搞定。

## 你需要的環境

- **.NET 6.0** 或更新版本（程式碼同樣支援 .NET Framework 4.6+）。  
- **Aspose.OCR** NuGet 套件 – 使用 `dotnet add package Aspose.OCR` 安裝。  
- 一張含有文字的影像（例如 `invoice.png`）。  
- 任意你喜歡的 IDE – Visual Studio、Rider 或 VS Code 都可以。

> **Pro tip:** 把影像檔放在專用資料夾（例如 `Resources/`）以保持路徑整潔。

## 步驟 1：設定 OCR Engine – How to Convert OCR

首先，我們建立一個 `OcrEngine` 實例，並告訴它要辨識的語言。大多數情況下 English 已足夠，但你也可以將 `Language.English` 換成任何支援的語言。

```csharp
using Aspose.OCR;
using System.IO;

class JsonXmlOcrDemo
{
    static void Main()
    {
        // Step 1: Initialise the OCR engine for English text
        var ocrEngine = new OcrEngine { Language = Language.English };
```

> **Why this matters:** 使用正確的語言初始化引擎，可大幅提升辨識準確度，尤其是非拉丁文字。

## 步驟 2：辨識文字 – Extract Text from Image

接著把影像傳給引擎。`Recognize` 方法會回傳一個 `OcrResult` 物件，裡面包含原始文字與位置資訊。

```csharp
        // Step 2: Recognise text from the supplied image
        // Replace "YOUR_DIRECTORY/invoice.png" with your actual file path
        var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/invoice.png");
```

如果找不到影像，`Recognize` 會拋出 `FileNotFoundException`。為了簡化示範，我們假設路徑正確；實務上應該使用 try‑catch 包住。

## 步驟 3：將結果轉成 JSON – Write JSON File C#

Aspose.OCR 的序列化非常簡單。`ToJson` 方法接受一個 `indent` 參數，可產生易讀的縮排輸出，這在你要用文字編輯器開啟時特別方便。

```csharp
        // Step 3: Convert OCR result to formatted JSON
        string jsonOutput = ocrResult.ToJson(indent: true);
```

### 預期的 JSON 範例

```json
{
  "Text": "Invoice #12345\nDate: 2024‑03‑31\nTotal: $250.00",
  "Regions": [
    {
      "Bounds": { "X": 10, "Y": 20, "Width": 200, "Height": 30 },
      "Text": "Invoice #12345"
    }
    // … more regions …
  ]
}
```

> **How to extract text**: `Text` 屬性會回傳純文字字串，你可以將它傳給其他服務（搜尋索引、資料庫等）。

## 步驟 4：寫入 JSON – Write JSON File C#（續）

取得 JSON 字串後，只要使用 `File.WriteAllText` 把它寫入檔案即可。此方法預設使用 UTF‑8 編碼。

```csharp
        // Step 4: Save JSON to disk
        File.WriteAllText("YOUR_DIRECTORY/invoice.json", jsonOutput);
```

現在 `invoice.json` 已經和影像放在同一目錄，隨時可供後續處理。

## 步驟 5：將結果轉成 XML – Write XML File C#

如果你的舊系統需要 XML，`ToXml` 方法會幫你完成大部分工作。與 `ToJson` 類似，它也支援縮排輸出。

```csharp
        // Step 5: Convert OCR result to formatted XML
        string xmlOutput = ocrResult.ToXml(indent: true);
```

### 預期的 XML 範例

```xml
<OcrResult>
  <Text>Invoice #12345
Date: 2024-03-31
Total: $250.00</Text>
  <Regions>
    <Region>
      <Bounds X="10" Y="20" Width="200" Height="30" />
      <Text>Invoice #12345</Text>
    </Region>
    <!-- … more regions … -->
  </Regions>
</OcrResult>
```

## 步驟 6：寫入 XML – Write XML File C#（續）

寫入 XML 的方式與寫入 JSON 完全相同，只要把副檔名改成 `.xml` 即可。

```csharp
        // Step 6: Save XML to disk
        File.WriteAllText("YOUR_DIRECTORY/invoice.xml", xmlOutput);
    }
}
```

### 完整範例程式

以下是可直接貼到 Console App 中執行的完整程式碼：

```csharp
using Aspose.OCR;
using System.IO;

class JsonXmlOcrDemo
{
    static void Main()
    {
        // Initialise OCR engine for English
        var ocrEngine = new OcrEngine { Language = Language.English };

        // Recognise text from image
        var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/invoice.png");

        // Convert to JSON and save
        string jsonOutput = ocrResult.ToJson(indent: true);
        File.WriteAllText("YOUR_DIRECTORY/invoice.json", jsonOutput);

        // Convert to XML and save
        string xmlOutput = ocrResult.ToXml(indent: true);
        File.WriteAllText("YOUR_DIRECTORY/invoice.xml", xmlOutput);
    }
}
```

執行程式後，你會在指定位置看到兩個新檔案——`invoice.json` 與 `invoice.xml`。打開它們即可驗證結構是否與上方範例相符。

## 常見問題與邊緣案例

| Question | Answer |
|----------|--------|
| **What if the image contains multiple languages?** | 為每種語言建立獨立的 `OcrEngine` 實例，或在支援時使用 `Language.Multi`。 |
| **Can I control the output format (e.g., exclude region data)?** | 可以。`ToJson` 與 `ToXml` 都接受可選參數來過濾欄位，請參考 Aspose.OCR 文件中的 `ExportOptions`。 |
| **How do I handle large PDFs with many pages?** | 逐頁處理，將結果彙總後再一次序列化。 |
| **Is the output UTF‑8 safe?** | 絕對安全——Aspose.OCR 內部使用 Unicode，`File.WriteAllText` 預設寫入 UTF‑8。 |
| **What about performance?** | OCR 本身相當耗 CPU。大量批次作業建議平行化或使用 Aspose 的雲端 API。 |

## 結論

現在你已掌握 **how to convert OCR** 結果為 JSON 與 XML，並使用 C# **extract text from image**、**write JSON file C#** 以及 **write XML file C#**。只需幾行程式碼，即可快速、可靠地處理任何 Aspose.OCR 支援的影像類型。

準備好接受下一個挑戰了嗎？試著把

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}