---
category: general
date: 2026-05-06
description: Tạo PDF có thể tìm kiếm từ hình ảnh bằng Aspose OCR trong C#. Học cách
  chuyển đổi PNG sang PDF, trích xuất văn bản từ hình ảnh và tạo PDF có thể tìm kiếm.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- extract text from image
- convert png to pdf
- ocr image to pdf
language: vi
og_description: Tạo PDF có thể tìm kiếm từ hình ảnh bằng Aspose OCR trong C#. Hướng
  dẫn chi tiết này cho thấy cách chuyển đổi PNG sang PDF, trích xuất văn bản từ hình
  ảnh và tạo ra PDF có thể tìm kiếm.
og_title: Tạo PDF có thể tìm kiếm từ hình ảnh – Hướng dẫn OCR Aspose bằng C#
tags:
- Aspose
- C#
- OCR
- PDF
title: Tạo PDF có thể tìm kiếm từ hình ảnh – Hướng dẫn OCR Aspose bằng C#
url: /vi/net/text-recognition/create-searchable-pdf-from-image-c-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo PDF có thể tìm kiếm từ Hình ảnh – Hướng dẫn C# Aspose OCR

Bạn đã bao giờ cần **tạo PDF có thể tìm kiếm** từ một bức ảnh đã quét nhưng không biết bắt đầu từ đâu? Có thể bạn có một biên lai PNG, một JPEG của hợp đồng, hoặc bất kỳ bitmap nào mà bạn muốn chuyển thành PDF mà thực sự có thể tìm kiếm. Đó là một vấn đề phổ biến, đặc biệt khi bạn phải làm việc với các bản quét cũ nằm im trong một thư mục.

Tin tốt là với Aspose OCR bạn có thể **chuyển đổi hình ảnh sang PDF**, lấy ra văn bản ẩn và có được một tài liệu hoàn toàn có thể tìm kiếm — chỉ trong vài dòng C#. Trong hướng dẫn này chúng tôi cũng sẽ chỉ cho bạn cách **chuyển đổi png sang PDF**, **trích xuất văn bản từ hình ảnh**, và thậm chí đề cập đến trường hợp đặc biệt khi xử lý TIFF đa trang. Khi kết thúc, bạn sẽ có một giải pháp tự chứa mà bạn có thể đưa vào bất kỳ dự án .NET nào.

## Những gì bạn cần

- **.NET 6+** (mã hoạt động trên .NET Framework 4.6+ cũng được)
- **Visual Studio 2022** hoặc bất kỳ IDE nào bạn thích
- **Aspose.OCR** gói NuGet (nó sẽ tự động kéo Aspose.PDF vào)
- Tệp hình ảnh (PNG, JPEG, BMP, TIFF) mà bạn muốn chuyển thành PDF có thể tìm kiếm

Không có thủ thuật cấp phép phức tạp, không có dịch vụ bên ngoài — chỉ cần một tham chiếu NuGet duy nhất và vài phút lập trình.

## Bước 1: Cài đặt gói NuGet Aspose.OCR

Đầu tiên, thêm thư viện vào dự án của bạn. Mở Package Manager Console và chạy:

```powershell
Install-Package Aspose.OCR
```

Lệnh duy nhất này sẽ tải về cả **Aspose.OCR** và assembly **Aspose.Pdf** mà nó phụ thuộc, vì vậy bạn đã sẵn sàng để đọc hình ảnh và ghi PDF.

> **Mẹo chuyên nghiệp:** Nếu bạn đang sử dụng .NET CLI, lệnh tương đương là `dotnet add package Aspose.OCR`.

## Bước 2: Khởi tạo Engine OCR

Tạo một thể hiện của `OcrEngine` là cổng vào cho mọi công việc OCR. Hãy nghĩ nó như bộ não sẽ nhìn vào hình ảnh của bạn và bắt đầu “đọc” các ký tự.

```csharp
using Aspose.OCR;
using Aspose.Pdf;   // pulled in by the OCR package

// Create an OCR engine instance – this object holds configuration and state
var ocrEngine = new OcrEngine();
```

Bạn có thể tự hỏi, *tại sao không chỉ gọi một phương thức tĩnh?* Cách tiếp cận hướng đối tượng cho phép bạn điều chỉnh các cài đặt sau này (ngôn ngữ, độ phân giải, v.v.) mà không cần thay đổi luồng tổng thể.

## Bước 3: Tải hình ảnh bạn muốn chuyển đổi

Đây là nơi chúng ta **chuyển đổi hình ảnh sang PDF** một cách ẩn ý — bằng cách đưa bitmap vào engine OCR. Thay thế `"YOUR_DIRECTORY/input.png"` bằng đường dẫn thực tế tới tệp của bạn.

```csharp
// Load the source image (PNG, JPEG, BMP, or multi‑page TIFF)
ocrEngine.SetImage("YOUR_DIRECTORY/input.png");
```

Nếu bạn có trường hợp **chuyển đổi png sang pdf**, chỉ cần chỉ tới file PNG. Đối với TIFF đa trang, Aspose.OCR sẽ tự động xử lý mỗi khung như một trang riêng.

## Bước 4: Chạy OCR và tùy chọn lấy văn bản

Gọi `Recognize()` thực hiện công việc nặng: nó phân tích hình ảnh, phát hiện ký tự và trả về kết quả có cấu trúc. Bạn có thể giữ lại văn bản để ghi log, lập chỉ mục tìm kiếm, hoặc hiển thị.

```csharp
// Perform OCR – this extracts the textual content from the image
var ocrResult = ocrEngine.Recognize();

// Optional: show the extracted text in the console
Console.WriteLine("Extracted text:");
Console.WriteLine(ocrResult.Text);
```

> **Tại sao phải trích xuất văn bản?** Mặc dù chúng ta sẽ nhúng nó vào PDF cuối cùng, việc có chuỗi thô có thể hữu ích cho việc xác thực hoặc phân tích.

## Bước 5: Cấu hình tùy chọn PDF cho tài liệu có thể tìm kiếm

Aspose.PDF cung cấp cho chúng ta một chế độ đặc biệt `PdfSaveOptions` gọi là **CreateSearchablePdf**. Nó yêu cầu thư viện nhúng văn bản OCR dưới dạng lớp vô hình phía sau hình ảnh, làm cho PDF có thể tìm kiếm.

```csharp
// Prepare PDF save options – this tells Aspose to embed OCR text
var pdfOptions = PdfSaveOptions.CreateSearchablePdf();
```

Nếu bạn cần một PDF chỉ chứa hình ảnh (không có văn bản ẩn), bạn có thể chuyển sang `PdfSaveOptions.CreatePdf()` thay thế. Nhưng với mục tiêu của chúng ta — **tạo PDF có thể tìm kiếm** — chế độ searchable là lựa chọn chính.

## Bước 6: Lưu PDF có thể tìm kiếm vào đĩa

Bây giờ chúng ta gắn mọi thứ lại với nhau. Phương thức `SavePdf` ghi hình ảnh và văn bản ẩn vào một tệp duy nhất.

```csharp
// Save the searchable PDF file
ocrEngine.SavePdf("YOUR_DIRECTORY/output.pdf", pdfOptions);

Console.WriteLine("Searchable PDF created successfully.");
```

Tại thời điểm này, bạn đã có một **PDF có thể tìm kiếm** mà bạn có thể mở trong Adobe Reader, gõ một từ vào ô tìm kiếm và ngay lập tức nhảy tới vị trí phù hợp — mặc dù trang hiển thị vẫn chỉ là hình ảnh gốc.

## Ví dụ Hoạt động Đầy đủ

Kết hợp tất cả các phần lại, đây là một ứng dụng console sẵn sàng chạy. Sao chép‑dán nó vào một dự án C# mới, điều chỉnh đường dẫn tệp, và nhấn **F5**.

```csharp
using System;
using Aspose.OCR;
using Aspose.Pdf; // included automatically with Aspose.OCR

class Program
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // Step 2: Load the image that contains the scanned document
        // Replace with your actual image path
        ocrEngine.SetImage("YOUR_DIRECTORY/input.png");

        // Step 3: Run the OCR process to extract text (optional but useful)
        var ocrResult = ocrEngine.Recognize();

        // Show extracted text – helpful for debugging
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine("======================");

        // Step 4: Prepare to export the recognized content as a searchable PDF
        var pdfOptions = PdfSaveOptions.CreateSearchablePdf();

        // Step 5: Save the searchable PDF to disk
        // Replace with your desired output path
        ocrEngine.SavePdf("YOUR_DIRECTORY/output.pdf", pdfOptions);

        // Step 6: Inform the user that the PDF has been created
        Console.WriteLine("Searchable PDF created successfully.");
    }
}
```

### Kết quả Dự kiến

Khi bạn chạy chương trình, console sẽ hiển thị một cái gì đó như sau:

```
=== Extracted Text ===
Invoice #12345
Date: 2024‑04‑30
Total: $1,250.00
...
======================
Searchable PDF created successfully.
```

Và trong `YOUR_DIRECTORY` bạn sẽ thấy `output.pdf`. Mở nó, nhấn **Ctrl F**, gõ “Invoice”, và bạn sẽ nhảy thẳng tới từ đó — mặc dù trang trông giống như một bản quét phẳng.

## Xử lý Các Biến Thể Thông Thường

### Chuyển đổi Nhiều Hình ảnh Cùng Lúc

Nếu bạn có một thư mục đầy các PNG và muốn một PDF có thể tìm kiếm duy nhất, lặp qua các tệp và thêm mỗi tệp làm một trang riêng:

```csharp
var allImages = Directory.GetFiles("YOUR_DIRECTORY", "*.png");
var ocrEngine = new OcrEngine();
var pdfOptions = PdfSaveOptions.CreateSearchablePdf();

foreach (var imgPath in allImages)
{
    ocrEngine.SetImage(imgPath);
    ocrEngine.Recognize(); // extracts text for the current page
    ocrEngine.SavePdf("temp_page.pdf", pdfOptions);

    // Merge temp_page.pdf into the final document (omitted for brevity)
}
```

Bạn cũng có thể sử dụng `PdfFileEditor` từ Aspose.PDF để hợp nhất các PDF tạm thời thành một tệp cuối cùng.

### Xử lý Các Bản Quét Độ Phân Giải Thấp

Độ chính xác OCR giảm khi DPI của hình ảnh dưới 150. Trước khi đưa hình ảnh vào, bạn có thể tăng độ phân giải:

```csharp
ocrEngine.ImageProcessingOptions.Dpi = 300; // forces 300 DPI for better recognition
```

### Chọn Ngôn Ngữ Cụ Thể

Nếu tài liệu của bạn không phải tiếng Anh, hãy đặt ngôn ngữ trước khi gọi `Recognize()`:

```csharp
ocrEngine.Language = Language.Spanish; // or Language.French, etc.
```

Những điều chỉnh này đảm bảo rằng **trích xuất văn bản từ hình ảnh** hoạt động một cách đáng tin cậy trong các kịch bản khác nhau.

## Kết quả Trực quan

![PDF có thể tìm kiếm được tạo bằng Aspose OCR – tạo PDF có thể tìm kiếm](https://example.com/images/searchable-pdf.png)

*Ảnh chụp màn hình trên cho thấy một PDF mà hình ảnh hiển thị, nhưng lớp văn bản có thể được tìm kiếm.*

## Kết luận

Bây giờ bạn đã có một công thức hoàn chỉnh, sẵn sàng cho môi trường sản xuất để **tạo PDF có thể tìm kiếm** từ bất kỳ hình ảnh nào bằng Aspose OCR và C#. Chúng tôi đã đề cập cách **chuyển đổi hình ảnh sang PDF**, **trích xuất văn bản từ hình ảnh**, và thậm chí chạm tới các trường hợp đặc biệt như **chuyển đổi png sang pdf** và **ocr image to pdf**. Mã nguồn hoàn toàn tự chứa, chạy trên bất kỳ môi trường .NET nào, và có thể mở rộng để xử lý hàng loạt hoặc hỗ trợ ngôn ngữ tùy chỉnh.

Tiếp theo là gì? Hãy thử thêm watermark, mã hoá PDF, hoặc đưa văn bản đã trích xuất vào chỉ mục tìm kiếm như Elasticsearch. Các khả năng là vô tận, và mẫu quy trình giống nhau — tải → nhận dạng → lưu — sẽ phục vụ tốt cho bất kỳ quy trình làm việc nào dựa trên OCR.

Nếu bạn gặp bất kỳ khó khăn nào hoặc có một trường hợp sử dụng thú vị để chia sẻ, hãy để lại bình luận bên dưới. Chúc lập trình vui vẻ, và tận hưởng việc biến những bản quét cứng đầu thành vàng có thể tìm kiếm!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}