---
category: general
date: 2026-04-06
description: Cách sử dụng OCR trong C# để trích xuất văn bản thuần từ các hình ảnh
  JPG, bao gồm cả ký tự Cyrillic. Học cách tải hình ảnh cho OCR, nhận dạng văn bản
  JPG và đạt được kết quả đáng tin cậy.
draft: false
keywords:
- how to use OCR
- extract plain text
- extract cyrillic text
- recognize text jpg
- load image for OCR
language: vi
og_description: Cách sử dụng OCR trong C# để trích xuất văn bản thuần từ các tệp JPG.
  Hướng dẫn này chỉ ra cách tải hình ảnh cho OCR, nhận dạng văn bản JPG và xử lý văn
  bản Cyrillic.
og_title: Cách sử dụng OCR trong C# – Trích xuất văn bản thuần từ hình ảnh
tags:
- C#
- OCR
- Aspose
- Image Processing
title: Cách sử dụng OCR trong C# – Trích xuất văn bản thuần từ hình ảnh
url: /vi/net/text-recognition/how-to-use-ocr-in-c-extract-plain-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Sử Dụng OCR trong C# – Trích Xuất Văn Bản Thuần Từ Hình Ảnh

Bạn đã bao giờ tự hỏi **cách sử dụng OCR** trong một dự án .NET mà không phải đấu tranh với các thư viện gốc chưa? Có thể bạn có một thư mục chứa các biên lai đã quét, một vài ảnh chụp màn hình có chú thích Cyrillic, hoặc chỉ cần lấy văn bản ra từ một tệp JPEG để phân tích nhanh. Tin tốt là Aspose OCR biến toàn bộ quá trình này thành chuyện đơn giản.

Trong tutorial này, chúng ta sẽ đi qua một ví dụ hoàn chỉnh, có thể chạy được, cho thấy **cách sử dụng OCR** để **trích xuất văn bản thuần** từ một hình JPEG, cách **tải ảnh cho OCR**, và thậm chí cách **trích xuất văn bản Cyrillic** khi ngôn ngữ nguồn không phải là Latin. Khi kết thúc, bạn sẽ có một ứng dụng console nhỏ in ra văn bản đã nhận dạng trực tiếp trên console—không cần tệp phụ, không có hiệu ứng phụ bí ẩn.

> **Bạn sẽ nhận được**  
> * Hướng dẫn từng bước mà bạn có thể sao chép‑dán vào Visual Studio.  
> * Giải thích *tại sao* mỗi dòng lại quan trọng, không chỉ *làm gì* nó thực hiện.  
> * Mẹo xử lý ảnh lớn, đa ngôn ngữ, và các lỗi thường gặp.

## Yêu cầu trước

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

* .NET 6 SDK hoặc mới hơn (mã cũng hoạt động với .NET Core và .NET Framework).  
* Visual Studio 2022 (hoặc bất kỳ trình soạn thảo nào bạn thích).  
* Kết nối Internet lần đầu chạy mẫu—Aspose OCR sẽ tải các gói ngôn ngữ khi cần.

Nếu bạn chưa có gói NuGet Aspose OCR, chúng ta sẽ hướng dẫn cài đặt trong bước đầu tiên.

## Bước 1 – Cài đặt Aspose OCR qua NuGet (và tại sao lại quan trọng)

Bước **tải ảnh cho OCR** không thể thực hiện cho tới khi thư viện đã có. Sử dụng NuGet đảm bảo bạn nhận được các binary mới nhất, đã được vá bảo mật và tự động kéo các phụ thuộc cần thiết.

```bash
dotnet add package Aspose.OCR
```

*Why this matters*: Aspose OCR cung cấp một DLL lõi rất nhỏ và chỉ tải dữ liệu ngôn ngữ khi bạn yêu cầu. Điều này giúp ứng dụng của bạn nhẹ hơn và tránh việc đóng gói hàng megabyte các tệp ngôn ngữ không dùng tới.

## Bước 2 – Khởi tạo OCR Engine (trái tim của **cách sử dụng OCR**)

Tạo một thể hiện `OcrEngine` là dòng mã thực sự đầu tiên quan trọng cho **cách sử dụng OCR**. Engine mặc định ở chế độ “on‑demand”, nghĩa là nó sẽ tải gói ngôn ngữ lần đầu bạn yêu cầu một ngôn ngữ cụ thể.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Step 2: Create the engine – it will fetch language data when needed.
var ocrEngine = new OcrEngine();
```

> **Pro tip**: Nếu bạn đang làm việc sau một proxy công ty, hãy đặt `OcrEngine.Proxy` trước lần gọi nhận dạng đầu tiên để việc tải xuống thành công.

## Bước 3 – Chọn Ngôn Ngữ – **Trích Xuất Văn Bản Cyrillic** khi cần

Aspose OCR hỗ trợ hàng chục script. Để **trích xuất văn bản Cyrillic**, chỉ cần đặt thuộc tính `Language` thành `OcrLanguage.Cyrillic`. Lần đầu dòng này chạy, mô-đun Cyrillic (≈ 5 MB) sẽ được kéo từ CDN của Aspose.

```csharp
// Step 3: Tell the engine which language to look for.
// This will automatically download the Cyrillic language pack on first use.
ocrEngine.Language = OcrLanguage.Cyrillic;
```

Nếu ảnh của bạn chỉ chứa ký tự Latin, bạn có thể thay `Cyrillic` bằng `English`. Cùng một mẫu áp dụng cho bất kỳ ngôn ngữ nào được hỗ trợ.

## Bước 4 – **Tải Ảnh cho OCR** – Từ Đĩa hoặc Stream

Bây giờ chúng ta thực sự **tải ảnh cho OCR**. Lớp `System.Drawing.Image` xử lý hầu hết các định dạng phổ biến (JPG, PNG, BMP). Nếu bạn đang chạy trên nền tảng không phải Windows, hãy cân nhắc dùng `ImageSharp` thay thế, nhưng với tutorial này kiểu tích hợp sẵn là đủ.

```csharp
using System.Drawing;

// Step 4: Load the picture that holds the text.
using var image = Image.FromFile(@"C:\Images\cyrillic_sample.jpg");
```

> **Why this matters**: Việc tải ảnh trong một khối `using` đảm bảo các tài nguyên GDI+ không quản lý được giải phóng kịp thời, tránh rò rỉ bộ nhớ trong các dịch vụ chạy lâu.

## Bước 5 – **Nhận Dạng Văn Bản JPG** – Chạy Quy Trình OCR

Với engine đã được cấu hình và ảnh đã được tải, cuối cùng chúng ta **nhận dạng văn bản jpg**. Phương thức `Recognize` trả về một `OcrResult` chứa chuỗi văn bản thuần, điểm tin cậy, và thậm chí các hộp bao quanh nếu bạn cần chúng sau này.

```csharp
// Step 5: Perform the recognition.
var ocrResult = ocrEngine.Recognize(image);
```

Nếu muốn tinh chỉnh độ chính xác, bạn có thể điều chỉnh `ocrEngine.Config` (ví dụ, bật `AutoRotate` hoặc đặt `TextOrientation`). Đối với hầu hết các kịch bản đơn giản, các giá trị mặc định hoạt động khá tốt.

## Bước 6 – **Trích Xuất Văn Bản Thuần** – Hiển Thị Kết Quả

Phần cuối cùng của **cách sử dụng OCR** là lấy chuỗi đã nhận dạng từ `ocrResult` và làm gì đó với nó. Ở đây chúng ta chỉ đơn giản ghi ra console, đồng thời minh họa cách **trích xuất văn bản thuần** từ đối tượng kết quả.

```csharp
// Step 6: Output the plain text to the console.
Console.WriteLine("=== Recognized Text ===");
Console.WriteLine(ocrResult.Text);
```

### Kết Quả Dự Kiến

Nếu `cyrillic_sample.jpg` chứa cụm từ “Привет мир” (Hello world), bạn sẽ thấy:

```
=== Recognized Text ===
Привет мир
```

Nếu ảnh mờ hoặc văn bản quá nhỏ, kết quả có thể chứa lỗi; bạn có thể kiểm tra `ocrResult.Confidence` để quyết định có nên thử lại với nguồn ảnh độ phân giải cao hơn không.

## Ví Dụ Đầy Đủ, Sẵn Sàng Chạy

Dưới đây là chương trình hoàn chỉnh. Sao chép vào một dự án Console App mới (`dotnet new console`) và chạy. Không cần tệp phụ nào ngoài ảnh bạn chỉ định.

```csharp
// ---------------------------------------------------------------
// How to Use OCR in C# – Complete Example
// ---------------------------------------------------------------
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // 1️⃣ Install Aspose.OCR via NuGet first (dotnet add package Aspose.OCR)

        // 2️⃣ Initialize the OCR engine – on‑demand language download.
        var ocrEngine = new OcrEngine();

        // 3️⃣ Select Cyrillic to **extract Cyrillic text**.
        ocrEngine.Language = OcrLanguage.Cyrillic;

        // 4️⃣ **Load image for OCR** – change the path to your own file.
        using var image = Image.FromFile(@"YOUR_DIRECTORY\cyrillic_sample.jpg");

        // 5️⃣ **Recognize text jpg** – run the engine.
        var ocrResult = ocrEngine.Recognize(image);

        // 6️⃣ **Extract plain text** – display it.
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

> **Note**: Thay `YOUR_DIRECTORY\cyrillic_sample.jpg` bằng đường dẫn thực tế tới tệp JPEG của bạn.

## Câu Hỏi Thường Gặp & Trường Hợp Đặc Biệt

### Nếu tôi cần **nhận dạng văn bản jpg** từ một stream thay vì tệp thì sao?

Bạn có thể truyền trực tiếp một `MemoryStream`:

```csharp
using var ms = new MemoryStream(File.ReadAllBytes("myImage.jpg"));
using var img = Image.FromStream(ms);
var result = ocrEngine.Recognize(img);
```

### Làm sao xử lý nhiều ngôn ngữ trong cùng một ảnh?

Đặt `ocrEngine.Language` thành `OcrLanguage.Multilingual`. Engine sẽ tự động phát hiện mỗi script, rất hữu ích khi một biên lai kết hợp English và Cyrillic.

```csharp
ocrEngine.Language = OcrLanguage.Multilingual;
```

### Ảnh của tôi quá lớn (hơn 5 MP). Engine có bị treo không?

Ảnh lớn làm tăng mức tiêu thụ bộ nhớ và có thể làm chậm nhận dạng. Việc giảm kích thước nhanh trước khi xử lý giúp:

```csharp
var resized = new Bitmap(image, new Size(image.Width / 2, image.Height / 2));
var result = ocrEngine.Recognize(resized);
```

### Tôi có thể lấy điểm tin cậy cho từng dòng không?

Có—`ocrResult.Lines` chứa `Confidence` cho mỗi dòng. Duyệt qua chúng cho phép bạn lọc các kết quả có độ tin cậy thấp.

```csharp
foreach (var line in ocrResult.Lines)
{
    if (line.Confidence > 0.8)
        Console.WriteLine(line.Text);
}
```

## Mẹo Chuyên Nghiệp cho OCR Sẵn Sàng Sản Xuất

* **Cache các gói ngôn ngữ** – lần tải đầu có thể mất vài giây; lưu các tệp này vào một thư mục cố định và đặt `ocrEngine.LanguageDataPath` để tái sử dụng.  
* **Xử lý hàng loạt** – tái sử dụng một thể hiện `OcrEngine` duy nhất cho nhiều ảnh; tạo engine mới cho mỗi tệp sẽ gây overhead không cần thiết.  
* **Xử lý lỗi** – bao bọc lời gọi `Recognize` trong khối try/catch. Aspose ném `OcrException` cho ảnh hỏng hoặc định dạng không hỗ trợ.  
* **Ghi log** – lưu `ocrResult.Confidence` để sau này có thể kiểm tra các trang cần xem lại thủ công.

## Kết Luận

Chúng ta vừa khám phá **cách sử dụng OCR** trong C# để **trích xuất văn bản thuần** từ một JPEG, trình bày các bước **tải ảnh cho OCR**, chỉ ra cách **nhận dạng văn bản jpg**, và thậm chí đã lấy **văn bản Cyrillic** ra khỏi ảnh. Mẫu này hoàn toàn hoạt động, chỉ yêu cầu một gói NuGet duy nhất, và có thể mở rộng để xử lý tài liệu đa ngôn ngữ, công việc batch, hoặc kịch bản quét thời gian thực.

Sẵn sàng cho thử thách tiếp theo? Hãy thử thay ngôn ngữ Cyrillic bằng Arabic, khám phá cờ `AutoRotate`, hoặc tích hợp kết quả vào một chỉ mục tìm kiếm. Khả năng là vô hạn

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}