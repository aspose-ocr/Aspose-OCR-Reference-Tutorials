---
category: general
date: 2026-06-22
description: Nhận dạng văn bản từ hình ảnh bằng Aspose OCR trong C#. Tìm hiểu cách
  tự động chỉnh nghiêng hình ảnh, tiền xử lý hình ảnh cho OCR và bật tính năng tự
  động chỉnh nghiêng trong một ví dụ OCR C# ngắn gọn.
draft: false
keywords:
- recognize text from image
- auto deskew image
- preprocess image for ocr
- c# ocr example
- enable auto deskew
language: vi
og_description: Nhận dạng văn bản từ hình ảnh bằng Aspose OCR trong C#. Hướng dẫn
  này chỉ cách tự động chỉnh nghiêng hình ảnh, tiền xử lý hình ảnh cho OCR và bật
  tính năng tự động chỉnh nghiêng trong một ví dụ thực tế về OCR bằng C#.
og_title: Nhận dạng văn bản từ hình ảnh trong C# – Ví dụ OCR đầy đủ
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Recognize text from image using Aspose OCR in C#. Learn how to auto
    deskew image, preprocess image for OCR, and enable auto deskew in a concise c#
    ocr example.
  headline: Recognize Text from Image in C# – Full OCR Example
  type: TechArticle
- description: Recognize text from image using Aspose OCR in C#. Learn how to auto
    deskew image, preprocess image for OCR, and enable auto deskew in a concise c#
    ocr example.
  name: Recognize Text from Image in C# – Full OCR Example
  steps:
  - name: 1. Low Contrast or Dark Backgrounds
    text: 'Aspose.OCR offers an extra flag `PreprocessingOptions.ContrastEnhancement`.
      Add it to the `Preprocessing` line:'
  - name: 2. Non‑English Documents
    text: Swap `OcrLanguage.English` for `OcrLanguage.Spanish`, `OcrLanguage.French`,
      etc. The engine auto‑loads the appropriate language model.
  - name: 3. Large Images
    text: 'Processing a 5 MP photo can be memory‑hungry. Scale it down first:'
  - name: 4. Getting Bounding Boxes
    text: 'If you need the exact location of each word (e.g., for a UI overlay), iterate
      over `result.Regions`:'
  type: HowTo
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Nhận dạng văn bản từ hình ảnh trong C# – Ví dụ OCR đầy đủ
url: /vi/net/ocr-optimization/recognize-text-from-image-in-c-full-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Nhận dạng Văn bản từ Hình ảnh trong C# – Ví dụ OCR Đầy đủ

Bạn đã bao giờ tự hỏi làm thế nào để **nhận dạng văn bản từ hình ảnh** trong một ứng dụng C# mà không phải loay hoay với các bản scan mờ? Bạn không phải là người duy nhất. Dù bạn đang số hoá biên lai, trích xuất dữ liệu từ mẫu đơn, hay chỉ đơn giản là chơi với các thủ thuật ảnh hỗ trợ AI, việc có được kết quả OCR sạch sẽ phụ thuộc vào việc tiền xử lý hợp lý — như tự động chỉnh nghiêng ảnh và giảm nhiễu.

Trong hướng dẫn này, chúng ta sẽ đi qua một **c# ocr example** sử dụng thư viện Aspose.OCR để **bật tính năng auto deskew**, tự động làm thẳng các bức ảnh nghiêng, và **tiền xử lý ảnh cho OCR** chỉ trong vài dòng code. Khi hoàn thành, bạn sẽ có một chương trình có thể chạy được và in ra văn bản đã nhận dạng trực tiếp trên console.

## Những gì bạn sẽ học

- Cách cài đặt và tham chiếu gói NuGet Aspose.OCR.  
- Thiết lập một `OcrEngine` với hỗ trợ ngôn ngữ tiếng Anh.  
- Bật **auto deskew image** và các tùy chọn tiền xử lý khác trong một bước.  
- Chạy engine trên một bức ảnh thực tế và xử lý kết quả.  
- Mẹo xử lý các trường hợp đặc biệt như ảnh bị xoay mạnh hoặc scan có độ tương phản thấp.

> **Yêu cầu trước** – Bạn cần .NET 6 (hoặc mới hơn) và kiến thức cơ bản về C#. Không cần kinh nghiệm OCR trước đó.

---

## ## Nhận dạng Văn bản từ Hình ảnh – Cài đặt Gói Aspose.OCR

Trước khi viết bất kỳ code nào, thư viện cần được thêm vào dự án. Mở terminal trong thư mục solution của bạn và chạy:

```bash
dotnet add package Aspose.OCR
```

Lệnh này sẽ tải phiên bản ổn định mới nhất của Aspose.OCR, bao gồm engine OCR, các gói ngôn ngữ và các tiện ích tiền xử lý mà chúng ta sẽ dùng.  

*Pro tip:* Nếu bạn đang nhắm tới .NET Framework thay vì .NET Core, hãy sử dụng giao diện Visual Studio NuGet Package Manager — chỉ cần tìm “Aspose.OCR” và nhấn **Install**.

---

## ## Nhận dạng Văn bản từ Hình ảnh – Khởi tạo Engine OCR

Bây giờ gói đã sẵn sàng, chúng ta có thể tạo engine. Bước đầu tiên là chỉ định ngôn ngữ mà engine sẽ nhận dạng. Trong hầu hết các trường hợp tiếng Anh là đủ, nhưng thư viện hỗ trợ hàng chục ngôn ngữ ngay từ đầu.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Step 1: Create an OCR engine and set the language to English
        var engine = new OcrEngine
        {
            Language = OcrLanguage.English,

            // Step 2: Enable preprocessing to automatically deskew and denoise the image
            Preprocessing = PreprocessingOptions.AutoDeskew | PreprocessingOptions.Denoise
        };
```

**Tại sao điều này quan trọng:**  
- `Language = OcrLanguage.English` cho engine biết bộ ký tự nào sẽ dùng, giúp cải thiện độ chính xác đáng kể.  
- Thuộc tính `Preprocessing` kết hợp hai cờ — `AutoDeskew` và `Denoise`. Bước **auto deskew image** này sẽ xoay lại ảnh về trục ngang, trong khi `Denoise` loại bỏ các nhiễu hạt gây rối cho engine OCR.  

Nếu bạn bỏ qua tiền xử lý, thường sẽ thấy kết quả rối rắm trên các biên lai scan hoặc ảnh chụp góc.

---

## ## Nhận dạng Văn bản từ Hình ảnh – Đưa Ảnh vào Engine

Với engine đã được chuẩn bị, bước tiếp theo là cung cấp cho nó một tệp ảnh. Aspose.OCR chấp nhận đường dẫn hoặc một `Stream`, vì vậy bạn có thể làm việc với tệp cục bộ, tài nguyên nhúng, hoặc thậm chí ảnh tải về từ web.

```csharp
        // Step 3: Recognize text from the input image
        var result = engine.RecognizeImage(@"YOUR_DIRECTORY/skewed_photo.jpg");
```

**Lưu ý trường hợp đặc biệt:**  
- Nếu ảnh **được xoay mạnh** (> 45°), `AutoDeskew` sẽ cố gắng hết sức, nhưng bạn có thể muốn tự xoay ảnh trước bằng `System.Drawing` hoặc `ImageSharp` trước khi truyền vào engine.  
- Đối với **PDF đa trang**, hãy gọi `engine.RecognizePdf` thay vì; các cờ tiền xử lý vẫn áp dụng như bình thường.

---

## ## Nhận dạng Văn bản từ Hình ảnh – Xuất Kết quả

Cuối cùng, chúng ta hiển thị văn bản đã trích xuất. Đối tượng `result` chứa nhiều hơn chỉ văn bản thuần — nó còn cung cấp điểm tin cậy, các bounding box và ảnh gốc với các vùng được đánh dấu. Đối với một demo nhanh, việc in `result.Text` là đủ.

```csharp
        // Step 4: Output the recognized text to the console
        System.Console.WriteLine(result.Text);
    }
}
```

Khi bạn chạy chương trình, bạn sẽ thấy một đầu ra giống như:

```
Invoice #12345
Date: 2026-06-01
Total: $256.78
Thank you for your business!
```

Nếu kết quả trông hỗn loạn, hãy kiểm tra lại ảnh nguồn có rõ ràng, đủ ánh sáng và **tiền xử lý ảnh cho OCR** đã được bật (các cờ `Preprocessing` ở trên).

---

## ## Nhận dạng Văn bản từ Hình ảnh – Xử lý Các Trường Hợp Thường Gặp

### 1. Độ tương phản thấp hoặc nền tối
Aspose.OCR cung cấp một cờ bổ sung `PreprocessingOptions.ContrastEnhancement`. Thêm nó vào dòng `Preprocessing`:

```csharp
Preprocessing = PreprocessingOptions.AutoDeskew |
                PreprocessingOptions.Denoise |
                PreprocessingOptions.ContrastEnhancement
```

### 2. Tài liệu không phải tiếng Anh
Thay `OcrLanguage.English` bằng `OcrLanguage.Spanish`, `OcrLanguage.French`, v.v. Engine sẽ tự động tải mô hình ngôn ngữ tương ứng.

### 3. Ảnh lớn
Xử lý ảnh 5 MP có thể tốn nhiều bộ nhớ. Hãy thu nhỏ ảnh trước:

```csharp
engine.Image = ImageProcessor.Resize(@"YOUR_DIRECTORY/skewed_photo.jpg", 1024, 768);
```

### 4. Lấy Bounding Boxes
Nếu bạn cần vị trí chính xác của từng từ (ví dụ để hiển thị overlay UI), hãy lặp qua `result.Regions`:

```csharp
foreach (var region in result.Regions)
{
    System.Console.WriteLine($"{region.Text} at {region.Bounds}");
}
```

---

## ## Nhận dạng Văn bản từ Hình ảnh – Ví dụ Hoàn chỉnh

Dưới đây là chương trình **đầy đủ, có thể sao chép‑dán** bao gồm tất cả các mẹo ở trên. Lưu lại dưới tên `Program.cs`, thay `YOUR_DIRECTORY` bằng thư mục chứa ảnh thử nghiệm của bạn, và chạy `dotnet run`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;

class Program
{
    static void Main()
    {
        // Create and configure the OCR engine
        var engine = new OcrEngine
        {
            Language = OcrLanguage.English,
            // Enable auto deskew, denoise, and contrast enhancement
            Preprocessing = PreprocessingOptions.AutoDeskew |
                            PreprocessingOptions.Denoise |
                            PreprocessingOptions.ContrastEnhancement
        };

        // Path to the image you want to process
        string imagePath = @"YOUR_DIRECTORY/skewed_photo.jpg";

        // Recognize the image
        var result = engine.RecognizeImage(imagePath);

        // Output plain text
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(result.Text);
        Console.WriteLine();

        // Optional: print bounding boxes for each detected region
        Console.WriteLine("=== Detected Regions ===");
        foreach (var region in result.Regions)
        {
            Console.WriteLine($"{region.Text}  -->  {region.Bounds}");
        }
    }
}
```

**Đầu ra dự kiến trên console** (giả sử ảnh chứa một biên lai đơn giản):

```
=== Recognized Text ===
Invoice #12345
Date: 2026-06-01
Total: $256.78
Thank you for your business!

=== Detected Regions ===
Invoice #12345  -->  {X=12,Y=34,Width=250,Height=20}
Date: 2026-06-01  -->  {X=12,Y=60,Width=200,Height=18}
Total: $256.78  -->  {X=12,Y=86,Width=180,Height=18}
Thank you for your business!  -->  {X=12,Y=112,Width=300,Height=22}
```

Nếu bạn thấy văn bản được in sạch sẽ, chúc mừng — bạn đã thành công **nhận dạng văn bản từ ảnh** với tính năng auto‑deskew và tiền xử lý!

---

## ## Nhận dạng Văn bản từ Hình ảnh – Các Bước Tiếp Theo & Chủ Đề Liên Quan

- **Xử lý hàng loạt:** Đặt lời gọi engine trong một vòng lặp `foreach` để xử lý hàng chục ảnh cùng lúc.  
- **Chuyển đổi PDF:** Dùng `engine.RecognizePdf` cho tài liệu đa trang, sau đó hợp nhất kết quả.  
- **Từ điển tùy chỉnh:** Cung cấp danh sách từ cho `engine.CustomWords` để cải thiện độ chính xác với thuật ngữ chuyên ngành (ví dụ mã y tế).  
- **Tối ưu hiệu năng:** Cache đối tượng `OcrEngine` nếu bạn xử lý nhiều ảnh; việc tạo engine là bước tốn kém nhất.  

Các mở rộng này đều dựa trên cùng các khái niệm — **tiền xử lý ảnh cho OCR**, **bật auto deskew**, và **nhận dạng văn bản từ ảnh** — vì vậy bạn có thể tái sử dụng các mẫu code vừa học.

---

## Kết luận

Chúng ta vừa đi qua một **c# ocr example** cho thấy cách **nhận dạng văn bản từ ảnh** bằng Aspose.OCR, đồng thời tự động chỉnh nghiêng và giảm nhiễu ảnh. Bằng cách bật `AutoDeskew` (tính năng **auto deskew image**) và thêm một vài cờ tiền xử lý, bạn sẽ tăng đáng kể độ tin cậy của OCR mà không cần viết một dòng code xử lý ảnh nào.

Bây giờ bạn có thể lấy khung sườn này, chèn ảnh của riêng mình, và bắt đầu trích xuất dữ liệu cho hoá đơn, CMND, hoặc bất kỳ loại tài liệu nào còn trên giấy. Gặp phải ảnh khó xử lý? Hãy thử các tùy chọn tiền xử lý bổ sung đã đề cập, hoặc khám phá các gói ngôn ngữ tùy chỉnh. Không có giới hạn nào.

Nếu hướng dẫn này giúp bạn giải quyết vấn đề, hãy để lại bình luận, chia sẻ kết quả, hoặc nhắn tin cho tôi trên GitHub — chúc bạn lập trình vui!

## Bạn Nên Học Gì Tiếp Theo?

Các tutorial dưới đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên đều bao gồm mã nguồn hoạt động đầy đủ cùng các giải thích chi tiết từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}