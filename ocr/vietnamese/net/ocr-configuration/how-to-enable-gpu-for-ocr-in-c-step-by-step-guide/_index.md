---
category: general
date: 2026-04-04
description: Cách bật GPU trong Aspose OCR nhanh chóng. Học cách trích xuất văn bản
  từ hình ảnh, tải hình ảnh cho OCR và nhận dạng văn bản bằng C#.
draft: false
keywords:
- how to enable gpu
- extract text from image
- how to extract text
- how to recognize text
- load image for ocr
language: vi
og_description: Cách bật GPU trong Aspose OCR nhanh chóng. Thực hiện theo hướng dẫn
  này để trích xuất văn bản từ hình ảnh, tải hình ảnh cho OCR và nhận dạng văn bản
  bằng C#.
og_title: Cách bật GPU cho OCR trong C# – Hướng dẫn đầy đủ
tags:
- Aspose OCR
- C#
- GPU acceleration
title: Cách bật GPU cho OCR trong C# – Hướng dẫn từng bước
url: /vi/net/ocr-configuration/how-to-enable-gpu-for-ocr-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách bật GPU cho OCR trong C# – Hướng dẫn đầy đủ

Bạn đã bao giờ tự hỏi **cách bật gpu** khi sử dụng Aspose OCR chưa? Có thể bạn đã gặp giới hạn hiệu năng khi xử lý hàng trăm biên lai, và CPU không thể theo kịp. Tin tốt là việc bật tăng tốc GPU rất đơn giản, và một khi đã bật, bạn sẽ thấy engine OCR chạy nhanh như chớp qua các hình ảnh.

Trong tutorial này chúng tôi không chỉ bật công tắc GPU, mà còn chỉ cho bạn cách **load image for OCR**, **recognize text**, và cuối cùng **extract text from image** bằng một ví dụ C# sạch sẽ. Khi kết thúc, bạn sẽ có một chương trình sẵn sàng chạy để lấy văn bản thuần từ bất kỳ hình ảnh nào được hỗ trợ—không cần dịch vụ bên ngoài.

## Những gì bạn cần

- .NET 6+ (hoặc .NET Framework 4.7.2 trở lên).  
- Aspose.OCR for .NET, phiên bản 24.2.0 hoặc mới hơn (cờ GPU được thêm vào trong bản phát hành này).  
- Một máy có GPU được bật và driver phù hợp (NVIDIA CUDA 11+ hoạt động tốt).  
- Một tệp hình ảnh bạn muốn xử lý—ví dụ như biên lai đã quét, hoá đơn chụp ảnh, hoặc ghi chú viết tay.

Nếu bạn đã có những thứ trên, tuyệt vời—hãy bắt đầu.

## Bước 1: Cách bật gpu – Cấu hình Engine OCR

Điều đầu tiên bạn phải làm là thông báo cho Aspose OCR sử dụng GPU. Điều này được thực hiện bằng cách đặt thuộc tính `UseGpu` trên đối tượng `OcrEngine`. Thuộc tính này mặc định là `false`, vì vậy chúng ta bật nó một cách rõ ràng.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // <-- GPU module namespace

// Create the OCR engine and enable GPU acceleration (available from version 24.2.0)
var ocrEngine = new OcrEngine
{
    // Enabling GPU can speed up recognition by 2‑5× on a modern card
    UseGpu = true
};
```

**Tại sao điều này quan trọng:** Khi `UseGpu` là `true`, thư viện sẽ chuyển các phép tính ma trận nặng sang bộ xử lý đồ họa. Trên một RTX 3060 trung bình, bạn sẽ thấy độ trễ giảm từ vài giây mỗi hình ảnh xuống chỉ còn phần nghìn giây.

> **Pro tip:** Nếu bạn đang chạy trong môi trường CI không có giao diện, hãy chắc chắn driver GPU đã được cài đặt và tài khoản dịch vụ có quyền truy cập vào thiết bị. Nếu không, engine sẽ tự động quay lại chế độ CPU mà không báo lỗi.

## Bước 2: Load Image for OCR – Đặt Engine vào Tệp của Bạn

Tiếp theo, chúng ta cần **load image for OCR**. Aspose OCR chấp nhận bất kỳ định dạng ảnh nào được System.Drawing hỗ trợ (PNG, JPEG, BMP, TIFF, v.v.). Trợ giúp `ImageStream.FromFile` sẽ gói tệp vào đối tượng stream cần thiết.

```csharp
// Replace the path with the location of your receipt or document
string imagePath = @"C:\MyImages\receipt.jpg";

ocrEngine.Image = ImageStream.FromFile(imagePath);
```

Nếu bạn muốn tải từ một `byte[]` (ví dụ khi ảnh đến từ cơ sở dữ liệu), bạn có thể dùng `ImageStream.FromBytes(byteArray)` thay thế—kết quả giống nhau, chỉ khác nguồn dữ liệu.

## Bước 3: Cách nhận dạng văn bản – Chạy quy trình OCR

Bây giờ engine đã được cấu hình và ảnh đã được tải, đã đến lúc **recognize text**. Phương thức `Recognize` thực hiện toàn bộ công việc nặng và trả về một đối tượng `OcrResult` chứa văn bản thuần, điểm tin cậy, và thậm chí các bounding box nếu bạn cần chúng sau này.

```csharp
// Run the recognition process (English is the default language)
OcrResult ocrResult = ocrEngine.Recognize();
```

Bạn cũng có thể thay đổi ngôn ngữ bằng cách đặt `ocrEngine.Language = OcrLanguage.French;` trước khi gọi `Recognize()`. Tăng tốc GPU hoạt động bất kể gói ngôn ngữ bạn tải.

## Bước 4: Cách trích xuất văn bản từ ảnh – Xuất kết quả

Cuối cùng chúng ta **extract text from image** bằng cách đọc thuộc tính `Text` của đối tượng kết quả. Đối với mục đích demo, chúng tôi sẽ chỉ in ra console, nhưng bạn có thể ghi vào tệp, cơ sở dữ liệu, hoặc truyền vào dịch vụ khác.

```csharp
// Output the extracted plain‑text to the console
Console.WriteLine("=== OCR RESULT ===");
Console.WriteLine(ocrResult.Text);
```

**Kết quả mong đợi** (văn bản thực tế của bạn sẽ khác tùy vào ảnh):

```
=== OCR RESULT ===
Store: Coffee Corner
Date: 03/28/2026
Item          Qty   Price
Latte          2    $5.00
Muffin         1    $2.50
Total                 $12.50
```

Nếu bạn cần các giá trị tin cậy thô, có thể lặp qua `ocrResult.Regions` và kiểm tra mỗi `Region.Confidence`.

## Ví dụ Hoạt động Đầy đủ – Một Tệp, Sẵn sàng Chạy

Dưới đây là chương trình hoàn chỉnh. Sao chép‑dán vào một dự án console mới, khôi phục gói NuGet Aspose.OCR, và nhấn **F5**.

```csharp
// ------------------------------------------------------------
// How to enable gpu for OCR in C# – Complete Example
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU module namespace

class Program
{
    static void Main()
    {
        // -------- Step 1: Enable GPU ----------
        var ocrEngine = new OcrEngine
        {
            UseGpu = true   // <-- crucial for acceleration
        };

        // -------- Step 2: Load image ----------
        // Make sure the file exists; otherwise an exception is thrown.
        string imagePath = @"YOUR_DIRECTORY/receipt.jpg";
        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // -------- Step 3: Recognize text -------
        OcrResult ocrResult = ocrEngine.Recognize();

        // -------- Step 4: Extract text ----------
        Console.WriteLine("=== OCR RESULT ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

> **Note:** Thay `YOUR_DIRECTORY/receipt.jpg` bằng đường dẫn thực tế tới ảnh của bạn. Nếu chương trình ném `FileNotFoundException`, hãy kiểm tra lại đường dẫn và quyền truy cập tệp.

## Các Câu hỏi Thường gặp & Trường hợp Cạnh

### Nếu GPU không được phát hiện thì sao?

Aspose OCR sẽ tự động quay lại chế độ CPU và ghi cảnh báo. Để xác nhận chế độ đang hoạt động, kiểm tra `ocrEngine.IsGpuEnabled` sau khi khởi tạo—nó trả về `true` chỉ khi driver GPU được tải thành công.

### Tôi có thể xử lý nhiều ảnh trong một vòng lặp không?

Chắc chắn rồi. Chỉ cần di chuyển dòng `ocrEngine.Image = …` vào trong vòng lặp `foreach (var file in files)`. Giữ lại cùng một instance của `OcrEngine`; việc tái sử dụng nó giúp tránh chi phí cấp phát tài nguyên GPU lặp lại.

```csharp
foreach (var file in Directory.GetFiles(@"C:\MyImages", "*.jpg"))
{
    ocrEngine.Image = ImageStream.FromFile(file);
    var result = ocrEngine.Recognize();
    Console.WriteLine($"{Path.GetFileName(file)} → {result.Text.Length} characters");
}
```

### Làm sao xử lý các ngôn ngữ không phải tiếng Anh?

Đặt ngôn ngữ trước khi gọi `Recognize()`:

```csharp
ocrEngine.Language = OcrLanguage.Spanish;   // or any supported language enum
```

Tăng tốc GPU hoạt động tương tự; chỉ có mô hình ngôn ngữ thay đổi.

### Còn các ảnh lớn, độ phân giải cao thì sao?

Nếu gặp lỗi hết bộ nhớ, hãy giảm kích thước ảnh trước. Aspose OCR cung cấp `ImageHelper.Resize` – cách nhanh chóng thu nhỏ mà không mất quá nhiều chi tiết.

```csharp
ocrEngine.Image = ImageHelper.Resize(
    ImageStream.FromFile(imagePath), 
    maxWidth: 2000, 
    maxHeight: 2000);
```

## Kết luận

Chúng tôi đã trình bày **cách bật gpu** cho Aspose OCR, chỉ cho bạn cách **load image for OCR**, hướng dẫn **cách nhận dạng văn bản**, và minh họa **cách trích xuất văn bản từ ảnh** bằng một chương trình C# ngắn gọn, sẵn sàng sản xuất. Bằng cách bật cờ `UseGpu` bạn sẽ mở khóa một tăng tốc đáng kể, đặc biệt khi xử lý hàng loạt biên lai, hoá đơn, hoặc bất kỳ luồng tài liệu khối lượng lớn nào.

Sẵn sàng cho bước tiếp theo? Hãy kết hợp pipeline OCR này với cơ sở dữ liệu để lưu trữ các biên lai đã trích xuất, hoặc đưa văn bản thuần vào mô hình xử lý ngôn ngữ tự nhiên để phân loại chi phí. Bạn cũng có thể khám phá bộ sưu tập `OcrResult.Regions` để lấy tọa độ bounding‑box và xây dựng giao diện UI đánh dấu từng từ trên ảnh gốc.

Chúc lập trình vui vẻ, và tận hưởng sức mạnh bổ sung mà tăng tốc GPU mang lại cho khối lượng công việc OCR của bạn!

---

![hình minh họa cách bật gpu](gpu-ocr-diagram.png "hình minh họa cách bật gpu")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}