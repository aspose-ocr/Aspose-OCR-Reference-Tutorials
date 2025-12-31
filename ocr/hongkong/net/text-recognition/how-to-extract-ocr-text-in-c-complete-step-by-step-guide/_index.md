---
category: general
date: 2025-12-30
description: 學習如何使用 C# 從圖像提取 OCR 文字。本教學涵蓋從圖像檔案提取文字、從 PNG 讀取文字，並包含完整的 C# OCR 教學。
draft: false
keywords:
- how to extract ocr
- extract text from image
- read text from png
- c# ocr tutorial
language: zh-hant
og_description: 如何使用 C# 從圖片中提取 OCR 文字。跟隨本 C# OCR 教學，輕鬆讀取 PNG 檔案中的文字並提取圖片文字。
og_title: 如何在 C# 中提取 OCR 文字 – 完整指南
tags:
- OCR
- C#
- Aspose
title: 如何在 C# 中提取 OCR 文字 – 完整逐步指南
url: /zh-hant/net/text-recognition/how-to-extract-ocr-text-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中擷取 OCR 文字 – 完整逐步教學

有沒有想過 **如何擷取 OCR** 文字，卻不想花上數小時寫自訂的解析程式？你並不是唯一有此需求的人。在許多實務專案中——例如發票處理、護照掃描或舊檔案數位化——都需要一個可靠的方式，從影像檔案中抽取文字。好消息是，只要使用 Aspose.OCR，幾行 C# 程式碼就能搞定。

在本教學中，我們將示範一個 **c# ocr tutorial**，教你如何 **從影像擷取文字**（以 PNG 為例），以及如何 **從 png 讀取文字**，同時保留每個字元的中繼資料。完成後，你將擁有一個可直接執行的 Console 應用程式，會在螢幕上印出包含 Aspose 所擷取全部資訊的格式化 JSON 字串。

> **先備條件**  
> • 已安裝 .NET 6.0 或更新版本  
> • Visual Studio 2022（或任意你慣用的 IDE）  
> • Aspose.OCR for .NET NuGet 套件（`Aspose.OCR`）  

如果上述條件都已備妥，讓我們開始吧。

---

## 如何在 C# 中從影像擷取 OCR 文字 – 建立專案

在撰寫程式碼之前，我們需要先建立一個乾淨的專案，並加入正確的相依套件。

```bash
# Create a new console app
dotnet new console -n OcrDemo
cd OcrDemo

# Add Aspose.OCR package
dotnet add package Aspose.OCR
```

> **小技巧：** 若使用 Visual Studio，可透過 NuGet 套件管理員 UI 加入套件——只要搜尋「Aspose.OCR」即可。

套件安裝完成後，開啟 `Program.cs`。你會看到預設的 `Main` 方法，等著我們填入程式碼。

---

## 步驟 1 – 初始化 OCR 引擎（為何重要）

OCR 引擎是整個流程的核心。初始化它可以告訴 Aspose 稍後要使用哪種語言模型。

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create the OCR engine instance
            var ocrEngine = new OcrEngine();

            // The rest of the steps will follow here...
        }
    }
}
```

*為什麼要這麼做？*  
建立 `OcrEngine` 物件會配置影像分析所需的資源。若沒有這個物件，就無法將影像餵給引擎，程式庫也無法套用其先進的模式辨識演算法。

---

## 步驟 2 – 載入英文語言模型（從影像擷取文字）

Aspose 內建多種語言套件。載入正確的語言模型可以大幅提升辨識準確度。

```csharp
// Step 2: Load the English language model
ocrEngine.LoadLanguage(LanguageModel.English);
```

如果你需要 **從 png 讀取文字**，且影像使用其他語言，只要將 `LanguageModel.English` 替換成相對應的列舉值（例如 `LanguageModel.French`）。這種彈性正是 Aspose 在全球化應用中受歡迎的原因。

---

## 步驟 3 – 從 PNG 檔案辨識文字（Read Text from PNG）

現在把引擎指向實際的影像檔。示範用的 PNG 檔名為 `form_image.png`，請放在相對於執行檔的 `YOUR_DIRECTORY` 資料夾內。

```csharp
// Step 3: Perform OCR on the image
var recognitionResult = ocrEngine.Recognize("YOUR_DIRECTORY/form_image.png");
```

> **如果找不到檔案會怎樣？**  
> `Recognize` 方法會拋出 `FileNotFoundException`。在正式環境建議使用 try‑catch 包住呼叫，以實作更友善的錯誤處理。

---

## 步驟 4 – 轉換結果為美化的 JSON（為何使用 JSON？）

Aspose 會回傳一個豐富的 `RecognitionResult` 物件，裡面不只包含純文字，還有邊框座標、信心分數與行資訊。將其序列化為 JSON，方便記錄、儲存或透過 API 傳遞。

```csharp
// Step 4: Serialize the result to a nicely indented JSON string
string json = JsonResult.FromRecognitionResult(recognitionResult)
                        .ToString(prettyPrint: true);

// Optional: Write the JSON to a file for later inspection
System.IO.File.WriteAllText("ocr_output.json", json);
```

`prettyPrint: true` 參數會加入換行與縮排，非常適合除錯使用。若只需要原始文字，也可以直接取用 `recognitionResult.Text`。

---

## 步驟 5 – 在主控台顯示 JSON 輸出（檢視結果）

最後，我們把 JSON 印到主控台，讓你能確認一切運作正常。

```csharp
// Step 5: Output the JSON to the console
Console.WriteLine(json);
```

執行程式後，應會看到類似以下（為簡潔起見已截斷）的輸出：

```json
{
  "Text": "John Doe\n123 Main St\nAnytown, USA",
  "Characters": [
    {
      "Value": "J",
      "Confidence": 0.99,
      "Bounds": { "X": 12, "Y": 8, "Width": 10, "Height": 14 }
    },
    // ... more character objects ...
  ],
  "Lines": [
    { "Text": "John Doe", "Confidence": 0.98 },
    { "Text": "123 Main St", "Confidence": 0.97 },
    { "Text": "Anytown, USA", "Confidence": 0.96 }
  ]
}
```

留意每個字元的中繼資料——這是 Aspose 相較於許多免費 OCR 函式庫的額外價值。你現在可以過濾低信心的字元，或將文字映射回原始影像以進行高亮顯示。

---

## 完整範例（一次呈現全部步驟）

以下是可直接複製貼上的完整程式碼，沒有遺漏任何部份。

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // Step 2: Load the English language model
            ocrEngine.LoadLanguage(LanguageModel.English);

            // Step 3: Recognize text from the PNG image
            var recognitionResult = ocrEngine.Recognize("YOUR_DIRECTORY/form_image.png");

            // Step 4: Convert the result to pretty‑printed JSON
            string json = JsonResult.FromRecognitionResult(recognitionResult)
                                    .ToString(prettyPrint: true);

            // Optional: Save JSON to a file
            System.IO.File.WriteAllText("ocr_output.json", json);

            // Step 5: Display the JSON output
            Console.WriteLine(json);
        }
    }
}
```

將此檔案存為 `Program.cs`，放入 PNG，執行 `dotnet run`，即可在主控台看到 JSON 輸出。

---

## 常見問題與邊緣案例（解答「如果…」）

### 如果影像是 JPEG 而不是 PNG？

`Recognize` 方法接受 Aspose 支援的任何格式（JPEG、BMP、TIFF 等）。只要在路徑中改成相應的副檔名即可。

### 如何提升低解析度掃描的辨識精度？

1. **前處理影像** – 提高對比度、轉為灰階或套用銳化濾鏡。  
2. **使用較高解析度的原始檔** – OCR 引擎通常需要至少 300 dpi 才能得到可靠結果。  
3. **啟用自動旋轉** – 在辨識前呼叫 `ocrEngine.AutoRotate = true;`。

### 我只想取得純文字，不要 JSON，怎麼做？

可以在 `Recognize` 後直接讀取 `recognitionResult.Text`：

```csharp
Console.WriteLine(recognitionResult.Text);
```

### 能否從多頁 PDF 中擷取文字？

Aspose.OCR 只能處理影像，但你可以結合 Aspose.PDF，先把每一頁 PDF 轉成影像，再將這些影像交給 OCR 引擎逐頁辨識。

---

## 強化 c# OCR 教學的實用技巧

- **釋放資源**：若大量處理影像，請將 `OcrEngine` 包在 `using` 區塊中，以即時釋放原生資源。  
- **批次處理**：對於大型資料夾，可使用 `Directory.GetFiles` 逐一列舉檔案，並在每次呼叫時加入 try‑catch，避免單一失敗檔案中斷整個流程。  
- **記錄**：保留信心分數；在需要人工審核時，可快速標記低品質結果。  
- **執行緒安全**：`OcrEngine` **不**支援多執行緒共享。若要平行化，請為每條執行緒建立獨立的實例。

---

## 結論

你已學會如何使用 C# 透過 Aspose.OCR **擷取 OCR** 文字。只要初始化 OCR 引擎、載入適當的語言模型、辨識 PNG，並將結果序列化為美化的 JSON，即可為任何文件數位化專案奠定堅實基礎。此 **c# ocr tutorial** 同時說明了 **從影像擷取文字**、**從 png 讀取文字**，以及常見的問題處理方式。

準備好進一步挑戰了嗎？試著把一批掃描發票投入同樣的流程，實驗不同語言套件，或將 JSON 輸出整合至可搜尋的資料庫。未來的可能性無限，而你剛寫好的程式碼，就是起飛的發射台。

如果本指南對你有幫助，歡迎分享給同事、為專案加星，或在下方留言分享你的 OCR 成功案例。祝開發順利！

![how to extract ocr example](https://example.com/ocr-demo.png "how to extract ocr example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}