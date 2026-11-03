---
category: general
date: 2026-01-10
description: Học cách nhận dạng văn bản từ hình ảnh, trích xuất tọa độ văn bản và
  chuyển đổi biên lai sang JSON bằng Aspose OCR trong C#. Hướng dẫn từng bước.
draft: false
keywords:
- recognize text from image
- how to extract text
- extract text coordinates
- convert receipt to json
language: vi
og_description: Nhận dạng văn bản từ hình ảnh trong C# bằng Aspose OCR. Hướng dẫn
  này cho thấy cách trích xuất văn bản, lấy tọa độ và chuyển biên lai sang JSON.
og_title: Nhận dạng văn bản từ hình ảnh – Hướng dẫn OCR đầy đủ bằng C#
tags:
- OCR
- C#
- Aspose
title: Nhận dạng văn bản từ hình ảnh trong C# – Hướng dẫn toàn diện về OCR và JSON
url: /vi/net/text-recognition/recognize-text-from-image-in-c-complete-guide-to-ocr-and-jso/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Nhận dạng văn bản từ hình ảnh – Hướng dẫn OCR C# đầy đủ

Bạn đã bao giờ cần nhận dạng văn bản từ hình ảnh nhưng không chắc thư viện nào nên chọn? Bạn không phải là người duy nhất. Trong nhiều ứng dụng thực tế—trình theo dõi chi phí, máy quét biên lai, hoặc lưu trữ tài liệu—việc trích xuất văn bản một cách đáng tin cậy là rào cản đầu tiên.  

Trong hướng dẫn này, chúng ta sẽ đi qua **cách trích xuất văn bản**, lấy các hộp bao quanh, và cuối cùng **chuyển đổi biên lai sang JSON** bằng Aspose.OCR cho .NET. Khi kết thúc, bạn sẽ có một dự án C# độc lập, cho phép chụp ảnh biên lai và xuất ra một tệp JSON gọn gàng với các điểm tin cậy và tọa độ.

## Những gì bạn cần

- **.NET 6.0 SDK** (hoặc bất kỳ phiên bản nào mới hơn). Các framework cũ cũng hoạt động, nhưng .NET 6 là lựa chọn tối ưu cho các thư viện hiện đại.
- **Visual Studio 2022** hoặc VS Code với phần mở rộng C#.
- **Aspose.OCR for .NET** gói NuGet (`Aspose.OCR` và `Aspose.OCR.Output`). Bạn có thể cài đặt nó qua Package Manager Console:

```powershell
Install-Package Aspose.OCR
Install-Package Aspose.OCR.Output
```

- Một hình ảnh biên lai mẫu (ví dụ, `receipt.jpg`) được đặt trong thư mục mà bạn sẽ tham chiếu sau.
- Đó là tất cả—không cần SDK bổ sung, không có binary gốc, chỉ mã quản lý thuần túy.

## Bước 1: Tạo dự án Console mới

Đầu tiên, tạo một ứng dụng console. Đây là cách nhanh nhất để thử OCR mà không cần giao diện người dùng.

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll fill this in later.
        }
    }
}
```

> **Mẹo:** Giữ thư mục dự án gọn gàng; tạo một thư mục con tên `Resources` và đặt `receipt.jpg` vào đó. Điều này giúp việc xử lý đường dẫn trở nên dễ dàng.

## Bước 2: Tải hình ảnh biên lai

Bây giờ chúng ta thực sự **nhận dạng văn bản từ hình ảnh**. Bước đầu tiên là chỉ định engine OCR tới tệp.

```csharp
// Inside Main()
string imagePath = @"Resources/receipt.jpg";
if (!System.IO.File.Exists(imagePath))
{
    Console.WriteLine($"❌ Image not found at {imagePath}");
    return;
}

// Initialise the OCR engine
OcrEngine ocrEngine = new OcrEngine
{
    Image = ImageStream.FromFile(imagePath)
};

Console.WriteLine("✅ Image loaded successfully.");
```

Tại sao chúng ta bao bọc việc tải trong một kiểm tra tồn tại đơn giản? Bởi vì trong môi trường thực tế, bạn thường xử lý các tệp tải lên của người dùng có thể bị thiếu hoặc hỏng. Phát hiện sớm vấn đề sẽ giúp tránh các ngoại lệ khó hiểu sau này.

## Bước 3: Thực hiện OCR – **nhận dạng văn bản từ hình ảnh**

Khi hình ảnh đã có trong bộ nhớ, chúng ta yêu cầu Aspose **nhận dạng văn bản từ hình ảnh**. Thao tác này đồng bộ và trả về một tập kết quả phong phú.

```csharp
// Still inside Main()
try
{
    ocrEngine.Recognize();
    Console.WriteLine("🧠 OCR completed.");
}
catch (Exception ex)
{
    Console.WriteLine($"❗ OCR failed: {ex.Message}");
    return;
}
```

Trong hậu trường, Aspose chạy một mạng nơ-ron được huấn luyện trên hàng triệu ký tự. Engine sẽ điền vào `ocrEngine.Text`, `ocrEngine.RecognitionResult`, và một tập hợp các đối tượng `OcrRegion` chứa tọa độ. Đó chính là những gì chúng ta cần cho bước tiếp theo.

## Bước 4: **Cách trích xuất văn bản** – Lấy chuỗi thô

Nếu bạn chỉ quan tâm đến văn bản thuần (có thể cho việc tìm kiếm nhanh), bạn có thể lấy trực tiếp từ engine:

```csharp
string plainText = ocrEngine.Text;
Console.WriteLine("\n--- Extracted Text ---");
Console.WriteLine(plainText);
```

Bạn sẽ thấy các ngắt dòng ở nơi OCR phát hiện ranh giới đoạn văn. Trong nhiều trường hợp quét biên lai, chuỗi thô đủ để trích xuất tổng tiền, ngày tháng, hoặc tên nhà cung cấp bằng các biểu thức chính quy đơn giản.

## Bước 5: **trích xuất tọa độ văn bản** – Hộp bao quanh cho mỗi từ

Thường bạn cần biết *ở đâu* trên hình ảnh một đoạn văn bản cụ thể nằm—ví dụ, để làm nổi bật tổng tiền trong giao diện người dùng. Aspose cung cấp thông tin này qua các đối tượng `OcrRegion`.

```csharp
Console.WriteLine("\n--- Text Coordinates (extract text coordinates) ---");
foreach (var region in ocrEngine.RecognitionResult.Regions)
{
    // Each region represents a word or a line depending on the engine settings.
    string word = region.Text;
    var bounds = region.BoundingBox; // X, Y, Width, Height
    Console.WriteLine($"Word: \"{word}\" | Box: X={bounds.X}, Y={bounds.Y}, W={bounds.Width}, H={bounds.Height}");
}
```

Lưu ý chúng ta đang lặp qua **trích xuất tọa độ văn bản** cho mỗi đoạn được nhận dạng. Các tọa độ là tương đối so với hình ảnh gốc, vì vậy bạn có thể phủ lên chúng trong một canvas đồ họa hoặc phần tử HTML `<canvas>`.

## Bước 6: **chuyển đổi biên lai sang JSON** – Lưu kết quả chi tiết

Bây giờ là phần kết nối mọi thứ lại với nhau: chúng ta muốn một cấu trúc máy đọc được, bao gồm văn bản, điểm tin cậy và các hộp bao quanh. Aspose cung cấp `JsonSaveOptions` giúp việc này trở nên dễ dàng.

```csharp
// Define where the JSON will be saved
string jsonPath = @"Resources/receipt.json";

// Configure JSON options to keep confidence and bounding boxes
JsonSaveOptions jsonOptions = new JsonSaveOptions
{
    IncludeConfidence = true,
    IncludeBoundingBoxes = true
};

// Save the OCR result
ocrEngine.Save(jsonPath, jsonOptions);
Console.WriteLine($"\n💾 Detailed OCR results saved to {jsonPath}");
```

Tệp kết quả trông giống như sau (được rút gọn để ngắn gọn):

```json
{
  "Regions": [
    {
      "Text": "Store",
      "Confidence": 0.99,
      "BoundingBox": { "X": 45, "Y": 120, "Width": 80, "Height": 20 }
    },
    {
      "Text": "Total",
      "Confidence": 0.97,
      "BoundingBox": { "X": 300, "Y": 560, "Width": 70, "Height": 22 }
    }
    // ... more regions ...
  ]
}
```

Bây giờ bạn có một artefact **chuyển đổi biên lai sang JSON** có thể đưa vào các dịch vụ hạ nguồn—ví dụ API báo cáo chi phí, pipeline phân tích, hoặc thậm chí một giao diện đơn giản vẽ hình chữ nhật quanh mỗi từ.

## Ví dụ Hoạt động đầy đủ

Kết hợp tất cả các phần lại, đây là file `Program.cs` hoàn chỉnh mà bạn có thể sao chép và dán vào dự án của mình:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Load the image
            // -------------------------------------------------
            string imagePath = @"Resources/receipt.jpg";
            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"❌ Image not found at {imagePath}");
                return;
            }

            OcrEngine ocrEngine = new OcrEngine
            {
                Image = ImageStream.FromFile(imagePath)
            };
            Console.WriteLine("✅ Image loaded.");

            // -------------------------------------------------
            // 2️⃣ Run OCR – recognize text from image
            // -------------------------------------------------
            try
            {
                ocrEngine.Recognize();
                Console.WriteLine("🧠 OCR completed.");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"❗ OCR failed: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 3️⃣ Extract plain text (how to extract text)
            // -------------------------------------------------
            Console.WriteLine("\n--- Extracted Text ---");
            Console.WriteLine(ocrEngine.Text);

            // -------------------------------------------------
            // 4️⃣ Get coordinates (extract text coordinates)
            // -------------------------------------------------
            Console.WriteLine("\n--- Text Coordinates ---");
            foreach (var region in ocrEngine.RecognitionResult.Regions)
            {
                var box = region.BoundingBox;
                Console.WriteLine($"Word: \"{region.Text}\" | Box: X={box.X}, Y={box.Y}, W={box.Width}, H={box.Height}");
            }

            // -------------------------------------------------
            // 5️⃣ Save detailed JSON (convert receipt to json)
            // -------------------------------------------------
            string jsonPath = @"Resources/receipt.json";
            JsonSaveOptions jsonOptions = new JsonSaveOptions
            {
                IncludeConfidence = true,
                IncludeBoundingBoxes = true
            };
            ocrEngine.Save(jsonPath, jsonOptions);
            Console.WriteLine($"\n💾 JSON saved at {jsonPath}");
        }
    }
}
```

Chạy chương trình (`dotnet run`) và quan sát đầu ra console. Mở `Resources/receipt.json` để kiểm tra cấu trúc.

## Câu hỏi Thường gặp & Trường hợp Đặc biệt

- **Nếu hình ảnh mờ?**  
  Aspose OCR hoạt động tốt nhất với độ phân giải 300 dpi hoặc cao hơn. Nếu bạn nhận được điểm tin cậy thấp, hãy cân nhắc áp dụng bộ lọc làm nét trước khi đưa hình ảnh vào engine.

- **Tôi có thể nhận dạng nhiều ngôn ngữ không?**  
  Có. Đặt `ocrEngine.Language = Language.English | Language.Spanish;` trước khi gọi `Recognize()`.

- **Làm sao để giới hạn đầu ra chỉ là số (ví dụ, tổng tiền)?**  
  Sau khi có văn bản thuần, chạy một regex như `\d+\.\d{2}` trên `ocrEngine.Text`. Vì chúng ta đã có tọa độ, bạn có thể ánh xạ chuỗi khớp lại với vùng của nó để làm nổi bật trực quan.

- **Định dạng JSON có thể tùy chỉnh không?**  
  Lớp `JsonSaveOptions` cung cấp một vài cờ. Nếu bạn cần một schema hoàn toàn tùy chỉnh, bạn có thể lặp qua `ocrEngine.RecognitionResult.Regions` và tự serialize các đối tượng bằng `System.Text.Json`.

## Kết luận

Chúng tôi vừa trình diễn cách **nhận dạng văn bản từ hình ảnh** trong C# bằng Aspose.OCR, **cách trích xuất văn bản**, lấy **trích xuất tọa độ văn bản**, và cuối cùng **chuyển đổi biên lai sang JSON**. Toàn bộ quy trình nằm trong một ứng dụng console đơn giản, dễ chạy, phù hợp cho các nguyên mẫu hoặc làm khối xây dựng trong các hệ thống lớn hơn.

Bước tiếp theo? Hãy thử đưa JSON vào giao diện front‑end để vẽ các hộp bao quanh, hoặc kết nối đầu ra với dịch vụ báo cáo chi phí. Bạn cũng có thể thử nghiệm với các định dạng hình ảnh khác (PNG, TIFF) hoặc xử lý hàng loạt một thư mục các biên lai.

Có thêm câu hỏi về OCR, Aspose, hoặc xử lý JSON? Hãy để lại bình luận bên dưới, và chúc bạn lập trình vui vẻ! 

![Ví dụ hình ảnh biên lai cho nhận dạng văn bản từ hình ảnh](receipt.jpg "Ví dụ hình ảnh biên lai")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}