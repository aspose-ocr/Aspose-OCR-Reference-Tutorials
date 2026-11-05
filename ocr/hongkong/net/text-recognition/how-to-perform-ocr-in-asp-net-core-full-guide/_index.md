---
category: general
date: 2026-05-28
description: 如何在 ASP.NET Core 中執行 OCR——學習上載圖片、從圖片提取文字，並有效率地處理檔案上載。
draft: false
keywords:
- how to perform OCR
- extract text from image
- handle file upload
- how to upload file
- upload image OCR
language: zh-hant
og_description: 如何在 ASP.NET Core 中執行 OCR。一步一步學習如何上傳圖片、從圖片中擷取文字，以及使用 Aspose OCR 處理檔案上傳。
og_title: 如何在 ASP.NET Core 中執行 OCR – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: How to perform OCR in ASP.NET Core—learn to upload image, extract text
    from image, and handle file upload efficiently.
  headline: How to Perform OCR in ASP.NET Core – Full Guide
  type: TechArticle
tags:
- OCR
- ASP.NET Core
- C#
- file upload
title: 如何在 ASP.NET Core 中執行 OCR – 完整指南
url: /zh-hant/net/text-recognition/how-to-perform-ocr-in-asp-net-core-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 ASP.NET Core 中執行 OCR – 完整指南

有沒有想過 **如何在現代 Web API 中執行 OCR** 而不讓自己抓狂？你並不是唯一有此困擾的人。開發者常常需要讓使用者上傳圖片——可能是收據、護照掃描件或手寫筆記——然後以 JSON 形式取得原始文字。  

在本教學中，我們將一步步示範完整、可投入生產環境的解決方案，說明 **如何上傳檔案**、驗證檔案、執行 Aspose OCR，最後 **從影像中擷取文字**。完成後，你將擁有一個可直接貼入任何 ASP.NET Core 專案的控制器。

## 您將建立的內容

- 一個接受 multipart/form‑data 上傳的 `OcrController`
- 驗證檔案確實存在且不為空
- 使用 Aspose OCR 引擎的非同步 OCR 處理
- 包含辨識文字的簡潔 JSON 回應

## 前置條件（開始前需要的項目）

| Requirement | Why It Matters |
|-------------|----------------|
| .NET 6 SDK or later | ASP.NET Core 6+ 提供最小 API 功能與非同步支援。 |
| Visual Studio 2022 (or VS Code) | IDE 讓除錯更方便，但任何編輯器皆可使用。 |
| Aspose.OCR NuGet package (`dotnet add package Aspose.OCR`) | 真正執行 OCR 工作的引擎。 |
| Basic knowledge of ASP.NET Core MVC | 我們將使用 `ControllerBase` 與路由屬性。 |

如果你已具備上述條件，太好了——讓我們開始吧。

## 步驟 1：設定專案並安裝 Aspose OCR

在終端機中開啟並建立一個全新的 Web API 專案：

```bash
dotnet new webapi -n OcrDemo
cd OcrDemo
dotnet add package Aspose.OCR
```

那條指令會把 OCR 函式庫及其所有相依套件一起拉下來。無需額外設定；Aspose 可直接支援常見影像格式。

## 步驟 2：新增 OCR 控制器（**如何執行 OCR** 的核心）

建立新檔案 `Controllers/OcrController.cs`，並貼上以下程式碼。這是完整、可執行的範例——沒有遺漏任何部份。

```csharp
using Aspose.OCR;
using Microsoft.AspNetCore.Mvc;
using System.Threading.Tasks;

namespace OcrDemo.Controllers
{
    [ApiController]
    [Route("[controller]")]
    public class OcrController : ControllerBase
    {
        // Step 1: Receive the uploaded file from the request
        [HttpPost("upload")]
        public async Task<IActionResult> Upload([FromForm] IFormFile uploadedFile)
        {
            // Step 2: Validate that a file was actually provided
            if (uploadedFile == null || uploadedFile.Length == 0)
                return BadRequest("No file supplied.");

            // Step 3: Open a read‑only stream for the file content
            await using var fileStream = uploadedFile.OpenReadStream();

            // Step 4: Create the OCR engine and load the image from the stream
            var ocrEngine = new OcrEngine();
            ocrEngine.Image = ImageStream.FromStream(fileStream);

            // Step 5: Perform asynchronous text recognition
            string extractedText = await ocrEngine.RecognizeAsync();

            // Step 6: Return the recognized text in the response
            return Ok(new { extractedText });
        }
    }
}
```

### 為什麼這樣可行

- **`[FromForm] IFormFile`** 告訴 ASP.NET Core 將 multipart 檔案部份繫結至 `uploadedFile`。這是 Web API 中 **處理檔案上傳** 的經典做法。  
- `if` 判斷式確保我們能優雅地 **處理檔案上傳** 錯誤，若客戶端忘記傳檔案則回傳 400 Bad Request。  
- `using var fileStream = uploadedFile.OpenReadStream();` 會開啟一個*唯讀*串流，對於大型檔案相當重要——不必一次將整張影像載入記憶體。  
- `ocrEngine.Image = ImageStream.FromStream(fileStream);` 直接將串流餵入 Aspose OCR，保持管線簡潔。  
- `await ocrEngine.RecognizeAsync();` 在背景執行繁重的辨識工作，使 API 保持回應。這就是 **如何非同步執行 OCR** 的核心。  
- 最後，我們將結果包裝成 JSON 物件 (`{ extractedText }`)——非常適合前端消費。

## 步驟 3：設定請求大小限制（可選但實用）

如果你預期會收到高解析度的掃描檔，請提升預設的請求大小限制。將以下程式碼加入 `Program.cs`：

```csharp
builder.Services.Configure<FormOptions>(options =>
{
    options.MultipartBodyLengthLimit = 50 * 1024 * 1024; // 50 MB
});
```

現在 API 不會在 10 MB 的收據影像上卡住。請依實際需求調整此上限。

## 步驟 4：使用 cURL 或 Postman 測試端點

以下是一個可直接在終端機執行的 cURL 指令：

```bash
curl -X POST http://localhost:5000/ocr/upload \
  -F "uploadedFile=@/path/to/your/image.png"
```

你應該會看到類似以下的 JSON 回傳內容：

```json
{
  "extractedText": "Sample text that was on the image."
}
```

若影像中沒有可辨識的字元，字串會是空的——不會當機，只是回傳空結果。這是值得留意的邊緣案例。

## 步驟 5：視覺確認（可選圖片）

以下是一張示意截圖，展示成功執行 OCR 後所收到的 JSON 回應。

![How to perform OCR result – screenshot of JSON response showing extracted text](/images/ocr-result.png)

*Alt text:* **如何執行 OCR 結果 – 顯示提取文字的 JSON 回應截圖**

## 常見陷阱與專業提示

| Pitfall | Solution |
|---------|----------|
| **不支援的影像格式**（例如多頁 TIFF） | 先轉成 PNG/JPEG，或在送入 `OcrEngine` 前使用 Aspose 的 `ImageConverter`。 |
| **大型檔案造成記憶體壓力** | 如範例使用串流處理；避免將 `IFormFile` 複製到 `MemoryStream`。 |
| **OCR 回傳亂碼** | 確保影像對比度高且方向正確；必要時使用 `ocrEngine.Preprocess()` 前處理。 |
| **多個同時請求** | Aspose OCR 為執行緒安全，但若伺服器記憶體受限，可使用 semaphore 限制併發數量。 |

## 擴充範例：批次上傳與平行處理

如果需要一次 **處理檔案上傳** 多張影像，請將動作簽章改為接受清單：

```csharp
[HttpPost("batch")]
public async Task<IActionResult> BatchUpload([FromForm] List<IFormFile> files)
{
    if (files == null || !files.Any())
        return BadRequest("No files supplied.");

    var results = new List<object>();

    foreach (var file in files)
    {
        await using var stream = file.OpenReadStream();
        var engine = new OcrEngine { Image = ImageStream.FromStream(stream) };
        var text = await engine.RecognizeAsync();
        results.Add(new { fileName = file.FileName, extractedText = text });
    }

    return Ok(results);
}
```

現在你可以 **批次上傳影像 OCR**——非常適合一次掃描整個收據資料夾。

## 安全性考量

- **驗證檔案副檔名**（`.png`、`.jpg`、`.jpeg`）以避免惡意上傳。  
- **掃描病毒**，若 API 暴露於網際網路，請整合如 ClamAV 等服務。  
- **速率限制** 端點，以防止拒絕服務攻擊。

## 預期輸出與驗證方式

當你以包含「Hello」字樣的清晰影像呼叫 `/ocr/upload` 端點時，回應應為：

```json
{
  "extractedText": "Hello"
}
```

你可以透過開啟瀏覽器的開發者工具 → Network 分頁，或檢查 cURL 輸出，快速驗證結果。

## 重點回顧 – 我們涵蓋的內容

- 設定 ASP.NET Core 專案並加入 Aspose OCR NuGet 套件。  
- 實作一個乾淨的控制器，示範 **如何執行 OCR**、**處理檔案上傳** 與 **從影像中擷取文字**。  
- 討論錯誤處理、效能調校與安全性最佳實踐。  
- 提供可直接執行的程式碼範例，另附批次上傳變體。

## 接下來可以做什麼？

- **加入語言支援**：Aspose OCR 可設定不同語言（`ocrEngine.Language = Language.English;`）。  
- **整合資料庫**：將擷取的文字與其他中繼資料一起儲存，供日後搜尋。  
- **前端 UI**：打造簡易的 React 或 Blazor 頁面，讓使用者拖放影像即時看到 OCR 結果。

盡情實驗吧——換掉 OCR 引擎、嘗試不同的影像前處理步驟，或將結果串接至下游 AI 模型。只要掌握 **如何在現代 .NET 堆疊中執行 OCR**，一切皆有可能。

祝編程愉快，願你的文字永遠清晰可辨！

## 相關教學

- [如何 OCR 圖片 – 在 OCR 圖像辨識中執行 OCR](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)
- [如何使用 Aspose 從串流辨識影像於 OCR 圖像辨識](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [如何設定 OCR 圖像辨識的閾值](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}