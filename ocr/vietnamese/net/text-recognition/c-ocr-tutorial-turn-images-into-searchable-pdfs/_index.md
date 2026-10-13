---
category: general
date: 2026-01-12
description: Hướng dẫn OCR C# cho bạn cách nhận dạng ảnh văn bản, trích xuất văn bản
  từ ảnh bằng C# và tạo tệp OCR ảnh sang PDF kèm điểm tin cậy.
draft: false
keywords:
- c# ocr tutorial
- image to pdf ocr
- recognize text image
- ocr confidence scores
- extract text image c#
language: vi
og_description: Học một hướng dẫn OCR C# hoàn chỉnh để nhận dạng hình ảnh văn bản,
  trích xuất văn bản từ hình ảnh bằng C# và tạo tài liệu OCR từ hình ảnh sang PDF
  với điểm tin cậy.
og_title: hướng dẫn OCR C# – Chuyển ảnh thành PDF có thể tìm kiếm
tags:
- OCR
- C#
- PDF
title: Hướng dẫn OCR C# – Chuyển hình ảnh thành PDF có thể tìm kiếm
url: /vi/net/text-recognition/c-ocr-tutorial-turn-images-into-searchable-pdfs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – Chuyển Hình Ảnh thành PDF có thể Tìm kiếm

Bạn đã bao giờ tự hỏi làm thế nào để **nhận dạng hình ảnh văn bản** trong một dự án C# mà không phải tìm kiếm dịch vụ của bên thứ ba? Bạn không phải là người duy nhất. Trong nhiều ứng dụng thực tế—như máy quét hoá đơn, theo dõi biên lai, hoặc kho lưu trữ tài liệu đa ngôn ngữ—các nhà phát triển cần một công cụ OCR đáng tin cậy, chạy trên máy chủ nội bộ và cũng cung cấp điểm tin cậy.

Bài **c# ocr tutorial** này sẽ hướng dẫn bạn qua mọi thứ cần thiết: từ việc tải ảnh, chọn mô hình ngôn ngữ, bật/tắt tăng tốc GPU, đến việc lưu kết quả dưới dạng PDF có thể tìm kiếm. Khi kết thúc, bạn sẽ có một mẫu mã sẵn sàng chạy, trích xuất văn bản, báo cáo độ tin cậy OCR, và tùy chọn tạo một tệp *image to pdf ocr* — tất cả trong chưa tới một phút viết mã.

## Những gì bạn sẽ xây dựng

- Tải một hình ảnh đa ngôn ngữ (`sample_multi_lang.jpg` được sử dụng làm placeholder).  
- Chọn các mô hình ngôn ngữ Arabic, Hindi và Russian (bạn có thể thêm nữa).  
- Bật xử lý GPU nếu máy của bạn hỗ trợ.  
- Lấy kết quả OCR thô **với điểm tin cậy**.  
- Chuỗi hoá kết quả thành JSON được định dạng đẹp **hoặc** ghi ra PDF có thể tìm kiếm.  

Không có dịch vụ web bên ngoài, không có phép thuật ẩn—chỉ có Aspose.OCR cho .NET, một vài dòng C#, và giải thích rõ ràng **tại sao** mỗi dòng lại quan trọng.

## Yêu cầu trước

- .NET 6.0 hoặc phiên bản sau (mã được biên dịch trên .NET Core và .NET Framework).  
- Visual Studio 2022 (hoặc bất kỳ IDE nào bạn thích).  
- Giấy phép Aspose.OCR cho .NET (bản dùng thử miễn phí hoạt động cho việc thử nghiệm).  
- Tùy chọn: GPU tương thích CUDA nếu bạn muốn tăng tốc nhận dạng.  

> **Mẹo chuyên nghiệp:** Nếu bạn không có GPU, chỉ cần đặt `UseGpu = false` và engine sẽ tự chuyển sang CPU mà không cần thay đổi mã.

## Bước 1: Cài đặt các gói NuGet cần thiết

Mở **Package Manager Console** và chạy:

```powershell
Install-Package Aspose.OCR
Install-Package Aspose.OCR.Gpu
Install-Package Newtonsoft.Json
```

Ba gói này cung cấp cho bạn engine OCR, tăng tốc GPU, và một bộ tuần tự hoá JSON đẹp cho đầu ra điểm tin cậy.

## Bước 2: Thiết lập cấu trúc dự án

Tạo một dự án console mới (`dotnet new console -n AsposeOcrDemo`) và thay thế `Program.cs` được tạo tự động bằng đoạn mã dưới đây.  
Toàn bộ logic nằm trong lớp `Program`; kiểu bổ sung duy nhất là một phương thức mở rộng nhỏ để định dạng kết quả OCR thành JSON.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Gpu;
using Aspose.OCR.Models;
using Newtonsoft.Json;

namespace AsposeOcrDemo
{
    class Program
    {
        // Step 1: Input image and language models
        private const string InputImagePath = @"YOUR_DIRECTORY/sample_multi_lang.jpg";
        private static readonly string[] Languages = { LanguageModel.Arabic, LanguageModel.Hindi, LanguageModel.Russian };

        // Step 2: Processing options (GPU toggle & output format)
        private const bool UseGpu = true;               // set false if no GPU
        private const string OutputFormat = "Json";     // change to "Pdf" for PDF output

        static void Main()
        {
            // Step 3: Initialise the appropriate OCR engine
            IOcrEngine engine = UseGpu ? (IOcrEngine)new GpuOcrEngine() : new OcrEngine();

            // Step 4: Run OCR – language models are auto‑downloaded if missing
            OcrResult result = engine.Recognize(
                InputImagePath,
                new OcrOptions { LanguageModels = Languages, AutoDownloadResources = true });

            // Step 5: Emit the result in the chosen format
            if (OutputFormat.Equals("json", StringComparison.OrdinalIgnoreCase))
            {
                string json = JsonConvert.SerializeObject(
                    result.GetWordsWithConfidence(),
                    Formatting.Indented);
                Console.WriteLine(json);
            }
            else if (OutputFormat.Equals("pdf", StringComparison.OrdinalIgnoreCase))
            {
                string pdfPath = Path.ChangeExtension(InputImagePath, ".pdf");
                File.WriteAllBytes(pdfPath, result.Pdf);
                Console.WriteLine($"PDF saved to: {pdfPath}");
            }
        }
    }

    // Helper that flattens OcrResult into a JSON‑friendly structure
    internal static class OcrResultExtensions
    {
        public static object GetWordsWithConfidence(this OcrResult result)
        {
            var words = new System.Collections.Generic.List<object>();
            foreach (var w in result.Words)
                words.Add(new
                {
                    Text = w.Text,
                    Confidence = w.Confidence,
                    BoundingBox = new { w.Bounds.X, w.Bounds.Y, w.Bounds.Width, w.Bounds.Height }
                });

            return new
            {
                RecognizedText = result.Text,
                LanguageModels = result.UsedLanguageModels,
                Words = words,
                ProcessingTimeMs = result.ProcessingTime.TotalMilliseconds
            };
        }
    }
}
```

### Tại sao đoạn mã này hoạt động

1. **GPU toggle** – `GpuOcrEngine` tận dụng các lõi CUDA; toán tử ba ngôi giúp việc chuyển đổi trở nên dễ dàng.  
2. **Automatic language download** – `AutoDownloadResources = true` đảm bảo các mô hình Arabic, Hindi và Russian được tải về lần đầu khi bạn chạy ứng dụng.  
3. **Confidence scores** – `result.Words` chứa một `Confidence` cho mỗi từ được nhận dạng; phương thức mở rộng định dạng chúng thành một đối tượng JSON sạch sẽ.  
4. **Searchable PDF** – `result.Pdf` đã là một PDF có thể tìm kiếm đầy đủ, vì vậy chúng ta chỉ cần ghi mảng byte ra đĩa. Không cần thư viện bổ sung.

## Bước 6: Chạy mẫu

Mở terminal, chuyển tới thư mục dự án, và thực thi:

```bash
dotnet run
```

Nếu bạn chọn đầu ra **JSON**, bạn sẽ thấy một cái gì đó giống như:

```json
{
  "RecognizedText": "مرحبا Hello Привет",
  "LanguageModels": [
    "Arabic",
    "Hindi",
    "Russian"
  ],
  "Words": [
    {
      "Text": "مرحبا",
      "Confidence": 0.98,
      "BoundingBox": { "X": 45, "Y": 12, "Width": 120, "Height": 30 }
    },
    {
      "Text": "Hello",
      "Confidence": 0.99,
      "BoundingBox": { "X": 180, "Y": 12, "Width": 80, "Height": 30 }
    },
    {
      "Text": "Привет",
      "Confidence": 0.97,
      "BoundingBox": { "X": 280, "Y": 12, "Width": 110, "Height": 30 }
    }
  ],
  "ProcessingTimeMs": 312
}
```

Nếu bạn chuyển sang **PDF**, console sẽ in ra đường dẫn và bạn sẽ tìm thấy một PDF có thể tìm kiếm ngay bên cạnh hình ảnh nguồn.

## Các câu hỏi thường gặp & Trường hợp đặc biệt

- **Nếu mô hình ngôn ngữ không có?**  
  Engine OCR sẽ ném ra một `ResourceNotFoundException` rõ ràng. Vì chúng ta đã đặt `AutoDownloadResources = true`, mô hình thiếu sẽ được tải tự động lần đầu, vì vậy ngoại lệ này hiếm khi xuất hiện trong môi trường sản xuất.

- **Có thể xử lý một loạt hình ảnh?**  
  Hoàn toàn có thể. Đặt lời gọi `engine.Recognize` trong một vòng `foreach` duyệt qua thư mục chứa các tệp. `OcrResultExtensions` vẫn hoạt động cho mỗi hình ảnh.

- **Có cần giấy phép cho GPU không?**  
  Không. Bản dùng thử miễn phí hoạt động cho cả CPU và GPU. Giấy phép đầy đủ sẽ loại bỏ watermark dùng thử và bỏ giới hạn số trang.

- **Độ chính xác của các điểm tin cậy như thế nào?**  
  Điểm nằm trong khoảng từ 0.0 (không tin cậy) đến 1.0 (tin cậy hoàn hảo). Thực tế, bất kỳ giá trị nào trên 0.90 đều đáng tin cậy cho các quy trình tiếp theo; bạn có thể lọc các từ có điểm tin cậy thấp hơn nếu cần độ kiểm tra chặt chẽ hơn.

## Bước 7: Các bước tiếp theo (Mở rộng bộ công cụ OCR của bạn)

1. **Thêm nhiều ngôn ngữ** – chỉ cần thêm `LanguageModel.French` (hoặc bất kỳ mô hình nào được hỗ trợ) vào mảng `Languages`.  
2. **Kết hợp OCR với chuyển đổi PDF/A** – Aspose.PDF có thể nhúng lớp OCR vào tài liệu PDF/A‑2b tuân thủ để lưu trữ.  
3. **Tích hợp với Azure Functions** – đóng gói logic vào một endpoint không máy chủ để xử lý tải lên ngay lập tức.  
4. **Tinh chỉnh ngưỡng tin cậy** – sử dụng `result.Words.Where(w => w.Confidence < 0.85)` để đánh dấu các từ không chắc chắn cho việc xem xét thủ công.

---

### TL;DR

Bài **c# ocr tutorial** này cho bạn biết cách:

- Tải một hình ảnh và chọn nhiều mô hình ngôn ngữ.  
- Bật tăng tốc GPU bằng một cờ boolean duy nhất.  
- Lấy kết quả OCR **với điểm tin cậy** và chuỗi hoá chúng thành JSON.  
- Tùy chọn ghi ra PDF có thể tìm kiếm (**image to pdf ocr**).  

Tất cả những điều trên đều có thể thực hiện chỉ với một vài dòng mã, bản dùng thử miễn phí của Aspose.OCR, và đoạn mã ở trên. Hãy thử, điều chỉnh danh sách ngôn ngữ, và bạn sẽ có một quy trình OCR sẵn sàng cho sản xuất trong vài phút.

![c# ocr tutorial example image](https://example.com/placeholder-image.jpg "c# ocr tutorial example image")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}