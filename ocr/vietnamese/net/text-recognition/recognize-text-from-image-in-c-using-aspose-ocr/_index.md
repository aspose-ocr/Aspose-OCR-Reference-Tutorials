---
category: general
date: 2026-05-31
description: Tìm hiểu cách nhận dạng văn bản từ hình ảnh trong C# với Aspose OCR,
  bao gồm cách trích xuất văn bản từ tệp TIFF và tải hình ảnh cho OCR một cách hiệu
  quả.
draft: false
keywords:
- recognize text from image
- extract text from tiff
- load image for OCR
- Aspose OCR C#
- GPU accelerated OCR
language: vi
og_description: Hướng dẫn từng bước nhận dạng văn bản từ hình ảnh bằng Aspose OCR,
  bao gồm việc trích xuất từ tiff và tải hình ảnh đúng cách cho OCR.
og_title: Nhận dạng văn bản từ hình ảnh trong C# bằng Aspose OCR
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to recognize text from image in C# with Aspose OCR, including
    how to extract text from tiff files and load image for OCR efficiently.
  headline: recognize text from image in C# using Aspose OCR
  type: TechArticle
- questions:
  - answer: Reduce its resolution before feeding it to the engine, or increase `GpuMemoryLimit`
      if you have enough VRAM.
    question: What if the image is huge (over 10 MB)?
  - answer: Absolutely. Just reuse the same `OcrEngine` instance and assign a new
      `ImageStream` each iteration.
    question: Can I process multiple images in a loop?
  - answer: '`OcrEngine` implements `IDisposable`. Wrap it in a `using` block for
      clean resource management, especially when working with GPU resources.'
    question: Do I need to dispose of anything?
  - answer: Set `engine.Language = OcrLanguage.Spanish` (or any supported language)
      before calling `Recognize()`.
    question: What about languages other than English?
  type: FAQPage
tags:
- OCR
- C#
- Aspose
title: Nhận dạng văn bản từ hình ảnh trong C# bằng Aspose OCR
url: /vi/net/text-recognition/recognize-text-from-image-in-c-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# nhận dạng văn bản từ hình ảnh trong C# bằng Aspose OCR

Bạn đã bao giờ cần **recognize text from image** nhưng không chắc bắt đầu từ đâu trong C#? Bạn không đơn độc—nhiều nhà phát triển gặp khó khăn khi làm việc với tài liệu quét hoặc các tệp TIFF đa trang. Trong hướng dẫn này, chúng tôi sẽ hướng dẫn bạn qua một ví dụ hoàn chỉnh, sẵn sàng chạy, sử dụng thư viện Aspose OCR để **recognize text from image**, và chúng tôi cũng sẽ chỉ cho bạn cách **extract text from tiff** và cách tốt nhất để **load image for OCR** mà không phải đau đầu.

Chúng tôi sẽ bao phủ mọi thứ từ việc cài đặt gói NuGet đến xử lý tăng tốc GPU và chuyển về CPU khi cần. Khi kết thúc hướng dẫn này, bạn sẽ có một ứng dụng console in ra văn bản đã nhận dạng và thời gian xử lý—không thiếu bất kỳ phần nào, không có tham chiếu mơ hồ.

## Những gì bạn sẽ xây dựng

- Một ứng dụng console .NET đơn giản tải một hình ảnh (bao gồm TIFF đa trang)  
- Một engine OCR được cấu hình để sử dụng GPU, với khả năng chuyển về CPU một cách mượt mà  
- Trích xuất văn bản thuần từ hình ảnh, in ra console  
- Thông tin thời gian để bạn có thể thấy ảnh hưởng hiệu năng của GPU so với CPU  

**Yêu cầu trước**

- .NET 6 SDK hoặc phiên bản mới hơn (mã hoạt động với .NET Core và .NET Framework)  
- Kiến thức cơ bản về C# và dòng lệnh  
- Kết nối Internet để tải gói NuGet Aspose.OCR  

Nếu bạn đã có những thứ này, hãy bắt đầu.

![C# code to recognize text from image using Aspose OCR](image.png "C# code to recognize text from image using Aspose OCR")

## Bước 1 – Recognize text from image: Cài đặt engine OCR

Đầu tiên, chúng ta cần một thể hiện `OcrEngine`. Aspose OCR cho phép bạn chọn thiết bị xử lý—GPU để tăng tốc, CPU như một biện pháp an toàn. Engine cũng chấp nhận gợi ý giới hạn bộ nhớ, điều này hữu ích trên các máy chia sẻ.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Create the OCR engine and request GPU acceleration.
        // If no compatible GPU is found, Aspose silently falls back to CPU.
        OcrEngine engine = new OcrEngine
        {
            Device = OcrDevice.Gpu,      // Try GPU first
            GpuMemoryLimit = 1024        // Optional: cap GPU memory usage (MB)
        };
```

**Tại sao điều này quan trọng:**  
Chọn `OcrDevice.Gpu` có thể giảm vài giây thời gian nhận dạng cho các hình ảnh lớn, đặc biệt là TIFF đa trang. `GpuMemoryLimit` ngăn ứng dụng của bạn chiếm hết bộ nhớ GPU trên một workstation chia sẻ.

## Bước 2 – Load image for OCR (bao gồm hỗ trợ TIFF)

Bây giờ chúng ta cung cấp cho engine một hình ảnh. `ImageStream.FromFile` của Aspose chấp nhận **bất kỳ** định dạng nào mà thư viện hỗ trợ—TIFF, PNG, JPEG, bạn gọi tên. Bước này trực tiếp đáp ứng yêu cầu **load image for OCR**.

```csharp
        // Load the image you want to process.
        // Replace the path with the actual location of your TIFF or other image.
        engine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/sample_multi_page.tif");
```

**Mẹo chuyên nghiệp:** Nếu bạn đang làm việc với TIFF đa trang, Aspose tự động coi mỗi trang là một khung riêng, và engine sẽ xử lý chúng tuần tự. Không cần mã bổ sung.

## Bước 3 – Run the recognition và **extract text from tiff**

Với engine đã sẵn sàng và hình ảnh đã được tải, chúng ta khởi động thao tác OCR. Phương thức `Recognize` trả về một `OcrResult` chứa văn bản thuần, điểm tin cậy và chi tiết thời gian.

```csharp
        // Perform the OCR operation.
        OcrResult result = engine.Recognize();
```

**Xử lý trường hợp đặc biệt:**  
Nếu GPU không khả dụng, `engine.Recognize()` vẫn hoạt động vì engine sẽ tự động chuyển sang CPU. Bạn có thể kiểm tra `engine.Device` sau khi nhận dạng nếu cần ghi lại thiết bị thực tế đã được sử dụng.

## Bước 4 – Lấy văn bản thuần đã nhận dạng

Việc trích xuất văn bản rất đơn giản—chỉ cần đọc thuộc tính `Text`. Đây là nơi chúng ta cuối cùng **extract text from tiff** (hoặc bất kỳ hình ảnh nào khác) và trình bày cho người dùng.

```csharp
        // Output the plain text that was extracted.
        Console.WriteLine($"Text:\n{result.Text}");
```

Bạn sẽ thấy các ký tự thô, ngắt dòng được giữ nguyên như trong hình ảnh nguồn. Đối với đầu ra có cấu trúc hơn (như JSON hoặc CSV), bạn có thể khám phá `result.Regions` và `result.Lines`, nhưng văn bản thuần thường đủ cho các script nhanh.

## Bước 5 – Đo thời gian xử lý và xử lý chuyển về CPU

Hiệu năng quan trọng, đặc biệt khi bạn xử lý hàng chục trang. Thuộc tính `ProcessingTime` cho bạn biết chính xác thời gian OCR mất, bất kể chạy trên GPU hay CPU.

```csharp
        // Show how long the recognition took.
        Console.WriteLine($"Time elapsed: {result.ProcessingTime.TotalSeconds}s");
    }
}
```

**Tại sao bạn nên quan tâm:**  
Nếu bạn thấy thời gian tăng đáng kể, bạn có thể muốn điều chỉnh `GpuMemoryLimit` hoặc chuyển sang CPU một cách rõ ràng (`Device = OcrDevice.Cpu`). Ngược lại, kết quả dưới một giây trên một TIFF lớn nghĩa là tăng tốc GPU của bạn đang hoạt động tốt.

## Ví dụ đầy đủ, sẵn sàng chạy

Sao chép mã dưới đây vào một dự án console mới (`dotnet new console -n OcrDemo`) và chạy `dotnet add package Aspose.OCR`. Sau đó thay thế `YOUR_DIRECTORY/sample_multi_page.tif` bằng đường dẫn tới hình ảnh của bạn.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine with GPU preference.
        OcrEngine engine = new OcrEngine
        {
            Device = OcrDevice.Gpu,
            GpuMemoryLimit = 1024
        };

        // Step 2: Load image for OCR (supports TIFF, PNG, JPEG, etc.).
        engine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/sample_multi_page.tif");

        // Step 3: Run recognition – this will also **extract text from tiff**.
        OcrResult result = engine.Recognize();

        // Step 4: Retrieve and display the recognized plain text.
        Console.WriteLine($"Text:\n{result.Text}");

        // Step 5: Display how long the operation took.
        Console.WriteLine($"Time elapsed: {result.ProcessingTime.TotalSeconds}s");
    }
}
```

**Kết quả mong đợi (rút gọn để ngắn gọn):**

```
Text:
Invoice #12345
Date: 2026-05-01
Total: $1,250.00
...
Time elapsed: 1.42s
```

Nếu máy của bạn không có GPU đủ mạnh, thời gian thực thi có thể dài hơn vài giây, nhưng văn bản vẫn sẽ được trích xuất đúng.

## Câu hỏi thường gặp & Những lưu ý

- **Nếu hình ảnh quá lớn (hơn 10 MB)?**  
  Giảm độ phân giải trước khi đưa vào engine, hoặc tăng `GpuMemoryLimit` nếu bạn có đủ VRAM.  
- **Tôi có thể xử lý nhiều hình ảnh trong một vòng lặp không?**  
  Chắc chắn. Chỉ cần tái sử dụng cùng một thể hiện `OcrEngine` và gán một `ImageStream` mới cho mỗi vòng lặp.  
- **Tôi có cần giải phóng bất kỳ tài nguyên nào không?**  
  `OcrEngine` triển khai `IDisposable`. Đặt nó trong khối `using` để quản lý tài nguyên sạch sẽ, đặc biệt khi làm việc với tài nguyên GPU.  

```csharp
using (OcrEngine engine = new OcrEngine { Device = OcrDevice.Gpu })
{
    // ... same steps as before
}
```

- **Còn các ngôn ngữ khác ngoài tiếng Anh thì sao?**  
  Đặt `engine.Language = OcrLanguage.Spanish` (hoặc bất kỳ ngôn ngữ nào được hỗ trợ) trước khi gọi `Recognize()`.

## Kết luận

Bây giờ bạn đã có một giải pháp hoàn chỉnh, đầu‑tới‑đầu để **recognize text from image** trong C# bằng Aspose OCR. Hướng dẫn đã đề cập cách **load image for OCR**, cách **extract text from tiff**, và cách đo hiệu năng trong khi xử lý chuyển về GPU một cách mượt mà.

Từ đây bạn có thể:

- Thử nghiệm với các định dạng hình ảnh khác nhau (BMP, PDF) để xem Aspose xử lý chúng như thế nào.  
- Khám phá `result.Regions` để lấy dữ liệu hộp bao nếu bạn cần nhận thức bố cục

## Bạn nên học gì tiếp theo?

- [Cách sử dụng Aspose để nhận dạng hình ảnh từ luồng trong OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [Trích xuất văn bản từ hình ảnh – Tối ưu hóa OCR với Aspose.OCR cho .NET](/ocr/english/net/ocr-optimization/)
- [Trích xuất văn bản từ hình ảnh – Nhận dạng dòng với Aspose.OCR](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}