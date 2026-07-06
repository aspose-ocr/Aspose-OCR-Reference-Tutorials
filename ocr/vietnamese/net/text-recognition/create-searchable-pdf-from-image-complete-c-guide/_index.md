---
category: general
date: 2026-03-23
description: Tạo PDF có thể tìm kiếm từ hình ảnh bằng Aspose OCR. Tìm hiểu cách chuyển
  đổi TIFF sang PDF với độ nén cao và nhận dạng văn bản trong hình ảnh chỉ trong vài
  phút.
draft: false
keywords:
- create searchable pdf
- convert tiff to pdf
- high compression pdf
- recognize image text
- searchable pdf from image
language: vi
og_description: Tạo PDF có thể tìm kiếm từ hình ảnh bằng Aspose OCR. Hướng dẫn này
  cho thấy cách chuyển TIFF sang PDF, thêm lớp văn bản có thể tìm kiếm và áp dụng
  nén cao.
og_title: Tạo PDF có thể tìm kiếm từ hình ảnh – Hướng dẫn C# đầy đủ
tags:
- Aspose OCR
- C#
- PDF generation
title: Tạo PDF có thể tìm kiếm từ hình ảnh – Hướng dẫn C# đầy đủ
url: /vi/net/text-recognition/create-searchable-pdf-from-image-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo PDF có thể tìm kiếm từ hình ảnh – Hướng dẫn đầy đủ C#  

Bạn đã bao giờ cần **create searchable pdf** từ một tài liệu đã quét nhưng không biết bắt đầu từ đâu chưa? Bạn không phải là người duy nhất—nhiều nhà phát triển gặp cùng một khó khăn khi chuyển các bản quét TIFF thành PDF có thể tìm kiếm. Tin tốt? Với Aspose OCR bạn có thể **convert tiff to pdf**, thêm một lớp văn bản ẩn lên trên, và thậm chí giảm kích thước tệp bằng các tùy chọn **high compression pdf**, tất cả chỉ trong vài dòng C#.

Trong tutorial này chúng ta sẽ đi qua toàn bộ quy trình: cài đặt các gói NuGet phù hợp, tải ảnh TIFF, nhận dạng văn bản, và cuối cùng xuất ra PDF có thể tìm kiếm. Khi hoàn thành, bạn sẽ có một ứng dụng console có thể chạy được mà **recognize image text** và tạo ra một PDF gọn nhẹ, có thể tìm kiếm, sẵn sàng cho việc lập chỉ mục. Không cần công cụ bổ sung, không cần các bước OCR thủ công—chỉ cần code sạch và một chút giải thích.

## Yêu cầu trước & Những gì bạn cần  

- **.NET 6+** (hoặc .NET Framework 4.6+). API hoạt động trên cả hai, nhưng .NET 6 mang lại các cải tiến runtime mới nhất.  
- **Visual Studio 2022** hoặc bất kỳ IDE nào bạn thích.  
- Các gói NuGet **Aspose.OCR** và **Aspose.OCR.Gpu** (gói GPU là tùy chọn nhưng giúp tăng tốc nhận dạng trên phần cứng hỗ trợ).  
- Một file TIFF mẫu (ví dụ: `invoice.tif`) được đặt trong thư mục bạn kiểm soát.  

Nếu bạn đã có những mục này, tuyệt—bỏ qua bước tiếp theo. Nếu chưa, bước cài đặt dưới đây sẽ bao gồm mọi thứ.

## Bước 1: Cài đặt các gói Aspose OCR  

Đầu tiên, mở thư mục dự án của bạn trong terminal và chạy:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Gpu
```

Các lệnh này sẽ kéo cả engine OCR lõi và thư viện tăng tốc GPU. Thứ hai không bắt buộc; engine sẽ tự chuyển sang chế độ CPU nếu không tìm thấy GPU tương thích.  

> **Pro tip:** Khi triển khai môi trường production, hãy khóa phiên bản gói trong file `csproj` của bạn để tránh các thay đổi gây lỗi không mong muốn.

## Bước 2: Thiết lập khung dự án  

Tạo một ứng dụng console mới (nếu bạn chưa có):

```bash
dotnet new console -n PdfExportDemo
cd PdfExportDemo
```

Thay thế file `Program.cs` được tạo tự động bằng toàn bộ mã sẽ được trình bày sau. Chương trình sẽ:

1. Khởi tạo một `OcrEngine` với hỗ trợ GPU.  
2. Tải ảnh TIFF.  
3. Thực hiện OCR và dừng lại một cách nhẹ nhàng nếu gặp lỗi.  
4. Cấu hình **PdfExportOptions** để tạo lớp có thể tìm kiếm và **high compression**.  
5. Ghi file đầu ra.

## Bước 3: Viết toàn bộ mã (Ví dụ đầy đủ)  

Dưới đây là *toàn bộ* file nguồn. Sao chép‑dán vào `Program.cs`. Các chú thích giải thích “tại sao” mỗi dòng, không chỉ “cái gì”.

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;
using System;

class PdfExport
{
    static void Main()
    {
        // ------------------------------------------------------------
        // 1️⃣ Initialise OCR engine with GPU acceleration.
        //    GpuMode.Enabled tells Aspose to use the GPU if one is present.
        //    If no compatible GPU exists, the engine automatically falls back
        //    to CPU mode—no extra code required.
        // ------------------------------------------------------------
        using (OcrEngine ocrEngine = new OcrEngine(GpuMode.Enabled))
        {
            // ------------------------------------------------------------
            // 2️⃣ Load the source image.
            //    ImageStream.FromFile supports many formats; here we use TIFF.
            // ------------------------------------------------------------
            string inputPath = @"YOUR_DIRECTORY\invoice.tif";
            ocrEngine.Image = ImageStream.FromFile(inputPath);

            // ------------------------------------------------------------
            // 3️⃣ Perform OCR recognition.
            //    Recognize() returns false if the engine cannot read the image.
            //    Exiting early prevents us from creating an empty PDF.
            // ------------------------------------------------------------
            if (!ocrEngine.Recognize())
            {
                Console.WriteLine("OCR failed – check the image path and format.");
                return;
            }

            // ------------------------------------------------------------
            // 4️⃣ Configure PDF export options.
            //    IncludeTextLayer = true adds an invisible, searchable text layer.
            //    CompressionLevel = High reduces file size dramatically.
            // ------------------------------------------------------------
            PdfExportOptions pdfExportOptions = new PdfExportOptions
            {
                IncludeTextLayer = true,
                CompressionLevel = PdfCompression.High
            };

            // ------------------------------------------------------------
            // 5️⃣ Save the searchable PDF.
            //    The output will be a compact, searchable PDF ready for indexing.
            // ------------------------------------------------------------
            string outputPath = @"YOUR_DIRECTORY\invoice.pdf";
            ocrEngine.Save(outputPath, pdfExportOptions);
            Console.WriteLine($"Searchable PDF saved to: {outputPath}");
        }
    }
}
```

### Tại sao cách này hoạt động  

- **GPU acceleration** có thể rút ngắn thời gian nhận dạng từ vài giây xuống mili giây trên các card hiện đại—rất hữu ích cho việc xử lý hàng loạt.  
- **IncludeTextLayer** nhúng văn bản được OCR tạo ra một cách ẩn, cho phép các trình xem PDF tìm kiếm tài liệu mà không làm thay đổi giao diện hình ảnh.  
- **High compression** sử dụng nén Flate (ZIP) cho luồng ảnh, mất không dữ liệu nhưng giảm đáng kể kích thước file—lý tưởng cho việc lưu trữ hàng ngàn hoá đơn.

## Bước 4: Chạy ứng dụng và kiểm tra kết quả  

Mở terminal trong thư mục dự án và thực thi:

```bash
dotnet run
```

Nếu mọi thứ được cấu hình đúng, bạn sẽ thấy:

```
Searchable PDF saved to: YOUR_DIRECTORY\invoice.pdf
```

Mở `invoice.pdf` bằng bất kỳ trình đọc PDF nào (Adobe Acrobat, Edge, hoặc thậm chí trình duyệt). Thử tìm kiếm một từ mà bạn biết có trong TIFF gốc—ví dụ “Total”. Trình xem sẽ đánh dấu từ đó mặc dù nó nằm trong hình ảnh. Đó là dấu hiệu của một **searchable pdf**.

### Kích thước file dự kiến  

Một hoá đơn quét thường (≈300 KB TIFF) thường giảm xuống **~80 KB** sau khi áp dụng `PdfCompression.High`. Kích thước thực tế phụ thuộc vào độ phức tạp của ảnh, nhưng bạn sẽ thấy sự giảm đáng kể.

## Bước 5: Các biến thể thường gặp & Trường hợp góc cạnh  

| Situation | What to Adjust | Why |
|-----------|----------------|-----|
| **No GPU available** | Change `new OcrEngine(GpuMode.Enabled)` to `new OcrEngine(GpuMode.Disabled)` | Prevents the engine from attempting GPU initialization, which can cause a brief delay. |
| **Multiple pages (multi‑page TIFF)** | Set `ocrEngine.Image = ImageStream.FromFile("multi.tif", PageRange.All);` | Loads all frames; Aspose will process each page and generate a multi‑page PDF. |
| **Need OCR language other than English** | `ocrEngine.Language = Language.French;` (or any supported language) | Improves accuracy for non‑English documents. |
| **Want a visible text overlay instead of hidden layer** | `pdfExportOptions.IncludeTextLayer = false;` and manually add `TextFragment` objects. | Useful when you want the OCR text to appear as selectable text on top of the image. |
| **Ultra‑small PDFs** | Combine `PdfCompression.High` with `ImageResolution = 150` DPI before recognition. | Lower DPI reduces image data, further shrinking the PDF at the cost of visual fidelity. |

> **Note:** Always test edge cases on a small sample before scaling to production. OCR accuracy can vary with image quality, noise, and language.

## Bước 6: Mẹo cho triển khai Production‑Ready  

1. **Error Logging** – Thay thế `Console.WriteLine` bằng một framework logging thích hợp (Serilog, NLog) để dễ dàng chẩn đoán.  
2. **Batch Processing** – Đóng gói logic cốt lõi trong một phương thức nhận đường dẫn đầu vào/đầu ra, sau đó lặp qua một thư mục chứa các file TIFF.  
3. **Async I/O** – Mặc dù Aspose OCR tự nó đồng bộ, việc tải và lưu file có thể thực hiện bất đồng bộ để giữ cho các luồng UI phản hồi nhanh.  
4. **Security** – Nếu bạn cung cấp chức năng này qua API web, hãy xác thực đường dẫn file và giới hạn kích thước file để tránh lạm dụng.  
5. **Version Pinning** – Sử dụng số phiên bản chính xác (`<PackageReference Include="Aspose.OCR" Version="23.12.0" />`) để đảm bảo hành vi nhất quán giữa các lần build.

## Kết luận  

Chúng ta vừa xây dựng một **complete, end‑to‑end solution** giúp **create searchable pdf** từ hình ảnh đã quét, **convert tiff to pdf**, và thực hiện các thiết lập **high compression pdf** đồng thời **recognize image text** một cách chính xác. PDF **searchable pdf from image** kết quả nhẹ, có thể tìm kiếm, và sẵn sàng cho các quy trình downstream như lập chỉ mục, lưu trữ, hoặc e‑discovery.

Có một loạt hoá đơn? Đưa phương thức vào vòng lặp, chỉ định thư mục, và để Aspose OCR lo phần còn lại. Muốn thử nghiệm các mức nén khác hoặc gói ngôn ngữ? Mã nguồn được thiết kế mô-đun đủ để thay đổi các tùy chọn trong vài giây.

---

*Bạn đã sẵn sàng nâng cấp?* Hãy thử thêm watermark, nhúng metadata, hoặc thậm chí ghép nhiều PDF đã qua OCR lại với nhau. Bộ công cụ Aspose cung cấp rất nhiều phần mở rộng—khám phá tài liệu và tiếp tục tiến bước. Chúc bạn lập trình vui vẻ!

![Create searchable PDF from image example screenshot](https://example.com/images/create-searchable-pdf.png "create searchable pdf example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}