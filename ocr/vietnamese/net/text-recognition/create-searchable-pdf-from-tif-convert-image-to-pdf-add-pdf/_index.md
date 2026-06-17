---
category: general
date: 2026-04-04
description: Tạo PDF có thể tìm kiếm từ ảnh TIF trong C# – tìm hiểu cách chuyển đổi
  ảnh sang PDF, thêm siêu dữ liệu PDF và tạo tài liệu có thể tìm kiếm bằng Aspose.OCR.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- add metadata to pdf
- add pdf metadata
- create pdf from tif
language: vi
og_description: Tạo PDF có thể tìm kiếm từ tệp TIF bằng C#. Chuyển đổi hình ảnh sang
  PDF, thêm siêu dữ liệu PDF và tạo tài liệu có thể tìm kiếm bằng Aspose.OCR.
og_title: Tạo PDF có thể tìm kiếm từ TIF – Hướng dẫn từng bước
tags:
- Aspose.OCR
- C#
- PDF generation
title: Tạo PDF có thể tìm kiếm từ TIF – Chuyển đổi hình ảnh sang PDF, Thêm siêu dữ
  liệu PDF
url: /vi/net/text-recognition/create-searchable-pdf-from-tif-convert-image-to-pdf-add-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo PDF có thể tìm kiếm từ TIF – Hướng dẫn đầy đủ bằng C#

Bạn đã bao giờ cần **tạo PDF có thể tìm kiếm** từ một hoá đơn đã quét nhưng không chắc làm sao để giữ cho văn bản có thể tìm kiếm và siêu dữ liệu tệp gọn gàng? Bạn không phải là người duy nhất. Trong nhiều dự án tự động hoá, PDF phải vừa có thể đọc được bởi máy móc vừa được gắn thẻ đúng cách với các thông tin như tiêu đề, tác giả và ngưỡng độ tin cậy.

Trong hướng dẫn này, chúng ta sẽ đi qua một giải pháp hoàn chỉnh **chuyển đổi hình ảnh sang PDF**, chèn **siêu dữ liệu PDF**, và lọc các kết quả OCR có độ tin cậy thấp — tất cả đều sử dụng thư viện Aspose.OCR. Khi kết thúc, bạn sẽ có một đoạn mã sẵn sàng dùng mà có thể chèn vào bất kỳ dự án .NET nào, cùng với một vài mẹo để xử lý các trường hợp đặc biệt.

## Yêu cầu trước

- .NET 6.0 trở lên (mã cũng chạy trên .NET Framework 4.6+)
- Gói NuGet Aspose.OCR (`Install-Package Aspose.OCR`)
- Một ảnh TIF bạn muốn chuyển thành PDF có thể tìm kiếm (ví dụ: `input.tif`)
- Kiến thức cơ bản về C# và Visual Studio (hoặc IDE yêu thích của bạn)

Không cần dịch vụ bên ngoài nào khác — toàn bộ quá trình chạy cục bộ.

## Bước 1 – Thiết lập Engine OCR (Tạo lõi PDF có thể tìm kiếm)

Điều đầu tiên chúng ta cần là một thể hiện `OcrEngine` biết ngôn ngữ cần nhận dạng. Trong hầu hết các kịch bản kinh doanh, tiếng Anh là đủ, nhưng bạn có thể thay `Language.English` bằng bất kỳ ngôn ngữ nào được hỗ trợ.

```csharp
using Aspose.OCR;
using Aspose.OCR.Pdf;   // PDF‑related extensions

// Initialize OCR engine with English language
OcrEngine ocrEngine = new OcrEngine
{
    Language = Language.English
};
```

**Tại sao điều này quan trọng:** Engine OCR thực hiện công việc nặng nề chuyển các pixel raster thành văn bản Unicode. Đặt đúng ngôn ngữ giúp cải thiện độ chính xác và giảm số từ có độ tin cậy thấp mà sau này sẽ bị lọc bỏ.

> **Mẹo chuyên nghiệp:** Nếu bạn xử lý tài liệu đa ngôn ngữ, hãy khởi tạo nhiều engine hoặc sử dụng `Language.Multilingual` để Aspose tự động phát hiện ngôn ngữ.

## Bước 2 – Tải ảnh TIF lên (Tạo PDF từ TIF)

Bây giờ chúng ta chỉ định engine tới tệp nguồn. Trợ giúp `ImageStream.FromFile` đọc ảnh vào một stream mà engine OCR có thể tiêu thụ.

```csharp
// Load the TIF image you want to make searchable
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/input.tif");
```

Bạn có thể tự hỏi, *“Có thể dùng JPEG hoặc PNG thay thế không?”* Hoàn toàn có — Aspose.OCR hỗ trợ hầu hết các định dạng raster. Chỉ cần đổi phần mở rộng tệp và bạn đã sẵn sàng.

## Bước 3 – Cấu hình tùy chọn PDF (Thêm siêu dữ liệu vào PDF)

Trước khi chuyển đổi, chúng ta định nghĩa một đối tượng `PdfOptions`. Đây là nơi chúng ta **thêm siêu dữ liệu PDF** như tiêu đề và tác giả, đồng thời chỉ định engine loại bỏ các từ có độ tin cậy dưới một ngưỡng.

```csharp
PdfOptions searchablePdfOptions = new PdfOptions
{
    Title = "Invoice #12345",
    Author = "MyCompany",
    // Hide words with confidence lower than 0.8 (80%)
    MinConfidence = 0.8f
};
```

**Điều gì đang diễn ra?**  
- `Title` và `Author` trở thành một phần của từ điển thông tin tài liệu PDF, giúp tệp dễ dàng được lập chỉ mục trong các hệ thống quản lý tài liệu.  
- `MinConfidence` là một rào chắn: OCR thường đọc sai các ký tự mờ; lọc chúng ra giúp lớp văn bản có thể tìm kiếm sạch sẽ hơn và cải thiện việc trích xuất văn bản ở các bước sau.

Nếu bạn cần siêu dữ liệu tùy chỉnh (ví dụ: `Subject`, `Keywords`), có thể đặt chúng qua `PdfOptions.CustomProperties`.

## Bước 4 – Chuyển đổi ảnh thành PDF có thể tìm kiếm (Chuyển đổi ảnh sang PDF)

Với engine đã sẵn sàng và các tùy chọn đã được thiết lập, lời gọi cuối cùng thực hiện việc chuyển đổi. Nó ghi một PDF có thể tìm kiếm vào đĩa, nhúng lớp văn bản OCR dưới ảnh gốc.

```csharp
ocrEngine.ConvertToSearchablePdf(
    outputPath: @"YOUR_DIRECTORY/output.pdf",
    pdfOptions: searchablePdfOptions);
```

Sau khi dòng này chạy, `output.pdf` sẽ chứa:
- Ảnh TIF gốc làm nền hình ảnh  
- Một lớp văn bản vô hình mà các công cụ tìm kiếm và thao tác sao chép‑dán có thể đọc được  
- Siêu dữ liệu chúng ta đã định nghĩa trước đó (tiêu đề, tác giả, v.v.)

### Kết quả mong đợi

Mở PDF đã tạo trong Adobe Reader hoặc bất kỳ trình xem PDF nào và thử chọn văn bản. Bạn sẽ có thể sao chép các câu trùng khớp với bản quét gốc. Hộp thoại **Properties** của tài liệu sẽ hiển thị tiêu đề “Invoice #12345” và tác giả “MyCompany”.

## Bước 5 – Xác minh lọc độ tin cậy (Tại sao MinConfidence hữu ích)

Thực tế, chúng ta nên kiểm tra xem các từ có độ tin cậy thấp đã thực sự bị loại bỏ chưa. Bạn có thể xem văn bản ẩn của PDF bằng công cụ như `pdftotext`:

```bash
pdftotext output.pdf - | grep -i "unlikelyword"
```

Nếu từ đó không xuất hiện, bộ lọc `MinConfidence` đã hoạt động như mong đợi. Điều chỉnh ngưỡng (ví dụ, `0.7f`) nếu bạn cần bộ lọc mạnh hơn hoặc nhẹ hơn.

## Bước 6 – Xử lý nhiều trang (Tạo PDF có thể tìm kiếm từ TIF đa trang)

Nhiều hoá đơn được lưu dưới dạng TIFF đa trang. Aspose.OCR tự động coi mỗi khung ảnh là một trang riêng. Chỉ cần chỉ định engine tới tệp đa trang; lời gọi `ConvertToSearchablePdf` sẽ tạo ra một PDF có thể tìm kiếm đa trang.

```csharp
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/multi_page.tif");
ocrEngine.ConvertToSearchablePdf(@"YOUR_DIRECTORY/multi_output.pdf", searchablePdfOptions);
```

**Trường hợp đặc biệt:** Nếu một trang trống, OCR có thể vẫn tạo ra một lớp văn bản rỗng, điều này không gây hại. Tuy nhiên, bạn có thể bỏ qua các trang trống bằng cách kiểm tra `ocrEngine.HasText` trước khi chuyển đổi.

## Bước 7 – Đóng gói ví dụ đầy đủ (Tất cả các bước cùng nhau)

Dưới đây là một chương trình duy nhất, sẵn sàng chạy, kết hợp mọi thứ lại. Thay `YOUR_DIRECTORY` bằng đường dẫn thư mục thực tế trên máy của bạn.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Pdf;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.English
        };

        // 2️⃣ Load the TIF image (create pdf from tif)
        string inputPath = @"YOUR_DIRECTORY/input.tif";
        ocrEngine.Image = ImageStream.FromFile(inputPath);

        // 3️⃣ Set PDF metadata and confidence filter
        PdfOptions pdfOptions = new PdfOptions
        {
            Title = "Invoice #12345",
            Author = "MyCompany",
            MinConfidence = 0.8f
        };

        // 4️⃣ Convert to searchable PDF (convert image to pdf)
        string outputPath = @"YOUR_DIRECTORY/output.pdf";
        ocrEngine.ConvertToSearchablePdf(outputPath, pdfOptions);

        Console.WriteLine($"✅ Searchable PDF created at: {outputPath}");
    }
}
```

Chạy chương trình (`dotnet run` hoặc nhấn **F5** trong Visual Studio) và bạn sẽ thấy thông báo xác nhận. PDF đã tạo sẽ nằm cạnh ảnh nguồn, sẵn sàng để lập chỉ mục hoặc lưu trữ.

## Câu hỏi thường gặp & Những lưu ý

| Câu hỏi | Trả lời |
|----------|--------|
| **Có thể thêm phông chữ tùy chỉnh vào lớp có thể tìm kiếm không?** | Lớp OCR sử dụng Unicode; giao diện hiển thị được quyết định bởi ảnh gốc, vì vậy không cần nhúng phông chữ thêm. |
| **Nếu TIF của tôi có màu thì sao?** | Aspose.OCR tự động chuyển ảnh màu sang thang xám để OCR, nhưng bạn có thể giữ màu gốc trong PDF bằng cách đặt `PdfOptions.PreserveColor = true`. |
| **Thư viện có hỗ trợ đa luồng không?** | Mỗi thể hiện `OcrEngine` nên được một luồng duy nhất sử dụng. Đối với xử lý song song, tạo một engine riêng cho mỗi luồng. |
| **Làm sao để mã hoá PDF?** | Sử dụng `PdfOptions.Security` để đặt mật khẩu và quyền truy cập sau khi chuyển đổi OCR. |

## Các bước tiếp theo (Mở rộng bộ công cụ PDF của bạn)

- **Xử lý hàng loạt:** Duyệt qua một thư mục chứa các TIFF và tạo PDF có thể tìm kiếm cho mỗi tệp.  
- **Xử lý hậu kỳ:** Dùng Aspose.PDF để hợp nhất các PDF đã tạo thành một tài liệu master duy nhất.  
- **Siêu dữ liệu nâng cao:** Điền các trường XMP tùy chỉnh để tích hợp tốt hơn với SharePoint hoặc hệ thống ECM.

Tất cả các mở rộng này dựa trên mẫu cốt lõi chúng ta vừa khám phá: **tạo PDF có thể tìm kiếm**, **chuyển đổi ảnh sang PDF**, và **thêm siêu dữ liệu PDF**.

---

*Chúc lập trình vui vẻ! Nếu gặp khó khăn, hãy để lại bình luận bên dưới hoặc tham khảo tài liệu Aspose.OCR để cập nhật các API mới nhất.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}