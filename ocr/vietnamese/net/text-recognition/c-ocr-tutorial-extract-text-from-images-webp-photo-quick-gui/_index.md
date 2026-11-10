---
category: general
date: 2026-03-17
description: Hướng dẫn OCR bằng C# – khám phá cách trích xuất văn bản từ các tệp hình
  ảnh, đọc văn bản từ ảnh WebP và chuyển đổi hình ảnh thành văn bản bằng OcrEngine
  đơn giản.
draft: false
keywords:
- c# OCR tutorial
- extract text from image
- read text from webp
- recognize text from photo
- convert image to text
language: vi
og_description: Hướng dẫn OCR bằng C# cho bạn cách trích xuất văn bản từ các tệp hình
  ảnh, đọc văn bản từ ảnh WebP và chuyển đổi hình ảnh thành văn bản chỉ với vài dòng
  code.
og_title: Hướng dẫn OCR C# – Trích xuất văn bản từ hình ảnh trong vài phút
tags:
- C#
- OCR
- Image Processing
title: 'Hướng dẫn OCR C#: Trích xuất văn bản từ hình ảnh (WebP, Ảnh) – Hướng dẫn nhanh'
url: /vi/net/text-recognition/c-ocr-tutorial-extract-text-from-images-webp-photo-quick-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# hướng dẫn OCR c# – Trích xuất văn bản từ hình ảnh (WebP, Ảnh)

Bạn đã bao giờ cần **trích xuất văn bản từ tệp hình ảnh** nhưng không biết bắt đầu từ đâu trong C#? Có thể bạn có một ảnh chụp màn hình WebP, một file JPEG của biên lai, hoặc một trang PDF đã quét và bạn chỉ muốn lấy các từ bên trong. Trong **hướng dẫn OCR c#** này, chúng ta sẽ đi qua một ví dụ hoàn chỉnh, sẵn sàng chạy, đọc văn bản từ một bức ảnh, xử lý WebP và các định dạng hiện đại khác, và chuyển đổi ảnh thành văn bản thuần – tất cả chỉ trong vài dòng mã.

**Lợi ích là gì?** Bạn sẽ có thể biến bất kỳ bức ảnh chứa văn bản nào thành các chuỗi có thể tìm kiếm, đưa chúng vào cơ sở dữ liệu, hoặc truyền chúng tới các pipeline AI tiếp theo. Không có ma thuật, chỉ có một engine OCR vững chắc, một vài API .NET, và giải thích rõ ràng “tại sao” cho mỗi bước.

## Những gì bạn cần

Trước khi bắt đầu, hãy chắc chắn rằng bạn đã có:

- **.NET 6 SDK** (hoặc mới hơn). Mã dưới đây biên dịch với .NET 6+ và chạy trên Windows, Linux hoặc macOS.
- **Visual Studio 2022** hoặc bất kỳ trình soạn thảo nào bạn thích (VS Code cũng hoạt động tốt).
- Gói NuGet **`Microsoft.Windows.SDK.Contracts`** (cung cấp `Windows.Media.Ocr`). Cài đặt bằng:

```bash
dotnet add package Microsoft.Windows.SDK.Contracts
```

- Một tệp ảnh mà bạn muốn xử lý – trong hướng dẫn này chúng ta sẽ dùng ảnh **WebP** tên `photo.webp` đặt trong thư mục `YOUR_DIRECTORY`.

> Mẹo chuyên nghiệp: Nếu bạn đang dùng nền tảng không phải Windows, bạn có thể thay thế `OcrEngine` bằng một thư viện đa nền tảng như **Tesseract**. Phần mã xung quanh hầu như không thay đổi.

## Bước 1: Tạo dự án hướng dẫn OCR C# mới

Đầu tiên, tạo một ứng dụng console mới. Mở terminal và chạy:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

Thêm gói cần thiết (như ở trên) và mở dự án trong IDE của bạn. Cấu trúc này cung cấp cho chúng ta một môi trường sạch sẽ cho **hướng dẫn OCR c#**.

## Bước 2: Nhập không gian tên và chuẩn bị ảnh

Chúng ta cần một vài chỉ thị `using` để trình biên dịch biết nơi tìm `OcrEngine`, `SoftwareBitmap`, và các trợ giúp tải ảnh.

```csharp
using System;
using System.IO;
using Windows.Graphics.Imaging;
using Windows.Media.Ocr;
using Windows.Storage.Streams;
```

> **Tại sao lại cần những không gian tên này?**  
> `Windows.Media.Ocr` chứa lớp `OcrEngine` thực hiện việc nhận dạng. `Windows.Graphics.Imaging` cho phép chúng ta giải mã ảnh (bao gồm WebP) thành một `SoftwareBitmap` mà engine có thể hiểu. Các trợ giúp `System.IO` và `Windows.Storage.Streams` giúp việc tải tệp trở nên dễ dàng.

Bây giờ, tải ảnh lên. Bộ giải mã tích hợp có thể xử lý WebP, HEIF, PNG, JPEG và nhiều định dạng khác, vì vậy bạn có thể **đọc văn bản từ WebP** mà không cần plugin bổ sung.

```csharp
// Step 2: Load the image file into a SoftwareBitmap
string imagePath = Path.Combine("YOUR_DIRECTORY", "photo.webp");

// Open the file as a random access stream
using (IRandomAccessStream stream = File.OpenRead(imagePath).AsRandomAccessStream())
{
    // Decode the image (auto-detects format)
    BitmapDecoder decoder = await BitmapDecoder.CreateAsync(stream);
    SoftwareBitmap bitmap = await decoder.GetSoftwareBitmapAsync();
    
    // Optional: Convert to grayscale for better OCR accuracy
    SoftwareBitmap grayBitmap = SoftwareBitmap.Convert(bitmap, BitmapPixelFormat.Gray8);
    
    // Pass the bitmap to the next step
    await RecognizeTextAsync(grayBitmap);
}
```

> **Trường hợp đặc biệt:** Nếu ảnh của bạn đã là đen‑trắng, bạn có thể bỏ qua bước chuyển đổi. Việc chuyển sang ảnh xám là một cải thiện hiệu suất nhỏ và thường giúp nhận dạng tốt hơn trên các ảnh nhiễu.

## Bước 3: Chạy engine OCR – Nhận dạng văn bản từ ảnh

Đây là phần cốt lõi của **hướng dẫn OCR c#**. Chúng ta tạo một thể hiện của `OcrEngine`, truyền bitmap vào, và lấy ra văn bản đã nhận dạng.

```csharp
static async Task RecognizeTextAsync(SoftwareBitmap bitmap)
{
    // Step 3: Create the OCR engine instance – it automatically picks the best language
    OcrEngine ocrEngine = OcrEngine.TryCreateFromUserProfileLanguages();

    if (ocrEngine == null)
    {
        Console.WriteLine("❌ No OCR engine available for the current language.");
        return;
    }

    // Perform recognition
    OcrResult ocrResult = await ocrEngine.RecognizeAsync(bitmap);

    // Step 4: Display the extracted text – this is the “convert image to text” part
    Console.WriteLine("📝 Recognized text:");
    Console.WriteLine(ocrResult.Text);
}
```

**Đang xảy ra gì?**  
- `TryCreateFromUserProfileLanguages()` chọn ngôn ngữ mà hồ sơ người dùng Windows của bạn đang sử dụng, thường bao gồm tiếng Anh, tiếng Tây Ban Nha, v.v. Nếu bạn cần một ngôn ngữ cụ thể, hãy dùng `OcrEngine.TryCreateFromLanguage(new Language("fr-FR"))`.
- `RecognizeAsync` thực hiện công việc nặng trên một luồng nền, trả về một `OcrResult` chứa chuỗi thô, các hộp bao quanh từ và điểm tin cậy.
- Cuối cùng, chúng ta in `ocrResult.Text`, cung cấp cho bạn kết quả **chuyển đổi ảnh thành văn bản** mà có thể truyền tới các bước tiếp theo.

## Bước 4: Ví dụ đầy đủ, có thể chạy ngay

Kết hợp tất cả lại, dưới đây là một chương trình tự chứa mà bạn có thể sao chép‑dán vào `Program.cs`. Nó biên dịch, chạy, và in ra văn bản đã được trích xuất từ `photo.webp`.

```csharp
// Program.cs – Complete c# OCR tutorial example
using System;
using System.IO;
using System.Threading.Tasks;
using Windows.Graphics.Imaging;
using Windows.Media.Ocr;
using Windows.Storage.Streams;

class Program
{
    static async Task Main(string[] args)
    {
        // Replace with your actual directory and file name
        string imagePath = Path.Combine("YOUR_DIRECTORY", "photo.webp");

        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"❗ Image not found: {imagePath}");
            return;
        }

        // Load and optionally preprocess the image
        using (IRandomAccessStream stream = File.OpenRead(imagePath).AsRandomAccessStream())
        {
            BitmapDecoder decoder = await BitmapDecoder.CreateAsync(stream);
            SoftwareBitmap bitmap = await decoder.GetSoftwareBitmapAsync();

            // Convert to grayscale – improves OCR accuracy on many photos
            SoftwareBitmap grayBitmap = SoftwareBitmap.Convert(bitmap, BitmapPixelFormat.Gray8);

            // Run OCR
            await RecognizeTextAsync(grayBitmap);
        }
    }

    static async Task RecognizeTextAsync(SoftwareBitmap bitmap)
    {
        // Create OCR engine (auto‑detect language)
        OcrEngine ocrEngine = OcrEngine.TryCreateFromUserProfileLanguages();

        if (ocrEngine == null)
        {
            Console.WriteLine("❌ Unable to create OCR engine. Ensure language packs are installed.");
            return;
        }

        // Perform recognition
        OcrResult result = await ocrEngine.RecognizeAsync(bitmap);

        // Output the extracted text
        Console.WriteLine("\n--- OCR Output ---");
        Console.WriteLine(result.Text);
        Console.WriteLine("--- End of Output ---\n");
    }
}
```

### Kết quả mong đợi

Nếu `photo.webp` chứa câu “Hello, world! This is a test.” bạn sẽ thấy một kết quả tương tự:

```
--- OCR Output ---
Hello, world!
This is a test.
--- End of Output ---
```

Các ngắt dòng cụ thể phụ thuộc vào bố cục của ảnh nguồn, nhưng kết quả **trích xuất văn bản từ ảnh** sẽ luôn là một chuỗi thuần mà bạn có thể xử lý tiếp.

## Câu hỏi thường gặp & Trường hợp đặc biệt

### Có hoạt động với các định dạng ảnh khác không?

Chắc chắn rồi. Bộ giải mã được dùng (`BitmapDecoder`) tự động phát hiện JPEG, PNG, BMP, GIF, **WebP**, HEIF và nhiều hơn nữa. Vì vậy bạn có thể **đọc văn bản từ WebP**, JPEG, hoặc thậm chí TIFF mà không cần thay đổi mã.

### Nếu engine OCR trả về độ tin cậy thấp thì sao?

Bạn có thể kiểm tra `ocrResult.Lines` và mỗi `OcrWord` để lấy `ConfidenceScore`. Nếu điểm thấp hơn một ngưỡng (ví dụ 0.6), hãy cân nhắc:

- Tiền xử lý ảnh (tăng độ tương phản, làm nét, chỉnh góc).
- Sử dụng ảnh nguồn có độ phân giải cao hơn.
- Chuyển sang thư viện chuyên dụng như **Tesseract** để hỗ trợ đa ngôn ngữ.

### Làm sao xử lý nhiều ngôn ngữ trong cùng một ảnh?

Tạo các thể hiện `OcrEngine` riêng cho mỗi ngôn ngữ và chạy chúng tuần tự, hoặc dùng một thư viện hỗ trợ phát hiện ngôn ngữ hỗn hợp. Đối với engine tích hợp, bạn có thể truyền một đối tượng `Language`:

```csharp
var spanishEngine = OcrEngine.TryCreateFromLanguage(new Language("es-ES"));
```

### Có thể chạy trên Linux/macOS không?

API `Windows.Media.Ocr` chỉ hỗ trợ Windows. Trên các nền tảng không phải Windows, hãy thay thế phần OCR bằng **Tesseract** (qua `Tesseract.Net.SDK`). Mã tải và tiền xử lý ảnh vẫn giữ nguyên, vì vậy phần còn lại của **hướng dẫn OCR c#** vẫn áp dụng.

## Mẹo chuyên nghiệp để cải thiện độ chính xác

- **Thay đổi kích thước** ảnh lớn xuống tối đa 2000 px ở cạnh dài nhất – các engine OCR hoạt động nhanh hơn với kích thước vừa phải.
- **Giảm nhiễu** bằng một bộ lọc Gaussian đơn giản nếu ảnh bị hạt.
- **Chỉnh góc** bitmap nếu văn bản không nằm ngang hoàn toàn; `SoftwareBitmap` có thể xoay trước khi truyền vào `OcrEngine`.
- **Cache** thể hiện `OcrEngine` nếu bạn xử lý nhiều ảnh trong một batch; việc tạo lại sẽ gây tốn tài nguyên.

## Chủ đề liên quan để khám phá

- **Chuyển đổi ảnh thành văn bản** bằng **Tesseract** cho các dự án đa nền tảng.
- **Trích xuất văn bản từ PDF** bằng cách render mỗi trang thành ảnh trước.
- **Batch OCR**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}