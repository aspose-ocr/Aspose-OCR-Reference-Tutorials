---
category: general
date: 2026-01-10
description: Cách chạy OCR nhanh chóng và trích xuất văn bản tiếng Ả Rập từ hình ảnh.
  Học cách chuyển đổi hình ảnh thành văn bản, đọc văn bản từ PNG và xem cách trích
  xuất văn bản bằng Aspose OCR.
draft: false
keywords:
- how to run OCR
- extract arabic text
- convert image to text
- read text from png
- how to extract text
language: vi
og_description: Cách chạy OCR trong C# và trích xuất văn bản tiếng Ả Rập từ hình ảnh
  PNG. Hướng dẫn này cho bạn biết cách chuyển đổi hình ảnh thành văn bản và đọc văn
  bản từ PNG từng bước.
og_title: Cách chạy OCR trong C# – Trích xuất văn bản tiếng Ả Rập từ PNG
tags:
- OCR
- C#
- Aspose
title: Cách chạy OCR trong C# – Trích xuất văn bản tiếng Ả Rập từ PNG
url: /vi/net/text-recognition/how-to-run-ocr-in-c-extract-arabic-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách chạy OCR trong C# – Trích xuất văn bản tiếng Ả Rập từ PNG

Bạn đã bao giờ tự hỏi **cách chạy OCR** trên một bức ảnh chứa ký tự tiếng Ả Rập chưa? Bạn không phải là người duy nhất. Nhiều nhà phát triển gặp khó khăn khi họ cần **trích xuất văn bản tiếng Ả Rập** từ một tệp PNG nhưng không biết thư viện nào sẽ xử lý các script từ phải sang trái mà không gặp rắc rối.  

Trong hướng dẫn này, chúng ta sẽ đi qua mọi thứ bạn cần biết để **chuyển đổi hình ảnh thành văn bản**, **đọc văn bản từ PNG**, và cuối cùng **cách trích xuất văn bản** bằng Aspose.OCR trong một ứng dụng console C# sạch sẽ. Khi kết thúc, bạn sẽ có một chương trình sẵn sàng chạy và in ra chuỗi tiếng Ả Rập trực tiếp trên terminal của bạn.

## Những gì bạn sẽ học

- Cài đặt và tham chiếu gói NuGet Aspose.OCR.  
- Cấu hình engine OCR để hỗ trợ ngôn ngữ tiếng Ả Rập.  
- Tải ảnh PNG và chạy quá trình nhận dạng.  
- Lấy và hiển thị văn bản đã trích xuất.  
- Tinh chỉnh cài đặt để cải thiện độ chính xác và xử lý các vấn đề thường gặp.

Không yêu cầu kinh nghiệm trước về OCR, chỉ cần hiểu cơ bản về C# và môi trường phát triển .NET (Visual Studio, Rider, hoặc `dotnet` CLI đều được).

---

## Cách chạy OCR – Cài đặt Aspose OCR

### Bước 1: Thêm gói NuGet Aspose.OCR

Điều đầu tiên chúng ta cần là thư viện OCR. Aspose.OCR là một sản phẩm thương mại, nhưng nó cung cấp bản dùng thử miễn phí hoạt động hoàn hảo cho mục đích học tập.

```bash
# Using the .NET CLI
dotnet add package Aspose.OCR
```

Hoặc, mở **NuGet Package Manager** trong Visual Studio, tìm kiếm **Aspose.OCR**, và nhấn **Install**.

> **Mẹo:** Nếu bạn dự định sử dụng thư viện trong pipeline CI, thêm cờ `-v` để khóa phiên bản, ví dụ, `dotnet add package Aspose.OCR -v 23.10`.

### Bước 2: Tạo một dự án Console mới (nếu bạn chưa có)

```bash
dotnet new console -n ArabicOcrDemo
cd ArabicOcrDemo
```

Bây giờ bạn đã có một tệp `Program.cs` mới sẵn sàng cho mã của chúng ta.

---

## Trích xuất văn bản tiếng Ả Rập – Viết mã OCR

Dưới đây là chương trình hoàn chỉnh, sẵn sàng chạy. Lưu nó dưới tên `Program.cs` (hoặc thay thế tệp được tự động tạo).

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Config;

namespace ArabicOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Create an OCR engine instance
            // -------------------------------------------------
            var ocrEngine = new OcrEngine();

            // -------------------------------------------------
            // Step 2: Choose the language for recognition.
            // Here we use Arabic. You can swap this for
            // OcrLanguage.Korean, OcrLanguage.SerbianCyrillic, etc.
            // -------------------------------------------------
            ocrEngine.Language = OcrLanguage.Arabic;

            // -------------------------------------------------
            // Step 3: Load the image containing the text.
            // Replace the path with the location of your PNG.
            // -------------------------------------------------
            string imagePath = "YOUR_DIRECTORY/arabic_sample.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // -------------------------------------------------
            // Step 4: Run the OCR process.
            // -------------------------------------------------
            ocrEngine.Recognize();

            // -------------------------------------------------
            // Step 5: Display the extracted text.
            // -------------------------------------------------
            Console.WriteLine("=== Extracted Arabic Text ===");
            Console.WriteLine(ocrEngine.Text);
        }
    }
}
```

#### Tại sao mỗi dòng lại quan trọng

- `OcrEngine`: Lớp trung tâm điều phối việc tải ảnh, chọn ngôn ngữ và nhận dạng.  
- `Language = OcrLanguage.Arabic`: Tiếng Ả Rập sử dụng script từ phải sang trái và các glyph độc đáo; việc đặt ngôn ngữ sẽ báo cho engine áp dụng các mô hình ký tự đúng.  
- `ImageStream.FromFile`: Xử lý PNG, JPEG, BMP và nhiều định dạng khác. Nếu bạn cần đọc từ `MemoryStream` (ví dụ, tệp được tải lên), hãy thay thế lời gọi này cho phù hợp.  
- `Recognize()`: Thực hiện công việc nặng—phân tích pixel, phân đoạn và phân loại ký tự.  
- `ocrEngine.Text`: Chuỗi Unicode cuối cùng, sẵn sàng cho việc xử lý tiếp theo, lưu trữ hoặc hiển thị.

### Kết quả mong đợi

Nếu `arabic_sample.png` chứa cụm từ “مرحبا بالعالم” (Hello World), console sẽ in ra:

```
=== Extracted Arabic Text ===
مرحبا بالعالم
```

Nếu kết quả bị rối, hãy kiểm tra lại ảnh có rõ ràng, ngôn ngữ đã được đặt là Arabic, và phiên bản engine OCR khớp với tài liệu.

---

## Chuyển đổi hình ảnh thành văn bản – Tinh chỉnh độ chính xác

Mặc dù cài đặt mặc định hoạt động cho hầu hết các bản quét sạch, nhưng các ảnh thực tế thường cần một chút tinh chỉnh thêm.

| Cài đặt | Chức năng | Khi nào sử dụng |
|---------|-----------|-----------------|
| `ocrEngine.Config.Preprocess = true` | Bật tự động nhị phân và loại bỏ nhiễu. | Tài liệu quét có bóng. |
| `ocrEngine.Config.Deskew = true` | Xoay ảnh để sửa độ nghiêng nhẹ. | Ảnh chụp góc nghiêng. |
| `ocrEngine.Config.PageSegMode = PageSegMode.SingleBlock` | Xem toàn bộ ảnh như một khối văn bản duy nhất. | Chú thích đơn giản hoặc nhãn một dòng. |
| `ocrEngine.Config.CharWhitelist = "ءاأإآبتثجحخدذرزس شصضطظعغفقكلمنهوية"` | Giới hạn nhận dạng chỉ các ký tự tiếng Ả Rập. | Giảm các kết quả sai trên các trang hỗn hợp ngôn ngữ. |

Bạn có thể thêm các dòng này ngay sau khi tạo engine:

```csharp
ocrEngine.Config.Preprocess = true;
ocrEngine.Config.Deskew = true;
ocrEngine.Config.CharWhitelist = "ءاأإآبتثجحخدذرزسشصضطظعغفقكلمنهوية";
```

---

## Đọc văn bản từ PNG – Xử lý các nguồn ảnh khác nhau

Đôi khi tệp PNG nằm trong cơ sở dữ liệu hoặc đến từ yêu cầu web. Dưới đây là một biến thể nhanh đọc từ `byte[]`:

```csharp
byte[] pngBytes = File.ReadAllBytes("YOUR_DIRECTORY/arabic_sample.png");
using var ms = new MemoryStream(pngBytes);
ocrEngine.Image = ImageStream.FromStream(ms);
ocrEngine.Recognize();
Console.WriteLine(ocrEngine.Text);
```

Phần còn lại của quy trình vẫn giống nhau, có nghĩa là **cách trích xuất văn bản** vẫn nhất quán bất kể nguồn.

---

## Cách trích xuất văn bản – Tùy chọn nâng cao & Trường hợp đặc biệt

### 1. PDF hoặc TIFF đa trang

Nếu bạn cần OCR một tài liệu đa trang, lặp qua từng trang:

```csharp
var pdfDoc = new Aspose.Pdf.Document("multi_page.pdf");
foreach (var page in pdfDoc.Pages)
{
    using var img = page.ConvertToImage();
    ocrEngine.Image = ImageStream.FromBitmap(img);
    ocrEngine.Recognize();
    Console.WriteLine($"Page {page.Number}: {ocrEngine.Text}");
}
```

> **Lưu ý:** Bạn sẽ cần gói `Aspose.PDF` cho đoạn mã này.

### 2. Tự động phát hiện ngôn ngữ

Aspose.OCR cũng cung cấp tính năng tự động phát hiện, nhưng chậm hơn. Nếu bạn không chắc ảnh chứa tiếng Ả Rập hay script khác, hãy bật tính năng này:

```csharp
ocrEngine.Language = OcrLanguage.AutoDetect;
```

### 3. Mẹo hiệu năng

- **Tái sử dụng đối tượng `OcrEngine`** cho nhiều ảnh; tạo một thể hiện mới mỗi lần sẽ tăng chi phí.  
- **Chạy song song** chỉ khi bạn có các thể hiện engine riêng cho mỗi luồng—chia sẻ một thể hiện sẽ gây ra race condition.

---

## Kết luận

Chúng tôi đã trình bày **cách chạy OCR** trong C# từ đầu đến cuối, cho bạn thấy cách **trích xuất văn bản tiếng Ả Rập**, **chuyển đổi hình ảnh thành văn bản**, **đọc văn bản từ PNG**, và trả lời **cách trích xuất văn bản** trong nhiều tình huống. Mã mẫu hoàn chỉnh, độc lập và sẵn sàng để bạn dán vào bất kỳ dự án console .NET nào.

Bước tiếp theo? Hãy thử thay `OcrLanguage.Arabic` bằng Korean hoặc Serbian Cyrillic để xem sức mạnh đa ngôn ngữ của thư viện. Thử nghiệm các cờ tiền xử lý để nâng cao độ chính xác trên các bản quét nhiễu, hoặc tích hợp quy trình OCR vào một API web để người dùng có thể tải lên ảnh và nhận kết quả văn bản ngay lập tức.

Chúc lập trình vui vẻ, và hy vọng kết quả OCR của bạn luôn rõ ràng như pha lê!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}