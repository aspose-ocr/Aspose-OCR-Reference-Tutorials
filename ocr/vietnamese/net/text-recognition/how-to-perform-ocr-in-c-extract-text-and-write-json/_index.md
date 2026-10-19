---
category: general
date: 2026-02-09
description: Học cách thực hiện OCR trong C# để trích xuất văn bản từ hình ảnh, nhận
  dạng văn bản từ PNG và nhanh chóng ghi file JSON bằng C#.
draft: false
keywords:
- how to perform OCR
- extract text from image
- recognize text from png
- write json file c#
language: vi
og_description: Cách thực hiện OCR trong C#? Hãy làm theo hướng dẫn từng bước này
  để trích xuất văn bản từ hình ảnh, nhận dạng văn bản từ PNG và ghi file JSON bằng
  C# một cách hiệu quả.
og_title: Cách thực hiện OCR trong C# – Trích xuất văn bản và ghi JSON
tags:
- OCR
- C#
- Aspose
- JSON
title: Cách thực hiện OCR trong C# – Trích xuất văn bản và ghi JSON
url: /vi/net/text-recognition/how-to-perform-ocr-in-c-extract-text-and-write-json/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Thực Hiện OCR trong C# – Hướng Dẫn Toàn Diện

Thực hiện OCR trong C# là một rào cản phổ biến khi bạn cần **extract text from image** files. Trong hướng dẫn này, chúng tôi sẽ hướng dẫn cách nhận dạng văn bản từ PNG, xuất kết quả chi tiết thành chuỗi JSON, và cuối cùng **write JSON file C#** kiểu C#. Bạn đã bao giờ nhìn vào một mẫu quét và tự hỏi làm sao biến những đường nét lộn xộn thành văn bản có thể tìm kiếm được chưa? Bạn không cô đơn; nhiều nhà phát triển gặp phải vấn đề này ngay từ đầu.

Chúng tôi sẽ sử dụng thư viện Aspose.OCR vì nó cung cấp độ tin cậy từng ký hiệu ngay từ đầu và hoạt động tốt với các dự án .NET 6+. Khi kết thúc hướng dẫn này, bạn sẽ có một ứng dụng console sẵn sàng chạy, tải một PNG, trích xuất mọi ký tự và lưu một tệp JSON gọn gàng mà bạn có thể đưa vào cơ sở dữ liệu hoặc mô hình AI. Không có các phím tắt bí ẩn “xem tài liệu”—chỉ có một giải pháp tự chứa.

## Những Gì Bạn Cần

- **.NET 6 SDK** (hoặc phiên bản mới hơn) – phiên bản LTS hiện tại tại thời điểm viết.
- **Aspose.OCR for .NET** gói NuGet – `Install-Package Aspose.OCR`.
- Một ảnh PNG bạn muốn quét (ví dụ, `form.png`).  
- Một IDE hoặc trình chỉnh sửa – Visual Studio, VS Code, Rider – bất kỳ công cụ nào bạn thoải mái sử dụng.

Đó là tất cả. Nếu bạn đã có những thành phần này, bạn đã sẵn sàng.

![Ví dụ thực hiện OCR](ocr-example.png "Cách thực hiện OCR trong C#")

*Văn bản thay thế hình ảnh: minh họa cách thực hiện OCR cho thấy một ứng dụng console C# xử lý một PNG.*

## Bước 1: Thiết Lập Dự Án và Thêm Các Phụ Thuộc

Đầu tiên, tạo một dự án console mới và kéo thư viện Aspose OCR vào.

```csharp
// Create a new console app (run in terminal)
dotnet new console -n OcrJsonDemo
cd OcrJsonDemo

// Add Aspose.OCR NuGet package
dotnet add package Aspose.OCR
```

> **Mẹo chuyên nghiệp:** Sử dụng cờ `--framework net6.0` nếu bạn muốn khóa phiên bản framework mục tiêu một cách rõ ràng.

Tại sao bước này quan trọng: gói NuGet chứa các lớp `OcrEngine`, `ImageStream` và `JsonExporter` mà chúng ta sẽ dựa vào. Nếu không có nó, trình biên dịch sẽ không biết “OCR” là gì.

## Bước 2: Viết Logic OCR Cốt Lõi

Mở `Program.cs` (hoặc tạo một tệp mới) và thay thế nội dung của nó bằng đoạn dưới đây. Mỗi phần đều có chú thích để bạn hiểu lý do tại sao nó tồn tại.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Export;
using System;

namespace OcrJsonDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Initialize the OCR engine – this prepares the
            //    internal models and allocates native resources.
            // -------------------------------------------------
            OcrEngine ocrEngine = new OcrEngine();

            // -------------------------------------------------
            // 2️⃣ Load the image you want to process.
            //    Replace the path with your own PNG file.
            // -------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY/form.png";
            ImageStream image = ImageStream.FromFile(imagePath);

            // -------------------------------------------------
            // 3️⃣ Perform OCR recognition – the heavy lifting.
            //    The result includes text, per‑symbol confidence,
            //    and layout information.
            // -------------------------------------------------
            RecognitionResult ocrResult = ocrEngine.Recognize(image);

            // -------------------------------------------------
            // 4️⃣ Export the result to a JSON string.
            //    JsonExporter respects the confidence values.
            // -------------------------------------------------
            JsonExporter jsonExporter = new JsonExporter();
            string jsonContent = jsonExporter.ExportToString(ocrResult);

            // -------------------------------------------------
            // 5️⃣ Write the JSON to disk – this is how we
            //    **write JSON file C#** style.
            // -------------------------------------------------
            string jsonPath = @"YOUR_DIRECTORY/form.json";
            System.IO.File.WriteAllText(jsonPath, jsonContent);

            // -------------------------------------------------
            // 6️⃣ Let the user know we succeeded.
            // -------------------------------------------------
            Console.WriteLine($"JSON file saved successfully at {jsonPath}");
        }
    }
}
```

### Tại Sao Mỗi Thành Phần Quan Trọng

- **OcrEngine**: Hãy nghĩ nó như bộ não của quá trình. Nó tải các mô hình ngôn ngữ và thiết lập pipeline suy luận.
- **ImageStream.FromFile**: Xử lý bất kỳ PNG, JPEG, BMP, v.v. Nó trừu tượng hoá các quirks của I/O file.
- **RecognitionResult**: Chứa văn bản thô cùng các điểm tin cậy. Đây là nơi bạn nhận được dữ liệu chi tiết cần cho việc xác thực downstream.
- **JsonExporter**: Chuyển đổi `RecognitionResult` phong phú thành payload JSON sạch sẽ, hoàn hảo cho API.
- **File.WriteAllText**: Cách .NET đơn giản để **write JSON file C#** mà không cần phụ thuộc thêm.

## Bước 3: Chạy Ứng Dụng và Xác Minh Kết Quả

Biên dịch và thực thi chương trình:

```bash
dotnet run
```

Bạn sẽ thấy một thông báo console tương tự như:

```
JSON file saved successfully at YOUR_DIRECTORY/form.json
```

Mở `form.json` – bạn sẽ thấy một thứ gì đó như:

```json
{
  "Text": "Sample Form\nName: John Doe\nDate: 2026-02-09",
  "Symbols": [
    { "Char": "S", "Confidence": 0.99, "X": 12, "Y": 8 },
    { "Char": "a", "Confidence": 0.98, "X": 22, "Y": 8 },
    // … more symbols …
  ]
}
```

Bước **extract text from image** đã thành công, và bạn hiện có một biểu diễn JSON có thể đọc được bởi máy cho mọi ký tự.

## Bước 4: Xử Lý Các Trường Hợp Cạnh Thường Gặp

### Thiếu hoặc Tập Tin Hỏng

Nếu đường dẫn PNG sai, `ImageStream.FromFile` sẽ ném ra `FileNotFoundException`. Bao quanh mã tải trong khối try‑catch:

```csharp
try
{
    ImageStream image = ImageStream.FromFile(imagePath);
}
catch (FileNotFoundException ex)
{
    Console.Error.WriteLine($"Could not find image: {ex.Message}");
    return;
}
```

### Điểm Tin Cậy Thấp

Đôi khi OCR trả về độ tin cậy thấp cho các bản quét nhiễu. Bạn có thể lọc các ký hiệu trước khi xuất:

```csharp
ocrResult.Symbols.RemoveAll(s => s.Confidence < 0.6);
```

Điều này đảm bảo JSON chỉ chứa các ký tự đáng tin cậy một cách hợp lý—hữu ích khi bạn đưa dữ liệu vào các pipeline xác thực downstream.

### Tập Tin Lớn & Bộ Nhớ

Xử lý một PNG đa megabyte có thể làm tăng sử dụng bộ nhớ. Hãy cân nhắc stream ảnh theo các khối hoặc sử dụng `OcrEngine.RecognizeAsync` (có sẵn trong các phiên bản Aspose mới hơn) để giữ UI phản hồi.

## Bước 5: Mở Rộng Giải Pháp (Tùy Chọn)

- **Batch processing**: Lặp qua một thư mục chứa các PNG và tạo một JSON tương ứng cho mỗi tệp.
- **Database storage**: Chèn JSON vào cột SQL `NVARCHAR(MAX)` để phân tích sau này.
- **Language selection**: Đặt `ocrEngine.Language = OcrLanguage.Spanish;` nếu bạn cần hỗ trợ ngôn ngữ không phải tiếng Anh.

Tất cả các mở rộng này tuân theo cùng một mẫu **how to perform OCR** mà chúng ta đã thiết lập—khởi tạo, nhận dạng, xuất và lưu trữ.

## Câu Hỏi Thường Gặp

**Q: Điều này có hoạt động với JPG hoặc TIFF không?**  
A: Hoàn toàn có. `ImageStream.FromFile` tự động phát hiện định dạng, vì vậy bạn có thể thay thế PNG bằng bất kỳ hình ảnh raster nào được hỗ trợ.

**Q: Nếu tôi cần trích xuất văn bản từ PDF thì sao?**  
A: Đầu tiên chuyển mỗi trang PDF thành hình ảnh (ví dụ, dùng `Aspose.PDF`) rồi đưa PNG vào luồng OCR mô tả ở đây.

**Q: Tôi có thể nhận kết quả OCR dưới dạng XML thay vì JSON không?**  
A: Có. Aspose.OCR cũng cung cấp một `XmlExporter`. Thay `JsonExporter` bằng `XmlExporter` và điều chỉnh phần mở rộng tệp.

## Kết Luận

Chúng tôi đã hướng dẫn **how to perform OCR** trong C# từ đầu đến cuối, cho bạn thấy cách **extract text from image**, **recognize text from PNG**, và **write JSON file C#** một cách trơn tru. Ví dụ hoàn chỉnh, có thể chạy được nằm trong các đoạn mã ở trên, và bạn giờ đã hiểu lý do đằng sau mỗi bước—khởi tạo engine, xử lý các trường hợp cạnh, và lưu trữ kết quả.

Tiếp theo, bạn có thể khám phá các pipeline OCR batch, tích hợp đầu ra JSON với Azure Cognitive Search, hoặc thử nghiệm các mô hình ngôn ngữ tùy chỉnh. Không gì là không thể một khi bạn đã nắm vững các kiến thức cơ bản về OCR trong C#.

Nếu bạn gặp bất kỳ khó khăn nào hoặc có ý tưởng cho các mở rộng tiếp theo, hãy để lại bình luận bên dưới. Chúc lập trình vui vẻ, và tận hưởng việc biến những bản quét pixel thành dữ liệu sạch, có thể tìm kiếm!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}