---
category: general
date: 2026-05-25
description: Tìm hiểu cách trích xuất văn bản từ hình ảnh bằng một API ASP.NET Core
  tối thiểu. Tải lên hình ảnh qua POST, đọc dữ liệu multipart form và thực hiện OCR
  trên hình ảnh.
draft: false
keywords:
- extract text from image
- upload image via post
- read multipart form data
- how to recognize text from image
- perform OCR on image
language: vi
og_description: Trích xuất văn bản từ hình ảnh bằng API ASP.NET Core tối giản. Hướng
  dẫn này cho thấy cách tải lên hình ảnh qua POST, đọc dữ liệu multipart form, và
  thực hiện OCR trên hình ảnh.
og_title: Trích xuất văn bản từ hình ảnh trong ASP.NET Core – Từng bước
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
title: Trích xuất văn bản từ hình ảnh trong ASP.NET Core Minimal API – Hướng dẫn đầy
  đủ
url: /vi/net/text-recognition/extract-text-from-image-in-asp-net-core-minimal-api-complete/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Trích xuất Văn bản từ Hình ảnh trong ASP.NET Core Minimal API – Hướng dẫn đầy đủ

Bạn đã bao giờ tự hỏi làm thế nào để **trích xuất văn bản từ hình ảnh** mà không phải đấu tranh với các framework nặng? Bạn không phải là người duy nhất. Nhiều nhà phát triển cần một cách nhanh chóng để cho phép người dùng tải lên một bức ảnh và nhận lại các ký tự thô, cho dù đó là quét biên lai, số hoá ghi chú viết tay, hay cung cấp dữ liệu cho chỉ mục tìm kiếm.

Trong hướng dẫn này, chúng ta sẽ tạo một ASP.NET Core Minimal API nhỏ gọn cho phép **tải lên hình ảnh qua POST**, phân tích payload *multipart/form‑data*, và sau đó **thực hiện OCR trên hình ảnh** bằng một singleton `OcrEngine`. Khi hoàn thành, bạn sẽ có một ứng dụng có thể chạy đầy đủ mà bạn có thể đưa vào bất kỳ dự án .NET 8 nào và bắt đầu trích xuất văn bản từ hình ảnh ngay lập tức.

## Những gì bạn sẽ xây dựng

- Một ứng dụng web tối thiểu lắng nghe tại `/ocr`.
- Một endpoint chấp nhận tệp hình ảnh được gửi bằng yêu cầu POST `multipart/form-data`.
- Logic đọc tệp đã tải lên, đưa nó vào OCR engine và trả về kết quả dạng văn bản thuần.
- Đoạn mã tăng tốc GPU (được chú thích) cho những người có card tương thích.

**Prerequisites**  
- .NET 8 SDK (hoặc phiên bản mới hơn).  
- Kiến thức cơ bản về C# và dòng lệnh.  
- Thư viện OCR cung cấp lớp `OcrEngine` (ví dụ giả định một gói NuGet).  

Nếu bạn đã có những điều trên, hãy bắt đầu.

## Bước 1: Thiết lập dự án và thêm gói OCR

Đầu tiên, tạo một dự án web mới và thêm thư viện OCR.

```bash
dotnet new web -n ImageOcrApi
cd ImageOcrApi
dotnet add package Awesome.Ocr --version 1.3.0   # replace with your actual OCR package
```

> **Mẹo:** Giữ các phụ thuộc của bạn luôn cập nhật. Các phiên bản mới thường mang lại cải thiện hiệu năng, đặc biệt đối với suy luận tăng tốc GPU.

## Bước 2: Đăng ký Singleton OCR Engine (Dịch vụ chính)

Chúng ta muốn một thể hiện `OcrEngine` duy nhất cho toàn bộ ứng dụng—không cần khởi tạo engine mới cho mỗi yêu cầu. Đăng ký nó trong container dịch vụ của builder.

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

**Tại sao lại là singleton?**  
Việc tạo một OCR engine có thể tốn kém—nghĩ đến việc tải trọng lượng mạng nơ-ron vào bộ nhớ. Bằng cách tái sử dụng cùng một thể hiện, chúng ta tiết kiệm cả chu kỳ CPU và RAM, giúp thời gian phản hồi nhanh hơn cho mỗi lời gọi `/ocr`.

## Bước 3: Xây dựng Ứng dụng

Bây giờ chúng ta khởi tạo đối tượng `WebApplication`.

```csharp
var app = builder.Build();
```

Dòng này trông gần như ma thuật, nhưng bên trong nó thiết lập routing, middleware và container DI mà chúng ta vừa cấu hình.

## Bước 4: Định nghĩa Endpoint POST – “Tải lên Hình ảnh qua POST”

Đây là phần cốt lõi của hướng dẫn: một endpoint cho phép **tải lên hình ảnh qua POST**, đọc payload multipart và chuyển dữ liệu cho OCR engine.

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

### Phân tích Logic

| Bước | Điều gì xảy ra | Tại sao quan trọng |
|------|----------------|--------------------|
| **ReadFormAsync** | Phân tích yêu cầu *multipart/form-data* đến. | Nếu không có bước này, bạn không thể truy cập các tệp đã tải lên. |
| **form.Files["image"]** | Lấy tệp có tên trường form là `image`. | Đảm bảo một hợp đồng dự đoán được cho người gọi. |
| **Content‑type check** | Kiểm tra tệp có phải là hình ảnh (ví dụ `image/png`). | Ngăn OCR engine bị lỗi khi nhận dữ liệu không phải hình ảnh. |
| **Image.FromStream** | Chuyển luồng raw thành một `System.Drawing.Image`. | Thư viện OCR yêu cầu một đối tượng `Image`, không phải mảng byte thô. |
| **ocr.Recognize(img)** | Gọi OCR engine để **nhận dạng văn bản từ hình ảnh**. | Đây là bước **thực hiện OCR trên hình ảnh** cốt lõi. |
| **Results.Text** | Trả về phản hồi dạng văn bản thuần. | Định dạng đơn giản, dễ tiêu thụ cho các dịch vụ downstream. |

## Bước 5: Chạy API

Cuối cùng, khởi động máy chủ web.

```csharp
app.Run();
```

Khi bạn chạy `dotnet run`, API sẽ lắng nghe tại `http://localhost:5000` (hoặc cổng bạn chọn). Bạn có thể kiểm tra bằng `curl`:

```bash
curl -X POST http://localhost:5000/ocr \
  -F "image=@/path/to/receipt.png" \
  -H "Accept: text/plain"
```

**Kết quả mong đợi:** Console sẽ in ra các ký tự đã nhận dạng, ví dụ:

```
Total: $23.45
Date: 2026-05-20
Item A  $12.00
Item B  $11.45
```

Nếu hình ảnh mờ hoặc ngôn ngữ không được hỗ trợ, OCR engine sẽ trả về chuỗi rỗng hoặc thông báo lỗi—hãy xử lý các trường hợp này trong mã production.

## Các Trường hợp Cạnh & Thực hành Tốt

### 1. Tệp lớn

Giới hạn mặc định cho body yêu cầu là 30 MB. Đối với các bản quét lớn hơn, bạn có thể cần điều chỉnh:

```csharp
builder.Services.Configure<FormOptions>(options =>
{
    options.MultipartBodyLengthLimit = 100 * 1024 * 1024; // 100 MB
});
```

### 2. OCR bất đồng bộ

Một số thư viện OCR cung cấp các phương thức async (`RecognizeAsync`). Nếu thư viện của bạn có, thay thế `ocr.Recognize(img)` bằng `await ocr.RecognizeAsync(img)` và đánh dấu lambda là `async`.

### 3. Các lưu ý bảo mật

- **Xác thực kích thước tệp** trước khi tải vào bộ nhớ.  
- **Làm sạch tên tệp** nếu bạn ghi nó ra đĩa.  
- **Giới hạn tốc độ** endpoint để tránh tấn công từ chối dịch vụ.

### 4. Tăng tốc GPU

Nếu bạn bỏ comment dòng `engine.GpuDevice = new GpuDevice(0);` và phần cứng của bạn hỗ trợ CUDA hoặc DirectML, bạn sẽ thấy tốc độ tăng đáng kể, đặc biệt với các hình ảnh độ phân giải cao.

## Ví dụ Hoạt động Đầy đủ

Dưới đây là file `Program.cs` hoàn chỉnh mà bạn có thể sao chép‑dán vào một dự án Minimal API mới.

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

Lưu lại, chạy `dotnet run`, và bạn đã sẵn sàng **trích xuất văn bản từ hình ảnh** theo yêu cầu.

## Kết luận

Chúng ta đã đi qua một **giải pháp hoàn chỉnh, đầu‑tới‑cuối** để trích xuất văn bản từ hình ảnh bằng ASP.NET Core Minimal API. Bắt đầu từ việc tạo khung dự án, chúng ta **đã đăng ký một singleton OCR engine**, xây dựng một endpoint cho phép **tải lên hình ảnh qua POST**, **đọc dữ liệu multipart**, và cuối cùng **thực hiện OCR trên hình ảnh** để trả về văn bản thuần sạch sẽ.

Từ đây bạn có thể:

- Thêm lớp bọc JSON để có phản hồi phong phú hơn.  
- Kết nối cơ sở dữ liệu để lưu trữ văn bản đã trích xuất.  
- Mở rộng hỗ trợ nhiều ngôn ngữ (`OcrLanguage.Spanish`, v.v.).  

Mẫu này mở rộng tốt—chỉ cần đưa cùng một endpoint vào một microservice lớn hơn hoặc expose nó phía sau một API gateway.

Bạn có câu hỏi về xử lý PDF, xử lý batch, hay tối ưu GPU? Hãy để lại bình luận, chúc lập trình vui!

## Các Hướng dẫn Liên quan

- [Extract Text from Image Using Aspose.OCR .NET](/ocr/english/net/image-and-drawing-recognition/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}