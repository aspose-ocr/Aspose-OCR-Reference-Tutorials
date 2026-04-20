---
category: general
date: 2026-02-28
description: Tạo PDF có thể tìm kiếm từ tệp TIFF đa trang trong C#. Hướng dẫn này
  cho thấy cách chuyển đổi hình ảnh thành PDF có thể tìm kiếm với một ví dụ OCR đầy
  đủ bằng C#.
draft: false
keywords:
- create searchable pdf
- image to searchable pdf
- convert tiff to pdf
- c# ocr example
- c# image to pdf
language: vi
og_description: Tạo PDF có thể tìm kiếm từ tệp TIFF bằng Aspose.OCR. Thực hiện ví
  dụ OCR C# từng bước để chuyển hình ảnh thành PDF có thể tìm kiếm.
og_title: Tạo PDF có thể tìm kiếm bằng C# – Chuyển ảnh sang PDF OCR
tags:
- OCR
- PDF
- C#
- Aspose
title: Tạo PDF có thể tìm kiếm bằng C# – Chuyển ảnh sang PDF bằng OCR
url: /vi/net/text-recognition/create-searchable-pdf-in-c-image-to-pdf-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo PDF có thể tìm kiếm trong C# – Chuyển ảnh sang PDF OCR

Bạn đã bao giờ cần **tạo PDF có thể tìm kiếm** từ một tài liệu đã quét nhưng không chắc bắt đầu từ đâu chưa? Bạn không phải là người duy nhất. Trong nhiều quy trình văn phòng, một PDF có thể tìm kiếm là sự khác biệt giữa một tệp vô ích và một kho lưu trữ có thể tìm kiếm.  

Trong hướng dẫn này, chúng tôi sẽ hướng dẫn qua một **c# ocr example** hoàn chỉnh giúp chuyển một tệp TIFF đa trang thành PDF có thể tìm kiếm, tất cả bằng Aspose.OCR. Khi kết thúc, bạn sẽ biết chính xác cách **image to searchable pdf**, cách **convert tiff to pdf**, và sẽ có một đoạn mã sẵn sàng chạy mà bạn có thể chèn vào bất kỳ dự án .NET nào.

## Những gì bạn sẽ học

* Cách cài đặt và tham chiếu Aspose.OCR trong dự án C#.
* Các bước chính xác để tải một TIFF, thiết lập ngôn ngữ và gọi `RecognizeToPdf`.
* Lý do mỗi bước quan trọng – từ quản lý bộ nhớ đến việc chọn ngôn ngữ.
* Mẹo xử lý tài liệu lớn, khắc phục các vấn đề OCR thường gặp, và mở rộng giải pháp sang các định dạng ảnh khác.

**Prerequisites** – một .NET SDK mới (4.6+ hoặc .NET Core 3.1+), Visual Studio (hoặc IDE yêu thích của bạn), và giấy phép Aspose.OCR (bản dùng thử miễn phí đủ cho việc thử nghiệm). Không cần thư viện bên ngoài nào khác.

---

## Tạo PDF có thể tìm kiếm – Tổng quan

Ở mức độ tổng quan, quy trình trông như sau:

1. **Initialize** `OcrEngine`.  
2. **Load** hình ảnh nguồn (một TIFF trong trường hợp của chúng tôi).  
3. **Configure** cài đặt ngôn ngữ để tăng độ chính xác.  
4. **Run** OCR và **save** kết quả trực tiếp dưới dạng PDF có thể tìm kiếm.  

Chỉ vậy thôi. Aspose API thực hiện phần công việc nặng, vì vậy bạn không cần phải ghép nối các thư viện OCR và PDF riêng biệt.

---

## Bước 1: Cài đặt Aspose.OCR và Thiết lập Dự án của Bạn

Đầu tiên, thêm gói NuGet Aspose.OCR:

```bash
dotnet add package Aspose.OCR
```

Hoặc, nếu bạn thích Package Manager Console trong Visual Studio:

```powershell
Install-Package Aspose.OCR
```

Sau khi gói được khôi phục, mở file dự án của bạn và xác nhận tham chiếu:

```xml
<ItemGroup>
  <PackageReference Include="Aspose.OCR" Version="23.10.0" />
</ItemGroup>
```

> **Pro tip:** Sử dụng phiên bản ổn định mới nhất (kiểm tra trang web Aspose) để nhận các bản sửa lỗi và các gói ngôn ngữ mới nhất.

---

## Bước 2: Chuyển TIFF sang PDF – Tải ảnh

Bây giờ chúng ta sẽ tải TIFF mà bạn muốn làm có thể tìm kiếm. Phương thức `Image.Load` của Aspose hỗ trợ TIFF đa trang ngay từ đầu.

```csharp
using Aspose.OCR;
using System.Drawing;

// Load the multi‑page TIFF. Replace the path with your actual file.
using var tiffImage = Image.Load(@"YOUR_DIRECTORY/input.tif");
```

> **Why this matters:** Tải ảnh trong một khối `using` đảm bảo các tài nguyên không quản lý được giải phóng kịp thời—rất quan trọng khi xử lý tài liệu lớn.

---

## Bước 3: Ảnh sang PDF có thể tìm kiếm – Cấu hình Engine OCR

Trước khi chạy OCR, chúng ta sẽ cho engine biết ngôn ngữ mong đợi. Tiếng Anh hoạt động cho hầu hết các trường hợp, nhưng bạn có thể thay thế bằng bất kỳ giá trị enum `OcrLanguage` nào.

```csharp
// Create the OCR engine instance
var ocrEngine = new OcrEngine();

// (Optional) Specify language for better accuracy
ocrEngine.Language = OcrLanguage.English;
```

> **Expert note:** Chọn ngôn ngữ đúng sẽ giảm đáng kể các nhận dạng sai. Nếu bạn có nhiều ngôn ngữ hỗn hợp, bạn có thể kết hợp chúng bằng toán tử `|`, ví dụ, `OcrLanguage.English | OcrLanguage.French`.

---

## Bước 4: Ví dụ OCR C# – Nhận dạng và Lưu

Khi engine đã sẵn sàng, gọi `RecognizeToPdf`. Phương thức này ghi PDF có thể tìm kiếm trực tiếp lên đĩa, nhúng một lớp văn bản ẩn phía sau ảnh gốc.

```csharp
// Define the output path for the searchable PDF
string outputPdfPath = @"YOUR_DIRECTORY/output.pdf";

// Perform OCR and write the searchable PDF
ocrEngine.RecognizeToPdf(tiffImage, outputPdfPath);
```

Sau khi dòng này thực thi, `output.pdf` sẽ chứa các trang TIFF gốc cộng với lớp văn bản ẩn mà bất kỳ trình đọc PDF nào cũng có thể tìm kiếm.

---

## Bước 5: Ảnh C# sang PDF – Xác minh Kết quả

Hãy xác nhận mọi thứ đã hoạt động. Mở PDF đã tạo trong Adobe Reader (hoặc bất kỳ trình xem nào) và thử tìm kiếm một từ mà bạn biết có trong TIFF nguồn.

```csharp
Console.WriteLine("Searchable PDF created at: " + outputPdfPath);
```

Nếu việc tìm kiếm trả về kết quả, bạn đã thành công **create searchable pdf** từ một ảnh. Nếu không, hãy kiểm tra lại cài đặt ngôn ngữ hoặc chất lượng của TIFF nguồn.

---

## Ví dụ Hoạt động Đầy đủ

Kết hợp tất cả các phần lại, đây là một ứng dụng console tự chứa mà bạn có thể biên dịch và chạy:

```csharp
using Aspose.OCR;
using System.Drawing;

class SearchablePdfDemo
{
    static void Main()
    {
        // Step 1: Initialize OCR engine
        var ocrEngine = new OcrEngine();

        // Step 2: Load the multi‑page TIFF
        using var tiffImage = Image.Load(@"YOUR_DIRECTORY/input.tif");

        // Step 3: (Optional) Set language for better accuracy
        ocrEngine.Language = OcrLanguage.English;

        // Step 4: Convert the image to a searchable PDF
        string outputPdfPath = @"YOUR_DIRECTORY/output.pdf";
        ocrEngine.RecognizeToPdf(tiffImage, outputPdfPath);

        // Step 5: Inform the user
        System.Console.WriteLine("Searchable PDF created at: " + outputPdfPath);
    }
}
```

**Expected output** (trong console):

```
Searchable PDF created at: C:\MyFolder\output.pdf
```

Mở `output.pdf` và bạn sẽ có thể gõ bất kỳ từ nào từ TIFF gốc vào ô tìm kiếm của trình xem và thấy các kết quả được đánh dấu.

---

![Create searchable PDF example](placeholder-image.png){: .align-center alt="ví dụ tạo pdf có thể tìm kiếm"}

*Ảnh chụp màn hình trên cho thấy một PDF có thể tìm kiếm được mở trong trình xem với lớp văn bản ẩn đang hoạt động.*

---

## Câu hỏi Thường gặp & Trường hợp Đặc biệt

### Nếu TIFF của tôi rất lớn (hàng trăm trang)?

Aspose.OCR truyền các trang một lần, nhưng bạn vẫn có thể gặp giới hạn bộ nhớ. Hãy cân nhắc xử lý TIFF theo lô:

```csharp
for (int i = 0; i < tiffImage.PageCount; i++)
{
    using var singlePage = tiffImage.ExtractPage(i);
    ocrEngine.RecognizeToPdf(singlePage, $"page_{i}.pdf");
}
```

Sau đó, hợp nhất các PDF từng trang bằng một thư viện PDF (ví dụ, Aspose.PDF).

### Tôi có thể xuất ra định dạng khác, như DOCX có thể tìm kiếm không?

Có—sử dụng `RecognizeToDocument` thay vì `RecognizeToPdf`. API tương tự như phương thức PDF, chỉ cần thay đổi phần mở rộng tệp đích.

### Làm sao để xử lý các ngôn ngữ khác ngoài tiếng Anh?

Thay thế `OcrLanguage.English` bằng enum phù hợp, ví dụ `OcrLanguage.Spanish`. Bạn cũng có thể kết hợp các ngôn ngữ:

```csharp
ocrEngine.Language = OcrLanguage.English | OcrLanguage.German;
```

### Còn các PDF được bảo vệ bằng mật khẩu thì sao?

Sau bước OCR, bạn có thể mở PDF đã tạo bằng Aspose.PDF và áp dụng mã hóa:

```csharp
var pdfDoc = new Aspose.Pdf.Document(outputPdfPath);
pdfDoc.Encrypt("ownerPassword", "userPassword", 
    Aspose.Pdf.Permissions.All, Aspose.Pdf.EncryptionAlgorithms.AES256);
pdfDoc.Save(outputPdfPath);
```

---

## Tổng kết

Chúng tôi đã bao phủ mọi thứ bạn cần để **create searchable PDF** từ các ảnh TIFF bằng C#. Bắt đầu từ việc cài đặt Aspose.OCR, tải ảnh, cấu hình ngôn ngữ, chạy OCR, và cuối cùng xác minh đầu ra có thể tìm kiếm, bạn hiện có một **c# ocr example** vững chắc mà bạn có thể điều chỉnh cho các định dạng khác.  

Nếu bạn đã sẵn sàng tiến xa hơn, hãy thử:

* **Convert TIFF to PDF** cho các kho lưu trữ không thể tìm kiếm (chỉ cần bỏ qua bước OCR).  
* Thử nghiệm với **image to searchable pdf**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}