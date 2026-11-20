---
category: general
date: 2026-11-20
description: Cách sử dụng OCR trong C# để nhận dạng văn bản từ hình ảnh. Học cách
  tải hình ảnh cho OCR, thiết lập ngôn ngữ OCR và trích xuất văn bản từ các tệp JPEG.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use OCR
- recognize text image
- load image OCR
- recognize text JPEG
- set OCR language
language: vi
lastmod: 2026-11-20
og_description: Cách sử dụng OCR trong C# để trích xuất văn bản từ hình ảnh. Hướng
  dẫn này cho thấy cách tải hình ảnh, thiết lập ngôn ngữ OCR và nhận dạng văn bản
  từ các tệp JPEG.
og_image_alt: Screenshot of C# code demonstrating how to use OCR to recognize text
  from an image
og_title: Cách sử dụng OCR trong C# – hướng dẫn đầy đủ
schemas:
- author: Aspose
  dateModified: '2026-11-20'
  description: How to use OCR in C# to recognize text from an image. Learn to load
    image OCR, set OCR language, and extract text from JPEG files.
  headline: How to use OCR in C# with image recognition
  type: TechArticle
tags:
- OCR
- C#
- Image processing
- Text extraction
title: Cách sử dụng OCR trong C# với nhận dạng hình ảnh
url: /vi/net/text-recognition/how-to-use-ocr-in-c-with-image-recognition/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách sử dụng OCR trong C# với nhận dạng hình ảnh

Nếu bạn cần **cách sử dụng OCR** trong một ứng dụng C#, hướng dẫn này sẽ dẫn bạn qua toàn bộ quy trình. Dù bạn đang số hoá các hợp đồng đã quét hoặc trích xuất thông tin từ ảnh, bạn sẽ học cách **nhận dạng hình ảnh văn bản** một cách nhanh chóng và đáng tin cậy.

Bài hướng dẫn bao gồm việc tải ảnh, cấu hình công cụ OCR, và lấy văn bản đã nhận dạng từ các tệp JPEG. Khi kết thúc, bạn sẽ có một ví dụ tự chứa, có thể chạy được mà bạn có thể đưa vào bất kỳ dự án .NET nào.

## Yêu cầu trước

* .NET 6.0 (hoặc mới hơn) đã được cài đặt.  
* Truy cập vào một thư viện OCR cung cấp `OcrEngine`, `ImageStream`, và các mô-đun ngôn ngữ (ví dụ, **Leadtools**, **Aspose.OCR**, hoặc bất kỳ gói nào tương thích).  
* Một ảnh mẫu có tên `sample.jpg` trong một thư mục đã biết.  

Không cần dịch vụ bên ngoài bổ sung — công cụ OCR sẽ tự động tải xuống các gói ngôn ngữ còn thiếu.

## Bước 1: Tải ảnh cho OCR

Việc tải ảnh là bước đầu tiên trong bất kỳ quy trình OCR nào. Đoạn mã dưới đây tạo một `ImageStream` từ tệp JPEG trên đĩa.

```csharp
// Step 1: Load the image to be recognized
var imagePath = Path.Combine("YOUR_DIRECTORY", "sample.jpg");
var image = ImageStream.FromFile(imagePath);
```

*Tại sao điều này quan trọng:* Đối tượng `ImageStream` trừu tượng hoá việc xử lý tệp và cung cấp dữ liệu pixel mà công cụ OCR tiêu thụ. Nếu tệp không được tìm thấy, `FromFile` sẽ ném ra một ngoại lệ rõ ràng, giúp việc gỡ lỗi trở nên đơn giản.

## Bước 2: Tạo một thể hiện công cụ OCR (tự giải phóng tài nguyên)

Sử dụng khối `using` đảm bảo rằng các tài nguyên không quản lý được giải phóng ngay khi công việc OCR hoàn thành.

```csharp
// Step 2: Create an OCR engine instance (automatically disposes when done)
using var ocrEngine = new OcrEngine();
```

*Mẹo chuyên nghiệp:* Câu lệnh `using` được ưu tiên hơn việc gọi `Dispose()` thủ công vì nó loại bỏ nguy cơ quên giải phóng bộ nhớ gốc, điều có thể gây rò rỉ bộ nhớ trong các dịch vụ chạy lâu dài.

## Bước 3: Đặt ngôn ngữ OCR (tùy chọn nhưng được khuyến nghị)

Nếu bạn biết ngôn ngữ của tài liệu nguồn, việc đặt ngôn ngữ sẽ cải thiện độ chính xác và tăng tốc xử lý. Ví dụ đặt ngôn ngữ thành Cyrillic; bạn có thể thay thế bằng bất kỳ enum ngôn ngữ nào được hỗ trợ.

```csharp
// Step 3 (optional): Specify the language module, e.g., Cyrillic
// The required language pack will be downloaded automatically if missing
ocrEngine.Language = OcrLanguage.Cyrillic;
```

*Tại sao phải đặt ngôn ngữ?* Các công cụ OCR chứa các mô hình ký tự riêng cho từng ngôn ngữ. Bằng cách chọn đúng mô hình, bạn giảm các kết quả sai và tránh các thay thế ký tự không cần thiết.

## Bước 4: Thực hiện OCR trên ảnh đã tải

Bây giờ công cụ xử lý bitmap và trả về văn bản đã nhận dạng dưới dạng một chuỗi.

```csharp
// Step 4: Perform OCR on the loaded image
string recognizedText = ocrEngine.Recognize(image);
```

*Trường hợp đặc biệt:* Nếu ảnh có độ phân giải thấp hoặc bị nén mạnh, công cụ có thể trả về kết quả một phần. Hãy cân nhắc tiền xử lý (ví dụ, nhị phân hoá) để có kết quả tốt hơn.

## Bước 5: Xuất văn bản đã nhận dạng

Cuối cùng, hiển thị văn bản đã trích xuất trong console hoặc chuyển nó tới thành phần khác.

```csharp
// Step 5: Output the recognized text
Console.WriteLine("=== Recognized Text ===");
Console.WriteLine(recognizedText);
```

**Kết quả mong đợi**

```
=== Recognized Text ===
Пример текста, полученного из изображения.
```

Nội dung chính xác phụ thuộc vào ảnh nguồn, nhưng console sẽ hiển thị toàn bộ chuỗi mà công cụ OCR đã phát hiện.

## Ví dụ đầy đủ, có thể chạy

Kết hợp tất cả các bước lại với nhau tạo ra một chương trình gọn gàng mà bạn có thể biên dịch và chạy ngay lập tức.

```csharp
using System;
using System.IO;

// Ensure you reference the OCR library that provides these types
// e.g., using Leadtools.OCR;

class Program
{
    static void Main()
    {
        // Load the image to be recognized
        var imagePath = Path.Combine("YOUR_DIRECTORY", "sample.jpg");
        var image = ImageStream.FromFile(imagePath);

        // Create an OCR engine instance (auto‑dispose)
        using var ocrEngine = new OcrEngine();

        // Optional: set the language (Cyrillic in this case)
        ocrEngine.Language = OcrLanguage.Cyrillic;

        // Perform OCR
        string recognizedText = ocrEngine.Recognize(image);

        // Output the result
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(recognizedText);
    }
}
```

Sao chép mã vào một dự án console mới, thay thế `YOUR_DIRECTORY` bằng đường dẫn tới ảnh của bạn, và chạy `dotnet run`. Chương trình sẽ in văn bản đã nhận dạng ra console.

## Các câu hỏi thường gặp và khắc phục sự cố

| Câu hỏi | Trả lời |
|----------|--------|
| **Nếu gói ngôn ngữ không được tải xuống thì sao?** | Thư viện OCR sẽ cố gắng tải nó tự động. Đảm bảo máy có kết nối internet, hoặc cài đặt trước gói ngôn ngữ theo tài liệu của thư viện. |
| **Tôi có thể nhận dạng văn bản từ tệp PNG hoặc BMP không?** | Có. `ImageStream.FromFile` hoạt động với bất kỳ định dạng nào mà thư viện ảnh nền hỗ trợ. Chỉ cần thay đổi phần mở rộng tệp. |
| **Làm sao cải thiện độ chính xác cho các bản quét nhiễu?** | Tiền xử lý ảnh (điều chỉnh độ tương phản, loại bỏ nhiễu) trước khi truyền vào `Recognize`. Nhiều thư viện cung cấp các lớp `ImageProcessor` cho mục đích này. |
| **Có an toàn khi chạy OCR trên các tệp do người dùng tải lên không?** | Xác thực kích thước và loại tệp, và chạy OCR trong môi trường sandbox để tránh các payload độc hại. |

## Kết luận

Bây giờ bạn đã biết **cách sử dụng OCR** trong C# để **nhận dạng hình ảnh văn bản**, **tải ảnh OCR**, **đặt ngôn ngữ OCR**, và **nhận dạng nội dung JPEG** một cách đáng tin cậy. Ví dụ hoàn chỉnh minh họa một quy trình làm việc sạch sẽ, có thể giải phóng tài nguyên, mà bạn có thể mở rộng với các bước tiền xử lý bổ sung, hỗ trợ đa ngôn ngữ, hoặc tích hợp vào các pipeline xử lý tài liệu lớn hơn.

### Các bước tiếp theo

* Khám phá xử lý hàng loạt bằng cách lặp qua một thư mục các tệp JPEG.  
* Kết hợp OCR với Xử lý Ngôn ngữ Tự nhiên (NLP) để trích xuất dữ liệu có cấu trúc.  
* Thử nghiệm các mô-đun ngôn ngữ khác như `OcrLanguage.English` hoặc `OcrLanguage.Arabic`.  

Bạn có thể tự do điều chỉnh mã cho trường hợp sử dụng cụ thể của mình, và chúc lập trình vui vẻ!

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoạt động đầy đủ với các giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Sử dụng Windows.Media.Ocr để nhận dạng hình ảnh văn bản trong C# – Hướng dẫn OCR đầy đủ](/ocr/english/net/text-recognition/recognize-text-image-in-c-full-ocr-guide/)
- [Cách sử dụng OCR trong C# – Trích xuất văn bản từ ảnh một cách bất đồng bộ](/ocr/english/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image-asynchronously/)
- [Cách sử dụng OCR trong C# – Trích xuất văn bản từ ảnh với Aspose OCR](/ocr/english/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image-with-aspose-ocr/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}