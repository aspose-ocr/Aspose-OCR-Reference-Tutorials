---
category: general
date: 2026-02-14
description: Học cách thực hiện OCR trên tệp TIFF hoặc hình ảnh và chuyển đổi PDF
  bằng OCR để tạo PDF có thể tìm kiếm—hướng dẫn C# từng bước.
draft: false
keywords:
- how to perform OCR
- convert pdf using OCR
- make searchable pdf
- tiff to searchable pdf
- searchable pdf from image
language: vi
og_description: Khám phá cách thực hiện OCR trên hình ảnh, chuyển đổi PDF bằng OCR
  và tạo PDF có thể tìm kiếm với Aspose OCR trong một hướng dẫn C# ngắn gọn.
og_title: Cách thực hiện OCR và tạo PDF có thể tìm kiếm trong C#
tags:
- OCR
- C#
- Aspose
- PDF conversion
title: Cách thực hiện OCR và tạo PDF có thể tìm kiếm trong C#
url: /vi/net/text-recognition/how-to-perform-ocr-and-create-a-searchable-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Thực Hiện OCR và Tạo PDF Có Thể Tìm Kiếm trong C#

Bạn đã bao giờ **thực hiện OCR** trên một tài liệu đã quét nhưng không chắc làm sao để chuyển kết quả thành PDF có thể tìm kiếm? Bạn không phải là người duy nhất—nhiều nhà phát triển gặp phải rào cản này khi làm việc với các kho lưu trữ TIFF cũ hoặc PDF chỉ chứa hình ảnh. Tin tốt là gì? Chỉ với vài dòng C# và thư viện Aspose.OCR, bạn có thể chuyển đổi một TIFF hoặc bất kỳ hình ảnh nào thành PDF có thể tìm kiếm đầy đủ chỉ trong vài giây.

Trong hướng dẫn này, chúng ta sẽ đi qua mọi thứ bạn cần biết: từ cài đặt thư viện, tải một TIFF đa trang, đến việc gọi `RecognizeToPdf` để bạn có thể **chuyển đổi PDF bằng OCR** và **tạo file PDF có thể tìm kiếm** mà người dùng thực sự có thể tìm kiếm. Khi kết thúc, bạn sẽ có một ứng dụng console sẵn sàng chạy, tạo ra PDF có thể tìm kiếm từ nguồn hình ảnh.

## Yêu Cầu Trước

- **.NET 6.0** trở lên (mã cũng hoạt động trên .NET Framework 4.7+).
- Giấy phép **Aspose.OCR** hợp lệ hoặc khóa đánh giá tạm thời (bản dùng thử miễn phí đủ cho việc thử nghiệm).
- Visual Studio 2022 (hoặc bất kỳ trình soạn thảo nào bạn thích) với **NuGet** package manager.
- Một tệp đầu vào có tên `input.tif` đặt trong thư mục bạn kiểm soát—các TIFF đa trang hoạt động ngay lập tức.

> **Mẹo chuyên nghiệp:** Nếu bạn đang dùng Windows, sao chép TIFF vào cùng thư mục với file `.exe` đã biên dịch để tránh các rắc rối liên quan đến đường dẫn.

## Bước 1: Cài Đặt Gói NuGet Aspose.OCR

Mở thư mục dự án của bạn trong terminal và chạy:

```bash
dotnet add package Aspose.OCR
```

Lệnh này sẽ tải phiên bản ổn định mới nhất (tính đến tháng 2 2026 là 23.10) và thêm tất cả các phụ thuộc cần thiết. Sau khi khôi phục hoàn tất, bạn sẽ thấy `Aspose.OCR` xuất hiện dưới **Dependencies** trong Solution Explorer.

## Bước 2: Tạo Ứng Dụng Console Tối Thiểu

Tạo một dự án console mới nếu bạn chưa có:

```bash
dotnet new console -n OcrSearchablePdfDemo
cd OcrSearchablePdfDemo
```

Thay thế `Program.cs` được tạo tự động bằng mã đầy đủ được hiển thị trong **Bước 3**. Chương trình sẽ:

1. Khởi tạo engine OCR.
2. Tải hình ảnh nguồn (hoặc TIFF đa trang).
3. Thực hiện OCR và ghi đầu ra trực tiếp vào PDF có thể tìm kiếm.
4. Thông báo cho người dùng rằng quá trình đã thành công.

## Bước 3: Mã Hoàn Chỉnh – Từ Hình Ảnh Đến PDF Có Thể Tìm Kiếm

Dưới đây là **toàn bộ** file nguồn. Sao chép‑dán nó vào `Program.cs`. Các chú thích được bao gồm để giải thích những phần không hiển nhiên.

```csharp
using System;
using Aspose.OCR;          // Core OCR namespace
using Aspose.OCR.Image;   // Provides ImageStream helpers

namespace OcrSearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Initialise the OCR engine.
            // -------------------------------------------------
            // The Engine class is the entry point for all OCR operations.
            // You can optionally pass a license object here if you have one.
            var ocrEngine = new Engine();

            // -------------------------------------------------
            // 2️⃣ Load the source image.
            // -------------------------------------------------
            // ImageStream.FromFile supports TIFF, PDF, JPEG, PNG, etc.
            // For multi‑page TIFFs the stream automatically contains all pages.
            string inputPath = "YOUR_DIRECTORY/input.tif";
            var imageStream = ImageStream.FromFile(inputPath);

            // -------------------------------------------------
            // 3️⃣ Perform OCR and write a searchable PDF.
            // -------------------------------------------------
            // RecognizeToPdf does the heavy lifting:
            // • It runs the OCR engine on every page.
            // • It embeds the extracted text as an invisible layer.
            // • The visual appearance of the original image is preserved.
            string outputPath = "YOUR_DIRECTORY/searchable.pdf";
            ocrEngine.RecognizeToPdf(imageStream, outputPath);

            // -------------------------------------------------
            // 4️⃣ Inform the user.
            // -------------------------------------------------
            Console.WriteLine("Searchable PDF created at: " + outputPath);
        }
    }
}
```

**Bạn sẽ thấy gì:** Sau khi chạy chương trình, một tệp có tên `searchable.pdf` sẽ xuất hiện trong thư mục đích. Mở nó bằng Adobe Reader hoặc bất kỳ trình xem PDF nào và thử tìm kiếm một từ có trong TIFF gốc. Văn bản sẽ được tìm ngay lập tức, chứng minh bạn đã **tạo PDF có thể tìm kiếm** từ hình ảnh thành công.

### Chạy Ứng Dụng

```bash
dotnet run
```

Nếu mọi thứ được thiết lập đúng, bạn sẽ nhận được:

```
Searchable PDF created at: YOUR_DIRECTORY/searchable.pdf
```

Mở PDF, nhấn `Ctrl+F`, gõ một từ từ nguồn, và xem phần nổi bật nhảy tới vị trí chính xác.

## Bước 4: Các Biến Thể Thông Thường và Trường Hợp Cạnh

### Chuyển Đổi PDF Thông Thường (chỉ hình ảnh) Thành PDF Có Thể Tìm Kiếm

Nếu nguồn của bạn là một PDF chứa các hình ảnh đã quét thay vì văn bản, bạn vẫn có thể sử dụng cùng một phương pháp—chỉ cần thay đổi nguồn `ImageStream`:

```csharp
var pdfStream = ImageStream.FromFile("YOUR_DIRECTORY/input.pdf");
ocrEngine.RecognizeToPdf(pdfStream, "YOUR_DIRECTORY/searchable_from_pdf.pdf");
```

Điều này đáp ứng kịch bản **convert pdf using OCR** mà không cần thêm mã nào.

### Xử Lý Tài Liệu Đa Trang Lớn

Đối với các tài liệu vượt quá vài trăm trang, hãy cân nhắc:

- **Tăng giới hạn bộ nhớ** (`Engine.MemoryLimit = 2_000; // MB`).
- **Xử lý theo lô**: tải một tập hợp con các trang, ghi các PDF trung gian, sau đó hợp nhất chúng bằng một thư viện PDF (ví dụ, Aspose.PDF).

### Xử Lý Các Ngôn Ngữ Không Phải Tiếng Anh

Aspose.OCR hỗ trợ nhiều ngôn ngữ ngay từ đầu. Đặt ngôn ngữ trước khi nhận dạng:

```csharp
ocrEngine.Language = OcrLanguage.French; // or OcrLanguage.Spanish, etc.
```

Nếu bạn cần **tiff to searchable pdf** cho một script không phải Latin, hãy chắc chắn rằng gói ngôn ngữ phù hợp đã được cài đặt.

### PDF Đầu Ra Bị Trống thì sao?

- Kiểm tra xem tệp đầu vào có bị hỏng không.
- Đảm bảo engine OCR có giấy phép hợp lệ—chế độ đánh giá có thể áp đặt giới hạn số trang.
- Kiểm tra độ phân giải hình ảnh ít nhất là 300 dpi; độ phân giải thấp hơn có thể gây nhận dạng kém.

## Bước 5: Xác Thực Kết Quả Bằng Chương Trình (Tùy Chọn)

Đôi khi bạn muốn xác nhận rằng PDF thực sự chứa lớp văn bản. Bạn có thể dùng Aspose.PDF để trích xuất văn bản:

```csharp
using Aspose.Pdf;

var pdfDoc = new Document("YOUR_DIRECTORY/searchable.pdf");
string extracted = pdfDoc.Pages[1].ExtractText();
Console.WriteLine("First page text snippet: " + extracted.Substring(0, 100));
```

Nếu `extracted` không rỗng, bạn đã **tạo searchable pdf** thành công.

## Kết Luận

Chúng ta đã đi qua **cách thực hiện OCR** trên một TIFF (hoặc bất kỳ hình ảnh nào) và liền mạch **chuyển đổi PDF bằng OCR** để tạo ra một **PDF có thể tìm kiếm** hoạt động như một tài liệu gốc. Các bước chính là:

1. Cài đặt Aspose.OCR.  
2. Khởi tạo `Engine`.  
3. Tải hình ảnh qua `ImageStream`.  
4. Gọi `RecognizeToPdf`.  

Từ đây bạn có thể thử nghiệm các cài đặt ngôn ngữ, xử lý hàng loạt lớn, hoặc kết hợp đầu ra với các tác vụ xử lý PDF khác. Mẫu này cũng hoạt động cho **tiff to searchable pdf**, **searchable pdf from image**, và thậm chí các PDF đã quét.

Sẵn sàng cho thử thách tiếp theo? Hãy thử nhúng OCR vào một web API để người dùng có thể tải lên các bản quét và nhận PDF có thể tìm kiếm ngay lập tức, hoặc khám phá OCR trên ghi chú viết tay bằng các cài đặt nâng cao của `OcrEngine`. Khả năng là vô hạn—chúc bạn lập trình vui vẻ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}