---
category: general
date: 2026-02-24
description: Cách sử dụng OCR trong C# để trích xuất văn bản từ các tệp hình ảnh.
  Học cách chuyển đổi PNG sang văn bản, đọc hình ảnh một cách bất đồng bộ và xử lý
  các lỗi thường gặp.
draft: false
keywords:
- how to use OCR
- extract text from image
- convert png to text
- how to extract text
- how to read image
language: vi
og_description: Cách sử dụng OCR trong C# để trích xuất văn bản từ hình ảnh. Hướng
  dẫn này trình bày OCR bất đồng bộ từng bước với Aspose, bao gồm chuyển đổi, xử lý
  lỗi và các thực tiễn tốt nhất.
og_title: Cách sử dụng OCR trong C# – Hướng dẫn đầy đủ
tags:
- OCR
- C#
- Aspose
title: Cách sử dụng OCR trong C# – Trích xuất văn bản từ hình ảnh bằng Aspose OCR
url: /vi/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách sử dụng OCR trong C# – Trích xuất văn bản từ hình ảnh

Bạn đã bao giờ tự hỏi **cách sử dụng OCR** để lấy văn bản từ một bức ảnh mà không phải gõ tay chưa? Bạn không phải là người duy nhất. Nhiều nhà phát triển gặp khó khăn khi họ cần *trích xuất văn bản từ hình ảnh* như các tệp PNG, và cách sao chép‑dán thông thường không đủ.  

Trong hướng dẫn này, chúng ta sẽ đi qua một giải pháp bất đồng bộ hoàn chỉnh mà **chuyển đổi PNG thành văn bản** bằng thư viện Aspose.OCR. Khi kết thúc, bạn sẽ biết chính xác cách đọc các tệp hình ảnh, xử lý lỗi và tích hợp kết quả vào ứng dụng của mình.  

Chúng ta sẽ bao phủ mọi thứ từ việc cài đặt gói NuGet đến tinh chỉnh công cụ OCR để đạt độ chính xác cao hơn, và chúng tôi sẽ cung cấp một số mẹo về cách xử lý khi hình ảnh không rõ ràng. Không cần phải chạy theo các liên kết tài liệu—mọi thứ bạn cần đều có ở đây.

## Những gì bạn cần

- .NET 6.0 hoặc mới hơn (mã chạy được trên .NET Core và .NET Framework cũng được)  
- Visual Studio 2022 (hoặc bất kỳ IDE nào bạn thích)  
- Gói NuGet **Aspose.OCR** (`Install-Package Aspose.OCR`)  
- Một tệp hình ảnh (PNG, JPG, BMP) bạn muốn xử lý – chúng tôi sẽ gọi nó là `input.png`

Đó là tất cả. Nếu bạn đã có những mục trên, bạn đã sẵn sàng bắt đầu.

![Diagram showing OCR workflow – how to use OCR to extract text from an image](/images/ocr-workflow.png)

## Bước 1: Cài đặt Aspose.OCR và Thêm Namespaces

Đầu tiên, đưa thư viện vào dự án của bạn. Mở Package Manager Console và chạy:

```powershell
Install-Package Aspose.OCR
```

Sau đó, ở đầu tệp C# của bạn, thêm các namespace cần thiết:

```csharp
using Aspose.OCR;
using System;
using System.Threading.Tasks;
```

> **Pro tip:** Nếu bạn đang sử dụng .NET 6 minimal APIs, bạn có thể đặt các câu lệnh `using` này trong một tệp toàn cục để không phải lặp lại chúng trong nhiều lớp.

### Tại sao điều này quan trọng

`Namespace` `Aspose.OCR` cung cấp cho bạn quyền truy cập vào `OcrEngine`, lớp cốt lõi thực sự đọc hình ảnh. Nếu không có nó, bạn sẽ phải tự viết mã phân tích pixel—một con đường rối rắm. Thêm các namespace giúp mã gọn gàng và thông báo cho trình biên dịch nơi tìm các kiểu bạn sẽ dùng.

## Bước 2: Tạo một OCR Engine bất đồng bộ

Chúng ta sẽ bao bọc lời gọi OCR trong một phương thức `async` để giao diện người dùng của bạn luôn phản hồi và mã phía máy chủ có thể mở rộng. Dưới đây là khung cơ bản của một ứng dụng console:

```csharp
class AsyncExample
{
    static async Task Main()
    {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Recognize text from the image asynchronously
        OcrResult ocrResult = await ocrEngine.RecognizeImageAsync("YOUR_DIRECTORY/input.png");

        // Output the extracted text
        Console.WriteLine(ocrResult.Text);
    }
}
```

### Giải thích

- **`OcrEngine ocrEngine = new OcrEngine();`** – Tạo một thể hiện của engine với các cài đặt mặc định. Bạn có thể sau này tinh chỉnh ngôn ngữ, chế độ phát hiện hoặc bộ lọc tiền xử lý.  
- **`await ocrEngine.RecognizeImageAsync(...)`** – Phương thức bất đồng bộ trả về một `Task<OcrResult>`. Đợi nó sẽ giải phóng luồng trong khi OCR chạy ở nền.  
- **`ocrResult.Text`** – Đại diện dạng văn bản thuần của mọi thứ engine có thể đọc được. Đây là trọng tâm của *cách trích xuất văn bản* từ một hình ảnh.

## Bước 3: Tinh chỉnh Engine để Độ chính xác cao hơn

OCR mặc định hoạt động tốt trên các hình ảnh sạch, độ tương phản cao, nhưng các ảnh thực tế thường cần một chút trợ giúp. Bạn có thể điều chỉnh một vài thuộc tính trước khi gọi `RecognizeImageAsync`:

```csharp
// Set language (English is default, but you can add more)
ocrEngine.Language = OcrLanguage.English;

// Enable automatic image preprocessing (deskew, despeckle)
ocrEngine.ImagePreprocessingOptions = ImagePreprocessingOptions.Auto;

// If you only need numbers, restrict the character set
ocrEngine.Characters = "0123456789";
```

### Khi nào nên sử dụng các cài đặt này

- **Quét chất lượng thấp** – Bật `ImagePreprocessingOptions.Auto` để Aspose làm sạch nhiễu.  
- **PDF đa ngôn ngữ** – Thay đổi `Language` thành `OcrLanguage.French` hoặc kết hợp các ngôn ngữ bằng bitmask.  
- **Trường biểu mẫu** – Giới hạn `Characters` chỉ cho các chữ số hoặc chữ hoa để giảm các kết quả sai.

## Bước 4: Xử lý lỗi một cách nhẹ nhàng

OCR không phải là phép màu; nó có thể thất bại nếu tệp bị thiếu, hỏng, hoặc ở định dạng không được hỗ trợ. Bao bọc lời gọi async trong khối try/catch:

```csharp
try
{
    OcrResult ocrResult = await ocrEngine.RecognizeImageAsync("YOUR_DIRECTORY/input.png");
    Console.WriteLine("Extracted Text:");
    Console.WriteLine(ocrResult.Text);
}
catch (FileNotFoundException ex)
{
    Console.Error.WriteLine($"File not found: {ex.Message}");
}
catch (OcrException ex)
{
    Console.Error.WriteLine($"OCR failed: {ex.Message}");
}
```

### Tại sao điều này hữu ích

Cung cấp thông báo lỗi rõ ràng giúp tăng tốc gỡ lỗi và cải thiện trải nghiệm người dùng cuối. Thay vì một lỗi chung, bạn nhận được một lời nhắc hữu ích cho biết nên kiểm tra đường dẫn, định dạng tệp, hay cấu hình của OCR engine.

## Bước 5: Kết hợp Tất cả – Ví dụ Hoàn chỉnh

Dưới đây là một chương trình console hoàn chỉnh, sẵn sàng chạy, minh họa **cách sử dụng OCR**, áp dụng tiền xử lý và xử lý lỗi. Sao chép và dán nó vào một `.csproj` mới và nhấn F5.

```csharp
using Aspose.OCR;
using System;
using System.IO;
using System.Threading.Tasks;

class AsyncOcrDemo
{
    static async Task Main()
    {
        // 1️⃣  Initialize the OCR engine with optional tweaks
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English,
            ImagePreprocessingOptions = ImagePreprocessingOptions.Auto
        };

        // 2️⃣  Define the path to the image you want to read
        string imagePath = Path.Combine(Environment.CurrentDirectory, "input.png");

        // 3️⃣  Perform the async recognition inside a safe try/catch
        try
        {
            OcrResult result = await ocrEngine.RecognizeImageAsync(imagePath);
            Console.WriteLine("\n--- Extracted Text ---\n");
            Console.WriteLine(result.Text);
            Console.WriteLine("\n--- End of Output ---\n");
        }
        catch (FileNotFoundException fnf)
        {
            Console.Error.WriteLine($"❌ Image not found: {fnf.Message}");
        }
        catch (OcrException ocrEx)
        {
            Console.Error.WriteLine($"❌ OCR processing error: {ocrEx.Message}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"❌ Unexpected error: {ex.Message}");
        }
    }
}
```

**Kết quả mong đợi** (giả sử `input.png` chứa cụm từ “Hello World”):

```
--- Extracted Text ---

Hello World

--- End of Output ---
```

Nếu hình ảnh mờ, bạn có thể thấy các ký tự thừa hoặc từ bị thiếu — đó là lúc các tùy chọn tiền xử lý từ Bước 3 trở nên quan trọng.

## Bước 6: Mở rộng Giải pháp – Từ PNG sang PDF hoặc Tệp Văn bản

Đôi khi bạn cần **chuyển đổi PNG thành văn bản** và sau đó lưu kết quả vào một tệp `.txt` hoặc nhúng vào báo cáo PDF. Dưới đây là đoạn mã nhanh ghi đầu ra OCR vào tệp:

```csharp
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.txt");
await File.WriteAllTextAsync(outputPath, result.Text);
Console.WriteLine($"✅ Text saved to {outputPath}");
```

Hoặc, nếu bạn đang tạo PDF bằng Aspose.PDF:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// ... after OCR result is obtained
Document pdfDoc = new Document();
Page page = pdfDoc.Pages.Add();
TextFragment fragment = new TextFragment(result.Text);
page.Paragraphs.Add(fragment);
pdfDoc.Save("Result.pdf");
Console.WriteLine("✅ PDF created with extracted text.");
```

Các phần mở rộng này minh họa cách **cách đọc dữ liệu hình ảnh** có thể cung cấp cho các quy trình tiếp theo — tạo báo cáo, lập chỉ mục tìm kiếm, hoặc thậm chí cung cấp cho mô hình ngôn ngữ.

## Câu hỏi Thường gặp & Trường hợp Đặc biệt

| Câu hỏi | Trả lời |
|----------|--------|
| *Các định dạng hình ảnh nào được hỗ trợ?* | Aspose.OCR hỗ trợ PNG, JPEG, BMP, TIFF và GIF. Nếu bạn có PDF, hãy trích xuất các trang của nó thành hình ảnh trước. |
| *Tôi có thể xử lý nhiều hình ảnh đồng thời không?* | Có — bao bọc mỗi lời gọi `RecognizeImageAsync` trong một task riêng và sử dụng `Task.WhenAll`. Chỉ cần chú ý tới việc sử dụng bộ nhớ. |
| *Nếu OCR trả về văn bản rỗng thì sao?* | Kiểm tra chất lượng hình ảnh: độ tương phản thấp hoặc văn bản bị quay thường thất bại. Bật `ImagePreprocessingOptions.Deskew` hoặc tự quay hình ảnh trước khi OCR. |
| *Có giới hạn kích thước hình ảnh không?* | Các hình ảnh lớn (>10 MP) có thể gây `OutOfMemoryException`. Hạ độ phân giải xuống mức hợp lý (ví dụ, 300 DPI) trước khi nhận dạng. |
| *Tôi có cần giấy phép cho Aspose.OCR không?* | Chế độ phát triển hoạt động với giấy phép tạm thời, nhưng trong môi trường production bạn sẽ cần mua giấy phép để loại bỏ watermark đánh giá. |

## Mẹo Tối ưu Hiệu suất

- **Tái sử dụng thể hiện `OcrEngine`** cho việc xử lý hàng loạt; tạo một engine mới cho mỗi hình ảnh sẽ gây tốn tài nguyên.  
- **Tắt các ngôn ngữ không dùng** để tăng tốc phát hiện — mỗi ngôn ngữ bổ sung sẽ tăng một chút chi phí xử lý.  
- **Chạy OCR trên một luồng nền** (như đã minh họa) để giữ cho các luồng UI phản hồi nhanh trong ứng dụng desktop hoặc web.

## Kết luận

Chúng tôi đã bao phủ **cách sử dụng OCR** trong C# từ đầu đến cuối: cài đặt Aspose.OCR, viết phương thức async, tinh chỉnh cài đặt cho hình ảnh nhiễu, xử lý lỗi và lưu trữ kết quả. Bây giờ bạn có một cách đáng tin cậy để *trích xuất văn bản từ hình ảnh*, *chuyển đổi PNG thành văn bản*, và thậm chí đưa văn bản đó vào các quy trình khác như tạo PDF.  

Sẵn sàng cho thử thách tiếp theo? Hãy thử đưa đầu ra OCR vào một chỉ mục Azure Cognitive Search có thể tìm kiếm, hoặc thử nghiệm OCR đa ngôn ngữ bằng cách thêm `OcrLanguage.Spanish | OcrLanguage.French` vào engine. Không gì là không thể khi bạn biết **cách đọc dữ liệu hình ảnh** một cách lập trình.

---

*Nếu bạn thấy hướng dẫn này hữu ích, hãy đánh dấu sao trên GitHub, chia sẻ với đồng nghiệp, hoặc để lại bình luận bên dưới với các mẹo OCR của bạn. Chúc lập trình vui vẻ!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}