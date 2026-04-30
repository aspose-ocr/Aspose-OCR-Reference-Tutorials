---
category: general
date: 2026-04-29
description: Cách chỉnh nghiêng ảnh và tăng độ chính xác OCR với Aspose OCR – học
  cách loại bỏ nhiễu, tăng độ tương phản ảnh và trích xuất văn bản từ hình ảnh.
draft: false
keywords:
- how to deskew image
- remove noise from image
- boost image contrast
- extract text from image
- improve ocr accuracy
language: vi
og_description: Cách chỉnh nghiêng ảnh và cải thiện độ chính xác OCR. Hướng dẫn này
  cho thấy cách loại bỏ nhiễu khỏi ảnh, tăng độ tương phản ảnh và trích xuất văn bản
  từ ảnh bằng Aspose OCR.
og_title: Cách chỉnh nghiêng ảnh – Hướng dẫn đầy đủ Aspose OCR
tags:
- Aspose OCR
- C#
- Image preprocessing
title: cách chỉnh nghiêng ảnh – Hướng dẫn tiền xử lý OCR của Aspose
url: /vi/net/ocr-optimization/how-to-deskew-image-aspose-ocr-preprocessing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# cách chỉnh nghiêng ảnh – Hướng dẫn đầy đủ Aspose OCR

Bạn đã bao giờ tự hỏi **cách chỉnh nghiêng ảnh** trước khi đưa chúng vào công cụ OCR chưa? Bạn không phải là người duy nhất. Một bản quét lệch hoặc một bức ảnh chụp góc có thể làm sai lệch việc nhận dạng văn bản, để lại kết quả rối rắm.  

Trong hướng dẫn này, chúng ta sẽ đi qua một giải pháp hoàn chỉnh, từ đầu đến cuối, không chỉ **cách chỉnh nghiêng ảnh** mà còn **loại bỏ nhiễu khỏi ảnh**, **tăng độ tương phản ảnh**, và cuối cùng **trích xuất văn bản từ ảnh** bằng Aspose OCR. Khi kết thúc, bạn sẽ thấy cách **cải thiện độ chính xác OCR** mà không cần lục lọi tài liệu.

> **Bạn sẽ nhận được:** một ứng dụng console C# sẵn sàng chạy, giải thích rõ ràng từng bước tiền xử lý, và một vài mẹo thực tế bạn có thể sao chép‑dán vào dự án của mình.

## Yêu cầu trước

- .NET 6.0 hoặc mới hơn (mã hoạt động với .NET Core và .NET Framework cũng được)  
- Gói NuGet Aspose.OCR (`Install-Package Aspose.OCR`)  
- Một ảnh mẫu bị lệch, nhiễu, hoặc độ tương phản thấp (ví dụ, `skewed_noisy.jpg`)  
- Visual Studio, VS Code, hoặc bất kỳ trình chỉnh sửa C# nào bạn thích  

Không cần thư viện gốc bổ sung – Aspose xử lý mọi thứ trong cùng tiến trình.

---

## Cách chỉnh nghiêng ảnh với Aspose OCR

Điều đầu tiên chúng ta cần là bộ lọc chỉnh nghiêng để sửa góc quay. Aspose OCR cung cấp `FilterDeskew`, bộ lọc này phân tích các đường cơ sở của văn bản và xoay bitmap tương ứng.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

class PreprocessDemo
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine – this is the core object that will later recognize text.
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Build an image‑processing pipeline.
        //    The order matters: deskew → denoise → contrast boost.
        ImageProcessingPipeline processingPipeline = new ImageProcessingPipeline();
        processingPipeline.Add(new FilterDeskew());          // ✅ how to deskew image
        processingPipeline.Add(new FilterDenoise());         // ✅ remove noise from image
        processingPipeline.Add(new FilterContrastBoost());   // ✅ boost image contrast

        // 3️⃣ Load your source picture.
        var sourceImage = OcrEngine.LoadImage(@"YOUR_DIRECTORY/skewed_noisy.jpg");

        // 4️⃣ Apply the pipeline – the image is now straight, cleaner, and sharper.
        var processedImage = processingPipeline.Apply(sourceImage);

        // 5️⃣ Run OCR on the cleaned‑up bitmap.
        var ocrResult = ocrEngine.Recognize(processedImage);

        // 6️⃣ Print the extracted text.
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Tại sao chúng ta bắt đầu với việc chỉnh nghiêng:** Nếu các dòng văn bản không nằm ngang, công cụ OCR sẽ cố gắng diễn giải các ký tự nghiêng như các glyph khác nhau, làm giảm đáng kể **cải thiện độ chính xác OCR**. Việc chỉnh nghiêng căn chỉnh các đường cơ sở, cung cấp cho bộ nhận dạng một nền sạch.

> *Mẹo chuyên nghiệp:* Nếu bạn biết trước góc quay (ví dụ, tất cả các bản quét lệch 90°), bạn có thể bỏ qua bộ lọc và xoay thủ công – đây là một cải thiện hiệu năng nhỏ.

---

## Loại bỏ nhiễu khỏi ảnh – Làm sạch bản quét

Nhiễu xuất hiện dưới dạng các đốm đen hoặc trắng ngẫu nhiên (mẫu “muối‑và‑tiêu” cổ điển) và có thể gây rối cho việc phân đoạn ký tự. `FilterDenoise` áp dụng bộ lọc trung vị để làm mịn chúng trong khi vẫn giữ các cạnh.

```csharp
// Inside the pipeline we already added FilterDenoise.
// If you need a custom strength, you can instantiate it like:
var denoise = new FilterDenoise { Strength = 2 }; // 1‑3 are typical values
processingPipeline.Add(denoise);
```

**Khi nào nên điều chỉnh độ mạnh:**  
- **Strength = 1** – Hạt nhẹ, xử lý nhanh.  
- **Strength = 3** – Các bản quét rất nhiễu (ví dụ, tài liệu fax).  

Tăng độ mạnh quá mức có thể làm mờ các nét mỏng, điều này có thể *gây hại* **cải thiện độ chính xác OCR**. Hãy thử một vài giá trị trên mẫu đại diện.

---

## Tăng độ tương phản ảnh – Làm nổi bật ký tự mờ

Các ảnh có độ tương phản thấp (như biên lai đã phai) thường khiến công cụ OCR bỏ lỡ các glyph nhẹ. `FilterContrastBoost` kéo dài histogram sao cho các pixel tối trở nên tối hơn và các pixel sáng trở nên sáng hơn.

```csharp
var contrast = new FilterContrastBoost { ContrastLevel = 1.5f }; // 1.0 = no change
processingPipeline.Add(contrast);
```

**Tại sao độ tương phản quan trọng:** Độ tương phản cao hơn cải thiện tỉ lệ tín hiệu‑nào, giúp bộ nhận dạng neural của Aspose dễ dàng phân biệt “I” với “l”. Tuy nhiên, tăng quá mức có thể làm bão hòa ảnh, biến các gradient mượt thành các cạnh cứng trông như nhiễu. Hãy hướng tới sự cân bằng; 1.5‑2.0 là mức khởi đầu tốt.

---

## Trích xuất văn bản từ ảnh – Bước OCR cuối cùng

Bây giờ ảnh đã thẳng, sạch và sống động, công cụ OCR có thể thực hiện công việc của mình. Phương thức `Recognize` trả về một đối tượng `OcrResult` chứa văn bản thô, điểm tin cậy, và thậm chí các hộp bao quanh nếu bạn cần.

```csharp
var ocrResult = ocrEngine.Recognize(processedImage);
Console.WriteLine(ocrResult.Text);
```

**Kết quả mẫu** (giả sử ảnh nguồn chứa “Invoice #12345”):

```
=== OCR Output ===
Invoice #12345
Date: 04/28/2026
Total: $1,234.56
```

Nếu bạn thấy thiếu ký tự, hãy kiểm tra lại pipeline tiền xử lý – có thể ảnh vẫn cần một mức lọc nhiễu mạnh hơn hoặc mức độ tương phản khác.

> *Câu hỏi thường gặp:* “Nếu tôi cần nhận dạng ngôn ngữ khác ngoài tiếng Anh thì sao?”  
> Chỉ cần đặt `ocrEngine.Language = Language.English;` sang một ngôn ngữ được hỗ trợ khác (ví dụ, `Language.French`). Các bước tiền xử lý vẫn giữ nguyên.

---

## Cải thiện độ chính xác OCR – Điều chỉnh bổ sung

Ngay cả với một pipeline hoàn hảo, một vài công tắc bổ sung có thể đẩy **cải thiện độ chính xác OCR** lên nữa:

| Mẹo | Khi nào dùng | Cách |
|-----|--------------|-----|
| **Binary Thresholding** | Rất tối hoặc rất sáng | `processingPipeline.Add(new FilterBinarize());` |
| **Resize Image** | Phông chữ nhỏ (<10 pt) | `processedImage = OcrEngine.Resize(processedImage, 2.0);` |
| **Specify Character Set** | Bảng chữ cái đã biết (chỉ số, v.v.) | `ocrEngine.Characters = "0123456789";` |
| **Multi‑page PDFs** | Xử lý hàng loạt | Loop over each page and reuse the same pipeline. |

Nhớ rằng: mỗi bộ lọc bổ sung sẽ tăng thời gian xử lý, vì vậy chỉ bật những gì bạn thực sự cần.

---

## Ví dụ hoạt động đầy đủ (Sẵn sàng sao chép‑dán)

Dưới đây là toàn bộ chương trình, sẵn sàng biên dịch. Thay thế `YOUR_DIRECTORY` bằng thư mục chứa `skewed_noisy.jpg`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

class PreprocessDemo
{
    static void Main()
    {
        // Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Build preprocessing pipeline
        ImageProcessingPipeline pipeline = new ImageProcessingPipeline();
        pipeline.Add(new FilterDeskew());                     // how to deskew image
        pipeline.Add(new FilterDenoise { Strength = 2 });    // remove noise from image
        pipeline.Add(new FilterContrastBoost { ContrastLevel = 1.8f }); // boost image contrast

        // Load source image
        var sourcePath = @"YOUR_DIRECTORY/skewed_noisy.jpg";
        var sourceImage = OcrEngine.LoadImage(sourcePath);

        // Apply pipeline
        var cleanImage = pipeline.Apply(sourceImage);

        // Perform OCR
        var result = ocrEngine.Recognize(cleanImage);

        // Output
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(result.Text);
    }
}
```

**Kết quả mong đợi:** Văn bản sạch, đã được chỉnh thẳng được in ra console, với ít lỗi nhận dạng hơn nhiều so với việc đưa file thô trực tiếp vào `ocrEngine.Recognize`.

---

## Kết luận

Chúng ta đã đề cập đến **cách chỉnh nghiêng ảnh**, cách **loại bỏ nhiễu khỏi ảnh**, cách **tăng độ tương phản ảnh**, và cuối cùng cách **trích xuất văn bản từ ảnh** bằng Aspose OCR. Khi kết hợp các bộ lọc này, bạn sẽ thấy sự cải thiện đáng kể trong **cải thiện độ chính xác OCR**, đặc biệt trên các bản quét chất lượng thấp.

Sẵn sàng cho thử thách tiếp theo? Hãy thử đưa một PDF đa trang vào cùng pipeline, hoặc thử nghiệm các ngưỡng tùy chỉnh cho việc nhị phân hoá. Các nguyên tắc vẫn giống nhau – chỉnh thẳng, làm sạch, làm sáng, rồi nhận dạng.

Có câu hỏi hoặc trường hợp đặc biệt? Để lại bình luận, và chúng ta sẽ cùng giải quyết. Chúc lập trình vui vẻ!  

![ví dụ cách chỉnh nghiêng ảnh](deskew-example.png "ví dụ cách chỉnh nghiêng ảnh")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}