---
category: general
date: 2026-09-06
description: Chuyển đổi OCR hình ảnh sang JSON trong C# bằng Aspose.OCR – hướng dẫn
  chi tiết từng bước để trích xuất văn bản từ hình ảnh và nhận kết quả dưới dạng JSON.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- ocr image to json
- extract text from image
- convert image to text
- recognize text from photo
- load image for ocr
language: vi
lastmod: 2026-09-06
og_description: OCR hình ảnh sang JSON trong C# với Aspose.OCR. Tìm hiểu cách tải
  hình ảnh để OCR, nhận dạng văn bản từ ảnh và chuyển kết quả sang JSON.
og_image_alt: Screenshot of C# code that converts an OCR image to JSON using Aspose.OCR
og_title: Chuyển đổi ảnh OCR sang JSON trong C# – hướng dẫn đầy đủ Aspose.OCR
schemas:
- author: Aspose
  dateModified: '2026-09-06'
  description: ocr image to json conversion in C# using Aspose.OCR – step‑by‑step
    guide to extract text from image and get JSON output.
  headline: How to convert an OCR image to JSON in C# with Aspose.OCR
  type: TechArticle
- description: ocr image to json conversion in C# using Aspose.OCR – step‑by‑step
    guide to extract text from image and get JSON output.
  name: How to convert an OCR image to JSON in C# with Aspose.OCR
  steps:
  - name: Place an image named `input.jpg` in the project root.
    text: Place an image named `input.jpg` in the project root.
  - name: Execute `dotnet run`.
    text: Execute `dotnet run`.
  - name: Observe the console output and open `output.json` to see the structured
      data.
    text: Observe the console output and open `output.json` to see the structured
      data.
  type: HowTo
- questions:
  - answer: Yes. Use `ocrEngine.SaveJson(Stream)` to write directly to a `MemoryStream`,
      then call `stream.ToArray()`.
    question: Can I get the OCR result as a byte array instead of a file?
  - answer: Aspose.OCR can accept PDF pages converted to images via Aspose.PDF, but
      the OCR engine itself works on raster images. Convert PDFs to images first,
      then **load image for ocr**.
    question: Does the engine support PDF input?
  - answer: 'Set `ocrEngine.Language = OcrLanguage.Arabic`. The JSON includes the
      correct text direction, which you can render in UI frameworks that support RTL.
      ## Conclusion You now have a complete solution for **ocr image to json** in
      C#. By loading an image, configuring the language, running the OCR engine, '
    question: How do I handle right‑to‑left scripts like Arabic?
  type: FAQPage
tags:
- Aspose.OCR
- C#
- JSON
- Image processing
title: Cách chuyển đổi hình ảnh OCR sang JSON trong C# với Aspose.OCR
url: /vi/net/text-recognition/how-to-convert-an-ocr-image-to-json-in-c-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách chuyển đổi hình ảnh OCR sang JSON trong C# với Aspose.OCR

Nếu bạn cần **ocr image to json** trong một ứng dụng .NET, hướng dẫn này sẽ chỉ cho bạn cách thực hiện với Aspose.OCR. Chúng tôi sẽ hướng dẫn cách tải hình ảnh để OCR, nhận dạng văn bản từ ảnh, và chuyển đổi kết quả sang JSON để bạn có thể sử dụng dữ liệu trong API hoặc cơ sở dữ liệu.

Trích xuất văn bản từ các tệp hình ảnh là một yêu cầu phổ biến cho việc xử lý hoá đơn, quét biên lai và các dự án lưu trữ. Khi kết thúc tutorial này, bạn sẽ có thể **convert image to text**, lấy kết quả văn bản thuần, và tạo một payload JSON có cấu trúc giữ nguyên thông tin bố cục.

## Yêu cầu trước

- .NET 6.0 SDK hoặc phiên bản mới hơn đã được cài đặt  
- Visual Studio 2022 (hoặc bất kỳ trình chỉnh sửa nào hỗ trợ .NET)  
- Gói NuGet Aspose.OCR (`Aspose.OCR`) đã được thêm vào dự án của bạn  
- Một hình ảnh mẫu (`input.jpg`) đặt trong thư mục mà bạn có thể tham chiếu từ mã  

Bạn không cần bất kỳ engine OCR bổ sung nào; Aspose.OCR tự xử lý phần nặng bên trong.

## Bước 1: Cài đặt gói NuGet Aspose.OCR

Mở terminal tại thư mục dự án của bạn và chạy:

```bash
dotnet add package Aspose.OCR
```

Gói này bao gồm lớp `Aspose.OCR.OcrEngine`, cung cấp các phương thức để **load image for ocr**, chọn ngôn ngữ, và xuất kết quả.

## Bước 2: Tạo một dự án console C# mới

Nếu bạn chưa có dự án, hãy tạo một dự án mới:

```bash
dotnet new console -n OcrToJsonDemo
cd OcrToJsonDemo
```

Thêm các chỉ thị `using` mà bạn sẽ cần:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;
using System.IO;
```

## Bước 3: Tải hình ảnh và cấu hình engine OCR

Mã dưới đây minh họa cách **load image for ocr**, đặt ngôn ngữ, và chuẩn bị engine để xử lý. Trong ví dụ này chúng tôi sử dụng Cyrillic, nhưng bạn có thể chuyển sang `OcrLanguage.English`, `OcrLanguage.French`, v.v., tùy thuộc vào ngôn ngữ nguồn.

```csharp
// Step 3: Initialize the OCR engine
var ocrEngine = new OcrEngine();

// Choose the language that matches the text in the image.
// Replace OcrLanguage.Cyrillic with the language you need.
ocrEngine.Language = OcrLanguage.Cyrillic;

// Load the image file. The ImageStream class abstracts file, stream, or byte[] sources.
string imagePath = Path.Combine(Environment.CurrentDirectory, "input.jpg");
ocrEngine.Image = ImageStream.FromFile(imagePath);
```

> **Tại sao điều này quan trọng:** Đặt ngôn ngữ đúng sẽ cải thiện đáng kể độ chính xác khi bạn **recognize text from photo**. Engine sử dụng các từ điển và bộ ký tự đặc thù cho từng ngôn ngữ.

## Bước 4: Chạy quá trình OCR và lấy kết quả

Bây giờ chạy engine OCR. Nếu quá trình thành công, bạn có thể **extract text from image** dưới dạng plain text, HTML, hoặc JSON. Aspose.OCR cung cấp phương thức `SaveJson` để ghi kết quả có cấu trúc vào tệp.

```csharp
// Step 4: Execute the OCR process
if (ocrEngine.Process())
{
    // Plain‑text output
    string plainText = ocrEngine.Text;
    Console.WriteLine("=== Plain Text ===");
    Console.WriteLine(plainText);

    // JSON output – includes bounding boxes, confidence scores, and line information
    string jsonPath = Path.Combine(Environment.CurrentDirectory, "output.json");
    ocrEngine.SaveJson(jsonPath);
    Console.WriteLine($"\nJSON result saved to: {jsonPath}");
}
else
{
    Console.WriteLine("OCR processing failed. Check the image path and format.");
}
```

### Cấu trúc JSON dự kiến

Một tệp `output.json` điển hình trông như sau (định dạng để dễ đọc):

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Text": "Пример текста",
          "Confidence": 0.96,
          "Rect": { "X": 45, "Y": 120, "Width": 210, "Height": 30 }
        },
        {
          "Text": "Еще одна строка",
          "Confidence": 0.93,
          "Rect": { "X": 45, "Y": 160, "Width": 230, "Height": 28 }
        }
      ]
    }
  ]
}
```

Payload JSON chứa văn bản của mỗi dòng, điểm confidence, và hình chữ nhật bao quanh dòng trong ảnh gốc. Điều này giúp dễ dàng ánh xạ kết quả OCR trở lại các phần tử UI hoặc trường cơ sở dữ liệu.

## Bước 5: Mã nguồn đầy đủ cho demo

Dưới đây là chương trình hoàn chỉnh, sẵn sàng chạy thực hiện quy trình **ocr image to json**. Sao chép vào `Program.cs` và chạy `dotnet run`.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace OcrToJsonDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Select the language (Cyrillic in this example)
            ocrEngine.Language = OcrLanguage.Cyrillic;

            // 3️⃣ Load the image you want to process
            string imagePath = Path.Combine(Environment.CurrentDirectory, "input.jpg");
            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"Image not found: {imagePath}");
                return;
            }
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 4️⃣ Run the OCR process
            if (ocrEngine.Process())
            {
                // 5️⃣ Retrieve plain text (optional)
                string plainText = ocrEngine.Text;
                Console.WriteLine("=== Plain Text ===");
                Console.WriteLine(plainText);

                // 6️⃣ Save the result as JSON
                string jsonPath = Path.Combine(Environment.CurrentDirectory, "output.json");
                ocrEngine.SaveJson(jsonPath);
                Console.WriteLine($"\nJSON result saved to: {jsonPath}");
            }
            else
            {
                Console.WriteLine("OCR processing failed. Verify the image format and language settings.");
            }
        }
    }
}
```

### Chạy ví dụ

1. Đặt một hình ảnh có tên `input.jpg` trong thư mục gốc của dự án.  
2. Thực thi `dotnet run`.  
3. Quan sát đầu ra console và mở `output.json` để xem dữ liệu có cấu trúc.

## Mẹo chuyên nghiệp và những khó khăn thường gặp

| Situation | Recommendation |
|-----------|----------------|
| **Ảnh độ phân giải thấp** | Tăng DPI trước khi xử lý hoặc sử dụng `ocrEngine.Image = ImageStream.FromFile(path, 300)` để ép 300 DPI. |
| **Ngôn ngữ hỗn hợp** | Đặt `ocrEngine.Language = OcrLanguage.Multilingual` và tùy chọn cung cấp danh sách ngôn ngữ qua `ocrEngine.Language = new[] { OcrLanguage.English, OcrLanguage.Cyrillic }`. |
| **Tài liệu lớn** | Xử lý một trang mỗi lần để giảm mức sử dụng bộ nhớ; engine hỗ trợ TIFF đa trang. |
| **Ký tự không đúng** | Xác minh rằng `OcrLanguage` đúng đã được chọn; sử dụng ngôn ngữ sai sẽ giảm độ chính xác khi bạn **convert image to text**. |
| **JSON thiếu trường** | Đảm bảo bạn đang sử dụng Aspose.OCR phiên bản 23.6 trở lên; các phiên bản cũ hơn không cung cấp phương thức `SaveJson`. |

## Câu hỏi thường gặp

**Q: Tôi có thể nhận kết quả OCR dưới dạng mảng byte thay vì tệp không?**  
A: Có. Sử dụng `ocrEngine.SaveJson(Stream)` để ghi trực tiếp vào `MemoryStream`, sau đó gọi `stream.ToArray()`.

**Q: Engine có hỗ trợ đầu vào PDF không?**  
A: Aspose.OCR có thể nhận các trang PDF đã được chuyển đổi thành hình ảnh qua Aspose.PDF, nhưng engine OCR tự nó chỉ làm việc trên hình ảnh raster. Chuyển PDF sang hình ảnh trước, sau đó **load image for ocr**.

**Q: Làm thế nào để xử lý các script viết từ phải sang trái như tiếng Ả Rập?**  
A: Đặt `ocrEngine.Language = OcrLanguage.Arabic`. JSON sẽ bao gồm hướng văn bản đúng, bạn có thể hiển thị trong các framework UI hỗ trợ RTL.

## Kết luận

Bây giờ bạn đã có một giải pháp hoàn chỉnh cho **ocr image to json** trong C#. Bằng cách tải hình ảnh, cấu hình ngôn ngữ, chạy engine OCR, và xuất kết quả dưới dạng JSON, bạn có thể **extract text from image**, **convert image to text**, và **recognize text from photo** trong một quy trình duy nhất, gọn gàng.  

Từ đây bạn có thể khám phá:

- Tích hợp đầu ra JSON với một Web API (`ASP.NET Core`)  
- Lưu kết quả vào cơ sở dữ liệu NoSQL như MongoDB  
- Thêm xử lý hậu kỳ để sửa các lỗi OCR thường gặp  

Bạn có thể thử nghiệm với các ngôn ngữ, định dạng hình ảnh, và tùy chọn đầu ra khác nhau để phù hợp với nhu cầu dự án của mình. Chúc lập trình vui vẻ!

## Bạn nên học gì tiếp theo?

Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã đầy đủ hoạt động với các giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [nhận dạng văn bản từ hình ảnh trong C# – Hướng dẫn đầy đủ về OCR và JSON](/ocr/english/net/text-recognition/recognize-text-from-image-in-c-complete-guide-to-ocr-and-jso/)
- [Chuyển đổi hình ảnh sang văn bản trong C# với Aspose OCR – Hướng dẫn từng bước](/ocr/english/net/text-recognition/convert-image-to-text-in-c-with-aspose-ocr-step-by-step-guid/)
- [Cách trích xuất văn bản từ hình ảnh bằng Aspose.OCR cho .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}