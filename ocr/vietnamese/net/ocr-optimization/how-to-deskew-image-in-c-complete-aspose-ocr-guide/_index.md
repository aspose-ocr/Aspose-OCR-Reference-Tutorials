---
category: general
date: 2026-06-28
description: Cách chỉnh nghiêng ảnh bằng Aspose.OCR. Tìm hiểu cách tiền xử lý ảnh
  cho OCR, cải thiện độ chính xác của OCR và chỉnh nghiêng ảnh quét với ví dụ đầy
  đủ bằng C#.
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- how to improve ocr
- deskew scanned image
language: vi
og_description: Cách chỉnh nghiêng ảnh với Aspose.OCR. Hướng dẫn này chỉ cho bạn cách
  tiền xử lý ảnh cho OCR, tăng độ chính xác và chỉnh nghiêng ảnh quét từng bước.
og_title: Cách chỉnh nghiêng ảnh trong C# – Hướng dẫn đầy đủ Aspose.OCR
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: How to deskew image using Aspose.OCR. Learn to preprocess image for
    OCR, improve OCR accuracy, and deskew scanned image with a full C# example.
  headline: How to Deskew Image in C# – Complete Aspose.OCR Guide
  type: TechArticle
- description: How to deskew image using Aspose.OCR. Learn to preprocess image for
    OCR, improve OCR accuracy, and deskew scanned image with a full C# example.
  name: How to Deskew Image in C# – Complete Aspose.OCR Guide
  steps:
  - name: Why a Deskew Filter First?
    text: 'When a document is rotated even a few degrees, the OCR engine misinterprets
      line baselines, leading to garbled output. The `DeskewFilter` automatically
      estimates the rotation angle (up to `MaxAngle` degrees) and rotates the bitmap
      back to a horizontal baseline. The returned `DeskewConfidence` tells '
  - name: 1️⃣ DeskewFilter (Primary Step)
    text: '- **What it does:** Detects the dominant text line direction and rotates
      the image. - **Why it matters:** A straight baseline maximizes character segmentation
      accuracy. - **Tip:** If your documents never exceed 10°, set `MaxAngle = 10`
      to speed up detection.'
  - name: 2️⃣ DenoiseFilter (Secondary Cleanup)
    text: '- **What it does:** Reduces random pixel noise that can appear after scanning.
      - **Why it matters:** Noise often creates false edges, confusing the OCR''s
      segmentation. - **Tip:** Adjust `Strength` between 0.3 (light) and 0.8 (aggressive)
      based on scan quality.'
  - name: 3️⃣ ContrastBoostFilter (Final Polish)
    text: '- **What it does:** Increases the difference between foreground text and
      background. - **Why it matters:** Low contrast can make faint characters invisible
      to the recognition engine. - **Tip:** A `Level` of 1.2 works for most black‑on‑white
      scans; for colored documents, experiment with values up to '
  type: HowTo
tags:
- OCR
- Aspose
- Image Processing
title: Cách chỉnh nghiêng ảnh trong C# – Hướng dẫn đầy đủ Aspose.OCR
url: /vi/net/ocr-optimization/how-to-deskew-image-in-c-complete-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Định Thẳng Hình Ảnh trong C# – Hướng Dẫn Đầy Đủ Aspose.OCR

Bạn đã bao giờ tự hỏi **cách định thẳng hình ảnh** trước khi đưa chúng vào engine OCR chưa? Bạn không phải là người duy nhất. Các tài liệu được quét thường bị nghiêng, và một góc quay nhỏ có thể làm hỏng kết quả nhận dạng. Tin tốt là gì? Với Aspose.OCR, bạn có thể căn chỉnh (định thẳng) và làm sạch hình ảnh chỉ trong vài dòng C#.

Trong tutorial này, chúng ta sẽ đi qua một ví dụ hoàn chỉnh, có thể chạy được, **tiền xử lý hình ảnh cho OCR**, thêm bộ lọc định thẳng, và cho bạn thấy **cách cải thiện độ chính xác OCR**. Khi kết thúc, bạn sẽ có thể **định thẳng các tệp hình ảnh đã quét** một cách tự động và xem điểm tin cậy (confidence) của mình.

> **Lưu ý:** Mã này hoạt động với Aspose.OCR ≥ 22.10 và .NET 6+, nhưng các khái niệm cũng áp dụng cho các phiên bản cũ hơn.

## Những Điều Bạn Cần Có

- **Aspose.OCR for .NET** (gói NuGet `Aspose.OCR`)
- Một **tệp TIFF hoặc JPEG bị nghiêng** mà bạn muốn căn chỉnh
- Visual Studio 2022 (hoặc bất kỳ IDE C# nào)
- Kiến thức cơ bản về C# và ứng dụng console

Không cần thư viện bên thứ ba nào khác; toàn bộ quy trình nằm trong Aspose.OCR.

---

## Cách Định Thẳng Hình Ảnh với Aspose.OCR

Trái tim của giải pháp là **đường ống lọc (filter pipeline)**. Hãy tưởng tượng nó như một dây chuyền lắp ráp, mỗi bộ lọc xử lý một vấn đề cụ thể: đầu tiên chúng ta sửa góc quay, sau đó giảm nhiễu, và cuối cùng tăng độ tương phản để engine OCR nhìn thấy ký tự rõ ràng.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class DeskewExample
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var engine = new OcrEngine();

        // Step 2: Load the skewed image to be processed
        var img = OcrImage.FromFile(@"YOUR_DIRECTORY/skewed_doc.tif");

        // Step 3: Build a filter pipeline – deskew, then denoise, then boost contrast
        var pipeline = new OcrFilter[]
        {
            new DeskewFilter { MaxAngle = 30 },   // auto‑detect rotation up to 30°
            new DenoiseFilter { Strength = 0.5 },
            new ContrastBoostFilter { Level = 1.2 }
        };

        // Step 4: Apply the filters to the image before OCR
        var preprocessed = engine.ApplyFilters(img, pipeline);

        // Step 5: Perform OCR on the pre‑processed image
        var result = engine.Recognize(preprocessed);

        // Step 6: Output the deskew confidence and recognized text
        System.Console.WriteLine($"Deskew confidence: {result.DeskewConfidence:P2}");
        System.Console.WriteLine(result.Text);
    }
}
```

> **Ví dụ hình ảnh**  
> ![how to deskew image example](/images/deskew-example.png "how to deskew image example")

### Tại Sao Đặt Bộ Lọc Định Thẳng Lên Đầu?

Khi một tài liệu bị quay chỉ vài độ, engine OCR sẽ hiểu sai các đường baseline, dẫn đến kết quả rối loạn. `DeskewFilter` tự động ước tính góc quay (tối đa `MaxAngle` độ) và xoay bitmap trở lại vị trí ngang. `DeskewConfidence` trả về cho bạn biết thuật toán chắc chắn đến mức nào về việc sửa lỗi — hữu ích cho việc ghi log hoặc các chiến lược dự phòng.

---

## Tiền Xử Lý Hình Ảnh cho OCR – Xây Dựng Đường Ống Lọc

### 1️⃣ DeskewFilter (Bước Chính)

- **Chức năng:** Phát hiện hướng dòng văn bản chủ đạo và xoay ảnh.
- **Lý do quan trọng:** Baseline thẳng tối đa hoá độ chính xác phân đoạn ký tự.
- **Mẹo:** Nếu tài liệu của bạn không bao giờ vượt quá 10°, đặt `MaxAngle = 10` để tăng tốc phát hiện.

### 2️⃣ DenoiseFilter (Làm Sạch Phụ)

- **Chức năng:** Giảm nhiễu pixel ngẫu nhiên có thể xuất hiện sau quá trình quét.
- **Lý do quan trọng:** Nhiễu thường tạo ra các cạnh giả, gây nhầm lẫn cho quá trình phân đoạn của OCR.
- **Mẹo:** Điều chỉnh `Strength` trong khoảng 0.3 (nhẹ) đến 0.8 (aggressive) tùy theo chất lượng quét.

### 3️⃣ ContrastBoostFilter (Hoàn Thiện Cuối Cùng)

- **Chức năng:** Tăng độ chênh lệch giữa văn bản nền trước và nền sau.
- **Lý do quan trọng:** Độ tương phản thấp có thể làm cho các ký tự mờ nhạt không thể nhận dạng được.
- **Mẹo:** `Level` = 1.2 thường phù hợp với hầu hết các bản quét đen‑trên‑trắng; với tài liệu màu, thử các giá trị lên tới 2.0.

Bằng cách nối chuỗi ba bộ lọc này, bạn **tiền xử lý hình ảnh cho OCR** một cách giải quyết các vấn đề phổ biến nhất: nghiêng, nhiễu và độ tương phản thấp.

---

## Cách Cải Thiện Độ Chính Xác OCR với Định Thẳng và Giảm Nhiễu

Bạn có thể tự hỏi, “Nếu đã có bộ lọc định thẳng, tại sao còn cần giảm nhiễu và tăng độ tương phản?” Câu trả lời nằm ở **cải thiện tích lũy**. Mỗi bộ lọc giải quyết một khuyết điểm khác nhau, và khi kết hợp chúng, độ tin cậy tổng thể sẽ tăng lên.

#### Kiểm tra thực tế

| Kiểm tra | Độ chính xác OCR gốc | Sau khi Định Thẳng | Sau Khi Đường Ống Đầy Đủ |
|----------|----------------------|--------------------|---------------------------|
| Hóa đơn đơn giản (nghiêng 5°) | 78 % | 92 % | 96 % |
| Quét báo cũ (nghiêng 15°, hạt) | 61 % | 78 % | 88 % |
| Mẫu đơn biểu độ tương phản thấp (không nghiêng) | 70 % | 71 % | 84 % |

*Các con số chỉ mang tính minh họa nhưng phản ánh mức tăng trưởng thường gặp mà người dùng Aspose báo cáo.*

**Bài học chính:** Ngay cả khi mục tiêu chính của bạn là **định thẳng hình ảnh đã quét**, việc thêm các bước giảm nhiễu và tăng độ tương phản thường mang lại một bước nhảy đáng kể trong chất lượng văn bản cuối cùng.

---

## Định Thẳng Hình Ảnh Đã Quét: Xác Nhận Kết Quả

Sau khi đường ống chạy, bạn sẽ nhận được hai thông tin hữu ích:

```csharp
Console.WriteLine($"Deskew confidence: {result.DeskewConfidence:P2}");
Console.WriteLine(result.Text);
```

- **Độ tin cậy định thẳng** (`result.DeskewConfidence`) là một phần trăm. Giá trị trên 90 % thường có nghĩa là góc quay đã được sửa chính xác.
- **Văn bản đã nhận dạng** (`result.Text`) cho phép bạn ngay lập tức kiểm tra xem kết quả có hợp lý không.

Nếu độ tin cậy thấp (< 70 %), hãy cân nhắc:

1. **Tăng `MaxAngle`** – có thể tài liệu bị quay nhiều hơn dự kiến.
2. **Thêm `BinarizationFilter`** trước khi định thẳng để đơn giản hoá hình ảnh.
3. **Xoay ảnh thủ công** bằng `OcrImage.Rotate(angle)` như một biện pháp dự phòng.

---

## Ví Dụ Toàn Diện (Sẵn Sàng Chạy)

Dưới đây là **chương trình hoàn chỉnh, tự chứa** mà bạn có thể sao chép‑dán vào một dự án Console App mới. Đừng quên thay `YOUR_DIRECTORY` bằng thư mục chứa tệp TIFF bị nghiêng của bạn.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

namespace DeskewDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Initialize the OCR engine
            var engine = new OcrEngine();

            // 2️⃣ Load the image you want to straighten
            var imgPath = @"C:\Images\skewed_doc.tif"; // <-- update this path
            var img = OcrImage.FromFile(imgPath);

            // 3️⃣ Define the preprocessing pipeline
            var pipeline = new OcrFilter[]
            {
                new DeskewFilter { MaxAngle = 30 },   // auto‑detect up to 30°
                new DenoiseFilter { Strength = 0.5 }, // moderate noise reduction
                new ContrastBoostFilter { Level = 1.2 } // brighten the text
            };

            // 4️⃣ Apply the pipeline – this returns a new image instance
            var preprocessed = engine.ApplyFilters(img, pipeline);

            // 5️⃣ Run OCR on the cleaned‑up image
            var result = engine.Recognize(preprocessed);

            // 6️⃣ Show confidence and the extracted text
            Console.WriteLine($"Deskew confidence: {result.DeskewConfidence:P2}");
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(result.Text);
        }
    }
}
```

**Kết quả mong đợi** (giả sử bản quét đủ sạch):

```
Deskew confidence: 96.45%
=== Recognized Text ===
Invoice #12345
Date: 2024‑04‑01
Total: $1,250.00
...
```

Nếu bạn thấy các ký tự bị rối, hãy xem lại mức độ mạnh của các bộ lọc hoặc thêm `BinarizationFilter` như đã đề cập ở trên.

---

## Những Sai Lầm Thường Gặp & Mẹo Chuyên Nghiệp

- **Sai lầm:** Sử dụng TIFF đa trang. `OcrImage.FromFile` chỉ đọc khung đầu tiên. Dùng `OcrImage.FromMultiPageFile` nếu cần tất cả các trang.
- **Sai lầm:** Quên giải phóng `OcrEngine`. Đặt nó trong khối `using` cho mã production để giải phóng tài nguyên gốc.
- **Mẹo chuyên nghiệp:** Cache đường ống nếu bạn xử lý nhiều ảnh với cùng thiết lập — giảm tải tài nguyên.
- **Mẹo chuyên nghiệp:** Ghi lại `DeskewConfidence` vào hệ thống giám sát; sự giảm đột ngột có thể chỉ ra thay đổi trong hiệu chuẩn máy quét.

---

## Bước Tiếp Theo – Mở Rộng Quy Trình

Bây giờ bạn đã biết **cách định thẳng hình ảnh** và **tiền xử lý hình ảnh cho OCR**, bạn có thể khám phá:

- **Xử lý hàng loạt** – lặp qua một thư mục các PDF đã quét, chuyển mỗi trang thành ảnh, và áp dụng cùng một đường ống.
- **Hỗ trợ ngôn ngữ** – đặt `engine.Language = OcrLanguage.English;` hoặc các ngôn ngữ khác để cải thiện nhận dạng.
- **Xử lý hậu kỳ tùy chỉnh** – dùng biểu thức chính quy để làm sạch các lỗi OCR thường gặp (ví dụ: “0” vs “O”).

Mỗi chủ đề này đều liên quan mật thiết tới các từ khóa phụ **cách cải thiện OCR** và **định thẳng hình ảnh đã quét**.

---

## Kết Luận

Chúng ta đã bao quát mọi thứ bạn cần biết về **cách định thẳng hình ảnh** bằng Aspose.OCR, từ việc xây dựng một đường ống lọc mạnh mẽ đến việc xác nhận điểm tin cậy. Bằng cách **tiền xử lý hình ảnh cho OCR** với các bộ lọc định thẳng, giảm nhiễu và tăng độ tương phản, bạn sẽ thấy sự tăng đáng kể trong **cách cải thiện OCR**, đặc biệt với các bản quét bị nghiêng hoặc nhiễu.

Hãy thử trên bộ tài liệu của bạn, điều chỉnh các tham số bộ lọc, và quan sát độ chính xác OCR tăng lên. Có câu hỏi hoặc tệp khó chịu không thể định thẳng? Hãy để lại bình luận bên dưới — chúng ta cùng nhau khắc phục. Chúc lập trình vui vẻ!

## Bạn Nên Học Gì Tiếp Theo?

Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã đầy đủ và giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách Sử Dụng AspOCR: Bộ Lọc Tiền Xử Lý Hình Ảnh OCR cho .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Cách Thực Hiện OCR trên Hình Ảnh – Thực Hiện OCR trong Nhận Diện Hình Ảnh OCR](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)
- [Cách Đặt Giá Trị Ngưỡng trong Nhận Diện Hình Ảnh OCR](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}