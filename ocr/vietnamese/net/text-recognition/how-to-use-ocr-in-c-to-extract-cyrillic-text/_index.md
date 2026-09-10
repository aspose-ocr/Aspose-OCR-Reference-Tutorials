---
category: general
date: 2026-09-10
description: Cách sử dụng OCR trong C# để trích xuất văn bản Cyrillic, tiền xử lý
  hình ảnh và chuyển đổi chúng thành tệp PDF hoặc HTML trong một ví dụ duy nhất, có
  thể chạy được.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use OCR
- preprocess image for OCR
- convert image to PDF
- convert image to HTML
- extract Cyrillic text
language: vi
lastmod: 2026-09-10
og_description: Cách sử dụng OCR trong C# để trích xuất văn bản Cyrillic, tiền xử
  lý hình ảnh và xuất kết quả dưới dạng PDF hoặc HTML. Hãy làm theo hướng dẫn từng
  bước này.
og_image_alt: Diagram illustrating how to use OCR to extract Cyrillic text and convert
  images
og_title: Cách sử dụng OCR trong C# – trích xuất văn bản Cyrillic và chuyển đổi hình
  ảnh
schemas:
- author: Aspose
  dateModified: '2026-09-10'
  description: How to use OCR in C# to extract Cyrillic text, preprocess images, and
    convert them to PDF or HTML files in a single, runnable example.
  headline: How to use OCR in C# to extract Cyrillic text
  type: TechArticle
tags:
- OCR
- C#
- Cyrillic
- Image processing
- PDF conversion
title: Cách sử dụng OCR trong C# để trích xuất văn bản Cyrillic
url: /vi/net/text-recognition/how-to-use-ocr-in-c-to-extract-cyrillic-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách sử dụng OCR trong C# để trích xuất văn bản Cyrillic

Nếu bạn cần **cách sử dụng OCR** trong C# để trích xuất văn bản Cyrillic từ tài liệu đã quét, hướng dẫn này sẽ cho bạn một giải pháp hoàn chỉnh, sẵn sàng chạy. Bạn cũng sẽ học cách **tiền xử lý hình ảnh cho OCR**, và cách **chuyển đổi hình ảnh sang PDF** hoặc **chuyển đổi hình ảnh sang HTML** sau khi văn bản đã được nhận dạng.

Các dự án số hóa tài liệu thường gặp hai vấn đề: bản quét chất lượng thấp và nhu cầu lưu kết quả ở nhiều định dạng. Bài hướng dẫn này giải quyết cả hai bằng cách sử dụng thư viện Aspose.OCR, tự động tải xuống các gói ngôn ngữ còn thiếu, cung cấp các công cụ xử lý ảnh tích hợp, và có thể xuất kết quả OCR sang PDF hoặc HTML chỉ với một lệnh.

## Yêu cầu trước

* .NET 6.0 SDK hoặc phiên bản mới hơn (mã cũng hoạt động với .NET Framework 4.7+).
* Visual Studio 2022 hoặc bất kỳ trình soạn thảo nào hỗ trợ dự án C#.
* Gói **Aspose.OCR** NuGet. Cài đặt bằng:

```bash
dotnet add package Aspose.OCR
```

* Một tệp hình ảnh chứa các ký tự Cyrillic (ví dụ, `sample_cyrillic.jpg`).  
  Đặt tệp này vào thư mục bạn có thể tham chiếu bằng `YOUR_DIRECTORY`.

Thư viện sẽ tự động tải xuống gói ngôn ngữ Cyrillic lần đầu tiên bạn đặt `ocrEngine.Language = Language.Cyrillic;`, vì vậy không cần tải xuống thủ công.

## Bước 1 – Khởi tạo công cụ OCR (cách sử dụng OCR)

Tạo một thể hiện `OcrEngine` chuẩn bị công cụ cho tất cả các thao tác tiếp theo.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

class Program
{
    static void Main()
    {
        // Initialize the OCR engine – the first step in how to use OCR with Aspose
        var ocrEngine = new OcrEngine();
```

**Tại sao điều này quan trọng:** Công cụ chứa các cấu hình như ngôn ngữ, cài đặt xử lý ảnh và tùy chọn đầu ra. Khởi tạo một lần giúp phần còn lại của mã sạch sẽ và an toàn với đa luồng.

## Bước 2 – Chọn ngôn ngữ Cyrillic (trích xuất văn bản Cyrillic)

```csharp
        // Select Cyrillic language; the pack is fetched automatically if missing
        ocrEngine.Language = Language.Cyrillic;
```

**Tại sao điều này quan trọng:** Độ chính xác của OCR phụ thuộc mạnh vào mô hình ngôn ngữ đúng. Bằng cách chọn rõ ràng `Language.Cyrillic`, công cụ áp dụng các bảng tần suất ký tự phù hợp cho tiếng Nga, Ukraina, Bulgaria, v.v.

## Bước 3 – Tiền xử lý hình ảnh cho OCR

Các bản quét chất lượng thấp có thể bị lệch, có điểm nhiễu, hoặc ánh sáng không đồng đều. `ImageProcessor` tích hợp có thể cải thiện tỷ lệ nhận dạng chỉ với hai lệnh.

```csharp
        // Optional but strongly recommended: deskew and despeckle the image
        ocrEngine.ImageProcessor.Deskew();      // Aligns rotated text
        ocrEngine.ImageProcessor.Despeckle();  // Removes isolated noise pixels
```

**Tại sao điều này quan trọng:** Tiền xử lý giảm các ký tự sai và tăng điểm tin cậy. Văn bản lệch thường cho ra kết quả rối; việc chỉnh lại góc sẽ thẳng thắn hơn. Loại bỏ nhiễu loại bỏ các artefact nhỏ mà công cụ OCR có thể nhầm thành chữ.

> **Mẹo chuyên nghiệp:** Nếu hình ảnh nguồn của bạn đã sạch sẽ, bạn có thể bỏ qua các lệnh này. Đối với các bản quét bị hư hỏng nặng, hãy cân nhắc các bước bổ sung như `Binarize()` hoặc `ContrastStretch()`.

## Bước 4 – Thực hiện OCR trên hình ảnh đầu vào

```csharp
        // The image path can be absolute or relative to the executable
        string inputPath = Path.Combine("YOUR_DIRECTORY", "sample_cyrillic.jpg");
        ocrEngine.Process(inputPath);
```

**Tại sao điều này quan trọng:** `Process` chạy quy trình nhận dạng trên bitmap được cung cấp. Nó trả về `void`; văn bản đã nhận dạng sẽ có sẵn qua thuộc tính `Text`.

## Bước 5 – Lấy văn bản đã nhận dạng và lưu vào tệp

```csharp
        // Access the recognized string
        string recognizedText = ocrEngine.Text;

        // Save the plain‑text result
        string txtOutput = Path.Combine("YOUR_DIRECTORY", "result.txt");
        File.WriteAllText(txtOutput, recognizedText);
        Console.WriteLine("Text saved to: " + txtOutput);
```

**Tại sao điều này quan trọng:** Lưu trữ văn bản thô cho phép các xử lý tiếp theo như tìm kiếm, lập chỉ mục, hoặc đưa vào dịch vụ dịch thuật.

## Bước 6 – Xuất kết quả OCR sang các định dạng khác (chuyển đổi hình ảnh sang PDF & chuyển đổi hình ảnh sang HTML)

```csharp
        // Export as PDF – useful for archival or sharing with non‑technical users
        string pdfOutput = Path.Combine("YOUR_DIRECTORY", "result.pdf");
        ocrEngine.SaveResultAsPdf(pdfOutput);
        Console.WriteLine("PDF saved to: " + pdfOutput);

        // Export as HTML – retains basic layout and can be displayed in browsers
        string htmlOutput = Path.Combine("YOUR_DIRECTORY", "result.html");
        ocrEngine.SaveResultAsHtml(htmlOutput);
        Console.WriteLine("HTML saved to: " + htmlOutput);
    }
}
```

**Tại sao điều này quan trọng:** Chuyển đổi kết quả OCR sang PDF hoặc HTML cho phép bạn giữ ngữ cảnh hình ảnh gốc đồng thời cung cấp văn bản có thể tìm kiếm. Điều này đặc biệt có giá trị cho các quy trình pháp lý hoặc lưu trữ.

### Kết quả mong đợi

Chạy chương trình với bản quét Cyrillic rõ ràng sẽ tạo ra ba tệp:

* `result.txt` – văn bản Unicode thuần, ví dụ `Пример текста на кириллице`.
* `result.pdf` – một PDF chứa hình ảnh với lớp văn bản ẩn để tìm kiếm.
* `result.html` – một trang HTML hiển thị hình ảnh và văn bản có thể chọn.

Mở bất kỳ tệp nào để xác nhận rằng các ký tự Cyrillic đã được trích xuất đúng.

## Các câu hỏi thường gặp và trường hợp đặc biệt

| Câu hỏi | Trả lời |
|----------|--------|
| **Nếu gói ngôn ngữ không tải xuống được thì sao?** | Đảm bảo máy có kết nối internet. Bạn cũng có thể tải trước gói từ trang của Aspose và đặt vào thư mục `bin`. |
| **Tôi có thể nhận dạng các bảng chữ cái khác trong cùng một lần chạy không?** | Có. Gọi `ocrEngine.Language = Language.English;` (hoặc bất kỳ enum nào được hỗ trợ) trước `Process`. Bạn có thể cần chạy `Process` riêng cho mỗi ngôn ngữ nếu hình ảnh chứa hỗn hợp các script. |
| **Hình ảnh của tôi là TIFF đa trang – có hoạt động không?** | `OcrEngine` xử lý một bitmap mỗi lần. Tải mỗi trang vào một `Bitmap` và gọi `Process` trong vòng lặp, nối các kết quả lại với nhau. |
| **Làm thế nào để tăng hiệu năng cho các lô lớn?** | Tái sử dụng một thể hiện `OcrEngine` duy nhất và đặt `ocrEngine.OptimizeMemory = true;`. Ngoài ra, cân nhắc xử lý song song với các thể hiện công cụ riêng cho mỗi luồng. |

## Kết luận

Bây giờ bạn đã biết **cách sử dụng OCR** trong C# để **trích xuất văn bản Cyrillic**, **tiền xử lý hình ảnh cho OCR**, và **chuyển đổi hình ảnh sang PDF** hoặc **chuyển đổi hình ảnh sang HTML** trong vài bước ngắn gọn. Ví dụ hoàn chỉnh minh họa một môi trường sản xuất‑

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách sử dụng AspOCR: Tiền xử lý bộ lọc OCR cho hình ảnh cho .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Cách trích xuất văn bản OCR trong C# – Hướng dẫn từng bước hoàn chỉnh](/ocr/english/net/text-recognition/how-to-extract-ocr-text-in-c-complete-step-by-step-guide/)
- [Cách sử dụng Aspose OCR để nhận kết quả JSON trong nhận dạng hình ảnh](/ocr/english/net/text-recognition/get-result-as-json/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}