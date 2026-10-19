---
category: general
date: 2026-03-07
description: Ví dụ Aspose OCR cho thấy cách bật kiểm tra chính tả, thêm từ điển tùy
  chỉnh, tải OCR hình ảnh và nhanh chóng sửa lỗi OCR.
draft: false
keywords:
- aspose ocr example
- how to enable spellcheck
- how to add dictionary
- load image ocr
- how to fix ocr errors
language: vi
og_description: Ví dụ Aspose OCR hướng dẫn bạn cách bật kiểm tra chính tả, thêm từ
  điển tùy chỉnh, tải hình ảnh để OCR và sửa các lỗi OCR thường gặp.
og_title: Ví dụ OCR Aspose – Bật kiểm tra chính tả & Sửa lỗi
tags:
- Aspose
- OCR
- C#
- SpellCheck
title: Ví dụ Aspose OCR – Bật kiểm tra chính tả và sửa lỗi trong C#
url: /vi/net/ocr-optimization/aspose-ocr-example-enable-spellcheck-and-fix-errors-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ví dụ Aspose OCR – Bật Kiểm tra Chính tả và Sửa Lỗi trong C#

Bạn đã bao giờ cần một **ví dụ Aspose OCR** không chỉ đọc văn bản từ hình ảnh mà còn làm sạch những lỗi chính tả phiền phức chưa? Bạn không phải là người duy nhất. Trong nhiều dự án thực tế, đầu ra OCR thô đầy những lỗi đánh máy, đặc biệt khi hình ảnh nguồn chứa phông chữ ít tương phản hoặc ghi chú viết tay.  

Tin tốt? Với Aspose.OCR bạn có thể **bật kiểm tra chính tả**, tích hợp từ điển của riêng mình, và nhận được một chuỗi đã được làm sạch chỉ trong vài dòng mã. Dưới đây bạn sẽ thấy chính xác **cách bật kiểm tra chính tả**, **cách thêm từ điển**, và **cách tải OCR hình ảnh** để cuối cùng **sửa lỗi OCR** mà không phải đau đầu.

Trong hướng dẫn này, chúng ta sẽ bao phủ mọi thứ bạn cần—từ cài đặt NuGet đến một chương trình hoàn chỉnh, có thể chạy được và in ra văn bản đã được sửa. Khi kết thúc, bạn sẽ có một **ví dụ Aspose OCR** vững chắc mà bạn có thể chèn ngay vào bất kỳ dự án .NET nào.

## Yêu cầu trước

- .NET 6.0 SDK hoặc phiên bản mới hơn (mã hoạt động với .NET Core và .NET Framework cũng được)
- Visual Studio 2022 hoặc bất kỳ IDE nào hỗ trợ C#
- Một tệp hình ảnh (`typed_text.png`) chứa văn bản tiếng Anh rõ ràng, được gõ
- Kết nối Internet để tải gói NuGet Aspose.OCR

Không cần thư viện bên thứ ba nào khác.

---

## Bước 1 – Cài đặt Gói NuGet Aspose.OCR (Tải OCR Hình ảnh)

Trước khi chúng ta có thể viết bất kỳ mã nào, chúng ta cần thư viện cung cấp động cơ OCR.

```bash
dotnet add package Aspose.OCR
```

> **Mẹo chuyên nghiệp:** Nếu bạn đang dùng Visual Studio, nhấp chuột phải vào dự án → *Manage NuGet Packages* → tìm **Aspose.OCR** và nhấn *Install*.  

Cài đặt gói sẽ cho bạn quyền truy cập vào `OcrEngine`, `ImageStream`, và các tiện ích kiểm tra chính tả tích hợp mà chúng ta sẽ dùng sau. Khi gói đã sẵn sàng, bạn đã sẵn sàng để **tải OCR hình ảnh**.

## Bước 2 – Tạo Instance cho Engine OCR

Tạo engine là bước cụ thể đầu tiên trong bất kỳ **ví dụ Aspose OCR** nào. Hãy nghĩ về `OcrEngine` như bộ não sẽ phân tích bitmap và xuất ra văn bản.

```csharp
using Aspose.OCR;
using Aspose.OCR.SpellCheck;

// Step 2: Initialize the OCR engine
var ocrEngine = new OcrEngine();
```

Constructor của `OcrEngine` không yêu cầu bất kỳ tham số nào, giúp nó gọn gàng và tiện lợi cho các prototype nhanh.

## Bước 3 – Cách Bật Kiểm tra Chính tả (và Tại sao Điều này Quan trọng)

Đầu ra OCR thô thường chứa các từ bị nhận dạng sai như “teh” thay vì “the”. Bật bộ kiểm tra chính tả tích hợp cho phép Aspose tự động thay thế những lỗi đó bằng cách viết đúng nhất có thể.

```csharp
// Step 3: Turn on spell checking and set the language to English
ocrEngine.Settings.SpellCheck.Enabled = true;
ocrEngine.Settings.SpellCheck.Language = SpellCheckLanguage.English;
```

> **Tại sao bật kiểm tra chính tả?**  
> - **Độ chính xác:** Kiểm tra chính tả sau xử lý có thể tăng độ chính xác tổng thể của văn bản lên 10‑15 % cho tài liệu in.  
> - **Trải nghiệm người dùng:** Văn bản sạch sẽ đồng nghĩa với việc giảm công việc làm sạch ở các bước tiếp theo khi bạn đưa kết quả vào chỉ mục tìm kiếm hoặc pipeline phân tích.

## Bước 4 – Cách Thêm Từ điển (Từ ngữ Tùy chỉnh)

Đôi khi từ điển mặc định không nhận biết các tên thương hiệu, mã sản phẩm, hoặc thuật ngữ chuyên ngành của bạn. Đó là lúc **cách thêm từ điển** trở nên cần thiết.

```csharp
// Step 4: Add custom words that the spell checker should accept
ocrEngine.Settings.SpellCheck.CustomDictionary.AddWords(new[]
{
    "AsposeOCR",   // our library name
    "OCRify",      // a fictional product
    "CSharpify"    // another custom term
});
```

Bạn có thể cung cấp một mảng, một danh sách, hoặc thậm chí đọc từ tệp nếu có một từ vựng tùy chỉnh lớn. Bộ kiểm tra chính tả sẽ coi những mục này là hợp lệ, ngăn ngừa các sửa chữa sai.

## Bước 5 – Tải Hình ảnh cho OCR (Tải OCR Hình ảnh)

Bây giờ engine đã được cấu hình, chúng ta cần chỉ định nó tới hình ảnh muốn đọc. Trợ giúp `ImageStream.FromFile` ẩn đi các chi tiết đọc tệp.

```csharp
// Step 5: Load the image that contains the text to be recognized
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/typed_text.png");
```

> **Mẹo:** Nếu hình ảnh của bạn nằm trong thư mục con của dự án, đặt thuộc tính *Copy to Output Directory* thành *Copy always* để đường dẫn được giải quyết khi chạy.

## Bước 6 – Thực hiện Nhận dạng và Sửa Lỗi OCR

Khi mọi thứ đã sẵn sàng, một lần gọi `Recognize()` sẽ chạy pipeline OCR, áp dụng kiểm tra chính tả, và lưu kết quả đã làm sạch vào `ocrEngine.Text`.

```csharp
// Step 6: Run OCR and let the spell checker clean the output
ocrEngine.Recognize();

// Step 7: Output the corrected text to the console
Console.WriteLine("Corrected text:");
Console.WriteLine(ocrEngine.Text);
```

### Kết quả Dự kiến

Giả sử `typed_text.png` chứa câu `The quick brown fox jumps over teh lazy dog`, console sẽ hiển thị:

```
Corrected text:
The quick brown fox jumps over the lazy dog
```

Chú ý cách “teh” đã được tự động sửa thành “the”. Nếu bạn đã thêm “OCRify” vào từ điển tùy chỉnh và hình ảnh chứa từ đó, engine sẽ giữ nguyên nó.

---

## Ví dụ Hoàn chỉnh (Sẵn sàng Sao chép‑Dán)

Dưới đây là chương trình đầy đủ mà bạn có thể chèn vào một dự án console mới. Nó bao gồm tất cả các bước ở trên, cộng thêm một vài chú thích để rõ ràng.

```csharp
// ---------------------------------------------------------------
// Aspose OCR Example – Enable Spellcheck and Fix Errors
// ---------------------------------------------------------------

using System;
using Aspose.OCR;
using Aspose.OCR.SpellCheck;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create the OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Enable spell checking (how to enable spellcheck)
            ocrEngine.Settings.SpellCheck.Enabled = true;
            ocrEngine.Settings.SpellCheck.Language = SpellCheckLanguage.English;

            // 3️⃣ Add custom words (how to add dictionary)
            ocrEngine.Settings.SpellCheck.CustomDictionary.AddWords(new[]
            {
                "AsposeOCR",
                "OCRify",
                "CSharpify"
            });

            // 4️⃣ Load the image (load image OCR)
            // Replace the path with the actual location of your image file
            ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/typed_text.png");

            // 5️⃣ Run OCR – this also fixes common OCR errors (how to fix ocr errors)
            ocrEngine.Recognize();

            // 6️⃣ Show the corrected result
            Console.WriteLine("Corrected text:");
            Console.WriteLine(ocrEngine.Text);
        }
    }
}
```

Lưu tệp này dưới tên `Program.cs`, chạy `dotnet run`, và bạn sẽ thấy câu đã được sửa được in ra console.

---

## Câu hỏi Thường gặp & Trường hợp Đặc biệt

| Câu hỏi | Trả lời |
|----------|--------|
| **Nếu hình ảnh là PDF đa trang thì sao?** | Aspose.OCR có thể xử lý các trang PDF dưới dạng hình ảnh. Sử dụng `ocrEngine.Image = ImageStream.FromPdf("file.pdf", pageNumber: 1);` và lặp qua các trang. |
| **Tôi có thể đổi ngôn ngữ sang thứ khác ngoài tiếng Anh không?** | Chắc chắn. Đặt `ocrEngine.Settings.SpellCheck.Language = SpellCheckLanguage.French;` (hoặc bất kỳ ngôn ngữ nào được hỗ trợ). |
| **Từ điển tùy chỉnh của tôi rất lớn—sẽ ảnh hưởng tới hiệu năng không?** | Thêm hàng ngàn từ sẽ tốn một chi phí ban đầu nhỏ, nhưng việc tra cứu là O(1) nhờ hash‑set bên trong. Đối với từ vựng rất lớn, hãy cân nhắc tải chúng một lần khi ứng dụng khởi động. |
| **Nếu engine OCR ném ngoại lệ khi hình ảnh bị hỏng thì sao?** | Bao bọc `Recognize()` trong khối try‑catch và kiểm tra `ocrEngine.LastError`. Bạn cũng có thể kiểm tra trước kích thước hình ảnh bằng `ocrEngine.Image.Width` và `Height`. |
| **Tôi có cần giấy phép cho việc sử dụng trong môi trường production không?** | Bản đánh giá miễn phí hoạt động cho việc thử nghiệm, nhưng giấy phép thương mại sẽ loại bỏ watermark đánh giá và mở khóa hiệu năng đầy đủ. |

---

## Kết luận

Bây giờ bạn đã có một **ví dụ Aspose OCR hoàn chỉnh** thể hiện **cách bật kiểm tra chính tả**, **cách thêm từ điển**, **tải OCR hình ảnh**, và **cách sửa lỗi OCR** một cách sạch sẽ, sẵn sàng cho production. Bằng cách cấu hình bộ kiểm tra chính tả và cung cấp danh sách từ tùy chỉnh, bạn cải thiện đáng kể chất lượng văn bản đã trích xuất mà không cần viết bất kỳ logic xử lý hậu kỳ nào.

Sẵn sàng cho bước tiếp theo? Hãy thử đổi ngôn ngữ sang tiếng Tây Ban Nha, đưa vào một PDF đa trang, hoặc tích hợp kết quả vào chỉ mục Azure Cognitive Search có khả năng tìm kiếm. Mẫu tương tự vẫn áp dụng—chỉ cần điều chỉnh cờ ngôn ngữ và có thể mở rộng từ điển tùy chỉnh.

Nếu bạn thấy hướng dẫn này hữu ích, hãy đánh dấu sao trên GitHub, chia sẻ với đồng nghiệp, hoặc để lại bình luận bên dưới. Chúc lập trình vui vẻ, và hy vọng kết quả OCR của bạn luôn không lỗi!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}