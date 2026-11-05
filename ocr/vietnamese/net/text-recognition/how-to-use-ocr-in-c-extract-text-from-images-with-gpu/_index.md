---
category: general
date: 2026-02-13
description: Học cách sử dụng OCR trong C# để trích xuất văn bản từ các tệp hình ảnh,
  kích hoạt xử lý GPU và chuyển đổi các bản quét thành văn bản nhanh chóng.
draft: false
keywords:
- how to use OCR
- extract text from image
- how to extract text
- convert scan to text
- enable gpu processing
language: vi
og_description: Cách sử dụng OCR trong C#? Hướng dẫn này chỉ cho bạn cách trích xuất
  văn bản từ các tệp hình ảnh, bật xử lý GPU và chuyển đổi các bản quét thành văn
  bản.
og_title: Cách sử dụng OCR trong C# – Trích xuất văn bản từ hình ảnh bằng GPU
tags:
- OCR
- C#
- Aspose
- GPU
- Image Processing
title: Cách sử dụng OCR trong C# – Trích xuất văn bản từ hình ảnh bằng GPU
url: /vi/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-images-with-gpu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Sử Dụng OCR trong C# – Trích Xuất Văn Bản từ Hình Ảnh với GPU

Bạn có bao giờ tự hỏi **cách sử dụng OCR** để lấy văn bản từ tài liệu đã quét mà không gặp khó khăn không? Bạn không phải là người duy nhất—các nhà phát triển liên tục hỏi, “Làm sao tôi có thể trích xuất văn bản từ các tệp hình ảnh một cách hiệu quả?” Tin tốt là với Aspose.OCR bạn có thể làm chính xác điều đó, và thậm chí **kích hoạt xử lý GPU** để tăng tốc đáng kể trên phần cứng hỗ trợ.

Trong hướng dẫn này, chúng ta sẽ đi qua một ví dụ hoàn chỉnh, từ đầu đến cuối, cho bạn thấy **cách sử dụng OCR**, cách **trích xuất văn bản từ hình ảnh**, cách **chuyển đổi quét thành văn bản**, và cách xử lý khi GPU không khả dụng. Khi kết thúc, bạn sẽ có một ứng dụng console C# sẵn sàng chạy, in ra văn bản đã nhận dạng và cho biết GPU có thực sự được sử dụng hay không.

## Những Gì Bạn Cần Chuẩn Bị

- .NET 6 SDK hoặc phiên bản mới hơn (mã cũng chạy được với .NET Core)  
- Visual Studio 2022 hoặc bất kỳ trình soạn thảo nào bạn thích  
- Gói Aspose.OCR cho .NET (có sẵn qua NuGet)  
- Một tệp hình ảnh độ phân giải cao (ví dụ: `highres_scan.tif`) để thử nghiệm  

Không cần cài đặt phức tạp—chỉ vài lệnh NuGet và bạn đã sẵn sàng.

## Bước 1: Cài Đặt Aspose.OCR và Chuẩn Bị Dự Án

Đầu tiên, bạn cần đưa thư viện OCR vào dự án. Mở terminal trong thư mục solution và chạy:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
dotnet add package Aspose.OCR
```

Lệnh này sẽ tạo một dự án console mới có tên **OcrDemo** và thêm gói NuGet `Aspose.OCR`. Thư viện này chứa lớp `OcrEngine` mà chúng ta sẽ sử dụng.

> **Mẹo chuyên nghiệp:** Nếu máy của bạn có GPU riêng, hãy chắc chắn rằng driver đồ họa mới nhất đã được cài đặt; nếu không, thư viện sẽ tự động chuyển sang chế độ CPU.

## Bước 2: Viết Toàn Bộ Mã OCR

Bây giờ mở `Program.cs` và thay thế nội dung của nó bằng đoạn dưới đây. Mỗi dòng đều có chú thích để bạn hiểu *tại sao* chúng ta làm như vậy.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣  Create an OCR engine and request GPU processing.
            //    If the GPU isn’t present, Aspose.OCR will silently
            //    switch to CPU mode – no crash, no extra code needed.
            // -------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                ProcessingMode = OcrProcessingMode.Gpu
            };

            // -------------------------------------------------
            // 2️⃣  Define the path to the image you want to process.
            //    Replace the placeholder with the actual file location.
            // -------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY/highres_scan.tif";

            // -------------------------------------------------
            // 3️⃣  Perform the recognition. The method returns an
            //    OcrResult object that contains the extracted text,
            //    confidence scores, and more.
            // -------------------------------------------------
            OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

            // -------------------------------------------------
            // 4️⃣  Report whether the GPU was really used.
            //    This is handy for debugging performance issues.
            // -------------------------------------------------
            Console.WriteLine($"GPU used: {ocrEngine.IsGpuEnabled}");

            // -------------------------------------------------
            // 5️⃣  Output the recognized text to the console.
            //    In a real app you might write this to a file,
            //    a database, or feed it into another workflow.
            // -------------------------------------------------
            Console.WriteLine("=== Extracted Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

### Tại Sao Cách Này Hoạt Động

- **ProcessingMode = Gpu** yêu cầu engine thử GPU trước. Thư viện ẩn đi các lời gọi CUDA/OpenCL cấp thấp, vì vậy bạn không cần quản lý ngữ cảnh thiết bị thủ công.  
- **IsGpuEnabled** là một biến boolean xác nhận liệu đường dẫn GPU có thành công hay không. Nếu bạn thấy `false`, engine đã tự động chuyển sang CPU—không có gì đáng lo.  
- **RecognizeImage** thực hiện toàn bộ công việc nặng: tải hình ảnh, chạy mô hình OCR và trả về kết quả dạng văn bản thuần. Không cần tiền xử lý bitmap trừ khi bạn có yêu cầu đặc biệt (ví dụ: chỉnh nghiêng).

## Bước 3: Chạy Ứng Dụng và Kiểm Tra Kết Quả

Biên dịch và thực thi:

```bash
dotnet run
```

Nếu mọi thứ được cấu hình đúng, bạn sẽ thấy đầu ra giống như:

```
GPU used: True
=== Extracted Text ===
This is the first line of the scanned document.
Here is the second line, and so on…
```

Nếu GPU không khả dụng, dòng đầu tiên sẽ hiển thị `GPU used: False`, nhưng văn bản đã trích xuất vẫn sẽ xuất hiện—nhờ cơ chế chuyển đổi mượt mà.

> **Câu hỏi thường gặp:** *Nếu hình ảnh của tôi là JPEG thay vì TIFF thì sao?*  
> Phương thức `RecognizeImage` chấp nhận bất kỳ định dạng nào được .NET `System.Drawing` hỗ trợ (JPEG, PNG, BMP, v.v.). Chỉ cần thay đổi phần mở rộng tệp trong `imagePath`.

## Bước 4: Tùy Chỉnh Cài Đặt Để Độ Chính Xác Cao Hơn

Aspose.OCR cung cấp một vài tùy chọn bạn có thể điều chỉnh:

| Setting | What it Does | When to Use |
|---------|--------------|-------------|
| `ocrEngine.Language` | Buộc sử dụng một ngôn ngữ cụ thể (ví dụ: `OcrLanguage.English`) | Khi bạn biết ngôn ngữ của tài liệu |
| `ocrEngine.PageSegMode` | Kiểm soát cách engine chia trang thành các khối | Đối với bố cục đa cột |
| `ocrEngine.DetectOrientation` | Tự động xoay văn bản không thẳng đứng | Các bản quét có thể bị lộn ngược |

Bạn có thể đặt các thuộc tính này trước khi gọi `RecognizeImage`. Ví dụ:

```csharp
ocrEngine.Language = OcrLanguage.English;
ocrEngine.DetectOrientation = true;
```

## Bước 5: Trực Quan Hóa Quy Trình (Hình Ảnh Với Alt Text)

Dưới đây là một sơ đồ đơn giản minh họa **cách sử dụng OCR** với tùy chọn tăng tốc GPU. Nó không bắt buộc để mã chạy, nhưng giúp bạn nắm bắt bức tranh tổng thể.

![Sơ đồ cho thấy cách sử dụng OCR với xử lý GPU](/images/ocr-gpu-flow.png)

*Alt text:* *Sơ đồ cho thấy cách sử dụng OCR với xử lý GPU, làm nổi bật việc chuyển sang CPU khi cần thiết.*

## Các Trường Hợp Cạnh & Khắc Phục Sự Cố

1. **Thiếu Bộ Nhớ trên GPU** – Các hình ảnh rất lớn có thể vượt quá dung lượng bộ nhớ GPU. Khi đó, thư viện sẽ tự động quay lại CPU. Bạn có thể thu nhỏ hình ảnh trước để giảm mức tiêu thụ bộ nhớ.  
2. **Định Dạng Hình Ảnh Không Hỗ Trợ** – Nếu `RecognizeImage` ném ra *NotSupportedException*, hãy kiểm tra phần mở rộng tệp và đảm bảo hình ảnh không bị hỏng. Chuyển sang PNG thường giải quyết được vấn đề.  
3. **Điểm Tin Cậy Thấp** – Khi kết quả OCR chứa nhiều ký tự không đọc được, hãy cân nhắc tiền xử lý (nhị phân hoá, loại bỏ nhiễu) hoặc chuyển sang bản quét có độ phân giải cao hơn.  

## Tổng Kết: Những Gì Chúng Ta Đã Đạt Được

Chúng ta vừa **đi qua cách sử dụng OCR** trong một ứng dụng console C#, minh họa cách **trích xuất văn bản từ hình ảnh**, và cho bạn thấy cách **kích hoạt xử lý GPU** để có kết quả nhanh hơn. Bây giờ bạn **biết cách chuyển đổi quét thành văn bản**, kiểm tra xem GPU có thực sự được dùng hay không, và điều chỉnh một vài thiết lập cho các trường hợp đặc biệt.

### Các Bước Tiếp Theo

- Thử đưa kết quả vào **công cụ tìm kiếm** (ví dụ: Elasticsearch) để các PDF đã quét của bạn có thể tìm kiếm được.  
- Thử nghiệm **xử lý hàng loạt**—lặp qua một thư mục các hình ảnh và ghi mỗi kết quả vào tệp `.txt`.  
- Kết hợp OCR với **API dịch thuật** để tự động dịch các tài liệu quét bằng ngôn ngữ nước ngoài.  

Có thêm câu hỏi? Hãy để lại bình luận, chúc bạn lập trình vui vẻ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}