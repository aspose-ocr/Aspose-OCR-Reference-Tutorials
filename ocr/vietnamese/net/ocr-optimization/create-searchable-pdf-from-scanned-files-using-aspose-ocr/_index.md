---
category: general
date: 2026-01-04
description: Tạo PDF có thể tìm kiếm từ PDF đã quét nhanh chóng. Tìm hiểu cách chuyển
  đổi PDF đã quét, thêm OCR vào PDF và điều chỉnh chất lượng hình ảnh với Aspose OCR
  trong C#.
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- add ocr to pdf
- adjust image quality
- how to use ocr
language: vi
og_description: Tạo PDF có thể tìm kiếm từ PDF đã quét nhanh chóng. Hãy làm theo hướng
  dẫn từng bước này để chuyển đổi PDF đã quét, thêm OCR vào PDF và điều chỉnh chất
  lượng hình ảnh.
og_title: Tạo PDF có thể tìm kiếm từ các tệp đã quét bằng Aspose OCR
tags:
- Aspose OCR
- C#
- PDF processing
title: Tạo PDF có thể tìm kiếm từ các tệp đã quét bằng Aspose OCR
url: /vi/net/ocr-optimization/create-searchable-pdf-from-scanned-files-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo PDF có thể tìm kiếm từ các tệp đã quét bằng Aspose OCR

Bạn đã bao giờ cần **tạo PDF có thể tìm kiếm** từ một đống tài liệu đã quét nhưng không biết bắt đầu từ đâu? Bạn không cô đơn—nhiều nhà phát triển gặp phải rào cản này khi xây dựng các pipeline quản lý tài liệu. Tin tốt là gì? Với Aspose OCR, bạn có thể **chuyển đổi PDF đã quét**, thêm một chút OCR, và tinh chỉnh chất lượng hình ảnh chỉ trong vài dòng C#.

Trong hướng dẫn này, chúng ta sẽ đi qua toàn bộ quy trình, từ việc tải PDF đã quét đến lưu phiên bản có thể tìm kiếm đầy đủ. Khi kết thúc, bạn sẽ biết **cách sử dụng OCR** với Aspose, tại sao mỗi thiết lập lại quan trọng, và cần điều chỉnh gì khi mọi thứ không diễn ra như mong đợi. Không có các tham chiếu mơ hồ—chỉ có một ví dụ hoàn chỉnh, có thể chạy được mà bạn có thể đưa vào dự án ngay hôm nay.

## Yêu cầu trước

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

- .NET 6.0 hoặc mới hơn (mã cũng hoạt động với .NET Core và .NET Framework)
- Giấy phép Aspose OCR hợp lệ (bản dùng thử miễn phí đủ cho việc thử nghiệm)
- Một tệp PDF đầu vào có tên `input.pdf` được đặt trong thư mục bạn kiểm soát
- Visual Studio 2022 hoặc bất kỳ trình soạn thảo C# nào bạn thích

Đó là tất cả. Nếu có bất kỳ mục nào bạn chưa quen, hãy tạm dừng và cài đặt phần còn thiếu—không cần gì khác.

## Bước 1: Khởi tạo OCR Engine và tải PDF đã quét  
**(Đây là nơi chúng ta **thêm OCR vào PDF** lần đầu tiên.)**

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Create the OCR engine instance
OcrEngine ocrEngine = new OcrEngine();

// Load the scanned PDF from disk
ocrEngine.LoadPdf(@"C:\Docs\input.pdf");
```

*Tại sao cần bước này?*  
`OcrEngine` là trái tim của Aspose OCR. Việc tải PDF cho engine biết nơi tìm các hình raster mà nó sẽ phân tích sau này. Nếu bỏ qua bước này, sẽ không có gì để chuyển đổi và các bước tiếp theo sẽ gây ra ngoại lệ.

> **Mẹo chuyên nghiệp:** Nếu PDF của bạn được bảo vệ bằng mật khẩu, hãy dùng `ocrEngine.LoadPdf(path, password)` để tránh lỗi thời gian chạy.

## Bước 2: Đặt ngôn ngữ chính và ngôn ngữ bổ sung  
**(Chúng ta sẽ **chuyển đổi PDF đã quét** sang tiếng Anh, Pháp và Đức.)**

```csharp
// Primary language – the most common language in the document
ocrEngine.Config.Language = Language.English;

// Add extra languages if the document contains multilingual text
ocrEngine.Config.AdditionalLanguages = new[] { Language.French, Language.German };
```

*Ngôn ngữ có quan trọng như thế nào?*  
Độ chính xác của OCR phụ thuộc vào bộ ký tự mà nó mong đợi. Bằng cách khai báo tiếng Anh là ngôn ngữ chính và thêm tiếng Pháp/Đức, engine có thể giải mã đúng các ký tự có dấu và glyph đặc biệt. Bỏ qua bước này thường dẫn đến văn bản rối rắm.

## Bước 3: Điều chỉnh chất lượng hình ảnh – Tinh chỉnh đầu ra PDF  
**(Ở đây chúng ta **điều chỉnh chất lượng hình ảnh** để cân bằng kích thước tệp và khả năng đọc.)**

```csharp
PdfSaveOptions pdfOptions = new PdfSaveOptions
{
    ImageQuality = 90,          // JPEG quality for embedded images (0‑100)
    Compress = true,            // Enable PDF compression to shrink file size
    PreserveOriginalLayout = true // Keep the scanned layout intact
};
```

*Tại sao cần tinh chỉnh `ImageQuality`?*  
Giá trị cao hơn (90‑100) giữ độ nét, điều này quan trọng cho độ chính xác của OCR, nhưng đồng thời làm tăng kích thước tệp. Nếu bạn đang lưu trữ hàng triệu trang, hãy hạ xuống 70‑80 để có PDF mỏng hơn mà không mất quá nhiều khả năng đọc.

## Bước 4: Lưu kết quả dưới dạng PDF có thể tìm kiếm  
**(Bây giờ chúng ta cuối cùng **tạo PDF có thể tìm kiếm** mà bạn có thể lập chỉ mục.)**

```csharp
// Export the OCR result as a searchable PDF
ocrEngine.SaveAsSearchablePdf(@"C:\Docs\output.pdf", pdfOptions);

// Let the user know we’re done
Console.WriteLine("Searchable PDF created at C:\\Docs\\output.pdf");
```

*Thực tế gì sẽ xảy ra?*  
Aspose OCR trích xuất lớp văn bản từ mỗi trang và nhúng nó phía sau hình ảnh gốc. PDF vẫn giữ nguyên hình ảnh, nhưng bây giờ bạn có thể chọn, sao chép và tìm kiếm văn bản—một lợi thế lớn cho các workflow tiếp theo.

## Bước 5: Xác minh đầu ra (Tùy chọn nhưng Được khuyến nghị)  
Dễ dàng cho rằng mọi thứ đã hoạt động, nhưng một kiểm tra nhanh sẽ tiết kiệm được nhiều phiền toái sau này.

```csharp
using System.Diagnostics;

// Open the generated PDF automatically (Windows only)
Process.Start(new ProcessStartInfo
{
    FileName = @"C:\Docs\output.pdf",
    UseShellExecute = true
});
```

Mở tệp, thử chọn một từ, hoặc nhấn `Ctrl+F` và gõ một cụm từ mà bạn biết tồn tại trong bản quét gốc. Nếu văn bản có thể chọn được, bạn đã **tạo PDF có thể tìm kiếm** thành công.

## Các trường hợp đặc biệt thường gặp & Cách xử lý  

| Tình huống | Nguyên nhân | Giải pháp nhanh |
|-----------|-------------|-----------------|
| **Trang có độ phân giải hỗn hợp** (một số 150 dpi, một số khác 300 dpi) | Chất lượng OCR thay đổi theo trang, dẫn đến khả năng tìm kiếm không đồng đều. | Đặt `ocrEngine.Config.Dpi = 300;` trước khi tải để ép nâng độ phân giải, hoặc tiền xử lý bằng `ImageProcessor` để chuẩn hoá DPI. |
| **PDF được mã hoá** | Aspose OCR không thể đọc nếu không có mật khẩu. | Truyền mật khẩu vào `LoadPdf` như đã chỉ ra ở trên. |
| **PDF lớn (>500 MB)** | Tiêu thụ bộ nhớ tăng mạnh, gây `OutOfMemoryException`. | Xử lý tài liệu theo từng khối: `ocrEngine.SplitPdfIntoPages();` rồi OCR từng trang riêng biệt và hợp nhất kết quả. |
| **Ký tự không phải Latin** (ví dụ: Cyrillic) | Ngôn ngữ chưa được thêm, nên các ký tự hiển thị thành “?” | Thêm `Language.Russian` (hoặc bất kỳ ngôn ngữ nào cần) vào `AdditionalLanguages`. |
| **Chất lượng hình ảnh quá thấp** | Văn bản bị mờ, OCR thất bại. | Tăng `ImageQuality` hoặc dùng `pdfOptions.Dpi = 300;` để nhúng hình ảnh có độ phân giải cao hơn. |

## Ví dụ đầy đủ, sẵn sàng chạy  

Dưới đây là chương trình hoàn chỉnh mà bạn có thể sao chép‑dán vào một ứng dụng console mới. Nó bao gồm tất cả các bước, xử lý lỗi, và chú thích để dễ hiểu.

```csharp
using System;
using System.Diagnostics;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace SearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Paths – adjust to your environment
            string inputPath = @"C:\Docs\input.pdf";
            string outputPath = @"C:\Docs\output.pdf";

            try
            {
                // 1️⃣ Initialize OCR engine and load scanned PDF
                OcrEngine ocrEngine = new OcrEngine();
                ocrEngine.LoadPdf(inputPath);

                // 2️⃣ Configure languages (primary + additional)
                ocrEngine.Config.Language = Language.English;
                ocrEngine.Config.AdditionalLanguages = new[] { Language.French, Language.German };

                // 3️⃣ Set PDF save options – adjust image quality as needed
                PdfSaveOptions pdfOptions = new PdfSaveOptions
                {
                    ImageQuality = 90,
                    Compress = true,
                    PreserveOriginalLayout = true
                };

                // 4️⃣ Save as searchable PDF
                ocrEngine.SaveAsSearchablePdf(outputPath, pdfOptions);
                Console.WriteLine($"✅ Searchable PDF created at {outputPath}");

                // 5️⃣ Optional: open the file to verify
                Process.Start(new ProcessStartInfo
                {
                    FileName = outputPath,
                    UseShellExecute = true
                });
            }
            catch (Exception ex)
            {
                // Friendly error message – helps during debugging
                Console.WriteLine($"❌ Oops! Something went wrong: {ex.Message}");
                // For real‑world apps, consider logging the stack trace
            }
        }
    }
}
```

**Kết quả mong đợi:**  
```
✅ Searchable PDF created at C:\Docs\output.pdf
```

Khi bạn mở `output.pdf`, bạn sẽ có thể chọn và tìm kiếm bất kỳ văn bản nào đã có trong bản quét gốc.

---

## Câu hỏi thường gặp (FAQs)

**H: Điều này có hoạt động với PDF chứa cả hình ảnh quét và văn bản gốc không?**  
Đ: Hoàn toàn có. Aspose OCR chỉ thêm lớp văn bản ẩn ở những nơi cần thiết, để lại văn bản hiện có không bị thay đổi.

**H: Tôi có thể xử lý hàng loạt các PDF trong một thư mục không?**  
Đ: Có. Bao bọc đoạn mã trên trong vòng lặp `foreach (var file in Directory.GetFiles(folder, "*.pdf"))` và điều chỉnh đường dẫn đầu ra cho phù hợp.

**H: Làm sao để giảm kích thước PDF cuối cùng hơn nữa?**  
Đ: Hạ `ImageQuality` xuống 70‑80, bật `Compress`, hoặc dùng `pdfOptions.Dpi = 150` để giảm độ phân giải hình ảnh trước khi nhúng.

**H: Có cách nào để trích xuất văn bản OCR mà không tạo PDF không?**  
Đ: Gọi `ocrEngine.ExtractText();` sau khi tải PDF. Phương thức này trả về một chuỗi văn bản thuần mà bạn có thể lưu hoặc lập chỉ mục.

---

## Kết luận  

Chúng ta vừa đi qua **cách sử dụng OCR** với Aspose để **tạo PDF có thể tìm kiếm** từ tài liệu đã quét, đã chỉ ra cách **chuyển đổi PDF đã quét**, trình bày **thêm OCR vào PDF**, và giải thích cách **điều chỉnh chất lượng hình ảnh** để đạt kết quả tối ưu. Mã mẫu đầy đủ đã sẵn sàng chạy, và bảng khắc phục sự cố sẽ giúp bạn tiến nhanh khi gặp vấn đề bất ngờ.

Tiếp theo bạn có thể thử:

- Các gói ngôn ngữ khác nhau cho kho lưu trữ đa ngôn ngữ
- Tiền xử lý hình ảnh tùy chỉnh (cân bằng, loại bỏ nhiễu) qua `ImageProcessor`
- Tích hợp PDF có thể tìm kiếm vào pipeline SharePoint hoặc ElasticSearch

Đừng ngại để lại bình luận nếu bạn gặp khó khăn hoặc phát hiện cách tối ưu thông minh. Chúc bạn lập trình vui vẻ và tận hưởng những PDF có thể tìm kiếm ngay lập tức!

![Lưu đồ tạo PDF có thể tìm kiếm hiển thị engine OCR → cấu hình ngôn ngữ → tùy chọn lưu PDF → đầu ra PDF có thể tìm kiếm](create-searchable-pdf-flow.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}