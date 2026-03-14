---
category: general
date: 2026-03-13
description: Tạo PDF có thể tìm kiếm từ bất kỳ hình ảnh nào bằng Aspose OCR. Tìm hiểu
  cách chuyển đổi hình ảnh sang EPUB, thêm văn bản có thể tìm kiếm và tạo PDF có thể
  tìm kiếm bằng C#.
draft: false
keywords:
- create searchable pdf
- convert image to epub
- ocr image to pdf
- add searchable text
- generate searchable pdf
language: vi
og_description: Tạo PDF có thể tìm kiếm từ bất kỳ hình ảnh nào bằng Aspose OCR. Hướng
  dẫn này chỉ cách chuyển đổi hình ảnh sang EPUB, thêm văn bản có thể tìm kiếm và
  tạo PDF có thể tìm kiếm trong C#.
og_title: Tạo PDF có thể tìm kiếm – Chuyển đổi hình ảnh sang EPUB & Thêm văn bản
tags:
- Aspose OCR
- C#
- PDF
- EPUB
title: Tạo PDF có thể tìm kiếm – Chuyển hình ảnh sang EPUB & Thêm văn bản
url: /vi/net/text-recognition/create-searchable-pdf-convert-image-to-epub-add-text/
---

final output.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo PDF có thể tìm kiếm – Chuyển đổi hình ảnh sang EPUB & Thêm Văn bản

Bạn muốn **tạo PDF có thể tìm kiếm** từ một biên lai đã quét hoặc bất kỳ hình ảnh nào? Trong hướng dẫn này chúng tôi sẽ chỉ cho bạn cách tạo PDF có thể tìm kiếm bằng Aspose OCR đồng thời **chuyển đổi hình ảnh sang EPUB** và **thêm lớp văn bản có thể tìm kiếm**—tất cả trong một dự án C# duy nhất.  

Nếu bạn từng gặp phải các tệp PDF trông đẹp mắt nhưng không thể tìm kiếm, bạn không phải là người duy nhất. Tin tốt là một lớp văn bản ẩn có thể biến một hình ảnh phẳng thành tài liệu có thể tìm kiếm hoàn toàn, và Aspose làm cho quá trình này gần như không đau đầu.

## Những gì bạn sẽ học

* Cách khởi tạo engine Aspose OCR và đặt ngôn ngữ.  
* Các bước chính để **chuyển đổi hình ảnh sang EPUB** cho việc phân phối e‑book.  
* Cách cấu hình trình ghi PDF sao cho đầu ra chứa một lớp văn bản ẩn, có thể tìm kiếm.  
* Mẹo xử lý các trường hợp đặc biệt như biên lai đa trang hoặc ngôn ngữ không phải tiếng Anh.  

Tất cả những gì bạn cần trước là môi trường phát triển .NET (Visual Studio 2022 trở lên) và gói NuGet Aspose OCR. Không cần dịch vụ bên ngoài, không cần các tệp cấu hình phức tạp—chỉ cần đoạn C# đơn giản mà bạn có thể sao chép‑dán và chạy.

## Yêu cầu trước

| Yêu cầu | Lý do quan trọng |
|-------------|----------------|
| .NET 6.0+   | Aspose OCR nhắm tới .NET Standard 2.0+, vì vậy .NET 6 mang lại các cải tiến runtime mới nhất. |
| Aspose.OCR NuGet package | Cung cấp các lớp `OcrEngine`, `EpubWriter` và `PdfWriter` được sử dụng trong mã. |
| Một tệp hình ảnh (ví dụ, `receipt.jpg`) | Nguồn dữ liệu mà bạn sẽ chạy OCR. Bất kỳ hình ảnh raster nào (PNG, JPEG, BMP) đều hoạt động. |
| Kiến thức cơ bản về C# | Bạn sẽ đọc và chỉnh sửa các đoạn mã mẫu, không phải học ngôn ngữ từ đầu. |

Bạn có thể cài đặt gói bằng lệnh sau:

```bash
dotnet add package Aspose.OCR
```

> **Mẹo chuyên nghiệp:** Nếu bạn đang dùng Visual Studio, UI của NuGet Package Manager cũng thực hiện cùng một công việc—chỉ cần tìm “Aspose.OCR”.

## Bước 1 – Tạo PDF có thể tìm kiếm với Aspose OCR

Điều đầu tiên chúng ta cần là một thể hiện `OcrEngine` biết ngôn ngữ nào sẽ được nhận dạng. Tiếng Anh là mặc định, nhưng bạn có thể thay đổi sang tiếng Pháp, tiếng Đức, v.v., bằng cách đặt `ocrEngine.Language`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;

// Initialise the OCR engine and set the language
OcrEngine ocrEngine = new OcrEngine
{
    Language = Language.English          // Change this if your document isn’t English
};
```

Tại sao phải khởi tạo engine trước? Engine giữ mô hình nhận dạng trong bộ nhớ, vì vậy tạo một lần và tái sử dụng cho nhiều hình ảnh sẽ tiết kiệm cả CPU và RAM. Trong các công việc batch lớn, bạn sẽ giữ cùng một thể hiện sống suốt quá trình chạy.

## Bước 2 – Tải hình ảnh và thực hiện OCR

Tiếp theo chúng ta chỉ định engine tới tệp cần xử lý. `ImageStream.FromFile` đọc hình ảnh vào định dạng mà engine OCR hiểu được.

```csharp
// Load the image you want to process
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.jpg");

// Run the recognition engine – this populates the internal text buffer
ocrEngine.Recognize();
```

> **Nếu hình ảnh là đa trang thì sao?**  
> Aspose OCR có thể xử lý các tệp TIFF đa trang ngay từ đầu. Chỉ cần truyền đường dẫn tới tệp TIFF; engine sẽ tự động lặp qua từng trang.

## Bước 3 – Chuyển đổi hình ảnh sang EPUB

Nếu bạn cũng cần một phiên bản e‑book của tài liệu đã quét, Aspose chỉ cần một dòng lệnh. `EpubWriter` sử dụng cùng một thể hiện `OcrEngine`, nghĩa là kết quả OCR được tái sử dụng mà không cần xử lý thêm.

```csharp
// Export the recognised content to an ePub file
EpubWriter epubWriter = new EpubWriter();
epubWriter.Save(ocrEngine, "YOUR_DIRECTORY/receipt.epub");
```

Tại sao xuất ra EPUB? EPUB là định dạng có thể tái bố cục—lý tưởng cho các thiết bị di động. Văn bản OCR trở nên có thể chọn được, trong khi hình ảnh gốc vẫn được giữ làm nền, bảo toàn giao diện của bản quét gốc.

## Bước 4 – Thêm lớp văn bản có thể tìm kiếm vào PDF

Bây giờ là phần thực sự **tạo PDF có thể tìm kiếm**. Bằng cách bật `AddSearchableTextLayer`, trình ghi PDF sẽ nhúng một lớp văn bản vô hình phản ánh đầu ra OCR. Người dùng có thể tìm kiếm, sao chép hoặc đánh dấu văn bản như trong một PDF gốc.

```csharp
// Configure PDF writer to include a hidden searchable text layer
PdfWriter pdfWriter = new PdfWriter
{
    AddSearchableTextLayer = true   // Enables the hidden text layer for searchability
};

// Save the OCR result as a searchable PDF
pdfWriter.Save(ocrEngine, "YOUR_DIRECTORY/receipt_searchable.pdf");
```

> **Cạm bẫy thường gặp:** Quên bật `AddSearchableTextLayer` sẽ tạo ra một PDF trông giống hệt nhưng không chứa văn bản có thể tìm kiếm. Luôn kiểm tra lại cờ này khi bạn cần tài liệu có khả năng tìm kiếm.

## Bước 5 – Ví dụ hoàn chỉnh hoạt động

Kết hợp tất cả lại, dưới đây là một ứng dụng console tự chứa mà bạn có thể đưa vào dự án .NET mới và chạy ngay lập tức.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace OcrToPdfAndEpub
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialise OCR engine
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.English
            };

            // 2️⃣ Load the source image
            string imagePath = "YOUR_DIRECTORY/receipt.jpg";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 3️⃣ Perform OCR
            ocrEngine.Recognize();

            // 4️⃣ Convert to EPUB (optional but handy)
            EpubWriter epubWriter = new EpubWriter();
            string epubPath = "YOUR_DIRECTORY/receipt.epub";
            epubWriter.Save(ocrEngine, epubPath);
            Console.WriteLine($"EPUB saved to {epubPath}");

            // 5️⃣ Create searchable PDF
            PdfWriter pdfWriter = new PdfWriter
            {
                AddSearchableTextLayer = true
            };
            string pdfPath = "YOUR_DIRECTORY/receipt_searchable.pdf";
            pdfWriter.Save(ocrEngine, pdfPath);
            Console.WriteLine($"Searchable PDF saved to {pdfPath}");
        }
    }
}
```

### Đầu ra mong đợi

* `receipt.epub` – một tệp EPUB mà bạn có thể mở bằng Calibre, Apple Books hoặc bất kỳ thiết bị đọc e‑book nào.  
* `receipt_searchable.pdf` – một PDF mà bạn có thể nhấn **Ctrl + F** và tìm bất kỳ từ nào xuất hiện trong hình ảnh gốc.

Nếu bạn mở PDF trong Adobe Acrobat và xem **File → Properties → Description**, bạn sẽ thấy một luồng văn bản ẩn dưới tab **Fonts**, xác nhận rằng lớp văn bản có thể tìm kiếm đã có mặt.

## Câu hỏi thường gặp & Trường hợp đặc biệt

**Q: Điều này có hoạt động với các ngôn ngữ không phải tiếng Anh không?**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}