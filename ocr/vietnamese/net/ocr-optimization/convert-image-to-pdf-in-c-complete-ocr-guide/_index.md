---
category: general
date: 2026-09-13
description: Tìm hiểu cách chuyển trang quét sang PDF trong C# bằng Aspose OCR. Hướng
  dẫn này trình bày việc tiền xử lý, nhận dạng văn bản tiếng Hàn và tạo PDF có thể
  tìm kiếm.
keywords:
- scanned page to pdf
- preprocess image for OCR
- generate pdf with text
- convert image to searchable pdf
- gpu accelerated OCR
- recognize Korean text image
lastmod: 2026-09-13
og_description: Tìm hiểu cách chuyển trang quét sang PDF trong C# với Aspose OCR.
  Bài hướng dẫn bao gồm tiền xử lý hình ảnh, OCR GPU‑accelerated cho văn bản tiếng
  Hàn và tạo PDF có thể tìm kiếm trong vài phút.
og_image_alt: Screenshot of C# console app converting a scanned Korean page to searchable
  PDF using Aspose OCR
og_title: Cách chuyển trang quét sang PDF trong C# với OCR
schemas:
- author: Aspose
  dateModified: '2026-09-13'
  description: Learn how to turn a scanned page to PDF in C# using Aspose OCR. This
    guide shows preprocessing, Korean text recognition, and creating a searchable
    PDF.
  headline: How to turn a scanned page to PDF in C# with OCR
  type: TechArticle
- description: Learn how to turn a scanned page to PDF in C# using Aspose OCR. This
    guide shows preprocessing, Korean text recognition, and creating a searchable
    PDF.
  name: How to turn a scanned page to PDF in C# with OCR
  steps:
  - name: Initialise the OCR engine with GPU support.
    text: Initialise the OCR engine with GPU support.
  - name: Add **preprocess image for OCR** filters such as deskew and denoise.
    text: Add **preprocess image for OCR** filters such as deskew and denoise.
  - name: Download and load the Korean language model (handled automatically).
    text: Download and load the Korean language model (handled automatically).
  - name: Run the OCR on the image.
    text: Run the OCR on the image.
  - name: Export the result with **SearchablePdfExporter** to **create searchable
      PDF image**.
    text: Export the result with **SearchablePdfExporter** to **create searchable
      PDF image**.
  - name: (Optional) Serialize the OCR output to JSON for downstream pipelines.
    text: (Optional) Serialize the OCR output to JSON for downstream pipelines.
  - name: '**Ensure the language model is fully downloaded** – check the console for
      a message like “Downloading Korean model…”.'
    text: '**Ensure the language model is fully downloaded** – check the console for
      a message like “Downloading Korean model…”.'
  - name: '**Increase the `MaxAngle`** in `DeskewFilter` if your scans are rotated
      beyond 12°.'
    text: '**Increase the `MaxAngle`** in `DeskewFilter` if your scans are rotated
      beyond 12°.'
  - name: '**Boost GPU memory** by setting `ocrEngine.GpuMemoryLimit = 2048;` (value
      in MB).'
    text: '**Boost GPU memory** by setting `ocrEngine.GpuMemoryLimit = 2048;` (value
      in MB).'
  type: HowTo
- questions:
  - answer: 'The exporter embeds the original bitmap at its native resolution. If
      size is a concern, downscale the image *before* recognition:'
    question: My PDF is huge compared to the original image.
  - answer: Verify that the image path is correct and that the file is not corrupted.
      Also, make sure the GPU driver is up‑to‑date; older drivers can cause silent
      failures.
    question: The OCR returns empty strings.
  - answer: Absolutely. Wrap steps 4‑6 in a `foreach (var file in Directory.GetFiles("Resources",
      "*.jpg"))` loop and change the output PDF path accordingly.
    question: Can I process multiple pages in a loop?
  type: FAQPage
tags:
- scanned page to pdf
- OCR
- Aspose
- C#
title: Cách chuyển trang quét sang PDF trong C# với OCR
url: /vi/net/ocr-optimization/convert-image-to-pdf-in-c-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách chuyển trang quét thành PDF trong C# với OCR

Nếu bạn cần **chuyển một trang quét thành PDF** trong khi giữ cho văn bản có thể tìm kiếm, bạn đã đến đúng nơi. Hướng dẫn này sẽ chỉ cho bạn cách sử dụng Aspose OCR để **tiền xử lý hình ảnh cho OCR**, **nhận dạng hình ảnh văn bản Hàn Quốc**, và cuối cùng **tạo ảnh PDF có thể tìm kiếm** – tất cả từ một ứng dụng console C# đơn giản.

## Câu trả lời nhanh
- **Thư viện nào xử lý OCR?** Aspose.OCR for .NET  
- **Tôi có thể sử dụng GPU không?** Yes – enable GPU acceleration for up to 2× faster processing  
- **Tôi có cần gói ngôn ngữ Hàn Quốc không?** It downloads automatically on first use  
- **Kết quả có thể tìm kiếm được không?** The generated PDF contains an invisible text layer  
- **Các phiên bản .NET nào được hỗ trợ?** .NET 6.0 and later (including .NET Core and .NET Framework)

## Yêu cầu

- **.NET 6.0 hoặc mới hơn** – works on .NET Core, .NET Framework, and .NET 5/6+  
- **Aspose.OCR for .NET** gói NuGet (`Aspose.OCR`) – trial keys are free on the Aspose site  
- Một hình mẫu có ký tự Hàn Quốc, ví dụ `korean_book_page.jpg`  
- IDE yêu thích của bạn (Visual Studio 2022, VS Code, Rider, v.v.)

> **Mẹo chuyên nghiệp:** Lưu trữ hình ảnh trong thư mục `Resources/` để đường dẫn luôn nhất quán trên các máy.

## Tổng quan quy trình

1. Khởi tạo engine OCR với hỗ trợ GPU.  
2. Thêm các bộ lọc **preprocess image for OCR** như deskew và denoise.  
3. Tải xuống và tải mô hình ngôn ngữ Hàn Quốc (được xử lý tự động).  
4. Chạy OCR trên hình ảnh.  
5. Xuất kết quả bằng **SearchablePdfExporter** để **create searchable PDF image**.  
6. (Tùy chọn) Serialize đầu ra OCR thành JSON cho các pipeline downstream.

Dưới đây chúng tôi sẽ mở rộng từng bước, giải thích *tại sao* nó quan trọng, và cung cấp cho bạn đoạn mã chính xác để copy‑paste.

## Quá trình chuyển trang quét thành PDF hoạt động như thế nào?

`OcrEngine` là lớp chính trong Aspose.OCR thực hiện nhận dạng ký tự quang học trên hình ảnh.  
`SearchablePdfExporter` tạo một PDF chứa hình ảnh gốc và một lớp văn bản vô hình để tìm kiếm.  
`RecognitionResult` chứa văn bản và dữ liệu độ tin cậy do engine OCR trả về.

Tải hình ảnh của bạn bằng `new OcrEngine()` và gọi `engine.Recognize("korean_book_page.jpg")`, sau đó truyền `RecognitionResult` cho `SearchablePdfExporter.Export`. Quy trình hai bước này đọc bitmap, trích xuất văn bản Unicode, và nhúng cả hai vào một PDF duy nhất trong đó lớp văn bản là vô hình nhưng có thể tìm kiếm. Tăng tốc GPU giảm thời gian nhận dạng khoảng một nửa, trong khi các bộ lọc deskew và denoise nâng độ chính xác lên tới 15 % trên các bản quét nhiễu.

## Chuyển hình ảnh sang PDF – quy trình đầy đủ

Đoạn mã dưới đây là chương trình *đầy đủ*. Tạo một dự án console mới (`dotnet new console -n OcrPdfDemo`) và thay thế file `Program.cs` được tạo tự động bằng mã được hiển thị trong placeholder.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;
using Aspose.OCR.Export;
using Aspose.OCR.Result;   // for JsonResult

namespace OcrPdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // Step 1: Initialise the OCR engine (GPU enabled, offline mode off)
            // -----------------------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                UseGpu = true,          // leverages your graphics card for faster inference
                OfflineMode = false    // allows on‑the‑fly language model download
            };

            // --------------------------------------------------------------
            // Step 2: Add preprocessing filters to improve accuracy
            // --------------------------------------------------------------
            // Deskew corrects slight rotations; MaxAngle = 12° is a safe default.
            ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 12 });

            // Denoise removes isolated speckles that often appear in scanned books.
            ocrEngine.Filters.Add(new DenoiseFilter());

            // --------------------------------------------------------------
            // Step 3: Load the Korean language model
            // --------------------------------------------------------------
            // Aspose will download the model the first time you run this on a new machine.
            ocrEngine.LoadLanguage(LanguageModel.Korean);

            // --------------------------------------------------------------
            // Step 4: Recognise text from the input image
            // --------------------------------------------------------------
            // Replace the path with your actual image location.
            string imagePath = "Resources/korean_book_page.jpg";
            var recognitionResult = ocrEngine.Recognize(imagePath);

            // --------------------------------------------------------------
            // Step 5: Export the recognised page as a searchable PDF
            // --------------------------------------------------------------
            string pdfPath = "Resources/korean_page.pdf";
            var exporter = new SearchablePdfExporter { OutputPath = pdfPath };
            exporter.Export(ocrEngine, imagePath);

            // --------------------------------------------------------------
            // Step 6: Obtain a structured JSON representation of the result
            // --------------------------------------------------------------
            string json = JsonResult.FromRecognitionResult(recognitionResult).ToString(true);
            Console.WriteLine("=== OCR JSON Result ===");
            Console.WriteLine(json);

            Console.WriteLine("\n✅ Conversion complete!");
            Console.WriteLine($"PDF saved to: {pdfPath}");
        }
    }
}
```

### Tại sao điều này hoạt động

- **GPU acceleration** giảm thời gian nhận dạng khoảng một nửa so với chế độ chỉ CPU.  
- **Deskew** và **Denoise** là các kỹ thuật *preprocess image for OCR* cổ điển; chúng sửa các khuyết điểm quét thường gặp mà nếu không sẽ khiến engine bỏ sót ký tự.  
- **Language model loading** là cần thiết cho **recognize Korean text image** – nếu không có mô hình Hàn Quốc, engine sẽ quay lại sử dụng bảng chữ cái Latin chung và tạo ra kết quả vô nghĩa.  
- Công cụ **SearchablePdfExporter** kết hợp bitmap gốc và một lớp văn bản vô hình, cung cấp cho bạn kết quả **create searchable pdf image** mà bạn có thể lập chỉ mục trong bất kỳ trình đọc PDF nào.

## Tại sao điều này hoạt động

- **GPU acceleration** giảm thời gian nhận dạng khoảng một nửa so với chế độ chỉ CPU.  
- **Deskew** và **Denoise** là các kỹ thuật *preprocess image for OCR* cổ điển; chúng sửa các khuyết điểm quét thường gặp mà nếu không sẽ khiến engine bỏ sót ký tự.  
- **Language model loading** là cần thiết cho **recognize Korean text image** – nếu không có mô hình Hàn Quốc, engine sẽ quay lại sử dụng bảng chữ cái Latin chung và tạo ra kết quả vô nghĩa.  
- Công cụ **SearchablePdfExporter** kết hợp bitmap gốc và một lớp văn bản vô hình, cung cấp cho bạn kết quả **create searchable pdf image** mà bạn có thể lập chỉ mục trong bất kỳ trình đọc PDF nào.

## Tiền xử lý hình ảnh cho OCR – mẹo & thủ thuật

`DeskewFilter` sửa độ xoay của các trang quét.  
`ContrastFilter` điều chỉnh độ tương phản ảnh để cải thiện độ chính xác OCR.  
`BinarizationFilter` chuyển ảnh sang đen‑trắng dựa trên ngưỡng, giảm nhiễu nền.  
`OrientationFilter` phát hiện và sửa các trang có hướng hỗn hợp (portrait/landscape).

| Vấn đề | Bộ lọc bổ sung | Cách thêm |
|-------|-------------------|------------|
| Độ tương phản thấp | `ContrastFilter { Level = 30 }` | `ocrEngine.Filters.Add(new ContrastFilter { Level = 30 });` |
| Nhiễu nền mạnh | `BinarizationFilter { Threshold = 128 }` | `ocrEngine.Filters.Add(new BinarizationFilter { Threshold = 128 });` |
| Hướng hỗn hợp (portrait & landscape) | `OrientationFilter()` | `ocrEngine.Filters.Add(new OrientationFilter());` |

> **Lưu ý:** Thêm quá nhiều bộ lọc có thể làm chậm quá trình. Hãy kiểm tra mỗi thay đổi trên một trang duy nhất trước khi mở rộng.

## Nhận dạng hình ảnh văn bản Hàn Quốc – các bẫy thường gặp

Ký tự Hàn Quốc chứa các âm tiết Hangul dày đặc về mặt hình ảnh. Nếu bạn thấy đầu ra bị rối:

1. **Đảm bảo mô hình ngôn ngữ đã được tải xuống đầy đủ** – kiểm tra console để thấy thông báo như “Downloading Korean model…”.  
2. **Tăng `MaxAngle`** trong `DeskewFilter` nếu các bản quét của bạn bị xoay vượt quá 12°.  
3. **Tăng bộ nhớ GPU** bằng cách đặt `ocrEngine.GpuMemoryLimit = 2048;` (giá trị tính bằng MB).  

`LanguageModel.Korean` tải dữ liệu ngôn ngữ Hàn Quốc cho OCR, cho phép nhận dạng Hangul chính xác.  

Những điều chỉnh này ảnh hưởng trực tiếp đến thành công của **recognize Korean text image**.

## Tạo ảnh PDF có thể tìm kiếm – xác minh kết quả

Sau khi chương trình kết thúc, mở `korean_page.pdf` bằng bất kỳ trình đọc PDF nào (Adobe Acrobat Reader, Foxit, thậm chí Chrome). Bạn nên có thể:

- **Chọn văn bản** bằng chuột như thể đó là một PDF gốc.  
- **Tìm kiếm** các từ Hàn bằng hộp tìm kiếm tích hợp.  

Nếu lớp văn bản hiện ra trống, hãy kiểm tra lại rằng phương thức `Export` nhận đúng đường dẫn hình ảnh và kết quả OCR chứa `RecognitionResult.Text` không rỗng.

## Đầu ra JSON đầy đủ – những gì mong đợi

Console in ra payload JSON được định dạng đẹp. Một ví dụ đã cắt ngắn như sau:

```json
{
  "Text": "첫 번째 페이지의 내용...",
  "Blocks": [
    {
      "Text": "첫 번째 페이지의 내용...",
      "BoundingBox": { "X": 12, "Y": 34, "Width": 560, "Height": 780 },
      "Confidence": 0.98
    }
  ],
  "Language": "Korean",
  "ProcessingTimeMs": 842
}
```

## Khắc phục sự cố & Câu hỏi thường gặp

**Q: PDF của tôi quá lớn so với hình ảnh gốc.**  
A: Trình xuất nhúng bitmap gốc ở độ phân giải gốc. Nếu kích thước là vấn đề, hãy giảm kích thước hình ảnh *trước* khi nhận dạng:

```csharp
ocrEngine.Filters.Add(new ResizeFilter { MaxWidth = 1240, MaxHeight = 1754 });
```

**Q: OCR trả về chuỗi rỗng.**  
A: Xác minh rằng đường dẫn hình ảnh đúng và tệp không bị hỏng. Ngoài ra, đảm bảo driver GPU đã được cập nhật; driver cũ có thể gây ra lỗi im lặng.

**Q: Tôi có thể xử lý nhiều trang trong một vòng lặp không?**  
A: Chắc chắn. Bao bọc các bước 4‑6 trong vòng lặp `foreach (var file in Directory.GetFiles("Resources", "*.jpg"))` và thay đổi đường dẫn PDF đầu ra cho phù hợp.

## Kết luận

Chúng ta vừa **chuyển hình ảnh sang PDF** trong khi giữ nguyên văn bản có thể tìm kiếm, nhờ vào pipeline mạnh mẽ của Aspose OCR. Bằng cách **preprocess image for OCR**, bạn tăng độ chính xác; bằng **recognize Korean text image**, bạn xử lý các script phức tạp; và bằng **create searchable pdf image**, bạn có được một tài liệu di động, có thể lập chỉ mục.

Lấy mã nguồn, chỉ vào các bản quét của bạn, và thử nghiệm với các bộ lọc hoặc mô hình ngôn ngữ bổ sung. Mẫu này cũng áp dụng cho tiếng Trung, Nhật, hoặc bất kỳ ngôn ngữ dựa trên Latin nào — chỉ cần thay `LanguageModel.Korean` bằng enum phù hợp.

Có thêm câu hỏi? Để lại bình luận, và chúc bạn lập trình vui!

---

**Cập nhật lần cuối:** 2026-09-13  
**Kiểm tra với:** Aspose.OCR 24.11 for .NET  
**Tác giả:** Aspose

## Hướng dẫn liên quan

- [Tạo PDF có thể tìm kiếm từ tệp quét bằng Aspose Ocr](/ocr/net/ocr-optimization/create-searchable-pdf-from-scanned-files-using-aspose-ocr/)
- [Pipeline tiền xử lý OCR – Cách nhận dạng văn bản từ hình ảnh](/ocr/net/ocr-optimization/ocr-preprocessing-pipeline-how-to-recognize-text-from-image/)
- [Nhận dạng văn bản từ hình ảnh với Aspose Ocr – Hướng dẫn C đầy đủ](/ocr/net/ocr-configuration/recognize-text-from-image-with-aspose-ocr-complete-c-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}