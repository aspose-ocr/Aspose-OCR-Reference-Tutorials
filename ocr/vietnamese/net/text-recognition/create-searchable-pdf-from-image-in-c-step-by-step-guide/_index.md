---
category: general
date: 2026-03-20
description: 'Tạo PDF có thể tìm kiếm nhanh chóng: chuyển ảnh sang PDF, trích xuất
  văn bản từ ảnh và thêm lớp văn bản ẩn để tìm kiếm đầy đủ.'
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- extract text from image
- pdf with hidden text
- scan image to pdf
language: vi
og_description: Tạo PDF có thể tìm kiếm trong C# bằng cách chuyển đổi hình ảnh sang
  PDF, trích xuất văn bản và nhúng lớp ẩn để tìm kiếm ngay lập tức.
og_title: Tạo PDF có thể tìm kiếm từ hình ảnh – Hướng dẫn C# đầy đủ
tags:
- Aspose
- C#
- OCR
- PDF generation
title: Tạo PDF có thể tìm kiếm từ hình ảnh trong C# – Hướng dẫn từng bước
url: /vi/net/text-recognition/create-searchable-pdf-from-image-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo PDF có thể tìm kiếm từ hình ảnh trong C# – Hướng dẫn toàn diện

Bạn đã bao giờ cần **tạo PDF có thể tìm kiếm** từ một hoá đơn đã quét nhưng không muốn gõ lại toàn bộ? Bạn không phải là người duy nhất. Trong nhiều quy trình văn phòng, việc chuyển một bản quét bitmap thành PDF có thể tìm kiếm là một vấn đề hàng ngày. Tin tốt? Chỉ với vài dòng C# và các thư viện OCR & PDF của Aspose, bạn có thể tự động hoá toàn bộ quá trình—không cần sao chép‑dán thủ công.

Trong tutorial này, chúng ta sẽ đi qua cách **chuyển đổi hình ảnh sang PDF**, trích xuất văn bản từ hình ảnh đó, và sau đó lớp văn bản ẩn để file cuối cùng hoạt động như một PDF gốc. Khi kết thúc, bạn sẽ có một phương pháp sẵn sàng để xây dựng **pdf with hidden text** cho bất kỳ tài liệu đã quét nào, dù là hoá đơn, hợp đồng, hay biên lai.

## Những gì bạn cần

- .NET 6.0 trở lên (mã sử dụng câu lệnh `using var`, vì vậy SDK mới sẽ dễ dàng hơn)
- Các gói NuGet Aspose.OCR và Aspose.Pdf (`Install-Package Aspose.OCR` và `Install-Package Aspose.Pdf`)
- Một file hình ảnh mẫu (PNG, JPG hoặc TIFF) chứa văn bản bạn muốn lập chỉ mục
- Visual Studio 2022 hoặc bất kỳ IDE nào bạn thích

> **Pro tip:** Nếu bạn đang làm việc với các bản quét đa trang, chỉ cần lặp lại quá trình cho mỗi hình ảnh – logic vẫn giống nhau.

---

## Bước 1 – Khởi tạo OCR Engine (Trích xuất Văn bản từ Hình ảnh)

Trước khi chúng ta có thể nhúng văn bản có thể tìm kiếm, cần phải đọc các ký tự từ ảnh. `OcrEngine` của Aspose thực hiện công việc nặng này.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Create the OCR engine and tell it which language to look for.
// English works for most invoices, but you can set Language.French, etc.
using var ocrEngine = new OcrEngine
{
    Language = Language.English
};
```

**Tại sao điều này quan trọng:** Khởi tạo engine với ngôn ngữ đúng sẽ cải thiện đáng kể độ chính xác. Nếu bỏ qua, OCR có thể nhận dạng sai số—điều bạn chắc chắn muốn tránh trong các tài liệu tài chính.

---

## Bước 2 – Tải Hình ảnh Đã Quét của Bạn (Chuyển Đổi Hình Ảnh sang PDF)

Bây giờ chúng ta đưa bitmap vào bộ nhớ. Aspose làm việc trực tiếp với `System.Drawing.Image`, vì vậy bất kỳ định dạng nào được .NET hỗ trợ đều được.

```csharp
using System.Drawing;

// Replace the path with the location of your scanned file.
var inputImage = Image.FromFile(@"C:\Docs\invoice.png");
```

Nếu bạn có quy trình **scan image to PDF** đã tạo ra một TIFF đa trang, chỉ cần thay đổi phần mở rộng file và lặp lại bước tải cho mỗi trang.

---

## Bước 3 – Chạy OCR và Ghi lại Văn bản Được Nhận Diện

Với hình ảnh đã sẵn sàng, chúng ta yêu cầu OCR engine thực hiện phép màu của nó.

```csharp
// Perform OCR – the result contains the raw text and confidence scores.
var ocrResult = ocrEngine.Recognize(inputImage);

// For debugging, you might want to see what was read.
Console.WriteLine("OCR Output:");
Console.WriteLine(ocrResult.Text);
```

**Trường hợp đặc biệt:** Nếu hình ảnh có độ phân giải thấp (< 300 dpi), độ tin cậy sẽ giảm. Hãy cân nhắc tăng kích thước hoặc quét lại ở DPI cao hơn trước khi đưa vào engine.

---

## Bước 4 – Tạo PDF và Đặt Hình ảnh Gốc làm Nền

Một **pdf with hidden text** vẫn cần biểu diễn hình ảnh quét. Chúng ta sẽ thêm hình ảnh làm nền trang.

```csharp
using Aspose.Pdf;

// Start a fresh PDF document.
var pdfDocument = new Document();

// Add a new page.
var pdfPage = pdfDocument.Pages.Add();

// Insert the image; it will fill the page by default.
pdfPage.Paragraphs.Add(new Aspose.Pdf.Image
{
    ImageInfo = new ImageInfo(@"C:\Docs\invoice.png")
});
```

**Lý do chúng ta dùng hình ảnh làm nền:** Người dùng vẫn có thể nhìn thấy bản quét gốc, bảo toàn chữ ký và con dấu, trong khi lớp văn bản ẩn cung cấp khả năng tìm kiếm.

---

## Bước 5 – Đặt Lớp Văn bản OCR lên trên như một Lớp Ẩn (PDF with Hidden Text)

Đây là phần quan trọng: chúng ta thêm một `TextFragment` nằm trên hình ảnh nhưng được đặt là ẩn. Aspose.Pdf làm cho việc này trở nên đơn giản.

```csharp
using Aspose.Pdf.Text;

// Create a text fragment from the OCR result.
var searchableText = new TextFragment(ocrResult.Text)
{
    // Position (0,0) aligns with the bottom‑left of the page.
    Position = new Position(0, 0),

    // Make the text invisible – it still participates in search.
    TextState = { Font = FontRepository.FindFont("Arial"), FontSize = 0.1f, IsHidden = true }
};

// Add the invisible text to the same page.
pdfPage.Paragraphs.Add(searchableText);
```

**Giải thích:** Đặt kích thước phông chữ rất nhỏ và đánh dấu fragment là hidden giữ cho đầu ra hình ảnh sạch sẽ, đồng thời đảm bảo lớp văn bản PDF chứa kết quả OCR. Các công cụ tìm kiếm và trình đọc PDF sẽ lập chỉ mục nó.

---

## Bước 6 – Lưu PDF có thể Tìm kiếm

Cuối cùng, ghi tài liệu ra đĩa.

```csharp
// Choose a destination path.
string outputPath = @"C:\Docs\invoice_searchable.pdf";

// Save the PDF. The file now contains both the image and searchable text.
pdfDocument.Save(outputPath);

Console.WriteLine($"Searchable PDF created at: {outputPath}");
```

Mở file kết quả trong Adobe Reader, nhấn **Ctrl + F**, gõ một từ bạn đã thấy trong hoá đơn, và bạn sẽ thấy kết quả được đánh dấu—mặc dù văn bản chưa từng hiển thị.

---

## Ví dụ Hoàn chỉnh (Tất cả các Bước Gộp lại)

Dưới đây là chương trình đầy đủ bạn có thể sao chép‑dán vào một ứng dụng console. Nó biên dịch và chạy ngay, với giả định các gói NuGet đã được cài và đường dẫn file đúng.

```csharp
// ------------------------------------------------------------
// Create Searchable PDF from Image – Complete C# Example
// ------------------------------------------------------------
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine
        using var ocrEngine = new OcrEngine
        {
            Language = Language.English
        };

        // 2️⃣ Load scanned image
        var inputImagePath = @"C:\Docs\invoice.png";
        var inputImage = Image.FromFile(inputImagePath);

        // 3️⃣ Perform OCR
        var ocrResult = ocrEngine.Recognize(inputImage);
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);

        // 4️⃣ Create PDF and add image as background
        var pdfDocument = new Document();
        var pdfPage = pdfDocument.Pages.Add();
        pdfPage.Paragraphs.Add(new Aspose.Pdf.Image
        {
            ImageInfo = new ImageInfo(inputImagePath)
        });

        // 5️⃣ Add invisible searchable text layer
        var searchableText = new TextFragment(ocrResult.Text)
        {
            Position = new Position(0, 0),
            TextState = { Font = FontRepository.FindFont("Arial"), FontSize = 0.1f, IsHidden = true }
        };
        pdfPage.Paragraphs.Add(searchableText);

        // 6️⃣ Save the searchable PDF
        var outputPath = @"C:\Docs\invoice_searchable.pdf";
        pdfDocument.Save(outputPath);
        Console.WriteLine($"✅ Searchable PDF saved to: {outputPath}");
    }
}
```

**Kết quả mong đợi:**  
- `invoice_searchable.pdf` trông giống hệt `invoice.png`.  
- Tìm kiếm văn bản hoạt động cho bất kỳ từ nào xuất hiện trong bản quét gốc.  
- Kích thước file chỉ tăng nhẹ (văn bản ẩn chỉ thêm vài kilobyte).

---

## Câu hỏi Thường gặp & Trường hợp Đặc biệt

### Tôi có thể xử lý nhiều trang trong một PDF không?
Chắc chắn rồi. Đặt logic OCR‑và‑PDF bên trong một vòng lặp `foreach (string imagePath in imageFiles)` và tạo một `Page` mới cho mỗi lần lặp. Lớp văn bản ẩn được thêm cho mỗi trang, vì vậy tìm kiếm hoạt động trên toàn bộ tài liệu.

### Nếu tài liệu của tôi chứa nhiều ngôn ngữ thì sao?
Đặt `ocrEngine.Language` thành `Language.Multilingual` hoặc khởi tạo các engine riêng cho từng đoạn ngôn ngữ. Aspose sẽ trả về kết quả hỗn hợp ngôn ngữ, sau đó bạn có thể đưa vào cùng một trang PDF.

### Làm sao để điều chỉnh DPI hoặc tỉ lệ hình ảnh?
Trước khi thêm hình ảnh vào PDF, bạn có thể thay đổi kích thước bằng `System.Drawing`:

```csharp
var resized = new Bitmap(inputImage, new Size(1240, 1754)); // A4 at 150 dpi
```

Sau đó truyền `resized` vào hàm khởi tạo ảnh PDF.

### Văn bản ẩn có thực sự không hiển thị trong mọi trình xem không?
Hầu hết các trình xem hiện đại tôn trọng cờ `IsHidden`. Nếu gặp trình xem vẫn hiển thị văn bản nhỏ, hãy giảm kích thước phông chữ hơn nữa (ví dụ `0.01f`) hoặc đặt màu văn bản thành hoàn toàn trong suốt bằng `TextState.FillColor = Color.Transparent`.

### Về bảo mật—tôi có thể đặt mật khẩu cho PDF không?
Có. Sau khi hoàn tất việc thêm nội dung, gọi:

```csharp
pdfDocument.Encrypt("ownerPwd", "userPwd", EncryptionAlgorithms.AES256);
```

Bây giờ PDF có thể tìm kiếm cũng tuân theo chính sách bảo mật của tổ chức bạn.

---

## Mẹo cho Triển khai Sẵn sàng Sản xuất

- **Xử lý hàng loạt:** Sử dụng `Parallel.ForEach` cho tập hợp hình ảnh lớn, nhưng chú ý tới các instance `OcrEngine` không thread‑safe—tạo một instance cho mỗi luồng.
- **Xử lý lỗi:** Bao bọc các lời gọi OCR trong try/catch; kiểm tra `ocrResult.IsRecognized` để bỏ qua các trang thất bại.
- **Ghi log:** Lưu giá trị `ocrResult.Confidence`; độ tin cậy thấp có thể cho thấy cần tiền xử lý ảnh (điều chỉnh góc, loại bỏ nhiễu).
- **Hiệu năng:** Tái sử dụng cùng một đối tượng `Document` cho tất cả các trang để tránh mở/đóng file liên tục.
- **Kiểm thử:** So sánh văn bản trích xuất từ PDF (`pdfDocument.Pages[1].ExtractText()`) với kết quả OCR để đảm bảo không bị cắt bớt.

---

## Kết luận

Chúng ta vừa chỉ cho bạn cách **tạo PDF có thể tìm kiếm** từ các hình ảnh đơn giản bằng C#. Bằng cách trích xuất văn bản với Aspose.OCR, lớp văn bản ẩn lên trang PDF, và lưu lại kết quả, bạn có được một tài liệu trông giống hệt bản quét gốc nhưng hoạt động như một PDF gốc. Kỹ thuật này bao phủ quy trình **convert image to PDF** truyền thống, thêm một **pdf with hidden text**, và giải quyết nhu cầu hàng ngày **scan image to PDF** mà bạn thực sự có thể tìm kiếm.

Sẵn sàng cho bước tiếp theo? Hãy thử mở rộng mã để xử lý hàng loạt thư mục biên lai, hoặc tích hợp vào một web API trả về PDF có thể tìm kiếm ngay lập tức. Bạn cũng có thể thử nghiệm với các phông chữ khác, thêm metadata, hoặc thậm chí nhúng điểm tin cậy OCR dưới dạng chú thích PDF để tạo dấu vết kiểm toán.

Nếu bạn thấy hướng dẫn này hữu ích, hãy cho nó một sao, chia sẻ với đồng nghiệp, hoặc để lại bình luận với các cải tiến của bạn. Chúc lập trình vui vẻ, và chúc các PDF của bạn luôn có thể tìm kiếm!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}