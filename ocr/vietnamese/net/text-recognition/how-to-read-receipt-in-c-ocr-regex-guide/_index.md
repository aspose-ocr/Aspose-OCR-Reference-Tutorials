---
category: general
date: 2026-02-13
description: Cách đọc biên lai nhanh chóng bằng Aspose OCR và trích xuất số tiền bằng
  regex. Học quy trình xử lý biên lai từng bước với OCR.
draft: false
keywords:
- how to read receipt
- extract amount using regex
- regex find total
- process receipt with ocr
language: vi
og_description: Cách đọc biên lai trong C# sử dụng Aspose OCR và regex. Hướng dẫn
  này cho bạn thấy cách xử lý biên lai bằng OCR và trích xuất tổng số tiền.
og_title: Cách Đọc Biên Lai trong C# – Hướng Dẫn Toàn Diện về OCR & Regex
tags:
- OCR
- C#
- Regex
- Aspose
title: Cách Đọc Biên Lai trong C# – Hướng Dẫn OCR + Regex
url: /vi/net/text-recognition/how-to-read-receipt-in-c-ocr-regex-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Đọc Hóa Đơn trong C# – Hướng Dẫn OCR + Regex

Bạn đã bao giờ tự hỏi **cách đọc hình ảnh hóa đơn** mà không phải gõ tay từng dòng chưa? Trong nhiều ứng dụng doanh nghiệp nhỏ, bạn cần lấy tổng số tiền từ một bức ảnh của hóa đơn, và việc làm thủ công sẽ làm mất ý nghĩa của tự động hoá. Tin tốt là gì? Với Aspose OCR, bạn có thể để engine thực hiện công việc nặng, sau đó một biểu thức chính quy đơn giản sẽ tìm ra tổng. Trong hướng dẫn này, chúng ta sẽ đi qua **process receipt with OCR**, trích xuất số tiền bằng regex, và có được giá trị tổng sẵn sàng sử dụng.

Bạn sẽ thấy một ví dụ đầy đủ, có thể chạy được, khám phá tại sao mô hình ngôn ngữ cho hóa đơn lại quan trọng, và nhận các mẹo để xử lý các trường hợp đặc biệt như ký hiệu tiền tệ khác nhau hoặc thiếu nhãn “Total”. Không cần tài liệu bên ngoài—mọi thứ bạn cần đều có ở đây.

## Những Điều Bạn Sẽ Học

- Cách thiết lập Aspose OCR cho nhận dạng chuyên biệt hóa đơn (mô hình ngôn ngữ `Receipt` tự động chỉnh nghiêng và giảm nhiễu ảnh).  
- Cách áp dụng một biểu thức chính quy **extract amount using regex** phù hợp với hầu hết các hóa đơn kiểu Mỹ.  
- Cách xử lý các biến thể phổ biến như “TOTAL”, “Total:”, hoặc “Grand Total – $12.34”.  
- Cách xuất kết quả một cách an toàn và cách xử lý khi không tìm thấy mẫu.

**Điều kiện tiên quyết**: .NET 6+ (hoặc .NET Framework 4.7+), giấy phép Aspose OCR hợp lệ hoặc bản dùng thử, và một ảnh hóa đơn được lưu cục bộ. Đó là tất cả—không cần thêm gói NuGet nào ngoài Aspose.OCR.

---

## Bước 1 – Cài Đặt Aspose OCR và Chuẩn Bị Dự Án

### Tại sao lại quan trọng

Aspose OCR cung cấp một mô hình **process receipt with OCR** được thiết kế riêng, biết cách làm thẳng một tờ giấy nhăn và bỏ qua nhiễu nền. Sử dụng mô hình văn bản chung sẽ gây ra nhiều lỗi hơn, đặc biệt với các bản scan độ phân giải thấp.

### Code

```csharp
// Install the package via NuGet first:
//   dotnet add package Aspose.OCR
using Aspose.OCR;
using Aspose.OCR.Enums;
using System.Text.RegularExpressions;

// If you have a license file, load it now (optional but removes trial watermark)
var license = new Aspose.OCR.License();
license.SetLicense("Aspose.OCR.lic");
```

> **Mẹo chuyên nghiệp:** Đặt file giấy phép ra ngoài thư mục kiểm soát nguồn để tránh commit nhầm.

---

## Bước 2 – Cấu Hình Engine OCR cho Nhận Dạng Hóa Đơn

### Tại sao lại quan trọng

Mô hình ngôn ngữ `Receipt` bao gồm tính năng chỉnh nghiêng và giảm nhiễu tích hợp, giúp cải thiện độ chính xác đáng kể trên các hóa đơn thực tế thường bị gập hoặc nhăn.

### Code

```csharp
// Step 2: Create and configure the OCR engine for receipt processing
var ocrEngine = new OcrEngine
{
    // Receipt model is optimized for invoices, grocery receipts, etc.
    Language = OcrLanguage.Receipt
};
```

---

## Bước 3 – Nhận Dạng Văn Bản Từ Ảnh Hóa Đơn

### Tại sao lại quan trọng

Bạn cần văn bản thô trước khi áp dụng bất kỳ regex nào. Phương thức `RecognizeImage` trả về một `OcrResult` chứa toàn bộ chuỗi, điểm tin cậy, và các thông tin khác nếu bạn cần sau này.

### Code

```csharp
// Step 3: Recognize text from the receipt image
// Replace the path with the actual location of your receipt file.
string receiptPath = @"C:\Receipts\sample-receipt.jpg";

OcrResult receiptResult = ocrEngine.RecognizeImage(receiptPath);

// Quick sanity check – print the whole OCR output (helps debugging)
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(receiptResult.Text);
Console.WriteLine("===================\n");
```

**Kết quả OCR dự kiến (ví dụ)**  
```
Walmart Supercenter
123 Main St.
Anytown, USA
Date: 02/12/2026
Item A   $3.45
Item B   $7.89
Subtotal $11.34
Tax      $0.91
Total:   $12.25
Thank you!
```

---

## Bước 4 – Xây Dựng Regex để **Extract Amount Using Regex**

### Tại sao lại quan trọng

Hóa đơn có nhiều định dạng, nhưng từ “Total” (hoặc biến thể gần giống) theo sau là một số tiền đô la là một mốc đáng tin cậy. Mẫu dưới đây chấp nhận khoảng trắng tùy chọn, dấu hai chấm, dấu gạch ngang, và dấu `$` tùy chọn.

### Code

```csharp
// Step 4: Use a regular expression to locate the total amount in the recognized text
string pattern = @"Total\s*[:\-]?\s*\$?(\d+(\.\d{2})?)";
RegexOptions options = RegexOptions.IgnoreCase;

Match totalMatch = Regex.Match(receiptResult.Text, pattern, options);
```

**Giải thích mẫu**

| Phần | Ý nghĩa |
|------|---------|
| `Total` | Tìm từ “Total” (không phân biệt chữ hoa/thường). |
| `\s*[:\-]?` | Cho phép bất kỳ khoảng trắng nào, sau đó là dấu hai chấm hoặc gạch ngang tùy chọn. |
| `\s*\$?` | Khoảng trắng tùy chọn và dấu đô la `$` tùy chọn. |
| `(\d+(\.\d{2})?)` | Bắt một hoặc nhiều chữ số, có thể theo sau là dấu thập phân và hai chữ số thập phân. |

---

## Bước 5 – Xuất Tổng Được Trích Xuất Hoặc Xử Lý Khi Dữ Liệu Thiếu

### Tại sao lại quan trọng

Ngay cả OCR tốt nhất cũng có thể bỏ lỡ một từ, đặc biệt trên các hóa đơn mờ. Cung cấp một cách dự phòng mềm mại ngăn ngừa lỗi và cho phép bạn thêm logic tùy chỉnh (ví dụ: yêu cầu người dùng xác nhận).

### Code

```csharp
// Step 5: Output the extracted total, or indicate it wasn't found
if (totalMatch.Success)
{
    string amount = totalMatch.Groups[1].Value;
    Console.WriteLine($"Total: ${amount}");
}
else
{
    Console.WriteLine("Total amount not found. Consider reviewing the OCR output manually.");
}
```

**Ví dụ đầu ra console**

```
Total: $12.25
```

---

## Ví Dụ Hoàn Chỉnh – Tất Cả Các Bước Trong Một File

Dưới đây là một chương trình tự chứa, bạn có thể sao chép‑dán vào dự án console. Nó bao gồm chú thích, xử lý lỗi, và tải giấy phép tùy chọn.

```csharp
// ---------------------------------------------------------------
// How to Read Receipt in C# – OCR + Regex (Complete Example)
// ---------------------------------------------------------------
using Aspose.OCR;
using Aspose.OCR.Enums;
using System;
using System.Text.RegularExpressions;

class Program
{
    static void Main()
    {
        // 0️⃣ Optional: Load your Aspose OCR license (remove trial watermark)
        try
        {
            var license = new Aspose.OCR.License();
            license.SetLicense("Aspose.OCR.lic"); // path to .lic file
        }
        catch (Exception ex)
        {
            Console.WriteLine("License not found – running in trial mode.");
        }

        // 1️⃣ Configure the OCR engine for receipt processing
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.Receipt // receipt model = de‑skew + de‑noise
        };

        // 2️⃣ Path to the receipt image (change to your file)
        string receiptPath = @"YOUR_DIRECTORY/receipt.jpg";

        // 3️⃣ Perform OCR
        OcrResult receiptResult = ocrEngine.RecognizeImage(receiptPath);

        // 4️⃣ Debug: show full OCR text (helps when regex fails)
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(receiptResult.Text);
        Console.WriteLine("===================\n");

        // 5️⃣ Regex to **extract amount using regex** (find the total)
        string pattern = @"Total\s*[:\-]?\s*\$?(\d+(\.\d{2})?)";
        Match totalMatch = Regex.Match(receiptResult.Text, pattern,
                                        RegexOptions.IgnoreCase);

        // 6️⃣ Output
        if (totalMatch.Success)
        {
            string amount = totalMatch.Groups[1].Value;
            Console.WriteLine($"Total: ${amount}");
        }
        else
        {
            Console.WriteLine("Total amount not found. You might need to adjust the regex or improve image quality.");
        }
    }
}
```

**Chạy chương trình**

1. Tạo một dự án console mới (`dotnet new console -n ReceiptReader`).  
2. Thêm gói NuGet Aspose.OCR (`dotnet add package Aspose.OCR`).  
3. Thay thế `YOUR_DIRECTORY/receipt.jpg` bằng đường dẫn thực tế tới ảnh hóa đơn.  
4. Biên dịch và chạy (`dotnet run`).  

Bạn sẽ thấy kết quả OCR được in ra, sau đó là `Total: $xx.xx` nếu mọi thứ khớp.

---

## Xử Lý Các Trường Hợp Đặc Biệt & Biến Thể Thông Thường

### 1. Ký Hiệu Tiền Tệ Khác

Nếu bạn làm việc với euro (€) hoặc bảng Anh (£), mở rộng mẫu:

```csharp
string pattern = @"Total\s*[:\-]?\s*[$€£]?\s*(\d+(\.\d{2})?)";
```

### 2. Thiếu Nhãn “Total”

Một số hóa đơn chỉ hiển thị “Grand Total”. Thêm một lựa chọn:

```csharp
string pattern = @"(?:Total|Grand\s*Total)\s*[:\-]?\s*[$]?\s*(\d+(\.\d{2})?)";
```

### 3. Nhiều Tổng (ví dụ, “Subtotal” và “Total”)

Nếu regex khớp với lần xuất hiện đầu tiên, bạn có thể muốn **lần cuối cùng**:

```csharp
MatchCollection matches = Regex.Matches(receiptResult.Text, pattern,
                                         RegexOptions.IgnoreCase);
Match last = matches.Count > 0 ? matches[matches.Count - 1] : null;
```

### 4. Ảnh Độ Phân Giải Thấp

- Tăng DPI khi scan (`300 DPI` là mức lý tưởng).  
- Tiền xử lý ảnh bằng bộ lọc giảm nhòe đơn giản trước khi đưa vào Aspose (không nằm trong phạm vi hướng dẫn này, nhưng đáng khám phá).

---

## Mẹo Chuyên Nghiệp Cho Dự Án Thực Tế

- **Cache kết quả OCR** nếu bạn cần trích xuất nhiều trường (thuế, mặt hàng, v.v.) – bạn chỉ trả chi phí OCR một lần.  
- **Ghi log văn bản OCR thô** vào cơ sở dữ liệu; nó trở thành một vết audit quý giá cho các chi phí tranh chấp.  
- Khi xây dựng API web, **chạy OCR trong worker nền**; nó có thể mất vài trăm miligiây, đủ cho xử lý bất đồng bộ nhưng không lý tưởng cho yêu cầu đồng bộ.  
- **Xác thực số tiền đã trích xuất** theo quy tắc kinh doanh (ví dụ: số tiền phải > 0) trước khi lưu.

---

## Kết Luận

Chúng ta đã khám phá **cách đọc hình ảnh hóa đơn** trong C# bằng Aspose OCR, sau đó **extract amount using regex** để tìm dòng tổng một cách đáng tin cậy. Bằng cách tận dụng mô hình ngôn ngữ `Receipt`, bạn nhận được văn bản đã được chỉnh nghiêng, giảm nhiễu, và một biểu thức chính quy ngắn gọn xử lý phần lớn các quirks định dạng. Đoạn mã hoàn chỉnh ở trên sẵn sàng đưa vào bất kỳ dự án .NET console hoặc service nào, và các đề xuất cho các trường hợp đặc biệt cung cấp nền tảng vững chắc cho việc triển khai thực tế.

Sẵn sàng cho bước tiếp theo? Hãy thử mở rộng giải pháp để lấy từng mục hàng, tính thuế tự động, hoặc tích hợp với API theo dõi chi phí. Và nếu gặp một hóa đơn phá vỡ mẫu, hãy nhớ rằng **regex find total** chỉ là điểm khởi đầu—bạn luôn có thể điều chỉnh mẫu để phù hợp với địa phương của mình.

Chúc lập trình vui vẻ, và hy vọng quá trình xử lý hóa đơn của bạn sẽ nhanh, chính xác và hoàn toàn tự động!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}