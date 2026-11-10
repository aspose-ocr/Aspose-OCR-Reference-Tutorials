---
category: general
date: 2026-03-23
description: Trích xuất văn bản từ biểu mẫu nhanh chóng bằng Aspose OCR. Tìm hiểu
  cách nhận dạng văn bản trong khu vực và xử lý phần OCR của hình ảnh với một ví dụ
  C# đầy đủ.
draft: false
keywords:
- extract text from form
- recognize text in area
- ocr part of image
- Aspose OCR C#
- region based OCR
language: vi
og_description: Trích xuất văn bản từ biểu mẫu bằng Aspose OCR. Hướng dẫn này cho
  thấy cách nhận dạng văn bản trong khu vực và xử lý phần OCR của hình ảnh trong C#.
og_title: Trích xuất văn bản từ biểu mẫu bằng Aspose OCR – Hướng dẫn đầy đủ
tags:
- C#
- OCR
- Aspose
- Image Processing
title: Trích xuất văn bản từ biểu mẫu bằng Aspose OCR – Hướng dẫn từng bước
url: /vi/net/text-recognition/extract-text-from-form-with-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Trích xuất văn bản từ biểu mẫu bằng Aspose OCR – Hướng dẫn từng bước

Bạn đã bao giờ cần **trích xuất văn bản từ biểu mẫu** nhưng toàn bộ trang lại đầy ồn ào? Bạn không phải là người duy nhất—các nhà phát triển luôn phải đấu tranh với PDF, hoá đơn đã quét, hoặc các bảng khảo sát viết tay trong đó chỉ một trường dữ liệu quan trọng. Tin tốt? Bạn có thể chỉ định cho Aspose OCR chỉ nhìn vào phần bạn quan tâm, bỏ qua phần còn lại.  

Trong hướng dẫn này chúng tôi sẽ chỉ cho bạn cách **nhận dạng văn bản trong khu vực** của một biểu mẫu đã quét, lấy ra giá trị cần thiết, và giữ phần còn lại của hình ảnh không bị thay đổi. Khi hoàn thành, bạn sẽ có một chương trình C# sẵn sàng chạy, xử lý **phần OCR của hình ảnh** mà bạn quan tâm, mà không cần gọi bất kỳ dịch vụ bên ngoài nào.

## Những gì bạn sẽ nhận được từ hướng dẫn này

- Một ứng dụng console C# đầy đủ, có thể chạy được, giúp trích xuất một trường dữ liệu từ hình ảnh biểu mẫu.  
- Giải thích rõ ràng tại sao việc nhắm mục tiêu vào một hình chữ nhật lại nhanh hơn và chính xác hơn.  
- Các mẹo xử lý kết quả rỗng, cài đặt DPI khác nhau, và biểu mẫu đa trang.  
- Danh sách kiểm tra nhanh để bạn có thể điều chỉnh mã cho dự án của mình trong vài phút.

**Prerequisites** – Bạn sẽ cần .NET 6 hoặc mới hơn, Visual Studio 2022 (hoặc bất kỳ IDE nào bạn thích), và một kết nối internet lần đầu để tải gói Aspose.OCR từ NuGet. Không cần thư viện nào khác.

---

## Trích xuất văn bản từ biểu mẫu – Cài đặt dự án

Trước khi chúng ta bắt đầu viết mã, hãy chắc chắn môi trường đã sẵn sàng. Các bước được đưa ra đơn giản vì phép màu thực sự sẽ xảy ra khi engine OCR được khởi tạo.

1. **Tạo một dự án console mới**  
   ```bash
   dotnet new console -n FormOcrDemo
   cd FormOcrDemo
   ```

2. **Thêm Aspose.OCR qua NuGet**  
   ```bash
   dotnet add package Aspose.OCR
   ```

3. **Sao chép biểu mẫu đã quét** vào thư mục dự án và đổi tên thành `form.png`.  
   (Nếu tệp của bạn là PDF, hãy xuất trang cần thiết ra PNG trước—Aspose OCR hoạt động tốt nhất với ảnh raster.)

Đó là tất cả. Các phần còn lại của hướng dẫn giả định ba bước trên đã được thực hiện.

![ví dụ trích xuất văn bản từ biểu mẫu](form-region.png "ví dụ trích xuất văn bản từ biểu mẫu")

*Văn bản thay thế hình ảnh: ví dụ trích xuất văn bản từ biểu mẫu hiển thị một vùng được đánh dấu trên tài liệu đã quét.*

## Nhận dạng văn bản trong khu vực – Xác định vùng quan tâm

Tại sao lại phải dùng một hình chữ nhật? Hãy tưởng tượng bạn có một bản quét 2 MB của toàn bộ tờ khai thuế. Chạy OCR trên toàn bộ tài liệu sẽ lãng phí CPU và có thể tạo ra các kết quả sai lệch từ các trường không liên quan. Bằng cách thu hẹp phạm vi chỉ tới các tọa độ chứa giá trị mục tiêu, bạn:

- **Rút ngắn thời gian xử lý** lên tới 80 % cho các ảnh lớn.  
- **Tăng độ chính xác** vì engine bỏ qua các đồ họa gây nhiễu.  
- **Đơn giản hoá bước hậu xử lý**—bạn biết chính xác văn bản nào sẽ xuất hiện.

Hình chữ nhật được định nghĩa bằng bốn số: `x`, `y`, `width`, và `height`. Các giá trị này đo bằng pixel từ góc trên‑trái của ảnh. Nếu bạn chưa chắc trường dữ liệu nằm ở đâu, mở ảnh trong Paint, di chuột tới góc trên‑trái để đọc giá trị X/Y, sau đó kéo để đo chiều rộng và chiều cao.

## Phần OCR của hình ảnh – Tải biểu mẫu và cấu hình engine

Bây giờ vùng đã rõ, hãy nói về engine. `OcrEngine` là trái tim của Aspose OCR. Nó tự động phát hiện ngôn ngữ, xử lý hiệu chỉnh nghiêng, và trả về một chuỗi plain‑text. Bạn cũng có thể tinh chỉnh các thuộc tính của nó—như `Resolution` hoặc `Language`—nếu biểu mẫu của bạn dùng script không phải Latin. Đối với hầu hết các biểu mẫu tiếng Anh, các giá trị mặc định hoạt động tốt.

Dưới đây là **chương trình đầy đủ, tự chứa** kết hợp mọi thứ lại với nhau. Bạn có thể sao chép‑dán vào `Program.cs` và nhấn **F5**.

```csharp
using Aspose.OCR;
using System;
using System.Drawing; // for Rectangle

class RegionExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Create the OCR engine (using ensures disposal)
        // -------------------------------------------------
        using (OcrEngine ocrEngine = new OcrEngine())
        {
            // -------------------------------------------------
            // Step 2: Load the image that contains the form
            // -------------------------------------------------
            // ImageStream.FromFile reads the file into Aspose's internal format
            // Replace "YOUR_DIRECTORY/form.png" with the actual path if needed
            ocrEngine.Image = ImageStream.FromFile("form.png");

            // -------------------------------------------------
            // Step 3: Define the region that holds the desired field
            // -------------------------------------------------
            // (x, y, width, height) – adjust these numbers for your form
            Rectangle regionOfInterest = new Rectangle(120, 350, 400, 80);

            // -------------------------------------------------
            // Step 4: Recognize text only inside the defined region
            // -------------------------------------------------
            bool success = ocrEngine.Recognize(regionOfInterest);
            string recognizedText = success ? ocrEngine.Text.Trim() : string.Empty;

            // -------------------------------------------------
            // Step 5: Display the extracted field value
            // -------------------------------------------------
            Console.WriteLine("Field value: " + (string.IsNullOrEmpty(recognizedText)
                ? "[No text detected]"
                : recognizedText));
        }

        // Keep the console window open when debugging
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

### Kết quả mong đợi

Nếu hình chữ nhật bao đúng một trường có nội dung “Invoice # 12345”, console sẽ in:

```
Field value: Invoice # 12345
```

Nếu vùng trống hoặc OCR thất bại, bạn sẽ thấy:

```
Field value: [No text detected]
```

---

## Hướng dẫn mã từng bước

Dưới đây chúng tôi chia chương trình thành các phần nhỏ, giải thích **lý do** mỗi dòng và chỉ ra những nơi bạn có thể cần điều chỉnh mã.

### Step 1: Install Aspose.OCR via NuGet *(H3)*

```bash
dotnet add package Aspose.OCR
```

*Why?* Gói NuGet chứa engine OCR gốc, các tệp dữ liệu ngôn ngữ, và một lớp .NET mỏng. Nếu không có nó, lớp `OcrEngine` sẽ không tồn tại.

### Step 2: Initialize OcrEngine *(H3)*

```csharp
using (OcrEngine ocrEngine = new OcrEngine())
```

*Why use `using`?* `OcrEngine` giữ các tài nguyên không quản lý (DLL gốc, bộ đệm ảnh). Câu lệnh `using` đảm bảo chúng được giải phóng, ngăn ngừa rò rỉ bộ nhớ trong các dịch vụ chạy lâu.

### Step 3: Load the Form Image *(H3)*

```csharp
ocrEngine.Image = ImageStream.FromFile("form.png");
```

*Why `ImageStream`?* Nó trừu tượng hoá việc I/O file và tự động chuyển đổi các định dạng phổ biến (PNG, JPEG, TIFF) thành biểu diễn bitmap nội bộ mà Aspose OCR yêu cầu.

### Step 4: Specify the Region to Extract Text *(H3)*

```csharp
Rectangle regionOfInterest = new Rectangle(120, 350, 400, 80);
```

*Why a `Rectangle`?* Engine OCR chấp nhận một `System.Drawing.Rectangle`. Bốn tham số cho phép bạn xác định chính xác trường dữ liệu, loại bỏ phần còn lại của trang.

*Tip:* Nếu cần hỗ trợ nhiều trường, lưu mỗi hình chữ nhật trong một `Dictionary<string, Rectangle>` và lặp qua chúng.

### Step 5: Run Recognition and Retrieve Result *(H3)*

```csharp
bool success = ocrEngine.Recognize(regionOfInterest);
string recognizedText = success ? ocrEngine.Text.Trim() : string.Empty;
```

*Why check `success`?* OCR có thể thất bại vì nhiều lý do—ảnh mờ, ngôn ngữ không được hỗ trợ, hoặc vùng trống. Kiểm tra giá trị boolean ngăn bạn làm việc với dữ liệu lỗi thời.

### Step 6: Handle Edge Cases and Common Pitfalls *(H3)*

- **Different DPI:** Nếu bản quét có độ phân giải thấp (< 150 DPI), tăng `ocrEngine.Image.DpiX` và `ocrEngine.Image.DpiY` trước khi gọi `Recognize`.  
- **Multiple Pages:** Đối với PDF đa trang, xuất mỗi trang thành PNG riêng và lặp lại logic hình chữ nhật cho mỗi trang.  
- **Non‑English Text:** Đặt `ocrEngine.Language = Language.Thai;` (hoặc bất kỳ ngôn ngữ nào được hỗ trợ) trước khi nhận dạng.  
- **Noise Reduction:** `ocrEngine.Image.Filters.Add(new GaussianBlurFilter(1.2f));` có thể cải thiện kết quả trên ảnh nhiễu.

## Tiến xa hơn – Các biến thể thực tế

### Trích xuất nhiều trường từ cùng một biểu mẫu

Nếu bạn cần lấy “Name”, “Date”, và “Amount” từ một tài liệu, tạo một collection:

```csharp
var fields = new Dictionary<string, Rectangle>
{
    { "Name",   new Rectangle(50, 200, 300, 60) },
    { "Date",   new Rectangle(400, 200, 200, 60) },
    { "Amount", new Rectangle(650, 200, 250, 60) }
};

foreach (var kvp in fields)
{
    bool ok = ocrEngine.Recognize(kvp.Value);
    Console.WriteLine($"{kvp.Key}: {(ok ? ocrEngine.Text.Trim() : "[Not found]")}");
}
```

### Tích hợp với cơ sở dữ liệu

Sau khi trích xuất, bạn có thể muốn lưu kết quả vào SQL Server:

```csharp
using (var conn = new SqlConnection(connectionString))
{
    conn.Open();
    var cmd = new SqlCommand(
        "INSERT INTO FormResults (FieldName, FieldValue) VALUES (@name, @value)", conn);
    cmd.Parameters.AddWithValue("@name", "InvoiceNumber");
    cmd.Parameters.AddWithValue("@value", recognizedText);
    cmd.ExecuteNonQuery();
}
```

### Tự động hoá trên máy chủ

Nếu bạn dự định chạy này như một dịch vụ nền, bọc logic trong một phương thức `async` và dùng `Task.Run` để giữ UI phản hồi. Đừng quên đặt `ocrEngine.ParallelProcessing = true;` để tăng tốc trên đa lõi.

## Kết luận

Bạn giờ đã có một cách tiếp cận vững chắc, sẵn sàng sản xuất để **trích xuất văn bản từ biểu mẫu** bằng Aspose OCR. Bằng cách tập trung vào một hình chữ nhật cụ thể

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}