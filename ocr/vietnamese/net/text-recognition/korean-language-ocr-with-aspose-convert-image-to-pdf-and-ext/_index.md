---
category: general
date: 2026-05-28
description: Hướng dẫn OCR ngôn ngữ Hàn Quốc sử dụng Aspose trong C#. Tìm hiểu cách
  tải hình ảnh từ luồng, trích xuất văn bản thuần, chuyển đổi hình ảnh sang PDF và
  xuất PDF có thể tìm kiếm.
draft: false
keywords:
- korean language ocr
- convert image to pdf
- load image from stream
- extract plain text
- export searchable pdf
language: vi
og_description: OCR tiếng Hàn trong C# sử dụng Aspose. Hướng dẫn từng bước để tải
  hình ảnh từ luồng, trích xuất văn bản thuần, chuyển đổi hình ảnh sang PDF và xuất
  PDF có thể tìm kiếm.
og_title: OCR Tiếng Hàn – Chuyển Hình Ảnh sang PDF & Trích Xuất Văn Bản (Hướng Dẫn
  C#)
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Korean Language OCR tutorial using Aspose in C#. Learn how to load
    image from stream, extract plain text, convert image to PDF and export searchable
    PDF.
  headline: 'Korean Language OCR with Aspose: Convert Image to PDF and Extract Text
    in C#'
  type: TechArticle
tags:
- Aspose OCR
- C#
- Image Processing
title: 'OCR tiếng Hàn với Aspose: Chuyển hình ảnh sang PDF và Trích xuất văn bản trong
  C#'
url: /vi/net/text-recognition/korean-language-ocr-with-aspose-convert-image-to-pdf-and-ext/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR tiếng Hàn với Aspose: Chuyển ảnh sang PDF và Trích xuất Văn bản trong C#

Bạn có bao giờ tự hỏi làm thế nào để chạy **Korean Language OCR** trên một bức ảnh mà không cần gửi bất kỳ dữ liệu nào lên đám mây không? Bạn không phải là người duy nhất. Dù bạn đang số hoá biển hiệu đường phố, xử lý biên lai, hay xây dựng một chỉ mục tìm kiếm đa ngôn ngữ, khả năng nhận dạng ký tự Hàn Quốc cục bộ có thể giúp bạn tiết kiệm thời gian, chi phí và tránh các rắc rối về quyền riêng tư.

Trong hướng dẫn này, chúng ta sẽ đi qua một ví dụ hoàn chỉnh, có thể chạy được, cho thấy cách **load image from stream**, **extract plain text**, **convert image to PDF**, và cuối cùng **export searchable PDF**—tất cả đều sử dụng Aspose.OCR và vài dòng C#. Không có dịch vụ bên ngoài, không có phép màu ẩn—chỉ là mã .NET thuần túy mà bạn có thể đưa vào bất kỳ ứng dụng console nào.

## Những gì bạn sẽ nhận được

- Một chương trình console hoạt động, đọc tệp JPEG thông qua một file stream.  
- Văn bản tiếng Hàn được trích xuất dưới dạng chuỗi Unicode thuần.  
- Báo cáo JSON chi tiết về quá trình OCR để gỡ lỗi hoặc phân tích.  
- Một PDF có thể tìm kiếm được, bạn có thể mở trong bất kỳ trình đọc PDF nào và thực sự chọn các từ tiếng Hàn.  

**Prerequisites**  
- .NET 6.0 trở lên (mã cũng hoạt động trên .NET Framework 4.7+).  
- Gói NuGet Aspose.OCR cho .NET đã được cài đặt (`Install-Package Aspose.OCR`).  
- Một thư mục chứa `korean_sign.jpg` và một vị trí có quyền ghi cho các tệp đầu ra.  

Nếu bạn đã có những thành phần này, tuyệt vời—hãy bắt tay vào thực hành.

## Bước 1: Khởi tạo OCR Engine cho Korean Language OCR

Điều đầu tiên bạn cần là một thể hiện `OcrEngine`. Bật GPU (nếu bạn có) sẽ tăng tốc độ nhận dạng đáng kể, và tắt tính năng tự động tải tài nguyên buộc thư viện sử dụng các gói ngôn ngữ offline mà bạn cung cấp.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Enums;

// Create the OCR engine
var ocrEngine = new OcrEngine();

// Enable GPU acceleration – optional but fast
ocrEngine.Configuration.EnableGpu = true;

// We’ll supply the Korean language pack ourselves
ocrEngine.Configuration.AutomaticResourceDownload = false;
ocrEngine.Configuration.ResourcesFolder = @"YOUR_DIRECTORY/Resources";
```

> **Tại sao điều này quan trọng:**  
> *GPU acceleration* có thể giảm thời gian xử lý từ giây xuống mili giây cho các lô lớn. Đặt `AutomaticResourceDownload` thành `false` đảm bảo bản demo hoạt động offline—một yêu cầu quan trọng đối với nhiều môi trường doanh nghiệp.

## Bước 2: Tải ảnh từ Stream

Đọc ảnh thông qua một stream mang lại cho bạn sự linh hoạt: bạn có thể lấy tệp từ đĩa, chia sẻ mạng, hoặc thậm chí các blob được lưu trong bộ nhớ. Ở đây chúng ta mở một tệp JPEG cục bộ, nhưng mẫu này cũng hoạt động với bất kỳ `Stream` nào.

```csharp
using System.IO;

// Open the image file as a read‑only stream
using var imageStream = File.OpenRead(@"YOUR_DIRECTORY/korean_sign.jpg");

// Feed the stream to the OCR engine
ocrEngine.Image = ImageStream.FromStream(imageStream);
```

> **Mẹo chuyên nghiệp:** Nếu bạn cần xử lý ảnh được tải lên qua một web API, chỉ cần thay thế `File.OpenRead` bằng `IFormFile.OpenReadStream()`—phần còn lại vẫn giống nhau.

## Bước 3: Chọn Korean Language và Áp dụng các Bộ lọc Tiền Xử lý

Aspose.OCR hỗ trợ một vài bước tiền xử lý để làm sạch ảnh trước khi nhận dạng. Đối với các biển hiệu Hàn Quốc, việc chỉnh nghiêng (deskew) và giảm nhiễu (denoise) thường là đủ.

```csharp
using Aspose.OCR.Enums;

// Tell the engine we’re dealing with Korean text
ocrEngine.Configuration.Language = Language.Korean;

// Apply deskew and denoise filters
ocrEngine.Configuration.PreprocessFilters = PreprocessFilter.Deskew |
                                            PreprocessFilter.Denoise;
```

> **Điều gì đang diễn ra bên trong?**  
> Bộ lọc `Deskew` làm thẳng văn bản bị xoay, trong khi `Denoise` loại bỏ hạt nhiễu có thể làm rối bộ phân loại ký tự. Bỏ qua các bước này thường dẫn đến kết quả rối rắm, đặc biệt với ảnh có độ phân giải thấp.

## Bước 4: Trích xuất Văn bản Thuần Asynchronously

Bây giờ là thời khắc quyết định—yêu cầu engine nhận dạng các ký tự và trả về một chuỗi sạch. Sử dụng `RecognizeAsync` giúp UI phản hồi nhanh nếu bạn nhúng vào ứng dụng desktop hoặc web.

```csharp
// Run OCR and get the plain text result
string plainText = await ocrEngine.RecognizeAsync();
```

Khi bạn chạy chương trình, bạn sẽ thấy một kết quả tương tự:

```
OCR complete. Extracted text:
서울시청
```

> **Tại sao async?**  
> OCR có thể tốn nhiều CPU. Thực thi bất đồng bộ ngăn luồng của bạn bị chặn, điều này đặc biệt hữu ích trong ASP.NET Core nơi tình trạng thiếu luồng là một mối quan ngại thực tế.

## Bước 5: Lấy Kết quả Nhận dạng Chi tiết và Lưu dưới dạng JSON

Đôi khi bạn cần nhiều hơn chỉ chuỗi thô—có thể bạn muốn điểm tin cậy, hộp bao quanh, hoặc dữ liệu ảnh gốc. Phương thức `RecognizeDetailed` trả về một đối tượng `RecognitionResult` có thể được tuần tự hoá thành JSON để phân tích sau.

```csharp
// Detailed result includes confidence, coordinates, etc.
RecognitionResult detailedResult = ocrEngine.RecognizeDetailed();

// Convert to nicely indented JSON
string jsonResult = detailedResult.ToJson(indent: true);

// Persist the JSON to disk
File.WriteAllText(@"YOUR_DIRECTORY/korean_ocr.json", jsonResult);
```

Mở `korean_ocr.json` sẽ hiển thị một cấu trúc tương tự như:

```json
{
  "Pages": [
    {
      "Text": "서울시청",
      "Confidence": 0.98,
      "Words": [
        {
          "Text": "서울시청",
          "BoundingBox": [12,34,56,78],
          "Confidence": 0.98
        }
      ]
    }
  ]
}
```

> **Khi nào nên sử dụng?**  
> Nếu bạn đang xây dựng một chỉ mục tìm kiếm, các giá trị confidence cho phép bạn lọc các kết quả chất lượng thấp. Nếu bạn cần làm nổi bật văn bản trong UI, các hộp bao quanh là bản đồ của bạn.

## Bước 6: Chuyển ảnh sang PDF và Xuất PDF có thể Tìm kiếm

Aspose thực hiện việc chuyển đổi từ raster sang vector một cách dễ dàng. Bằng cách đặt `OutputFormat` thành `SearchablePdf`, thư viện sẽ nhúng ảnh gốc và phủ một lớp văn bản vô hình chứa kết quả OCR. PDF tạo ra có thể được tìm kiếm, sao chép và lập chỉ mục giống như bất kỳ PDF gốc nào.

```csharp
using Aspose.OCR.Enums;

// Tell the engine to produce a searchable PDF
ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf;

// Save the PDF to the target folder
ocrEngine.Save(@"YOUR_DIRECTORY/korean_searchable.pdf");
```

Mở `korean_searchable.pdf` trong Adobe Reader hoặc bất kỳ trình xem PDF nào, nhấn **Ctrl+F**, gõ một từ tiếng Hàn, và xem nó nhảy đến vị trí chính xác trên trang. Đó là sức mạnh của PDF có thể tìm kiếm.

> **Mẹo bổ sung:** Nếu bạn chỉ cần một PDF trực quan mà không có lớp văn bản ẩn, hãy chuyển `OutputFormat` sang `Pdf` thay vì.

## Ví dụ Hoàn chỉnh

Dưới đây là chương trình hoàn chỉnh—sao chép, dán, thay thế `YOUR_DIRECTORY` bằng một đường dẫn thực tế, và nhấn **F5**.

```csharp
using System;
using System.IO;
using System.Threading.Tasks;
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Enums;

class OcrDemo
{
    static async Task Main()
    {
        // Step 1: Create the OCR engine and enable GPU with offline resources
        var ocrEngine = new OcrEngine();
        ocrEngine.Configuration.EnableGpu = true;
        ocrEngine.Configuration.AutomaticResourceDownload = false;
        ocrEngine.Configuration.ResourcesFolder = @"YOUR_DIRECTORY/Resources";

        // Step 2: Select the language and apply preprocessing filters
        ocrEngine.Configuration.Language = Language.Korean;
        ocrEngine.Configuration.PreprocessFilters = PreprocessFilter.Deskew |
                                                    PreprocessFilter.Denoise;

        // Step 3: Load the image to be recognized from a file stream
        using var imageStream = File.OpenRead(@"YOUR_DIRECTORY/korean_sign.jpg");
        ocrEngine.Image = ImageStream.FromStream(imageStream);

        // Step 4: Run OCR asynchronously and obtain the plain text result
        string plainText = await ocrEngine.RecognizeAsync();

        // Step 5: Get a detailed recognition result, convert it to JSON, and save it
        RecognitionResult detailedResult = ocrEngine.RecognizeDetailed();
        string jsonResult = detailedResult.ToJson(indent: true);
        File.WriteAllText(@"YOUR_DIRECTORY/korean_ocr.json", jsonResult);

        // Step 6: Export the recognized page as a searchable PDF
        ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf;
        ocrEngine.Save(@"YOUR_DIRECTORY/korean_searchable.pdf");

        Console.WriteLine("OCR complete. Extracted text:");
        Console.WriteLine(plainText);
    }
}
```

### Kết quả Console dự kiến

```
OCR complete. Extracted text:
서울시청
```

Và bạn sẽ thấy ba tệp mới bên cạnh ảnh nguồn của mình:

- `korean_ocr.json` – dữ liệu nhận dạng đầy đủ.  
- `korean_searchable.pdf` – PDF có thể tìm kiếm.  
- (tùy chọn) bất kỳ log trung gian nào bạn muốn thêm.

## Câu hỏi Thường gặp & Trường hợp Đặc biệt

**Nếu tôi không có GPU thì sao?**  
Đặt `EnableGpu = false`; việc chuyển sang CPU hoàn toàn ổn cho các lô nhỏ.

**Tôi có thể xử lý nhiều ảnh trong một lần chạy không?**  
Chắc chắn. Bao bọc logic chính trong một vòng lặp `foreach (var file in Directory.GetFiles(...))` và gán lại `ocrEngine.Image` mỗi lần lặp.

**Làm sao để xử lý các ngôn ngữ khác cùng với tiếng Hàn?**  
Aspose.OCR cho phép bạn đặt `Language = Language.AutoDetect` hoặc kết hợp các ngôn ngữ bằng toán tử OR bitwise (ví dụ, `Language.Korean | Language.English`).

**Nếu độ tin cậy OCR thấp thì sao?**  
Kiểm tra `detailedResult.Pages[0].Words` và lọc các mục có `Confidence < 0.7`. Bạn cũng có thể điều chỉnh các bộ lọc tiền xử lý—thử thêm `PreprocessFilter.ContrastEnhancement`.

## Kết luận

Bạn vừa thấy cách thực hiện **Korean Language OCR** từ đầu đến cuối, từ **loading image from stream** đến **extract plain text**, sau đó **convert image to PDF** và cuối cùng **export searchable PDF**. Cách tiếp cận này mô-đun, vì vậy bạn có thể thay đổi nguồn ảnh, thay đổi định dạng đầu ra, hoặc đưa JSON vào bất kỳ pipeline nào tiếp theo.

What’s next

## Các Hướng dẫn Liên quan

- [Trích xuất văn bản ảnh C# với lựa chọn ngôn ngữ bằng Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Nhận dạng văn bản ảnh với Aspose OCR cho nhiều ngôn ngữ](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [Trích xuất Văn bản từ Ảnh – Tối ưu hóa OCR với Aspose.OCR cho .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}