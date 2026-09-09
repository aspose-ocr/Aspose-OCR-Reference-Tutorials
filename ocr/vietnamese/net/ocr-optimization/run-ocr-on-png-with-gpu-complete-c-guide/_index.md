---
category: general
date: 2026-01-02
description: Chạy OCR trên PNG nhanh chóng bằng Aspose OCR và hỗ trợ GPU. Tìm hiểu
  cách nhận dạng văn bản từ hình ảnh, trích xuất văn bản từ hình ảnh và đặt giới hạn
  bộ nhớ GPU.
draft: false
keywords:
- run OCR on PNG
- recognize text from image
- extract text from image
- how to extract text
- set GPU memory limit
language: vi
og_description: Chạy OCR trên PNG một cách hiệu quả bằng cách tận dụng Aspose OCR
  và tăng tốc GPU. Hướng dẫn này cho bạn cách nhận dạng văn bản từ hình ảnh, trích
  xuất văn bản từ hình ảnh và kiểm soát việc sử dụng bộ nhớ GPU.
og_title: Chạy OCR trên PNG với GPU – Hướng dẫn C# đầy đủ
tags:
- OCR
- C#
- GPU
title: Chạy OCR trên PNG với GPU – Hướng dẫn C# đầy đủ
url: /vi/net/ocr-optimization/run-ocr-on-png-with-gpu-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Chạy OCR trên PNG với GPU – Hướng dẫn đầy đủ C# 

Bạn đã bao giờ cần **run OCR on PNG** nhưng gặp khó khăn về hiệu năng? Bạn không phải là người duy nhất. Trong nhiều quy trình thực tế, một tệp PNG độ phân giải cao có thể làm chậm engine OCR chỉ dùng CPU, biến việc tra cứu nhanh thành một phút chờ đợi.  

Tin tốt là Aspose OCR đi kèm với các phần mở rộng GPU cho phép bạn **recognize text from image** trong một phần nhỏ thời gian. Trong hướng dẫn này, chúng tôi sẽ trình bày một ví dụ thực tế cho bạn thấy cách **run OCR on PNG** bằng C#, cách **extract text from image**, và thậm chí cách **set GPU memory limit** để bạn giữ trong giới hạn phần cứng.  

Chúng tôi cũng sẽ đề cập đến “cách” và “tại sao của mỗi bước, để bạn có mô hình tư duy vững chắc — không chỉ là một đoạn mã copy‑paste.

## Những gì bạn sẽ học

- Các điều kiện tiên quyết để sử dụng hỗ trợ GPU của Aspose OCR.  
- Cách tải một PNG vào `Bitmap` và đưa nó vào engine OCR.  
- Cách cấu hình `GpuDevice` và `GpuMemoryLimitMb` để đạt hiệu suất tối ưu.  
- Cách **recognize text from image** và lấy kết quả văn bản thuần.  
- Mẹo xử lý các trường hợp đặc biệt thường gặp như GPU bộ nhớ thấp hoặc PNG đa trang.  

Khi kết thúc hướng dẫn này, bạn sẽ có thể **run OCR on PNG** với tốc độ GPU và tự tin kiểm soát dung lượng bộ nhớ của các công việc OCR.

![Sơ đồ cho việc chạy OCR trên PNG với tăng tốc GPU](run-ocr-on-png-diagram.png "ví dụ chạy OCR trên PNG")

## Yêu cầu trước

Trước khi bắt đầu, hãy chắc chắn bạn có:

1. .NET 6.0 hoặc mới hơn (mã hoạt động với .NET Core và .NET Framework cũng được).  
2. GPU NVIDIA có hỗ trợ CUDA (ví dụ này chọn chỉ mục thiết bị 0).  
3. Gói NuGet Aspose.OCR và các phần mở rộng GPU của nó (`Aspose.OCR.Extensions`).  
4. Một tệp PNG mẫu (`input.png`) đặt trong thư mục bạn có thể tham chiếu từ dự án.  

Nếu bất kỳ mục nào trên không quen thuộc, đừng lo — chúng tôi sẽ ghi chú các lựa chọn thay thế khi cần.

---

## Bước 1 – Cài đặt Aspose OCR và các phần mở rộng GPU

Đầu tiên, không có các thư viện đúng, phần còn lại của mã sẽ không biên dịch được.

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Extensions
```

`Aspose.OCR.Extensions` package sẽ kéo các binary CUDA gốc cần thiết cho tăng tốc GPU.  
*Mẹo:* Nếu bạn đang trên máy không có GPU, vẫn có thể biên dịch dự án; chỉ cần đặt `PreferGpu = false` sau này.

---

## Bước 2 – Tải PNG bạn muốn xử lý

Bây giờ chúng ta thực sự **run OCR on PNG** bằng cách tải nó vào `Bitmap`. Bước này đơn giản nhưng cần lưu ý: `Bitmap` yêu cầu một đường dẫn tệp, vì vậy hãy chắc chắn đường dẫn đúng tương đối với tệp thực thi của bạn.

```csharp
using System.Drawing;        // Bitmap handling
using Aspose.OCR;
using Aspose.OCR.Extensions; // GPU support extensions

// ...

// Step 2: Load the PNG image
string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "YOUR_DIRECTORY", "input.png");
Bitmap imageBitmap = new Bitmap(imagePath);
```

Nếu PNG có kích thước bất thường lớn (ví dụ, > 5000 px một cạnh), bạn có thể muốn giảm kích thước trước để tránh tiêu thụ hết bộ nhớ GPU. Đó là lúc tùy chọn **set GPU memory limit** trở nên hữu ích sau này.

---

## Bước 3 – Tạo và cấu hình Engine OCR để sử dụng GPU

Đây là phần cốt lõi của hướng dẫn: cấu hình engine OCR để **recognize text from image** bằng GPU. Hai thuộc tính quan trọng:

- `GpuDevice` – chọn thiết bị CUDA nào sẽ dùng.  
- `GpuMemoryLimitMb` – giới hạn lượng bộ nhớ GPU mà engine có thể cấp phát.

```csharp
// Step 3: Initialize OCR engine with GPU settings
OcrEngine ocrEngine = new OcrEngine()
{
    // Pick the first CUDA device (index 0)
    GpuDevice = GpuDeviceInfo.GetDevice(0),

    // Optional: limit GPU memory consumption (in MB)
    GpuMemoryLimitMb = 2048   // Adjust based on your GPU's VRAM
};
```

**Tại sao cần đặt giới hạn bộ nhớ?** Một số GPU chia sẻ bộ nhớ với màn hình hoặc chạy nhiều tải cùng lúc. Bằng cách giới hạn việc cấp phát, bạn ngăn được lỗi hết bộ nhớ, đặc biệt khi xử lý nhiều PNG song song.

---

## Bước 4 – Định nghĩa tùy chọn nhận dạng (Ngôn ngữ & Ưu tiên GPU)

Đối tượng `RecognitionOptions` cho engine biết ngôn ngữ cần tìm và có **prefer GPU** ngay cả với ảnh nhỏ. Đối với hầu hết tài liệu tiếng Anh, điều này đủ, nhưng bạn có thể thay `Language.English` bằng các locale hỗ trợ khác.

```csharp
// Step 4: Set recognition options
RecognitionOptions recognitionOptions = new RecognitionOptions
{
    Language = Language.English,
    PreferGpu = true // Force GPU path even for smaller images
};
```

Nếu bạn cần **extract text from image** bằng ngôn ngữ khác ngoài tiếng Anh, chỉ cần thay đổi enum `Language`. Thư viện hỗ trợ hàng chục ngôn ngữ ngay từ đầu.

---

## Bước 5 – Chạy OCR và lấy kết quả

Khi mọi thứ đã được kết nối, lời gọi cuối cùng chỉ một dòng duy nhất thực sự **run OCR on PNG** và trả về một đối tượng kết quả phong phú.

```csharp
// Step 5: Perform OCR
OcrResult ocrResult = ocrEngine.Recognize(imageBitmap, recognitionOptions);

// Output the extracted text
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

`OcrResult` không chỉ chứa văn bản thuần (`ocrResult.Text`) mà còn có điểm tin cậy, hộp bao, và thậm chí hình ảnh gốc với các từ được đánh dấu — hữu ích nếu bạn cần gỡ lỗi hoặc trực quan hoá quá trình trích xuất.

**Kết quả mong đợi** (cho một PNG mẫu có chữ “Hello World”):

```
=== OCR Output ===
Hello World
```

Nếu văn bản xuất hiện rối, hãy kiểm tra lại PNG không bị hỏng và giới hạn bộ nhớ GPU không quá thấp so với kích thước ảnh.

---

## Bước 6 – Xử lý các trường hợp đặc biệt và mẹo thực hành tốt

### GPU bộ nhớ thấp

Nếu bạn gặp ngoại lệ như `CudaException: out of memory`, giảm `GpuMemoryLimitMb` hoặc chia PNG thành các ô trước khi xử lý. Việc chia ô có thể thực hiện bằng `Graphics.DrawImage` trên một bản sao `Bitmap`.

### Nhiều PNG trong một lô

Khi xử lý một thư mục chứa nhiều PNG, hãy tái sử dụng cùng một thể hiện `OcrEngine` — khởi tạo một lần giúp giảm việc chuyển đổi ngữ cảnh GPU.

```csharp
foreach (var file in Directory.GetFiles("images", "*.png"))
{
    using var bmp = new Bitmap(file);
    var result = ocrEngine.Recognize(bmp, recognitionOptions);
    Console.WriteLine($"{Path.GetFileName(file)}: {result.Text}");
}
```

### Quay lại CPU

Nếu không có GPU, chỉ cần đặt `PreferGpu = false`. Engine sẽ tự động quay lại CPU mà không cần thay đổi mã.

```csharp
recognitionOptions.PreferGpu = false; // Safe CPU path
```

---

## Ví dụ làm việc đầy đủ

Dưới đây là chương trình hoàn chỉnh bạn có thể copy‑paste vào một dự án console mới. Nó bao gồm tất cả các bước trên, cộng thêm một vài kiểm tra an toàn.

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Extensions; // GPU support extensions

class GpuExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the PNG image
        // -------------------------------------------------
        string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory,
                                         "YOUR_DIRECTORY", "input.png");

        if (!File.Exists(imagePath))
        {
            Console.Error.WriteLine($"File not found: {imagePath}");
            return;
        }

        using Bitmap imageBitmap = new Bitmap(imagePath);

        // -------------------------------------------------
        // Step 2: Initialize OCR engine with GPU settings
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine()
        {
            GpuDevice = GpuDeviceInfo.GetDevice(0), // First CUDA device
            GpuMemoryLimitMb = 2048                  // Adjust as needed
        };

        // -------------------------------------------------
        // Step 3: Set recognition options
        // -------------------------------------------------
        RecognitionOptions recognitionOptions = new RecognitionOptions
        {
            Language = Language.English,
            PreferGpu = true // Force GPU even for small images
        };

        // -------------------------------------------------
        // Step 4: Perform OCR
        // -------------------------------------------------
        OcrResult ocrResult = ocrEngine.Recognize(imageBitmap, recognitionOptions);

        // -------------------------------------------------
        // Step 5: Output the extracted text
        // -------------------------------------------------
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

Lưu tệp dưới tên `Program.cs`, chạy `dotnet run`, và bạn sẽ thấy văn bản đã trích xuất được in ra console.

---

## Kết luận

Chúng tôi vừa trình diễn cách **run OCR on PNG** bằng các phần mở rộng GPU của Aspose OCR, cách **recognize text from image**, và cách **extract text from image** đồng thời kiểm soát **set GPU memory limit**. Bằng cách cấu hình `GpuDevice` và `GpuMemoryLimitMb` bạn giữ cho ứng dụng nhanh và ổn định, ngay cả trên các GPU khiêm tốn.

Từ đây bạn có thể:

- Thử nghiệm các ngôn ngữ khác (`Language.French`, `Language.Spanish`).  
- Tích hợp bước OCR vào một pipeline xử lý tài liệu lớn hơn.  
- Thêm xử lý hậu kỳ như kiểm tra chính tả hoặc trích xuất thực thể để làm sạch văn bản thô.  

Hãy nhớ, chìa khóa không chỉ là mã mà còn là hiểu vì sao mỗi thiết lập quan trọng. Khi bạn biết cách **set GPU memory limit** và khi nào nên quay lại CPU, bạn sẽ xây dựng các giải pháp OCR mở rộng một cách linh hoạt.

Có câu hỏi về kích thước PNG cụ thể, TIFF đa trang, hoặc khắc phục lỗi GPU? Hãy để lại bình luận bên dưới, chúc bạn lập trình vui!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}