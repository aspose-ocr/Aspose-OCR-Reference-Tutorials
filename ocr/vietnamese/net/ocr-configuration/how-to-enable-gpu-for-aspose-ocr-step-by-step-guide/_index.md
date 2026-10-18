---
category: general
date: 2026-09-08
description: Tìm hiểu cách bật GPU cho Aspose OCR, thực hiện xử lý OCR hàng loạt và
  trích xuất văn bản từ hình ảnh một cách hiệu quả bằng .NET.
draft: false
keywords:
- how to enable gpu
- extract text from images
- batch ocr processing
- ocr gpu acceleration
- aspose ocr .net
lastmod: 2026-09-08
og_description: Cách bật GPU cho Aspose OCR. Hướng dẫn này trình bày việc xử lý OCR
  hàng loạt, trích xuất văn bản từ hình ảnh và chọn thiết bị GPU tối ưu trong .NET.
og_image_alt: Diagram of Aspose OCR engine offloading work to GPU for faster text
  extraction
og_title: Cách bật GPU cho Aspose OCR – hướng dẫn đầy đủ
schemas:
- author: Aspose
  dateModified: '2026-09-08'
  description: Learn how to enable GPU for Aspose OCR, run batch OCR processing, and
    extract text from images efficiently using .NET.
  headline: How to enable GPU for Aspose OCR – complete tutorial
  type: TechArticle
- description: Learn how to enable GPU for Aspose OCR, run batch OCR processing, and
    extract text from images efficiently using .NET.
  name: How to enable GPU for Aspose OCR – complete tutorial
  steps:
  - name: 'Install the NuGet package: `dotnet add package Aspose.OCR --version 23.10.0`'
    text: 'Install the NuGet package: `dotnet add package Aspose.OCR --version 23.10.0`'
  - name: Replace the paths in `imageFiles` with the location of your own `.tif` files.
    text: Replace the paths in `imageFiles` with the location of your own `.tif` files.
  - name: 'Build and run: `dotnet run`.'
    text: 'Build and run: `dotnet run`.'
  type: HowTo
- questions:
  - answer: Yes, a commercial Aspose.OCR license is needed for production deployments;
      a free trial is available for evaluation.
    question: Is a license required for production use?
  - answer: Any NVIDIA GPU that supports CUDA 11.0 or newer, such as RTX 2060, RTX
      3070, RTX 4090, and the corresponding Tesla series.
    question: Which GPU models are officially supported?
  - answer: Absolutely. The same `OcrEngine` instance can be reused across requests;
      just ensure thread safety by cloning the engine per request.
    question: Can I run this code in an ASP.NET Core web API?
  - answer: Yes, you can set `ocrEngine.Language = Language.English | Language.Spanish`
      to enable simultaneous recognition of multiple languages.
    question: Does Aspose OCR handle multi‑language documents?
  - answer: The engine streams image data, so you can process images up to 10,000
      × 10,000 pixels without exhausting GPU memory, though performance may vary.
    question: What is the maximum image size the GPU can handle?
  type: FAQPage
tags:
- Aspose OCR
- GPU acceleration
- C#
- .NET
title: Cách bật GPU cho Aspose OCR – hướng dẫn đầy đủ
url: /vi/net/ocr-configuration/how-to-enable-gpu-for-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách bật GPU cho Aspose OCR – hướng dẫn đầy đủ

Bạn đã bao giờ tự hỏi **cách bật GPU** khi sử dụng Aspose OCR chưa? Bạn không phải là người duy nhất—các nhà phát triển phải xử lý khối lượng tài liệu khổng lồ thường gặp rào cản hiệu năng vì engine OCR bị kẹt ở CPU. Tin tốt là gì? Bật tăng tốc GPU khá đơn giản và có thể giảm vài giây cho mỗi trang. Trong hướng dẫn này chúng tôi sẽ chỉ cho bạn **cách bật GPU**, chạy **xử lý OCR hàng loạt**, trích xuất văn bản đã nhận dạng, và thậm chí chọn thiết bị GPU phù hợp. Khi kết thúc, bạn sẽ biết **cách sử dụng Aspose** để trích xuất văn bản OCR nhanh như chớp.

## Câu trả lời nhanh
- **Việc bật GPU làm gì?** Nó chuyển việc phân tích mức pixel sang card đồ họa, giảm thời gian xử lý tới 80 % trên các ảnh 300 dpi tiêu chuẩn.  
- **Tôi có cần giấy phép đặc biệt không?** Không, gói NuGet Aspose.OCR tiêu chuẩn đã bao gồm hỗ trợ GPU.  
- **Phiên bản .NET nào được yêu cầu?** .NET 6.0 trở lên; API sử dụng các tính năng C# hiện đại.  
- **Tôi có thể chạy trên máy chỉ có CPU không?** Có — nếu không tìm thấy GPU tương thích, engine sẽ tự động chuyển sang CPU.  
- **Tôi có thể xử lý bao nhiêu ảnh cùng lúc?** Bạn có thể xếp hàng hàng trăm tệp; GPU sẽ xử lý chúng tuần tự trong khi mã của bạn có thể đưa ảnh tiếp theo ngay khi ảnh trước hoàn thành.

## Cái gì là cách bật GPU?
`how to enable GPU` là quá trình cấu hình Aspose OCR’s `OcrEngine` để chuyển tải công việc xử lý ảnh sang card đồ họa tương thích CUDA thay vì bộ xử lý trung tâm. Công tắc này được điều khiển bởi hai thuộc tính: `UseGpu` và `GpuDeviceId`. Bật cờ này chuyển việc phân tích pixel tốn kém sang GPU, nơi có thể xử lý hàng nghìn luồng song song, giảm đáng kể thời gian xử lý.

Lớp `OcrEngine` là thành phần cốt lõi của Aspose OCR thực hiện phân tích ảnh và nhận dạng văn bản.

## Tại sao nên sử dụng tăng tốc GPU với Aspose OCR?
Aspose OCR hỗ trợ **hơn 50 định dạng ảnh đầu vào** và có thể xử lý các lô hàng trăm trang mà không cần tải toàn bộ tài liệu vào bộ nhớ. Khi bật tăng tốc GPU, các bài kiểm tra benchmark cho thấy **giảm 70 %‑80 %** thời gian xử lý trung bình mỗi trang trên RTX 3080 so với chỉ dùng CPU. Tốc độ tăng lên giúp giảm chi phí đám mây và mang lại kết quả nhanh hơn cho người dùng trong các ứng dụng xử lý tài liệu mạnh.

## Yêu cầu trước
- .NET 6.0 trở lên (mã sử dụng cú pháp C# hiện đại)  
- Gói NuGet Aspose.OCR cho .NET (phiên bản 23.10 hoặc mới hơn)  
- GPU tương thích CUDA với driver phù hợp đã cài đặt (tối thiểu CUDA 11.0)  
- Thư mục chứa các tệp mẫu `.tif` để chạy batch  

Nếu bạn đã có những điều cơ bản này, hãy cùng bắt đầu.

## Cách bật GPU trong Aspose OCR

Tải engine OCR, bật chế độ GPU, và tùy chọn chọn chỉ số thiết bị.  

`OcrEngine` là lớp cốt lõi của Aspose OCR thực hiện phân tích ảnh và nhận dạng văn bản.  

Bật GPU là một thao tác hai bước: đặt `UseGpu = true` và, khi có nhiều GPU, chỉ định `GpuDeviceId` mong muốn. Đoạn văn trả lời trực tiếp này giải thích toàn bộ quy trình trong 45 từ.

Điều đầu tiên bạn cần làm là thông báo cho `OcrEngine` sử dụng GPU. Điều này được thực hiện qua hai thuộc tính đơn giản: `UseGpu` và tùy chọn `GpuDeviceId`. Đặt `UseGpu` thành `true` sẽ chuyển engine sang chế độ GPU, trong khi `GpuDeviceId` cho phép bạn chọn GPU nào (nếu có hơn một) sẽ thực hiện công việc nặng.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑specific namespace
using System;
using System.Collections.Generic;

// Step 1: Create the OCR engine and enable GPU acceleration
var ocrEngine = new OcrEngine
{
    // Turn on GPU support – this is the core of “how to enable gpu”
    UseGpu = true,

    // (optional) Choose GPU index 0; change if you have multiple devices
    GpuDeviceId = 0
};
```

> **Tại sao điều này quan trọng** – Phiên bản CPU xử lý từng pixel một cách tuần tự, có thể trở thành nút thắt cho các ảnh độ phân giải cao. Phiên bản GPU chạy hàng nghìn luồng song song, giảm đáng kể thời gian mỗi trang.

### Tổng quan trực quan  

![Sơ đồ cho thấy cách engine OCR chuyển tải công việc sang GPU khi “cách bật gpu” được thiết lập](/images/enable-gpu-diagram.png){: .center .responsive alt="cách bật gpu"}

[Sơ đồ cho thấy cách engine OCR chuyển tải công việc sang GPU khi “cách bật gpu” được thiết lập](/images/enable-gpu-diagram.png)

*(Nếu bạn không thể xem hình ảnh, hãy tưởng tượng một sơ đồ luồng nơi engine OCR chuyển bộ đệm ảnh cho lõi CUDA.)*

## Cách chạy xử lý OCR hàng loạt với Aspose

Phương thức `Recognize` của `OcrEngine` xử lý một ảnh và trả về `OcrResult` chứa văn bản đã trích xuất và siêu dữ liệu. Bạn có thể xử lý toàn bộ thư mục bằng cách lặp qua danh sách các đường dẫn tệp. Engine tự động xếp hàng mỗi ảnh vào GPU, giữ pipeline bận rộn trong khi ứng dụng của bạn tiếp tục cung cấp các tệp mới. Cách tiếp cận này cho phép bạn xử lý hàng trăm tệp TIFF một cách hiệu quả, với GPU thực hiện công việc nặng song song.

```csharp
// Step 2: Define the image files you want to process
var imageFiles = new List<string>
{
    @"C:\OCRSamples\page1.tif",
    @"C:\OCRSamples\page2.tif",
    @"C:\OCRSamples\page3.tif"
};

// Step 3: Process each image and report the character count
foreach (var imagePath in imageFiles)
{
    // Recognize the image – the GPU does the heavy lifting behind the scenes
    var ocrResult = ocrEngine.Recognize(imagePath);

    // Show how many characters were extracted – a quick sanity check
    Console.WriteLine($"{imagePath}: {ocrResult.Text.Length} characters");
}
```

> **Mẹo chuyên nghiệp** – Đối với các lô rất lớn, hãy cân nhắc sử dụng `Parallel.ForEach` kết hợp với `ocrEngine.Clone()` để tránh các vấn đề về an toàn luồng. Phương thức `Clone` tạo một bản sao nông của engine nhưng vẫn trỏ tới cùng một ngữ cảnh GPU.

### Kết quả mong đợi

```
C:\OCRSamples\page1.tif: 1245 characters
C:\OCRSamples\page2.tif: 1130 characters
C:\OCRSamples\page3.tif: 1389 characters
```

Nếu các số liệu có vẻ hợp lý, **xử lý OCR hàng loạt** của bạn đang hoạt động và GPU đang được sử dụng.

## Cách trích xuất văn bản từ ảnh – nhận kết quả

`OcrResult` là đối tượng chứa đầu ra OCR, bao gồm văn bản đã nhận dạng, điểm tin cậy và thông tin bố cục. Phương thức `Recognize` trả về một đối tượng `OcrResult`. Lấy văn bản thuần từ thuộc tính `Text` và ghi nó vào tệp để sử dụng tiếp theo. Lưu trữ văn bản OCR cho phép xử lý downstream (lập chỉ mục tìm kiếm, khai thác dữ liệu, v.v.) mà không cần chạy lại engine và cung cấp bản ghi vĩnh viễn để gỡ lỗi.

```csharp
foreach (var imagePath in imageFiles)
{
    var ocrResult = ocrEngine.Recognize(imagePath);
    var extractedText = ocrResult.Text;

    // Save the text to a .txt file with the same base name
    var outputPath = System.IO.Path.ChangeExtension(imagePath, ".txt");
    System.IO.File.WriteAllText(outputPath, extractedText);

    Console.WriteLine($"Extracted text saved to {outputPath}");
}
```

> **Tại sao phải trích xuất ra tệp?** – Lưu trữ văn bản OCR cho phép xử lý downstream (lập chỉ mục tìm kiếm, khai thác dữ liệu, v.v.) mà không cần chạy lại engine. Nó cũng cung cấp bản ghi vĩnh viễn để gỡ lỗi.

## Cách đặt thiết bị GPU để đạt hiệu suất tối ưu

`CudaDeviceInfo` cung cấp thông tin về các GPU tương thích CUDA được cài đặt trên hệ thống. Khi có nhiều GPU, sử dụng `GpuDeviceId` để chọn GPU tốt nhất. Chỉ số này tương ứng với thứ tự trả về bởi `CudaDeviceInfo.GetDevices()`. Việc chọn thiết bị phù hợp đảm bảo bạn sử dụng GPU mạnh nhất và tránh xung đột với các tải công việc khác trên các card phụ.

```csharp
using Aspose.OCR.Gpu;

// List all available GPU devices
var devices = CudaDeviceInfo.GetDevices();
for (int i = 0; i < devices.Length; i++)
{
    Console.WriteLine($"Device {i}: {devices[i].Name} (Compute Capability {devices[i].ComputeCapability})");
}

// Suppose you want to use the second GPU (index 1)
ocrEngine.GpuDeviceId = 1;
Console.WriteLine($"Switched to GPU device {ocrEngine.GpuDeviceId}");
```

> **Trường hợp đặc biệt** – Một số GPU cũ không hỗ trợ phiên bản CUDA yêu cầu. Trong trường hợp đó, `UseGpu = true` sẽ tự động chuyển sang CPU mà không báo, vì vậy luôn kiểm tra `ocrEngine.IsGpuEnabled` sau khi khởi tạo.

## Cách sử dụng Aspose OCR trong dự án thực tế

Kết hợp tất cả lại, dưới đây là một ứng dụng console ngắn gọn, sẵn sàng chạy, minh họa **cách bật GPU**, chạy **xử lý OCR hàng loạt**, trích xuất văn bản, và cho phép bạn chọn thiết bị GPU. Mẫu tạo một `OcrEngine`, bật GPU, liệt kê các thiết bị khả dụng, xử lý từng ảnh, và ghi văn bản đã nhận dạng vào tệp `.txt` bên cạnh ảnh nguồn.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;
using System.Collections.Generic;
using System.IO;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Initialize OCR engine with GPU support
        // -------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            UseGpu = true,
            GpuDeviceId = 0 // change if you have multiple GPUs
        };

        // -------------------------------------------------
        // 2️⃣ (Optional) Show available GPU devices
        // -------------------------------------------------
        var devices = CudaDeviceInfo.GetDevices();
        Console.WriteLine("Available GPU devices:");
        for (int i = 0; i < devices.Length; i++)
        {
            Console.WriteLine($"  [{i}] {devices[i].Name} – Compute {devices[i].ComputeCapability}");
        }

        // -------------------------------------------------
        // 3️⃣ Define the batch of images to process
        // -------------------------------------------------
        var imageFiles = new List<string>
        {
            @"C:\OCRSamples\page1.tif",
            @"C:\OCRSamples\page2.tif",
            @"C:\OCRSamples\page3.tif"
        };

        // -------------------------------------------------
        // 4️⃣ Process each image, extract text, and save it
        // -------------------------------------------------
        foreach (var imagePath in imageFiles)
        {
            var result = ocrEngine.Recognize(imagePath);
            var text = result.Text;

            var txtPath = Path.ChangeExtension(imagePath, ".txt");
            File.WriteAllText(txtPath, text);

            Console.WriteLine($"{Path.GetFileName(imagePath)} → {Path.GetFileName(txtPath)} ({text.Length} chars)");
        }

        Console.WriteLine("All done! GPU‑accelerated OCR batch completed.");
    }
}
```

### Chạy mẫu

1. Cài đặt gói NuGet: `dotnet add package Aspose.OCR --version 23.10.0`  
2. Thay thế các đường dẫn trong `imageFiles` bằng vị trí các tệp `.tif` của bạn.  
3. Biên dịch và chạy: `dotnet run`.  

Bạn sẽ thấy danh sách các GPU, tiếp theo là một dòng cho mỗi ảnh báo số ký tự và đường dẫn của tệp `.txt` đã tạo.

## Câu hỏi thường gặp & lưu ý

- **Điều này có hoạt động trên máy chỉ có CPU không?**  
  Có — nếu `UseGpu` là `true` nhưng không tìm thấy GPU tương thích, Aspose sẽ tự động chuyển sang CPU. Bạn có thể xác nhận chế độ qua `ocrEngine.IsGpuEnabled`.

- **Nếu tôi nhận được lỗi “CUDA driver version is insufficient” thì sao?**  
  Cập nhật driver NVIDIA lên phiên bản mới nhất phù hợp với toolkit CUDA đi kèm Aspose. Thư viện yêu cầu ít nhất CUDA 11.0 cho các tính năng GPU mới.

- **Tôi có thể xử lý PDF trực tiếp không?**  
  Aspose OCR làm việc trên ảnh raster. Hãy chuyển các trang PDF sang ảnh trước (ví dụ, dùng Aspose.PDF) rồi đưa chúng vào engine OCR.

- **Làm thế nào để cải thiện độ chính xác trên các bản quét nhiễu?**  
  Bật các tùy chọn tiền xử lý như `ocrEngine.Preprocess = true` hoặc sử dụng ảnh độ phân giải cao hơn (300 dpi trở lên). Tăng tốc GPU vẫn được áp dụng.

## Câu hỏi thường gặp

**Q: Cần giấy phép cho việc sử dụng trong môi trường sản xuất không?**  
A: Có, cần giấy phép thương mại Aspose.OCR cho triển khai sản xuất; bản dùng thử miễn phí có sẵn để đánh giá.

**Q: Các mẫu GPU nào được hỗ trợ chính thức?**  
A: Bất kỳ GPU NVIDIA nào hỗ trợ CUDA 11.0 trở lên, chẳng hạn RTX 2060, RTX 3070, RTX 4090 và các dòng Tesla tương ứng.

**Q: Tôi có thể chạy mã này trong API web ASP.NET Core không?**  
A: Hoàn toàn có thể. Cùng một instance `OcrEngine` có thể được tái sử dụng qua các yêu cầu; chỉ cần đảm bảo an toàn luồng bằng cách clone engine cho mỗi yêu cầu.

**Q: Aspose OCR có xử lý tài liệu đa ngôn ngữ không?**  
A: Có, bạn có thể đặt `ocrEngine.Language = Language.English | Language.Spanish` để bật nhận dạng đồng thời nhiều ngôn ngữ.

**Q: Kích thước ảnh tối đa mà GPU có thể xử lý là bao nhiêu?**  
A: Engine truyền dữ liệu ảnh theo luồng, vì vậy bạn có thể xử lý ảnh lên tới 10.000 × 10.000 pixel mà không làm cạn bộ nhớ GPU, mặc dù hiệu năng có thể thay đổi.

**Last Updated:** 2026-09-08  
**Tested with:** Aspose.OCR 23.10 for .NET  
**Author:** Aspose

## Hướng dẫn liên quan

- [Cách sử dụng OCR trong C để trích xuất văn bản từ ảnh với tăng tốc GPU](/ocr/net/ocr-optimization/how-to-use-ocr-in-c-extract-text-from-images-with-gpu-accele/)
- [Trích xuất văn bản từ ảnh với Aspose OCR GPU C Guide](/ocr/net/ocr-optimization/extract-text-from-image-with-aspose-ocr-gpu-c-guide/)
- [Xóa nền OCR với Aspose OCR Hướng dẫn GPU hoàn chỉnh](/ocr/net/ocr-optimization/remove-background-ocr-with-aspose-ocr-complete-gpu-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}