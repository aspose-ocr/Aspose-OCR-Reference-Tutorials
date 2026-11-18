---
category: general
date: 2026-05-25
description: Cách sử dụng OCR trong C# để trích xuất văn bản từ các tệp hình ảnh.
  Học cách nhận dạng ký tự Trung Quốc từ file JPG bằng Aspose.OCR trong vài bước đơn
  giản.
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from jpg
- recognize chinese characters
- ocr chinese simplified
language: vi
og_description: Cách sử dụng OCR trong C# để trích xuất văn bản từ các tệp hình ảnh.
  Hướng dẫn này chỉ cho bạn cách nhận dạng ký tự tiếng Trung từ một tệp JPG bằng Aspose.OCR.
og_title: Cách sử dụng OCR trong C# – Nhận dạng văn bản tiếng Trung từ JPG
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: How to use OCR in C# to extract text from image files. Learn to recognize
    Chinese characters from a JPG using Aspose.OCR in a few simple steps.
  headline: How to Use OCR in C# – Recognize Chinese Text from JPG
  type: TechArticle
- description: How to use OCR in C# to extract text from image files. Learn to recognize
    Chinese characters from a JPG using Aspose.OCR in a few simple steps.
  name: How to Use OCR in C# – Recognize Chinese Text from JPG
  steps:
  - name: What’s happening under the hood?
    text: '- **`OcrEngine.Language`** tells Aspose which dictionary to use. By picking
      `ChineseSimplified`, we instruct the engine to look for the Simplified Chinese
      language pack. - **First‑time download**: When `Recognize` runs, the SDK reaches
      out to Aspose’s CDN, pulls the ≈6 MB language file, caches it lo'
  - name: 5.1 Dealing with Low‑Quality Images
    text: 'OCR accuracy drops when the source image is blurry, noisy, or has poor
      lighting. A quick fix is to pre‑process the image:'
  - name: 5.2 Running in a Headless Environment
    text: 'If you’re deploying to a Linux container without a GUI, make sure the `libgdiplus`
      library (required for `System.Drawing`) is installed:'
  - name: 5.3 Caching the Language Pack Manually
    text: You can download the language file once and point Aspose to it via the `License`
      API, which eliminates the one‑time network call. This is handy for offline scenarios.
  - name: Expected Output
    text: 'If the JPG contains the phrase “欢迎光临”, the console will print:'
  type: HowTo
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Cách sử dụng OCR trong C# – Nhận dạng văn bản tiếng Trung từ JPG
url: /vi/net/text-recognition/how-to-use-ocr-in-c-recognize-chinese-text-from-jpg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách sử dụng OCR trong C# – Nhận dạng văn bản tiếng Trung từ JPG

Bạn đã bao giờ tự hỏi **cách sử dụng OCR** để lấy các từ ra khỏi một bức ảnh bạn chụp bằng điện thoại chưa? Bạn không phải là người duy nhất. Trong nhiều dự án thực tế—như máy quét biên lai, ứng dụng dịch thuật, hoặc nhập dữ liệu tự động—bạn sẽ cần **trích xuất văn bản từ hình ảnh** một cách nhanh chóng và đáng tin cậy.

Trong hướng dẫn này, chúng ta sẽ đi qua một ví dụ đầy đủ, có thể chạy được mà **nhận dạng văn bản từ các tệp JPG** và thậm chí xử lý trường hợp khó khăn của **nhận dạng ký tự tiếng Trung** bằng cách sử dụng gói ngôn ngữ **OCR Chinese Simplified**. Khi kết thúc, bạn sẽ có một ứng dụng console tự chứa, in chuỗi đã phát hiện ra trên console, mà không cần tải xuống thủ công nào thêm.

> **Lưu ý nhanh:** Mã này hoạt động với Aspose.OCR ≥ 23.7, tự động tải về tài nguyên ngôn ngữ khi sử dụng lần đầu. Nếu bạn đang dùng phiên bản cũ hơn, bạn sẽ cần thêm ngôn ngữ một cách thủ công.

## Yêu cầu trước

- .NET 6.0 SDK hoặc phiên bản mới hơn (ví dụ này nhắm tới .NET 6, nhưng .NET 5 cũng hoạt động được)
- Phiên bản mới nhất của Visual Studio 2022 hoặc VS Code với phần mở rộng C#
- Kết nối internet để tải ngôn ngữ lần đầu
- Một hình ảnh JPG chứa văn bản tiếng Trung giản thể (chúng tôi sẽ gọi nó là `chinese_sign.jpg`)

Chỉ vậy thôi—không cần các engine OCR nặng, không cần xử lý DLL gốc. Chỉ cần một vài lệnh NuGet và một vài dòng mã.

## Bước 1: Cài đặt Aspose.OCR qua NuGet

Đầu tiên, chúng ta cần thư viện OCR. Mở terminal trong thư mục dự án và chạy:

```bash
dotnet add package Aspose.OCR
```

Hoặc, nếu bạn thích giao diện Visual Studio, nhấp chuột phải vào **Dependencies → Manage NuGet Packages**, tìm “Aspose.OCR”, và nhấn **Install**.

> **Mẹo chuyên nghiệp:** Giữ các gói của bạn luôn cập nhật. Các gói ngôn ngữ mới và cải tiến hiệu năng luôn xuất hiện trong mỗi bản phát hành phụ.

## Bước 2: Tạo dự án Console mới (Nếu bạn chưa có)

Nếu bạn bắt đầu từ đầu, tạo một ứng dụng console mới:

```bash
dotnet new console -n OcrChineseDemo
cd OcrChineseDemo
```

Bây giờ bạn đã có tệp `Program.cs` sẵn sàng cho mã OCR.

## Bước 3: Viết mã OCR – Nhận dạng tiếng Trung giản thể từ JPG

Mở `Program.cs` và thay thế nội dung của nó bằng đoạn sau. Mỗi dòng đều có chú thích để bạn thấy *tại sao* chúng ta thực hiện từng bước, không chỉ *cái gì* chúng ta đang làm.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;   // Required for Image.FromFile

namespace OcrChineseDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // --------------------------------------------------------------
            // 1️⃣  Initialise the OCR engine and request the Simplified Chinese
            //     language. This language isn’t bundled in the core package,
            //     so Aspose.OCR will download it the first time you call
            //     Recognize().
            // --------------------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                // The enum value maps to the language pack name.
                Language = OcrLanguage.ChineseSimplified
            };

            // --------------------------------------------------------------
            // 2️⃣  Load the image you want to process. Replace the path with
            //     the actual location of your JPG file.
            // --------------------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY/chinese_sign.jpg";
            using var image = Image.FromFile(imagePath);

            // --------------------------------------------------------------
            // 3️⃣  Perform the recognition. The first call may take a few
            //     seconds because the language resources are being fetched.
            // --------------------------------------------------------------
            string recognizedText = ocrEngine.Recognize(image);

            // --------------------------------------------------------------
            // 4️⃣  Output the result to the console.
            // --------------------------------------------------------------
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(recognizedText);
        }
    }
}
```

### Điều gì đang diễn ra phía sau?

- **`OcrEngine.Language`** cho Aspose biết từ điển nào sẽ được sử dụng. Bằng cách chọn `ChineseSimplified`, chúng ta chỉ định engine tìm gói ngôn ngữ tiếng Trung giản thể.
- **Tải xuống lần đầu**: Khi `Recognize` chạy, SDK sẽ liên hệ tới CDN của Aspose, tải về tệp ngôn ngữ ≈6 MB, lưu vào bộ nhớ cache cục bộ, và sau đó thực hiện OCR. Các lần gọi sau đều tức thì.
- **`Image.FromFile`** hoạt động với bất kỳ định dạng raster nào mà .NET có thể giải mã—JPG, PNG, BMP—do đó bạn có thể **trích xuất văn bản từ hình ảnh** của nhiều loại, không chỉ JPG.

## Bước 4: Chạy ứng dụng và kiểm tra đầu ra

Biên dịch và chạy:

```bash
dotnet run
```

Bạn sẽ thấy một cái gì đó giống như:

```
=== Recognized Text ===
欢迎光临
```

Nếu console in ra ký tự rác hoặc chuỗi trống, hãy kiểm tra lại rằng:

1. Hình ảnh thực sự chứa các ký tự tiếng Trung rõ ràng, độ tương phản cao.
2. Đường dẫn tệp đúng (không có khoảng trắng thừa hoặc thiếu phần mở rộng).
3. Máy của bạn có thể truy cập `https://download.aspose.com` để tải gói ngôn ngữ.

## Bước 5: Xử lý các trường hợp đặc biệt và những khó khăn thường gặp

### 5.1 Xử lý hình ảnh chất lượng thấp

Độ chính xác của OCR giảm khi hình ảnh nguồn bị mờ, nhiễu, hoặc ánh sáng kém. Một cách khắc phục nhanh là tiền xử lý hình ảnh:

```csharp
using System.Drawing.Imaging;

// Convert to grayscale
var gray = new Bitmap(image.Width, image.Height);
using (var g = Graphics.FromImage(gray))
{
    var colorMatrix = new ColorMatrix(
        new float[][]{
            new float[]{0.3f,0.3f,0.3f,0,0},
            new float[]{0.59f,0.59f,0.59f,0,0},
            new float[]{0.11f,0.11f,0.11f,0,0},
            new float[]{0,0,0,1,0},
            new float[]{0,0,0,0,1}
        });
    var attributes = new ImageAttributes();
    attributes.SetColorMatrix(colorMatrix);
    g.DrawImage(image, new Rectangle(0,0,image.Width,image.Height),
                0,0,image.Width,image.Height, GraphicsUnit.Pixel, attributes);
}

// Use the processed bitmap for OCR
string recognizedText = ocrEngine.Recognize(gray);
```

### 5.2 Chạy trong môi trường không giao diện (headless)

Nếu bạn triển khai vào container Linux không có GUI, hãy chắc chắn rằng thư viện `libgdiplus` (cần cho `System.Drawing`) đã được cài đặt:

```bash
apt-get update && apt-get install -y libgdiplus
```

### 5.3 Lưu cache gói ngôn ngữ thủ công

Bạn có thể tải tệp ngôn ngữ một lần và chỉ định cho Aspose thông qua API `License`, điều này loại bỏ lần gọi mạng duy nhất. Thực tế hữu ích cho các kịch bản offline.

```csharp
// Assuming you have the .dat file downloaded to /opt/ocr/langs/
ocrEngine.SetLicense("Aspose.OCR.lic"); // optional if you have a paid license
ocrEngine.LoadLanguage(@" /opt/ocr/langs/ChineseSimplified.dat");
```

## Ví dụ hoàn chỉnh (Tất cả trong một)

Dưới đây là chương trình *đầy đủ* mà bạn có thể sao chép và dán vào `Program.cs`. Không có đoạn mã ẩn, không có script bên ngoài.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;

namespace OcrChineseDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialise OCR engine with Simplified Chinese language
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.ChineseSimplified
            };

            // Path to the JPG image containing Chinese text
            string imagePath = @"YOUR_DIRECTORY/chinese_sign.jpg";

            // Load the image (ensure the file exists)
            using var image = Image.FromFile(imagePath);

            // Recognize text – first call may download the language pack
            string recognizedText = ocrEngine.Recognize(image);

            // Display the result
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(recognizedText);
        }
    }
}
```

### Đầu ra dự kiến

Nếu JPG chứa cụm từ “欢迎光临”, console sẽ in ra:

```
=== Recognized Text ===
欢迎光临
```

Bạn có thể thay thế hình ảnh bằng bất kỳ biển hiệu tiếng Trung giản thể nào khác, tên đường, hoặc nhãn sản phẩm—engine sẽ cố gắng hết sức.

## Kết luận

Chúng ta vừa mới tìm hiểu **cách sử dụng OCR** trong C# để **trích xuất văn bản từ hình ảnh**; đặc biệt là giải quyết thách thức **nhận dạng ký tự tiếng Trung** trong một **JPG**. Bằng cách tận dụng việc tải ngôn ngữ ngay lập tức của Aspose.OCR, bạn có thể giữ cho việc triển khai nhẹ nhàng trong khi vẫn hỗ trợ **OCR Chinese Simplified** ngay từ đầu.

Tiếp theo là gì? Hãy thử các ý tưởng sau:

- **Xử lý hàng loạt**: Duyệt qua một thư mục các hình ảnh và ghi mỗi kết quả vào file CSV.
- **Kết hợp với API dịch thuật**: Đưa chuỗi đã nhận dạng vào Azure Translator để tạo ứng dụng đa ngôn ngữ thời gian thực.
- **Khám phá các ngôn ngữ khác**: Thay `OcrLanguage.ChineseSimplified` bằng `Japanese` hoặc `Arabic` và xem cách mã tương tự thích nghi.

Có câu hỏi về tối ưu hiệu năng, giấy phép, hoặc tích hợp OCR vào dịch vụ web? Hãy để lại bình luận bên dưới—chúc lập trình vui!

---

![Ảnh chụp màn hình đầu ra console cho thấy cách sử dụng OCR trong C# để nhận dạng văn bản tiếng Trung từ ảnh JPG](ocr-chinese-demo.png "cách sử dụng OCR đầu ra console")

## Các hướng dẫn liên quan

- [Trích xuất văn bản hình ảnh C# với lựa chọn ngôn ngữ bằng Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Nhận dạng văn bản hình ảnh với Aspose OCR cho nhiều ngôn ngữ](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [Cách trích xuất văn bản từ hình ảnh bằng cách chuẩn bị các hình chữ nhật trong OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}