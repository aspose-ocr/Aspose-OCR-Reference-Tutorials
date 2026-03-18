---
category: general
date: 2026-03-18
description: Cách chỉnh nghiêng ảnh và giảm nhiễu trong các tệp quét. Tìm hiểu cách
  tải ảnh từ tệp, trích xuất văn bản từ TIFF và nhận dạng văn bản từ ảnh bằng Aspose
  OCR.
draft: false
keywords:
- how to deskew image
- how to reduce noise
- recognize text from image
- load image from file
- extract text from tiff
language: vi
og_description: Cách chỉnh nghiêng ảnh nhanh chóng bằng Aspose OCR. Hướng dẫn này
  cho bạn biết cách giảm nhiễu, tải ảnh từ tệp và trích xuất văn bản từ TIFF trong
  C#.
og_title: Cách chỉnh nghiêng ảnh – Hướng dẫn OCR đầy đủ bằng C#
tags:
- OCR
- C#
- Image Processing
title: Cách chỉnh nghiêng ảnh và làm sạch các bản quét – Hướng dẫn C# đầy đủ
url: /vi/net/skew-angle-calculation/how-to-deskew-image-and-clean-up-scans-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Deskew Image – Hướng Dẫn Toàn Diện OCR C#

Bạn có bao giờ tự hỏi **cách deskew image** các tệp ảnh trông như được chụp từ một máy quét lắc lư không? Bạn không phải là người duy nhất. Hầu hết các nhà phát triển gặp phải vấn đề này khi tệp TIFF nguồn hơi lệch, và kết quả OCR trở nên lộn xộn. Tin tốt là gì? Chỉ với vài dòng C# bạn có thể làm thẳng hình ảnh, loại bỏ nền nhiễu, và lấy văn bản sạch, có thể tìm kiếm trực tiếp từ tệp.

Trong hướng dẫn này, chúng ta sẽ đi qua **cách giảm nhiễu**, **load image from file**, và cuối cùng **recognize text from image** bằng Aspose OCR. Khi kết thúc, bạn sẽ có thể **extract text from tiff** tài liệu mà không gặp khó khăn.

> **Mẹo chuyên nghiệp:** Nếu bạn đã sử dụng Aspose OCR cho các dự án khác, bạn có thể chèn các bộ lọc này mà không gặp bất kỳ rắc rối cấp phép nào.

## Những Gì Bạn Cần

- .NET 6 hoặc phiên bản mới hơn (mã cũng chạy trên .NET Core)  
- Gói NuGet Aspose.OCR (`Install-Package Aspose.OCR`)  
- Một tệp TIFF đã quét có hơi xoay hoặc nhiễu (chúng ta sẽ dùng `skewed_scanned_doc.tif` làm ví dụ)  
- Trình soạn thảo văn bản hoặc IDE (Visual Studio, VS Code, Rider – tùy sở thích)

Không cần thư viện bổ sung nào; các bộ lọc chúng ta sẽ sử dụng đã được tích hợp trong Aspose OCR.

## Bước 1 – Tạo OCR Engine (How to Deskew Image)

Điều đầu tiên bạn làm là khởi tạo một `OcrEngine`. Hãy nghĩ nó như bộ não sẽ đọc các ký tự cho bạn sau này.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Filters;

class PreprocessDemo
{
    static void Main()
    {
        // Initialize the OCR engine – this object holds all settings
        var ocrEngine = new OcrEngine();
```

Tại sao phải tạo engine từ đầu? Nó cung cấp một nơi duy nhất để gắn các bộ lọc tiền xử lý, gói ngôn ngữ và tùy chọn đầu ra. Nếu bạn bỏ qua bước này và gọi trực tiếp `OcrEngine.Recognize`, bạn sẽ mất cơ hội làm sạch ảnh trước, và đó chính là lý do chúng ta quan tâm đến việc deskew.

## Bước 2 – Thêm Bộ Lọc Deskew và Noise‑Reduction (How to Reduce Noise)

Now we attach two filters:

| Filter | Chức năng | Lý do quan trọng |
|--------|-----------|-------------------|
| `AutoDeskewFilter` | Phát hiện và sửa lỗi xoay | Làm thẳng các dòng văn bản để OCR engine có thể đọc chính xác |
| `NoiseReductionFilterV2` | Loại bỏ các đốm và hạt nền | Pixel sạch hơn đồng nghĩa với ít nhận dạng sai hơn |

```csharp
        // Add filters to improve OCR accuracy
        ocrEngine.Settings.Filters.Add(new AutoDeskewFilter());          // corrects rotation
        ocrEngine.Settings.Filters.Add(new NoiseReductionFilterV2());   // reduces background noise
```

Bạn có thể thay `NoiseReductionFilterV2` bằng phiên bản cũ hơn, nhưng thuật toán v2 xử lý máy quét hiện đại tốt hơn. Nếu tài liệu của bạn đã hoàn toàn thẳng, bộ lọc deskew sẽ chỉ truyền ảnh qua mà không thay đổi—không gây hại gì.

## Bước 3 – Load Image from File (Load Image from File)

Aspose cung cấp tiện ích `ImageStream.FromFile` giúp đọc nhiều định dạng, bao gồm TIFF, JPEG, PNG và BMP. Đây là cách chúng ta tải tệp vào bộ nhớ:

```csharp
        // Load the scanned image you want to preprocess
        var image = ImageStream.FromFile(@"YOUR_DIRECTORY/skewed_scanned_doc.tif");
```

Thay `YOUR_DIRECTORY` bằng đường dẫn thực tế trên máy của bạn. Nếu bạn làm việc với đường dẫn tương đối, hãy chắc chắn tệp nằm cạnh file thực thi hoặc đặt thư mục làm việc cho phù hợp.

## Bước 4 – Run OCR on the Preprocessed Image (Recognize Text from Image)

Với các bộ lọc đã được gắn và ảnh đã được tải, cuối cùng chúng ta yêu cầu Aspose đọc các ký tự:

```csharp
        // Perform OCR – the engine will automatically apply the filters first
        var ocrResult = ocrEngine.Recognize(image);
```

Trong nền, engine chạy thuật toán deskew, làm mịn nhiễu, và sau đó chạy bộ nhận dạng dựa trên mạng nơ-ron. Kết quả được đóng gói trong đối tượng `OcrResult` cung cấp văn bản thô, điểm tin cậy, và thậm chí các bounding box nếu bạn cần sau này.

## Bước 5 – Display hoặc Save Extracted Text (Extract Text from TIFF)

Để demo nhanh, chúng ta chỉ in văn bản ra console, nhưng bạn có thể ghi vào file, cơ sở dữ liệu, hoặc đưa vào quy trình downstream.

```csharp
        // Show the recognized text in the console
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Kết quả mong đợi** (ví dụ, sẽ khác tùy tài liệu của bạn):

```
Invoice #12345
Date: 2023‑04‑01
Total: $1,250.00
Thank you for your business!
```

Nếu kết quả vẫn chứa ký tự rối, hãy kiểm tra lại TIFF gốc không quá thấp độ phân giải (khuyến nghị tối thiểu 300 dpi) và ngôn ngữ đã được đặt đúng trong `ocrEngine.Settings.Language`.

## Ví dụ Hoàn Chỉnh (All Steps in One Place)

Dưới đây là chương trình hoàn chỉnh bạn có thể sao chép‑dán vào một dự án console mới và chạy ngay lập tức.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Filters;

class PreprocessDemo
{
    static void Main()
    {
        // 1️⃣ Create OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Add preprocessing filters
        ocrEngine.Settings.Filters.Add(new AutoDeskewFilter());          // deskew image
        ocrEngine.Settings.Filters.Add(new NoiseReductionFilterV2());   // reduce noise

        // 3️⃣ Load the image file (TIFF, JPEG, etc.)
        var image = ImageStream.FromFile(@"YOUR_DIRECTORY/skewed_scanned_doc.tif");

        // 4️⃣ Recognize text – filters run automatically
        var ocrResult = ocrEngine.Recognize(image);

        // 5️⃣ Output the extracted text
        Console.WriteLine(ocrResult.Text);
    }
}
```

Lưu file dưới tên `Program.cs`, chạy `dotnet run`, và bạn sẽ thấy văn bản đã được làm sạch xuất hiện trong terminal.

## Câu Hỏi Thường Gặp & Trường Hợp Đặc Biệt

### Nếu TIFF của tôi có nhiều trang thì sao?

Aspose OCR có thể xử lý ảnh đa trang bằng cách lặp qua `image.GetPages()` (hoặc dùng `image.Pages`). Mỗi trang trả về một `OcrResult` riêng. Kết hợp chúng bằng `StringBuilder` nếu bạn cần một chuỗi duy nhất.

### Bộ lọc deskew có hoạt động trên ảnh xoay mạnh không?

Nó xử lý các góc xoay tới khoảng ±15°. Nếu vượt quá, bạn có thể cần xoay ảnh thủ công bằng thư viện đồ họa (ví dụ, `System.Drawing` hoặc `SkiaSharp`) trước khi đưa vào Aspose.

### Làm sao để cải thiện độ chính xác cho văn bản không phải tiếng Anh?

Đặt ngôn ngữ một cách rõ ràng:

```csharp
ocrEngine.Settings.Language = Language.English; // or Language.French, etc.
```

Bạn cũng có thể tải các gói ngôn ngữ tùy chỉnh nếu các gói có sẵn không hỗ trợ bảng chữ cái của bạn.

### Tôi có thể chạy điều này trên Linux không?

Chắc chắn. Aspose OCR hỗ trợ đa nền tảng; chỉ cần đảm bảo các phụ thuộc gốc có sẵn (thường không có đối với phiên bản .NET thuần). Dùng `dotnet publish -r linux-x64` để tạo binary tự chứa.

## Bonus: Visualizing the Deskewed Image

Nếu bạn muốn xem ảnh đã được chỉnh sửa trước khi OCR, bạn có thể lưu lại lên đĩa:

```csharp
// After OCR, the filtered image is stored in ocrEngine.Settings.FiltersResult
var corrected = ocrEngine.Settings.FiltersResult;
corrected.Save(@"output/deskewed_cleaned.tif");
```

![ví dụ cách deskew image](https://example.com/deskew-demo.png "ví dụ cách deskew image")

*Văn bản thay thế hình ảnh:* **ví dụ cách deskew image** – hiển thị trước/sau của một TIFF bị xoay được chỉnh sửa bằng AutoDeskewFilter.

## Kết Luận

Chúng ta đã đề cập đến **cách deskew image** các tệp, **cách giảm nhiễu**, và toàn bộ quy trình để **recognize text from image**, **load image from file**, và **extract text from tiff** bằng Aspose OCR trong C#. Điều quan trọng? Chỉ cần thêm hai bộ lọc tiền xử lý có thể biến một bản quét lắc lư, nhiễu thành tài liệu sắc nét, có thể tìm kiếm mà không cần công cụ bên ngoài.

Sẵn sàng cho bước tiếp theo? Hãy thử thay `AutoDeskewFilter` bằng `AutoRotateFilter` nếu tài liệu của bạn bị lộn ngược, hoặc thử nghiệm `ContrastEnhancementFilter` cho các bản in mờ. Mẫu tương tự—engine → filters → load → recognize—áp dụng cho mọi trường hợp Aspose OCR, vì vậy bạn có thể tái sử dụng khung này cho PDF, PNG, hoặc thậm chí ảnh chụp bằng camera.

Chúc lập trình vui vẻ, và chúc OCR của bạn luôn chính xác!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}