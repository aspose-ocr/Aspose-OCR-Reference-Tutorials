---
category: general
date: 2026-04-08
description: Tạo PDF có thể tìm kiếm nhanh chóng và học cách nén hình ảnh PDF, nhúng
  phông chữ vào PDF và nhận dạng văn bản trong hình ảnh bằng C# sử dụng Aspose.OCR.
draft: false
keywords:
- create searchable pdf
- compress pdf images
- embed fonts pdf
- image to searchable pdf
- recognize text image
language: vi
og_description: Tạo PDF có thể tìm kiếm nhanh chóng với Aspose.OCR. Học cách nén hình
  ảnh PDF, nhúng phông chữ vào PDF và nhận dạng văn bản trong hình ảnh trong một hướng
  dẫn duy nhất.
og_title: Tạo PDF có thể tìm kiếm – Hướng dẫn C# toàn diện
tags:
- Aspose.OCR
- C#
- PDF Generation
title: Tạo PDF có thể tìm kiếm – Hướng dẫn C# đầy đủ cho chuyển ảnh sang PDF
url: /vi/net/text-recognition/create-searchable-pdf-complete-c-guide-for-image-to-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo PDF có thể tìm kiếm – Hướng dẫn đầy đủ C#

Cần **tạo PDF có thể tìm kiếm** từ một hình ảnh đã quét? Bạn không phải là người duy nhất đã nhìn chằm chằm vào một tệp PNG khổng lồ và tự hỏi làm thế nào để biến nó thành một tài liệu nhẹ, có thể tìm kiếm bằng văn bản. Tin tốt là với Aspose.OCR bạn có thể làm điều đó chỉ trong vài dòng, và bạn sẽ còn học cách **nén hình ảnh PDF**, **nhúng phông chữ PDF**, và **nhận dạng văn bản trong hình ảnh** mà không gặp khó khăn.

Trong hướng dẫn này, chúng ta sẽ đi qua toàn bộ quy trình: từ việc tải hình ảnh, chạy OCR, điều chỉnh các tùy chọn lưu PDF, cho đến khi cuối cùng ghi một PDF có thể tìm kiếm ra đĩa. Khi kết thúc, bạn sẽ có một phương pháp sẵn sàng sử dụng mà bạn có thể đưa vào bất kỳ dự án .NET nào, cùng với một vài mẹo chuyên nghiệp cho các trường hợp đặc biệt mà bạn có thể gặp sau này.

## Bạn sẽ cần gì

- **.NET 6+** (mã cũng hoạt động trên .NET Framework 4.7, nhưng chúng ta sẽ nhắm tới .NET 6 để dùng cú pháp hiện đại).  
- **Aspose.OCR for .NET** – cài đặt qua NuGet: `Install-Package Aspose.OCR`.  
- Một tệp hình ảnh (PNG, JPEG, TIFF) chứa văn bản bạn muốn làm cho có thể tìm kiếm.  
- Một chút tò mò – phần còn lại sẽ được giải thích bên dưới.

> **Mẹo chuyên nghiệp:** Nếu bạn dự định xử lý hàng chục trang, hãy cân nhắc tái sử dụng một thể hiện `OcrEngine` duy nhất để tránh việc tải lại dữ liệu ngôn ngữ liên tục.

## Bước 1: Cài đặt Engine OCR – Nhận dạng Văn bản trong Hình ảnh

Điều đầu tiên chúng ta cần là một engine OCR có thể đọc các ký tự từ bitmap nguồn. Aspose.OCR cho phép bạn chỉ định ngôn ngữ (English, French, v.v.) và trả về một đối tượng `OcrResult` chứa cả văn bản thô và dữ liệu hình ảnh.

```csharp
using Aspose.Ocr;
using Aspose.Ocr.Pdf;
using System;

public static OcrResult LoadAndRecognize(string imagePath)
{
    // Initialize the OCR engine – “en” is the ISO code for English.
    var ocrEngine = new OcrEngine { Language = "en" };

    // Recognize the image and get the result.
    OcrResult result = ocrEngine.RecognizeImage(imagePath);

    // Quick sanity check – throw if nothing was detected.
    if (string.IsNullOrWhiteSpace(result.Text))
        throw new InvalidOperationException("No text was recognized in the image.");

    return result;
}
```

**Tại sao điều này quan trọng:**  
- Đặt ngôn ngữ giúp cải thiện độ chính xác đáng kể; engine tải các từ điển đặc thù cho ngôn ngữ phía sau.  
- `OcrResult` không chỉ chứa chuỗi đã trích xuất mà còn giữ bitmap gốc, mà chúng ta sẽ nhúng vào PDF để tài liệu vẫn giữ nguyên hình ảnh quét ban đầu.

## Bước 2: Cấu hình tùy chọn lưu PDF – Nén hình ảnh PDF & Nhúng phông chữ

PDF có thể tìm kiếm thực chất là một PDF thông thường với một lớp văn bản ẩn phía trên hình ảnh đã quét. Nếu bạn bỏ qua việc nén, tệp cuối cùng có thể rất lớn. Lớp `PdfSaveOptions` cung cấp kiểm soát chi tiết về chất lượng hình ảnh, nhúng phông chữ, và việc có nên sub‑set phông chữ hay không.

```csharp
public static PdfSaveOptions GetPdfSaveOptions()
{
    return new PdfSaveOptions
    {
        // Reduce file size by compressing the raster image.
        CompressImages = true,

        // ImageQuality ranges from 0 (worst) to 100 (best). 75 is a good balance.
        ImageQuality = 75,

        // Embedding fonts ensures the text layer looks the same on any machine.
        EmbedFonts = true,

        // Subsetting keeps only the glyphs we actually use – another size saver.
        FontSubset = true
    };
}
```

**Tại sao bạn nên nhúng phông chữ vào PDF:**  
Khi một PDF được mở trên hệ thống không có phông chữ chính xác được sử dụng trong lớp OCR, văn bản có thể bị rối. Nhúng phông chữ đảm bảo độ trung thực hình ảnh trên mọi nền tảng, điều này rất quan trọng đối với các tài liệu pháp lý hoặc lưu trữ.

## Bước 3: Lưu Kết quả dưới dạng PDF có thể tìm kiếm – Hình ảnh thành PDF có thể tìm kiếm

Bây giờ chúng ta gắn kết mọi thứ lại: lấy `OcrResult`, áp dụng `PdfSaveOptions` của chúng ta, và ghi tệp. Phương thức `SaveAsSearchablePdf` thực hiện phần việc nặng—tạo một lớp văn bản ẩn phản ánh đầu ra OCR trong khi vẫn giữ nguyên hình ảnh gốc.

```csharp
public static void CreateCompressedSearchablePdf(string inputImage, string outputPdf)
{
    // Step 1: Recognize the image.
    OcrResult ocrResult = LoadAndRecognize(inputImage);

    // Step 2: Prepare PDF options.
    PdfSaveOptions pdfOptions = GetPdfSaveOptions();

    // Step 3: Write the searchable PDF.
    ocrResult.SaveAsSearchablePdf(outputPdf, pdfOptions);

    Console.WriteLine($"Searchable PDF created at: {outputPdf}");
}
```

### Ví dụ Hoạt động đầy đủ

Dưới đây là một chương trình console tự chứa mà bạn có thể sao chép và dán vào một dự án console .NET mới. Nó giả định hình ảnh nằm trong thư mục có tên `YOUR_DIRECTORY` tương đối với tệp thực thi.

```csharp
using Aspose.Ocr;
using Aspose.Ocr.Pdf;
using System;

class Program
{
    static void Main()
    {
        string inputPath = "YOUR_DIRECTORY/input.png";
        string outputPath = "YOUR_DIRECTORY/output.pdf";

        try
        {
            CreateCompressedSearchablePdf(inputPath, outputPath);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error: {ex.Message}");
        }
    }

    // --- Methods from the previous steps -------------------------------------------------
    public static OcrResult LoadAndRecognize(string imagePath)
    {
        var ocrEngine = new OcrEngine { Language = "en" };
        OcrResult result = ocrEngine.RecognizeImage(imagePath);
        if (string.IsNullOrWhiteSpace(result.Text))
            throw new InvalidOperationException("OCR did not detect any text.");
        return result;
    }

    public static PdfSaveOptions GetPdfSaveOptions()
    {
        return new PdfSaveOptions
        {
            CompressImages = true,
            ImageQuality = 75,
            EmbedFonts = true,
            FontSubset = true
        };
    }

    public static void CreateCompressedSearchablePdf(string inputImage, string outputPdf)
    {
        OcrResult ocrResult = LoadAndRecognize(inputImage);
        PdfSaveOptions pdfOptions = GetPdfSaveOptions();
        ocrResult.SaveAsSearchablePdf(outputPdf, pdfOptions);
        Console.WriteLine("Searchable PDF created.");
    }
}
```

Chạy chương trình sẽ tạo ra `output.pdf` mà bạn có thể mở trong Adobe Reader, Foxit, hoặc bất kỳ trình xem PDF nào và ngay lập tức tìm kiếm các từ ban đầu chỉ có trong hình ảnh.

## Bước 4: Xác minh Đầu ra – Tìm kiếm có hoạt động không?

Sau khi tệp được tạo, mở nó và thử tính năng tìm kiếm tích hợp (Ctrl + F). Nếu bạn có thể tìm thấy các từ như “invoice”, “date”, hoặc “total”, bạn đã tạo thành công một **PDF có thể tìm kiếm**.  

Nếu tìm kiếm không trả về kết quả:

1. **Kiểm tra độ chính xác OCR** – có thể hình ảnh nguồn có độ phân giải thấp. Hãy cân nhắc tăng DPI trước OCR (Aspose cho phép bạn đặt `Resolution` trên engine).  
2. **Xác nhận việc nhúng phông chữ** – mở thuộc tính PDF và xem mục *Fonts*; bạn nên thấy phông chữ đã được nhúng liệt kê.  
3. **Kiểm tra nén hình ảnh** – `ImageQuality` quá thấp có thể làm lớp hình ảnh không đọc được, đôi khi gây nhầm lẫn cho các công cụ xử lý tiếp theo.

## Các Biến thể Thông thường & Trường hợp Đặc biệt

| Kịch bản | Cần Điều chỉnh | Lý do |
|----------|----------------|-------|
| **TIFF đa trang** | Lặp qua mỗi khung, gọi `RecognizeImage` cho mỗi trang, sau đó sử dụng `PdfSaveOptions` với `AppendMode = true`. | Giữ mỗi trang quét thành một trang có thể tìm kiếm riêng. |
| **Ngôn ngữ không phải tiếng Anh** | Thay đổi `Language = "fr"` (hoặc mã ISO phù hợp) và tùy chọn cung cấp từ điển tùy chỉnh. | Cải thiện nhận dạng cho các ký tự có dấu và glyph đặc thù của ngôn ngữ. |
| **Hình ảnh rất lớn** | Giảm kích thước bitmap trước OCR (`ocrEngine.Image = Image.FromFile(...).GetThumbnailImage(...)`). | Giảm việc sử dụng bộ nhớ và tăng tốc OCR mà không làm giảm quá nhiều độ chính xác. |
| **Cần độ tin cậy OCR** | Truy cập `ocrResult.RecognizedWords` và kiểm tra thuộc tính `Confidence`. | Cho phép bạn đánh dấu các từ có độ tin cậy thấp để xem xét thủ công. |

## Mẹo về Hiệu suất

- **Tái sử dụng `OcrEngine`** khi xử lý một loạt tệp – nó sẽ cache dữ liệu ngôn ngữ.  
- **Song song hoá** bước nhận dạng với `Parallel.ForEach` nếu bạn đang chạy trên máy đa nhân, nhưng giữ việc ghi PDF tuần tự để tránh xung đột truy cập tệp.  
- **Tinh chỉnh `ImageQuality`**: 85‑90 cho hình ảnh gần như không mất chất, trong khi 60‑70 thường đủ cho các tài liệu chủ yếu là văn bản.

## Kết luận

Chúng ta đã bao quát mọi thứ bạn cần để **tạo PDF có thể tìm kiếm** từ hình ảnh bằng Aspose.OCR, đồng thời học cách **nén hình ảnh PDF**, **nhúng phông chữ PDF**, và hiệu quả **nhận dạng văn bản trong hình ảnh**. Mẫu mã hoàn chỉnh đã sẵn sàng để đưa vào bất kỳ dự án C# nào, và các mẹo bổ sung sẽ giúp bạn điều chỉnh giải pháp cho khối lượng công việc lớn hơn hoặc ngôn ngữ khác.

Sẵn sàng cho bước tiếp theo? Hãy thử thêm watermark, hợp nhất nhiều PDF có thể tìm kiếm, hoặc tích hợp quy trình này vào một web API để người dùng có thể tải lên các bản quét và ngay lập tức nhận được PDF có thể tìm kiếm. Khả năng là vô hạn, và với nền tảng đã có, bạn sẽ dễ dàng mở rộng quy trình làm việc.

Chúc lập trình vui vẻ, và chúc các PDF của bạn luôn nhỏ gọn, có thể tìm kiếm và hiển thị hoàn hảo!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}