---
category: general
date: 2026-02-28
description: Tạo PDF có thể tìm kiếm trong C# bằng cách kết hợp các hình ảnh theo
  chiều dọc. Tìm hiểu cách xếp chồng hình ảnh theo chiều dọc và chuyển đổi các trang
  PDF đã quét bằng Aspose OCR.
draft: false
keywords:
- create searchable pdf
- combine images vertically
- how to stack images vertically
- convert scanned pages pdf
language: vi
og_description: Tạo PDF có thể tìm kiếm trong C# bằng cách ghép các hình ảnh theo
  chiều dọc. Hướng dẫn này chỉ cách xếp chồng các hình ảnh theo chiều dọc và chuyển
  đổi các trang PDF đã quét sang dạng có thể tìm kiếm bằng Aspose OCR.
og_title: Tạo PDF có thể tìm kiếm trong C# – Kết hợp ảnh theo chiều dọc
tags:
- Aspose OCR
- C#
- PDF generation
title: Tạo PDF có thể tìm kiếm bằng C# – Kết hợp các hình ảnh theo chiều dọc
url: /vi/net/text-recognition/create-searchable-pdf-in-c-combine-images-vertically/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo PDF có thể tìm kiếm trong C# – Kết hợp hình ảnh theo chiều dọc

Bạn đã bao giờ cần **tạo PDF có thể tìm kiếm** từ một vài tệp PNG đã quét nhưng không biết bắt đầu từ đâu chưa? Bạn không phải là người duy nhất. Trong nhiều dự án tự động hoá tài liệu, vấn đề khó khăn nhất là chuyển một chồng các tệp hình ảnh thành một PDF gọn gàng, có thể tìm kiếm mà bạn có thể lập chỉ mục và chia sẻ.  

Trong hướng dẫn này, chúng ta sẽ đi qua một ví dụ hoàn chỉnh, sẵn sàng chạy, cho bạn thấy **cách xếp chồng hình ảnh theo chiều dọc**, **kết hợp hình ảnh theo chiều dọc**, và cuối cùng **chuyển đổi PDF các trang đã quét** thành một tài liệu có thể tìm kiếm duy nhất bằng cách sử dụng engine tăng tốc GPU của Aspose.OCR. Khi kết thúc, bạn sẽ có một chương trình tự chứa mà bạn có thể đưa vào bất kỳ giải pháp .NET nào.

> **Bạn sẽ học được**
> - Khởi tạo một engine OCR với hỗ trợ GPU.
> - Xử lý một lô hình ảnh song song.
> - **Kết hợp hình ảnh theo chiều dọc** để mô phỏng một bản quét đa trang.
> - Xuất PDF có thể tìm kiếm và báo cáo JSON chi tiết cho phân tích downstream.

## Yêu cầu trước

- .NET 6+ (mã biên dịch với .NET 6, .NET 7 hoặc .NET 8)
- Gói NuGet Aspose.OCR (`Install-Package Aspose.OCR`)
- Một máy có GPU nếu bạn muốn giữ cài đặt `ProcessingMode.Gpu` (cũng có thể dùng CPU)
- Một thư mục chứa một vài tệp PNG/JPEG đã quét (bản demo sử dụng `page1.png`, `page2.png`, `page3.png`)

Không có dịch vụ bên ngoài, không có tệp cấu hình ẩn—chỉ thuần C#.

## Bước 1 – Thiết lập Engine OCR để **tạo PDF có thể tìm kiếm**

Đầu tiên chúng ta tạo một `OcrEngine`, bật tăng tốc GPU, chọn tiếng Anh làm ngôn ngữ, và thêm một vài bộ lọc tiền xử lý. Các bộ lọc này cải thiện độ chính xác bằng cách làm thẳng các trang nghiêng (`DeskewFilter`) và loại bỏ nhiễu (`DenoiseFilter`).

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;
using System.Collections.Generic;
using System.Drawing;

class AllInOneDemo
{
    static void Main()
    {
        // Initialize OCR engine – this is the heart of creating a searchable PDF
        var ocrEngine = new OcrEngine
        {
            ProcessingMode = ProcessingMode.Gpu,   // Switch to CPU if no GPU
            Language = OcrLanguage.English
        };
        // Pre‑processing improves OCR quality
        ocrEngine.Filters.Add(new DeskewFilter());
        ocrEngine.Filters.Add(new DenoiseFilter());
```

**Tại sao điều này quan trọng:** Engine OCR thực hiện phần công việc nặng nhất là nhận dạng văn bản. Bật `ProcessingMode.Gpu` có thể giảm thời gian nhận dạng xuống một nửa trên card đồ họa hiện đại, trong khi các bộ lọc giảm các artefact quét phổ biến mà nếu không sẽ tạo ra đầu ra rối rắm.

## Bước 2 – Cấu hình Batch Processor để **chuyển đổi PDF các trang đã quét** một cách hiệu quả

Xử lý từng trang một cách tuần tự là ổn cho một vài hình ảnh, nhưng các dự án thực tế thường liên quan đến hàng chục hoặc hàng trăm trang. `OcrBatchProcessor` của Aspose.OCR cho phép chúng ta chạy nhận dạng song song, tăng tốc đáng kể bước **chuyển đổi PDF các trang đã quét**.

```csharp
        // Set up batch processor – ideal for converting many scanned pages to PDF
        var batchProcessor = new OcrBatchProcessor
        {
            MaxDegreeOfParallelism = 2,          // Adjust based on CPU/GPU cores
            Language = OcrLanguage.English,
            ProcessingMode = ProcessingMode.Gpu
        };

        // List the image files you want to turn into a searchable PDF
        List<string> imageFiles = new()
        {
            "YOUR_DIRECTORY/page1.png",
            "YOUR_DIRECTORY/page2.png",
            "YOUR_DIRECTORY/page3.png"
        };
```

**Mẹo chuyên nghiệp:** Nếu bạn chỉ có CPU, đặt `ProcessingMode = ProcessingMode.Cpu`. Batch processor vẫn sẽ tôn trọng `MaxDegreeOfParallelism`, vì vậy bạn có thể điều chỉnh để tránh quá tải máy.

## Bước 3 – Chạy OCR trên lô và thu thập kết quả

Bây giờ chúng ta thực sự nhận dạng văn bản. Phương thức `Recognize` trả về một danh sách các đối tượng `OcrResult`, mỗi đối tượng chứa cả hình ảnh gốc và văn bản đã trích xuất.

```csharp
        // Run OCR on all images at once
        List<OcrResult> ocrResults = batchProcessor.Recognize(imageFiles);
```

Tại thời điểm này, bạn đã có mọi thứ cần thiết để **tạo PDF có thể tìm kiếm**: các hình ảnh (vẫn trong bộ nhớ) và các lớp văn bản liên quan.

## Bước 4 – **Kết hợp hình ảnh theo chiều dọc** và tạo PDF có thể tìm kiếm

Hầu hết các tài liệu đã quét là PDF đa trang, vì vậy chúng ta cần ghép các hình ảnh trang riêng lẻ thành một hình ảnh dài cao phản ánh một chồng vật lý. Aspose.OCR cung cấp `Image.CombineVertical` cho mục đích này.

```csharp
        // Stitch the page images into one tall image – this is how we **combine images vertically**
        using var combinedImage = Image.CombineVertical(
            ocrResults.ConvertAll(r => r.Image));

        // Finally, create a searchable PDF from the combined image
        ocrEngine.RecognizeToPdf(combinedImage, "YOUR_DIRECTORY/combined_searchable.pdf");
```

Tệp kết quả (`combined_searchable.pdf`) chứa văn bản có thể chọn, có thể tìm kiếm dưới mỗi hình ảnh trang—đúng là những gì bạn cần để **tạo PDF có thể tìm kiếm** từ các nguồn đã quét.

![Create searchable PDF example](/images/create-searchable-pdf.png "create searchable pdf example")

*Văn bản thay thế hình ảnh: ví dụ tạo PDF có thể tìm kiếm hiển thị một PDF đã kết hợp với văn bản có thể tìm kiếm.*

**Tại sao xếp chồng theo chiều dọc?** Nhiều thư viện OCR coi mỗi hình ảnh là một trang riêng biệt. Bằng cách xếp chồng chúng, chúng ta giữ thứ tự trang của PDF nguyên vẹn đồng thời vẫn tận dụng một lần OCR duy nhất cho toàn bộ tài liệu.

## Bước 5 – Xuất JSON chi tiết cho Trang đầu tiên (Tuyệt vời cho các quy trình downstream)

Đôi khi bạn cần hơn một PDF; có thể bạn muốn đưa dữ liệu OCR vào cơ sở dữ liệu hoặc pipeline machine‑learning. Aspose.OCR cho phép bạn tuần tự hoá mỗi `OcrResult` thành JSON, bảo toàn các bounding box, điểm tin cậy và hơn thế nữa.

```csharp
        // Dump the first page’s OCR result to pretty‑printed JSON
        string jsonOutput = ocrResults[0].ToJson(prettyPrint: true);
        Console.WriteLine("--- JSON for first page ---");
        Console.WriteLine(jsonOutput);
    }
}
```

**Đoạn JSON dự kiến (được cắt ngắn):**

```json
{
  "Text": "Sample scanned text …",
  "Confidence": 0.97,
  "Blocks": [
    {
      "Text": "Header",
      "BoundingBox": { "X": 15, "Y": 10, "Width": 480, "Height": 30 }
    }
    // …
  ]
}
```

Bây giờ bạn có thể đưa JSON này vào bất kỳ hệ thống downstream nào—cho dù bạn đang lập chỉ mục văn bản trong Elasticsearch hoặc đưa nó vào bảng điều khiển phân tích tùy chỉnh.

---

## Cách **Xếp chồng hình ảnh theo chiều dọc** – Tóm tắt nhanh

Nếu bạn tự hỏi **cách xếp chồng hình ảnh theo chiều dọc** mà không dùng Aspose, bạn có thể sử dụng `System.Drawing` để tạo một bitmap mới và vẽ từng trang liên tiếp. Tuy nhiên, `Image.CombineVertical` tích hợp sẵn của Aspose xử lý DPI, định dạng pixel và quản lý bộ nhớ cho bạn, làm cho nó trở thành lựa chọn đáng tin cậy nhất cho mã sản xuất.

### Thay thế: Sử dụng `System.Drawing` (chỉ để khám phá)

```csharp
int totalHeight = 0;
int maxWidth = 0;
foreach (var img in ocrResults)
{
    totalHeight += img.Image.Height;
    maxWidth = Math.Max(maxWidth, img.Image.Width);
}
var canvas = new Bitmap(maxWidth, totalHeight);
using var g = Graphics.FromImage(canvas);
int offset = 0;
foreach (var img in ocrResults)
{
    g.DrawImage(img.Image, 0, offset);
    offset += img.Image.Height;
}
canvas.Save("combined_manual.png");
```

Cách tiếp cận thủ công hoạt động, nhưng bạn sẽ mất tiện lợi của việc tự động xử lý DPI và khả năng đưa kết quả trực tiếp trở lại `RecognizeToPdf`. Hãy dùng `CombineVertical` trừ khi bạn có yêu cầu rất đặc thù.

## Các lỗi thường gặp & Cách tránh

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Lỗi hết bộ nhớ** khi xử lý hàng chục bản quét độ phân giải cao | Mỗi hình ảnh vẫn ở trong bộ nhớ cho đến khi PDF được ghi | Giải phóng các đối tượng `Image` ngay khi hoàn thành (`using` blocks) hoặc giảm kích thước hình ảnh trước khi ghép |
| **Văn bản rác** sau OCR | Quét nghiêng hoặc độ tương phản thấp | Giữ `DeskewFilter` và `DenoiseFilter`; cân nhắc thêm `ContrastFilter` nếu cần |
| **Thiếu lớp có thể tìm kiếm** | Sử dụng `Recognize` thay vì `RecognizeToPdf` | Đảm bảo bạn gọi `ocrEngine.RecognizeToPdf` trên hình ảnh đã ghép |
| **GPU fallback thất bại** trên máy không có driver phù hợp | `ProcessingMode.Gpu` gây ra ngoại lệ | Bao quanh việc tạo engine trong try/catch và chuyển sang `ProcessingMode.Cpu` |

## Các bước tiếp theo – Mở rộng quy trình làm việc

Bây giờ bạn đã biết cách **tạo PDF có thể tìm kiếm**, bạn có thể muốn:

- **Xử lý hàng loạt toàn bộ thư mục** bằng `Directory.GetFiles` và vòng lặp `foreach`.
- **Thêm watermark** vào mỗi trang trước khi ghép (sử dụng `ImageProcessor` từ Aspose.Imaging).
- **Tách PDF có thể tìm kiếm thành các trang riêng lẻ** nếu bạn cần PDF từng trang sau này (`PdfDocument.Split` từ Aspose.PDF).
- **Tích hợp với Azure Blob Storage** để lấy hình ảnh từ đám mây và đẩy PDF cuối cùng lên lại.

Tất cả các mở rộng này đều liên quan đến các khái niệm cốt lõi giống nhau: thiết lập OCR, xử lý hình ảnh và xuất PDF.

---

## Kết luận

Chúng tôi đã bao phủ mọi thứ bạn cần để **tạo PDF có thể tìm kiếm** từ một bộ sưu tập hình ảnh đã quét trong C#. Bằng cách khởi tạo một `OcrEngine` hỗ trợ GPU, chạy batch song song với `OcrBatchProcessor`, **kết hợp hình ảnh theo chiều dọc**, và cuối cùng gọi `RecognizeToPdf`, bạn sẽ có một tài liệu gọn gàng, có thể tìm kiếm, sẵn sàng để lưu trữ hoặc lập chỉ mục. Việc xuất JSON bổ sung cung cấp cho bạn khả năng quan sát đầy đủ kết quả OCR, mở ra các cơ hội cho phân tích hoặc quy trình tùy chỉnh.

Hãy thử nghiệm, khám phá các bộ lọc khác nhau, và xem quy trình tự động hoá tài liệu của bạn trở nên mượt mà hơn. Nếu gặp bất kỳ vấn đề nào, hãy để lại bình luận—chúc lập trình vui vẻ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}