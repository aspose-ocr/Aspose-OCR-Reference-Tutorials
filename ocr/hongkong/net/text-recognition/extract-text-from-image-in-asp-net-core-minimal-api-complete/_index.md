---
category: general
date: 2026-05-25
description: 學習如何使用精簡的 ASP.NET Core API 從圖像中提取文字。透過 POST 上傳圖像，讀取 multipart 表單資料並對圖像執行
  OCR。
draft: false
keywords:
- extract text from image
- upload image via post
- read multipart form data
- how to recognize text from image
- perform OCR on image
language: zh-hant
og_description: 使用精簡的 ASP.NET Core API 從圖像提取文字。本指南說明如何透過 POST 上傳圖像、讀取 multipart 表單資料，並對圖像執行
  OCR。
og_title: 在 ASP.NET Core 中從圖像擷取文字 – 步驟說明
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: Learn how to extract text from image with a minimal ASP.NET Core API.
    Upload image via POST, read multipart form data and perform OCR on image.
  headline: Extract Text from Image in ASP.NET Core Minimal API – Complete Guide
  type: TechArticle
- description: Learn how to extract text from image with a minimal ASP.NET Core API.
    Upload image via POST, read multipart form data and perform OCR on image.
  name: Extract Text from Image in ASP.NET Core Minimal API – Complete Guide
  steps:
  - name: Breaking Down the Logic
    text: '| Step | What Happens | Why It Matters | |------|--------------|----------------|
      | **ReadFormAsync** | Parses the incoming *multipart/form-data* request. | Without
      this, you can’t access the uploaded files. | | **form.Files["image"]** | Retrieves
      the file whose form‑field name is `image`. | Guarant'
  - name: 1. Large Files
    text: 'The default request body limit is 30 MB. For larger scans you might need
      to adjust:'
  - name: 2. Asynchronous OCR
    text: Some OCR libraries expose async methods (`RecognizeAsync`). If yours does,
      replace `ocr.Recognize(img)` with `await ocr.RecognizeAsync(img)` and mark the
      lambda as `async`.
  - name: 3. Security Considerations
    text: '- **Validate file size** before loading it into memory. - **Sanitize the
      filename** if you ever write it to disk. - **Rate‑limit** the endpoint to avoid
      denial‑of‑service attacks.'
  - name: 4. GPU Acceleration
    text: If you uncomment the `engine.GpuDevice = new GpuDevice(0);` line and your
      hardware supports CUDA or DirectML, you’ll see a noticeable speed boost, especially
      on high‑resolution images.
  type: HowTo
tags:
- ASP.NET Core
- OCR
- Minimal API
title: 在 ASP.NET Core Minimal API 中從圖片提取文字 – 完整指南
url: /zh-hant/net/text-recognition/extract-text-from-image-in-asp-net-core-minimal-api-complete/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從圖像中提取文字的 ASP.NET Core Minimal API 完整指南

你有沒有想過如何在不使用龐大框架的情況下 **extract text from image**？你並不孤單。許多開發者需要一個快速的方式，讓使用者上傳圖片後即可取得原始文字，無論是掃描收據、數位化手寫筆記，或是為搜尋索引提供文字。

在本教學中，我們將建立一個小型的 ASP.NET Core Minimal API，具備 **uploads image via POST** 功能，解析 *multipart/form‑data* 負載，然後使用單例 `OcrEngine` 來 **perform OCR on image**。完成後，你將擁有一個可直接在任何 .NET 8 專案中使用的完整可執行應用，即可立即開始從圖像中提取文字。

## 你將建立的內容

- 一個監聽 `/ocr` 的最小化 Web 應用程式。
- 一個接受使用 `multipart/form-data` POST 請求傳送的圖像檔案的端點。
- 讀取上傳檔案、將其送入 OCR 引擎，並回傳純文字結果的邏輯。
- 可選的 GPU 加速程式碼片段（已註解），供具備相容顯示卡的使用者使用。

**先決條件**  
- .NET 8 SDK（或更新版本）。  
- 具備 C# 與命令列的基本知識。  
- 提供 `OcrEngine` 類別的 OCR 函式庫（範例假設使用一個虛構的 NuGet 套件）。

如果你已具備上述條件，讓我們開始吧。

## 步驟 1：設定專案並加入 OCR 套件

首先，建立一個新的 Web 專案，並將 OCR 函式庫加入專案。

```bash
dotnet new web -n ImageOcrApi
cd ImageOcrApi
dotnet add package Awesome.Ocr --version 1.3.0   # replace with your actual OCR package
```

> **專業提示：** 請保持相依套件為最新版本。較新的版本通常能提升效能，尤其是在 GPU 加速推論時。

## 步驟 2：註冊單例 OCR 引擎（主要服務）

我們希望整個應用程式只使用一個 `OcrEngine` 實例——不必在每個請求都重新建立引擎。將它註冊到 builder 的服務容器中。

```csharp
using Awesome.Ocr;               // <-- the OCR library namespace
using Microsoft.AspNetCore.Builder;
using Microsoft.AspNetCore.Http;
using System.Drawing;            // System.Drawing.Common for Image handling

var builder = WebApplication.CreateBuilder(args);

// Register a singleton OCR engine (English language)
// Uncomment the GPU line if you have a compatible GPU and the library supports it.
builder.Services.AddSingleton<OcrEngine>(sp =>
{
    var engine = new OcrEngine { Language = OcrLanguage.English };
    // engine.GpuDevice = new GpuDevice(0); // enable GPU acceleration
    return engine;
});
```

**為什麼使用單例？**  
建立 OCR 引擎的成本相當高——例如需要將神經網路權重載入記憶體。重複使用同一個實例可節省 CPU 時間與記憶體，從而提升每次 `/ocr` 呼叫的回應速度。

## 步驟 3：建構應用程式

現在我們將實體化 `WebApplication` 物件。

```csharp
var app = builder.Build();
```

那行程式碼看起來幾乎像魔法，但實際上它在底層為我們剛剛設定的路由、middleware 與 DI 容器 **wires** 起來。

## 步驟 4：定義 POST 端點 – “Upload Image via POST”

這就是本教學的核心：一個會 **upload image via POST**、讀取 multipart 負載，並將資料交給 OCR 引擎的端點。

```csharp
app.MapPost("/ocr", async (HttpRequest request, OcrEngine ocr) =>
{
    // Step 5: Read multipart form data and extract the uploaded image
    var form = await request.ReadFormAsync();               // <-- read multipart/form-data
    var file = form.Files["image"];                         // expects a field named "image"

    if (file is null || file.Length == 0)
    {
        return Results.BadRequest("No image file provided.");
    }

    // Guard against unsupported content types
    if (!file.ContentType.StartsWith("image/"))
    {
        return Results.BadRequest("Uploaded file is not an image.");
    }

    // Load the image into a System.Drawing.Image
    using var img = Image.FromStream(file.OpenReadStream());

    // Step 6: Perform OCR on the image
    string text = ocr.Recognize(img);                       // <-- perform OCR on image

    // Step 7: Return the extracted text as plain‑text
    return Results.Text(text);
});
```

### 逐步說明邏輯

| 步驟 | 發生了什麼 | 為何重要 |
|------|------------|----------|
| **ReadFormAsync** | 解析傳入的 *multipart/form-data* 請求。 | 若未執行此步驟，將無法取得上傳的檔案。 |
| **form.Files["image"]** | 取得表單欄位名稱為 `image` 的檔案。 | 為呼叫端提供可預測的合約。 |
| **Content‑type check** | 檢查檔案是否為圖像（例如 `image/png`）。 | 防止 OCR 引擎在非圖像資料上失敗。 |
| **Image.FromStream** | 將原始串流轉換為 `System.Drawing.Image`。 | OCR 函式庫需要 `Image` 物件，而非原始位元組陣列。 |
| **ocr.Recognize(img)** | 呼叫 OCR 引擎以 **how to recognize text from image**。 | 這是核心的 **perform OCR on image** 步驟。 |
| **Results.Text** | 回傳純文字回應。 | 為下游服務提供簡單、易於消費的格式。 |

## 步驟 5：執行 API

最後，啟動 Web 伺服器。

```csharp
app.Run();
```

當你執行 `dotnet run` 時，API 會監聽在 `http://localhost:5000`（或你自行設定的埠號）。你可以使用 `curl` 進行測試：

```bash
curl -X POST http://localhost:5000/ocr \
  -F "image=@/path/to/receipt.png" \
  -H "Accept: text/plain"
```

**預期輸出：** 主控台會印出辨識出的字元，例如：

```
Total: $23.45
Date: 2026-05-20
Item A  $12.00
Item B  $11.45
```

若圖像模糊或語言不受支援，OCR 引擎會回傳空字串或錯誤訊息——請在 **production code** 中妥善處理這些情況。

## 邊緣案例與最佳實踐

### 1. 大檔案

預設的請求主體大小上限為 30 MB。若要處理更大的掃描檔，可能需要調整：

```csharp
builder.Services.Configure<FormOptions>(options =>
{
    options.MultipartBodyLengthLimit = 100 * 1024 * 1024; // 100 MB
});
```

### 2. 非同步 OCR

某些 OCR 函式庫提供非同步方法（`RecognizeAsync`）。如果你的函式庫支援，請將 `ocr.Recognize(img)` 改為 `await ocr.RecognizeAsync(img)`，並將 lambda 標記為 `async`。

### 3. 安全性考量

- **Validate file size**：在載入記憶體前先驗證檔案大小。  
- **Sanitize the filename**：若將檔案寫入磁碟，請先清理檔名。  
- **Rate‑limit**：對端點實施速率限制，以防止拒絕服務攻擊。

### 4. GPU 加速

若取消註解 `engine.GpuDevice = new GpuDevice(0);` 並且硬體支援 CUDA 或 DirectML，你將看到明顯的效能提升，特別是在高解析度圖像上。

## 完整範例

以下是完整的 `Program.cs`，你可以直接複製貼上到全新的 Minimal API 專案中。

```csharp
using Awesome.Ocr;
using Microsoft.AspNetCore.Builder;
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Http.Features;
using System.Drawing;

var builder = WebApplication.CreateBuilder(args);

// Optional: increase multipart limit for big images
builder.Services.Configure<FormOptions>(options =>
{
    options.MultipartBodyLengthLimit = 50 * 1024 * 1024; // 50 MB
});

// Register the OCR engine as a singleton
builder.Services.AddSingleton<OcrEngine>(sp =>
{
    var engine = new OcrEngine { Language = OcrLanguage.English };
    // engine.GpuDevice = new GpuDevice(0); // enable GPU if available
    return engine;
});

var app = builder.Build();

app.MapPost("/ocr", async (HttpRequest request, OcrEngine ocr) =>
{
    var form = await request.ReadFormAsync();
    var file = form.Files["image"];

    if (file is null || file.Length == 0)
        return Results.BadRequest("No image file provided.");

    if (!file.ContentType.StartsWith("image/"))
        return Results.BadRequest("Uploaded file is not an image.");

    using var img = Image.FromStream(file.OpenReadStream());

    // Core OCR operation
    string text = ocr.Recognize(img);

    return Results.Text(text);
});

app.Run();
```

儲存後，執行 `dotnet run`，即可隨時 **extract text from image**。

## 結論

我們已完整說明如何使用 ASP.NET Core Minimal API 來實作 **complete, end‑to‑end solution**，從專案骨架開始，**registered a singleton OCR engine**，建立一個 **uploads image via POST**、**read multipart form data** 的端點，最終 **perform OCR on image**，回傳乾淨的純文字。

從此你可以：

- 為回應加入 JSON 包裝，以提供更豐富的資料。  
- 接入資料庫以儲存提取出的文字。  
- 擴充支援多語言（例如 `OcrLanguage.Spanish` 等）。

這個模式相當易於擴展——只要將相同的端點放入更大的微服務，或在 API Gateway 後面暴露即可。

有關 PDF 處理、批次作業或 GPU 調校的問題嗎？歡迎留言，祝開發愉快！

## 相關教學

- [使用 Aspose.OCR .NET 提取圖像文字](/ocr/english/net/image-and-drawing-recognition/)
- [提取圖像文字 – 使用 Aspose.OCR for .NET 進行 OCR 最佳化](/ocr/english/net/ocr-optimization/)
- [使用 Aspose.OCR 以 C# 提取圖像文字並選擇語言](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}