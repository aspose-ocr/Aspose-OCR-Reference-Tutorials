---
category: general
date: 2026-05-21
description: Tạo PDF có thể tìm kiếm bằng Aspose OCR, đồng thời nâng cao độ chính
  xác của OCR và học cách tải ảnh để OCR trong C#. Hướng dẫn chi tiết từng bước.
draft: false
keywords:
- create searchable PDF
- improve OCR accuracy
- load image for OCR
- Aspose OCR C#
- PDF output with OCR
language: vi
og_description: Tạo PDF có thể tìm kiếm với Aspose OCR. Tìm hiểu cách cải thiện độ
  chính xác của OCR và tải hình ảnh cho OCR trong một ví dụ duy nhất, có thể chạy
  được.
og_title: Tạo PDF có thể tìm kiếm với Aspose OCR – Hướng dẫn toàn diện
schemas:
- author: Aspose
  dateModified: '2026-05-21'
  description: Create searchable PDF using Aspose OCR while you improve OCR accuracy
    and learn how to load image for OCR in C#. Step‑by‑step tutorial.
  headline: Create Searchable PDF with Aspose OCR – Complete Programming Guide
  type: TechArticle
tags:
- OCR
- Aspose
- PDF
- C#
title: Tạo PDF có thể tìm kiếm với Aspose OCR – Hướng dẫn lập trình đầy đủ
url: /vi/net/ocr-optimization/create-searchable-pdf-with-aspose-ocr-complete-programming-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo PDF có thể tìm kiếm với Aspose OCR – Hướng dẫn lập trình đầy đủ

Bạn đã bao giờ cần **tạo PDF có thể tìm kiếm** từ một hình ảnh đã quét nhưng không biết bắt đầu từ đâu chưa? Bạn không đơn độc—nhiều nhà phát triển gặp khó khăn này khi lần đầu tiên thực hiện các dự án OCR. Tin tốt là Aspose OCR làm cho toàn bộ quy trình—tải hình ảnh, tinh chỉnh ảnh để có kết quả tốt hơn, và cuối cùng lưu thành PDF có thể tìm kiếm—rất đơn giản.

Trong hướng dẫn này, chúng tôi sẽ đi qua một ví dụ đầy đủ, từ đầu đến cuối, không chỉ cho bạn cách **tạo PDF có thể tìm kiếm**, mà còn minh họa cách **cải thiện độ chính xác OCR** và cách **tải hình ảnh cho OCR** đúng cách. Khi hoàn thành, bạn sẽ có một ứng dụng console C# sẵn sàng chạy, tạo ra một PDF có thể tìm kiếm với hình ảnh gốc được nhúng.

## Bạn sẽ học được gì

- Cài đặt Aspose OCR (bao gồm tùy chọn tăng tốc GPU)  
- Cấu hình engine cho tiếng Pháp (hoặc bất kỳ ngôn ngữ nào) để **cải thiện độ chính xác OCR**  
- **Tải hình ảnh cho OCR** đúng cách bằng `ImageStream`  
- Xây dựng chuỗi bộ lọc để làm sạch hình ảnh trước khi nhận dạng  
- Lưu kết quả dưới dạng PDF có thể tìm kiếm với hình ảnh nguồn được nhúng  

Không cần bất kỳ phụ thuộc bên ngoài nào ngoài Aspose OCR, và mã hoạt động trên .NET 6+ (hoặc .NET Framework 4.6+). Hãy bắt đầu.

---

![Mẫu PDF có thể tìm kiếm được tạo bởi Aspose OCR – ví dụ tạo PDF có thể tìm kiếm](images/searchable-pdf-sample.png "ví dụ tạo PDF có thể tìm kiếm")

## Bước 1: Tạo PDF có thể tìm kiếm – Bật GPU & Đặt đường dẫn tài nguyên  

Nếu bạn có một GPU tương thích, bật nó có thể tăng tốc độ nhận dạng một cách đáng kể. Ngay cả khi bạn bỏ qua bước này, phần còn lại của mã vẫn hoạt động tốt.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;          // optional GPU support
using Aspose.OCR.Pdf;          // PDF output
using Aspose.OCR.Filters;     // pre‑processing filters

// Enable GPU acceleration (optional)
OcrEngine.EnableGpu(true);

// Tell Aspose where to find language data files (offline mode)
OcrEngine.SetResourcesPath(@"YOUR_DIRECTORY/Resources");
```

**Tại sao điều này quan trọng:** Tăng tốc GPU giảm độ trễ khi xử lý các lô lớn, và việc đặt đường dẫn tài nguyên đảm bảo engine có thể hoạt động mà không cần kết nối internet—hoàn hảo cho các pipeline CI hoặc môi trường không có kết nối mạng.

> **Mẹo chuyên nghiệp:** Nếu bạn đang chạy trên máy chủ không có giao diện, hãy kiểm tra driver CUDA có khớp với phiên bản đi kèm trong Aspose OCR; các phiên bản không khớp có thể gây ra lỗi im lặng.

## Bước 2: Cải thiện độ chính xác OCR – Chọn ngôn ngữ phù hợp  

Chọn mô hình ngôn ngữ đúng là cách nhanh để nâng cao độ chính xác. Ở đây chúng tôi chọn tiếng Pháp, nhưng bạn có thể thay `OcrLanguage.French` bằng bất kỳ ngôn ngữ nào được hỗ trợ.

```csharp
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.French   // improves OCR accuracy for French documents
};
```

**Tại sao điều này quan trọng:** Các từ điển đặc thù cho ngôn ngữ giúp engine giải quyết các ký tự mơ hồ (ví dụ, “œ” so với “oe”). Nếu bỏ qua bước này, engine sẽ mặc định tiếng Anh, điều này có thể làm giảm đáng kể **cải thiện độ chính xác OCR** cho các văn bản không phải tiếng Anh.

## Bước 3: Tải hình ảnh cho OCR – Sử dụng ImageStream  

Bây giờ chúng ta **tải hình ảnh cho OCR**. Trợ giúp `ImageStream.FromFile` trừu tượng hoá việc xử lý bitmap thô và hoạt động với hầu hết các định dạng phổ biến (JPG, PNG, TIFF).

```csharp
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/input.jpg");
```

**Tại sao điều này quan trọng:** Tải hình ảnh theo cách này đảm bảo Aspose nhận được hình ảnh ở định dạng mà nó có thể xử lý hiệu quả. Nếu bạn cố gắng truyền trực tiếp một `Bitmap` thô, có thể gặp các vấn đề quản lý bộ nhớ khi làm việc với các tệp lớn.

## Bước 4: Xây dựng chuỗi bộ lọc hình ảnh để tăng độ chính xác  

Một hình ảnh sạch sẽ là một nửa thành công. Chuỗi bộ lọc dưới đây sẽ chỉnh nghiêng ảnh và loại bỏ nhiễu nền—hai nguyên nhân cổ điển làm giảm **cải thiện độ chính xác OCR**.

```csharp
var filterPipeline = new ImageFilterPipeline();
filterPipeline.Add(new DeskewFilter());   // corrects rotation
filterPipeline.Add(new DenoiseFilter()); // reduces grainy artifacts

// Apply the pipeline and replace the original image
ocrEngine.Image = filterPipeline.Apply(ocrEngine.Image);
```

**Tại sao điều này quan trọng:** Việc chỉnh nghiêng (deskew) đảm bảo các dòng văn bản nằm ngang, trong khi giảm nhiễu (denoising) giảm các khối ký tự sai. Bạn có thể thêm các bộ lọc khác (ví dụ, `ContrastFilter`) nếu các bản quét nguồn của bạn đặc biệt kém chất lượng.

## Bước 5: Thực hiện nhận dạng OCR  

Với hình ảnh đã được tiền xử lý, cuối cùng chúng ta để engine thực hiện phép màu của nó.

```csharp
ocrEngine.Recognize();
```

Dòng lệnh duy nhất này kích hoạt mô hình deep‑learning phía sau Aspose OCR. Nó sẽ điền `ocrEngine.Text` bằng văn bản thuần và đồng thời chuẩn bị đầu ra PDF.

> **Nếu văn bản bị rối?** Hãy kiểm tra lại cài đặt ngôn ngữ ở Bước 2 và cân nhắc thêm `BinarizeFilter` vào chuỗi bộ lọc.

## Bước 6: Lưu kết quả dưới dạng PDF có thể tìm kiếm  

Phần cuối cùng là lưu một **PDF có thể tìm kiếm** trong đó văn bản đã trích xuất nằm phía sau hình ảnh gốc—đúng những gì bạn cần cho tài liệu pháp lý hoặc lưu trữ.

```csharp
ocrEngine.Save(@"YOUR_DIRECTORY/output.pdf",
    new PdfSaveOptions { EmbedOriginalImage = true });
```

**Tại sao điều này quan trọng:** `EmbedOriginalImage = true` giữ nguyên độ trung thực hình ảnh quét trong khi vẫn cho phép tìm kiếm văn bản. Nếu bạn đặt nó thành `false`, PDF sẽ chỉ chứa văn bản đã trích xuất, hữu ích cho các kho lưu trữ nhẹ.

### Tùy chọn: In văn bản đã nhận dạng & JSON  

Nếu bạn muốn kiểm tra đầu ra thô, các dòng này sẽ xuất ra văn bản thuần và một payload JSON có cấu trúc.

```csharp
Console.WriteLine(ocrEngine.Text);               // plain text
Console.WriteLine(ocrEngine.GetResultAsJson());  // JSON with layout info
```

**Kết quả mong đợi:** Sau khi chạy chương trình, bạn sẽ thấy các câu tiếng Pháp được in ra console, tiếp theo là một đối tượng JSON chứa các hộp bao, điểm tin cậy và siêu dữ liệu ngôn ngữ.

---

## Ví dụ hoàn chỉnh (Sẵn sàng sao chép‑dán)

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;          // optional GPU support
using Aspose.OCR.Pdf;          // PDF output
using Aspose.OCR.Filters;     // pre‑processing filters

// 1️⃣ Enable GPU (optional) and set resources path
OcrEngine.EnableGpu(true);
OcrEngine.SetResourcesPath(@"YOUR_DIRECTORY/Resources");

// 2️⃣ Create and configure the OCR engine (improve OCR accuracy)
var ocrEngine = new OcrEngine { Language = OcrLanguage.French };

// 3️⃣ Load the source image (load image for OCR)
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/input.jpg");

// 4️⃣ Build filter pipeline (deskew + denoise)
var filterPipeline = new ImageFilterPipeline();
filterPipeline.Add(new DeskewFilter());
filterPipeline.Add(new DenoiseFilter());
ocrEngine.Image = filterPipeline.Apply(ocrEngine.Image);

// 5️⃣ Recognize text
ocrEngine.Recognize();

// 6️⃣ Save as searchable PDF (create searchable PDF)
ocrEngine.Save(@"YOUR_DIRECTORY/output.pdf",
    new PdfSaveOptions { EmbedOriginalImage = true });

// Optional: output text and JSON
Console.WriteLine(ocrEngine.Text);
Console.WriteLine(ocrEngine.GetResultAsJson());
```

Chạy chương trình, chỉ định `YOUR_DIRECTORY` tới thư mục chứa `input.jpg` và các tài nguyên Aspose OCR, và bạn sẽ nhận được `output.pdf` ngay bên cạnh.

---

## Kết luận

Bạn giờ đã có một công thức vững chắc, sẵn sàng cho môi trường sản xuất để **tạo PDF có thể tìm kiếm** với Aspose OCR, đồng thời học cách **cải thiện độ chính xác OCR** và **tải hình ảnh cho OCR** đúng cách. Quy trình—GPU (tùy chọn) → lựa chọn ngôn ngữ → tải hình ảnh → chuỗi bộ lọc → nhận dạng → lưu PDF—bao phủ mọi bước quan trọng, vì vậy bạn có thể điều chỉnh nó cho các ngôn ngữ khác, lô lớn hơn, hoặc định dạng đầu ra khác.

Tiếp theo bạn muốn làm gì? Hãy thử thay `PdfSaveOptions` bằng `DocxSaveOptions` để tạo tài liệu Word có thể tìm kiếm, thử nghiệm các bộ lọc bổ sung như `ContrastFilter`, hoặc tích hợp mã này vào một API ASP.NET Core để tạo PDF “on‑the‑fly”. Các khả năng là vô hạn, và với nền tảng đã được xây dựng ở đây, bạn đã sẵn sàng đối mặt với bất kỳ thách thức nào liên quan đến OCR.

Có câu hỏi hoặc gặp khó khăn? Để lại bình luận, chúc bạn lập trình vui!

## Các hướng dẫn liên quan

- [Cách OCR PDF trong .NET với Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Cách trích xuất bảng từ hình ảnh bằng Aspose.OCR cho .NET](/ocr/english/net/text-recognition/recognize-table/)
- [Cách OCR văn bản hình ảnh với ngôn ngữ sử dụng Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}