---
category: general
date: 2026-01-15
description: Hướng dẫn OCR bằng C# cho thấy cách nhận dạng văn bản từ hình ảnh, trích
  xuất văn bản từ hoá đơn và chuyển đổi hình ảnh thành văn bản bằng Aspose OCR trên
  GPU.
draft: false
keywords:
- c# ocr tutorial
- recognize text from image
- extract text from invoice
- convert image to text
- load image for ocr
language: vi
og_description: Hướng dẫn OCR C# dạy bạn cách nhận dạng văn bản từ hình ảnh, trích
  xuất văn bản từ hoá đơn và chuyển đổi hình ảnh thành văn bản bằng Aspose OCR trên
  GPU.
og_title: hướng dẫn OCR c# – Nhận dạng văn bản nhanh bằng GPU
tags:
- OCR
- C#
- Aspose
- GPU
title: Hướng dẫn OCR C# – Nhận dạng văn bản từ hình ảnh với tốc độ tăng tốc GPU
url: /vi/net/ocr-optimization/c-ocr-tutorial-recognize-text-from-image-with-gpu-accelerati/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – Nhận dạng Văn bản từ Hình ảnh với Tăng tốc GPU

Bạn đã bao giờ cần một **c# ocr tutorial** thực sự hoàn thành công việc mà không phải thử‑và‑sai vô tận? Có thể bạn đang nhìn vào một hoá đơn độ phân giải cao và tự hỏi làm thế nào để **extract text from invoice** trong vòng vài giây. Tin tốt là bạn không cần phải tự phát minh lại bánh xe—Aspose.OCR cung cấp cho bạn một API sạch, tăng tốc bằng GPU, thực hiện phần công việc nặng cho bạn.

Trong hướng dẫn này, chúng tôi sẽ đi qua một ví dụ hoàn chỉnh, có thể chạy được, cho thấy cách **recognize text from image** các tệp, **convert image to text**, và xử lý các vấn đề thường gặp nhất. Khi kết thúc, bạn sẽ có một chương trình tự chứa có thể đọc bất kỳ hình ảnh tài liệu nào, từ biên lai đến hợp đồng đã quét, và xuất ra văn bản sạch, có thể tìm kiếm.

## Những gì bạn sẽ học

- Cách cài đặt và tham chiếu gói NuGet Aspose.OCR.
- Cách cấu hình engine OCR để chạy trên GPU với hiệu năng cực nhanh.
- Cách đúng để **load image for ocr** bằng `OcrImage.FromFile`.
- Cách gọi `Recognize` với ngôn ngữ mong muốn và lấy kết quả.
- Mẹo xử lý PDF đa trang, ảnh quét độ tương phản thấp, và xử lý lỗi.

Không cần kinh nghiệm trước với Aspose; chỉ cần một môi trường phát triển .NET hoạt động (Visual Studio 2022 hoặc VS Code) và một GPU vừa phải (ngay cả GPU tích hợp Intel cũng đủ).

---

## Bước 1 – Cài đặt Aspose.OCR và Chuẩn bị Dự án của Bạn

Đầu tiên: bạn cần thư viện Aspose.OCR. Cách dễ nhất là qua NuGet.

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** Nếu bạn đang nhắm tới .NET 6 hoặc mới hơn, gói sẽ tự động tải các binary GPU gốc cho Windows, Linux và macOS. Không cần sao chép DLL thêm.

Sau khi đã thêm gói, mở tệp dự án của bạn (`*.csproj`) và kiểm tra tham chiếu:

```xml
<ItemGroup>
  <PackageReference Include="Aspose.OCR" Version="23.12.0" />
</ItemGroup>
```

Bây giờ bạn đã có mọi thứ cần thiết để bắt đầu viết mã.

## Bước 2 – Tạo một OCR Engine hỗ trợ GPU (c# ocr tutorial)

Trọng tâm của **c# ocr tutorial** là `OcrEngine`. Bằng cách đặt `Engine = Engine.Gpu` chúng ta nói với Aspose sử dụng card đồ họa thay vì CPU.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

namespace GpuOcrDemo
{
    class Program
    {
        static void Main()
        {
            // Initialize the OCR engine with GPU acceleration.
            var ocrEngine = new OcrEngine
            {
                Engine = Engine.Gpu // GPU acceleration is selected; the library auto‑detects the device.
            };

            // The rest of the steps are broken out into separate methods for clarity.
            string imagePath = @"YOUR_DIRECTORY/high_res_invoice.png";
            PerformOcr(ocrEngine, imagePath);
        }
    }
}
```

> **Why GPU?** GPU có thể xử lý hàng nghìn pixel song song, giảm thời gian OCR từ giây xuống phần nghìn giây trên các ảnh lớn, DPI cao.

## Bước 3 – Tải ảnh cho OCR (load image for ocr)

Việc tải ảnh đúng cách quan trọng hơn bạn nghĩ. `OcrImage.FromFile` hỗ trợ PNG, JPEG, BMP, TIFF và thậm chí các trang PDF. Nó cũng đọc DPI của ảnh, ảnh hưởng đến độ chính xác.

```csharp
static void PerformOcr(OcrEngine engine, string filePath)
{
    // Step 3: Load the image you want to recognize.
    // The FromFile method automatically detects the format.
    var image = OcrImage.FromFile(filePath);

    // Optional: Pre‑process the image for better results.
    // For example, you can increase contrast or convert to grayscale.
    image = ImagePreprocessor.AdjustContrast(image, 1.2);
    image = ImagePreprocessor.ConvertToGrayscale(image);
    
    // Continue to recognition...
    RecognizeAndDisplay(engine, image);
}
```

**Lưu ý:** Nếu bạn đang làm việc với PDF, bạn có thể trích xuất mỗi trang dưới dạng `OcrImage` và đưa chúng vào một một.

## Bước 4 – Nhận dạng Văn bản từ Ảnh (recognize text from image)

Bây giờ phép màu xảy ra. Chúng ta yêu cầu engine nhận dạng văn bản tiếng Anh, nhưng bạn có thể truyền bất kỳ ngôn ngữ nào được Aspose hỗ trợ (Tiếng Tây Ban Nha, Đức, Trung Quốc, v.v.).

```csharp
static void RecognizeAndDisplay(OcrEngine engine, OcrImage image)
{
    // Step 4: Perform OCR on the image using the desired language.
    var result = engine.Recognize(image, Language.English);

    // Step 5: Output the recognized text.
    Console.WriteLine("=== OCR RESULT ===");
    Console.WriteLine(result.Text);
}
```

Thuộc tính `result.Text` chứa chuỗi thuần. Nếu bạn cần điểm tin cậy cho mỗi từ, bạn có thể kiểm tra `result.Regions`.

### Kết quả Dự kiến

```
=== OCR RESULT ===
Invoice #12345
Date: 2025‑12‑01
Total: $1,234.56
Thank you for your business!
```

Nếu ảnh bị mờ, bạn có thể thấy các ký tự rối—đây là nơi tiền xử lý từ Bước 3 giúp ích.

## Bước 5 – Trích xuất Văn bản từ Hoá đơn – Ví dụ Thực tế

Giả sử bạn có một thư mục chứa đầy các hoá đơn đã quét và bạn muốn lấy ra tổng số tiền. Dưới đây là một phần mở rộng nhanh của đoạn mã trước, sử dụng biểu thức chính quy đơn giản.

```csharp
using System.Text.RegularExpressions;

static void ExtractTotalAmount(string ocrText)
{
    // Look for a pattern like "$1,234.56"
    var match = Regex.Match(ocrText, @"\$\d{1,3}(,\d{3})*(\.\d{2})?");
    if (match.Success)
        Console.WriteLine($"Detected total: {match.Value}");
    else
        Console.WriteLine("Total amount not found.");
}
```

Bạn sẽ gọi `ExtractTotalAmount(result.Text);` ngay sau khi in kết quả OCR. Điều này cho thấy việc **extract text from invoice** các tệp trở nên dễ dàng như thế nào khi đã có chuỗi thô.

## Bước 6 – Chuyển đổi Ảnh sang Văn bản Hàng loạt (convert image to text)

Xử lý một tệp đơn lẻ là ổn cho bản demo, nhưng mã sản xuất thường cần xử lý hàng chục hoặc hàng trăm ảnh. Dưới đây là một vòng lặp ngắn gọn xử lý toàn bộ thư mục:

```csharp
static void ProcessFolder(OcrEngine engine, string folderPath)
{
    foreach (var file in Directory.EnumerateFiles(folderPath, "*.*", SearchOption.TopDirectoryOnly)
                                 .Where(f => f.EndsWith(".png") || f.EndsWith(".jpg") || f.EndsWith(".tiff")))
    {
        Console.WriteLine($"\nProcessing: {Path.GetFileName(file)}");
        var img = OcrImage.FromFile(file);
        var res = engine.Recognize(img, Language.English);
        Console.WriteLine(res.Text);
        ExtractTotalAmount(res.Text); // optional invoice extraction
    }
}
```

Chạy `ProcessFolder(ocrEngine, @"C:\Invoices")` sẽ **convert image to text** cho mọi tệp được hỗ trợ trong thư mục, tận dụng GPU để tăng tốc.

## Các Trường hợp Cạnh và Những Cạm Bẫy Thường Gặp

| **Quét độ‑tương‑cản thấp** | OCR gặp khó khăn trong việc phân biệt tiền cảnh và nền. | Tăng độ tương phản (`ImagePreprocessor.AdjustContrast`) hoặc áp dụng ngưỡng thích nghi. |
| **PDF đa‑trang** | `OcrImage.FromFile` chỉ đọc trang đầu tiên. | Sử dụng `PdfDocument` để trích xuất mỗi trang dưới dạng `OcrImage` và lặp lại. |
| **Ngôn ngữ không được hỗ trợ** | Ngôn ngữ mặc định được đặt là tiếng Anh. | Truyền `Language.Spanish` hoặc bất kỳ giá trị enum nào được hỗ trợ. |
| **GPU không được phát hiện** | Thiếu các binary gốc hoặc driver đã lỗi thời. | Kiểm tra driver GPU đã cập nhật; cài lại gói NuGet với flag `-runtime`. |
| **Thiếu bộ nhớ khi ảnh quá lớn** | Bộ nhớ GPU có giới hạn. | Thu nhỏ ảnh (`image = ImagePreprocessor.Resize(image, 2000, 0)`). |

Giải quyết những vấn đề này sớm sẽ tiết kiệm cho bạn hàng giờ gỡ lỗi sau này.

## Ví dụ Hoạt động Đầy đủ

Dưới đây là chương trình hoàn chỉnh bạn có thể sao chép‑dán vào một ứng dụng console mới. Nó bao gồm tất cả các phương thức trợ giúp đã thảo luận ở trên.

```csharp
using System;
using System.IO;
using System.Linq;
using System.Text.RegularExpressions;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace GpuOcrDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Initialize GPU‑accelerated OCR engine.
            var ocrEngine = new OcrEngine { Engine = Engine.Gpu };

            // 2️⃣ Define the path to a single image or a folder.
            string imagePath = @"YOUR_DIRECTORY/high_res_invoice.png";
            // string folderPath = @"C:\Invoices";

            // Uncomment one of the following lines:
            PerformOcr(ocrEngine, imagePath);
            // ProcessFolder(ocrEngine, folderPath);
        }

        // -------------------------------------------------
        // Load image, preprocess, recognize, and display.
        // -------------------------------------------------
        static void PerformOcr(OcrEngine engine, string filePath)
        {
            var image = OcrImage.FromFile(filePath);
            image = ImagePreprocessor.AdjustContrast(image, 1.2);
            image = ImagePreprocessor.ConvertToGrayscale(image);

            var result = engine.Recognize(image, Language.English);
            Console.WriteLine("=== OCR RESULT ===");
            Console.WriteLine(result.Text);

            ExtractTotalAmount(result.Text);
        }

        // -------------------------------------------------
        // Bulk processing of a folder.
        // -------------------------------------------------
        static void ProcessFolder(OcrEngine engine, string folderPath)
        {
            foreach (var file in Directory.EnumerateFiles(folderPath, "*.*")
                                          .Where(f => f.EndsWith(".png") || f.EndsWith(".jpg") || f.EndsWith(".tiff")))
            {
                Console.WriteLine($"\nProcessing: {Path.GetFileName(file)}");
                var img = OcrImage.FromFile(file);
                var res = engine.Recognize(img, Language.English);
                Console.WriteLine(res.Text);
                ExtractTotalAmount(res.Text);
            }
        }

        // -------------------------------------------------
        // Simple regex to pull the total amount from an invoice.
        // -------------------------------------------------
        static void ExtractTotalAmount(string ocrText)
        {
            var match = Regex.Match(ocrText, @"\$\d{1,3}(,\d{3})*(\.\d{2})?");
            if (match.Success)
                Console.WriteLine($"Detected total: {match.Value}");
            else
                Console.WriteLine("Total amount not found.");
        }
    }
}
```

**Run it** (`

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}