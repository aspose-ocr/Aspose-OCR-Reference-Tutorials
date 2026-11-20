---
category: general
date: 2026-06-06
description: Tìm hiểu cách tạo PDF có thể tìm kiếm và chuyển đổi hình ảnh sang PDF
  với OCR. Bao gồm việc thêm lớp, cài đặt nén và toàn bộ mã C#.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- how to ocr image
- how to add layer
- how to set compression
language: vi
og_description: Tạo PDF có thể tìm kiếm từ hình ảnh bằng OCR. Hướng dẫn này chỉ cách
  thêm lớp văn bản ẩn, thiết lập nén và chuyển đổi hình ảnh sang PDF.
og_title: Tạo PDF có thể tìm kiếm – Hướng dẫn C# toàn diện
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Learn how to create searchable PDF and convert image to PDF with OCR.
    Includes layer addition, compression settings, and full C# code.
  headline: Create Searchable PDF from an Image – Full Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to create searchable PDF and convert image to PDF with OCR.
    Includes layer addition, compression settings, and full C# code.
  name: Create Searchable PDF from an Image – Full Step‑by‑Step Guide
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 or later (the code also works on .NET Framework 4.7+). - The
      Aspose.OCR and Aspose.Pdf NuGet packages (or any equivalent library that offers
      `OcrEngine` and `PdfSaveOptions`). - A sample image, e.g., `invoice.png`, placed
      in a folder you can reference. - A basic understanding of C# syntax'
  - name: Full Working Example
    text: 'Putting it all together, here’s the complete, ready‑to‑run program:'
  - name: Pro tip
    text: If you need to **convert image to PDF** without OCR (just a plain image
      PDF), set `AddTextLayer = false`. The same `PdfSaveOptions` still lets you control
      compression, which is handy for archiving scanned documents that don’t need
      searchability.
  type: HowTo
tags:
- OCR
- PDF
- C#
- Aspose
title: Tạo PDF có thể tìm kiếm từ hình ảnh – Hướng dẫn chi tiết từng bước
url: /vi/net/ocr-configuration/create-searchable-pdf-from-an-image-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo PDF có thể tìm kiếm – Hướng dẫn C# đầy đủ

Bạn đã bao giờ tự hỏi làm thế nào để **tạo PDF có thể tìm kiếm** từ một hoá đơn đã quét mà không phải tốn hàng giờ trong một công cụ GUI không? Bạn không phải là người duy nhất. Nhiều nhà phát triển gặp khó khăn khi họ cần chuyển một hình ảnh thành PDF vừa giữ nguyên hình ảnh gốc vừa cho phép người dùng sao chép hoặc tìm kiếm văn bản.  

Trong hướng dẫn này chúng ta sẽ đi qua các bước chính xác để **chuyển đổi hình ảnh sang PDF**, chạy OCR trên nó, thêm một lớp văn bản ẩn, và thậm chí tinh chỉnh các cài đặt nén. Khi kết thúc, bạn sẽ có một đoạn mã C# sẵn sàng sử dụng mà bạn có thể chèn vào bất kỳ dự án .NET nào.

## Những gì bạn sẽ học

- Thiết lập một engine OCR và hiểu **cách OCR hình ảnh**.
- Sử dụng các tùy chọn **cách thêm lớp** để nhúng một lớp văn bản có thể tìm kiếm.
- Áp dụng **cách thiết lập nén** để tạo các PDF nhỏ hơn, nén bằng ZIP.
- Biến một bức ảnh thông thường thành quy trình **tạo PDF có thể tìm kiếm** mà bạn có thể tự động hoá.
- Các lỗi thường gặp và mẹo chuyên nghiệp để giữ PDF của bạn sắc nét và nhanh chóng.

### Yêu cầu trước

- .NET 6.0 hoặc mới hơn (mã cũng hoạt động trên .NET Framework 4.7+).
- Các gói NuGet Aspose.OCR và Aspose.Pdf (hoặc bất kỳ thư viện tương đương nào cung cấp `OcrEngine` và `PdfSaveOptions`).
- Một hình ảnh mẫu, ví dụ `invoice.png`, được đặt trong thư mục bạn có thể tham chiếu.
- Kiến thức cơ bản về cú pháp C# — không cần hiểu sâu về OCR.

> **Mẹo chuyên nghiệp:** Nếu bạn đang dùng Visual Studio, cài đặt các gói qua Package Manager Console:  
> `Install-Package Aspose.OCR`  
> `Install-Package Aspose.Pdf`

---

![Create searchable PDF example showing an invoice image turned into a PDF with hidden text layer](/images/create-searchable-pdf.png)

## Bước 1: Khởi tạo OCR Engine – **how to ocr image**

Đầu tiên chúng ta cần một engine OCR có thể đọc văn bản tiếng Anh từ ảnh của chúng ta. Lớp `OcrEngine` là điểm vào; bạn chỉ cần đặt ngôn ngữ và sau đó cung cấp cho nó một hình ảnh.

```csharp
using Aspose.OCR;
using Aspose.Pdf;

// Create and configure the OCR engine
OcrEngine engine = new OcrEngine
{
    Language = OcrLanguage.English
};
```

*Lý do quan trọng:* Khởi tạo engine với ngôn ngữ đúng sẽ cải thiện độ chính xác đáng kể. Nếu bỏ qua bước này, bạn có thể nhận được các ký tự bị rối.

## Bước 2: Tải ảnh lên – **convert image to pdf**

Bây giờ chúng ta chỉ engine tới tệp mà chúng ta muốn xử lý. `ImageStream.FromFile` đọc các byte và chuẩn bị chúng cho OCR.

```csharp
// Load the image you want to turn into a searchable PDF
engine.Image = ImageStream.FromFile(@"C:\Docs\invoice.png");
```

Bạn cũng có thể tải từ một `MemoryStream` nếu ảnh đến từ yêu cầu web hoặc cơ sở dữ liệu.

## Bước 3: Chạy nhận dạng OCR – **how to ocr image**

Với ảnh đã được tải, công việc nặng sẽ diễn ra trong một lời gọi duy nhất. Phương thức `Recognize` trả về một `OcrResult` chứa cả văn bản đã trích xuất và bitmap gốc.

```csharp
// Perform OCR on the loaded image
OcrResult ocrResult = engine.Recognize();
```

*Phía sau màn hình:* Engine phân tích từng pixel, phát hiện ký tự và xây dựng một chuỗi Unicode. Nó cũng giữ lại dữ liệu vị trí cần thiết cho lớp văn bản ẩn sau này.

## Bước 4: Cấu hình tùy chọn lưu PDF – **how to add layer** & **how to set compression**

Đây là nơi phép màu của PDF có thể tìm kiếm xảy ra. Chúng ta tạo một đối tượng `PdfSaveOptions` để chỉ cho Aspose.Pdf cách nhúng ảnh gốc, thêm lớp văn bản ẩn, và nén tệp cuối cùng.

```csharp
// Set up PDF options for a searchable PDF
PdfSaveOptions pdfOptions = new PdfSaveOptions
{
    IncludeImage = true,          // Keep the original image in the PDF
    AddTextLayer = true,          // Add a hidden text layer with OCR results
    Compression = PdfCompression.Zip   // Use ZIP compression for smaller size
};
```

- **IncludeImage** đảm bảo độ trung thực hình ảnh của bản quét gốc.
- **AddTextLayer** tạo một lớp vô hình mà trình duyệt và trình đọc PDF có thể lập chỉ mục để tìm kiếm.
- **Compression** giảm kích thước tệp mà không làm giảm chất lượng; ZIP là mặc định tốt cho hầu hết tài liệu.

## Bước 5: Lưu kết quả – **create searchable pdf**

Cuối cùng, chúng ta ghi kết quả OCR ra đĩa bằng các tùy chọn vừa định nghĩa. Phương thức `Save` nhận đường dẫn đích và thể hiện `PdfSaveOptions`.

```csharp
// Save the OCR result as a searchable PDF
ocrResult.Save(@"C:\Docs\invoice_searchable.pdf", pdfOptions);
```

Khi bạn mở `invoice_searchable.pdf` trong Adobe Reader hoặc bất kỳ trình xem hiện đại nào, bạn sẽ thấy ảnh gốc, nhưng giờ bạn có thể chọn, sao chép và tìm kiếm văn bản như thể nó là một PDF gốc.

### Ví dụ làm việc đầy đủ

Kết hợp tất cả lại, đây là chương trình hoàn chỉnh, sẵn sàng chạy:

```csharp
using System;
using Aspose.OCR;
using Aspose.Pdf;

namespace SearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine
            OcrEngine engine = new OcrEngine
            {
                Language = OcrLanguage.English
            };

            // 2️⃣ Load the source image
            string imagePath = @"C:\Docs\invoice.png";
            engine.Image = ImageStream.FromFile(imagePath);

            // 3️⃣ Perform OCR
            OcrResult result = engine.Recognize();

            // 4️⃣ Configure PDF options (layer + compression)
            PdfSaveOptions pdfOptions = new PdfSaveOptions
            {
                IncludeImage = true,
                AddTextLayer = true,
                Compression = PdfCompression.Zip
            };

            // 5️⃣ Save as searchable PDF
            string pdfPath = @"C:\Docs\invoice_searchable.pdf";
            result.Save(pdfPath, pdfOptions);

            Console.WriteLine($"Searchable PDF created at: {pdfPath}");
        }
    }
}
```

**Kết quả mong đợi** (trong console):  
`Searchable PDF created at: C:\Docs\invoice_searchable.pdf`

Mở tệp kết quả, nhấn **Ctrl F**, gõ một từ bạn thấy trong hoá đơn, và xem trình xem ngay lập tức nhảy tới vị trí đó. Đó là cốt lõi của **create searchable pdf** đang hoạt động.

## Các lỗi thường gặp & Cách tránh

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| Text not searchable | `AddTextLayer` left `false` or using an older Aspose version | Ensure `AddTextLayer = true` and update to the latest NuGet package |
| PDF huge (megabytes) | Compression set to `PdfCompression.None` | Switch to `PdfCompression.Zip` or `PdfCompression.Jpeg` for images |
| Garbled characters | Wrong language or low‑resolution image | Set `engine.Language` appropriately and supply at least 300 dpi images |
| Hidden layer invisible in some viewers | PDF generated with a non‑standard PDF version | Use `PdfSaveOptions.PdfVersion = PdfVersion.PDF_1_7` (default) or upgrade viewer |

### Mẹo chuyên nghiệp

Nếu bạn cần **chuyển đổi hình ảnh sang PDF** mà không dùng OCR (chỉ PDF ảnh thuần), đặt `AddTextLayer = false`. `PdfSaveOptions` vẫn cho phép bạn kiểm soát nén, rất hữu ích cho việc lưu trữ tài liệu quét không cần khả năng tìm kiếm.

## Mở rộng giải pháp

- **Multiple pages**: Loop over a list of image files, call `engine.Image = ...` each time, and accumulate results into a single PDF using `PdfDocument` aggregation.
- **Different languages**: Change `engine.Language = OcrLanguage.Spanish` (or any supported language) to handle multilingual invoices.
- **Custom compression**: For color‑rich images, `PdfCompression.Jpeg` with a quality setting (`pdfOptions.JpegQuality = 80`) can shrink files further.

## Kết luận

Chúng ta vừa bao quát mọi thứ bạn cần để **tạo PDF có thể tìm kiếm** từ hình ảnh bằng C#. Từ việc khởi tạo engine OCR, tải ảnh, thực hiện nhận dạng, cấu hình lớp văn bản ẩn, đến thiết lập nén — mỗi phần đều đóng vai trò quan trọng trong việc cung cấp một tài liệu nhanh, có thể tìm kiếm.  

Bây giờ bạn có thể tự động hoá xử lý hoá đơn, lưu trữ hợp đồng, hoặc xây dựng công cụ quét hàng loạt biến đống giấy thành PDF có thể tìm kiếm ngay lập tức.  

Sẵn sàng cho thử thách tiếp theo? Hãy thử thêm watermark, hợp nhất nhiều PDF có thể tìm kiếm, hoặc mở rộng logic này qua một Web API để toàn bộ tổ chức của bạn có thể tải lên ảnh và nhận PDF có thể tìm kiếm ngay lập tức.

---

*Nếu bạn thấy hướng dẫn này hữu ích, hãy cho nó một ⭐, chia sẻ với đồng nghiệp, hoặc để lại bình luận với các cải tiến của bạn. Chúc lập trình vui vẻ!*

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã được trình bày trong bài viết này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [How to OCR Image – Perform OCR on Image in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}