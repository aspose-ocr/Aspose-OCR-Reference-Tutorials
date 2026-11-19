---
category: general
date: 2026-05-21
description: Thực hiện OCR trên hình ảnh bằng C#. Tìm hiểu cách tải hình ảnh cho OCR,
  trích xuất văn bản từ PNG và nhận dạng văn bản từ hình ảnh bằng một đoạn mã ngắn.
draft: false
keywords:
- perform OCR on image
- extract text from PNG
- recognize text from image
- load image for OCR
language: vi
og_description: Thực hiện OCR trên hình ảnh trong C# nhanh chóng. Hướng dẫn này chỉ
  cách tải hình ảnh để OCR, trích xuất văn bản từ PNG và nhận dạng văn bản từ hình
  ảnh với đầu ra HTML nhận biết bố cục.
og_title: Thực hiện OCR trên ảnh bằng C# – Hướng dẫn lập trình đầy đủ
schemas:
- author: Aspose
  dateModified: '2026-05-21'
  description: Perform OCR on image using C#. Learn how to load image for OCR, extract
    text from PNG, and recognize text from image with a tiny code sample.
  headline: Perform OCR on Image with C# – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Perform OCR on image using C#. Learn how to load image for OCR, extract
    text from PNG, and recognize text from image with a tiny code sample.
  name: Perform OCR on Image with C# – Complete Step‑by‑Step Guide
  steps:
  - name: Load Image for OCR
    text: The line `engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.png");`
      is where we **load image for OCR**. The `ImageStream` helper abstracts away
      file‑format details, so you can feed JPEG, BMP, or TIFF without changing code.
  - name: Extract Text from PNG
    text: 'Once `engine.Recognize()` finishes, the OCR engine holds the recognized
      text internally. You can pull it out as a string if you only need raw text:'
  - name: Recognize Text from Image
    text: 'The `Recognize()` call does the heavy lifting. Under the hood the engine:'
  - name: Handling Layout‑Aware HTML Output
    text: 'Most developers stop at plain text, but the `HtmlSaveOptions` we used let
      you **perform OCR on image** and keep the visual structure intact. Two flags
      matter:'
  - name: Scaling to Multiple Files
    text: 'If you need to **perform OCR on image** files in a folder, wrap the core
      logic in a simple loop:'
  type: HowTo
tags:
- OCR
- C#
- Image Processing
- Aspose.OCR
title: Thực hiện OCR trên hình ảnh bằng C# – Hướng dẫn chi tiết từng bước
url: /vi/net/text-recognition/perform-ocr-on-image-with-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Thực hiện OCR trên Hình ảnh với C# – Hướng dẫn chi tiết từng bước

Bạn đã bao giờ tự hỏi làm thế nào để **perform OCR on image** các tệp mà không phải vật lộn với các giao diện nặng? Bạn không phải là người duy nhất. Dù bạn đang số hoá biên lai, trích xuất dữ liệu từ các mẫu quét, hay chỉ cần chuyển một PNG thành văn bản có thể tìm kiếm, chỉ vài dòng C# cũng có thể hoàn thành công việc.

Trong hướng dẫn này, chúng ta sẽ đi qua việc tải hình ảnh cho OCR, nhận dạng văn bản từ hình ảnh, và cuối cùng trích xuất văn bản từ PNG dưới dạng HTML sạch. Khi kết thúc, bạn sẽ có một ứng dụng console sẵn sàng chạy mà **performs OCR on image** các tệp và giữ nguyên bố cục gốc.

## Những gì bạn sẽ xây dựng

- Một chương trình console tối thiểu đọc một PNG (hoặc bất kỳ hình ảnh nào được hỗ trợ)  
- Sử dụng một engine OCR để **recognize text from image**  
- Lưu kết quả dưới dạng HTML có nhận thức bố cục, nhúng ảnh gốc  
- Hiển thị cách **load image for OCR**, **extract text from PNG**, và xử lý các trường hợp đặc biệt thường gặp  

> **Prerequisites**  
> - .NET 6.0 SDK hoặc phiên bản mới hơn (bạn cũng có thể nhắm tới .NET Framework 4.7+)  
> - Thư viện OCR tương thích NuGet – ví dụ sử dụng *Aspose.OCR* nhưng bất kỳ thư viện nào có API tương tự đều hoạt động  
> - Kiến thức cơ bản về C# (không cần phức tạp)  

Có đầy đủ chưa? Tuyệt—hãy bắt đầu.

## Thực hiện OCR trên Hình ảnh – Hướng dẫn mã đầy đủ

Dưới đây là chương trình **complete, runnable**. Sao chép‑dán nó vào một dự án console mới (`dotnet new console`) và nhấn **F5**.

```csharp
using System;
using Aspose.OCR;               // OCR engine namespace
using Aspose.OCR.Models;        // Save options namespace
using Aspose.OCR.ImageProcessing; // Image loading helpers

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Create an OCR engine and set the language
            // -------------------------------------------------
            var engine = new OcrEngine
            {
                Language = OcrLanguage.English   // You can change to French, German, etc.
            };

            // -------------------------------------------------
            // Step 2: Load the image for OCR
            // -------------------------------------------------
            // Replace the path with your actual PNG/JPEG/TIFF file.
            engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.png");

            // -------------------------------------------------
            // Step 3: Perform OCR recognition
            // -------------------------------------------------
            engine.Recognize();

            // -------------------------------------------------
            // Step 4: Configure HTML save options – keep layout
            // -------------------------------------------------
            var htmlOptions = new HtmlSaveOptions
            {
                PreserveLayout = true,   // Keep columns, tables, and spacing
                EmbedImages = true       // Embed the original PNG inside the HTML
            };

            // -------------------------------------------------
            // Step 5: Save the recognized content as layout‑aware HTML
            // -------------------------------------------------
            engine.Save("YOUR_DIRECTORY/form.html", htmlOptions);

            Console.WriteLine("HTML with layout saved.");
        }
    }
}
```

> **Expected output**  
> ```
> HTML with layout saved.
> ```  
> Sau khi chạy, bạn sẽ thấy `form.html` nằm cạnh PNG của bạn. Mở nó trong trình duyệt và bạn sẽ thấy bố cục giống hệt, nhưng bây giờ văn bản có thể chọn và tìm kiếm.

### Tải hình ảnh cho OCR

Dòng `engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.png");` là nơi chúng ta **load image for OCR**. Trợ giúp `ImageStream` ẩn đi chi tiết định dạng tệp, vì vậy bạn có thể cung cấp JPEG, BMP, hoặc TIFF mà không cần thay đổi mã.

**Why not just pass a `Bitmap`?**  
Bởi vì nhiều SDK OCR yêu cầu một stream cũng chứa siêu dữ liệu DPI. Sử dụng bộ tải tích hợp của thư viện đảm bảo engine nhìn thấy hình ảnh chính xác như trên màn hình, giúp tăng độ chính xác.

#### Pro tip
Nếu bạn đang xử lý một loạt tệp, hãy bao bọc bước tải trong một `try/catch` và ghi lại bất kỳ `FileNotFoundException` nào. Điều này ngăn toàn bộ lô bị sập vì một tệp bị thiếu.

### Trích xuất Văn bản từ PNG

Khi `engine.Recognize()` hoàn thành, engine OCR giữ văn bản đã nhận dạng bên trong. Bạn có thể lấy ra dưới dạng chuỗi nếu chỉ cần văn bản thô:

```csharp
string plainText = engine.Text;   // Returns the whole document as plain text
Console.WriteLine(plainText);
```

Đây là cách nhanh nhất để **extract text from PNG** khi bạn không quan tâm tới bố cục. Đối với hầu hết các công việc nhập dữ liệu, văn bản thuần là đủ—chỉ cần nhớ loại bỏ các ngắt dòng nếu bạn dự định nhập vào CSV.

### Nhận dạng Văn bản từ Hình ảnh

Lệnh `Recognize()` thực hiện phần công việc nặng. Bên trong engine:

1. Chuẩn hoá hình ảnh (sửa lệch, loại bỏ nhiễu)  
2. Phân đoạn thành các dòng và từ  
3. Chạy bộ phân loại mạng nơ‑ron đã được huấn luyện trên hàng triệu glyph  

Vì chúng ta đặt `Language = OcrLanguage.English`, engine áp dụng từ điển đặc thù cho tiếng Anh, giảm đáng kể các kết quả sai. Nếu bạn cần hỗ trợ đa ngôn ngữ, chỉ cần truyền một mảng các ngôn ngữ:

```csharp
engine.Language = OcrLanguage.English | OcrLanguage.Spanish;
```

### Xử lý Đầu ra HTML Nhận thức Bố cục

Hầu hết các nhà phát triển chỉ dừng ở văn bản thuần, nhưng `HtmlSaveOptions` mà chúng tôi sử dụng cho phép bạn **perform OCR on image** và giữ nguyên cấu trúc hình ảnh. Hai cờ quan trọng:

- `PreserveLayout = true` – giữ lại cột, bảng và khoảng cách.  
- `EmbedImages = true` – chèn PNG gốc dưới dạng phần tử `<img>` được mã hoá Base64, vì vậy HTML tự chứa.

Nếu bạn muốn tệp nhẹ hơn, đặt `EmbedImages = false` và HTML sẽ tham chiếu tới PNG gốc trên đĩa.

#### Trường hợp đặc biệt: Tệp lớn

Đối với các hình ảnh lớn hơn 5 MB, việc nhúng có thể làm tăng kích thước HTML rất lớn. Trong những trường hợp này, hãy chuyển sang tham chiếu ảnh bên ngoài và cân nhắc nén PNG trước bằng `ImageProcessor.Compress`.

## Những Cạm Bẫy Thông Thường và Mẹo Chuyên Gia

| Symptom | Likely Cause | Fix |
|--------|--------------|-----|
| Ký tự bị rối | Đặt ngôn ngữ sai hoặc thiếu gói ngôn ngữ | Cài đặt các tệp dữ liệu ngôn ngữ phù hợp và đặt `engine.Language` đúng |
| Không có văn bản trong đầu ra | Hình ảnh quá tối hoặc độ phân giải thấp | Tiền xử lý bằng `engine.Image = ImageProcessor.AdjustContrast(engine.Image, 1.2)` |
| Bố cục bị phá vỡ trong HTML | `PreserveLayout` để mặc định `false` | Đặt `PreserveLayout = true` trong `HtmlSaveOptions` |
| Xử lý chậm khi nhiều trang | Engine khởi tạo lại cho mỗi tệp | Tái sử dụng cùng một thể hiện `OcrEngine` và chỉ thay đổi `engine.Image` mỗi vòng lặp |

### Mở rộng cho Nhiều Tệp

Nếu bạn cần **perform OCR on image** các tệp trong một thư mục, hãy bao bọc logic chính trong một vòng lặp đơn giản:

```csharp
foreach (var file in Directory.GetFiles("YOUR_DIRECTORY", "*.png"))
{
    engine.Image = ImageStream.FromFile(file);
    engine.Recognize();
    var htmlPath = Path.ChangeExtension(file, ".html");
    engine.Save(htmlPath, htmlOptions);
    Console.WriteLine($"Processed {Path.GetFileName(file)}");
}
```

Chú ý chúng tôi **load image for OCR** bên trong vòng lặp, nhưng giữ cùng một đối tượng `engine` và `htmlOptions`. Điều này giảm việc tiêu tốn bộ nhớ và tăng tốc các công việc batch.

## Vượt Xa: Xuất ra PDF hoặc DOCX

Cùng một `engine` có thể lưu sang các định dạng khác:

```csharp
engine.Save("output.pdf", new PdfSaveOptions { PreserveLayout = true });
engine.Save("output.docx", new WordSaveOptions { PreserveLayout = true });
```

Nếu hệ thống downstream của bạn yêu cầu PDF có thể tìm kiếm, đây là một thay đổi một dòng—không cần viết một pipeline chuyển đổi riêng.

## Kết luận

Chúng tôi vừa cho bạn thấy cách **perform OCR on image** các tệp với C#, từ tải ảnh đến **extract text from PNG** và cuối cùng **recognize text from image** thành một tệp HTML nhận thức bố cục. Ví dụ đầy đủ đã sẵn sàng chạy, và bạn đã hiểu tại sao mỗi bước quan trọng, cách điều chỉnh cho các ngôn ngữ khác nhau, và những cạm bẫy cần lưu ý.

Tiếp theo, hãy thử thay đổi ngôn ngữ tiếng Anh sang một ngôn ngữ khác, thử nghiệm với `PreserveLayout = false` để có HTML nhẹ hơn, hoặc chuyển đầu ra văn bản thuần vào cơ sở dữ liệu để lưu trữ có thể tìm kiếm. Không gì là không thể khi bạn kết hợp một engine OCR mạnh mẽ với vài dòng C#.

Có câu hỏi về việc xử lý TIFF đa trang, hoặc muốn biết cách tích hợp điều này vào ASP.NET Core API? Để lại bình luận bên dưới, và chúc bạn lập trình vui!

## Các Hướng Dẫn Liên Quan

- [Trích xuất văn bản hình ảnh C# với lựa chọn ngôn ngữ bằng Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Cách Trích xuất Văn bản từ Hình ảnh bằng cách Chuẩn bị Hình chữ nhật trong OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Trích xuất Văn bản từ Hình ảnh – Nhận dạng Dòng với Aspose.OCR](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}