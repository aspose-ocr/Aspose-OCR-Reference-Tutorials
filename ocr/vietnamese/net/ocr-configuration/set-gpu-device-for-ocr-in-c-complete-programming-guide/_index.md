---
category: general
date: 2026-03-18
description: Cài đặt thiết bị GPU trong Aspose OCR để trích xuất văn bản từ hình ảnh
  nhanh chóng. Tìm hiểu cách tải hình ảnh cho OCR, nhận dạng hình ảnh biên lai và
  nhận kết quả chính xác.
draft: false
keywords:
- set GPU device
- extract text from image
- how to extract text
- load image for OCR
- recognize receipt image
language: vi
og_description: Cài đặt thiết bị GPU trong Aspose OCR để trích xuất văn bản từ hình
  ảnh nhanh chóng. Hãy làm theo hướng dẫn từng bước này để tải hình ảnh cho OCR và
  nhận dạng hình ảnh biên lai.
og_title: Thiết lập thiết bị GPU cho OCR trong C# – Hướng dẫn lập trình toàn diện
tags:
- OCR
- C#
- GPU
- Aspose
title: Thiết lập thiết bị GPU cho OCR trong C# – Hướng dẫn lập trình toàn diện
url: /vi/net/ocr-configuration/set-gpu-device-for-ocr-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Đặt Thiết Bị GPU cho OCR trong C# – Hướng Dẫn Lập Trình Đầy Đủ

Cần **đặt thiết bị GPU** để xử lý OCR nhanh hơn? Trong hướng dẫn này chúng tôi sẽ chỉ cho bạn cách thiết lập thiết bị GPU bằng Aspose OCR, sau đó trích xuất văn bản từ ảnh biên lai chỉ trong vài dòng mã.  

Nếu bạn từng gặp khó khăn khi **tải ảnh cho OCR** hoặc tự hỏi *cách trích xuất văn bản* từ các bản quét độ phân giải cao, bạn đang ở đúng chỗ. Khi hoàn thành, bạn sẽ có một chương trình có thể chạy được, nhận diện ảnh biên lai, in ra văn bản thuần và tự chuyển sang CPU một cách nhẹ nhàng nếu không có GPU.

## Nội Dung Hướng Dẫn

Chúng tôi sẽ bao phủ mọi thứ bạn cần biết:

* Cài đặt gói NuGet Aspose OCR (phụ thuộc duy nhất).  
* Đặt thiết bị GPU (`set GPU device`) và tùy chọn chọn chỉ mục GPU khác.  
* Tải tệp ảnh cho OCR – đúng, bao gồm bước “load image for OCR” mà nhiều người mới bắt đầu thường gặp rắc rối.  
* Chạy engine nhận dạng để **recognize receipt image**.  
* Trích xuất chuỗi kết quả để bạn có thể **extract text from image** và sử dụng trong ứng dụng của mình.  

Không có phép màu, không có liên kết tài liệu ẩn – chỉ một giải pháp hoàn chỉnh, tự chứa mà bạn có thể sao chép‑dán vào Visual Studio và chạy ngay hôm nay.

## Yêu Cầu Trước

* .NET 6.0 trở lên (mã cũng chạy trên .NET Core và .NET Framework).  
* Máy có GPU và đã cài driver phù hợp – nếu không, thư viện sẽ tự động chuyển sang chế độ CPU.  
* Một ảnh biên lai mẫu (ví dụ: `receipt_highres.png`) được đặt ở vị trí bạn có thể tham chiếu bằng đường dẫn đầy đủ.  

Chỉ vậy thôi. Nếu bạn chưa có gói NuGet, chạy `dotnet add package Aspose.OCR` trong thư mục dự án của bạn.

---

## Bước 1 – Đặt Thiết Bị GPU trong Aspose OCR

Điều đầu tiên bạn phải làm là **set GPU device** trên engine OCR. Điều này báo cho Aspose chuyển phần xử lý nặng sang card đồ họa thay vì CPU.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;

class GpuDemo
{
    static void Main()
    {
        // Create the OCR engine instance
        var ocrEngine = new OcrEngine();

        // Enable GPU processing – this is where we set the GPU device
        ocrEngine.Settings.ProcessingMode = ProcessingMode.Gpu;

        // (Optional) Choose a specific GPU if you have more than one.
        // The default is device 0, but you can set it to 1, 2, etc.
        ocrEngine.Settings.GpuDeviceId = 0;
```

**Tại sao lại quan trọng:**  
Khi engine chạy ở `ProcessingMode.Gpu`, các kernel CUDA bên dưới có thể tăng tốc việc phân đoạn ký tự và suy luận mạng nơ‑ron một cách đáng kể. Trên một RTX 3080 hiện đại, thời gian OCR sẽ giảm từ vài giây xuống dưới một giây cho các biên lai độ phân giải cao.

> **Mẹo chuyên nghiệp:** Nếu bạn không chắc chỉ mục GPU nào nên dùng, gọi `OcrEngine.GetAvailableGpuDevices()` (có trong các phiên bản mới) và chọn thiết bị có bộ nhớ trống nhiều nhất.

---

## Bước 2 – Tải Ảnh cho OCR

Sau khi đã cấu hình engine, chúng ta cần **load image for OCR**. Aspose cung cấp một wrapper tiện lợi `ImageStream` giúp trừu tượng hoá I/O và hỗ trợ stream từ bộ nhớ, mạng hoặc đĩa.

```csharp
        // Load the receipt image you want to recognize
        var imagePath = @"C:\OCR\Samples\receipt_highres.png";
        var imageStream = ImageStream.FromFile(imagePath);
```

**Có thể gặp vấn đề gì?**  
Nếu đường dẫn tệp sai hoặc ảnh bị hỏng, `FromFile` sẽ ném ra `FileNotFoundException`. Kiểm tra nhanh `File.Exists(imagePath)` trước khi tạo stream sẽ giúp tránh lỗi nghiêm trọng.

---

## Bước 3 – Nhận Diện Ảnh Biên Lai

Với ảnh đã sẵn sàng, chúng ta gọi `Recognize`. Đây là bước thực sự **recognize receipt image** nội dung bằng pipeline tăng tốc GPU mà chúng ta đã thiết lập trước đó.

```csharp
        // Perform OCR – this returns an OcrResult object
        var ocrResult = ocrEngine.Recognize(imageStream);
```

**Bên trong engine:**  
Engine đầu tiên chuyển ảnh thành bitmap xám chuẩn hoá, sau đó chạy mô hình deep‑learning dự đoán xác suất ký tự. Vì đang chạy trên GPU, mô hình xử lý toàn bộ bitmap đồng thời, vì vậy các biên lai lớn hoàn thành nhanh chóng.

---

## Bước 4 – Trích Xuất Văn Bản từ Ảnh và Kiểm Tra Kết Quả

Cuối cùng, chúng ta lấy kết quả văn bản thuần từ `OcrResult` và in ra console. Đây là lúc bạn **extract text from image** và có thể đưa nó vào các luồng xử lý tiếp theo (ví dụ: phân tích các mục hàng).

```csharp
        // Output the recognized plain text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine("==================");
    }
}
```

**Kết quả mong đợi:**  

```
=== OCR Result ===
Store Name
Date: 03/15/2026
Item A   $12.99
Item B   $5.49
Total    $18.48
==================
```

Nếu văn bản bị lộn xộn, hãy kiểm tra lại ảnh có độ phân giải cao và driver GPU đã được cập nhật. Bạn cũng có thể bật `ocrEngine.Settings.PreprocessMode` để cải thiện độ tương phản cho các biên lai thiếu ánh sáng.

---

## Bước 5 – Chuyển Sang CPU (Xử Lý Trường Hợp Ngoại Lệ)

Nếu máy mục tiêu không có GPU tương thích thì sao? Thay vì bị crash, bạn có thể phát hiện tình huống và chuyển sang xử lý bằng CPU.

```csharp
        // Detect GPU availability – fallback if needed
        if (!ocrEngine.IsGpuAvailable)
        {
            Console.WriteLine("GPU not detected, falling back to CPU mode.");
            ocrEngine.Settings.ProcessingMode = ProcessingMode.Cpu;
        }
```

**Tại sao cần có phần này?**  
Trong các pipeline CI hoặc container đám mây, bạn thường chạy trên server không có GPU. Việc giảm dần một cách nhẹ nhàng đảm bảo cùng một đoạn mã hoạt động ở mọi nơi.

---

## Những Sai Lầm Thường Gặp và Mẹo Thực Tiễn

| Sai Lầm | Cách Tránh |
|---------|------------|
| Quên đặt `ProcessingMode` trước khi tải ảnh. | Luôn cấu hình engine trước (Bước 1). |
| Dùng chỉ mục GPU sai (`GpuDeviceId`). | Truy vấn các thiết bị khả dụng hoặc dùng mặc định `0`. |
| Tải ảnh độ phân giải thấp, làm giảm độ chính xác OCR. | Đảm bảo ít nhất 300 DPI cho biên lai. |
| Không giải phóng `ImageStream` – gây khóa tệp. | Đặt stream trong khối `using` hoặc gọi `Dispose()` thủ công. |
| Bỏ qua cờ `IsGpuAvailable` trên máy không có CUDA. | Thêm logic fallback từ Bước 5. |

---

## Ví Dụ Hoàn Chỉnh (Sẵn Sàng Sao Chép‑Dán)

Dưới đây là toàn bộ chương trình, sẵn sàng biên dịch. Lưu dưới tên `Program.cs`, thêm gói NuGet Aspose OCR, và chạy.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;

class GpuDemo
{
    static void Main()
    {
        // ---------- Step 1: Set GPU device ----------
        var ocrEngine = new OcrEngine();
        ocrEngine.Settings.ProcessingMode = ProcessingMode.Gpu; // set GPU device
        ocrEngine.Settings.GpuDeviceId = 0; // use the first GPU (change if needed)

        // Optional: fallback if GPU isn't present
        if (!ocrEngine.IsGpuAvailable)
        {
            Console.WriteLine("GPU not detected, switching to CPU.");
            ocrEngine.Settings.ProcessingMode = ProcessingMode.Cpu;
        }

        // ---------- Step 2: Load image for OCR ----------
        var imagePath = @"C:\OCR\Samples\receipt_highres.png";
        if (!System.IO.File.Exists(imagePath))
        {
            Console.WriteLine($"File not found: {imagePath}");
            return;
        }
        var imageStream = ImageStream.FromFile(imagePath);

        // ---------- Step 3: Recognize receipt image ----------
        var ocrResult = ocrEngine.Recognize(imageStream);

        // ---------- Step 4: Extract text from image ----------
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine("==================");
    }
}
```

Chạy chương trình sẽ in ra văn bản biên lai đã được trích xuất trên console, giống như ví dụ ở trên. Bạn có thể truyền chuỗi này vào bộ phân tích, cơ sở dữ liệu, hoặc bất kỳ logic kinh doanh nào khác.

---

## Kết Luận

Chúng tôi đã chỉ cho bạn cách **set GPU device** trong Aspose OCR, **load image for OCR**, và **recognize receipt image** để bạn có thể **extract text from image** với tốc độ cực nhanh. Ví dụ đầy đủ, có thể chạy ngay cho thấy cả “cách làm” và “tại sao”, cung cấp nền tảng vững chắc cho bất kỳ dự án C# OCR nào cần tăng tốc GPU.

Sẵn sàng cho bước tiếp theo? Hãy thử:

* Xử lý nhiều ảnh đồng thời bằng `Parallel.ForEach`.  
* Điều chỉnh `ocrEngine.Settings.PreprocessMode` để cải thiện kết quả trên các bản quét ít tương phản.  
* Xuất kết quả OCR ra JSON để phân tích tiếp theo.  

Nếu gặp khó khăn, hãy để lại bình luận, và chúc bạn lập trình vui vẻ!

![Sơ đồ minh họa cách đặt thiết bị GPU cho quá trình xử lý OCR](set-gpu-device.png "set GPU device")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}