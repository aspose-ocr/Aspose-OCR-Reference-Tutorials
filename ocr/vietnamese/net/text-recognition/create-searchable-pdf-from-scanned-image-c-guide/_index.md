---
category: general
date: 2026-04-26
description: Tạo PDF có thể tìm kiếm từ hình ảnh đã quét bằng Aspose OCR trong C#.
  Tìm hiểu cách chuyển đổi hình ảnh đã quét, trích xuất văn bản và nhanh chóng tạo
  PDF có thể tìm kiếm.
draft: false
keywords:
- create searchable pdf
- convert scanned image
- extract text from image
- how to ocr document
- convert tiff to pdf
language: vi
og_description: Tạo PDF có thể tìm kiếm từ hình ảnh đã quét bằng Aspose OCR. Mã C#
  từng bước để chuyển đổi, trích xuất văn bản và tạo PDF có thể tìm kiếm.
og_title: Tạo PDF có thể tìm kiếm từ hình ảnh đã quét – Hướng dẫn C#
tags:
- Aspose OCR
- C#
- PDF
- OCR
title: Tạo PDF có thể tìm kiếm từ hình ảnh đã quét – Hướng dẫn C#
url: /vi/net/text-recognition/create-searchable-pdf-from-scanned-image-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo PDF có thể tìm kiếm từ ảnh quét – Hướng dẫn C#

Bạn đã bao giờ cần **tạo PDF có thể tìm kiếm** từ các hợp đồng giấy, biên lai, hoặc các tài liệu lưu trữ cũ chưa? Bạn không phải là người duy nhất—hầu hết các nhà phát triển gặp phải rào cản này khi khách hàng giao cho họ một đống các tệp TIFF quét và mong muốn một PDF có thể tìm kiếm là sản phẩm cuối cùng.

Trong hướng dẫn này, chúng tôi sẽ chỉ cho bạn cách **thực hiện OCR trên tài liệu** và chuyển đổi ảnh quét thành **PDF có thể tìm kiếm** bằng Aspose OCR cho .NET. Khi kết thúc, bạn sẽ có thể **chuyển đổi ảnh quét**, **trích xuất văn bản từ ảnh**, và thậm chí xử lý các tệp TIFF đa trang mà không gặp khó khăn.

## Những gì bạn cần

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

* .NET 6.0 trở lên (API hoạt động với .NET Core, .NET Framework và .NET 5+).  
* Giấy phép Aspose OCR hợp lệ hoặc bạn chấp nhận watermark đánh giá.  
* Gói NuGet `Aspose.OCR` đã được cài đặt (`dotnet add package Aspose.OCR`).  
* Một tệp TIFF mẫu (ví dụ: `contract_scan.tif`) mà bạn muốn chuyển thành PDF có thể tìm kiếm.

Chỉ vậy—không cần thư viện bổ sung, không cấu hình phức tạp. Sẵn sàng? Bắt đầu thôi.

![Ví dụ tạo PDF có thể tìm kiếm](create-searchable-pdf.png "ví dụ tạo pdf có thể tìm kiếm")

## Bước 1 – Khởi tạo Engine OCR (Tạo PDF có thể tìm kiếm)

Điều đầu tiên cần làm: bạn cần một thể hiện của `OcrEngine`. Đối tượng này là công cụ chính đọc bitmap, nhận dạng ký tự và trả lại văn bản cho bạn.  

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Tell the engine which language to look for – Latin works for most English documents
ocrEngine.Language = Language.Latin;
```

**Tại sao phải đặt ngôn ngữ?**  
Nếu để mặc định, Aspose sẽ thử mọi gói ngôn ngữ, làm chậm quá trình. Đặt `Language.Latin` cho engine tập trung vào bảng chữ cái Latin, giúp tăng tốc và cho kết quả chính xác hơn cho các hợp đồng bằng tiếng Anh.

## Bước 2 – Tải ảnh quét của bạn (Chuyển đổi ảnh quét)

Bây giờ chúng ta cung cấp cho engine ảnh mà chúng ta muốn xử lý. Aspose có thể đọc từ đường dẫn tệp, stream, hoặc thậm chí một `byte[]`. Để đơn giản, chúng ta sẽ dùng `ImageStream.FromFile`.  

```csharp
// Load the TIFF (or any supported image format)
ocrEngine.Image = ImageStream.FromFile(@"C:\Docs\contract_scan.tif");
```

Nếu sau này bạn cần **chuyển đổi TIFF sang PDF**, hãy nhớ rằng các TIFF đa trang sẽ được xử lý tự động—mỗi khung sẽ trở thành một trang PDF riêng.

## Bước 3 – Thực hiện OCR và Lấy Văn bản (Trích xuất văn bản từ ảnh)

Thực hiện OCR đơn giản như gọi `Recognize`. Engine sẽ trả về một `RecognitionResult` chứa văn bản thuần, điểm tin cậy và thông tin bố cục.  

```csharp
// Perform the OCR operation
RecognitionResult result = ocrEngine.Recognize();

// The raw text is available via the Text property
string extractedText = result.Text;

// Quick sanity check – print the first 200 characters
Console.WriteLine(extractedText.Substring(0, Math.Min(200, extractedText.Length)));
```

**Mẹo chuyên nghiệp:** Nếu bạn chỉ cần văn bản (không cần PDF), bạn có thể dừng ở đây và ghi `extractedText` vào tệp `.txt`. Nhưng hầu hết thời gian mục tiêu của chúng ta là PDF có thể tìm kiếm, vì vậy chúng ta sẽ tiếp tục.

## Bước 4 – Lưu dưới dạng PDF có thể tìm kiếm (Tạo PDF có thể tìm kiếm)

Aspose làm cho bước cuối cùng trở nên đơn giản: chỉ cần gọi `Save` với `SaveFormat.PdfSearchable`. Bên trong, thư viện sẽ nhúng văn bản đã trích xuất dưới dạng lớp vô hình trong khi vẫn giữ nguyên hình ảnh gốc.  

```csharp
// Save the result as a searchable PDF
ocrEngine.Save(@"C:\Docs\contract_searchable.pdf", SaveFormat.PdfSearchable);
```

Khi bạn mở `contract_searchable.pdf` trong bất kỳ trình xem PDF nào, bạn sẽ có thể chọn, sao chép và tìm kiếm văn bản—đúng như khách hàng mong đợi từ một “PDF có thể tìm kiếm”.

## Xử lý TIFF đa trang (Chuyển đổi Tiff sang PDF)

Nếu tệp nguồn của bạn chứa nhiều trang, Aspose sẽ tự động coi mỗi khung là một trang riêng. Không cần vòng lặp bổ sung. Tuy nhiên, bạn có thể muốn kiểm soát DPI hoặc chất lượng ảnh cho mỗi trang:

```csharp
// Optional: tweak image processing settings before OCR
ocrEngine.ImageProcessingOptions.Dpi = 300; // higher DPI improves accuracy
ocrEngine.ImageProcessingOptions.Compression = ImageCompression.Jpeg;
```

Sau khi thiết lập các tùy chọn này, lặp lại **Bước 2** cho mỗi khung, hoặc đơn giản chỉ cần trỏ `ImageStream.FromFile` tới tệp TIFF đa trang và để Aspose thực hiện công việc.

## Những lỗi thường gặp và cách khắc phục

| Triệu chứng | Nguyên nhân khả dĩ | Cách khắc phục |
|-------------|--------------------|----------------|
| Văn bản bị rối hoặc thiếu | Cài đặt ngôn ngữ sai | Đặt `ocrEngine.Language` thành gói ngôn ngữ đúng (ví dụ: `Language.German`). |
| PDF quá lớn (10 MB cho một trang quét) | Mức nén ảnh mặc định quá thấp | Điều chỉnh `ocrEngine.ImageProcessingOptions.Compression` thành `Jpeg` và đặt giá trị `Quality` hợp lý (0‑100). |
| OCR chạy rất chậm | Sử dụng phát hiện ngôn ngữ mặc định `Auto` | Cài đặt ngôn ngữ mong muốn một cách rõ ràng. |
| Không có lớp có thể tìm kiếm xuất hiện | Lưu bằng `SaveFormat.Pdf` thay vì `PdfSearchable` | Sử dụng `PdfSearchable`. |

## Ví dụ đầy đủ từ đầu đến cuối

Kết hợp tất cả lại, đây là một ứng dụng console sẵn sàng chạy mà bạn có thể sao chép‑dán vào Visual Studio:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace SearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.Latin,
                // Optional: improve accuracy for low‑resolution scans
                ImageProcessingOptions = { Dpi = 300, Compression = ImageCompression.Jpeg }
            };

            // 2️⃣ Load the scanned image (convert scanned image)
            string inputPath = @"C:\Docs\contract_scan.tif";
            ocrEngine.Image = ImageStream.FromFile(inputPath);

            // 3️⃣ Run OCR and extract text (extract text from image)
            RecognitionResult result = ocrEngine.Recognize();
            Console.WriteLine("First 200 characters of extracted text:");
            Console.WriteLine(result.Text.Substring(0, Math.Min(200, result.Text.Length)));

            // 4️⃣ Save as searchable PDF (create searchable pdf)
            string outputPath = @"C:\Docs\contract_searchable.pdf";
            ocrEngine.Save(outputPath, SaveFormat.PdfSearchable);
            Console.WriteLine($"Searchable PDF created at: {outputPath}");
        }
    }
}
```

**Bạn sẽ thấy:**  
* Một cửa sổ console in ra một đoạn trích của văn bản đã OCR.  
* Một tệp `contract_searchable.pdf` nằm bên cạnh tệp TIFF gốc của bạn. Mở nó, nhấn **Ctrl + F**, và tìm bất kỳ từ nào xuất hiện trong bản quét gốc—voilà, nó hoạt động.

## Các bước tiếp theo & Chủ đề liên quan

- **Cách OCR tài liệu** theo lô – bọc đoạn mã trên trong một vòng lặp `foreach` và xử lý toàn bộ thư mục.  
- **Chuyển đổi ảnh quét** sang các định dạng khác ngoài TIFF (PNG, JPEG) – API vẫn hoạt động; chỉ cần thay đổi phần mở rộng tệp.  
- **Trích xuất văn bản từ ảnh** để phân tích sâu hơn – đưa `result.Text` vào quy trình xử lý ngôn ngữ tự nhiên.  
- **Tối ưu kích thước PDF** – khám phá `PdfSaveOptions` để nén ảnh hơn hoặc nhúng phông chữ chỉ khi cần.

Hãy thử nghiệm các ý tưởng này, và bạn sẽ nhanh chóng trở thành người được nhắc tới cho bất kỳ yêu cầu “chuyển đổi bản quét này thành PDF có thể tìm kiếm” nào.

---

### TL;DR

Bây giờ bạn đã biết cách **tạo PDF có thể tìm kiếm** từ ảnh quét bằng Aspose OCR trong C#. Quy trình là: khởi tạo engine, tải ảnh, thực hiện OCR, và lưu với `PdfSearchable`. Điều chỉnh cài đặt ngôn ngữ, DPI và nén để xử lý các trường hợp đặc biệt, và bạn đã sẵn sàng **chuyển đổi ảnh quét**, **trích xuất văn bản từ ảnh**, và thậm chí **chuyển đổi TIFF sang PDF** ở quy mô lớn. Chúc lập trình vui vẻ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}