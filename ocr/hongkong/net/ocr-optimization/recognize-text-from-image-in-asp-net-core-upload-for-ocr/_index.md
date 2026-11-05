---
category: general
date: 2026-06-28
description: 在 ASP.NET Core 中辨識圖像文字 – 學習如何上傳圖像以進行 OCR，並有效率地從串流處理 OCR 圖像。
draft: false
keywords:
- recognize text from image
- upload image for ocr
- ocr image from stream
language: zh-hant
og_description: 在 ASP.NET Core 中使用 Aspose OCR 進行圖像文字辨識。上傳圖片進行 OCR，從串流處理 OCR 圖像，並回傳純文字。
og_title: 在 ASP.NET Core 中從圖像辨識文字 – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: recognize text from image in ASP.NET Core – learn how to upload image
    for OCR and process ocr image from stream efficiently.
  headline: recognize text from image in ASP.NET Core – upload for OCR
  type: TechArticle
- description: recognize text from image in ASP.NET Core – learn how to upload image
    for OCR and process ocr image from stream efficiently.
  name: recognize text from image in ASP.NET Core – upload for OCR
  steps:
  - name: Why This Pattern Works
    text: '- **Single `OcrEngine` instance**: Instantiating the engine once avoids
      the overhead of loading language data on every request. - **Async everything**:
      By using `await` on `FromStreamAsync` and `RecognizeAsync`, the ASP.NET Core
      thread pool stays free to serve other callers. - **`IFormFile` binding*'
  - name: Edge Cases to Watch
    text: '- **Corrupt files**: If the uploaded file isn’t a valid image, `FromStreamAsync`
      throws an exception. Wrap the call in a try/catch if you need graceful error
      messages. - **Unsupported formats**: Aspose supports PNG, JPEG, BMP, TIFF, etc.
      If you need PDF input, you’ll have to convert it to an image f'
  - name: Why Not Use `Recognize` (Sync)?
    text: The synchronous version would block the ASP.NET Core thread pool until the
      CPU‑intensive OCR finishes. On a busy server that quickly becomes a bottleneck,
      leading to 504 timeouts. The async variant keeps the API snappy.
  type: HowTo
tags:
- ASP.NET Core
- OCR
- Aspose.OCR
title: 在 ASP.NET Core 中辨識圖片文字 – 上傳以進行 OCR
url: /zh-hant/net/ocr-optimization/recognize-text-from-image-in-asp-net-core-upload-for-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 ASP.NET Core 中從圖像辨識文字 – 完整教學

有沒有曾經需要在 Web API 中 **recognize text from image**，卻不知道從哪裡開始？你並不孤單。在許多專案中——例如發票掃描器、收據追蹤器，甚至簡單的「read‑me」功能——取得可靠的 OCR 結果是一項必備技能。

在本指南中，我們將一步步示範一個完整、可直接執行的範例，教你如何 **upload image for OCR**、將上傳的檔案轉換為 **ocr image from stream**，最後以乾淨的 JSON 回傳擷取的文字。沒有遺漏的部份，沒有模糊的參考——只要把這個獨立的解決方案放入任何 ASP.NET Core 專案，即可立即使用。

**先決條件**：.NET 6 或更新版本、Visual Studio 2022（或 VS Code），以及 Aspose.OCR 授權（免費試用版可用於測試）。如果你已具備這些，讓我們開始吧。

![recognize text from image workflow diagram](https://example.com/ocr-workflow.png "recognize text from image workflow")

## 你將學會的內容

- 一個完整運作的 `OcrController`，可接受 multipart form 上傳。  
- 逐行說明每段程式碼，讓你了解我們為何這樣做。  
- 處理大型檔案、避免執行緒阻塞、保持 API 響應性的技巧。  
- 如何擴充此解決方案的概觀（多語言、圖像前處理等）。  

## 如何在 ASP.NET Core 中辨識圖像文字

此解決方案的核心位於單一的 Controller。以下是 **完整、可執行的程式碼**；所有引用、`using` 指令以及非同步呼叫皆已包含，讓你可以直接複製貼上到新的 ASP.NET Core Web API 專案中。

```csharp
using Aspose.OCR;
using Microsoft.AspNetCore.Mvc;
using System.Threading.Tasks;

[ApiController]
[Route("api/ocr")]
public class OcrController : ControllerBase
{
    // Step 1: Create a reusable OCR engine instance
    // Reusing the same OcrEngine across requests saves memory and speeds up init.
    private readonly OcrEngine _ocrEngine = new OcrEngine();

    // Step 2: Define the endpoint that accepts a file upload
    [HttpPost("recognize")]
    public async Task<IActionResult> Recognize([FromForm] IFormFile uploadedFile)
    {
        // Guard clause – make sure we actually got a file
        if (uploadedFile == null || uploadedFile.Length == 0)
            return BadRequest(new { error = "No file uploaded." });

        // Step 3: Open the uploaded file as a read‑only stream
        // This is the **ocr image from stream** part.
        await using var imageStream = uploadedFile.OpenReadStream();

        // Step 4: Load the image asynchronously for OCR processing
        // Aspose.OCR provides FromStreamAsync which off‑loads the I/O work.
        var ocrImage = await OcrImage.FromStreamAsync(imageStream);

        // Step 5: Run OCR recognition without blocking the request thread
        // RecognizeAsync runs the heavy lifting on a background thread.
        var ocrResult = await _ocrEngine.RecognizeAsync(ocrImage);

        // Step 6: Return the extracted text as a JSON response
        return Ok(new { text = ocrResult.Text });
    }
}
```

### 為何此模式可行

- **單一 `OcrEngine` 實例**：只建立一次引擎，可避免在每次請求時重新載入語言資料的開銷。  
- **全程非同步**：在 `FromStreamAsync` 與 `RecognizeAsync` 上使用 `await`，讓 ASP.NET Core 執行緒池保持空閒，以服務其他呼叫者。  
- `IFormFile` 綁定：`[FromForm]` 屬性讓客戶端只需 POST multipart/form‑data 請求——這正是瀏覽器與 Postman 等工具已熟悉的操作。  

既然程式碼已呈現在眼前，讓我們逐段拆解說明。

## 上傳圖像進行 OCR – 處理 Multipart 請求

當客戶端傳送檔案時，ASP.NET Core 會將其綁定為 `IFormFile`。此物件提供安全的原始位元組存取方式，且不會一次將整個檔案載入記憶體。

```csharp
[HttpPost("recognize")]
public async Task<IActionResult> Recognize([FromForm] IFormFile uploadedFile)
{
    if (uploadedFile == null || uploadedFile.Length == 0)
        return BadRequest(new { error = "No file uploaded." });

    // …
}
```

**小技巧**：如果預期會收到大型圖像（例如 >10 MB），可在此加入檔案大小檢查，並回傳 413 Payload Too Large。這可防止伺服器因記憶體不足而意外崩潰。

## 非同步處理來自 Stream 的 OCR 圖像

`await OcrImage.FromStreamAsync(imageStream)` 這行程式碼負責將圖像位元組解碼成 Aspose.OCR 能理解的格式。由於它是非同步的，底層的 I/O（磁碟或網路）不會阻塞請求執行緒。

```csharp
await using var imageStream = uploadedFile.OpenReadStream();
var ocrImage = await OcrImage.FromStreamAsync(imageStream);
```

### 需留意的邊緣情況

- **損毀檔案**：如果上傳的檔案不是有效的圖像，`FromStreamAsync` 會拋出例外。若需要友善的錯誤訊息，請將呼叫包在 try/catch 中。  
- **不支援的格式**：Aspose 支援 PNG、JPEG、BMP、TIFF 等。如果需要 PDF 輸入，必須先將其轉換為圖像（可使用 Aspose.PDF 協助）。

## 執行 OCR 引擎而不阻塞

`_ocrEngine.RecognizeAsync(ocrImage)` 在背景執行緒上執行 OCR 演算法。這就是 **recognize text from image** 操作實際發生的時刻。

```csharp
var ocrResult = await _ocrEngine.RecognizeAsync(ocrImage);
```

回傳的 `ocrResult` 包含 `Text` 屬性，內含原始擷取的字串。你可以在回傳前進一步後處理（去除空白、修正常見 OCR 錯誤等）。

### 為何不使用 `Recognize`（同步）？

同步版本會阻塞 ASP.NET Core 執行緒池，直至耗費 CPU 的 OCR 完成。在繁忙的伺服器上，這很快會成為瓶頸，導致 504 超時。非同步版本則保持 API 的即時回應。

## 回傳乾淨的 JSON – 最後一步

```csharp
return Ok(new { text = ocrResult.Text });
```

客戶端會收到整潔的 JSON 資料：

```json
{
  "text": "Sample extracted text from the uploaded image."
}
```

如果需要額外的中繼資料——信心分數、語言偵測、邊界框等——只要擴充匿名物件或定義正式的 DTO 即可。

## 測試端點

你可以使用 **cURL**、**Postman**，或甚至簡單的 HTML 表單來驗證功能是否正常。

```bash
curl -X POST https://localhost:5001/api/ocr/recognize \
     -F "uploadedFile=@/path/to/your/image.png"
```

成功的回應範例如下：

```
{"text":"Hello World"}
```

如果忘記傳送檔案，將會收到：

```
{"error":"No file uploaded."}
```

## 更進一步 – 常見強化功能

| 增強功能 | 為何有幫助 | 快速程式碼提示 |
|------------|--------------|-----------------|
| **語言選擇** | 當告訴引擎預期的語言時，OCR 的準確度會提升。 | `_ocrEngine.Language = OcrLanguage.English;` |
| **圖像前處理** | 調整亮度/對比度可拯救低品質掃描。 | `ocrImage = OcrImage.FromBitmap(ImageProcessor` |

## 接下來該學什麼？

以下教學涵蓋與本指南密切相關的主題，並以此為基礎。每個資源皆提供完整可運作的程式碼範例與逐步說明，協助你精通更多 API 功能，並在自己的專案中探索替代實作方式。

- [How to Perform Image Text Extraction from Stream Using Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}