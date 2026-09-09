---
category: general
date: 2025-12-30
description: Chuyển đổi hình ảnh sang PDF bằng Aspose OCR trong C#. Tìm hiểu cách
  tiền xử lý hình ảnh cho OCR, nhận dạng hình ảnh văn bản tiếng Hàn và tạo nhanh PDF
  có thể tìm kiếm.
draft: false
keywords:
- convert image to pdf
- preprocess image for ocr
- recognize korean text image
- create searchable pdf image
language: vi
og_description: Chuyển đổi hình ảnh sang PDF với Aspose OCR. Hướng dẫn này cho thấy
  cách tiền xử lý hình ảnh cho OCR, nhận dạng hình ảnh văn bản tiếng Hàn và tạo PDF
  có thể tìm kiếm từ hình ảnh.
og_title: Chuyển Đổi Hình Ảnh Sang PDF trong C# – Hướng Dẫn OCR Toàn Diện
tags:
- C#
- OCR
- Aspose
- PDF
title: Chuyển Đổi Hình Ảnh Sang PDF trong C# – Hướng Dẫn OCR Toàn Diện
url: /vi/net/ocr-optimization/convert-image-to-pdf-in-c-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Chuyển Đổi Hình Ảnh Sang PDF trong C# – Hướng Dẫn OCR Đầy Đủ

Bạn đã bao giờ cần **convert image to PDF** nhưng cũng muốn văn bản bên trong có thể tìm kiếm không? Bạn không phải là người duy nhất. Nhiều nhà phát triển gặp cùng một khó khăn khi xử lý các trang quét, đặc biệt là những trang viết bằng tiếng Hàn. Tin tốt là với Aspose OCR bạn có thể **preprocess image for OCR**, **recognize Korean text image**, và cuối cùng **create searchable PDF image** chỉ trong vài dòng mã.

Trong hướng dẫn này, chúng tôi sẽ đi qua toàn bộ quy trình — từ việc tải một tệp JPEG thô của một trang sách tiếng Hàn, làm sạch nó, trích xuất văn bản, và đóng gói mọi thứ thành một PDF có thể tìm kiếm. Khi kết thúc, bạn sẽ có một ứng dụng console C# sẵn sàng chạy mà bạn có thể đưa vào bất kỳ dự án .NET nào.

## Những Gì Bạn Cần

- **.NET 6.0 hoặc mới hơn** (code hoạt động trên .NET Core và .NET Framework)  
- **Aspose.OCR for .NET** gói NuGet (`Aspose.OCR`) – khóa dùng thử miễn phí có sẵn trên trang Aspose.  
- Một hình mẫu chứa văn bản tiếng Hàn (ví dụ, `korean_book_page.jpg`).  
- Môi trường phát triển bạn chọn (Visual Studio, VS Code, Rider – tôi đang dùng VS 2022).

> **Mẹo chuyên nghiệp:** Giữ các tệp hình ảnh của bạn trong một thư mục riêng như `Resources/` để đường dẫn luôn nhất quán trên các máy.

## Tổng Quan Quy Trình

1. **Khởi tạo engine OCR** với hỗ trợ GPU để tăng tốc.  
2. **Thêm các bộ lọc tiền xử lý** (deskew, denoise) để cải thiện độ chính xác nhận dạng.  
3. **Tải xuống và tải mô hình ngôn ngữ tiếng Hàn** – Aspose sẽ tự động thực hiện nếu cần.  
4. **Chạy quá trình nhận dạng** trên hình ảnh đầu vào.  
5. **Xuất kết quả dưới dạng PDF có thể tìm kiếm** bằng bộ xuất tích hợp.  
6. **Tùy chọn, tuần tự hoá kết quả thành JSON** để phân tích hoặc ghi log tiếp theo.

Dưới đây chúng tôi sẽ phân tích từng bước, giải thích *tại sao* nó quan trọng, và cung cấp cho bạn đoạn mã chính xác để sao chép‑dán.

---

## ## Chuyển Đổi Hình Ảnh Sang PDF – Quy Trình Đầy Đủ

Đoạn mã sau là chương trình *đầy đủ*. Bạn có thể tạo một dự án console mới (`dotnet new console -n OcrPdfDemo`) và thay thế tệp `Program.cs` được tạo tự động bằng đoạn mã này.

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

### Tại Sao Điều Này Hoạt Động

- **GPU acceleration** giảm thời gian nhận dạng khoảng một nửa so với chế độ chỉ CPU.  
- **Deskew** và **Denoise** là các kỹ thuật *preprocess image for OCR* cổ điển; chúng sửa các khuyết điểm quét thường gặp mà nếu không sẽ khiến engine bỏ sót ký tự.  
- **Language model loading** là cần thiết cho **recognize Korean text image** – nếu không có mô hình tiếng Hàn, engine sẽ quay lại sử dụng bảng chữ cái Latin chung và tạo ra kết quả vô nghĩa.  
- **SearchablePdfExporter** kết hợp bitmap gốc và một lớp văn bản vô hình, cung cấp cho bạn kết quả **create searchable pdf image** mà bạn có thể lập chỉ mục trong bất kỳ trình xem PDF nào.

---

## ## Tiền Xử Lý Hình Ảnh Cho OCR – Mẹo & Thủ Thuật

Mặc dù hai bộ lọc chúng tôi đã thêm thường đủ, bạn có thể gặp các hình ảnh khó xử lý. Dưới đây là một vài bước bổ sung bạn có thể thử:

| Issue | Additional Filter | How to Add |
|-------|-------------------|------------|
| Độ tương phản thấp | `ContrastFilter { Level = 30 }` | `ocrEngine.Filters.Add(new ContrastFilter { Level = 30 });` |
| Nhiễu nền mạnh | `BinarizationFilter { Threshold = 128 }` | `ocrEngine.Filters.Add(new BinarizationFilter { Threshold = 128 });` |
| Hướng hỗn hợp (dọc & ngang) | `OrientationFilter()` | `ocrEngine.Filters.Add(new OrientationFilter());` |

> **Lưu ý:** Thêm quá nhiều bộ lọc có thể làm chậm quá trình. Hãy thử mỗi thay đổi trên một trang duy nhất trước khi mở rộng.

---

## ## Nhận Dạng Hình Ảnh Văn Bản Tiếng Hàn – Những Rủi Ro Thường Gặp

Chữ viết tiếng Hàn chứa các âm tiết Hangul dày đặc. Nếu bạn thấy kết quả bị rối loạn:

1. **Đảm bảo mô hình ngôn ngữ đã được tải xuống đầy đủ** – kiểm tra console để xem thông báo như “Downloading Korean model…”.  
2. **Tăng `MaxAngle`** trong `DeskewFilter` nếu các bản quét của bạn bị xoay quá 12°.  
3. **Tăng bộ nhớ GPU** bằng cách đặt `ocrEngine.GpuMemoryLimit = 2048;` (giá trị tính bằng MB).

Những điều chỉnh này ảnh hưởng trực tiếp đến thành công của **recognize Korean text image**.

---

## ## Tạo PDF Hình Ảnh Có Thể Tìm Kiếm – Kiểm Tra Kết Quả

Sau khi chương trình hoàn thành, mở `korean_page.pdf` bằng bất kỳ trình đọc PDF nào (Adobe Acrobat Reader, Foxit, thậm chí Chrome). Bạn nên có thể:

- **Chọn văn bản** bằng chuột như thể nó là một PDF gốc.  
- **Tìm kiếm** các từ tiếng Hàn bằng hộp tìm kiếm tích hợp.

Nếu lớp văn bản hiển thị trống, hãy kiểm tra lại rằng phương thức `Export` nhận đúng đường dẫn hình ảnh và kết quả OCR chứa `RecognitionResult.Text` không rỗng.

---

## ## Đầu Ra JSON Đầy Đủ – Những Gì Bạn Mong Đợi

Console in ra một payload JSON được định dạng đẹp. Một ví dụ đã cắt ngắn như sau:

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

---

## ## Khắc Phục Sự Cố & Câu Hỏi Thường Gặp

**Hỏi: PDF của tôi quá lớn so với hình ảnh gốc.**  
**Đáp:** Bộ xuất nhúng bitmap gốc ở độ phân giải gốc. Nếu kích thước là vấn đề, hãy giảm kích thước hình ảnh *trước* khi nhận dạng:

```csharp
ocrEngine.Filters.Add(new ResizeFilter { MaxWidth = 1240, MaxHeight = 1754 });
```

**Hỏi: OCR trả về chuỗi rỗng.**  
**Đáp:** Kiểm tra lại đường dẫn hình ảnh và chắc chắn tệp không bị hỏng. Ngoài ra, đảm bảo driver GPU đã được cập nhật; driver cũ có thể gây lỗi im lặng.

**Hỏi: Tôi có thể xử lý nhiều trang trong một vòng lặp không?**  
**Đáp:** Chắc chắn. Đặt các bước 4‑6 trong vòng lặp `foreach (var file in Directory.GetFiles("Resources", "*.jpg"))` và thay đổi đường dẫn PDF đầu ra cho phù hợp.

---

## ## Kết Luận

Chúng ta vừa **converted image to PDF** trong khi giữ lại văn bản có thể tìm kiếm, tất cả nhờ vào pipeline mạnh mẽ của Aspose OCR. Bằng cách **preprocess image for OCR**, bạn tăng độ chính xác; bằng **recognize Korean text image**, bạn xử lý các script phức tạp; và bằng **create searchable pdf image**, bạn có được một tài liệu di động, có thể lập chỉ mục.

Lấy mã nguồn, chỉ vào các bản quét của bạn, và thử nghiệm với các bộ lọc hoặc mô hình ngôn ngữ bổ sung. Mẫu tương tự cũng hoạt động cho tiếng Trung, tiếng Nhật, hoặc bất kỳ ngôn ngữ dựa trên Latin nào — chỉ cần thay `LanguageModel.Korean` bằng enum phù hợp.

Có thêm câu hỏi? Để lại bình luận, và chúc bạn lập trình vui vẻ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}