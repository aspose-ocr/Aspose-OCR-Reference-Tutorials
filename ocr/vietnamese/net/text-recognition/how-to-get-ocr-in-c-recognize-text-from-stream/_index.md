---
category: general
date: 2026-03-05
description: Cách thực hiện OCR nhanh chóng bằng Aspose.OCR và nhận dạng văn bản từ
  luồng trong vài bước đơn giản. Tìm hiểu mã C# đầy đủ và các mẹo cho việc truyền
  dữ liệu hình ảnh dưới dạng luồng.
draft: false
keywords:
- how to get OCR
- recognize text from stream
- Aspose OCR
- streaming OCR C#
- image chunk processing
language: vi
og_description: Cách sử dụng OCR trong C# và nhận dạng văn bản từ luồng bằng Aspose.OCR.
  Hãy theo dõi hướng dẫn từng bước này để có giải pháp sẵn sàng chạy.
og_title: Cách sử dụng OCR trong C# – Hướng dẫn nhận dạng luồng toàn diện
tags:
- OCR
- C#
- Aspose
title: Cách sử dụng OCR trong C# – Nhận dạng văn bản từ luồng
url: /vi/net/text-recognition/how-to-get-ocr-in-c-recognize-text-from-stream/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách sử dụng OCR trong C# – Nhận dạng văn bản từ luồng

Bạn đã bao giờ tự hỏi **cách để có OCR** hoạt động trong một ứng dụng .NET mà không cần lưu toàn bộ hình ảnh vào đĩa không? Bạn không phải là người duy nhất. Nhiều nhà phát triển cần **nhận dạng văn bản từ luồng** — ví dụ khi xử lý các hình ảnh đến qua mạng, nguồn cấp camera, hoặc API lưu trữ đám mây.  

Trong hướng dẫn này, chúng tôi sẽ đi qua một ví dụ hoàn chỉnh, sẵn sàng chạy, cho thấy chính xác điều đó. Khi kết thúc, bạn sẽ có một chương trình C# độc lập tạo ra một engine Aspose OCR, truyền các đoạn ảnh vào nó dưới dạng luồng, và in văn bản đã trích xuất ra console. Không có công cụ bên ngoài bí ẩn, chỉ có mã rõ ràng và một vài mẹo thực tế.

## Những gì bạn sẽ học

- Cách cài đặt và cấp phép thư viện Aspose.OCR.
- Cách cung cấp dữ liệu hình ảnh từng phần bằng phương thức `AppendChunk`.
- Cách bắt đầu và kết thúc chu kỳ nhận dạng (`BeginRecognize` / `EndRecognize`).
- Cách xử lý các trường hợp biên thường gặp như các đoạn không đầy đủ hoặc lỗi giấy phép.
- Kết quả đầu ra trông như thế nào và cách xác minh.

### Yêu cầu trước

- .NET 6.0 trở lên (mã hoạt động với .NET Core và .NET Framework cũng được).
- Một tệp giấy phép Aspose OCR hợp lệ (`Aspose.OCR.lic`). Bạn có thể lấy bản dùng thử miễn phí từ trang web Aspose.
- Kiến thức cơ bản về C# và `async`/`await` nếu bạn muốn đọc từ một luồng bất đồng bộ (ví dụ sử dụng một stub đồng bộ để dễ hiểu).

> **Tại sao điều này quan trọng:** OCR dạng luồng giúp bạn giữ mức sử dụng bộ nhớ thấp và giảm độ trễ khi xử lý các hình ảnh lớn hoặc nguồn video liên tục. Đây là mẫu bạn sẽ thấy trong các máy quét tài liệu thời gian thực, ứng dụng di động, và các pipeline xử lý phía máy chủ.

## Bước 1: Thiết lập dự án và thêm Aspose.OCR

Đầu tiên, tạo một dự án console mới và thêm gói NuGet Aspose.OCR.

```bash
dotnet new console -n StreamOcrDemo
cd StreamOcrDemo
dotnet add package Aspose.OCR
```

> **Mẹo chuyên nghiệp:** Nếu bạn đang dùng Visual Studio, nhấp chuột phải vào dự án → *Manage NuGet Packages* → tìm “Aspose.OCR” và cài đặt phiên bản ổn định mới nhất.

Bây giờ thêm tệp giấy phép vào thư mục gốc của dự án và đặt thuộc tính **Copy to Output Directory** thành **Copy always**. Điều này đảm bảo tệp có sẵn khi chạy.

```csharp
// Program.cs – top of the file
using System;
using System.IO;
using Aspose.OCR;
```

## Bước 2: Khởi tạo OCR Engine và áp dụng giấy phép

Việc tạo engine rất đơn giản, nhưng việc áp dụng giấy phép **phải** được thực hiện trước bất kỳ lời gọi nhận dạng nào; nếu không bạn sẽ gặp hạn chế chế độ dùng thử.

```csharp
static OcrEngine InitializeOcrEngine()
{
    var engine = new OcrEngine();

    // Load the license – adjust the path if your file lives elsewhere
    string licensePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "Aspose.OCR.lic");
    if (!File.Exists(licensePath))
    {
        Console.Error.WriteLine("License file not found at " + licensePath);
        Environment.Exit(1);
    }

    engine.SetLicense(licensePath);
    return engine;
}
```

> **Lý do chúng ta làm điều này:** Đặt giấy phép sớm đảm bảo rằng tất cả các lời gọi API tiếp theo chạy ở chế độ đầy đủ tính năng, tránh watermark “phiên bản đánh giá”.

## Bước 3: Mô phỏng nguồn luồng

Trong một ứng dụng thực tế, bạn sẽ đọc từ `NetworkStream`, `FileStream`, hoặc SDK camera. Để minh họa, chúng tôi sẽ mô phỏng một luồng bằng một hàm trợ giúp trả về mảng byte đại diện cho một đoạn ảnh JPEG.

```csharp
static byte[] GetNextChunk()
{
    // Replace this with your actual streaming logic.
    // Here we simply read the whole file and pretend it’s a single chunk.
    string sampleImagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "sample.jpg");
    if (!File.Exists(sampleImagePath))
    {
        Console.Error.WriteLine("Sample image not found at " + sampleImagePath);
        Environment.Exit(1);
    }

    return File.ReadAllBytes(sampleImagePath);
}
```

> **Lưu ý trường hợp biên:** Nếu bạn nhận được nhiều đoạn nhỏ, bạn có thể gọi `engine.Image.AppendChunk(chunk)` liên tục trước khi kết thúc nhận dạng. Engine sẽ lưu trữ trong bộ nhớ nội bộ cho đến khi có đủ dữ liệu để bắt đầu xử lý.

## Bước 4: Cung cấp dữ liệu ảnh từng phần và chạy OCR

Bây giờ chúng ta kết hợp mọi thứ lại. Thứ tự thực hiện là:

1. `BeginRecognize()` – thông báo cho engine rằng chúng ta sắp cung cấp dữ liệu.
2. `AppendChunk()` – thêm mỗi mảng byte (bạn có thể lặp qua nhiều đoạn).
3. `EndRecognize()` – báo hiệu rằng đoạn cuối cùng đã được gửi và kích hoạt quá trình nhận dạng thực tế.

```csharp
static string PerformOcr(OcrEngine engine, byte[] imageChunk)
{
    // Start the recognition session
    engine.BeginRecognize();

    // Feed the image data. If you have multiple chunks, call this in a loop.
    engine.Image.AppendChunk(imageChunk);

    // End the session – the engine now processes the accumulated data.
    engine.EndRecognize();

    // Retrieve the result object; .Text holds the plain string.
    return engine.GetResult().Text;
}
```

## Bước 5: Kết hợp tất cả trong `Main`

Dưới đây là phương thức `Main` đầy đủ, kết nối mọi thứ, in ra văn bản đã nhận dạng, và giải phóng engine một cách sạch sẽ.

```csharp
static void Main(string[] args)
{
    // 1️⃣ Initialize OCR engine with license
    var ocrEngine = InitializeOcrEngine();

    try
    {
        // 2️⃣ Get a chunk of image data (replace with your streaming source)
        byte[] imageChunk = GetNextChunk();

        // 3️⃣ Run OCR on the streamed data
        string recognizedText = PerformOcr(ocrEngine, imageChunk);

        // 4️⃣ Output the result
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(recognizedText);
    }
    catch (Exception ex)
    {
        // Helpful error handling – you’ll often see OCR exceptions when the image is corrupted.
        Console.Error.WriteLine("OCR failed: " + ex.Message);
    }
    finally
    {
        // Release any native resources held by the engine.
        ocrEngine.Dispose();
    }
}
```

### Kết quả mong đợi

Nếu `sample.jpg` chứa cụm từ “Hello, World!” bạn sẽ thấy:

```
=== Recognized Text ===
Hello, World!
```

Nếu hình ảnh mờ hoặc đoạn không đầy đủ, kết quả có thể rỗng hoặc chứa các ký tự lộn xộn – đó là lý do việc xử lý đoạn đúng cách (đảm bảo đoạn cuối cùng được gửi) rất quan trọng.

## Xử lý nhiều đoạn (Nâng cao)

Khi làm việc với dữ liệu thực sự dạng luồng, bạn có thể nhận được nhiều mảnh nhỏ. Mẫu dưới đây cho thấy cách lặp cho đến khi nguồn kết thúc.

```csharp
static string OcrFromStream(OcrEngine engine, Stream source)
{
    engine.BeginRecognize();

    byte[] buffer = new byte[8192]; // 8 KB per read – adjust as needed
    int bytesRead;
    while ((bytesRead = source.Read(buffer, 0, buffer.Length)) > 0)
    {
        // If the last read returned fewer bytes, copy only that many.
        if (bytesRead < buffer.Length)
        {
            byte[] chunk = new byte[bytesRead];
            Array.Copy(buffer, chunk, bytesRead);
            engine.Image.AppendChunk(chunk);
        }
        else
        {
            engine.Image.AppendChunk(buffer);
        }
    }

    engine.EndRecognize();
    return engine.GetResult().Text;
}
```

> **Lý do điều này hữu ích:** Bằng cách luồng trực tiếp từ `NetworkStream` hoặc `FileStream`, bạn không bao giờ tải toàn bộ hình ảnh vào bộ nhớ, điều này đặc biệt có lợi cho các PDF lớn hoặc ảnh độ phân giải cao.

## Những cạm bẫy phổ biến & Cách tránh chúng

| Cạm bẫy | Triệu chứng | Cách khắc phục |
|---------|------------|----------------|
| Không tìm thấy giấy phép | `SetLicense` ném `FileNotFoundException` | Kiểm tra đường dẫn và đặt *Copy to Output Directory* thành *Copy always*. |
| Kết quả rỗng | Không có văn bản nào được in | Đảm bảo bạn đã gọi `BeginRecognize` **trước** `AppendChunk` và `EndRecognize` **sau** đoạn cuối cùng. |
| Rò rỉ bộ nhớ | Ứng dụng chậm lại sau nhiều lần gọi OCR | Giải phóng `OcrEngine` sau mỗi lần sử dụng hoặc tái sử dụng một thể hiện duy nhất với các lời gọi `Dispose` đúng cách. |
| Đoạn hỏng | Ký tự lộn xộn | Xác thực kích thước đoạn; đối với JPEG/PNG, vài byte đầu tiên nên bắt đầu bằng `0xFF 0xD8` hoặc `0x89 0x50`. |

## Bonus: Sử dụng luồng bất đồng bộ

Nếu nguồn của bạn là luồng phản hồi `HttpClient`, bạn có thể điều chỉnh vòng lặp để `await` các lần đọc:

```csharp
static async Task<string> OcrFromAsyncStream(OcrEngine engine, Stream asyncSource)
{
    engine.BeginRecognize();

    byte[] buffer = new byte[8192];
    int bytesRead;
    while ((bytesRead = await asyncSource.ReadAsync(buffer, 0, buffer.Length)) > 0)
    {
        if (bytesRead < buffer.Length)
        {
            var chunk = new byte[bytesRead];
            Array.Copy(buffer, chunk, bytesRead);
            engine.Image.AppendChunk(chunk);
        }
        else
        {
            engine.Image.AppendChunk(buffer);
        }
    }

    engine.EndRecognize();
    return engine.GetResult().Text;
}
```

Điều này giữ cho UI phản hồi trong các ứng dụng desktop hoặc di động và tối đa hoá lưu lượng trên máy chủ.

## Kết luận

Bạn hiện đã có một **giải pháp hoàn chỉnh, độc lập cho cách sử dụng OCR** trong C# và **nhận dạng văn bản từ luồng** bằng Aspose.OCR. Hướng dẫn đã bao phủ mọi thứ từ cấp phép và khởi tạo đến cung cấp các đoạn ảnh, xử lý các trường hợp biên, và thậm chí một biến thể bất đồng bộ.  

Hãy thử nghiệm — thay thế `sample.jpg` bằng nguồn cấp camera trực tiếp, hình ảnh lưu trữ trên đám mây, hoặc tải lên HTTP multipart. Khi đã quen, khám phá các tính năng nâng cao như gói ngôn ngữ, tiền xử lý tùy chỉnh, hoặc xử lý hàng loạt nhiều luồng.

**Các bước tiếp theo:**  
- Thử OCR trên PDF bằng cách chuyển mỗi trang thành hình ảnh trước.  
- Thử nghiệm với `engine.Config` để tăng độ chính xác cho các phông chữ cụ thể.  
- Kết hợp điều này với Azure Functions hoặc AWS Lambda để tạo pipeline trích xuất văn bản không máy chủ.

Chúc lập trình vui vẻ, và mong các luồng của bạn luôn rõ nét và kết quả OCR luôn hoàn hảo!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}