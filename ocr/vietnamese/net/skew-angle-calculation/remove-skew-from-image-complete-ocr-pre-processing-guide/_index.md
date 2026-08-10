---
category: general
date: 2026-02-14
description: Tìm hiểu cách loại bỏ độ nghiêng của ảnh, tiền xử lý ảnh cho OCR, giảm
  nhiễu trong ảnh và trích xuất văn bản từ ảnh bằng Aspose OCR trong C#.
draft: false
keywords:
- remove skew from image
- preprocess image for ocr
- reduce noise in image
- extract text from image
- recognize text from document
language: vi
og_description: Loại bỏ độ nghiêng của ảnh, tiền xử lý ảnh cho OCR và trích xuất văn
  bản từ ảnh với hướng dẫn C# từng bước sử dụng Aspose OCR.
og_title: Xóa độ nghiêng khỏi hình ảnh – Hướng dẫn tiền xử lý OCR hoàn chỉnh
tags:
- OCR
- CSharp
- ImageProcessing
title: Xóa độ nghiêng khỏi hình ảnh – Hướng dẫn tiền xử lý OCR toàn diện
url: /vi/net/skew-angle-calculation/remove-skew-from-image-complete-ocr-pre-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Xóa Độ nghiêng của Hình ảnh – Hướng dẫn Tiền xử lý OCR đầy đủ

Bạn đã bao giờ cần **remove skew from image** trước khi đưa nó vào một engine OCR chưa? Bạn không phải là người duy nhất—các tài liệu được quét, ảnh biên lai, hoặc ảnh chụp màn hình thường bị nghiêng, và góc nhỏ đó có thể phá hỏng việc nhận dạng văn bản.  

Tin tốt? Với một vài bộ lọc Aspose OCR, bạn có thể làm thẳng, giảm nhiễu, tăng độ tương phản, và sau đó **extract text from image** trong một pipeline liền mạch. Trong hướng dẫn này, chúng tôi sẽ đi qua toàn bộ quá trình, từ việc tải một hình ảnh bị nghiêng đến **recognize text from document** và in kết quả.

---

## Những gì bạn sẽ xây dựng

By the end of this tutorial you’ll have a ready‑to‑run C# console app that:

1. **Removes skew from image** sử dụng `DeskewFilter`.
2. **Reduces noise in image** với `DenoiseFilter`.
3. **Preprocesses image for OCR** bằng cách tăng độ tương phản.
4. **Recognizes text from document** qua Aspose OCR’s `Engine`.
5. **Extracts text from image** và hiển thị nó trên console.

Không có dịch vụ bên ngoài, chỉ cần gói NuGet Aspose OCR và một vài dòng code.

---

## Yêu cầu trước

- .NET 6.0 SDK hoặc phiên bản mới hơn (code cũng hoạt động với .NET Core và .NET Framework).  
- Visual Studio 2022 hoặc bất kỳ trình soạn thảo nào bạn thích.  
- Aspose.OCR for .NET đã được cài đặt (`dotnet add package Aspose.OCR`).  
- Một hình ảnh mẫu (`skewed_noisy.jpg`) được đặt trong thư mục bạn có thể tham chiếu.

Nếu bạn đã có những thứ này, hãy bắt đầu.

---

## Bước 1: Tải hình ảnh nguồn

Điều đầu tiên chúng ta cần là một `ImageStream` trỏ tới tệp mà chúng ta muốn làm sạch.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Load the source image that needs cleaning
ImageStream sourceImage = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");
```

> **Tại sao điều này quan trọng:** `ImageStream` trừu tượng hoá bitmap nền, cho phép các bộ lọc Aspose hoạt động mà không cần bạn quản lý dữ liệu pixel thô.

---

## Bước 2: Xây dựng Pipeline Tiền xử lý (Remove Skew & Reduce Noise)

Thay vì gọi từng bộ lọc riêng lẻ, Aspose cho phép bạn nối chúng lại trong một `ImageProcessingPipeline`. Điều này giữ cho code gọn gàng và đảm bảo các thao tác diễn ra theo đúng thứ tự.

```csharp
// Create a pipeline and add desired filters
var processingPipeline = new ImageProcessingPipeline()
    .AddFilter(new DeskewFilter())                     // Remove skew
    .AddFilter(new DenoiseFilter())                    // Reduce noise
    .AddFilter(new ContrastBoostFilter { Level = 30 });// Boost contrast (0‑100)
```

### Tại sao thứ tự quan trọng

1. **Deskew first** – Làm thẳng hình ảnh trước khi giảm nhiễu ngăn bộ lọc nhiễu xử lý các cạnh nghiêng như là nhiễu.  
2. **Denoise second** – Khi hình ảnh đã được cân bằng, thuật toán có thể phân biệt tốt hơn giữa tín hiệu và hạt nhiễu.  
3. **Contrast boost last** – Tăng độ tương phản sau khi hình ảnh đã sạch tối đa hoá khả năng đọc OCR mà không làm tăng nhiễu.

---

## Bước 3: Áp dụng Pipeline và Nhận Hình ảnh Đã Làm sạch

Bây giờ chúng ta chạy pipeline trên luồng gốc.

```csharp
// Apply the pipeline to obtain a cleaned image
ImageStream cleanedImage = processingPipeline.Apply(sourceImage);
```

Tại thời điểm này, hình ảnh đã được làm thẳng, giảm nhiễu và tăng độ tương phản—hoàn hảo cho OCR.

---

## Bước 4: Khởi tạo Engine OCR và Nhận dạng Văn bản

Với một hình ảnh sạch sẽ trong tay, cuối cùng chúng ta có thể đưa nó vào Aspose OCR.

```csharp
// Initialise the OCR engine
Engine ocrEngine = new Engine();

// Recognise text from the cleaned image
OcrResult ocrResult = ocrEngine.Recognize(cleanedImage);
```

> **Mẹo:** Nếu bạn cần tinh chỉnh theo ngôn ngữ, `Engine` chấp nhận thuộc tính `Language` (ví dụ, `ocrEngine.Language = Language.English;`). Đối với hầu hết các tài liệu dựa trên Latin, mặc định hoạt động tốt.

---

## Bước 5: Hiển thị Văn bản Được Trích xuất

Một `Console.WriteLine` nhanh sẽ hiển thị kết quả.

```csharp
// Output the extracted text
Console.WriteLine(ocrResult.Text);
```

Khi bạn chạy chương trình, bạn sẽ thấy nội dung văn bản của `skewed_noisy.jpg` được in ra terminal—sạch, dễ đọc và sẵn sàng cho các bước xử lý tiếp theo.

---

## Ví dụ Hoạt động Đầy đủ

Dưới đây là chương trình hoàn chỉnh, sẵn sàng sao chép. Lưu lại dưới tên `Program.cs`, thay `YOUR_DIRECTORY` bằng đường dẫn thực tế, và chạy `dotnet run`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

namespace ImageOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Load the source image that needs cleaning
            ImageStream sourceImage = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");

            // Step 2: Create an image‑processing pipeline and add desired filters
            var processingPipeline = new ImageProcessingPipeline()
                .AddFilter(new DeskewFilter())                     // Remove skew
                .AddFilter(new DenoiseFilter())                    // Reduce noise
                .AddFilter(new ContrastBoostFilter { Level = 30 });// Boost contrast (0‑100)

            // Step 3: Apply the pipeline to obtain a cleaned image
            ImageStream cleanedImage = processingPipeline.Apply(sourceImage);

            // Step 4: Initialise the OCR engine and recognize text from the cleaned image
            Engine ocrEngine = new Engine();
            OcrResult ocrResult = ocrEngine.Recognize(cleanedImage);

            // Step 5: Display the extracted text
            Console.WriteLine("=== Extracted Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

**Kết quả mong đợi** (ví dụ cho một biên lai đơn giản):

```
=== Extracted Text ===
Store: Coffee Corner
Date: 02/12/2026
Item          Qty   Price
Latte          2    $5.80
Croissant      1    $2.50
Total                $8.30
```

Nếu kết quả trông rối mắt, hãy kiểm tra lại đường dẫn hình ảnh và chắc chắn tệp nguồn thực sự chứa văn bản có thể đọc được.

---

## Câu hỏi Thường gặp & Trường hợp Đặc biệt

### Nếu hình ảnh bị quay 90° thay vì chỉ nghiêng nhẹ thì sao?

`DeskewFilter` xử lý các góc nhỏ (±15°). Đối với quay toàn bộ, hãy gọi `new RotateFilter { Angle = 90 }` trước bước deskew.

### Hình ảnh của tôi ở định dạng PNG—có gì thay đổi không?

Không. `ImageStream.FromFile` tự động phát hiện định dạng, vì vậy PNG, JPEG, BMP, hoặc TIFF đều hoạt động giống nhau.

### Làm sao tôi có thể điều chỉnh độ mạnh của việc giảm nhiễu?

`DenoiseFilter` cung cấp thuộc tính `Strength` (0‑100). Giá trị cao hơn loại bỏ nhiều hạt nhiễu hơn nhưng có thể làm mờ chi tiết nhỏ. Thử nghiệm với giá trị khoảng 30‑50 cho các tài liệu chứa nhiều văn bản.

### Tôi cần xử lý một loạt tệp—có thể tái sử dụng pipeline không?

Chắc chắn. Tạo `processingPipeline` một lần, sau đó lặp qua từng tệp:

```csharp
foreach (var path in Directory.GetFiles("batch_folder", "*.jpg"))
{
    var src = ImageStream.FromFile(path);
    var cleaned = processingPipeline.Apply(src);
    var result = ocrEngine.Recognize(cleaned);
    // Save or log result.Text
}
```

Tái sử dụng cùng một instance `Engine` cũng cải thiện hiệu năng.

---

## Mẹo chuyên nghiệp cho OCR sẵn sàng sản xuất

- **Cache the pipeline**: Instantiating filters repeatedly can be costly in high‑throughput scenarios.  
- **Set OCR language**: `ocrEngine.Language = Language.Spanish;` for non‑English docs.  
- **Handle empty results**: Always check `ocrResult.Text?.Length > 0` before proceeding.  
- **Log intermediate images**: Saving `cleanedImage` to disk (`cleanedImage.Save("debug.png");`) helps you fine‑tune filter parameters.

---

## Kết luận

Chúng tôi đã trình bày cách **remove skew from image**, **reduce noise in image**, và **preprocess image for OCR** bằng pipeline bộ lọc mạnh mẽ của Aspose OCR, sau đó **recognize text from document** và cuối cùng **extract text from image**. Toàn bộ quy trình chỉ dưới 50 dòng C# và dễ mở rộng cho xử lý batch, mô hình ngôn ngữ tùy chỉnh, hoặc các bộ lọc bổ sung.

Sẵn sàng cho bước tiếp theo? Hãy thử thêm `BinarizeFilter` để ép đầu ra đen‑trắng, hoặc thử nghiệm các mức `ContrastBoostFilter` khác nhau để xem chúng ảnh hưởng như thế nào đến độ chính xác nhận dạng. Bạn càng thử nghiệm pipeline, bạn sẽ càng hiểu rõ mỗi bộ lọc đóng góp như thế nào cho kết quả OCR sạch sẽ.

Chúc lập trình vui vẻ, và hy vọng hình ảnh của bạn luôn thẳng!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}