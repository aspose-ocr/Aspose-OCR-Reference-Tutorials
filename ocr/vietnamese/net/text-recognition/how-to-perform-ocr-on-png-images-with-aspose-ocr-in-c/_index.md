---
category: general
date: 2026-11-26
description: Tìm hiểu cách thực hiện OCR trên các tệp PNG, chuyển đổi PNG thành văn
  bản và trích xuất văn bản Cyrillic bằng Aspose.OCR – hướng dẫn từng bước cho các
  nhà phát triển.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- convert PNG to text
- recognize text from PNG
- extract Cyrillic text
- load image for OCR
language: vi
lastmod: 2026-11-26
og_description: Cách thực hiện OCR trên các tệp PNG và trích xuất văn bản Cyrillic
  bằng Aspose.OCR trong C#. Theo dõi hướng dẫn đầy đủ này để chuyển đổi PNG sang văn
  bản.
og_image_alt: how to perform OCR on a PNG image using Aspose.OCR
og_title: Cách thực hiện OCR trên hình ảnh PNG với Aspose.OCR – Hướng dẫn C#
schemas:
- author: Aspose
  dateModified: '2026-11-26'
  description: Learn how to perform OCR on PNG files, convert PNG to text, and extract
    Cyrillic text using Aspose.OCR – step‑by‑step guide for developers.
  headline: How to perform OCR on PNG images with Aspose.OCR in C#
  type: TechArticle
- description: Learn how to perform OCR on PNG files, convert PNG to text, and extract
    Cyrillic text using Aspose.OCR – step‑by‑step guide for developers.
  name: How to perform OCR on PNG images with Aspose.OCR in C#
  steps:
  - name: Handling large images
    text: 'If the PNG is larger than 2 MB, consider down‑scaling it before recognition
      to speed up processing:'
  - name: 'Edge case: Missing language module'
    text: 'If the download fails (e.g., offline environment), the engine throws an
      `OcrException`. Catch it to provide a graceful fallback:'
  - name: Expected output
    text: 'If `sample_image.png` contains the Cyrillic phrase “Привет мир”, the console
      will display:'
  - name: How it works
    text: 1. **Engine creation** – prepares the OCR pipeline. 2. **Image loading**
      – supports both raw PNG and down‑scaled versions for performance. 3. **Language
      selection** – demonstrates **extract Cyrillic text** while handling missing
      modules. 4. **Recognition** – the core **recognize text from PNG** call
  type: HowTo
tags:
- OCR
- C#
- Aspose.OCR
title: Cách thực hiện OCR trên hình ảnh PNG bằng Aspose.OCR trong C#
url: /vi/net/text-recognition/how-to-perform-ocr-on-png-images-with-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách thực hiện OCR trên hình ảnh PNG với Aspose.OCR trong C#

Nếu bạn cần **cách thực hiện OCR** trên một tệp PNG, hướng dẫn này sẽ cho bạn các bước chính xác để chuyển đổi PNG thành văn bản bằng Aspose.OCR. Dù bạn đang trích xuất văn bản Cyrillic từ tài liệu quét hoặc chỉ đơn giản là nhận dạng văn bản từ ảnh chụp màn hình PNG, giải pháp này hoạt động ngay lập tức và chỉ yêu cầu vài dòng mã C#.

Trong tutorial này, bạn sẽ học cách:

* **tải ảnh cho OCR** từ một thư mục cục bộ,
* cấu hình engine để **trích xuất văn bản Cyrillic**,
* **nhận dạng văn bản từ PNG** và nhận được một chuỗi sạch,
* xử lý các vấn đề thường gặp như thiếu mô-đun ngôn ngữ và hình ảnh lớn.

Không cần kinh nghiệm trước với Aspose.OCR—chỉ cần môi trường phát triển .NET và một hình ảnh PNG bạn muốn xử lý.

## Yêu cầu trước

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

* .NET 6.0 (hoặc phiên bản mới hơn) đã được cài đặt.
* Bản sao có giấy phép hoặc bản dùng thử của **Aspose.OCR for .NET**. Bạn có thể lấy bản dùng thử miễn phí từ trang web Aspose.
* Visual Studio 2022 (hoặc bất kỳ IDE nào hỗ trợ .NET).
* Một tệp PNG chứa văn bản bạn muốn trích xuất (ví dụ sử dụng `sample_image.png`).

## Bước 1: Cài đặt gói NuGet Aspose.OCR

Mở terminal trong thư mục dự án của bạn và chạy:

```bash
dotnet add package Aspose.OCR
```

Gói này bao gồm engine OCR lõi và tất cả các mô-đun ngôn ngữ. Khi bạn yêu cầu một ngôn ngữ chưa có trên máy, Aspose.OCR sẽ tự động tải xuống mô-đun cần thiết.

## Bước 2: Tạo một thể hiện OCR engine (cách thực hiện OCR)

Bước hành động đầu tiên trong bất kỳ quy trình OCR nào là khởi tạo engine. Đối tượng này quản lý tất cả các thao tác tiếp theo như tải ảnh và thực hiện nhận dạng.

```csharp
using Aspose.OCR;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();
```

**Tại sao điều này quan trọng:** Lớp `OcrEngine` bao bọc quy trình OCR. Tạo một thể hiện duy nhất và tái sử dụng nó cho nhiều ảnh sẽ giảm tải bộ nhớ và cải thiện hiệu năng.

## Bước 3: Tải ảnh cho OCR – chỉ định tệp PNG nguồn

Việc tải ảnh là điểm mà bạn **tải ảnh cho OCR**. Aspose.OCR chấp nhận nhiều loại đầu vào; cách đơn giản nhất là `ImageStream.FromFile`.

```csharp
// Load the PNG image from disk
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/sample_image.png");
```

> **Mẹo chuyên nghiệp:** Sử dụng đường dẫn tuyệt đối hoặc `Path.Combine` để tránh lỗi thời gian chạy trên các môi trường khác nhau.

### Xử lý ảnh lớn

Nếu PNG lớn hơn 2 MB, hãy cân nhắc giảm kích thước trước khi nhận dạng để tăng tốc xử lý:

```csharp
using System.Drawing;

// Downscale large images to a maximum width of 1200 pixels
Bitmap original = new Bitmap(@"YOUR_DIRECTORY/sample_image.png");
int maxWidth = 1200;
int newHeight = (int)(original.Height * (maxWidth / (double)original.Width));
Bitmap resized = new Bitmap(original, new Size(maxWidth, newHeight));

using (var ms = new MemoryStream())
{
    resized.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
    ocrEngine.Image = ImageStream.FromStream(ms);
}
```

## Bước 4: Cấu hình ngôn ngữ – trích xuất văn bản Cyrillic

Mặc định, Aspose.OCR giả định tiếng Anh. Để **trích xuất văn bản Cyrillic**, đặt thuộc tính `Language` thành `Language.Cyrillic`. Mô-đun cần thiết sẽ được tải tự động lần đầu khi bạn chạy mã.

```csharp
// Set the OCR language to Cyrillic
ocrEngine.Language = Language.Cyrillic;
```

Nếu bạn cần nhận dạng nhiều ngôn ngữ (ví dụ, tiếng Anh và Cyrillic), bạn có thể kết hợp chúng:

```csharp
ocrEngine.Language = Language.English | Language.Cyrillic;
```

### Trường hợp đặc biệt: Thiếu mô-đun ngôn ngữ

Nếu việc tải xuống thất bại (ví dụ, môi trường offline), engine sẽ ném ra một `OcrException`. Bắt ngoại lệ này để cung cấp phương án dự phòng nhẹ nhàng:

```csharp
try
{
    ocrEngine.Language = Language.Cyrillic;
}
catch (OcrException ex)
{
    Console.WriteLine($"Language module could not be loaded: {ex.Message}");
    // Optionally, fall back to English or abort the process
}
```

## Bước 5: Thực hiện thao tác nhận dạng (nhận dạng văn bản từ PNG)

Bây giờ ảnh và ngôn ngữ đã được thiết lập, bạn có thể **nhận dạng văn bản từ PNG**. Phương thức `Recognize` chạy quy trình OCR đồng bộ.

```csharp
// Run OCR
ocrEngine.Recognize();
```

**Tại sao nó hoạt động:** Nội bộ, Aspose.OCR áp dụng tiền xử lý (nhị phân hoá, loại bỏ nhiễu) trước khi đưa ảnh vào bộ nhận dạng dựa trên mạng nơ‑ron được tinh chỉnh cho ngôn ngữ đã chọn.

## Bước 6: Lấy và hiển thị văn bản đã nhận dạng (chuyển PNG thành văn bản)

Sau khi nhận dạng, chuỗi đã trích xuất có sẵn qua thuộc tính `Text`. Đây là bước cuối cùng trong **chuyển PNG thành văn bản**.

```csharp
// Get the recognized text
string recognizedText = ocrEngine.Text;

// Output the result
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(recognizedText);
```

### Kết quả mong đợi

Nếu `sample_image.png` chứa cụm từ Cyrillic “Привет мир”, console sẽ hiển thị:

```
=== OCR Result ===
Привет мир
```

Kết quả có thể bao gồm các dấu ngắt dòng và dấu câu chính xác như trong ảnh. Bạn có thể xử lý hậu kỳ chuỗi bằng `String.Trim()`, `Regex`, hoặc các tiện ích làm sạch văn bản khác nếu cần.

## Bước 7: Tùy chọn – Lưu kết quả vào tệp

Lưu kết quả OCR cho phép xử lý tiếp theo (ví dụ, lập chỉ mục, dịch thuật). Dưới đây là cách nhanh để ghi văn bản vào tệp UTF‑8:

```csharp
File.WriteAllText(@"YOUR_DIRECTORY/ocr_output.txt", recognizedText, Encoding.UTF8);
Console.WriteLine("OCR text saved to ocr_output.txt");
```

## Các vấn đề thường gặp và cách tránh chúng

| Vấn đề | Triệu chứng | Giải pháp |
|-------|----------|-----|
| **Thiếu mô-đun ngôn ngữ** | `OcrException` on `Language = Language.Cyrillic` | Đảm bảo kết nối internet khi chạy lần đầu hoặc tải trước các mô-đun qua gói offline của Aspose. |
| **Ảnh mờ hoặc độ tương phản thấp** | Độ chính xác kém, nhiều ký tự “?” | Tiền xử lý ảnh: tăng độ tương phản, áp dụng làm nét, hoặc chuyển sang grayscale trước khi đưa vào engine. |
| **PNG rất lớn** | Thời gian xử lý lâu, có thể `OutOfMemoryException` | Giảm kích thước như trong Bước 3, hoặc chia ảnh đa trang thành các tile riêng. |
| **Ký tự không phải UTF‑8** | Kết quả bị rối | Xác minh console hoặc bộ ghi tệp sử dụng mã hoá UTF‑8 (`Encoding.UTF8`). |

## Ví dụ đầy đủ, có thể chạy

Dưới đây là chương trình hoàn chỉnh tích hợp tất cả các bước ở trên. Sao chép nó vào một dự án console mới và chạy sau khi điều chỉnh các đường dẫn tệp.

```csharp
using System;
using System.Drawing;
using System.IO;
using System.Text;
using Aspose.OCR;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1. Create OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // 2. Load PNG image (with optional down‑scaling for large files)
            string imagePath = @"YOUR_DIRECTORY/sample_image.png";
            Bitmap original = new Bitmap(imagePath);
            const int maxWidth = 1200;

            if (original.Width > maxWidth)
            {
                int newHeight = (int)(original.Height * (maxWidth / (double)original.Width));
                Bitmap resized = new Bitmap(original, new Size(maxWidth, newHeight));

                using (var ms = new MemoryStream())
                {
                    resized.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
                    ocrEngine.Image = ImageStream.FromStream(ms);
                }
            }
            else
            {
                ocrEngine.Image = ImageStream.FromFile(imagePath);
            }

            // 3. Set language to Cyrillic (fallback to English if needed)
            try
            {
                ocrEngine.Language = Language.Cyrillic;
            }
            catch (OcrException ex)
            {
                Console.WriteLine($"Failed to load Cyrillic module: {ex.Message}");
                Console.WriteLine("Falling back to English.");
                ocrEngine.Language = Language.English;
            }

            // 4. Recognize text
            ocrEngine.Recognize();

            // 5. Retrieve and display the text (convert PNG to text)
            string recognizedText = ocrEngine.Text;
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(recognizedText);

            // 6. Save result to a UTF‑8 file
            string outputPath = @"YOUR_DIRECTORY/ocr_output.txt";
            File.WriteAllText(outputPath, recognizedText, Encoding.UTF8);
            Console.WriteLine($"OCR text saved to {outputPath}");
        }
    }
}
```

### Cách hoạt động

1. **Engine creation** – chuẩn bị pipeline OCR.  
2. **Image loading** – hỗ trợ cả PNG gốc và phiên bản đã giảm kích thước để tăng hiệu năng.  
3. **Language selection** – minh họa **trích xuất văn bản Cyrillic** đồng thời xử lý các mô-đun thiếu.  
4. **Recognition** – lời gọi cốt lõi **nhận dạng văn bản từ PNG**.  
5. **Result handling** – hiển thị **chuyển PNG thành văn bản** và ghi kết quả ra tệp.

Chạy chương trình bằng `dotnet run`. Nếu mọi thứ đã được cấu hình đúng, bạn sẽ thấy văn bản đã nhận dạng được in ra console và lưu vào `ocr_output.txt`.

## Kết luận

Trong tutorial này, bạn đã học **cách thực hiện OCR** trên các tệp PNG bằng Aspose.OCR cho .NET, bao gồm mọi thứ từ **tải ảnh cho OCR** đến **trích xuất văn bản Cyrillic** và **chuyển PNG thành văn bản**. Ví dụ đầy đủ, có thể chạy minh họa quy trình chuẩn, các trường hợp đặc biệt thường gặp, và các mẹo thực tiễn giúp pipeline OCR của bạn luôn ổn định.

**Bước tiếp theo**

* Khám phá **nhận dạng văn bản từ PNG** với các ngôn ngữ bổ sung (Arabic, Chinese) bằng cách kết hợp các cờ `Language`.  
* Tích hợp kết quả OCR với Azure Cognitive Search để tạo kho lưu trữ tài liệu có thể tìm kiếm.  
* Thử nghiệm các cài đặt của `OcrEngine` trong Aspose.OCR như `Resolution

## Bạn nên học gì tiếp theo?

Các tutorial sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên đều có các ví dụ mã hoạt động đầy đủ với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách tải mô hình Aspose.OCR và trích xuất văn bản từ PNG trong C#](/ocr/english/net/text-recognition/how-to-download-ocr-model-and-extract-text-from-png-using-as/)
- [Cách thực hiện OCR trong C# – Nhận dạng văn bản Cyrillic với Aspose](/ocr/english/net/text-recognition/how-to-perform-ocr-in-c-recognize-cyrillic-text-with-aspose/)
- [Cách thực hiện OCR hàng loạt trong C# – Cách nhanh để trích xuất văn bản từ các tệp PNG](/ocr/english/net/ocr-optimization/how-to-batch-ocr-in-c-fast-way-to-extract-text-png-files/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}