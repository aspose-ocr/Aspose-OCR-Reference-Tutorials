---
category: general
date: 2026-02-09
description: Trích xuất văn bản từ hình ảnh bằng C# OCR offline. Một ví dụ hoàn chỉnh
  về OCR bằng C# cho thấy cách tải hình ảnh để OCR, nhận dạng văn bản Cyrillic và
  trích xuất văn bản từ hộ chiếu.
draft: false
keywords:
- extract text from image
- c# ocr example
- load image for ocr
- recognize cyrillic text
- recognize text from passport
language: vi
og_description: Trích xuất văn bản từ hình ảnh bằng OCR offline C#. Học ví dụ OCR
  C# từng bước, tải hình ảnh để OCR, nhận dạng văn bản Cyrillic và trích xuất văn
  bản từ hộ chiếu.
og_title: Trích xuất văn bản từ hình ảnh trong C# – Hướng dẫn OCR offline
tags:
- OCR
- C#
- Aspose
title: Trích xuất văn bản từ hình ảnh trong C# – Ví dụ OCR offline
url: /vi/net/text-recognition/extract-text-from-image-in-c-offline-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Trích xuất văn bản từ hình ảnh trong C# – Ví dụ OCR Offline

Bạn đã bao giờ cần **trích xuất văn bản từ hình ảnh** nhưng gặp khó khăn với các API phụ thuộc vào mạng? Bạn không phải là người duy nhất. Nhiều nhà phát triển gặp phải vấn đề khi dịch vụ OCR cố gắng tải các gói ngôn ngữ tại thời gian chạy, đặc biệt trong các môi trường bị hạn chế.

Trong hướng dẫn này, chúng tôi sẽ hướng dẫn qua một **c# ocr example** chạy hoàn toàn offline, tải một hình ảnh để OCR và nhận dạng văn bản Cyrillic từ hộ chiếu. Khi kết thúc, bạn sẽ có một chương trình sẵn sàng chạy, in nội dung văn bản thuần từ bất kỳ hình ảnh hỗ trợ nào trực tiếp lên console.

## Những gì bạn sẽ học

- Cách thiết lập Aspose.OCR để xử lý offline.  
- Mã chính xác để **load image for OCR** từ đĩa.  
- Cách cấu hình engine để **recognize cyrillic text**.  
- Một **c# ocr example** đầy đủ, sẵn sàng copy‑paste, để trích xuất văn bản từ ảnh kiểu hộ chiếu.  

Không cần kinh nghiệm trước với Aspose; chỉ cần SDK .NET 6 (hoặc mới hơn) và Visual Studio 2022 (hoặc VS Code) là đủ.

---

![Trích xuất văn bản từ hình ảnh bằng Aspose OCR trên ảnh hộ chiếu](/images/ocr-passport.jpg "trích xuất văn bản từ hình ảnh")

## Bước 1: Thiết lập dự án để trích xuất văn bản từ hình ảnh

Trước khi viết bất kỳ mã nào, hãy chắc chắn rằng gói NuGet Aspose.OCR đã được thêm vào dự án của bạn:

```bash
dotnet add package Aspose.OCR
```

> **Mẹo chuyên nghiệp:** Sử dụng cờ `--version` để khóa vào phiên bản ổn định mới nhất (ví dụ, `13.9.0`). Điều này đảm bảo tính tương thích với .NET 6.

Tạo một ứng dụng console mới đơn giản như sau:

```bash
dotnet new console -n OfflineOcrDemo
cd OfflineOcrDemo
```

Bây giờ bạn có một môi trường trống sạch, nơi chúng ta sẽ **trích xuất văn bản từ hình ảnh** mà không cần kết nối internet.

## Bước 2: Tải hình ảnh cho OCR – Đọc ảnh hộ chiếu

Điều đầu tiên mà engine OCR cần là một bitmap hoặc stream đại diện cho hình ảnh. Trong kịch bản của chúng ta, chúng ta sẽ **load image for OCR** từ một tệp cục bộ có tên `cyrillic_passport.jpg`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;

// Step 2: Load the image file (this is the “load image for ocr” part)
var imagePath = @"YOUR_DIRECTORY\cyrillic_passport.jpg";

// Validate the file exists – helpful when the path is wrong.
if (!System.IO.File.Exists(imagePath))
{
    Console.WriteLine($"❌ Image not found at {imagePath}");
    return;
}

// ImageStream abstracts the underlying format; it works with JPEG, PNG, etc.
var image = ImageStream.FromFile(imagePath);
```

> **Tại sao điều này quan trọng:** Cung cấp một stream thay vì một `Bitmap` thô cho phép Aspose tự động phát hiện định dạng, giảm bớt mã lặp lại và các lỗi tiềm ẩn.

## Bước 3: Cấu hình chế độ Offline và chọn ngôn ngữ Cyrillic

Aspose.OCR có thể tải các mô hình ngôn ngữ khi cần, nhưng điều này làm mất mục đích của giải pháp offline. Tắt các cuộc gọi mạng và chỉ định rõ ràng cho engine ngôn ngữ nào sẽ sử dụng.

```csharp
// Step 3: Create the OCR engine and switch to offline mode
var ocrEngine = new OcrEngine
{
    Configuration =
    {
        OfflineMode = true,               // No network traffic – perfect for secure environments
        Language = new[] { OcrLanguage.Cyrillic } // We want to **recognize cyrillic text**
    }
};
```

> **Trường hợp đặc biệt:** Nếu sau này bạn cần nhận dạng ký tự Latin trong cùng tài liệu, chỉ cần thêm `OcrLanguage.English` vào mảng. Engine sẽ tự động xử lý phát hiện đa ngôn ngữ.

## Bước 4: Chạy engine OCR và nhận dạng văn bản Cyrillic

Bây giờ chúng ta thực sự **recognize text from passport**‑style images. Phương thức `Recognize` trả về một đối tượng kết quả phong phú, chứa văn bản thuần, điểm tin cậy và các hộp bao quanh.

```csharp
// Step 4: Perform the OCR operation
OcrResult result = ocrEngine.Recognize(image);

// Step 5: Output the plain text – this is where we finally **extract text from image**
Console.WriteLine("📝 Extracted Text:");
Console.WriteLine("-------------------");
Console.WriteLine(result.PlainText);
```

### Kết quả dự kiến trên console

```
📝 Extracted Text:
-------------------
ПАСПОРТ РФ
Иванов Иван Иванович
01.01.1990
...
```

Nếu kết quả bị rối, hãy kiểm tra lại rằng ảnh nguồn rõ ràng và gói ngôn ngữ `OfflineMode` cho Cyrillic có trong thư mục cài đặt Aspose (thường là `\Aspose.OCR\resources\languages`).

## Ví dụ OCR C# hoàn chỉnh – Mã nguồn đầy đủ

Dưới đây là **c# ocr example** đầy đủ. Sao chép‑dán nó vào `Program.cs` và chạy `dotnet run`. Mọi thứ bạn cần để **trích xuất văn bản từ hình ảnh** đều có ở đây.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;

class OfflineExample
{
    static void Main()
    {
        // --------------------------------------------------------------
        // Step 1: Create the OCR engine (offline mode)
        // --------------------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Configuration =
            {
                OfflineMode = true,                     // No network calls
                Language = new[] { OcrLanguage.Cyrillic } // Recognize Cyrillic text
            }
        };

        // --------------------------------------------------------------
        // Step 2: Load the image for OCR (passport photo)
        // --------------------------------------------------------------
        var imagePath = @"YOUR_DIRECTORY\cyrillic_passport.jpg";

        if (!System.IO.File.Exists(imagePath))
        {
            Console.WriteLine($"❌ Image not found at {imagePath}");
            return;
        }

        var image = ImageStream.FromFile(imagePath);

        // --------------------------------------------------------------
        // Step 3: Recognize the text
        // --------------------------------------------------------------
        var result = ocrEngine.Recognize(image);

        // --------------------------------------------------------------
        // Step 4: Output the plain text (the final extraction)
        // --------------------------------------------------------------
        Console.WriteLine("📝 Extracted Text:");
        Console.WriteLine("-------------------");
        Console.WriteLine(result.PlainText);
    }
}
```

### Chạy ví dụ

```bash
dotnet run
```

Bạn sẽ thấy console in ra các chi tiết hộ chiếu bằng Cyrillic. Đó là lúc bạn biết rằng quy trình **trích xuất văn bản từ hình ảnh** của bạn đã hoạt động.

## Những lỗi thường gặp & Cách khắc phục

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| Empty `PlainText` | Mô hình ngôn ngữ sai hoặc ảnh quá tối | Đảm bảo ngôn ngữ `OfflineMode` bao gồm `Cyrillic` và tăng độ tương phản của ảnh |
| `System.DllNotFoundException` | Thiếu các tệp nhị phân gốc của Aspose OCR | Cài đặt lại gói NuGet hoặc sao chép `Aspose.OCR.Native.dll` vào thư mục đầu ra |
| Slow performance on large images | Engine xử lý toàn bộ độ phân giải | Giảm kích thước ảnh xuống ≤ 1500 px chiều rộng trước khi đưa vào `ImageStream` |
| Garbled characters | Ảnh bị quay sai hướng | Sử dụng `Image.RotateFlip(RotateFlipType.Rotate90FlipNone)` trước khi tạo stream |

## Các bước tiếp theo – Mở rộng quy trình OCR Offline

- **Load image for OCR** từ một `MemoryStream` khi xử lý các tệp tải lên trong ASP.NET Core.  
- Chuyển sang **recognize text from passport** ở chế độ batch bằng cách lặp qua một thư mục chứa các ảnh quét hộ chiếu.  
- Kết hợp kết quả với **regular expressions** để trích xuất các trường như số hộ chiếu hoặc ngày sinh.  
- Thử nghiệm `ocrEngine.Configuration.UseParallelProcessing = true` để tăng tốc đa lõi.

---

### Kết luận

Chúng tôi vừa cho bạn thấy cách **trích xuất văn bản từ hình ảnh** bằng một pipeline OCR C# hoàn toàn offline. **c# ocr example** ngắn gọn, tự chứa này tải một hình ảnh, cấu hình engine để **recognize cyrillic text**, và in dữ liệu hộ chiếu đã trích xuất — tất cả mà không có bất kỳ yêu cầu mạng nào.

Bạn có thể tự do chỉnh sửa mã, thêm nhiều ngôn ngữ hơn, hoặc đưa kết quả vào cơ sở dữ liệu. Khi đã nắm vững các kiến thức cơ bản về tải hình ảnh cho OCR và nhận dạng văn bản từ ảnh kiểu hộ chiếu, mọi thứ đều có thể.

Có câu hỏi hoặc muốn chia sẻ các chỉnh sửa của bạn? Hãy để lại bình luận bên dưới, và chúc bạn lập trình vui vẻ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}