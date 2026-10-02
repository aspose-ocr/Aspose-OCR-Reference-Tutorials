---
category: general
date: 2026-02-25
description: Cách sử dụng OCR nhanh chóng trong C# để trích xuất văn bản từ hình ảnh,
  tải hình ảnh cho OCR và thiết lập ngôn ngữ OCR với Aspose OCR. Hướng dẫn từng bước.
draft: false
keywords:
- how to use OCR
- extract text from image
- load image for OCR
- set OCR language
language: vi
og_description: Tìm hiểu cách sử dụng OCR trong C# để trích xuất văn bản từ hình ảnh,
  tải hình ảnh cho OCR và thiết lập ngôn ngữ OCR bằng Aspose OCR. Ví dụ đầy đủ bất
  đồng bộ.
og_title: Cách sử dụng OCR trong C# – Hướng dẫn async toàn diện
tags:
- C#
- Aspose OCR
- async programming
title: Cách sử dụng OCR trong C# – Trích xuất văn bản từ hình ảnh một cách bất đồng
  bộ
url: /vi/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image-asynchronously/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách sử dụng OCR trong C# – Trích xuất văn bản từ hình ảnh một cách bất đồng bộ

Bạn đã bao giờ cần **cách sử dụng OCR** trên một biên lai, hoá đơn, hoặc một mẫu quét và tự hỏi tại sao các ví dụ mã bạn tìm thấy đều không đầy đủ hoặc bị kẹt ở chế độ đồng bộ? Bạn không phải là người duy nhất. Trong nhiều ứng dụng thực tế, bạn muốn **trích xuất văn bản từ hình ảnh** mà không làm đóng băng giao diện người dùng, và bạn cũng muốn có sự linh hoạt để chọn ngôn ngữ phù hợp cho việc nhận dạng.  

Trong tutorial này chúng ta sẽ đi qua một ví dụ hoàn chỉnh, có thể chạy được, cho bạn thấy chính xác cách **tải hình ảnh cho OCR**, cấu hình tùy chọn **đặt ngôn ngữ OCR**, và thực hiện nhận dạng một cách bất đồng bộ. Khi hoàn thành, bạn sẽ có một ứng dụng console tự chứa, in ra văn bản đã nhận dạng lên console, cùng với một vài mẹo để xử lý các trường hợp biên và mở rộng giải pháp.

## Yêu cầu trước

- .NET 6.0 hoặc mới hơn (mã hoạt động với .NET Core và .NET Framework cũng được)  
- Gói NuGet Aspose.OCR (`Aspose.OCR`) đã được cài đặt  
- Một tệp hình ảnh mẫu (ví dụ: `receipt.jpg`) được đặt trong một thư mục bạn có thể tham chiếu  
- Kiến thức cơ bản về C# – bạn không cần các thủ thuật async nâng cao, chỉ cần những kiến thức nền tảng  

Nếu bạn thiếu bất kỳ mục nào ở trên, hãy tải gói NuGet bằng `dotnet add package Aspose.OCR` và tạo một thư mục đơn giản cho hình ảnh kiểm thử của bạn. Không cần gì phức tạp.

---

## Cách sử dụng OCR: Triển khai từng bước

Dưới đây chúng tôi chia quy trình thành bốn bước logic. Mỗi bước có tiêu đề H2 riêng, và tiêu đề đầu tiên lặp lại từ khóa chính để đáp ứng SEO.

### Bước 1 – Khởi tạo OCR Engine (Cách sử dụng OCR)

Điều đầu tiên bạn cần là một thể hiện của `OcrEngine`. Hãy nghĩ nó như bộ não phía sau hoạt động; nó chứa cấu hình, hình ảnh và kết quả.

```csharp
using System;
using System.Threading.Tasks;
using Aspose.OCR;
using Aspose.OCR.Enums;

public class AsyncExample
{
    public static async Task RunAsync()
    {
        // Create the OCR engine – this object will manage everything.
        var ocrEngine = new OcrEngine();

        // Next steps will configure it further.
```

**Tại sao điều này quan trọng:**  
Tạo engine một lần và tái sử dụng nó có thể cải thiện hiệu năng khi bạn xử lý nhiều hình ảnh. Nó cũng cho bạn một nơi duy nhất để đặt các tùy chọn toàn cục như ngôn ngữ.

### Bước 2 – Đặt ngôn ngữ OCR (Cài đặt ngôn ngữ OCR đúng cách)

Nếu bạn bỏ qua việc chọn ngôn ngữ, Aspose OCR sẽ mặc định là tiếng Anh, có thể ổn cho biên lai nhưng không phù hợp với tài liệu nước ngoài. Đặt ngôn ngữ chỉ cần một dòng:

```csharp
        // Set the recognition language to English.
        // You can change OcrLanguage.French, OcrLanguage.Spanish, etc.
        ocrEngine.Config.Language = OcrLanguage.English;
```

**Mẹo chuyên nghiệp:**  
Khi bạn cần hỗ trợ đa ngôn ngữ, bạn có thể truyền một mảng ngôn ngữ (`OcrLanguage.English | OcrLanguage.French`). Engine sẽ thử từng ngôn ngữ theo thứ tự, rất hữu ích cho các biên lai hỗn hợp ngôn ngữ.

### Bước 3 – Tải hình ảnh cho OCR (Tải hình ảnh cho OCR một cách hiệu quả)

Bây giờ chúng ta chỉ định engine tới tệp mà chúng ta muốn đọc. Aspose cung cấp `ImageStream.FromFile`, giúp ẩn đi việc xử lý stream bên dưới.

```csharp
        // Load the image you want to analyze.
        // Replace the path with the actual location of your image file.
        ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.jpg");
```

**Trường hợp đặc biệt:**  
Nếu đường dẫn tệp sai hoặc định dạng hình ảnh không được hỗ trợ, `FromFile` sẽ ném ra ngoại lệ. Hãy bọc đoạn này trong try/catch nếu bạn đang xây dựng UI mạnh mẽ.

### Bước 4 – Thực hiện nhận dạng bất đồng bộ (Trích xuất văn bản từ hình ảnh)

Đây là nơi phép thuật xảy ra. Phương thức `RecognizeAsync` chạy OCR trên một luồng nền, giải phóng luồng gọi—hoàn hảo cho UI hoặc ứng dụng web.

```csharp
        // Run OCR asynchronously.
        var ocrResult = await ocrEngine.RecognizeAsync();

        // Display the recognized text.
        Console.WriteLine("OCR completed:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Bạn sẽ thấy:**  
Nếu `receipt.jpg` chứa văn bản “Total: $12.34”, đầu ra console sẽ là:

```
OCR completed:
Total: $12.34
```

**Tại sao phải async?**  
OCR đồng bộ có thể chặn luồng trong vài giây, đặc biệt với hình ảnh độ phân giải cao. Sử dụng `await` giúp ứng dụng của bạn phản hồi nhanh và hoạt động tốt với pipeline yêu cầu của ASP.NET Core.

---

## Ví dụ đầy đủ hoạt động

Sao chép toàn bộ đoạn mã dưới đây vào một dự án console mới (`dotnet new console`) và chạy nó. Nhớ thay thế `YOUR_DIRECTORY/receipt.jpg` bằng đường dẫn thực tế tới hình ảnh của bạn.

```csharp
using System;
using System.Threading.Tasks;
using Aspose.OCR;
using Aspose.OCR.Enums;

public class AsyncExample
{
    public static async Task Main(string[] args)
    {
        await RunAsync();
    }

    public static async Task RunAsync()
    {
        // Step 1: Create the OCR engine.
        var ocrEngine = new OcrEngine();

        // Step 2: Set the OCR language (English by default).
        ocrEngine.Config.Language = OcrLanguage.English;

        // Step 3: Load the image you want to process.
        // Ensure the file exists; otherwise an exception is thrown.
        ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.jpg");

        // Step 4: Perform asynchronous OCR recognition.
        var ocrResult = await ocrEngine.RecognizeAsync();

        // Output the recognized text.
        Console.WriteLine("OCR completed:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Kết quả mong đợi** (giả sử hình ảnh chứa văn bản tiếng Anh có thể đọc được):

```
OCR completed:
Your extracted text appears here, line by line.
```

Nếu bạn nhận được một chuỗi rỗng, hãy kiểm tra lại xem hình ảnh có rõ ràng không và cài đặt ngôn ngữ có khớp với văn bản không.

---

## Những lỗi thường gặp và cách tránh

| Vấn đề | Nguyên nhân | Cách khắc phục |
|-------|----------------|-----|
| **Kết quả trống** | Hình ảnh độ phân giải thấp hoặc ngôn ngữ sai | Sử dụng bản scan độ phân giải cao hơn, hoặc đặt `ocrEngine.Config.Language` thành ngôn ngữ đúng |
| **Ngoại lệ khi `FromFile`** | Đường dẫn sai hoặc định dạng không được hỗ trợ | Kiểm tra lại đường dẫn, dùng đường dẫn tuyệt đối, hoặc chuyển đổi hình ảnh sang PNG/JPEG trước |
| **Độ trễ hiệu năng** | Xử lý lô lớn đồng bộ | Xử lý hình ảnh song song bằng `Task.WhenAll` và tái sử dụng một thể hiện `OcrEngine` duy nhất |
| **Rò rỉ bộ nhớ** | Không giải phóng stream trong mã tải tùy chỉnh | Dùng `ImageStream.FromFile` vì nó tự xử lý giải phóng, hoặc dùng khối `using` nếu bạn tự tải |

**Mẹo bổ sung:**  
Nếu bạn cần trích xuất dữ liệu có cấu trúc (ví dụ: cặp khóa‑giá trị từ biên lai), hãy xem xét xử lý hậu kỳ `ocrResult.Text` bằng biểu thức chính quy hoặc một thư viện NLP nhẹ.

---

## Mở rộng giải pháp

Bây giờ bạn đã biết **cách sử dụng OCR** cho một hình ảnh duy nhất, bạn có thể tự hỏi, “Nếu tôi có hàng chục biên lai mỗi đêm thì sao?”  

- **Xử lý batch:** Đặt logic `RunAsync` trong một vòng lặp và thu thập kết quả vào danh sách.  
- **Song song:** Sử dụng `Parallel.ForEach` với hỗ trợ async (`Parallel.ForEachAsync` trong .NET 6) để chạy nhiều nhận dạng đồng thời.  
- **Lưu trữ kết quả:** Lưu `ocrResult.Text` vào cơ sở dữ liệu, hoặc ghi ra file CSV để phân tích sau.

Tất cả các mở rộng này vẫn dựa trên các bước cốt lõi mà chúng ta đã đề cập: khởi tạo engine, đặt ngôn ngữ, tải hình ảnh, và gọi `RecognizeAsync`.

---

## Tóm tắt trực quan

![ví dụ cách sử dụng OCR](/images/ocr-example.png "cách sử dụng OCR trong C# với Aspose OCR")

*Biểu đồ trên minh họa luồng từ việc tải hình ảnh đến nhận được văn bản đã nhận dạng.*

---

## Kết luận

Chúng ta vừa đi qua một ví dụ hoàn chỉnh, sẵn sàng cho môi trường production, cho thấy **cách sử dụng OCR** trong C# để **trích xuất văn bản từ hình ảnh**, **tải hình ảnh cho OCR**, và **đặt ngôn ngữ OCR** một cách chính xác—tất cả trong khi giữ UI phản hồi nhanh nhờ các cuộc gọi bất đồng bộ.  

Trong một script tự chứa duy nhất, bạn giờ đã có mọi thứ cần thiết để bắt đầu lấy văn bản từ ảnh, biên lai, hoặc bất kỳ tài liệu quét nào. Từ đây bạn có thể mở rộng thành batch, thêm xử lý lỗi, hoặc tích hợp kết quả vào quy trình làm việc lớn hơn.

Sẵn sàng cho bước tiếp theo? Hãy thử thay `OcrLanguage.English` bằng ngôn ngữ khác, thử nghiệm với các định dạng hình ảnh khác nhau, hoặc kết nối đầu ra với một cơ sở dữ liệu đơn giản. Các khả năng rộng mở như những tài liệu bạn cần đọc.

Có câu hỏi hoặc gặp khó khăn? Để lại bình luận bên dưới, và chúc bạn lập trình vui vẻ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}