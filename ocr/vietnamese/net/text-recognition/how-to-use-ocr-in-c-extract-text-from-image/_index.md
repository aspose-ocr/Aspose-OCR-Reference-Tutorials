---
category: general
date: 2026-03-05
description: Cách sử dụng OCR trong C# để trích xuất văn bản từ hình ảnh. Học cách
  chuyển đổi hình ảnh thành văn bản, đọc ký tự Hàn Quốc và tải hình ảnh cho OCR nhanh
  chóng.
draft: false
keywords:
- how to use OCR
- extract text from image
- convert image to text
- read korean characters
- load image for OCR
language: vi
og_description: Cách sử dụng OCR trong C# và ngay lập tức trích xuất văn bản từ hình
  ảnh. Hướng dẫn này chỉ cách chuyển đổi hình ảnh thành văn bản, đọc ký tự tiếng Hàn
  và tải hình ảnh cho OCR.
og_title: Cách sử dụng OCR trong C# – Trích xuất văn bản từ hình ảnh
tags:
- OCR
- C#
- Aspose
title: Cách sử dụng OCR trong C# – Trích xuất văn bản từ hình ảnh
url: /vi/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Sử Dụng OCR trong C# – Trích Xuất Văn Bản Từ Hình Ảnh

Bạn đã bao giờ tự hỏi **cách sử dụng OCR** khi có một ảnh chụp màn hình đầy văn bản tiếng Hàn và bạn cần chuỗi ký tự thuần không? Bạn không phải là người duy nhất bối rối về vấn đề này. Trong hướng dẫn này, chúng tôi sẽ đi qua một ví dụ hoàn chỉnh, sẵn sàng chạy mà **trích xuất văn bản từ hình ảnh**, **chuyển đổi hình ảnh thành văn bản**, và thậm chí cho bạn thấy cách **đọc ký tự tiếng Hàn** với Aspose.OCR.

Chúng tôi cũng sẽ đề cập đến bước thường bị bỏ qua là **tải hình ảnh cho OCR** để bạn không gặp lỗi “file không tìm thấy” sau này. Khi kết thúc, bạn sẽ có một chương trình tự chứa mà bạn có thể chèn vào bất kỳ dự án .NET nào.

## Những Gì Bạn Cần

- .NET 6+ (hoặc .NET Framework 4.7.2 trở lên) – mã chạy trên cả hai.  
- Aspose.OCR cho .NET – bạn có thể tải bản dùng thử miễn phí từ trang web Aspose.  
- Một hình mẫu (`korean_doc.png`) chứa văn bản tiếng Hàn.  
- IDE yêu thích của bạn (Visual Studio, Rider, VS Code – bất kỳ cái nào bạn thích).  

Không cần thư viện bên thứ ba nào khác.

## Bước 1: Thiết Lập Dự Án và Thêm Aspose.OCR

Đầu tiên, tạo một ứng dụng console mới:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

Sau đó thêm gói NuGet Aspose.OCR:

```bash
dotnet add package Aspose.OCR
```

> **Mẹo chuyên nghiệp:** Nếu bạn có tệp giấy phép, đặt nó ở thư mục gốc của dự án; nếu không, bản dùng thử miễn phí sẽ hoạt động nhưng sẽ thêm một watermark vào kết quả.

## Bước 2: Cách Sử Dụng OCR – Khởi Tạo Engine

Bây giờ chúng ta sẽ viết mã C#. Điều đầu tiên cần làm khi **cách sử dụng OCR** là khởi tạo `OcrEngine`. Đối tượng này là trái tim của thư viện; nó chứa tất cả các cài đặt bạn sẽ cần sau này.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // Optional: apply your license to remove trial limitations
            // Replace the path with the actual location of your .lic file
            ocrEngine.SetLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

**Tại sao điều này quan trọng:** Nếu không có một thể hiện engine đúng, bạn không thể đặt ngôn ngữ, tải hình ảnh, hoặc lấy kết quả. Engine cũng quản lý tài nguyên nội bộ, vì vậy tạo một lần và tái sử dụng sẽ hiệu quả hơn so với việc liên tục tạo đối tượng mới.

## Bước 3: Chọn Ngôn Ngữ – Đọc Ký Tự Tiếng Hàn

Dòng tiếp theo cho engine biết ngôn ngữ cần tìm. Vì mục tiêu của chúng ta là **đọc ký tự tiếng Hàn**, chúng ta đặt `OcrLanguage.Korean`. Bạn có thể thay thế bằng Arabic, Thai, Gujarati, v.v., tùy vào trường hợp sử dụng.

```csharp
            // Step 3: Tell the engine which language to recognize
            ocrEngine.Language = OcrLanguage.Korean; // alternatives: Arabic, Thai, Gujarati, etc.
```

**Tại sao nó quan trọng:** Việc chọn ngôn ngữ cải thiện độ chính xác đáng kể. Engine OCR sử dụng từ điển và mô hình ký tự riêng cho từng ngôn ngữ; cung cấp ngôn ngữ sai có thể tạo ra đầu ra rối rắm.

## Bước 4: Tải Hình Ảnh cho OCR – Chuyển Đổi Hình Ảnh Thành Văn Bản

Trước khi engine có thể thực hiện bất kỳ công việc nào, bạn cần **tải hình ảnh cho OCR**. Phương thức `ImageStream.FromFile` đọc tệp vào định dạng mà engine hiểu.

```csharp
            // Step 4: Load the image that contains the text
            ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/korean_doc.png");
```

Nếu hình ảnh nằm trong thư mục khác, chỉ cần điều chỉnh đường dẫn. Nhớ đặt *Build Action* của tệp thành “Copy if newer” để tệp thực thi có thể tìm thấy nó khi chạy.

> **Cạm bẫy thường gặp:** Cung cấp đường dẫn có dấu gạch chéo ngược (`\`) trong một literal string mà không escape sẽ gây lỗi biên dịch. Hãy sử dụng hoặc dấu gạch chéo ngược kép (`\\`) hoặc chuỗi verbatim (`@\"C:\\path\\file.png\"`).

## Bước 5: Thực Hiện OCR – Trích Xuất Văn Bản Từ Hình Ảnh

Bây giờ công việc nặng sẽ diễn ra. Gọi `Recognize()` chạy thuật toán OCR, và thuộc tính `Text` cung cấp cho bạn chuỗi thô.

```csharp
            // Step 5: Run OCR and get the recognized text
            string recognizedText = ocrEngine.Recognize().Text;
```

Ở thời điểm này, bạn đã **trích xuất văn bản từ hình ảnh** và thực sự **chuyển đổi hình ảnh thành văn bản**. Kết quả có thể chứa ký tự xuống dòng nếu bố cục gốc có ngắt dòng.

## Bước 6: Hiển Thị Kết Quả – Xác Minh Đầu Ra

Cuối cùng, hãy in kết quả ra console để bạn có thể xác minh nó đã hoạt động.

```csharp
            // Step 6: Output the result to the console
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(recognizedText);
        }
    }
}
```

Chạy chương trình:

```bash
dotnet run
```

### Kết Quả Dự Kiến

```
=== Recognized Text ===
안녕하세요. 이것은 OCR 테스트 문서입니다.
```

Nếu bạn thấy các ký tự tiếng Hàn giống như trong hình ảnh, chúc mừng—bạn đã thành thạo **cách sử dụng OCR** với Aspose.OCR!

![sơ đồ ví dụ cách sử dụng OCR](image.png)

*Văn bản thay thế hình ảnh: sơ đồ ví dụ cách sử dụng OCR mô tả luồng từ tải hình ảnh đến in ra văn bản đã nhận dạng.*

## Các Trường Hợp Cạnh & Biến Thể

### 1. Xử Lý Nhiều Trang

Nếu bạn cần **trích xuất văn bản từ hình ảnh** có chứa nhiều trang (ví dụ, TIFF đa trang), hãy lặp qua mỗi trang và gọi `Recognize()` cho mỗi thể hiện `ImageStream`.

### 2. Xử Lý Ảnh Quét Chất Lượng Thấp

Hình ảnh độ phân giải thấp có thể làm giảm độ chính xác. Trước khi gọi `Recognize()`, bạn có thể cải thiện hình ảnh bằng công cụ tiền xử lý của Aspose:

```csharp
ocrEngine.Image = ImageProcessing.Preprocess(ocrEngine.Image, ImageProcessingOptions.Deskew);
```

### 3. Thay Đổi Ngôn Ngữ Khi Chạy

Giả sử bạn có một tài liệu hỗn hợp ngôn ngữ. Bạn có thể thay đổi `ocrEngine.Language` giữa các lần nhận dạng:

```csharp
ocrEngine.Language = OcrLanguage.English;
string english = ocrEngine.Recognize().Text;

ocrEngine.Language = OcrLanguage.Korean;
string korean = ocrEngine.Recognize().Text;
```

### 4. Lưu Kết Quả Vào Tệp

Nếu bạn muốn **chuyển đổi hình ảnh thành văn bản** và lưu lại, chỉ cần ghi chuỗi vào tệp `.txt`:

```csharp
System.IO.File.WriteAllText("output.txt", recognizedText);
```

## Câu Hỏi Thường Gặp

- **Tôi có cần giấy phép để chạy đoạn mã này không?**  
  Không. Bản dùng thử miễn phí hoạt động tốt cho việc thử nghiệm, nhưng nó sẽ thêm một watermark vào kết quả. Giấy phép mua sẽ loại bỏ watermark và mở khóa hiệu năng đầy đủ.

- **Tôi có thể sử dụng điều này trên Linux không?**  
  Chắc chắn. Aspose.OCR là đa nền tảng; chỉ cần đảm bảo bạn có các phụ thuộc gốc cần thiết (libgdiplus cho .NET Core trên Linux).

- **Nếu hình ảnh của tôi ở dạng stream thay vì tệp thì sao?**  
  Sử dụng `ImageStream.FromStream(yourStream)` – API chấp nhận bất kỳ `System.IO.Stream` nào.

## Kết Luận

Chúng tôi đã hướng dẫn bạn từng bước **cách sử dụng OCR** trong C# để **trích xuất văn bản từ hình ảnh**, **chuyển đổi hình ảnh thành văn bản**, và **đọc ký tự tiếng Hàn** đồng thời **tải hình ảnh cho OCR** một cách đúng đắn. Ví dụ hoàn chỉnh, có thể chạy được ở trên sẽ hoạt động ngay lập tức, và các mẹo bổ sung cung cấp cho bạn lộ trình cho các kịch bản nâng cao hơn.

Sẵn sàng cho thử thách tiếp theo? Hãy thử thay đổi ngôn ngữ, xử lý PDF trang theo trang, hoặc tích hợp lời gọi OCR vào một API web để người dùng có thể tải lên hình ảnh và nhận kết quả văn bản ngay lập tức. Các khả năng là vô hạn, và giờ bạn đã có nền tảng vững chắc để xây dựng.

Chúc lập trình vui vẻ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}