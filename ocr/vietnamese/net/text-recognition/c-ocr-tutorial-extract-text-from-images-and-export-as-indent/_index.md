---
category: general
date: 2026-05-02
description: Hướng dẫn C# OCR cho thấy cách trích xuất văn bản từ hình ảnh, nhận dạng
  văn bản PNG, sau đó ghi JSON có thụt lề bằng JsonSerializer C#. Hướng dẫn từng bước
  dành cho các nhà phát triển.
draft: false
keywords:
- c# ocr tutorial
- extract text image c#
- recognize png text
- write indented json
- use jsonserializer c#
language: vi
og_description: Hướng dẫn OCR bằng C# minh họa cách trích xuất văn bản từ hình ảnh,
  nhận dạng văn bản PNG, sau đó ghi JSON có thụt lề bằng JsonSerializer C#. Ví dụ
  đầy đủ, có thể chạy được.
og_title: hướng dẫn OCR C# – Trích xuất văn bản và xuất dưới dạng JSON có thụt lề
tags:
- OCR
- C#
- Aspose
- JSON
title: Hướng dẫn OCR bằng C# – Trích xuất văn bản từ hình ảnh và xuất dưới dạng JSON
  có thụt lề
url: /vi/net/text-recognition/c-ocr-tutorial-extract-text-from-images-and-export-as-indent/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# hướng dẫn c# ocr – Trích xuất văn bản từ hình ảnh và xuất dưới dạng JSON có thụt lề

Bạn đã bao giờ cần một **c# ocr tutorial** chuyển từ một bức ảnh chứa văn bản ngay thành một tệp JSON được định dạng đẹp mắt? Bạn không phải là người duy nhất. Trong nhiều dự án – như quét hoá đơn, phân tích biên lai, hoặc thậm chí trích xuất văn bản meme đơn giản – bạn sẽ có một tệp PNG và tự hỏi làm sao lấy ra các từ mà không phải viết bộ nhận dạng tùy chỉnh.  

Hướng dẫn này cung cấp cho bạn một giải pháp thực tế: chúng ta sẽ **extract text image c#** sử dụng Aspose.OCR, **recognize png text**, và sau đó **write indented json** bằng `JsonSerializer` trong C#. Khi kết thúc, bạn sẽ có một ứng dụng console tự chứa mà có thể đưa vào bất kỳ giải pháp .NET nào. Không có các liên kết mơ hồ “xem tài liệu”, chỉ có một ví dụ hoàn chỉnh, sẵn sàng sao chép‑dán.

## Những gì bạn cần

- **.NET 6** (hoặc bất kỳ phiên bản .NET gần đây nào). Các framework cũ cũng hoạt động, nhưng cú pháp được trình bày nhắm vào .NET 6+.
- **Aspose.OCR for .NET** – cài đặt qua NuGet: `dotnet add package Aspose.OCR`.
- Một hình PNG mẫu (`text.png`) chứa văn bản rõ ràng, có thể đọc được bởi máy.
- Một IDE hoặc trình soạn thảo mà bạn thích – Visual Studio, VS Code, Rider, v.v.

> **Mẹo chuyên nghiệp:** Nếu bạn dự định xử lý nhiều hình ảnh, hãy cân nhắc tái sử dụng một thể hiện `OcrEngine` duy nhất thay vì tạo mới cho mỗi tệp. Điều này giảm tải và cải thiện tốc độ xử lý.

## Bước 1: Thiết lập dự án c# ocr tutorial

Đầu tiên, tạo một dự án console. Các lệnh sau tạo cấu trúc dự án và kéo thư viện OCR vào:

```bash
dotnet new console -n OcrJsonDemo
cd OcrJsonDemo
dotnet add package Aspose.OCR
```

Bây giờ mở tệp `Program.cs` đã tạo. Chúng ta sẽ thay thế nội dung của nó bằng ví dụ đầy đủ sau, nhưng hiện tại chỉ cần chắc chắn dự án biên dịch được:

```bash
dotnet build
```

Nếu không thấy lỗi nào, bạn đã sẵn sàng tiếp tục.

## Bước 2: Nhận dạng văn bản PNG từ hình ảnh

Trái tim của bất kỳ **c# ocr tutorial** nào là chính engine OCR. Aspose.OCR ẩn đi các chi tiết mức thấp và cung cấp cho bạn một lớp `OcrEngine` sạch sẽ. Dưới đây chúng ta tạo engine, chỉ tới một tệp PNG, và yêu cầu nó nhận dạng văn bản.

```csharp
using Aspose.OCR;
using System;
using System.Text.Json;

class JsonExportExample
{
    public static void Run()
    {
        // 1️⃣ Create an OCR engine instance – this is the entry point for all OCR work.
        var ocrEngine = new OcrEngine();

        // 2️⃣ Recognize text from the input image. 
        //    The method automatically detects the language (default is English) and returns an OcrResult.
        var ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/text.png");

        // If the image couldn't be read, handle it gracefully.
        if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
        {
            Console.WriteLine("No text detected – double‑check the file path and image quality.");
            return;
        }

        // Continue to serialization...
```

### Tại sao cách này hoạt động

- **`RecognizeImage`** chấp nhận nhiều định dạng (PNG, JPEG, BMP). Chúng ta đặc biệt **recognize png text** vì PNG giữ chi tiết không mất mát, rất phù hợp cho OCR.
- `OcrResult` trả về không chỉ văn bản thuần mà còn điểm tin cậy cho từng glyph, hữu ích nếu bạn cần lọc các ký tự có độ tin cậy thấp sau này.

## Bước 3: Ghi JSON có thụt lề bằng JsonSerializer c#

Bây giờ chúng ta đã có `ocrResult`, bước tiếp theo hợp lý trong **c# ocr tutorial** của chúng ta là chuyển đối tượng đó thành JSON dễ đọc cho con người. Bộ serializer tích hợp `System.Text.Json` thực hiện công việc này, và chúng ta sẽ cấu hình nó để **write indented json** nhằm tăng tính rõ ràng.

```csharp
        // 3️⃣ Serialize the OCR result (including confidence per glyph) to indented JSON.
        var jsonOptions = new JsonSerializerOptions
        {
            WriteIndented = true // This makes the output pretty‑printed.
        };

        string jsonOutput = JsonSerializer.Serialize(ocrResult, jsonOptions);

        // 4️⃣ Display the JSON result – you could also write it to a file if you prefer.
        Console.WriteLine(jsonOutput);
    }
}
```

### Sử dụng `JsonSerializer` đúng cách

- Cờ `WriteIndented` là cách đơn giản nhất để **write indented json** mà không cần đưa thư viện bên thứ ba.
- Nếu bạn cần tên thuộc tính dạng camel‑case, hãy thêm `PropertyNamingPolicy = JsonNamingPolicy.CamelCase` vào tùy chọn.
- Chuỗi `jsonOutput` có thể được lưu bằng `File.WriteAllText("result.json", jsonOutput);` – một thủ thuật hữu ích cho các pipeline thực tế.

## Bước 4: Chạy và Kiểm tra Kết quả

Biên dịch và chạy chương trình:

```bash
dotnet run
```

Giả sử `text.png` chứa cụm từ *“Hello, OCR World!”*, bạn sẽ thấy kết quả tương tự:

```json
{
  "Text": "Hello, OCR World!",
  "Confidence": 0.9875,
  "Lines": [
    {
      "Text": "Hello, OCR World!",
      "Confidence": 0.9875,
      "Words": [
        {
          "Text": "Hello,",
          "Confidence": 0.9921,
          "BoundingBox": { "X": 12, "Y": 34, "Width": 58, "Height": 20 }
        },
        {
          "Text": "OCR",
          "Confidence": 0.9812,
          "BoundingBox": { "X": 78, "Y": 34, "Width": 34, "Height": 20 }
        },
        {
          "Text": "World!",
          "Confidence": 0.9890,
          "BoundingBox": { "X": 118, "Y": 34, "Width": 62, "Height": 20 }
        }
      ]
    }
  ]
}
```

JSON đó **được thụt lề**, giúp dễ đọc trong log hoặc chuyển giao cho các dịch vụ hạ nguồn.

### Trường hợp đặc biệt & Mẹo

| Situation | What to Do |
|-----------|------------|
| **Image is blurry** | Tăng `ocrEngine.Config.Dpi` (ví dụ, `ocrEngine.Config.Dpi = 300`) trước khi gọi `RecognizeImage`. |
| **Non‑English language** | Đặt `ocrEngine.Config.Language = OcrLanguage.German` (hoặc bất kỳ ngôn ngữ nào được hỗ trợ). |
| **Large batch of files** | Duyệt qua một thư mục, tái sử dụng cùng một thể hiện `OcrEngine`; lưu mỗi kết quả JSON với tên tệp duy nhất. |
| **Need only high‑confidence text** | Lọc `ocrResult.Lines` nơi `Confidence` ≥ 0.95 trước khi serialize. |

## Ví dụ Hoạt động Đầy đủ (Sẵn sàng Sao chép‑Dán)

Dưới đây là chương trình *toàn bộ*, sẵn sàng đưa vào `Program.cs`. Nó bao gồm tất cả các bước, xử lý lỗi, và các chú thích giúp mã tự giải thích.

```csharp
using Aspose.OCR;
using System;
using System.IO;
using System.Text.Json;

class JsonExportExample
{
    public static void Main()
    {
        // 👉 Step 1: Initialize the OCR engine.
        var ocrEngine = new OcrEngine();

        // 👉 Step 2: Path to the PNG image you want to process.
        string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "text.png");

        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"Image not found at {imagePath}");
            return;
        }

        // 👉 Step 3: Perform OCR – this is where we **recognize png text**.
        var ocrResult = ocrEngine.RecognizeImage(imagePath);

        // 👉 Step 4: Validate the result.
        if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
        {
            Console.WriteLine("No recognizable text found. Try a clearer image or adjust DPI settings.");
            return;
        }

        // 👉 Step 5: Configure JsonSerializer to **write indented json**.
        var jsonOptions = new JsonSerializerOptions
        {
            WriteIndented = true // Pretty‑print the JSON.
        };

        // 👉 Step 6: Serialize the OCR result – this demonstrates **use jsonserializer c#**.
        string jsonOutput = JsonSerializer.Serialize(ocrResult, jsonOptions);

        // 👉 Step 7: Output to console (or write to a file).
        Console.WriteLine(jsonOutput);

        // Optional: Save to disk.
        string outputPath = Path.ChangeExtension(imagePath, ".json");
        File.WriteAllText(outputPath, jsonOutput);
        Console.WriteLine($"JSON saved to {outputPath}");
    }
}
```

Chạy mã, kiểm tra console hoặc tệp `.json` được tạo, và bạn sẽ thấy văn bản đã trích xuất cùng với điểm tin cậy, tất cả đều **được thụt lề** một cách gọn gàng.

## Kết luận

Bây giờ bạn đã có một **c# ocr tutorial** vững chắc, cho thấy cách **extract text image c#**, **recognize png text**, và **write indented json** bằng `JsonSerializer`. Ví dụ này hoàn chỉnh, có thể chạy, và bao gồm các mẹo thực tiễn cho các tình huống thực tế.  

Bước tiếp theo? Hãy thử thay thế Aspose.OCR bằng một engine khác (ví dụ, Tesseract) và xem cấu trúc `OcrResult` thay đổi như thế nào, hoặc đưa JSON vào một API hạ nguồn lưu trữ dữ liệu OCR trong cơ sở dữ liệu. Bạn cũng có thể thử nghiệm các tùy chọn **use jsonserializer c#** như bộ chuyển đổi tùy chỉnh cho định dạng ngày hoặc xử lý enum.

Chúc lập trình vui vẻ, và hy vọng các pipeline OCR của bạn luôn chính xác!  

---  

![sơ đồ hướng dẫn c# ocr](image.png "Sơ đồ minh họa quy trình OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}