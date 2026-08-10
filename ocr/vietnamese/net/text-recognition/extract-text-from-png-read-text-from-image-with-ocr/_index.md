---
category: general
date: 2026-03-17
description: Trích xuất văn bản từ PNG bằng Aspose OCR trong C#. Học cách đọc văn
  bản từ hình ảnh, xử lý OCR biên lai và tạo engine OCR với tăng tốc GPU.
draft: false
keywords:
- extract text from png
- read text from image
- ocr receipt image
- process receipt ocr
- create ocr engine
language: vi
og_description: Trích xuất văn bản từ PNG bằng Aspose OCR. Hướng dẫn này chỉ cách
  đọc văn bản từ hình ảnh, xử lý OCR biên lai và tạo engine OCR một cách hiệu quả.
og_title: Trích xuất văn bản từ PNG – Đọc văn bản từ hình ảnh bằng OCR
tags:
- OCR
- CSharp
- Aspose
title: Trích xuất văn bản từ PNG – Đọc văn bản từ hình ảnh bằng OCR
url: /vi/net/text-recognition/extract-text-from-png-read-text-from-image-with-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Trích xuất Văn bản từ PNG – Đọc Văn bản từ Hình ảnh bằng OCR

Bạn đã bao giờ cần **trích xuất văn bản từ PNG** nhưng không chắc thư viện nào sẽ cho kết quả đáng tin cậy? Bạn không phải là người duy nhất—các nhà phát triển luôn hỏi, “Làm sao để đọc văn bản từ các tệp hình ảnh như biên lai mà không phải tự viết mạng nơ-ron tùy chỉnh?” Tin tốt là Aspose OCR sẽ thực hiện phần việc nặng cho bạn, và bạn thậm chí có thể bật GPU để tăng tốc.

Trong hướng dẫn này, chúng ta sẽ đi qua mọi thứ bạn cần để **xử lý OCR biên lai**, từ cài đặt gói NuGet đến tạo một engine OCR hiểu được tệp PNG của bạn. Khi hoàn thành, bạn sẽ có một ứng dụng console tự chứa, đọc ảnh biên lai, in ra văn bản đã nhận dạng và chỉ cho bạn cách tinh chỉnh engine cho các kịch bản khác nhau. Không có tài liệu bên ngoài, chỉ có mã thuần và giải thích rõ ràng.

## Các Điều Kiện Cần Có

- .NET 6.0 SDK (hoặc bất kỳ phiên bản .NET gần đây nào)  
- Visual Studio 2022 hoặc VS Code với các extension C#  
- GPU NVIDIA được hỗ trợ với driver mới nhất (tùy chọn, nhưng khuyến nghị cho chế độ GPU)  
- Gói NuGet **Aspose.OCR** (`dotnet add package Aspose.OCR`)  

Nếu bạn không có GPU, vẫn có thể chạy ví dụ ở chế độ CPU—chỉ cần bỏ qua các dòng cấu hình GPU.

## Bước 1: Cài đặt Aspose.OCR và Thiết lập Dự án

Đầu tiên, tạo một dự án console mới và đưa thư viện Aspose OCR vào.

```bash
dotnet new console -n ReceiptOcrDemo
cd ReceiptOcrDemo
dotnet add package Aspose.OCR
```

Tại sao điều này quan trọng: gói `Aspose.OCR` bao gồm engine OCR, bộ tải ảnh và hỗ trợ GPU tùy chọn. Thêm nó qua NuGet đảm bảo bạn nhận được phiên bản ổn định mới nhất (tính đến tháng 3 2026 là 23.10).

## Bước 2: Nhập Namespace và Tạo Engine OCR

Bây giờ mở **Program.cs** và thêm các chỉ thị `using` cần thiết. Sau đó khởi tạo engine.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Create an OCR engine instance
            var ocrEngine = new OcrEngine();

            // Optional: Enable GPU acceleration if a compatible GPU is present
            // This dramatically speeds up processing of high‑resolution PNGs
            ocrEngine.Config.EngineMode = EngineMode.Gpu;   // <-- primary way to "process receipt ocr" fast
            ocrEngine.Config.GpuDeviceId = 0; // selects the first GPU in the system

            // The rest of the code follows...
```

**Mẹo chuyên nghiệp:** Nếu gặp lỗi `System.DllNotFoundException` trên máy không có GPU, chỉ cần chú thích hai dòng thiết lập `EngineMode` và `GpuDeviceId`. Engine sẽ tự động chuyển sang CPU.

## Bước 3: Tải Ảnh PNG Bạn Muốn Trích xuất Văn bản

Aspose OCR có thể đọc ảnh trực tiếp từ đường dẫn tệp, stream hoặc thậm chí mảng byte. Trong bản demo này, chúng ta sẽ tải một ảnh biên lai cục bộ.

```csharp
            // Step 3: Load the image (replace the path with your own PNG file)
            string imagePath = @"C:\Images\receipt.png";

            // Validate the file exists to avoid runtime surprises
            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found – {imagePath}");
                return;
            }

            // Load the image into the engine
            ocrEngine.Image = ImageStream.FromFile(imagePath);
```

Lưu ý cách chúng ta kiểm tra trường hợp tệp không tồn tại. Trong các ứng dụng thực tế, bạn có thể hiển thị thông báo UI thân thiện thay vì chỉ thoát.

## Bước 4: Thực hiện Nhận dạng OCR

Việc trích xuất văn bản thực tế diễn ra bằng một lời gọi phương thức duy nhất. Engine trả về một đối tượng `OcrResult` chứa chuỗi thô, điểm tin cậy và thông tin bố cục.

```csharp
            // Step 4: Run the OCR process
            OcrResult ocrResult = ocrEngine.Recognize();

            // Check if the engine succeeded
            if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
            {
                Console.WriteLine("No text could be recognized.");
                return;
            }
```

Tại sao chúng ta kiểm tra `ocrResult.Text`: đôi khi một PNG chất lượng thấp sẽ trả về chuỗi rỗng, và tốt hơn là thông báo cho người dùng thay vì im lặng không xuất gì.

## Bước 5: Xuất Văn bản Đã Nhận dạng

Cuối cùng, in chuỗi đã trích xuất ra console. Bạn cũng có thể ghi nó vào tệp, cơ sở dữ liệu, hoặc truyền vào dịch vụ khác.

```csharp
            // Step 5: Display the recognized text
            Console.WriteLine("=== Extracted Text from PNG ===");
            Console.WriteLine(ocrResult.Text);
            Console.WriteLine("=== End of Output ===");
        }
    }
}
```

Khi chạy chương trình (`dotnet run`), bạn sẽ thấy kết quả tương tự:

```
=== Extracted Text from PNG ===
Store: Coffee Corner
Date: 03/15/2026
Item      Qty   Price
Latte      2    $5.40
Muffin     1    $2.30
Total            $7.70
=== End of Output ===
```

Đó là **giải pháp hoàn chỉnh để trích xuất văn bản từ các tệp PNG** bằng Aspose OCR, và bạn vừa học cách **đọc văn bản từ hình ảnh** giống như các biên lai.

## Tùy chọn: Tinh chỉnh Engine OCR (Nâng cao)

Nếu bạn cần độ chính xác cao hơn cho các phông chữ cụ thể hoặc nền nhiễu, hãy cân nhắc điều chỉnh các thiết lập sau:

```csharp
// Enable language detection (default is English)
ocrEngine.Config.Language = Language.English;

// Turn on automatic image preprocessing (deskew, binarization)
ocrEngine.Config.EnableImagePreprocessing = true;

// Set a confidence threshold if you only want high‑certainty results
ocrEngine.Config.ConfidenceThreshold = 0.75f;
```

Những tinh chỉnh này đặc biệt hữu ích khi bạn **xử lý OCR biên lai** trong các công việc batch mà một số bản scan không hoàn hảo.

## Những Sai Lầm Thường Gặp & Cách Tránh

| Vấn đề | Nguyên nhân | Giải pháp |
|-------|-------------|-----------|
| **Thiếu driver GPU** | Engine cố gắng tải CUDA nhưng không tìm thấy DLL. | Cài đặt driver NVIDIA mới nhất hoặc chuyển sang chế độ CPU bằng cách xóa dòng `EngineMode.Gpu`. |
| **Đường dẫn ảnh không đúng** | `ImageStream.FromFile` ném lỗi nếu không tìm thấy tệp. | Luôn xác thực đường dẫn (xem Bước 3) hoặc dùng `Path.Combine` để an toàn đa nền tảng. |
| **Độ tin cậy thấp trên biên lai mờ** | Engine OCR không phân biệt được ký tự. | Bật `EnableImagePreprocessing` và tùy chọn tăng DPI ảnh trước khi đưa vào engine. |
| **Rò rỉ bộ nhớ trong dịch vụ chạy lâu** | Mỗi `OcrEngine` giữ tài nguyên không quản lý. | Giải phóng engine sau khi dùng: `using var ocrEngine = new OcrEngine();` |

## Ví dụ Hoàn chỉnh (Sao chép‑Dán)

Dưới đây là **toàn bộ chương trình** bạn có thể dán vào `Program.cs`. Nó bao gồm tất cả các tinh chỉnh tùy chọn đã được chú thích để dễ kích hoạt.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create OCR engine
            using var ocrEngine = new OcrEngine();

            // Enable GPU acceleration if you have a supported card
            ocrEngine.Config.EngineMode = EngineMode.Gpu;
            ocrEngine.Config.GpuDeviceId = 0;

            // Optional fine‑tuning (uncomment as needed)
            //ocrEngine.Config.Language = Language.English;
            //ocrEngine.Config.EnableImagePreprocessing = true;
            //ocrEngine.Config.ConfidenceThreshold = 0.75f;

            // Load PNG image
            string imagePath = @"C:\Images\receipt.png";
            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found – {imagePath}");
                return;
            }
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // Perform OCR
            OcrResult ocrResult = ocrEngine.Recognize();

            // Verify result
            if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
            {
                Console.WriteLine("No text could be recognized.");
                return;
            }

            // Output the extracted text
            Console.WriteLine("=== Extracted Text from PNG ===");
            Console.WriteLine(ocrResult.Text);
            Console.WriteLine("=== End of Output ===");
        }
    }
}
```

Lưu, chạy `dotnet run`, và bạn sẽ thấy nội dung biên lai được in ra console.

![ví dụ trích xuất văn bản từ png](receipt.png "ví dụ trích xuất văn bản từ png")

*Hình ảnh trên hiển thị một mẫu biên lai PNG mà mã có thể xử lý.*

## Tóm tắt

Chúng ta đã tìm hiểu cách **trích xuất văn bản từ các tệp PNG** bằng Aspose OCR, minh họa cách **đọc văn bản từ hình ảnh**, và đi qua một quy trình **xử lý OCR biên lai** đầy đủ, bao gồm tùy chọn tăng tốc GPU. Bằng cách **tạo một engine OCR** riêng, bạn có toàn quyền kiểm soát cấu hình, hiệu năng và xử lý lỗi.

## Bạn Có Thể Khám Phá Gì Tiếp Theo?

- **Xử lý batch**: Lặp qua một thư mục các biên lai PNG và ghi mỗi kết quả vào tệp CSV.  
- **Tích hợp với Azure Functions**: Biến console app này thành endpoint serverless nhận tải lên ảnh.  
- **Hỗ trợ đa ngôn ngữ**: Thay `Language.English` bằng `Language.Spanish` hoặc thêm từ điển tùy chỉnh.  
- **Xử lý hậu kỳ**: Dùng biểu thức chính quy để trích xuất các trường như tổng tiền, ngày, hoặc mã số thuế từ chuỗi OCR thô.

Hãy thoải mái thử nghiệm—OCR là công cụ linh hoạt hơn bạn nghĩ khi biết cách điều chỉnh các tham số. Nếu gặp khó khăn, hãy để lại bình luận bên dưới hoặc tham khảo tài liệu API Aspose OCR để tìm hiểu sâu hơn.

Chúc lập trình vui vẻ, và tận hưởng việc biến những biên lai PNG cứng đầu thành văn bản có thể tìm kiếm!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}