---
category: general
date: 2026-02-13
description: Cách sử dụng OCR trong C# để trích xuất văn bản từ hình ảnh, nhận dạng
  văn bản từ ảnh hoặc JPG, và chạy OCR trên hình ảnh mà không cần internet.
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from photo
- recognize text from jpg
- run OCR on image
language: vi
og_description: Cách sử dụng OCR trong C# để trích xuất văn bản từ hình ảnh, nhận
  dạng văn bản từ ảnh và chạy OCR trên hình ảnh với một ví dụ đầy đủ, có thể chạy
  được.
og_title: Cách sử dụng OCR trong C# – Trích xuất văn bản từ hình ảnh
tags:
- OCR
- C#
- Image Processing
title: Cách sử dụng OCR trong C# – Trích xuất văn bản từ hình ảnh và nhận dạng văn
  bản từ ảnh chụp
url: /vi/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image-and-recognize-te/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Sử Dụng OCR trong C# – Trích Xuất Văn Bản Từ Hình Ảnh và Nhận Diện Văn Bản Từ Ảnh

Bạn đã bao giờ tự hỏi **cách sử dụng OCR** để lấy các từ ra khỏi một ảnh chụp màn hình, một biên lai đã quét, hoặc một bức ảnh ngẫu nhiên bạn chụp bằng điện thoại chưa? Bạn không phải là người duy nhất. Trong nhiều ứng dụng thực tế, chúng ta cần chuyển đổi hình ảnh thành văn bản có thể tìm kiếm, và thực hiện việc này cục bộ—không cần kết nối internet không ổn định—có thể cảm giác như một câu đố.

Đó là lý do tại sao hướng dẫn này sẽ chỉ cho bạn cách **trích xuất văn bản từ hình ảnh** bằng một engine OCR C#, và cũng đề cập đến cách **nhận diện văn bản từ ảnh**, **nhận diện văn bản từ JPG**, và **chạy OCR trên hình ảnh** nằm trực tiếp trên ổ đĩa của bạn. Khi hoàn thành, bạn sẽ có một chương trình sẵn sàng sao chép‑dán và hoạt động ngay lập tức.

## Những Điều Bạn Sẽ Học

- Cách cấu hình một engine OCR cho tiếng Trung giản thể (hoặc bất kỳ ngôn ngữ nào bạn muốn).  
- Đoạn mã chính xác để **tải tài nguyên** từ một thư mục cục bộ—không cần gọi mạng.  
- Cách **nhận diện văn bản từ ảnh** như JPEG, PNG, hoặc BMP.  
- Mẹo xử lý các trường hợp biên như thiếu file mô hình hoặc định dạng ảnh không được hỗ trợ.  
- Một ví dụ đầy đủ, có thể chạy được mà bạn có thể đưa vào Visual Studio và thấy kết quả ngay lập tức.

### Các Điều Kiện Cần Có

- .NET 6.0 trở lên (API được dùng ở đây nhắm tới .NET Standard 2.0, vì vậy các phiên bản cũ hơn cũng hoạt động).  
- Kiến thức cơ bản về C# và Visual Studio (hoặc bất kỳ IDE nào bạn thích).  
- Thư viện OCR bạn đang dùng (đoạn mã giả định một lớp `OcrEngine` hư cấu đi kèm với các mô hình ngôn ngữ).  
- Một thư mục chứa các file mô hình ngôn ngữ cần thiết—hãy nghĩ nó như “bộ não” mà engine dùng để đọc các ký tự Trung Quốc.

> **Mẹo chuyên nghiệp:** Nếu bạn chưa có các file mô hình tiếng Trung, hãy tải chúng một lần từ trang của nhà cung cấp và đặt vào một thư mục như `C:\OcrResources`. Engine sẽ không bao giờ cần kết nối internet nữa.

---

![Diagram showing OCR process on a photo](path/to/ocr-diagram.png "Sơ đồ quy trình OCR trên ảnh")

## Cách Sử Dụng OCR: Thiết Lập Engine

Điều đầu tiên bạn cần là một thể hiện của engine OCR, được cấu hình cho ngôn ngữ bạn quan tâm. Trong tutorial này chúng ta nhắm tới **tiếng Trung giản thể**, nhưng việc thay `OcrLanguage.ChineseSimplified` bằng `OcrLanguage.English` (hoặc bất kỳ giá trị enum nào khác) chỉ mất một dòng.

```csharp
using System;
using YourOcrLibrary;   // Replace with the actual namespace of your OCR SDK

// Step 1: Create and configure the OCR engine for Simplified Chinese
var ocrEngine = new OcrEngine
{
    // Primary keyword appears here naturally
    Language = OcrLanguage.ChineseSimplified,

    // Point to a folder that already contains the Chinese model files
    ResourceFolder = @"C:\OcrResources"
};
```

**Tại sao điều này quan trọng:**  
Việc đặt thuộc tính `Language` cho engine biết bộ ký tự nào sẽ được mong đợi. `ResourceFolder` là nơi engine tìm các trọng số mạng nơ‑ron và từ điển ngôn ngữ—giống như ngân hàng nhớ của bộ não. Nếu bạn chỉ tới thư mục sai, engine sẽ ném ra `FileNotFoundException` và bạn sẽ bị kẹt.

## Trích Xuất Văn Bản Từ Hình Ảnh – Tải Tài Nguyên

Trước khi engine thực sự có thể đọc bất cứ thứ gì, bạn phải tải các file mô hình vào bộ nhớ. Bước này **rất quan trọng** vì nó tránh việc gọi mạng mỗi khi bạn xử lý một hình ảnh.

```csharp
// Step 2: Load the language resources from the specified folder (no internet required)
try
{
    ocrEngine.LoadResources();
    Console.WriteLine("Resources loaded successfully.");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed to load OCR resources: {ex.Message}");
    // In a real app you might fallback to a default language or abort gracefully
}
```

**Có thể xảy ra lỗi gì?**  
Nếu đường dẫn thư mục sai hoặc các file bị hỏng, `LoadResources()` sẽ ném ra ngoại lệ. Khối `try/catch` ở trên minh họa cách xử lý lỗi một cách nhẹ nhàng—điều bạn thường cần trong môi trường production.

## Nhận Diện Văn Bản Từ Ảnh – Chạy OCR

Bây giờ là phần thú vị: đưa một file ảnh vào engine và nhận lại văn bản đã được nhận diện. Đây là trung tâm của các kịch bản **run OCR on image**, bất kể ảnh là JPEG, PNG, hay thậm chí BMP.

```csharp
// Step 3: Recognize text from an image file
string imagePath = @"C:\OcrResources\photo.jpg";

try
{
    var recognitionResult = ocrEngine.RecognizeImage(imagePath);
    Console.WriteLine("=== OCR Output ===");
    Console.WriteLine(recognitionResult.Text);
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error during OCR processing: {ex.Message}");
}
```

Phương thức `RecognizeImage` trả về một `RecognitionResult` (hoặc bất kỳ tên nào SDK của bạn dùng) thường chứa:

- `Text` – bản sao văn bản thuần.  
- `Confidence` – điểm số số cho biết mức độ chắc chắn của engine đối với mỗi dòng.  
- `BoundingBoxes` – tọa độ tùy chọn cho vị trí của mỗi từ trên ảnh.

**Tại sao bạn có thể quan tâm đến confidence:**  
Nếu bạn đang xây dựng một công cụ tự động nhập dữ liệu, bạn có thể đặt ngưỡng (ví dụ, 0.85) và yêu cầu người dùng xác nhận các dòng có confidence thấp. Điều này cải thiện đáng kể độ chính xác tổng thể.

## Nhận Diện Văn Bản Từ JPG – Xử Lý Các Định Dạng Khác Nhau

Nhiều nhà phát triển cho rằng OCR chỉ hoạt động với PNG, nhưng các engine hiện đại cũng hỗ trợ **JPG** một cách hoàn hảo. Điều duy nhất cần lưu ý là nén JPEG có thể tạo ra các artefact gây nhầm lẫn cho mô hình.

```csharp
// Bonus: Recognize text from a JPG with optional preprocessing
string jpgPath = @"C:\OcrResources\scanned_doc.jpg";

// Optional: use a simple image‑preprocess step to improve accuracy
var preprocessed = ImageHelper.DenoiseAndDeskew(jpgPath); // pseudo‑method
var result = ocrEngine.RecognizeImage(preprocessed);
Console.WriteLine($"Detected text ({result.Confidence:P0} confidence):");
Console.WriteLine(result.Text);
```

Nếu bạn không có hàm trợ giúp `DenoiseAndDeskew`, nhiều thư viện (ví dụ, OpenCvSharp) cung cấp các chức năng này. Điểm mấu chốt là: **run OCR on image** sau một chút làm sạch nếu ảnh đến từ máy quét hoặc camera điện thoại.

## Run OCR on Image – Mẹo, Trường Hợp Cạnh, và Thực Hành Tốt Nhất

### 1. Quản Lý Bộ Nhớ
Tải các mô hình ngôn ngữ lớn có thể tiêu tốn hàng trăm megabyte. Hãy giải phóng engine khi không còn dùng:

```csharp
ocrEngine.Dispose(); // or using statement if the SDK implements IDisposable
```

### 2. Xử Lý Hàng Loạt
Nếu bạn cần xử lý hàng chục ảnh, hãy tải tài nguyên một lần, sau đó lặp:

```csharp
string[] files = Directory.GetFiles(@"C:\BatchPhotos", "*.jpg");
foreach (var file in files)
{
    var res = ocrEngine.RecognizeImage(file);
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), res.Text);
}
```

### 3. Kịch Bản Đa Ngôn Ngữ
Bạn có thể chuyển đổi ngôn ngữ ngay lập tức bằng cách gán lại `ocrEngine.Language` và gọi lại `LoadResources()`. Chỉ cần chú ý tới thời gian tải thêm.

### 4. Xử Lý Kết Quả Trống
Đôi khi engine trả về một chuỗi rỗng. Thông thường điều này nghĩa là ảnh quá mờ hoặc màu chữ hòa vào nền. Kiểm tra nhanh:

```csharp
if (string.IsNullOrWhiteSpace(recognitionResult.Text))
{
    Console.WriteLine("No text detected – consider increasing image contrast.");
}
```

### 5. Các Xem Xét Về Bảo Mật
Không bao giờ đưa các file do người dùng tải lên trực tiếp vào engine OCR mà không kiểm tra. Ít nhất, hãy xác minh phần mở rộng và kích thước file, và cân nhắc quét để phát hiện phần mềm độc hại.

---

## Ví Dụ Hoàn Chỉnh Hoạt Động

Dưới đây là một chương trình đơn, tự chứa mà bạn có thể sao chép vào một dự án Console App mới. Nó minh họa **cách sử dụng OCR**, **trích xuất văn bản từ hình ảnh**, **nhận diện văn bản từ ảnh**, **nhận diện văn bản từ JPG**, và **run OCR on image**—tất cả trong một lần.

```csharp
// File: Program.cs
using System;
using System.IO;
using YourOcrLibrary; // Replace with actual namespace

namespace OcrDemo
{
    class Program
    {
        static void Main()
        {
            // ------------------------------
            // 1️⃣ Configure the OCR engine
            // ------------------------------
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.ChineseSimplified,
                ResourceFolder = @"C:\OcrResources"
            };

            // Load language resources (no internet needed)
            try
            {
                ocrEngine.LoadResources();
                Console.WriteLine("Resources loaded.");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"Failed to load resources: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 2️⃣ Recognize text from a photo (JPG in this case)
            // -------------------------------------------------
            string imagePath = @"C:\OcrResources\photo.jpg";

            if (!File.Exists(imagePath))
            {
                Console.Error.WriteLine($"Image not found: {imagePath}");
                return;
            }

            try
            {
                var result = ocrEngine.RecognizeImage(imagePath);
                Console.WriteLine("\n=== OCR Output ===");
                Console.WriteLine(result.Text);
                Console.WriteLine($"\nConfidence: {result.Confidence:P2}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"OCR error: {ex.Message}");
            }

            // Clean up
            ocrEngine.Dispose();
        }
    }
}
```

**Kết quả mong đợi (ví dụ):**

```
Resources loaded.

=== OCR Output ===
中华人民共和国
北京
2026年02月13日

Confidence: 92.45%
```

Văn bản thực tế của bạn sẽ khác tùy vào nội dung ảnh, nhưng bạn sẽ thấy một khối ký tự Unicode được in ra console cùng với phần trăm confidence.

---

## Kết Luận

Chúng ta đã đi qua **cách sử dụng OCR** trong C# từ đầu đến cuối—cấu hình engine, tải tài nguyên ngôn ngữ, và cuối cùng **nhận diện văn bản từ ảnh** hoặc **JPG** mà không cần kết nối internet. Bằng cách làm theo các bước trên, bạn có thể **trích xuất văn bản từ hình ảnh**, **run OCR on image** cho các tài sản, và xử lý những cạm bẫy phổ biến mà người mới thường gặp.

Sẵn sàng cho thử thách tiếp theo? Hãy thử đưa một trang PDF đã chuyển thành hình ảnh vào engine, hoặc thử nghiệm với một gói ngôn ngữ khác để xem điểm confidence thay đổi như thế nào. Bạn có thể

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}