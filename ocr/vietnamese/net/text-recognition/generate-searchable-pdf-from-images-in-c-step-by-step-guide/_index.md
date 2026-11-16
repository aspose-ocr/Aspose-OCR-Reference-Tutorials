---
category: general
date: 2026-02-22
description: Tạo PDF có thể tìm kiếm và trích xuất văn bản từ hình ảnh bằng Aspose
  OCR. Tìm hiểu cách chuyển đổi hình ảnh sang PDF và xuất văn bản thuần trong một
  hướng dẫn duy nhất.
draft: false
keywords:
- generate searchable pdf
- extract text from image
- convert image to pdf
- output plain text
- convert scanned image pdf
language: vi
og_description: Tạo PDF có thể tìm kiếm từ hình ảnh đã quét bằng Aspose OCR. Hướng
  dẫn này cho thấy cách trích xuất văn bản từ hình ảnh, xuất văn bản thuần và chuyển
  đổi hình ảnh sang PDF.
og_title: Tạo PDF có thể tìm kiếm từ hình ảnh – Hướng dẫn C# toàn diện
tags:
- C#
- OCR
- PDF generation
- Aspose
title: Tạo PDF có thể tìm kiếm từ hình ảnh trong C# – Hướng dẫn từng bước
url: /vi/net/text-recognition/generate-searchable-pdf-from-images-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo PDF có thể tìm kiếm từ ảnh trong C# – Hướng dẫn đầy đủ

Bạn đã bao giờ cần **tạo PDF có thể tìm kiếm** từ một bức ảnh đã quét nhưng không biết bắt đầu từ đâu? Bạn không đơn độc—hầu hết các nhà phát triển đều gặp khó khăn này khi lần đầu tiếp xúc với OCR. Tin tốt là gì? Với Aspose OCR bạn có thể **trích xuất văn bản từ ảnh**, **xuất văn bản thuần**, và **chuyển ảnh sang PDF** chỉ trong vài dòng C#.

Trong hướng dẫn này, chúng ta sẽ đi qua toàn bộ quy trình, từ việc tải một tệp PNG đến lưu PDF có thể tìm kiếm và tệp văn bản thuần. Khi kết thúc, bạn sẽ có một đoạn mã có thể tái sử dụng và chèn vào bất kỳ dự án .NET nào. Không có phần thừa, chỉ có những gì cần thiết để hoàn thành công việc.

## Những gì bạn sẽ học

- Cách thiết lập **Aspose.OCR** trong một ứng dụng console .NET.  
- Sự khác biệt giữa chế độ **output plain text** và **searchable PDF**.  
- Cách **extract text from image** và ghi nó vào tệp `.txt`.  
- Cách **convert image to PDF** giữ nguyên bitmap gốc đồng thời thêm lớp văn bản ẩn.  
- Mẹo xử lý các lô lớn, các lỗi thường gặp, và nơi bạn có thể tinh chỉnh cài đặt để đạt độ chính xác cao hơn.

> **Yêu cầu trước** – Bạn cần .NET 6+ (hoặc .NET Framework 4.7+), Visual Studio 2022 (hoặc bất kỳ trình soạn thảo nào), và giấy phép Aspose OCR (hoặc bản dùng thử miễn phí). Không cần thư viện bên thứ ba nào khác.

![generate searchable pdf example](image-placeholder.png "Example of a generated searchable PDF")

## Bước 1: Cài đặt Aspose OCR và tạo Engine

Điều đầu tiên cần làm—thêm gói NuGet vào dự án của bạn:

```bash
dotnet add package Aspose.OCR
```

Bây giờ chúng ta có thể khởi tạo OCR engine và chỉ định ngôn ngữ đang xử lý. Tiếng Anh là mặc định, nhưng bạn có thể chuyển sang tiếng Pháp, Tây Ban Nha, v.v., bằng cách thay đổi enum `Language`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System.IO;

class Program
{
    static void Main()
    {
        // Initialize the OCR engine for English
        OcrEngine ocrEngine = new OcrEngine { Language = Language.English };
```

**Tại sao điều này quan trọng:** Engine chứa tất cả cấu hình—ngôn ngữ, định dạng đầu ra, và các cờ tiền xử lý tùy chọn. Thiết lập một lần và tái sử dụng sẽ tránh việc tạo một instance mới cho mỗi tệp, giảm tải tài nguyên.

## Bước 2: Trích xuất văn bản và lưu dưới dạng Plain Text

Nếu bạn chỉ cần các ký tự thô, chuyển engine sang `OutputFormat.Text`. Điều này yêu cầu Aspose OCR bỏ qua việc tạo PDF và trả về một chuỗi.

```csharp
        // Tell the engine to return plain text
        ocrEngine.OutputFormat = OutputFormat.Text;

        // Path to your source image (PNG, JPEG, BMP, etc.)
        string inputImagePath = @"YOUR_DIRECTORY/input.png";

        // Perform recognition – the result contains the extracted string
        OcrResult plainTextResult = ocrEngine.Recognize(Image.Load(inputImagePath));

        // Write the text to a .txt file
        string textOutputPath = @"YOUR_DIRECTORY/output.txt";
        File.WriteAllText(textOutputPath, plainTextResult.Text);
```

**Mẹo chuyên nghiệp:** `plainTextResult.Text` đã loại bỏ các ngắt dòng thuộc bố cục OCR. Nếu bạn cần giữ nguyên khoảng cách gốc, hãy kiểm tra `plainTextResult.TextBlocks` thay thế.

### Kết quả mong đợi

Mở `output.txt` và bạn sẽ thấy nội dung tương tự:

```
Hello, world!
This is a sample scanned document.
```

Đó là phần **output plain text** của tutorial—nhanh, nhẹ, và hoàn hảo cho các quy trình xử lý tiếp theo (ví dụ: lập chỉ mục).

## Bước 3: Chuyển sang chế độ Searchable PDF

Bây giờ chúng ta tạo một **searchable PDF**. Engine sẽ nhúng bitmap gốc và đặt lớp văn bản do OCR tạo ra phía dưới, cho phép tài liệu có thể tìm kiếm trong bất kỳ trình xem PDF nào.

```csharp
        // Change the output format to searchable PDF
        ocrEngine.OutputFormat = OutputFormat.SearchablePdf;

        // Recognize the same image again – this time we get PDF bytes
        OcrResult pdfResult = ocrEngine.Recognize(Image.Load(inputImagePath));

        // Save the PDF bytes to a file
        string pdfOutputPath = @"YOUR_DIRECTORY/output.pdf";
        File.WriteAllBytes(pdfOutputPath, pdfResult.RawData);
    }
}
```

**Tại sao chúng ta phải nhận dạng lại:** Engine OCR lưu cache ảnh cuối cùng, nhưng định dạng đầu ra quyết định dữ liệu nào được trả về. Thay đổi định dạng buộc một lần xử lý mới bao gồm lớp văn bản ẩn.

### PDF sẽ trông như thế nào

Mở `output.pdf` trong Adobe Reader hoặc bất kỳ trình xem nào và thử chọn văn bản. Bạn sẽ thấy có thể sao chép, tìm kiếm và đánh dấu nội dung—mặc dù hình ảnh hiển thị vẫn là bitmap gốc. Đó là đặc trưng của **convert scanned image pdf**.

## Bước 4: Xử lý nhiều tệp (Tùy chọn)

Trong thực tế, dự án hiếm khi chỉ làm việc với một ảnh duy nhất. Dưới đây là một vòng lặp nhanh xử lý mọi PNG trong một thư mục, tạo ra các tệp `.txt` và `.pdf` tương ứng.

```csharp
        string folder = @"YOUR_DIRECTORY";
        foreach (var file in Directory.GetFiles(folder, "*.png"))
        {
            // Plain‑text extraction
            ocrEngine.OutputFormat = OutputFormat.Text;
            var txtResult = ocrEngine.Recognize(Image.Load(file));
            File.WriteAllText(Path.ChangeExtension(file, ".txt"), txtResult.Text);

            // Searchable PDF generation
            ocrEngine.OutputFormat = OutputFormat.SearchablePdf;
            var pdfResult = ocrEngine.Recognize(Image.Load(file));
            File.WriteAllBytes(Path.ChangeExtension(file, ".pdf"), pdfResult.RawData);
        }
```

**Lưu ý trường hợp biên:** Ảnh lớn có thể làm hết bộ nhớ. Nếu gặp `OutOfMemoryException`, hãy cân nhắc giảm kích thước bằng `Image.Resize` trước khi nhận dạng, hoặc xử lý các tệp theo các lô nhỏ hơn.

## Bước 5: Tinh chỉnh độ chính xác OCR

Aspose OCR cung cấp một vài tùy chọn bạn có thể bật:

| Cài đặt | Chức năng | Khi nào nên dùng |
|---------|-----------|-------------------|
| `ocrEngine.PageSegmentationMode` | Kiểm soát cách engine chia ảnh thành các khối văn bản. | Hữu ích cho bố cục đa cột. |
| `ocrEngine.Deskew` | Tự động xoay các trang hơi nghiêng. | Tài liệu quét không được căn chỉnh hoàn hảo. |
| `ocrEngine.RemoveNoise` | Cố gắng làm sạch các điểm nhiễu và nhiễu nền. | Quét chất lượng thấp hoặc fax. |

Ví dụ:

```csharp
ocrEngine.Deskew = true;
ocrEngine.RemoveNoise = true;
```

Bật các tùy chọn này có thể làm tăng thời gian xử lý, nhưng cải thiện chất lượng **extract text from image** thường đáng giá.

## Bước 6: Kiểm tra đầu ra bằng chương trình

Đôi khi bạn cần xác nhận rằng PDF thực sự chứa văn bản có thể tìm kiếm (ví dụ: trong các bài kiểm tra tự động). Kiểm tra đơn giản nhất là xác nhận mảng byte PDF không rỗng và độ dài `RawData` lớn hơn kích thước ảnh.

```csharp
if (pdfResult.RawData.Length > Image.Load(inputImagePath).Data.Length)
{
    Console.WriteLine("Searchable PDF generated successfully!");
}
else
{
    Console.WriteLine("Warning: PDF may not contain hidden text.");
}
```

Đối với việc xác thực sâu hơn, bạn có thể dùng một thư viện PDF (như iTextSharp) để trích xuất luồng văn bản và so sánh với `plainTextResult.Text`.

## Những lỗi thường gặp & Cách tránh

- **Thiếu giấy phép** – Nếu không có giấy phép Aspose hợp lệ, thư viện sẽ chạy ở chế độ đánh giá, thêm watermark vào PDF. Đăng ký giấy phép sớm (`License license = new License(); license.SetLicense("Aspose.OCR.lic");`).  
- **Đường dẫn sai** – Việc hard‑code đường dẫn tuyệt đối hoạt động trên máy của bạn nhưng sẽ lỗi ở nơi khác. Hãy dùng `Path.Combine` với `AppDomain.CurrentDomain.BaseDirectory` để tăng tính di động.  
- **Định dạng ảnh không được hỗ trợ** – GIF và TIFF có nhiều khung cần xử lý đặc biệt (`Image.LoadMultiPage`). Chuyển chúng sang PNG/JPEG trước nếu bạn chỉ cần trang đầu tiên.  
- **Nút thắt hiệu năng** – Tạo lại `OcrEngine` trong vòng lặp tốn kém. Giữ một instance duy nhất và chỉ thay đổi `OutputFormat` như đã minh họa.

## Tóm tắt

Chúng ta đã đi qua toàn bộ quy trình **generate searchable PDF** từ ảnh đã quét bằng Aspose OCR:

1. Cài đặt gói NuGet và tạo một `OcrEngine`.  
2. Đặt `OutputFormat.Text` để **output plain text** và ghi vào tệp `.txt`.  
3. Chuyển sang `OutputFormat.SearchablePdf` để **convert image to PDF** với lớp văn bản ẩn.  
4. Lưu byte PDF và tùy chọn lặp qua thư mục để xử lý hàng loạt.  
5. Tinh chỉnh độ chính xác bằng các tùy chọn deskew, loại bỏ nhiễu, và phân đoạn trang.  

Tất cả đều gói gọn trong một chương trình tự chứa mà bạn có thể sao chép‑dán vào Visual Studio.

## Bạn có thể thử gì tiếp theo?

- **Xử lý batch** với giao diện UI (WinForms hoặc WPF) để người dùng kéo‑thả tệp.  
- **Phát hiện ngôn ngữ** – Aspose OCR có thể tự động phát hiện ngôn ngữ; thử `ocrEngine.Language = Language.AutoDetect`.  
- **Xử lý hậu kỳ** – Đưa văn bản đã trích xuất vào một chỉ mục tìm kiếm (ElasticSearch, Azure Cognitive Search) để truy xuất tài liệu ngay lập tức.  
- **Đầu ra thay thế** – Sử dụng `OutputFormat.Hocr` cho kết quả OCR dạng HTML, hữu ích cho preview trên web.

Hãy thoải mái thử nghiệm với các độ phân giải ảnh, chế độ màu và cài đặt OCR khác nhau. Bạn càng thử nghiệm, bạn sẽ càng hiểu rõ các đánh đổi giữa tốc độ và độ chính xác.

---

**Chúc lập trình vui!** Nếu gặp bất kỳ vấn đề nào, hãy để lại bình luận bên dưới hoặc tham khảo tài liệu Aspose OCR để tìm hiểu sâu hơn. Dự án tiếp theo của bạn—dù là lập hoá đơn, lưu trữ, hay xây dựng một kho kiến thức có thể tìm kiếm—giờ đã trở nên dễ dàng hơn rất nhiều.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}