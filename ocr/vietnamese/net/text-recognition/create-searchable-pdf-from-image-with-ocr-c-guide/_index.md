---
category: general
date: 2026-03-18
description: Tạo PDF có thể tìm kiếm bằng Aspose OCR trong C#. Chuyển đổi hình ảnh
  sang PDF, thêm lớp văn bản OCR và ghi các byte PDF vào tệp trong vài bước đơn giản.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- recognize text from image
- add ocr text layer
- write pdf bytes to file
language: vi
og_description: Tạo PDF có thể tìm kiếm nhanh chóng với Aspose OCR trong C#. Tìm hiểu
  cách chuyển đổi hình ảnh sang PDF, thêm lớp văn bản OCR và ghi dữ liệu PDF ra tệp.
og_title: Tạo PDF có thể tìm kiếm từ hình ảnh – Hướng dẫn OCR C# nhanh
tags:
- OCR
- PDF
- C#
- Aspose
title: Tạo PDF có thể tìm kiếm từ hình ảnh với OCR – Hướng dẫn C#
url: /vi/net/text-recognition/create-searchable-pdf-from-image-with-ocr-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo PDF có thể tìm kiếm từ Hình ảnh với OCR – Hướng dẫn C#

Bạn đã bao giờ cần **tạo PDF có thể tìm kiếm** từ một bức ảnh đã quét chưa? Với Aspose OCR, bạn có thể thực hiện chỉ trong vài dòng code, không cần thư viện nặng. Trong hướng dẫn này, chúng ta sẽ **chuyển đổi hình ảnh sang PDF**, thêm một **lớp văn bản OCR** lên trên, và cuối cùng **ghi dữ liệu PDF ra file** để bạn có được một tài liệu PDF/A‑2b tuân chuẩn mà người dùng thực sự có thể tìm kiếm.

Nếu bạn thắc mắc tại sao phải tốn công tạo PDF có thể tìm kiếm thay vì chỉ một file hình ảnh đơn thuần, hãy nghĩ đến trải nghiệm người dùng: PDF có thể tìm kiếm cho phép người dùng sao chép, chọn và lập chỉ mục văn bản—rất hữu ích cho lưu trữ, tài liệu pháp lý, hoặc bất kỳ quy trình nào cần trích xuất văn bản sau này. Hãy bắt đầu.

## Những gì bạn cần

- .NET 6 hoặc phiên bản mới hơn (mã cũng chạy trên .NET Framework 4.7+)
- Gói NuGet Aspose.OCR (`Aspose.OCR` phiên bản 23.10 hoặc mới hơn)
- Một ảnh raster (`.png`, `.jpg`, v.v.) mà bạn muốn chuyển thành PDF có thể tìm kiếm
- Kiến thức cơ bản về C#—không cần gì phức tạp, chỉ cần những kiến thức nền tảng

Chỉ vậy thôi. Không cần công cụ bên ngoài, không cần bộ chuyển đổi thêm. Tất cả công việc nặng được xử lý bởi engine OCR của Aspose.

## Tạo PDF có thể tìm kiếm – Tổng quan

Trước khi chúng ta đi sâu vào mã, hãy phác thảo quy trình:

1. **Instantiate** engine OCR – đối tượng này biết cách đọc văn bản từ hình ảnh.  
2. **Load** ảnh nguồn – chúng ta sẽ truyền một `ImageStream` cho engine.  
3. **Configure** tùy chọn lưu PDF/A‑2b – điều này yêu cầu Aspose nhúng văn bản đã nhận dạng dưới dạng lớp ẩn.  
4. **Run** OCR và **capture** dữ liệu PDF thu được.  
5. **Write** các byte đó ra đĩa, tạo ra file PDF có thể tìm kiếm cuối cùng.

Mỗi bước trong số đó tương ứng trực tiếp với một hoặc hai dòng C#, khiến toàn bộ quy trình cảm giác như một script nhỏ thay vì một dự án lớn.

## Bước 1: Chuyển đổi hình ảnh sang PDF – Tải ảnh

Điều đầu tiên cần làm: chúng ta phải cung cấp cho engine OCR một thứ để đọc. Trợ giúp `ImageStream.FromFile` tải file vào một stream mà Aspose có thể xử lý.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Output;
using System;

// 1️⃣ Load the source image you want to turn into a searchable PDF
ImageStream image = ImageStream.FromFile("YOUR_DIRECTORY/input.png");
```

> **Mẹo:** Giữ độ phân giải ảnh ở mức 300 dpi hoặc cao hơn; độ chính xác OCR giảm đáng kể khi quét ở độ phân giải thấp.

## Bước 2: Nhận dạng văn bản từ ảnh và Thêm lớp văn bản OCR

Bây giờ chúng ta tạo engine OCR và yêu cầu nó nhận dạng văn bản. Phép màu xảy ra khi chúng ta kết hợp kết quả nhận dạng với `PdfSaveOptions` có `IncludeTextLayer = true`. Cờ này buộc Aspose nhúng các ký tự đã trích xuất dưới dạng lớp văn bản ẩn, chính vì vậy PDF trở nên có thể tìm kiếm.

```csharp
// 2️⃣ Create the OCR engine instance
OcrEngine ocrEngine = new OcrEngine();

// 3️⃣ Set up PDF/A‑2b save options – includes the hidden text layer
PdfSaveOptions pdfSaveOptions = new PdfSaveOptions
{
    PdfCompliance = PdfCompliance.PdfA2b, // ensures PDF/A‑2b compliance
    IncludeTextLayer = true               // this is the key for searchable PDFs
};
```

Tại sao lại là PDF/A‑2b? Đó là định dạng lưu trữ tiêu chuẩn ISO, đảm bảo bảo quản lâu dài và, quan trọng đối với chúng ta, buộc PDF chứa lớp văn bản có thể tìm kiếm. Nếu bạn không cần tuân thủ lưu trữ, bạn có thể bỏ `PdfCompliance` hoàn toàn, nhưng việc giữ lại không tốn gì cả.

## Bước 3: Ghi dữ liệu PDF ra file – Lưu kết quả

Khi engine đã sẵn sàng và các tùy chọn đã được thiết lập, chúng ta chạy quá trình nhận dạng và ngay lập tức yêu cầu Aspose cung cấp PDF dưới dạng `byte[]`. Sau đó, chúng ta ghi các byte này ra đĩa bằng `File.WriteAllBytes`. Đơn giản, nhưng mạnh mẽ.

```csharp
// 4️⃣ Perform OCR on the image and get the PDF bytes
byte[] pdfBytes = ocrEngine.Recognize(image).Save(pdfSaveOptions);

// 5️⃣ Write the PDF/A‑2b file to the output location
System.IO.File.WriteAllBytes("YOUR_DIRECTORY/output.pdf", pdfBytes);
Console.WriteLine("PDF/A‑2b file created – you now have a searchable PDF!");
```

Dòng `Console.WriteLine` đó là tùy chọn, nhưng nó cung cấp phản hồi ngay lập tức khi bạn chạy chương trình từ terminal.

## Ví dụ hoàn chỉnh hoạt động

Kết hợp tất cả lại, đây là chương trình đầy đủ, sẵn sàng chạy. Sao chép‑dán nó vào một dự án console mới, thay thế `YOUR_DIRECTORY` bằng đường dẫn thực tế, và nhấn **F5**.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Output;
using System;

class PdfA2bDemo
{
    static void Main()
    {
        // Step 1: Load the source image
        ImageStream image = ImageStream.FromFile("YOUR_DIRECTORY/input.png");

        // Step 2: Create OCR engine and configure PDF/A‑2b options
        OcrEngine ocrEngine = new OcrEngine();
        PdfSaveOptions pdfSaveOptions = new PdfSaveOptions
        {
            PdfCompliance = PdfCompliance.PdfA2b,
            IncludeTextLayer = true
        };

        // Step 3: Recognize and save as PDF bytes
        byte[] pdfBytes = ocrEngine.Recognize(image).Save(pdfSaveOptions);

        // Step 4: Write the bytes to a searchable PDF file
        System.IO.File.WriteAllBytes("YOUR_DIRECTORY/output.pdf", pdfBytes);
        Console.WriteLine("PDF/A‑2b file created.");
    }
}
```

### Kết quả mong đợi

- Một file có tên `output.pdf` xuất hiện trong thư mục bạn đã chỉ định.  
- Mở nó bằng Adobe Acrobat Reader hoặc bất kỳ trình xem PDF nào và thử chọn văn bản—nếu bạn có thể sao chép từ, bạn đã **tạo thành công PDF có thể tìm kiếm**.  
- Tài liệu cũng sẽ vượt qua các công cụ kiểm tra PDF/A‑2b vì chúng ta đã sử dụng cờ tuân thủ phù hợp.

## Các câu hỏi thường gặp & Trường hợp đặc biệt

**Nếu ảnh của tôi chứa nhiều trang thì sao?**  
Đóng mỗi trang trong một `ImageStream` riêng và đưa chúng lần lượt vào `OcrEngine`. Aspose sẽ tự động nối các trang lại thành một PDF duy nhất.

**Tôi có thể thay đổi ngôn ngữ OCR không?**  
Chắc chắn. Đặt `ocrEngine.Language = Language.English;` (hoặc bất kỳ ngôn ngữ nào được hỗ trợ) trước khi gọi `Recognize`.

**Về việc sử dụng bộ nhớ cho các file lớn thì sao?**  
Nếu bạn đang xử lý các bản quét quy mô gigabyte, hãy cân nhắc stream kết quả trực tiếp tới một `FileStream` thay vì giữ toàn bộ `byte[]` trong bộ nhớ:

```csharp
using (var file = new FileStream("output.pdf", FileMode.Create))
{
    ocrEngine.Recognize(image).Save(pdfSaveOptions, file);
}
```

**Tôi có cần giấy phép không?**  
Aspose cung cấp bản dùng thử miễn phí không có watermark. Đối với sử dụng trong môi trường sản xuất, mua giấy phép để loại bỏ banner đánh giá và mở khóa đầy đủ tính năng.

## Mẹo để cải thiện độ chính xác OCR

- **Tiền xử lý** ảnh: chỉnh thẳng, loại bỏ nhiễu, và tăng độ tương phản.  
- **Sử dụng định dạng không mất dữ liệu** như PNG; các artefact nén JPEG có thể làm rối engine.  
- **Tránh nền màu**; nền trắng đơn sẽ cho kết quả tốt nhất.

## Các bước tiếp theo

Bây giờ bạn đã có thể **tạo PDF có thể tìm kiếm**, bạn có thể muốn:

- **Xử lý hàng loạt** một thư mục ảnh bằng `Directory.GetFiles`.  
- **Trích xuất văn bản ẩn** sau này bằng API `PdfDocument` để lập chỉ mục.  
- **Kết hợp OCR với chữ ký số** để tạo các kho lưu trữ có khả năng phát hiện giả mạo.  

Tất cả những điều này dựa trên cùng một mẫu cốt lõi mà chúng ta đã đề cập: tải, nhận dạng, cấu hình, lưu.

---

*Bạn đã sẵn sàng biến các kho lưu trữ đã quét thành PDF có thể tìm kiếm chưa? Lấy mã nguồn, chỉ vào các ảnh của bạn, và để Aspose thực hiện công việc nặng. Chúc lập trình vui vẻ!*

![Ví dụ tạo PDF có thể tìm kiếm](/images/create-searchable-pdf.png "Minh họa PDF có thể tìm kiếm được tạo từ một hình ảnh")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}