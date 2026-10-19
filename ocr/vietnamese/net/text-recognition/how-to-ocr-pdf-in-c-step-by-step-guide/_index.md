---
category: general
date: 2025-12-29
description: Học cách OCR tệp PDF trong C# và trích xuất văn bản từ các trang PDF.
  Bài hướng dẫn này cũng bao gồm cách chuyển PDF sang văn bản và các kỹ thuật đọc
  trang PDF bằng C#.
draft: false
keywords:
- how to ocr pdf
- extract text from pdf
- convert pdf to text
- extract pdf text c#
- read pdf page c#
language: vi
og_description: Cách OCR PDF trong C# được giải thích trong một hướng dẫn ngắn gọn.
  Nhận mã đầy đủ để trích xuất văn bản từ PDF, chuyển PDF sang văn bản và đọc trang
  PDF bằng C#.
og_title: Cách OCR PDF trong C# – Hướng dẫn lập trình đầy đủ
tags:
- OCR
- C#
- PDF processing
title: Cách OCR PDF trong C# – Hướng dẫn từng bước
url: /vi/net/text-recognition/how-to-ocr-pdf-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách OCR PDF trong C# – Hướng dẫn từng bước

Bạn đã bao giờ tự hỏi **cách OCR PDF** trực tiếp từ ứng dụng C# của mình chưa? Có thể bạn có một đống hoá đơn đã quét và cần trích xuất văn bản mà không phải sao chép thủ công. Đó là một vấn đề phổ biến, đặc biệt khi các PDF là dạng hình ảnh và việc trích xuất văn bản truyền thống không hoạt động.  

Trong tutorial này, chúng tôi sẽ hướng dẫn bạn qua một giải pháp hoàn chỉnh, sẵn sàng chạy, không chỉ cho bạn biết **cách OCR PDF** mà còn minh họa cách *extract text from PDF*, *convert PDF to text*, và *read PDF page C#* bằng thư viện Aspose.OCR. Không có những tham chiếu mơ hồ—chỉ có mã bạn có thể chèn vào Visual Studio và bắt đầu thử nghiệm.

## Những gì bạn cần

- **.NET 6.0** hoặc mới hơn (mã cũng chạy trên .NET Framework 4.7+)  
- Gói NuGet **Aspose.OCR** – cài đặt bằng `dotnet add package Aspose.OCR`  
- Một PDF đã quét (ví dụ, `invoice.pdf`) đặt trong thư mục bạn có thể tham chiếu  
- Kiến thức cơ bản về ứng dụng console C#  

Chỉ vậy thôi. Nếu bạn đã có dự án, chỉ cần thêm gói và bạn đã sẵn sàng.

## Bước 1: Thiết lập dự án và thêm Aspose.OCR

Đầu tiên, tạo một dự án console mới (hoặc sử dụng dự án hiện có) và đưa thư viện OCR vào.

```csharp
// Create a new console app (run this in a terminal)
// > dotnet new console -n OcrPdfDemo
// > cd OcrPdfDemo
// > dotnet add package Aspose.OCR
```

Tại sao bước này quan trọng: Aspose.OCR thực hiện các công việc nặng như phân tích hình ảnh, phát hiện bố cục và nhận dạng ký tự. Nếu không có nó, bạn sẽ phải ghép nối một rasterizer, một engine Tesseract và rất nhiều mã nối.

## Bước 2: Nhập các namespace và chuẩn bị OcrEngine

Bây giờ mở `Program.cs` (hoặc bất kỳ tệp .cs nào bạn muốn) và thêm các chỉ thị `using` cần thiết.

```csharp
using System;
using Aspose.OCR;   // Core OCR classes
```

Việc tạo engine rất đơn giản, nhưng chúng ta cũng sẽ cấu hình một vài tùy chọn để cải thiện độ chính xác trên các hoá đơn thường gặp.

```csharp
// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine
{
    // Enable automatic language detection (optional but handy)
    Language = Language.English,
    // Turn on deskew to correct rotated pages
    ImagePreprocessingOptions = new ImagePreprocessingOptions
    {
        Deskew = true,
        Binarization = true
    }
};
```

**Mẹo chuyên nghiệp:** Nếu bạn biết ngôn ngữ trước, hãy đặt `Language` một cách rõ ràng; nó sẽ tăng tốc quá trình.

## Bước 3: Chỉ đến tệp PDF của bạn

Xác định đường dẫn tuyệt đối hoặc tương đối tới PDF bạn muốn xử lý. Trong ví dụ này, chúng tôi sẽ giả sử tệp nằm trong thư mục có tên `Samples`.

```csharp
// Path to the PDF you want to OCR
string pdfFilePath = @"Samples/invoice.pdf";

// Verify the file exists early to avoid runtime surprises
if (!System.IO.File.Exists(pdfFilePath))
{
    Console.WriteLine($"File not found: {pdfFilePath}");
    return;
}
```

Kiểm tra sự tồn tại của tệp là một bước nhỏ, nhưng nó giúp bạn tránh các ngoại lệ khó hiểu sau này.

## Bước 4: Chọn trang (các trang) để đọc

Một PDF có thể có hàng chục trang, nhưng thường bạn chỉ cần một trang cụ thể—ví dụ, trang thứ hai của hoá đơn nơi tổng số tiền nằm. Phương thức `RecognizePdf` cho phép bạn chỉ định một trang duy nhất hoặc toàn bộ tài liệu.

```csharp
// Extract text from page 2 (page numbers are 1‑based)
int pageNumber = 2;

// The method returns an OcrResult containing the recognized text
OcrResult ocrResult = ocrEngine.RecognizePdf(pdfFilePath, pageNumber);
```

Nếu bạn muốn *convert PDF to text* cho toàn bộ tài liệu, chỉ cần bỏ qua đối số `pageNumber`:

```csharp
// OcrResult fullResult = ocrEngine.RecognizePdf(pdfFilePath);
```

## Bước 5: Hiển thị hoặc lưu văn bản đã trích xuất

Bây giờ OCR engine đã hoàn thành công việc, bạn có thể in văn bản ra console, ghi vào tệp `.txt`, hoặc đưa vào hệ thống khác (ví dụ, cơ sở dữ liệu).

```csharp
// Show the recognized text in the console
Console.WriteLine("=== OCR Result (Page {0}) ===", pageNumber);
Console.WriteLine(ocrResult.Text);

// Optionally, save to a .txt file
string outputPath = $"output_page{pageNumber}.txt";
System.IO.File.WriteAllText(outputPath, ocrResult.Text);
Console.WriteLine($"Text saved to {outputPath}");
```

**Tại sao điều này quan trọng:** Bằng cách lưu trữ kết quả, bạn tạo ra một tài sản có thể tái sử dụng—hoàn hảo cho phân tích downstream hoặc lập chỉ mục tìm kiếm.

## Ví dụ hoàn chỉnh hoạt động

Kết hợp tất cả lại, đây là một chương trình tự chứa mà bạn có thể sao chép‑dán vào `Program.cs` và chạy ngay lập tức.

```csharp
using System;
using Aspose.OCR;

namespace OcrPdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine with helpful options
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.English,
                ImagePreprocessingOptions = new ImagePreprocessingOptions
                {
                    Deskew = true,
                    Binarization = true
                }
            };

            // 2️⃣ Define the PDF path
            string pdfFilePath = @"Samples/invoice.pdf";
            if (!System.IO.File.Exists(pdfFilePath))
            {
                Console.WriteLine($"Error: File not found -> {pdfFilePath}");
                return;
            }

            // 3️⃣ Choose which page to OCR (change as needed)
            int pageNumber = 2; // read PDF page C# example

            // 4️⃣ Perform OCR on the selected page
            OcrResult ocrResult = ocrEngine.RecognizePdf(pdfFilePath, pageNumber);

            // 5️⃣ Output the result
            Console.WriteLine($"--- OCR Result for page {pageNumber} ---");
            Console.WriteLine(ocrResult.Text);

            // 6️⃣ Save to a text file for later use
            string outputPath = $"output_page{pageNumber}.txt";
            System.IO.File.WriteAllText(outputPath, ocrResult.Text);
            Console.WriteLine($"Extracted text saved to: {outputPath}");
        }
    }
}
```

### Kết quả mong đợi

```
--- OCR Result for page 2 ---
Invoice #12345
Date: 2024‑11‑30
Total: $1,250.00
...
Extracted text saved to: output_page2.txt
```

Nếu PDF chứa các bản quét rõ ràng, độ phân giải cao, kết quả sẽ gần như hoàn hảo. Hình ảnh chất lượng thấp có thể cần tiền xử lý bổ sung (ví dụ, tăng DPI hoặc áp dụng bộ lọc); `ImagePreprocessingOptions` của Aspose.OCR có thể điều chỉnh để phù hợp với những trường hợp đó.

## Các câu hỏi thường gặp & trường hợp đặc biệt

### 1️⃣ Nếu PDF được bảo mật bằng mật khẩu thì sao?

`RecognizePdf` overload của Aspose.OCR chấp nhận một đối tượng `PdfLoadOptions` nơi bạn có thể đặt mật khẩu:

```csharp
var loadOptions = new PdfLoadOptions { Password = "mySecret" };
OcrResult result = ocrEngine.RecognizePdf(pdfFilePath, pageNumber, loadOptions);
```

### 2️⃣ Tôi có thể OCR toàn bộ tài liệu một lần không?

Có—chỉ cần gọi `RecognizePdf(pdfFilePath)` mà không chỉ định số trang. Phương thức trả về một `OcrResult` duy nhất chứa văn bản đã nối từ tất cả các trang.

### 3️⃣ Điều này khác như thế nào so với “extract text from PDF” bằng thư viện dựa trên văn bản?

Việc trích xuất văn bản thuần (ví dụ, dùng iTextSharp) chỉ hoạt động trên các PDF đã có văn bản có thể chọn được. **Cách OCR PDF** là cần thiết khi PDF thực chất là tập hợp các hình ảnh, như hoá đơn đã quét. Trong những trường hợp này, OCR engine thực hiện nhận dạng ký tự quang học để biến hình ảnh thành văn bản có thể tìm kiếm.

### 4️⃣ Hiệu năng khi xử lý PDF lớn như thế nào?

Thời gian xử lý tăng gần như tuyến tính với số trang và độ phân giải hình ảnh. Đối với công việc hàng loạt, hãy cân nhắc:
- Chạy OCR song song (`Parallel.ForEach`)  
- Giảm DPI của hình ảnh trước OCR (`Resolution = 150`)  
- Lưu cache đối tượng `OcrEngine` thay vì tạo mới cho mỗi tệp

### 5️⃣ Có cách nào để lấy bounding box của mỗi từ không?

`OcrResult` cung cấp một tập hợp các đối tượng `OcrRegion`, mỗi đối tượng chứa tọa độ. Bạn có thể duyệt qua chúng để tạo PDF có thể tìm kiếm hoặc làm nổi bật kết quả trong giao diện người dùng.

```csharp
foreach (var region in ocrResult.Regions)
{
    Console.WriteLine($"{region.Text} – ({region.Bounds.X}, {region.Bounds.Y}, {region.Bounds.Width}, {region.Bounds.Height})");
}
```

## Mẹo cho triển khai sẵn sàng sản xuất

- **Xử lý lỗi:** Bao bọc các lời gọi OCR trong khối try/catch để hiển thị các ngoại lệ đặc thù của thư viện.  
- **Ghi log:** Ghi lại số trang và thời gian xử lý; chúng giúp phát hiện các bản quét có vấn đề.  
- **Quản lý bộ nhớ:** Giải phóng các đối tượng `Bitmap` lớn nếu bạn tự chuyển đổi các trang PDF thành hình ảnh trước khi OCR.  
- **Bảo mật:** Không bao giờ lưu trữ PDF thô trên đĩa không an toàn; hãy cân nhắc truyền trực tiếp chúng vào OCR engine.  

## Kết luận

Bây giờ bạn đã có một câu trả lời toàn diện, đầu‑tới‑cuối cho **cách OCR PDF** bằng C#. Tutorial đã bao phủ mọi thứ từ cài đặt Aspose.OCR, chọn trang cụ thể, trích xuất văn bản, và xử lý các trường hợp đặc biệt phổ biến. Với nền tảng này, bạn có thể *extract text from PDF*, *convert PDF to text*, và *read PDF page C#* cho bất kỳ pipeline xử lý tài liệu nào bạn đang xây dựng.

Sẵn sàng cho bước tiếp theo? Hãy thử đưa kết quả OCR vào công cụ tìm kiếm toàn văn như Lucene.NET, hoặc tạo PDF có thể tìm kiếm bằng cách phủ lên văn bản đã nhận dạng lên các hình ảnh gốc. Không có giới hạn, và bạn đã có công cụ để thực hiện.

---

![how to ocr pdf example](image-placeholder.png "Illustration of OCR processing on a PDF page")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}