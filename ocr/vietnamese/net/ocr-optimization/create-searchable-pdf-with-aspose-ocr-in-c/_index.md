---
category: general
date: 2026-04-01
description: Tạo PDF có thể tìm kiếm trong C# bằng Aspose OCR – học cách chuyển đổi
  PDF đã quét, thêm OCR vào PDF và kích hoạt tăng tốc GPU để có kết quả nhanh chóng.
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- convert pdf to searchable
- add OCR to pdf
- enable GPU acceleration
language: vi
og_description: Tạo PDF có thể tìm kiếm trong C# nhanh chóng—chuyển đổi PDF đã quét,
  thêm OCR vào PDF và kích hoạt tăng tốc GPU để xử lý hiệu suất cao.
og_title: Tạo PDF có thể tìm kiếm bằng Aspose OCR trong C#
tags:
- Aspose OCR
- C#
- PDF processing
title: Tạo PDF có thể tìm kiếm bằng Aspose OCR trong C#
url: /vi/net/ocr-optimization/create-searchable-pdf-with-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo PDF có thể tìm kiếm với Aspose OCR trong C#

Bạn đã bao giờ cần **tạo PDF có thể tìm kiếm** từ một đống tài liệu đã quét chưa? Bạn không phải là người duy nhất—nhiều nhóm gặp khó khăn trong việc chuyển các PDF chỉ có hình ảnh thành tài sản có thể tìm kiếm bằng văn bản. Tin tốt? Với Aspose OCR, bạn có thể **chuyển đổi PDF đã quét** thành phiên bản có thể tìm kiếm đầy đủ chỉ trong vài dòng mã C#. Trong hướng dẫn này, chúng tôi sẽ đi qua toàn bộ quy trình, từ việc thêm OCR vào PDF đến việc **bật tăng tốc GPU** để tăng tốc độ.

Chúng tôi cũng sẽ chỉ cho bạn cách **chuyển đổi pdf sang định dạng có thể tìm kiếm**, thảo luận tại sao bạn có thể muốn **thêm OCR vào PDF**, và cung cấp các mẹo thực tế để xử lý các lô lớn. Khi hoàn thành, bạn sẽ có một ứng dụng console sẵn sàng chạy, tạo ra PDF có thể tìm kiếm mà bạn có thể đưa vào bất kỳ hệ thống quản lý tài liệu nào.

---

## Những gì bạn cần

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

- **.NET 6.0** trở lên (API cũng hoạt động với .NET Framework, nhưng .NET 6+ là lựa chọn tối ưu).
- Gói NuGet **Aspose.OCR for .NET** (`Install-Package Aspose.OCR`).
- Một tệp PDF đã quét (chỉ có hình ảnh) để làm đầu vào.
- Tùy chọn: một máy tính tương thích GPU với CUDA® được cài đặt nếu bạn muốn **bật tăng tốc GPU**.

Đó là tất cả—không cần engine OCR nặng, không cần dịch vụ bên ngoài. Mọi thứ chạy cục bộ.

---

## Tạo PDF có thể tìm kiếm – Tổng quan các bước

Dưới đây là luồng công việc cấp cao mà chúng ta sẽ theo:

1. **Khởi tạo engine OCR** – cho Aspose biết ngôn ngữ cần tìm và có bật GPU hay không.
2. **Chỉ định engine tới PDF đã quét của bạn** – định nghĩa đường dẫn đầu vào và đầu ra.
3. **Chạy quá trình chuyển đổi** – Aspose thực hiện công việc nặng và ghi ra PDF có thể tìm kiếm.
4. **Xác minh kết quả** – mở tệp đầu ra và thử tìm kiếm văn bản.

Mỗi bước được chia thành một phần riêng, vì vậy bạn có thể chọn lọc những phần quan trọng nhất đối với mình.

---

## Chuyển đổi PDF đã quét sang PDF có thể tìm kiếm

Điều đầu tiên bạn cần làm là tạo một thể hiện của `OcrEngine`. Đối tượng này là động cơ chính đọc các ảnh raster bên trong PDF và trích xuất văn bản.

```csharp
using Aspose.OCR;
using System;

class PdfSearchableDemo
{
    static void Main()
    {
        // Step 1: Create and configure the OCR engine
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.English,
            // Optional: enable GPU for faster processing
            UseGpuAcceleration = true
        };

        // Step 2: Specify the input scanned PDF and the output searchable PDF paths
        string sourcePdfPath = @"C:\Docs\input.pdf";
        string searchablePdfPath = @"C:\Docs\output.pdf";

        // Step 3: Convert the scanned PDF into a searchable PDF
        ocrEngine.ConvertToSearchablePdf(sourcePdfPath, searchablePdfPath);

        // Step 4: Notify the user where the searchable PDF was saved
        Console.WriteLine("Searchable PDF created at: " + searchablePdfPath);
    }
}
```

**Tại sao cách này hoạt động:** `ConvertToSearchablePdf` đọc từng trang, chạy OCR trên nội dung raster, sau đó nhúng một lớp văn bản vô hình phía sau hình ảnh gốc. Kết quả trông giống hệt tài liệu đã quét ban đầu, nhưng bây giờ bạn có thể sao chép, chọn và tìm kiếm văn bản.

---

## Thêm OCR vào PDF bằng Aspose

Nếu bạn đã có một PDF và chỉ muốn **thêm OCR vào PDF** mà không cần chuyển đổi toàn bộ tệp, bạn có thể gọi cùng một phương thức—Aspose coi thao tác này là “thêm OCR”. Đoạn mã ở trên đã làm điều đó, nhưng dưới đây là một biến thể nhanh cho phép bạn xử lý nhiều tệp trong một vòng lặp:

```csharp
string[] pdfFiles = Directory.GetFiles(@"C:\Docs\Scanned", "*.pdf");
foreach (var file in pdfFiles)
{
    string output = Path.Combine(@"C:\Docs\Searchable", Path.GetFileNameWithoutExtension(file) + "_searchable.pdf");
    ocrEngine.ConvertToSearchablePdf(file, output);
    Console.WriteLine($"Processed {Path.GetFileName(file)} → {Path.GetFileName(output)}");
}
```

**Mẹo:** Giữ lại cùng một thể hiện `OcrEngine` cho toàn bộ lô. Tạo lại mỗi lần sẽ gây tốn tài nguyên không cần thiết, đặc biệt khi bạn **bật tăng tốc GPU**.

---

## Bật tăng tốc GPU để OCR nhanh hơn

Tăng tốc GPU có thể cắt giảm vài phút cho một lô lớn. Aspose OCR tận dụng NVIDIA CUDA ở phía sau, vì vậy bạn chỉ cần bật một cờ boolean:

```csharp
ocrEngine.UseGpuAcceleration = true; // set to false if no compatible GPU
```

**Khi nào nên dùng:** Nếu bạn đang xử lý các PDF lớn hơn 10 MB hoặc hơn vài chục tệp, GPU thường mang lại tăng tốc 2‑3×. Trên một laptop thông thường không có GPU hỗ trợ CUDA, hãy để `false`—thư viện sẽ tự động quay lại CPU.

**Cạm bẫy phổ biến:** Quên cài đặt đúng phiên bản driver CUDA có thể gây ra ngoại lệ thời chạy (`CudaException`). Đảm bảo driver của bạn khớp với phiên bản Aspose yêu cầu (kiểm tra ghi chú phát hành trên trang NuGet).

---

## Ví dụ hoàn chỉnh (Tất cả các bước kết hợp)

Dưới đây là một ứng dụng console tự chứa mà bạn có thể sao chép‑dán vào một dự án .NET mới. Nó bao gồm các chú thích hữu ích, xử lý lỗi, và một bước xác minh cuối cùng in ra số trang đã xử lý.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class PdfSearchableDemo
{
    static void Main()
    {
        try
        {
            // 1️⃣ Initialize OCR engine – English language, GPU on if available
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.English,
                UseGpuAcceleration = true // set to false on non‑GPU machines
            };

            // 2️⃣ Define input and output paths
            string sourcePdfPath = @"C:\Docs\input.pdf";
            string searchablePdfPath = @"C:\Docs\output.pdf";

            // 3️⃣ Perform the conversion – this creates a searchable PDF
            ocrEngine.ConvertToSearchablePdf(sourcePdfPath, searchablePdfPath);

            // 4️⃣ Simple verification – count pages in the new file
            int pageCount = new Aspose.Pdf.Facades.PdfFileInfo(searchablePdfPath).NumberOfPages;
            Console.WriteLine($"✅ Searchable PDF created at: {searchablePdfPath}");
            Console.WriteLine($"📄 The new file contains {pageCount} pages.");

            // 5️⃣ Optional: open the file automatically (Windows only)
            // System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo(searchablePdfPath) { UseShellExecute = true });
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"❌ Oops! Something went wrong: {ex.Message}");
        }
    }
}
```

**Kết quả mong đợi**

```
✅ Searchable PDF created at: C:\Docs\output.pdf
📄 The new file contains 12 pages.
```

Mở `output.pdf` trong bất kỳ trình xem PDF nào và thử gõ một từ xuất hiện trong các hình ảnh đã quét. Nếu văn bản được tô sáng, bạn đã **tạo pdf có thể tìm kiếm** thành công.

---

## Các vấn đề thường gặp và Mẹo chuyên nghiệp

| Vấn đề | Nguyên nhân | Cách khắc phục / Tránh |
|-------|-------------|------------------------|
| **GPU không được phát hiện** | Thiếu hoặc không khớp driver CUDA. | Cài đặt phiên bản driver được liệt kê trong ghi chú phát hành của Aspose; đặt `UseGpuAcceleration = false` làm dự phòng. |
| **Ngôn ngữ sai** | OCR mặc định là tiếng Anh; các ngôn ngữ khác cần thiết lập rõ ràng. | Đặt `Language = Language.Spanish` (hoặc bất kỳ enum hỗ trợ nào) trước khi chuyển đổi. |
| **PDF lớn gây OutOfMemory** | Engine tải toàn bộ trang vào bộ nhớ. | Xử lý PDF theo từng khối bằng `ocrEngine.PageRange = new PageRange(1, 5)` cho mỗi lô. |
| **Tệp đầu ra bị hỏng** | Thư mục đích không có quyền ghi. | Chạy ứng dụng với quyền nâng cao hoặc chọn đường dẫn có thể ghi. |
| **Lớp văn bản không tìm kiếm được** | Trình xem cache phiên bản cũ. | Làm mới trình xem PDF hoặc mở lại tệp. |

**Mẹo chuyên nghiệp:** Khi bạn phải làm việc với hỗn hợp PDF đã quét và PDF gốc, hãy kiểm tra cờ `HasText` của mỗi trang (`PdfPageInfo.HasText`) trước khi chạy OCR. Điều này tiết kiệm CPU và tránh OCR kép trên các trang đã có thể tìm kiếm.

---

## Xác minh kết quả bằng mã (Tùy chọn)

Nếu bạn muốn tự động xác minh, Aspose.PDF có thể trích xuất văn bản ẩn:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Load the searchable PDF
Document doc = new Document(searchablePdfPath);
TextAbsorber absorber = new TextAbsorber();
doc.Pages.Accept(absorber);
string extracted = absorber.Text;

// Simple check – does the word "Invoice" appear?
if (extracted.Contains("Invoice"))
    Console.WriteLine("✅ OCR succeeded – 'Invoice' found.");
else
    Console.WriteLine("⚠️ OCR may have missed some text.");
```

Đoạn mã này chứng minh rằng bạn thực sự **chuyển đổi pdf sang định dạng có thể tìm kiếm**, không chỉ phủ lên một hình ảnh.

---

## Ví dụ hình ảnh

![Ví dụ đầu ra PDF có thể tìm kiếm](https://example.com/images/searchable-pdf.png "Tạo PDF có thể tìm kiếm bằng Aspose OCR")

*Văn bản thay thế:* **ví dụ tạo pdf có thể tìm kiếm** hiển thị trước (đã quét) và sau (có thể tìm kiếm).

---

## Các bước tiếp theo & Chủ đề liên quan

- **Xử lý hàng loạt:** Đóng gói vòng lặp từ phần “Thêm OCR vào PDF” trong một Windows Service hoặc Azure Function để chạy vào ban đêm.
- **Hỗ trợ ngôn ngữ nâng cao:** Khám phá `ocrEngine.Language = Language.Multilingual` cho tài liệu chứa nhiều script khác nhau.
- **Dọn dẹp sau OCR:** Sử dụng `TextFragmentAbsorber` của Aspose.PDF để sửa các lỗi OCR thường gặp (ví dụ, “0” vs “O”).
- **Bảo mật**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}