---
category: general
date: 2026-03-07
description: Tìm hiểu cách chỉnh thẳng hình ảnh, tăng độ tương phản và trích xuất
  văn bản từ bản quét bằng Aspose OCR. Thực hiện OCR trên hình ảnh với ví dụ C# đầy
  đủ và dễ dàng tải hình ảnh để OCR.
draft: false
keywords:
- how to deskew image
- extract text from scan
- how to boost contrast
- perform ocr on image
- load image for OCR
language: vi
og_description: Tìm hiểu cách chỉnh nghiêng ảnh, tăng độ tương phản và trích xuất
  văn bản từ bản quét bằng Aspose OCR trong C#. Thực hiện OCR trên ảnh với mã hướng
  dẫn từng bước.
og_title: Cách chỉnh nghiêng ảnh và chạy OCR trong C# – Hướng dẫn đầy đủ
tags:
- C#
- OCR
- Image Processing
title: Cách chỉnh nghiêng ảnh và chạy OCR trong C# – Hướng dẫn toàn diện
url: /vi/net/ocr-optimization/how-to-deskew-image-and-run-ocr-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Cân Chỉnh Ảnh và Chạy OCR trong C# – Hướng Dẫn Toàn Diện

Nếu bạn từng thắc mắc **cách cân chỉnh ảnh** trước khi chạy OCR, bạn đang ở đúng nơi. Trong tutorial này chúng tôi sẽ hướng dẫn bạn tăng độ tương phản, tải ảnh lên để OCR, và cuối cùng **trích xuất văn bản từ bản quét** bằng Aspose OCR.  

Dù bạn đang số hoá các biên lai cũ, làm sạch hợp đồng đã quét, hay chỉ cần một cách đáng tin cậy để đọc văn bản từ một bức ảnh nghiêng, các bước dưới đây bao gồm mọi thứ bạn cần. Không có phần thừa—chỉ có một ví dụ hoạt động mà bạn có thể sao chép‑dán vào Visual Studio.  

## Những Điều Bạn Sẽ Đạt Được

Khi hoàn thành hướng dẫn này, bạn sẽ có thể:

* Sửa độ nghiêng lên tới 30° (đó là phần **cách cân chỉnh ảnh**).  
* Tăng độ tương phản ảnh để các ký tự sắc nét hơn (**cách tăng độ tương phản**).  
* Tải hình ảnh của bạn vào engine OCR (**tải ảnh cho OCR**).  
* Chạy quá trình nhận dạng và **trích xuất văn bản từ bản quét**.  

Tất cả đều hoạt động với gói NuGet Aspose.OCR .NET mới nhất (v23.11 tại thời điểm viết).  

---

![Ví dụ cách cân chỉnh ảnh](/images/deskew-example.png "cách cân chỉnh ảnh")

*Hình ảnh trên hiển thị một tài liệu đã quét trước và sau khi cân chỉnh.*

## Yêu Cầu Trước

* .NET 6.0 hoặc mới hơn (mã cũng chạy trên .NET Framework 4.7+).  
* Visual Studio 2022 (hoặc bất kỳ IDE C# nào bạn thích).  
* Gói NuGet Aspose.OCR – cài đặt bằng `dotnet add package Aspose.OCR`.  

Đó là tất cả. Không cần dịch vụ bên ngoài, không cần khóa API.

---

## Cách Cân Chỉnh Ảnh với Aspose OCR

Điều đầu tiên chúng ta làm là tạo một **ImageProcessingPipeline** và thêm một `DeskewFilter`. Bộ lọc này tự động phát hiện góc dòng văn bản chiếm ưu thế và xoay ảnh trở lại ngang.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Create the OCR engine
var ocrEngine = new OcrEngine();

// Build a pipeline – Deskew is the first filter
var processingPipeline = new ImageProcessingPipeline()
    .Add(new DeskewFilter { MaxAngle = 30 })   // how to deskew image up to 30°
    .Add(new DenoiseFilter { Level = DenoiseLevel.High }) // remove noise
    .Add(new ContrastBoostFilter { Strength = 1.5 })      // how to boost contrast
    .Add(new BinarizationFilter { Method = BinarizationMethod.Sauvola }); // binarize

// Attach the pipeline to the engine
ocrEngine.Settings.ImageProcessing = processingPipeline;
```

**Tại sao điều này quan trọng:**  
Một bản quét nghiêng làm rối loạn engine OCR vì các ký tự không còn căn chỉnh với đường cơ sở. `DeskewFilter` phân tích histogram của ảnh, tìm góc, và xoay ảnh, cải thiện đáng kể độ chính xác nhận dạng.

> **Mẹo chuyên nghiệp:** Nếu bạn biết tài liệu của mình không bao giờ nghiêng quá 15°, hãy đặt `MaxAngle = 15` để tăng tốc xử lý.

---

## Cách Tăng Độ Tương Phản Để Nhận Diện Tốt Hơn

Sau khi cân chỉnh, bước tiếp theo là làm cho văn bản nổi bật. `ContrastBoostFilter` kéo dài dải cường độ pixel, rất hữu ích cho các bản in đã phai.

```csharp
// The ContrastBoostFilter is already in the pipeline above.
// You can tweak the Strength value (1.0 = no change, >1.0 = stronger boost)
.Add(new ContrastBoostFilter { Strength = 1.5 })
```

**Lý do nó hữu ích:**  
Các bản quét có độ tương phản thấp tạo ra các ký tự màu xám mà bộ nhị phân hoá có thể hiểu nhầm là nền. Tăng độ tương phản làm cho pixel tối hơn và pixel sáng hơn, cung cấp cho `BinarizationFilter` một nền sạch hơn.

---

## Thực Hiện OCR trên Ảnh – Tải Tệp

Bây giờ ảnh đã được tiền xử lý, chúng ta cần **tải ảnh cho OCR**. Aspose cung cấp một helper tiện lợi `ImageStream.FromFile`.

```csharp
// Load the source image – replace the path with your own file
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");
```

Nếu ảnh của bạn nằm trong một stream (ví dụ, được tải lên qua API web), bạn có thể dùng `ImageStream.FromStream(yourStream)` thay thế. Engine hỗ trợ BMP, JPEG, PNG, TIFF và nhiều định dạng khác.

---

## Chạy Quá Trình Nhận Dạng và Trích Xuất Văn Bản Từ Bản Quét

Khi mọi thứ đã được kết nối, gọi `Recognize()` sẽ thực hiện phần công việc nặng. Sau lệnh này, văn bản đã nhận dạng sẽ có sẵn qua `ocrEngine.Text`.

```csharp
// Run OCR
ocrEngine.Recognize();

// Output the result
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(ocrEngine.Text);
```

**Kết quả mong đợi** (ví dụ cho một hoá đơn đơn giản):

```
=== Extracted Text ===
Invoice #12345
Date: 03/05/2026
Total: $1,250.00
Thank you for your business!
```

Nếu kết quả trông rối rắm, hãy kiểm tra lại thứ tự của pipeline—đầu tiên cân chỉnh, sau đó giảm nhiễu, tăng độ tương phản, và cuối cùng là nhị phân hoá. Thay đổi thứ tự có thể làm giảm chất lượng kết quả.

---

## Những Sai Lầm Thường Gặp và Các Trường Hợp Đặc Biệt

| Vấn đề | Nguyên nhân | Giải pháp |
|-------|-------------|-----------|
| **Kết quả rỗng** | Ảnh quá tối hoặc quá sáng đối với phương pháp nhị phân hoá mặc định. | Tăng `ContrastBoostFilter.Strength` hoặc chuyển sang `BinarizationMethod.Otsu`. |
| **Một phần văn bản bị thiếu** | Nhiễu vẫn còn sau khi giảm nhiễu. | Dùng `DenoiseLevel.Medium` cho ảnh nhẹ, hoặc thêm một `DenoiseFilter` thứ hai. |
| **Hướng xoay sai** | Tài liệu có hướng hỗn hợp (ví dụ, ảnh chụp một trang đã xoay). | Thiết lập thủ công `DeskewFilter.MaxAngle` thấp hơn và xoay trước ảnh bằng `ImageProcessor.Rotate`. |
| **Chậm hiệu năng** | Lô lượng lớn ảnh độ phân giải cao. | Thu nhỏ ảnh (`ImageProcessor.Resize`) trước pipeline, hoặc xử lý song song (`Parallel.ForEach`). |

---

## Ví Dụ Hoàn Chỉnh (Sẵn Sàng Sao Chép‑Dán)

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // 1️⃣ Create OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Build image‑processing pipeline
        var processingPipeline = new ImageProcessingPipeline()
            .Add(new DeskewFilter { MaxAngle = 30 })                     // how to deskew image up to 30°
            .Add(new DenoiseFilter { Level = DenoiseLevel.High })       // remove high‑level noise
            .Add(new ContrastBoostFilter { Strength = 1.5 })            // how to boost contrast
            .Add(new BinarizationFilter { Method = BinarizationMethod.Sauvola }); // binarize image

        // 3️⃣ Attach pipeline to OCR settings
        ocrEngine.Settings.ImageProcessing = processingPipeline;

        // 4️⃣ Load the image you want to OCR
        // Replace the path with the location of your own file
        ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");

        // 5️⃣ Run the recognition engine
        ocrEngine.Recognize();

        // 6️⃣ Display the extracted text
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrEngine.Text);
    }
}
```

Lưu lại dưới tên `Program.cs`, chạy `dotnet run`, và quan sát console in ra kết quả **trích xuất văn bản từ bản quét**.  

---

## Các Bước Tiếp Theo & Chủ Đề Liên Quan

* **Xử lý hàng loạt** – Đặt logic trên vào một vòng lặp để xử lý hàng chục tệp.  
* **Gói ngôn ngữ tùy chỉnh** – Nếu bạn cần đọc các script không phải Latin, tải mô hình ngôn ngữ qua `ocrEngine.Settings.Language = OcrLanguage.ChineseSimplified;`.  
* **Xuất PDF** – Kết hợp Aspose.PDF với OCR để nhúng văn bản có thể tìm kiếm trực tiếp vào tệp PDF.  
* **Tinh chỉnh hiệu năng** – Thử nghiệm thứ tự của `ImageProcessingPipeline`; đôi khi giảm nhiễu trước khi cân chỉnh cho kết quả nhanh hơn trên ảnh nhiễu.  

Tất cả các mục trên dựa trên các khái niệm cốt lõi chúng ta đã đề cập: **cách cân chỉnh ảnh**, **cách tăng độ tương phản**, **tải ảnh cho OCR**, **thực hiện OCR trên ảnh**, và cuối cùng **trích xuất văn bản từ bản quét**.

---

## Tổng Kết

Chúng tôi vừa trình bày một cách hoàn chỉnh, sẵn sàng cho môi trường production để **cách cân chỉnh ảnh** và chạy OCR trong C#. Bằng cách xâu chuỗi một bộ lọc cân chỉnh, một bước giảm nhiễu, một bộ tăng độ tương phản, và một bộ nhị phân hoá, bạn sẽ có một đầu vào sạch sẽ giúp Aspose OCR đáng tin cậy **trích xuất văn bản từ bản quét**.  

Hãy thử chạy mã, điều chỉnh các tham số bộ lọc cho tài liệu của bạn, và bạn sẽ thấy độ chính xác nhận dạng cải thiện nhanh chóng. Có câu hỏi? Để lại bình luận, chúc bạn lập trình vui vẻ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}