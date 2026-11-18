---
category: general
date: 2026-10-11
description: Tìm hiểu cách thực hiện OCR trên hình ảnh trong C# với Aspose.OCR, bao
  gồm cài đặt System.Drawing.Common và trích xuất văn bản từ các tệp JPG.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- extract text from JPG
- recognize text from picture
- load image for OCR
- install System.Drawing.Common package
language: vi
lastmod: 2026-10-11
og_description: Thực hiện OCR trên hình ảnh trong C# bằng Aspose.OCR. Hướng dẫn này
  chỉ cho bạn cách cài đặt System.Drawing.Common, tải hình ảnh để OCR và trích xuất
  văn bản từ file JPG.
og_image_alt: Screenshot of C# console output displaying recognized text after performing
  OCR on image
og_title: Thực hiện OCR trên hình ảnh trong C# – hướng dẫn từng bước
schemas:
- author: Aspose
  dateModified: '2026-10-11'
  description: Learn how to perform OCR on image in C# with Aspose.OCR, including
    installing System.Drawing.Common and extracting text from JPG files.
  headline: How to perform OCR on image in C# using Aspose.OCR
  type: TechArticle
tags:
- OCR
- C#
- Aspose
title: Cách thực hiện OCR trên hình ảnh trong C# bằng Aspose.OCR
url: /vi/net/text-recognition/how-to-perform-ocr-on-image-in-c-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách thực hiện OCR trên hình ảnh trong C# bằng Aspose.OCR

Nếu bạn cần **perform OCR on image** các tệp trong một ứng dụng .NET, hướng dẫn này sẽ cho bạn một giải pháp hoàn chỉnh. Sử dụng Aspose.OCR, bạn có thể nhanh chóng **recognize text from picture** các tệp như JPG và hiển thị kết quả trong cửa sổ console.

Bạn sẽ học cách:

* **install System.Drawing.Common package** – thư viện cung cấp lớp `Image`,
* **load image for OCR** – đọc một tệp JPEG hoặc PNG vào bộ nhớ,
* cấu hình mô hình ngôn ngữ,
* **perform OCR on image** và cuối cùng,
* **extract text from JPG** và xuất ra.

Các bước được viết cho .NET 6+, nhưng chúng cũng hoạt động với .NET Framework 4.6.1 trở lên.

---

## Yêu cầu trước

| Yêu cầu | Lý do quan trọng |
|-------------|----------------|
| .NET 6 SDK (or .NET Framework 4.6.1+) | Cung cấp môi trường chạy cho ứng dụng console C#. |
| Visual Studio 2022 (or any IDE) | Giúp dễ dàng thêm các gói NuGet và chạy chương trình. |
| Internet connection (first run only) | Aspose.OCR tự động tải xuống mô-đun ngôn ngữ. |
| A sample image containing Cyrillic or Latin text (e.g., `sample_cyrillic.jpg`) | Được dùng để minh họa **extract text from JPG**. |

## Bước 1: Cài đặt gói System.Drawing.Common

Gói NuGet `System.Drawing.Common` cung cấp lớp `Image` mà bạn sẽ **load image for OCR**. Mở Package Manager Console và chạy:

```powershell
Install-Package System.Drawing.Common
```

> **Mẹo:** Đặt mục tiêu `net6.0-windows` hoặc thêm `<UseWindowsForms>true</UseWindowsForms>` vào tệp dự án nếu bạn gặp cảnh báo liên quan đến nền tảng trên Linux/macOS.

## Bước 2: Thêm gói NuGet Aspose.OCR

Aspose.OCR chứa engine OCR và các mô hình ngôn ngữ. Cài đặt nó bằng:

```powershell
Install-Package Aspose.OCR
```

Gói này nhẹ; dữ liệu ngôn ngữ cần thiết (ví dụ: Cyrillic) sẽ được tải xuống lần đầu tiên bạn đặt `OcrEngine.Language`.

## Bước 3: Cách tải hình ảnh cho OCR

Việc tải ảnh là bước cụ thể đầu tiên trước khi bạn có thể **perform OCR on image**. Phương thức `Image.FromFile` đọc bất kỳ định dạng nào được GDI+ hỗ trợ, bao gồm JPG, PNG, BMP và TIFF.

```csharp
using System.Drawing; // Requires System.Drawing.Common

// Replace the path with the location of your test picture.
string imagePath = @"YOUR_DIRECTORY/sample_cyrillic.jpg";
Image ocrImage = Image.FromFile(imagePath);
```

*Nếu tệp không tồn tại, sẽ ném `FileNotFoundException` – hãy bao bọc lời gọi trong khối try/catch cho mã sản xuất.*

## Bước 4: Cấu hình engine và **perform OCR on image**

Tạo một thể hiện `OcrEngine`, chọn mô hình ngôn ngữ, gán ảnh đã tải, và gọi `Recognize()`.

```csharp
using Aspose.OCR;

// Step 4: Initialize OCR engine and set language
var ocrEngine = new OcrEngine
{
    // Choose the language you need; Cyrillic is used in this example.
    Language = OcrLanguage.Cyrillic,
    Image = ocrImage
};

// Execute the OCR operation
OcrResult ocrResult = ocrEngine.Recognize();
```

Phương thức `Recognize()` trả về một đối tượng `OcrResult` chứa văn bản đã trích xuất, điểm tin cậy và các hộp bao quanh. Mô-đun ngôn ngữ được tải tự động lần đầu sử dụng, vì vậy không cần tệp bổ sung.

## Bước 5: **Extract text from JPG** và hiển thị

Bây giờ bạn có thể **recognize text from picture** và xuất kết quả. Thuộc tính `Text` của `OcrResult` chứa chuỗi văn bản thuần.

```csharp
// Step 5: Output recognized text
Console.WriteLine("Recognized text:");
Console.WriteLine(ocrResult.Text);
```

### Đầu ra console dự kiến

```
Recognized text:
Пример текста на кириллице
```

Nếu hình ảnh nguồn chứa văn bản tiếng Anh, đầu ra sẽ là câu tiếng Anh bạn đặt trong ảnh.

## Các trường hợp đặc biệt và mẹo thực hành tốt nhất

| Tình huống | Khuyến nghị |
|-----------|----------------|
| **Hình ảnh lớn ( > 5 MB )** | Thu nhỏ hình ảnh xuống ≤ 2000 px ở cạnh dài nhất trước khi OCR để giảm sử dụng bộ nhớ và tăng tốc độ. |
| **Nhiều ngôn ngữ trong một hình ảnh** | Gọi `ocrEngine.AddLanguage(OcrLanguage.English)` bổ sung cho Cyrillic, sau đó đặt `ocrEngine.Language = OcrLanguage.Multilingual`. |
| **Quét độ tương phản thấp** | Tăng độ tương phản bằng `System.Drawing.Graphics` trước khi truyền bitmap cho engine. |
| **Chạy trên Linux/macOS** | Đảm bảo phụ thuộc gốc `libgdiplus` đã được cài đặt (`sudo apt-get install -y libgdiplus`). |
| **Gọi OCR lặp lại** | Tái sử dụng cùng một thể hiện `OcrEngine` và chỉ thay thế `ocrEngine.Image` để tránh tải lại mô-đun. |

## Chương trình đầy đủ, có thể chạy

Dưới đây là ứng dụng console hoàn chỉnh tích hợp tất cả các bước trước. Sao chép mã vào một dự án console C# mới, thay đổi đường dẫn hình ảnh, và chạy nó.

```csharp
using System;
using System.Drawing;                 // Install System.Drawing.Common if needed
using Aspose.OCR;                     // NuGet package: Aspose.OCR

class Program
{
    static void Main()
    {
        // Step 1: Install System.Drawing.Common (handled via NuGet)
        // Step 2: Install Aspose.OCR (handled via NuGet)

        // Step 3: Load the image that contains the text to be recognized
        // Replace the placeholder with the actual path to your JPG or PNG file.
        string imagePath = @"YOUR_DIRECTORY/sample_cyrillic.jpg";
        Image ocrImage;
        try
        {
            ocrImage = Image.FromFile(imagePath);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Failed to load image: {ex.Message}");
            return;
        }

        // Step 4: Create the OCR engine and choose the language model
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.Cyrillic, // Change to OcrLanguage.English for Latin scripts
            Image = ocrImage
        };

        // Step 5: Perform OCR on the loaded picture
        OcrResult ocrResult = ocrEngine.Recognize();

        // Step 6: Display the extracted text
        Console.WriteLine("Recognized text:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Chạy chương trình** sẽ in chuỗi đã nhận dạng ra console, xác nhận rằng bạn đã thành công **performed OCR on image** và **extracted text from JPG**.

## Kết luận

Bây giờ bạn đã biết cách **perform OCR on image** các tệp trong C# bằng Aspose.OCR, từ việc cài đặt **System.Drawing.Common package** cần thiết đến **loading image for OCR**, chọn ngôn ngữ phù hợp, và cuối cùng **extracting text from JPG**. Ví dụ toàn diện này cung cấp nền tảng vững chắc để xây dựng các pipeline xử lý tài liệu nâng cao hơn, chẳng hạn như xử lý hàng loạt thư mục ảnh hoặc tích hợp OCR vào API web.

### Tiếp theo là gì?

* Khám phá **recognize text from picture** trong PDF bằng cách chuyển mỗi trang thành hình ảnh trước.
* Thử nghiệm các thuộc tính `Resolution`, `Threshold`, và `MaxProcessingTime` của `OcrEngine` để tinh chỉnh độ chính xác trên các bản quét nhiễu.
* Kết hợp kết quả OCR với thư viện xử lý ngôn ngữ tự nhiên để tự động phân loại nội dung đã trích xuất.

Bạn có thể tự do điều chỉnh mã cho các định dạng ảnh khác, thêm xử lý lỗi, hoặc tích hợp vào các ứng dụng lớn hơn. Chúc lập trình vui vẻ!

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoạt động đầy đủ với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Trích xuất văn bản từ hình ảnh trong C# – Hướng dẫn Aspose OCR đầy đủ](/ocr/english/net/text-recognition/extract-text-from-image-in-c-complete-aspose-ocr-guide/)
- [Trích xuất văn bản hình ảnh C# với lựa chọn ngôn ngữ bằng Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Cách thực hiện trích xuất văn bản hình ảnh từ luồng bằng Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}