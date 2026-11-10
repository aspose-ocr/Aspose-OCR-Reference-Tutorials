---
category: general
date: 2026-04-04
description: Cách sử dụng OCR nhanh chóng và an toàn. Học cách trích xuất văn bản
  từ hình ảnh, chuyển đổi DJVU sang văn bản và tải hình ảnh cho OCR bằng Aspose.OCR.
draft: false
keywords:
- how to use OCR
- extract text from image
- convert djvu to text
- load image for OCR
- extract text from djvu
language: vi
og_description: Cách sử dụng OCR trong C# để trích xuất văn bản từ các tệp hình ảnh
  và tài liệu DJVU. Hướng dẫn từng bước kèm mã nguồn đầy đủ.
og_title: Cách sử dụng OCR trong C# – Hướng dẫn đầy đủ
tags:
- OCR
- C#
- Aspose
title: Cách sử dụng OCR trong C# – Trích xuất văn bản từ hình ảnh và tệp DJVU
url: /vi/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-images-and-djvu-files/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Sử Dụng OCR trong C# – Trích Xuất Văn Bản từ Hình Ảnh và Tệp DJVU

Bạn đã bao giờ tự hỏi **cách sử dụng OCR** để lấy các từ ra khỏi một trang đã quét mà không cần gõ tay chưa? Bạn không phải là người duy nhất. Trong nhiều dự án—cho dù bạn đang số hoá sách cũ hay trích xuất dữ liệu từ biên lai—việc lấy văn bản từ hình ảnh là một vấn đề thường gặp. Tin tốt là gì? Với Aspose.OCR, bạn có thể thực hiện điều này chỉ trong vài dòng mã, ngay cả khi nguồn là tệp DJVU.

Trong hướng dẫn này, chúng ta sẽ đi qua mọi thứ bạn cần để **trích xuất văn bản từ hình ảnh**, **tải hình ảnh cho OCR**, và thậm chí **chuyển đổi DJVU sang văn bản** bằng C#. Khi kết thúc, bạn sẽ có một ứng dụng console sẵn sàng chạy, in ra văn bản đã nhận dạng trực tiếp trên console. Không có bí ẩn, không có phụ thuộc thêm, chỉ C# thuần và Aspose.

## Những Điều Bạn Sẽ Học

- Cách cài đặt và tham chiếu thư viện Aspose.OCR.
- Mã chính xác để **tải hình ảnh cho OCR**, bất kể đó là PNG, JPEG hay một trang DJVU.
- Cách gọi engine và lấy kết quả.
- Mẹo xử lý tài liệu lớn và các lỗi thường gặp.
- Một ví dụ hoàn chỉnh, có thể chạy được mà bạn có thể sao chép‑dán vào Visual Studio.

> **Prerequisite:** .NET 6.0 trở lên và một giấy phép Aspose.OCR hợp lệ (hoặc bản dùng thử miễn phí). Nếu bạn chưa có thư viện, tải nó từ NuGet bằng `dotnet add package Aspose.OCR`.

---

## Cách Sử Dụng OCR với Aspose trong C#

Đây là bước cốt lõi nơi chúng ta thực sự trả lời câu hỏi **cách sử dụng OCR** trong một dự án C#. Đoạn mã dưới đây là một chương trình đầy đủ; bạn có thể đặt nó vào một ứng dụng console mới và nhấn F5.

```csharp
using System;
using Aspose.OCR;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create the OCR engine instance.
            var ocrEngine = new OcrEngine();

            // Step 2: Load the image (or DJVU page) you want to analyze.
            // Replace the path with your own file location.
            ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/book-page.djvu");

            // Step 3: Run the recognition process.
            OcrResult ocrResult = ocrEngine.Recognize();

            // Step 4: Output the extracted text.
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

**Tại sao cách này hoạt động:**  
- `OcrEngine` là điểm vào; nó trừu tượng hoá việc tiền xử lý ảnh, phát hiện ngôn ngữ và phân loại ký tự.  
- `ImageStream.FromFile` có thể xử lý nhiều định dạng, bao gồm DJVU, nghĩa là bạn có thể **chuyển đổi DJVU sang văn bản** mà không cần bước chuyển đổi riêng.  
- `Recognize()` trả về một đối tượng `OcrResult` chứa đầu ra văn bản thuần, điểm tin cậy, và thậm chí các hộp bao quanh nếu bạn cần chúng sau này.

Chạy chương trình sẽ in ra một thứ gì đó như:

```
=== OCR Result ===
In the beginning God created the heavens and the earth.
```

Đó là tất cả—hoạt động **trích xuất văn bản từ DJVU** đầu tiên của bạn đã thành công.

![how to use OCR example](/images/ocr-demo.png "Screenshot showing how to use OCR in a C# console app")

*Alt text: “cách sử dụng OCR” ảnh chụp màn hình đầu ra console.*

---

## Tải Hình Ảnh cho OCR

Trước khi engine có thể đọc bất kỳ thứ gì, bạn phải **tải hình ảnh cho OCR** một cách chính xác. Aspose hỗ trợ hầu hết các định dạng raster ngay từ đầu, nhưng một vài mẹo có thể làm cho việc nhận dạng mượt mà hơn:

- **Thay đổi kích thước ảnh lớn** xuống tối đa 2000 px ở cạnh dài nhất. Các tệp quá lớn tăng mức sử dụng bộ nhớ và có thể làm chậm engine.  
- **Chuyển ảnh màu sang thang xám** nếu bạn thấy nền nhiễu. Dùng `ocrEngine.Image = ImageStream.FromFile(path).ConvertToGrayscale();`.  
- **Đặt DPI thủ công** cho các bản quét độ phân giải thấp (`ocrEngine.Image.DpiX = 300; ocrEngine.Image.DpiY = 300;`).

Những điều chỉnh này là tùy chọn nhưng thường cải thiện độ chính xác khi bạn **trích xuất văn bản từ hình ảnh** như các biên lai đã quét.

---

## Trích Xuất Văn Bản từ Hình Ảnh – Các Thực Hành Tốt Nhất

Khi bạn làm việc với các định dạng ảnh thông thường (PNG, JPEG, BMP), các bước vẫn giống nhau, nhưng bạn có thể tinh chỉnh engine:

```csharp
ocrEngine.Image = ImageStream.FromFile("sample.png");

// Optional: enable language packs for better accuracy.
ocrEngine.Language = Language.English;

// Optional: set recognition mode to auto.
ocrEngine.RecognitionMode = RecognitionMode.Auto;
```

- **Lựa chọn ngôn ngữ** quan trọng. Nếu bạn xử lý tài liệu đa ngôn ngữ, đặt `ocrEngine.Language = Language.Multilingual;`.  
- **RecognitionMode** có thể là `Auto`, `Fast`, hoặc `Accurate`. `Accurate` cho chất lượng cao hơn nhưng chậm hơn—dùng nó cho các nhiệm vụ lưu trữ.

---

## Chuyển Đổi DJVU sang Văn Bản – Xử Lý Tệp Đa Trang

Các tệp DJVU thường chứa nhiều trang. Aspose xem mỗi trang như một luồng ảnh riêng, vì vậy bạn có thể lặp qua chúng:

```csharp
using Aspose.OCR;
using System.Collections.Generic;

var ocrEngine = new OcrEngine();
List<string> allPagesText = new List<string>();

int pageCount = ImageStream.GetPageCount("book.djvu");
for (int i = 1; i <= pageCount; i++)
{
    ocrEngine.Image = ImageStream.FromFile("book.djvu", i); // Load page i
    OcrResult result = ocrEngine.Recognize();
    allPagesText.Add(result.Text);
}

// Combine all pages into a single string.
string fullText = string.Join("\n--- Page Break ---\n", allPagesText);
Console.WriteLine(fullText);
```

**Tại sao phải lặp?**  
Các tệp DJVU thực chất là một chồng các ảnh. Bằng cách duyệt từng trang, bạn **trích xuất văn bản từ DJVU** theo thứ tự, giữ nguyên luồng tài liệu gốc.

---

## Các Vấn Đề Thường Gặp và Mẹo Chuyên Nghiệp

| Vấn đề | Nguyên nhân | Cách khắc phục |
|------|----------------|-----|
| **Ký tự rác** | DPI thấp hoặc nén mạnh | Tăng kích thước ảnh, đặt `ocrEngine.Image.DpiX/Y = 300` |
| **Xử lý chậm** | Sử dụng chế độ `Accurate` trên các tệp lớn | Chuyển sang chế độ `Fast` cho các công việc hàng loạt |
| **Thiếu hỗ trợ ngôn ngữ** | Ngôn ngữ mặc định chỉ tiếng Anh | Tải các gói ngôn ngữ bổ sung (`ocrEngine.Language = Language.Spanish;`) |
| **Lỗi hết bộ nhớ** | Tải nhiều trang độ phân giải cao cùng lúc | Xử lý từng trang một và giải phóng tài nguyên (`ocrEngine.Dispose();`) |

Một **mẹo chuyên nghiệp** nhanh: luôn gọi `ocrEngine.Dispose()` sau khi bạn hoàn thành một trang. Điều này giải phóng tài nguyên gốc và ngăn ngừa các rò rỉ bộ nhớ tiềm ẩn có thể làm sập các dịch vụ chạy lâu.

---

## Kiểm Tra Quy Trình OCR Của Bạn

Để xác minh mọi thứ hoạt động, hãy thử các kiểm tra đơn giản sau:

1. **In độ dài** của chuỗi đã nhận dạng: `Console.WriteLine($"Characters recognized: {ocrResult.Text.Length}");`  
2. **So sánh với văn bản đã biết** bằng một thư viện diff đơn giản nếu bạn có dữ liệu chuẩn.  
3. **Ghi lại điểm tin cậy** (`ocrResult.Confidence`) để tự động phát hiện các trang chất lượng thấp.

Nếu điểm tin cậy liên tục dưới 0.7, hãy xem lại các bước tiền xử lý ảnh đã đề cập ở trên.

---

## Các Bước Tiếp Theo

Bây giờ bạn đã biết **cách sử dụng OCR**, hãy cân nhắc mở rộng quy trình làm việc:

- **Xử lý hàng loạt**: Bao bọc vòng lặp trong một `Parallel.ForEach` để tăng tốc cho bộ sưu tập lớn.  
- **Xuất ra PDF**: Dùng Aspose.PDF để nhúng văn bản đã nhận dạng dưới dạng lớp ẩn, tạo PDF có thể tìm kiếm.  
- **Tích hợp với AI**: Đưa các chuỗi đã trích xuất vào mô hình ngôn ngữ để tóm tắt hoặc trích xuất thực thể.

Tất cả những điều này dựa trên nền tảng bạn vừa thiết lập, và mỗi bước đều hưởng lợi từ các nguyên tắc **trích xuất văn bản từ hình ảnh** mà chúng ta đã đề cập.

---

## Kết Luận

Chúng ta đã đi sâu vào **cách sử dụng OCR** trong C# với Aspose, bao gồm mọi thứ từ tải ảnh, **trích xuất văn bản từ ảnh**, xử lý các tệp **DJVU**, và khắc phục các lỗi thường gặp. Ví dụ hoàn chỉnh, có thể chạy được ở trên cung cấp cho bạn một điểm khởi đầu vững chắc, và các mẹo rải rác trong bài sẽ giúp bạn điều chỉnh giải pháp cho các dự án thực tế.

Hãy thử ngay, tinh chỉnh các cài đặt cho tài liệu của bạn, và bạn sẽ biến các trang đã quét thành văn bản có thể tìm kiếm trong chớp mắt. Có câu hỏi hay tệp khó chịu không hợp? Để lại bình luận—chúc bạn lập trình vui vẻ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}