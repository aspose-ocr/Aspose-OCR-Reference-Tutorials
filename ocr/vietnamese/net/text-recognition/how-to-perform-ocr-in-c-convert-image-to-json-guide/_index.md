---
category: general
date: 2026-02-17
description: Cách thực hiện OCR trong C# và chuyển đổi hình ảnh sang JSON nhanh chóng.
  Theo dõi hướng dẫn OCR C# này để trích xuất văn bản từ hình ảnh và lưu bố cục dưới
  dạng JSON.
draft: false
keywords:
- how to perform OCR
- convert image to json
- c# ocr tutorial
- extract text image c#
- load image file c#
language: vi
og_description: Cách thực hiện OCR trong C#? Hướng dẫn này cho bạn biết cách chuyển
  đổi hình ảnh sang JSON, trích xuất văn bản từ hình ảnh trong C#, và tải tệp hình
  ảnh cho OCR.
og_title: Cách thực hiện OCR trong C# – Chuyển đổi hình ảnh sang JSON
tags:
- OCR
- C#
- Aspose
title: Cách thực hiện OCR trong C# – Hướng dẫn chuyển đổi hình ảnh sang JSON
url: /vi/net/text-recognition/how-to-perform-ocr-in-c-convert-image-to-json-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách thực hiện OCR trong C# – Hướng dẫn chuyển đổi hình ảnh sang JSON

Bạn đã bao giờ tự hỏi **cách thực hiện OCR** trên biên lai, hoá đơn hoặc bất kỳ tài liệu quét nào bằng C# chưa? Bạn không phải là người duy nhất. Nhiều nhà phát triển gặp khó khăn khi cần trích xuất văn bản *và* giữ nguyên bố cục mà không phải dành hàng giờ viết bộ phân tích tùy chỉnh.  

Trong tutorial này, chúng tôi sẽ hướng dẫn chi tiết **c# ocr tutorial** cho bạn biết cách thực hiện OCR, **chuyển đổi hình ảnh sang json**, và lưu kết quả để phân tích sau. Khi hoàn thành, bạn sẽ có một ứng dụng console sẵn sàng chạy, tải một tệp hình ảnh trong C#, trích xuất văn bản và ghi một tệp JSON chi tiết chứa tọa độ, điểm tin cậy và văn bản thô.

## Các yêu cầu trước – Những gì bạn cần

- .NET 6 SDK hoặc phiên bản mới hơn (mã cũng chạy trên .NET Core)  
- Visual Studio 2022 hoặc bất kỳ trình soạn thảo nào bạn thích  
- Giấy phép Aspose OCR (bạn có thể bắt đầu với bản dùng thử miễn phí)  
- Một hình ảnh mẫu, ví dụ `receipt.png`, đặt trong thư mục bạn có thể tham chiếu  

Đó là tất cả—không cần thêm bất kỳ gói NuGet nào ngoài `Aspose.OCR`. Nếu bạn đã có những thành phần này, bạn đã sẵn sàng.

## Cách thực hiện OCR và nhận đầu ra JSON

Cốt lõi của **cách thực hiện OCR** với Aspose rất đơn giản: tạo một `OcrEngine`, cung cấp cho nó một luồng hình ảnh, gọi `Recognize`, rồi tuần tự hoá `OcrResult` thành JSON. Hãy cùng phân tích từng bước.

### Bước 1: Cài đặt gói NuGet Aspose OCR

Mở terminal trong thư mục dự án và chạy:

```bash
dotnet add package Aspose.OCR
```

> **Mẹo chuyên nghiệp:** Sử dụng tùy chọn `--version` để khóa phiên bản ổn định mới nhất (ví dụ, `23.9.0`). Điều này giúp quá trình build của bạn có thể tái tạo được.

### Bước 2: Tạo khung dự án Console

Nếu bạn chưa có dự án, tạo một dự án mới:

```bash
dotnet new console -n OcrJsonDemo
cd OcrJsonDemo
```

Bây giờ bạn đã có tệp `Program.cs` sẵn sàng cho mã sẽ **load image file c#** và bắt đầu quá trình OCR.

### Bước 3: Viết mã OCR‑to‑JSON đầy đủ

Dưới đây là chương trình hoàn chỉnh, sẵn sàng chạy. Sao chép‑dán vào `Program.cs`. Mỗi dòng đều có chú thích để bạn hiểu *tại sao* mỗi phần lại quan trọng.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonOutput
{
    static void Main()
    {
        // ---------------------------------------------------------
        // 1️⃣  Initialize the OCR engine – this object holds
        //     language settings, recognition options, etc.
        // ---------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // ---------------------------------------------------------
        // 2️⃣  Load the image you want to analyze.
        //     This demonstrates **load image file c#** in a clean way.
        // ---------------------------------------------------------
        // Replace the path with the actual location of your receipt.png
        string imagePath = Path.Combine(
            Environment.CurrentDirectory, "receipt.png");
        ImageStream image = ImageStream.FromFile(imagePath);

        // ---------------------------------------------------------
        // 3️⃣  Perform the recognition.
        //     The engine returns an OcrResult containing text,
        //     confidence scores, and layout information.
        // ---------------------------------------------------------
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // ---------------------------------------------------------
        // 4️⃣  Convert the result to a detailed JSON string.
        //     This is the heart of **convert image to json**.
        // ---------------------------------------------------------
        string jsonResult = ocrResult.ToJson();

        // ---------------------------------------------------------
        // 5️⃣  Save the JSON to disk – you can later import this into
        //     databases, analytics pipelines, or UI components.
        // ---------------------------------------------------------
        string jsonPath = Path.Combine(
            Environment.CurrentDirectory, "receipt.json");
        File.WriteAllText(jsonPath, jsonResult);

        // ---------------------------------------------------------
        // 6️⃣  Let the user know we’re done.
        // ---------------------------------------------------------
        Console.WriteLine("JSON with layout saved to " + jsonPath);
    }
}
```

#### Những gì mã thực hiện

| Bước | Tại sao quan trọng |
|------|--------------------|
| **Initialize OcrEngine** | Thiết lập ngôn ngữ mặc định (Tiếng Anh) và chuẩn bị các mô hình nội bộ. |
| **Load image file** | Sử dụng `ImageStream.FromFile` đảm bảo hình ảnh được đọc theo định dạng mà Aspose mong đợi. |
| **Recognize** | Công việc nặng — phân tích pixel, phân đoạn ký tự và tra từ điển. |
| **ToJson** | Tạo ra đầu ra có cấu trúc, bao gồm các hộp giới hạn, độ tin cậy và văn bản thô. |
| **WriteAllText** | Lưu JSON để bạn có thể chia sẻ với các dịch vụ khác. |
| **Console.WriteLine** | Cung cấp phản hồi ngay lập tức — hữu ích khi chạy từ terminal. |

> **Cảnh báo:** Nếu hình ảnh của bạn quá lớn, hãy cân nhắc thu nhỏ nó trước để cải thiện tốc độ và sử dụng bộ nhớ. Aspose cung cấp các phương thức `Resize` mà bạn có thể gọi trên `ImageStream`.

### Bước 4: Chạy ứng dụng và kiểm tra đầu ra

Từ terminal:

```bash
dotnet run
```

Bạn sẽ thấy:

```
JSON with layout saved to C:\Path\To\OcrJsonDemo\receipt.json
```

Mở `receipt.json` bằng bất kỳ trình soạn thảo nào; bạn sẽ thấy nội dung tương tự:

```json
{
  "Pages": [
    {
      "Blocks": [
        {
          "Text": "Total: $12.34",
          "Confidence": 0.98,
          "BoundingBox": { "X": 120, "Y": 340, "Width": 150, "Height": 30 }
        }
      ]
    }
  ]
}
```

JSON đó chứa **extract text image c#** cùng với siêu dữ liệu bố cục, hoàn hảo cho các quy trình xử lý tiếp theo.

## Chuyển đổi hình ảnh sang JSON – Ngoài những kiến thức cơ bản

Bây giờ bạn đã biết **cách thực hiện OCR**, hãy khám phá một vài biến thể mà bạn có thể cần trong các dự án thực tế.

### Xử lý nhiều trang

Nếu nguồn của bạn là PDF hoặc TIFF đa trang, chỉ cần lặp qua từng trang:

```csharp
foreach (var pageStream in multiPageImageStreams)
{
    OcrResult result = ocrEngine.Recognize(pageStream);
    // Append each page's JSON to a master list
}
```

### Tùy chỉnh ngôn ngữ và độ chính xác

Aspose hỗ trợ hơn 40 ngôn ngữ. Để chuyển sang tiếng Tây Ban Nha:

```csharp
ocrEngine.Language = Language.Spanish;
```

Bạn cũng có thể điều chỉnh `ocrEngine.Settings` để bật **tự động xoay**, **loại bỏ nhiễu**, hoặc **sửa lỗi dựa trên từ điển** — tất cả đều cải thiện chất lượng JSON bạn nhận được.

### Lưu JSON ở định dạng đẹp (pretty‑printed)

Nếu bạn muốn JSON có thụt lề để dễ đọc:

```csharp
string prettyJson = ocrResult.ToJson(true); // true = formatted
File.WriteAllText(jsonPath, prettyJson);
```

## Load Image File C# – Những lỗi thường gặp và mẹo

Khi bạn **load image file c#**, có thể gặp:

- **File not found** – Đảm bảo đường dẫn là tuyệt đối hoặc sử dụng `Path.Combine` với `Environment.CurrentDirectory`.  
- **Unsupported format** – Aspose hỗ trợ PNG, JPEG, BMP, TIFF và PDF. Đối với định dạng RAW, hãy chuyển đổi chúng trước.  
- **Large file memory pressure** – Sử dụng `ImageStream.FromFile(path, maxSizeInKB)` để giảm kích thước khi tải.

Giải quyết những vấn đề này từ sớm sẽ giúp bạn tránh các ngoại lệ khó hiểu trong pipeline OCR.

## Extract Text Image C# – Xác minh kết quả

Sau khi có JSON, bạn có thể muốn chỉ lấy văn bản thuần:

```csharp
var ocrResult = ocrEngine.Recognize(image);
string plainText = ocrResult.Text; // Simple string with line breaks
Console.WriteLine(plainText);
```

Đoạn mã này minh họa **extract text image c#** mà không có chi tiết bố cục — tiện lợi cho việc tìm kiếm nhanh hoặc ghi log.

---

![Diagram showing OCR workflow – how to perform OCR, convert image to JSON, and extract text image c#](/images/ocr-workflow.png "how to perform OCR workflow")

*Văn bản thay thế hình ảnh: "sơ đồ quy trình OCR minh họa chuyển đổi hình ảnh sang JSON và trích xuất văn bản hình ảnh c#"*  

*(Hình ảnh là placeholder; thay thế bằng sơ đồ thực tế khi xuất bản.)*

---

## Kết luận

Chúng tôi đã trình bày **cách thực hiện OCR** trong C# từ đầu đến cuối, chỉ cho bạn cách **chuyển đổi hình ảnh sang JSON**, và giải thích các chi tiết của **load image file c#** và **extract text image c#**. Ví dụ mã hoàn chỉnh đã sẵn sàng để đưa vào bất kỳ dự án .NET nào, và đầu ra JSON cung cấp cả văn bản thô và dữ liệu bố cục chính xác cho các phân tích downstream.

Tiếp theo bạn có thể: đưa JSON vào cơ sở dữ liệu, hiển thị các hộp giới hạn trên giao diện UI, hoặc xâu chuỗi nhiều lần OCR cho xử lý hàng loạt. Bạn cũng có thể thử nghiệm các tính năng khác của Aspose như nhận dạng chữ viết tay hoặc phát hiện mã vạch — cả hai đều tích hợp tự nhiên vào cùng một pipeline.

Nếu gặp khó khăn, hãy xem lại các mẹo khắc phục trong phần “Load Image File C#”, hoặc khám phá tài liệu chi tiết của Aspose để tùy chỉnh nâng cao. Chúc bạn lập trình vui vẻ và tận hưởng việc biến hình ảnh thành dữ liệu có cấu trúc!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}