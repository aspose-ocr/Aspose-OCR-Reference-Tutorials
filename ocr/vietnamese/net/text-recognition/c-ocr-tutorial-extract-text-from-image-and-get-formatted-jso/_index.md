---
category: general
date: 2026-01-13
description: Hướng dẫn C# OCR cho thấy cách trích xuất văn bản từ hình ảnh, tải hình
  ảnh để OCR và định dạng đầu ra JSON bằng Aspose OCR. Học cách tuần tự hoá đối tượng
  thành JSON.
draft: false
keywords:
- c# ocr tutorial
- extract text from image
- format json output
- serialize object to json
- load image for ocr
language: vi
og_description: Hướng dẫn c# OCR giúp bạn thực hiện việc trích xuất văn bản từ hình
  ảnh, tải hình ảnh cho OCR và định dạng đầu ra JSON bằng Aspose OCR.
og_title: c# OCR tutorial – Trích xuất văn bản & Định dạng JSON
tags:
- OCR
- C#
- JSON
title: Hướng dẫn OCR bằng C# – Trích xuất văn bản từ hình ảnh và nhận JSON định dạng
url: /vi/net/text-recognition/c-ocr-tutorial-extract-text-from-image-and-get-formatted-jso/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – Trích xuất Văn bản từ Hình ảnh và Định dạng Đầu ra JSON

Bạn đã bao giờ tự hỏi làm thế nào để **trích xuất văn bản từ hình ảnh** trong một dự án C# mà không phải vật lộn với xử lý pixel mức thấp? Đó là vấn đề mà *c# ocr tutorial* này giải quyết. Chỉ trong vài phút, bạn sẽ thấy cách **tải hình ảnh cho ocr**, chạy Aspose OCR, và **định dạng đầu ra json** để có thể đưa dữ liệu thẳng vào API hoặc cơ sở dữ liệu của mình.

Chúng tôi sẽ đi qua từng dòng code, giải thích tại sao mỗi phần lại quan trọng, và thậm chí cho bạn thấy JSON chính xác mà bạn nên mong đợi. Khi kết thúc, bạn sẽ có một ứng dụng console sẵn sàng chạy, chuyển đổi một file PNG hoá đơn thành JSON sạch sẽ, có thụt lề. Không có phần thừa, chỉ là giải pháp thực tiễn mà bạn có thể đưa vào bất kỳ dự án .NET 6+ nào.

## Những gì c# ocr tutorial này sẽ đề cập

- Cài đặt gói NuGet Aspose.OCR  
- Tải một file hình ảnh để xử lý OCR  
- Nhận dạng văn bản tiếng Anh (hoặc bất kỳ ngôn ngữ nào được hỗ trợ)  
- **Serializing kết quả OCR thành JSON** với định dạng đẹp mắt  
- Hiển thị JSON trong console và lưu lại nếu muốn  

Bạn chỉ cần hiểu cơ bản về C# và một .NET SDK mới. Không cần gì hơn. Nếu tò mò về cách **trích xuất văn bản từ hình ảnh** cho hoá đơn, biên lai, hoặc các mẫu quét, hãy tiếp tục đọc.

---

## Bước 1: Thiết lập Môi trường c# ocr tutorial

Trước khi viết bất kỳ code nào, hãy chắc chắn rằng bạn có các công cụ cần thiết:

1. **.NET 6 SDK hoặc mới hơn** – bạn có thể tải từ trang của Microsoft.  
2. **Visual Studio 2022** (Community hoàn toàn đủ) hoặc bất kỳ trình soạn thảo nào bạn thích.  
3. **Gói NuGet Aspose.OCR** – chạy `dotnet add package Aspose.OCR` trong thư mục dự án của bạn.

> **Pro tip:** Nếu bạn đang dùng pipeline CI, hãy thêm tham chiếu gói vào file `.csproj` để quá trình build tự động khôi phục.

---

## Bước 2: Tải Hình ảnh cho OCR

Bước thực tế đầu tiên trong tutorial của chúng ta là lấy hình ảnh bạn muốn xử lý. Aspose OCR hỗ trợ các định dạng phổ biến như PNG, JPEG và TIFF.

```csharp
using Aspose.OCR;
using System.Text.Json;

// Replace this with the actual path to your invoice image
string imagePath = @"C:\Invoices\invoice.png";

// Create an OcrImage instance from the file system
OcrImage inputImage = OcrImage.FromFile(imagePath);
```

> **Tại sao điều này quan trọng:** Việc tải hình ảnh dưới dạng `OcrImage` cho phép engine truy cập dữ liệu bitmap và bất kỳ thông tin DPI nào, giúp cải thiện độ chính xác nhận dạng. Bỏ qua bước này hoặc đưa vào file bị hỏng sẽ gây ra ngoại lệ thời gian chạy.

---

## Bước 3: Trích xuất Văn bản từ Hình ảnh

Bây giờ chúng ta thực sự chạy engine OCR. Phương thức `Recognize` trả về một đối tượng `OcrResult` phong phú, chứa văn bản thô, điểm tin cậy và chi tiết bố cục.

```csharp
// Initialize the OCR engine – no license needed for a trial run
OcrEngine ocrEngine = new OcrEngine();

// Recognize English text (you can change the language enum if needed)
OcrResult ocrResult = ocrEngine.Recognize(inputImage, OcrLanguage.English);
```

> **Trường hợp đặc biệt:** Nếu bạn cần xử lý tài liệu đa ngôn ngữ, hãy gọi `Recognize` hai lần với các giá trị `OcrLanguage` khác nhau và nối kết quả lại. Engine an toàn với đa luồng, vì vậy bạn thậm chí có thể song song xử lý các batch lớn.

---

## Bước 4: Serialize Đối tượng thành JSON – Định dạng Đầu ra JSON

Đối tượng `OcrResult` là một lớp C# đơn giản, vì vậy chúng ta có thể đưa nó cho `System.Text.Json`. Khi bật `WriteIndented`, đầu ra sẽ dễ đọc cho con người.

```csharp
// Serialize the OCR result with pretty printing
string json = JsonSerializer.Serialize(ocrResult, new JsonSerializerOptions
{
    WriteIndented = true
});
```

> **Bạn sẽ nhận được:** Một chuỗi JSON được thụt lề đẹp mắt, bao gồm văn bản đã nhận dạng, độ tin cậy và bố cục trang. Điều này hoàn hảo cho việc ghi log, gửi tới dịch vụ web, hoặc lưu trữ trong cơ sở dữ liệu NoSQL.

---

## Bước 5: Hiển thị và (Tùy chọn) Lưu JSON Định dạng

Cuối cùng, chúng ta xuất JSON ra console. Bạn cũng có thể ghi nó vào file bằng `File.WriteAllText` nếu muốn.

```csharp
// Show the JSON in the console
Console.WriteLine(json);

// Optional: Save to a .json file next to the image
string jsonPath = Path.ChangeExtension(imagePath, ".json");
File.WriteAllText(jsonPath, json);
Console.WriteLine($"\nJSON saved to: {jsonPath}");
```

**Đầu ra console dự kiến (rút gọn để ngắn gọn):**

```json
{
  "Text": "Invoice #12345\nDate: 2025‑12‑01\nTotal: $250.00",
  "Confidence": 0.97,
  "Pages": [
    {
      "PageNumber": 1,
      "Blocks": [
        {
          "Text": "Invoice #12345",
          "Confidence": 0.99,
          "Rectangle": { "X": 50, "Y": 30, "Width": 200, "Height": 30 }
        }
        // …more blocks…
      ]
    }
  ]
}
```

Nếu engine OCR không tìm thấy bất kỳ văn bản nào, trường `Text` sẽ là chuỗi rỗng và `Confidence` sẽ là `0`. Đó là dấu hiệu để bạn kiểm tra lại chất lượng hình ảnh.

---

## Bước 6: Ví dụ Hoàn chỉnh Hoạt động

Kết hợp mọi thứ lại, đây là chương trình đầy đủ mà bạn có thể sao chép‑dán vào một ứng dụng console mới:

```csharp
using Aspose.OCR;
using System;
using System.IO;
using System.Text.Json;

class JsonResultDemo
{
    static void Main()
    {
        // 1️⃣ Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load the source image (replace with your own path)
        string imagePath = @"C:\Invoices\invoice.png";
        OcrImage inputImage = OcrImage.FromFile(imagePath);

        // 3️⃣ Recognize text – this is the core of our c# ocr tutorial
        OcrResult ocrResult = ocrEngine.Recognize(inputImage, OcrLanguage.English);

        // 4️⃣ Serialize the result with pretty formatting
        string json = JsonSerializer.Serialize(ocrResult, new JsonSerializerOptions
        {
            WriteIndented = true
        });

        // 5️⃣ Output to console and optionally write to a file
        Console.WriteLine(json);
        string jsonPath = Path.ChangeExtension(imagePath, ".json");
        File.WriteAllText(jsonPath, json);
        Console.WriteLine($"\nJSON saved to: {jsonPath}");
    }
}
```

Chạy chương trình (`dotnet run` từ thư mục dự án) và quan sát console in ra một biểu diễn JSON được định dạng đẹp mắt của hoá đơn đã quét.

---

## Những Cạm Bẫy Thường Gặp & Mẹo (c# ocr tutorial Extras)

| Vấn đề | Tại sao xảy ra | Cách khắc phục |
|-------|----------------|----------------|
| **Trường `Text` trống** | Hình ảnh có độ tương phản thấp hoặc bị xoay. | Tiền xử lý hình ảnh (tăng độ tương phản, cân chỉnh) hoặc dùng `OcrEngine.ImagePreprocess`. |
| **`System.DllNotFoundException`** | Thiếu binary gốc của Aspose OCR. | Đảm bảo gói NuGet đã được khôi phục đúng và kiến trúc runtime (x64/x86) phù hợp với hệ điều hành. |
| **Độ trễ khi xử lý PDF lớn** | OCR xử lý từng trang một cách tuần tự. | Song song hoá bằng cách tạo các instance `OcrEngine` riêng cho mỗi trang (engine an toàn đa luồng). |
| **JSON quá lớn** | Bạn đang serialize mọi chi tiết, bao gồm cả bounding box. | Sử dụng DTO chỉ chứa `Text` và `Confidence` trước khi serialize. |

> **Nhớ:** Mục tiêu của tutorial này là trình bày một luồng công việc sạch sẽ, từ đầu tới cuối. Bạn luôn có thể cắt bớt JSON hoặc thêm metadata sau này.

---

## Kết luận

Bạn vừa hoàn thành một **c# ocr tutorial** giúp tải hình ảnh, **trích xuất văn bản từ hình ảnh**, và tạo **định dạng json output** bằng cách **serializing đối tượng thành json**. Các bước đơn giản, code đã sẵn sàng chạy, và JSON được thụt lề hoàn hảo cho các hệ thống downstream.

Tiếp theo bạn muốn làm gì? Hãy thử đổi `OcrLanguage.English` sang `OcrLanguage.French` hoặc đưa một thư mục các biên lai vào vòng lặp. Bạn cũng có thể khám phá việc lưu JSON trực tiếp vào Azure Blob Storage hoặc đưa vào mô hình machine‑learning.

Nếu gặp khó khăn, hãy kiểm tra lại đường dẫn hình ảnh và chắc chắn rằng giấy phép Aspose OCR (nếu có) đã được tải trước khi gọi `Recognize`. Chúc bạn lập trình vui vẻ, và hy vọng kết quả OCR luôn sắc nét!

--- 

*Image illustrating the OCR flow (alt text: "c# ocr tutorial diagram showing load image, recognize text, serialize to JSON")*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}