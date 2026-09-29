---
category: general
date: 2026-02-20
description: Tìm hiểu cách đọc biên lai trong C# bằng cách trích xuất văn bản từ hình
  ảnh và chuyển đổi sang JSON. Mã từng bước sử dụng Aspose OCR.
draft: false
keywords:
- how to read receipt
- extract text from image
- convert image to json
- load image file c#
- OCR receipt C#
- Aspose OCR tutorial
language: vi
og_description: Khám phá cách đọc biên lai trong C# bằng cách tải tệp hình ảnh, trích
  xuất văn bản với Aspose OCR và chuyển kết quả sang JSON. Ví dụ mã đầy đủ.
og_title: Cách Đọc Biên Lai trong C# – Trích xuất Văn bản, Chuyển đổi sang JSON
tags:
- C#
- OCR
- Image Processing
- JSON
title: Cách đọc biên lai trong C# – Hướng dẫn đầy đủ để trích xuất văn bản từ hình
  ảnh
url: /vi/net/text-recognition/how-to-read-receipt-in-c-complete-guide-to-extract-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Đọc Hóa Đơn trong C# – Hướng Dẫn Toàn Diện

Bạn đã bao giờ tự hỏi **how to read receipt** ảnh một cách lập trình chưa? Có thể bạn đang xây dựng một ứng dụng theo dõi chi phí và cần trích xuất các mục chi từ một bức ảnh hóa đơn tạp hóa. Theo kinh nghiệm của tôi, điểm đau lớn nhất là biến JPEG mờ thành dữ liệu có cấu trúc mà bạn thực sự có thể sử dụng. Tin tốt là gì? Chỉ với vài dòng C# và Aspose OCR, bạn có thể **extract text from image**, sau đó **convert image to JSON** một cách gần như kỳ diệu.

Trong tutorial này, bạn sẽ có một giải pháp sẵn sàng chạy được **loads an image file C#**, thực hiện OCR và xuất ra một payload JSON chi tiết. Không cần dịch vụ bên ngoài, không cần các cuộc gọi REST rắc rối—chỉ là mã .NET thuần túy mà bạn có thể chèn vào bất kỳ dự án console hoặc ASP.NET nào. Khi hoàn thành, bạn sẽ hiểu tại sao mỗi bước lại quan trọng, cách xử lý các trường hợp biên thường gặp (như kích thước hóa đơn không chuẩn), và JSON đầu ra thực sự trông như thế nào.

## Những gì bạn cần

- **.NET 6.0 trở lên** – mã sử dụng `System.Drawing.Common` hỗ trợ trên Windows, Linux và macOS.  
- **Aspose.OCR for .NET** – bạn có thể tải gói NuGet dùng thử miễn phí (`Aspose.OCR`) hoặc dùng bản có giấy phép nếu đã có.  
- Một **hình ảnh mẫu hóa đơn** (`receipt.jpg`) đặt ở vị trí mà ứng dụng của bạn có thể đọc được.  
- Bất kỳ IDE nào bạn thích (Visual Studio, Rider, VS Code).  

Đó là tất cả. Không cần cấu hình thêm, không cần khóa API.

---

## Bước 1 – Load the Image File C# (Primary Keyword in Action)

Trước khi engine OCR thực hiện phép màu, bạn phải đưa ảnh vào bộ nhớ. Đây là bước “load image file C#” cổ điển mà nhiều nhà phát triển thường bỏ qua.

```csharp
using System.Drawing;          // Required for Image
using Aspose.OCR;
using Aspose.OCR.Models;

// Path to your receipt image – adjust as needed
string imagePath = @"C:\Receipts\receipt.jpg";

// Load the image into a System.Drawing.Image object
Image receiptImage = Image.FromFile(imagePath);
```

**Tại sao lại quan trọng:**  
`Image.FromFile` đọc file *một lần* và giữ một handle mở, rất phù hợp cho một lần OCR nhanh. Nếu bạn xử lý nhiều hóa đơn trong vòng lặp, hãy cân nhắc dùng `Image.FromStream` để tránh khóa file.

> **Mẹo chuyên nghiệp:** Nếu gặp *FileNotFoundException*, hãy kiểm tra lại đường dẫn và chắc chắn rằng ảnh thực sự tồn tại. Đường dẫn tương đối cũng hoạt động (`"./receipt.jpg"`), nhưng đường dẫn tuyệt đối an toàn hơn cho môi trường production.

---

## Bước 2 – Create and Configure the OCR Engine

Aspose OCR đi kèm với một `OcrEngine` đã được chuẩn bị sẵn. Bạn không cần đào tạo mô hình; thư viện đã biết cách đọc văn bản in, chính là những gì hầu hết hóa đơn sử dụng.

```csharp
// Instantiate the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Optional: tweak recognition settings if your receipts are low‑contrast
ocrEngine.Config.Language = OcrLanguage.English;
ocrEngine.Config.DetectOrientation = true;   // Handles rotated receipts
```

**Tại sao chúng ta thiết lập các tùy chọn này:**  
`DetectOrientation` yêu cầu engine tự động xoay ảnh nếu hóa đơn được quét ngược. Đặt ngôn ngữ giúp thu hẹp bộ ký tự, cải thiện độ chính xác—đặc biệt khi bạn chỉ cần dữ liệu alphanumeric tiếng Anh.

---

## Bước 3 – Recognize the Image and Convert to JSON

Bây giờ là phần thú vị: **extract text from image** và **convert image to JSON** trong một lời gọi duy nhất.

```csharp
// Perform OCR and get the result as a JSON string
string jsonResult = ocrEngine.RecognizeToJson(receiptImage);
```

Phương thức `RecognizeToJson` trả về một cấu trúc JSON phong phú bao gồm:

- `Text`: văn bản thuần được nối lại.  
- `Lines`: mảng các đối tượng dòng kèm tọa độ.  
- `Words`: mỗi từ kèm điểm tin cậy.  
- `Regions`: các hộp bao quanh các khối văn bản được phát hiện.

Bạn có thể deserialize JSON này thành một đối tượng C# nếu cần truy cập kiểu, nhưng trong nhiều trường hợp việc in thô JSON đã đủ.

---

## Bước 4 – Output the JSON (or Store It)

Hãy xem kết quả và thảo luận về cách xử lý.

```csharp
// Write the JSON to the console – perfect for quick debugging
Console.WriteLine(jsonResult);

// Bonus: Save the JSON to a file for later processing
File.WriteAllText("receipt_output.json", jsonResult);
```

### Kết quả mẫu

```json
{
  "Text":"Walmart\n123 Main St\nItem A  $2.99\nItem B  $5.49\nTotal   $8.48",
  "Lines":[
    {"Text":"Walmart","BoundingBox":{"X":10,"Y":15,"Width":200,"Height":30}},
    {"Text":"123 Main St","BoundingBox":{"X":10,"Y":50,"Width":180,"Height":25}},
    {"Text":"Item A  $2.99","BoundingBox":{"X":10,"Y":85,"Width":210,"Height":28}},
    {"Text":"Item B  $5.49","BoundingBox":{"X":10,"Y":120,"Width":210,"Height":28}},
    {"Text":"Total   $8.48","BoundingBox":{"X":10,"Y":155,"Width":210,"Height":30}}
  ],
  "Words":[
    {"Text":"Walmart","Confidence":0.99,"BoundingBox":{...}},
    …
  ]
}
```

**Tiếp theo bạn sẽ làm gì?**  
Phân tích mảng `Lines` để lấy số tiền `Total`, hoặc đưa JSON vào dịch vụ downstream lưu trữ các mục chi. Vì kết quả đã ở dạng JSON, bạn có thể kết nối trực tiếp với bất kỳ cơ sở dữ liệu NoSQL, Azure Function, hay Power Automate flow nào.

---

## Bước 5 – Xử lý các Trường hợp Biên Thường Gặp

Ngay cả những engine OCR tốt nhất cũng gặp khó khăn với một vài vấn đề. Dưới đây là các kịch bản bạn có thể gặp khi học **how to read receipt** ảnh.

| Tình huống | Cách khắc phục / Đề xuất |
|-----------|--------------------------|
| **Hóa đơn độ phân giải thấp (≤ 150 dpi)** | Tăng kích thước ảnh trước bằng `Bitmap` và `Graphics` (`InterpolationMode.HighQualityBicubic`). |
| **Hóa đơn bị xoay hoặc nghiêng** | Giữ `DetectOrientation = true`. Đối với nghiêng nghiêm trọng, tiền xử lý bằng `Image.RotateFlip` hoặc thư viện bên thứ ba như OpenCV. |
| **Nền màu (ví dụ: hóa đơn đặt trên bàn)** | Chuyển sang grayscale và tăng độ tương phản trước OCR (`ImageAttributes`). |
| **Nhiều hóa đơn trong một bức ảnh** | Cắt từng vùng hóa đơn thủ công hoặc dùng `ocrEngine.Config.RecognizeMultipleRegions = true`. |
| **File lớn gây OutOfMemory** | Sử dụng câu lệnh `using` để giải phóng đối tượng `Image` kịp thời, hoặc xử lý theo từng khối. |

```csharp
// Example: simple grayscale conversion
using (Bitmap bmp = new Bitmap(receiptImage))
{
    for (int y = 0; y < bmp.Height; y++)
        for (int x = 0; x < bmp.Width; x++)
        {
            Color c = bmp.GetPixel(x, y);
            int gray = (int)(c.R * 0.3 + c.G * 0.59 + c.B * 0.11);
            bmp.SetPixel(x, y, Color.FromArgb(gray, gray, gray));
        }
    receiptImage = (Image)bmp.Clone();
}
```

---

## Bước 6 – Ví dụ Hoàn Chỉnh (Sẵn Sàng Sao Chép)

Dưới đây là chương trình *đầy đủ* bạn có thể biên dịch ngay. Nó bao gồm tất cả các bước, các `using` directive phù hợp, và xử lý lỗi một cách nhẹ nhàng.

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace ReceiptReaderDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Load the image file C#
            // -------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY\receipt.jpg";

            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"❌ Image not found: {imagePath}");
                return;
            }

            Image receiptImage;
            try
            {
                receiptImage = Image.FromFile(imagePath);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"⚠️ Failed to load image: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 2️⃣ Create and configure OCR engine
            // -------------------------------------------------
            OcrEngine ocrEngine = new OcrEngine
            {
                Config =
                {
                    Language = OcrLanguage.English,
                    DetectOrientation = true
                }
            };

            // -------------------------------------------------
            // 3️⃣ Recognize and convert to JSON
            // -------------------------------------------------
            string jsonResult;
            try
            {
                jsonResult = ocrEngine.RecognizeToJson(receiptImage);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"🛑 OCR failed: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 4️⃣ Output results
            // -------------------------------------------------
            Console.WriteLine("🗂️ OCR JSON Result:");
            Console.WriteLine(jsonResult);

            // Optionally persist the JSON
            string outputPath = Path.Combine(
                Path.GetDirectoryName(imagePath) ?? ".", "receipt_output.json");
            File.WriteAllText(outputPath, jsonResult);
            Console.WriteLine($"✅ JSON saved to {outputPath}");
        }
    }
}
```

**Chạy nó:**  
`dotnet run` từ thư mục dự án. Nếu mọi thứ đã được cấu hình đúng, bạn sẽ thấy JSON được in ra console và lưu bên cạnh ảnh hóa đơn của bạn.

---

## Kết luận

Chúng ta vừa hoàn thành **how to read receipt** ảnh trong C# từ đầu đến cuối. Bằng cách load ảnh, cấu hình Aspose OCR, và gọi `RecognizeToJson`, bạn có thể **extract text from image** và **convert image to JSON** mà hầu như không cần boilerplate. Cách tiếp cận này có thể mở rộng—from một demo đơn lẻ đến một batch processor xử lý hàng trăm hóa đơn mỗi đêm.

Các bước tiếp theo bạn có thể khám phá:

- **Parse the JSON** để lấy ngày, tổng tiền và các mục chi (sử dụng `System.Text.Json` hoặc `Newtonsoft.Json`).  
- **Tích hợp với cơ sở dữ liệu** (SQL, Cosmos DB) để tự động lưu hồ sơ chi phí.  
- **Thêm giao diện UI** (WinForms, WPF, hoặc Blazor) để người dùng kéo‑thả hóa đơn.  
- **Thay Aspose OCR** bằng engine khác (Tesseract, Microsoft Azure OCR) nếu lo ngại về giấy phép—chỉ cần giữ nguyên mẫu “load image file C#”.

Hãy thoải mái thử nghiệm, phá vỡ, và quay lại đây để làm mới kiến thức. Nếu gặp khó khăn, cộng đồng (và các diễn đàn Aspose) là nơi tuyệt vời để đặt câu hỏi. Chúc lập trình vui vẻ, và tận hưởng việc biến những tờ hóa đơn giấy thành dữ liệu sạch, có thể tìm kiếm được!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}