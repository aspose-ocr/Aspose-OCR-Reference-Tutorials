---
category: general
date: 2026-05-28
description: Tạo PDF có thể tìm kiếm bằng Aspose OCR trong C#. Tìm hiểu cách chạy
  OCR trên PDF, nhận dạng văn bản PDF và chuyển PDF đã quét bằng OCR thành PDF có
  thể tìm kiếm.
draft: false
keywords:
- create searchable pdf
- run ocr on pdf
- recognize text pdf
- ocr scanned pdf
- aspose ocr pdf
language: vi
og_description: Tạo PDF có thể tìm kiếm bằng Aspose OCR trong C#. Hãy làm theo hướng
  dẫn từng bước này để chạy OCR trên PDF, nhận dạng văn bản PDF và xử lý các tệp PDF
  đã quét bằng OCR.
og_title: Tạo PDF có thể tìm kiếm với Aspose OCR – Chạy OCR trên PDF
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Create searchable PDF using Aspose OCR in C#. Learn how to run OCR
    on PDF, recognize text PDF, and turn an OCR scanned PDF into a searchable PDF.
  headline: Create Searchable PDF with Aspose OCR – Run OCR on PDF
  type: TechArticle
- description: Create searchable PDF using Aspose OCR in C#. Learn how to run OCR
    on PDF, recognize text PDF, and turn an OCR scanned PDF into a searchable PDF.
  name: Create Searchable PDF with Aspose OCR – Run OCR on PDF
  steps:
  - name: Multiple Languages (OCR Scanned PDF)
    text: 'If your source PDF contains both English and Spanish text, combine languages:'
  - name: Password‑Protected PDFs
    text: 'When dealing with secured PDFs, supply the password before calling `Recognize`:'
  - name: Controlling Image Quality
    text: 'Higher DPI yields better OCR results but consumes more memory. Adjust the
      DPI if you notice garbled characters:'
  - name: License vs. Evaluation Mode
    text: 'In evaluation mode a watermark appears on each page. To remove it, apply
      your license before any OCR call:'
  - name: What’s Next?
    text: '- Explore the **aspose ocr pdf** API further: extract plain text, export
      to DOCX, or generate searchable PDFs in bulk. - Combine the searchable PDF output
      with Aspose.PDF to add bookmarks or watermarks. - Experiment with different
      DPI settings or custom OCR dictionaries for niche fonts.'
  type: HowTo
tags:
- Aspose
- OCR
- PDF
- C#
title: Tạo PDF có thể tìm kiếm với Aspose OCR – Chạy OCR trên PDF
url: /vi/net/text-recognition/create-searchable-pdf-with-aspose-ocr-run-ocr-on-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo PDF có thể tìm kiếm với Aspose OCR – Chạy OCR trên PDF

Bạn đã bao giờ cần **tạo các tệp PDF có thể tìm kiếm** từ một đống tài liệu đã quét chưa? Bạn không phải là người duy nhất. Trong nhiều quy trình làm việc văn phòng, điều duy nhất ngăn cản bạn có một kho lưu trữ hoàn toàn có thể tìm kiếm là một vài dòng mã chạy OCR trên các trang PDF.  

Trong hướng dẫn này, chúng ta sẽ đi qua một ví dụ hoàn chỉnh, sẵn sàng chạy, cho bạn thấy chính xác cách **tạo PDF có thể tìm kiếm** bằng thư viện Aspose OCR cho .NET. Khi kết thúc, bạn sẽ biết cách *chạy OCR trên PDF*, *nhận dạng văn bản PDF*, và biến một *PDF đã quét bằng OCR* thành phiên bản có thể tìm kiếm mà không cần dịch vụ bên thứ ba nào.

> **Tiền đề** – Một .NET SDK mới (khuyến nghị 6.0+), giấy phép Aspose.OCR cho .NET hợp lệ (hoặc khóa đánh giá tạm thời), và một tệp PDF bạn muốn xử lý.

![Create searchable PDF diagram](alt="Sơ đồ minh họa quy trình tạo PDF có thể tìm kiếm bằng Aspose OCR")  

---

## Những gì hướng dẫn này bao phủ

- Cài đặt thư viện Aspose OCR trong dự án C#.  
- Tải một PDF nguồn (bất kỳ số lượng trang nào).  
- Cấu hình engine để xuất **PDF có thể tìm kiếm**.  
- Chạy quá trình OCR và lưu kết quả.  
- Mẹo xử lý tài liệu đa trang, lựa chọn ngôn ngữ, và các lỗi thường gặp.  

Nếu bạn làm theo từng bước, cuối cùng bạn sẽ có một tệp có thể mở trong Adobe Reader, nhấn **Ctrl + F**, và ngay lập tức tìm kiếm bất kỳ từ nào xuất hiện trong bản quét gốc.

---

## Bước 1: Cài đặt Aspose OCR cho .NET

Trước khi viết bất kỳ mã nào, thêm gói NuGet vào dự án của bạn:

```bash
dotnet add package Aspose.OCR
```

> **Mẹo chuyên nghiệp:** Sử dụng cờ `--version` để khóa vào phiên bản ổn định mới nhất (ví dụ, `Aspose.OCR 23.10`). Điều này đảm bảo khả năng tương thích với .NET 6 và các phiên bản mới hơn.

---

## Bước 2: Tạo một thể hiện OcrEngine

Trái tim của quá trình là `OcrEngine`. Hãy nghĩ nó như bộ não đọc hình ảnh và xuất ra văn bản. Khởi tạo nó rất đơn giản:

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

namespace PdfSearchableDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Instantiate the OCR engine
            var ocrEngine = new OcrEngine();
```

Đối tượng `OcrEngine` sẽ giữ cả luồng ảnh đầu vào và cấu hình cho biết Aspose muốn đầu ra như thế nào.

---

## Bước 3: Tải PDF nguồn (Chạy OCR trên PDF)

Aspose OCR có thể tiếp nhận trực tiếp một PDF; nó sẽ trích xuất mỗi trang dưới dạng hình ảnh bên trong. Thay thế đường dẫn placeholder bằng vị trí của tài liệu đã quét của bạn:

```csharp
            // Step 3: Load the source PDF – this is where we *run OCR on PDF*
            string inputPath = @"C:\Docs\handbook.pdf";
            ocrEngine.Image = ImageStream.FromFile(inputPath);
```

> **Tại sao cách này hoạt động:** Phương thức `ImageStream.FromFile` tự động phát hiện định dạng PDF và chuẩn bị một biểu diễn raster cho OCR. Không cần bước chuyển đổi bổ sung.

---

## Bước 4: Cấu hình Định dạng Đầu ra và Ngôn ngữ

Ở đây chúng ta cho Aspose biết chúng ta muốn gì trả về. Đặt `OutputFormat` thành `SearchablePdf` chỉ thị cho engine nhúng văn bản đã nhận dạng phía sau các hình ảnh trang gốc, tạo ra một **PDF có thể tìm kiếm**. Bạn cũng có thể chọn ngôn ngữ để cải thiện độ chính xác — tiếng Anh là mặc định, nhưng bạn có thể chuyển sang tiếng Pháp, tiếng Đức, v.v.

```csharp
            // Step 4: Choose output format and language
            ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf; // creates searchable PDF
            ocrEngine.Configuration.Language = Language.English;               // *recognize text PDF* in English
```

Nếu bạn cần xử lý tài liệu song ngữ, bạn có thể kết hợp các ngôn ngữ bằng cách sử dụng các cờ enum `Language`.

---

## Bước 5: Chạy Quá trình OCR – Nhận dạng Văn bản PDF

Bây giờ công việc nặng nề diễn ra. Phương thức `Recognize` quét mọi trang, trích xuất glyphs, và xây dựng một luồng PDF nội bộ chứa cả hình ảnh gốc và lớp văn bản vô hình. Đây là bước chúng ta *nhận dạng văn bản PDF*.

```csharp
            // Step 5: Execute OCR – this *recognizes text PDF* and builds the searchable stream
            ocrEngine.Recognize();
```

> **Câu hỏi thường gặp:** *Nếu PDF có 200 trang thì sao?*  
> Engine xử lý các trang tuần tự và truyền luồng kết quả, vì vậy mức tiêu thụ bộ nhớ vẫn ở mức vừa phải. Tuy nhiên, đối với các tệp cực lớn, bạn có thể muốn tăng cài đặt `MemoryLimit` trong `ocrEngine.Configuration`.

---

## Bước 6: Lưu PDF có thể tìm kiếm

Cuối cùng, ghi đầu ra ra đĩa. Phương thức `Save` ghi luồng nội bộ vào một tệp mới mà bạn có thể mở bằng bất kỳ trình xem PDF nào.

```csharp
            // Step 6: Save the searchable PDF to disk
            string outputPath = @"C:\Docs\handbook_searchable.pdf";
            ocrEngine.Save(outputPath);

            Console.WriteLine($"Searchable PDF created at: {outputPath}");
        }
    }
}
```

Chạy chương trình (`dotnet run`) và xem console xác nhận việc tạo tệp. Mở `handbook_searchable.pdf` và thử tìm kiếm một từ bạn biết có trong bản quét gốc – bạn sẽ thấy kết quả ngay lập tức.

---

## Xử lý Các Trường hợp Cạnh và Kịch bản Nâng cao

### Nhiều Ngôn ngữ (PDF đã quét bằng OCR)

Nếu PDF nguồn của bạn chứa cả tiếng Anh và tiếng Tây Ban Nha, hãy kết hợp các ngôn ngữ:

```csharp
ocrEngine.Configuration.Language = Language.English | Language.Spanish;
```

Aspose OCR sẽ chuyển đổi từ điển ngay lập tức, tăng độ chính xác cho tài liệu đa ngôn ngữ.

### PDF có Mật khẩu Bảo vệ

Khi làm việc với PDF được bảo mật, cung cấp mật khẩu trước khi gọi `Recognize`:

```csharp
ocrEngine.Image = ImageStream.FromFile(inputPath, "MySecretPassword");
```

Nếu mật khẩu sai, `Recognize` sẽ ném ra `InvalidPasswordException`; bắt ngoại lệ này cho phép bạn yêu cầu người dùng nhập lại mật khẩu đúng.

### Kiểm soát Chất lượng Hình ảnh

DPI cao hơn cho kết quả OCR tốt hơn nhưng tiêu tốn nhiều bộ nhớ hơn. Điều chỉnh DPI nếu bạn nhận thấy ký tự bị lỗi:

```csharp
ocrEngine.Configuration.Dpi = 300; // default is 200
```

### Giấy phép vs. Chế độ Đánh giá

Trong chế độ đánh giá, một watermark sẽ xuất hiện trên mỗi trang. Để loại bỏ, áp dụng giấy phép của bạn trước bất kỳ lời gọi OCR nào:

```csharp
var license = new License();
license.SetLicense(@"C:\Aspose\Aspose.OCR.lic");
```

---

## Mẹo Chuyên nghiệp cho Sản xuất

- **Xử lý hàng loạt:** Đặt logic cốt lõi trong một vòng `foreach` lặp qua danh sách các PDF. Giải phóng `OcrEngine` sau mỗi tệp để giải phóng tài nguyên gốc.  
- **Ghi log:** Sử dụng `ocrEngine.Configuration.Logger` để ghi lại các thống kê OCR chi tiết (ví dụ, ký tự nhận dạng được mỗi giây). Điều này vô giá khi khắc phục lỗi độ chính xác thấp.  
- **Tối ưu hiệu năng:** Đối với máy chủ đa lõi, khởi tạo các đối tượng `OcrEngine` riêng cho mỗi luồng; thư viện an toàn với luồng khi mỗi thể hiện được cô lập.  
- **Xử lý lỗi:** Luôn bao quanh `Recognize` và `Save` bằng các khối `try/catch`. Các ngoại lệ thường gặp bao gồm `FileNotFoundException`, `OutOfMemoryException`, và `UnsupportedFormatException`.

---

## Ví dụ Hoàn chỉnh (Sẵn sàng Sao chép‑Dán)

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

namespace PdfSearchableDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Apply license (optional – removes evaluation watermark)
            // var license = new License();
            // license.SetLicense(@"C:\Aspose\Aspose.OCR.lic");

            // 1️⃣ Create OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Load PDF – this is where we *run OCR on PDF*
            string inputPath = @"C:\Docs\handbook.pdf";
            ocrEngine.Image = ImageStream.FromFile(inputPath);

            // 3️⃣ Configure output as searchable PDF and set language
            ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf;
            ocrEngine.Configuration.Language = Language.English;

            // 4️⃣ Run OCR – *recognize text PDF*
            ocrEngine.Recognize();

            // 5️⃣ Save the searchable PDF
            string outputPath = @"C:\Docs\handbook_searchable.pdf";
            ocrEngine.Save(outputPath);

            Console.WriteLine($"Searchable PDF created at: {outputPath}");
        }
    }
}
```

**Kết quả mong đợi** (console):

```
Searchable PDF created at: C:\Docs\handbook_searchable.pdf
```

Mở tệp kết quả, nhấn **Ctrl + F**, và bạn sẽ có thể định vị bất kỳ từ nào xuất hiện trong các trang quét gốc. Đó là phép màu của việc biến một *PDF đã quét bằng OCR* thành một **PDF có thể tìm kiếm**.

---

## Kết luận

Chúng ta vừa trình diễn cách **tạo PDF có thể tìm kiếm** bằng Aspose OCR cho .NET, bao quát mọi thứ từ cài đặt gói đến xử lý PDF đa ngôn ngữ và PDF có mật khẩu bảo vệ. Bằng cách làm theo các bước này, bạn có thể tin cậy *chạy OCR trên PDF*, *nhận dạng văn bản PDF*, và chuyển đổi bất kỳ *PDF đã quét bằng OCR* nào thành tài sản hoàn toàn có thể tìm kiếm.

### Tiếp theo là gì?

- Khám phá thêm API **aspose ocr pdf**: trích xuất văn bản thuần, xuất ra DOCX, hoặc tạo PDF có thể tìm kiếm hàng loạt.  
- Kết hợp đầu ra PDF có thể tìm kiếm với Aspose.PDF để thêm dấu trang hoặc watermark.  
- Thử nghiệm các cài đặt DPI khác nhau hoặc từ điển OCR tùy chỉnh cho các phông chữ đặc thù.

Hãy thoải mái tùy chỉnh mẫu, tích hợp nó vào quy trình quản lý tài liệu của bạn, hoặc đặt câu hỏi trong phần bình luận. Chúc lập trình vui vẻ, và tận hưởng việc biến những bản quét không đọc được thành vàng có thể tìm kiếm!

## Các Hướng dẫn Liên quan

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Cómo hacer OCR a PDF en .NET con Aspose.OCR](/ocr/spanish/net/text-recognition/recognize-pdf/)
- [كيفية إجراء OCR لملف PDF في .NET باستخدام Aspose.OCR](/ocr/arabic/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}