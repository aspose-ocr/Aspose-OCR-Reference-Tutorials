---
category: general
date: 2026-03-17
description: Tìm hiểu cách phân tích JSON từ kết quả OCR trong C#. Hướng dẫn này bao
  gồm cách trích xuất văn bản, tải hình ảnh để OCR, thực hiện nhận dạng OCR và sử
  dụng hiệu quả công cụ OCR trong C#.
draft: false
keywords:
- how to parse json
- how to extract text
- load image for OCR
- run OCR recognition
- use OCR engine C#
language: vi
og_description: Cách phân tích JSON từ đầu ra OCR trong C#. Theo dõi hướng dẫn của
  chúng tôi để trích xuất văn bản, tải hình ảnh cho OCR, chạy nhận dạng OCR và sử
  dụng công cụ OCR trong C#.
og_title: Cách phân tích JSON bằng OCR Engine C# – Hướng dẫn đầy đủ
tags:
- C#
- OCR
- JSON
- Image Processing
title: Cách phân tích JSON bằng OCR Engine C# – Hướng dẫn chi tiết từng bước
url: /vi/net/text-recognition/how-to-parse-json-with-ocr-engine-c-complete-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Phân Tích JSON với OCR Engine C# – Hướng Dẫn Toàn Diện Từng Bước

Bạn đã bao giờ tự hỏi **cách phân tích json** mà nhận được trực tiếp từ một OCR engine chưa? Bạn không phải là người duy nhất. Hầu hết các nhà phát triển đều gặp phải vấn đề này—nhận được JSON thô, rồi phải tìm cách trích xuất những phần hữu ích như điểm tin cậy hoặc văn bản thực tế. Trong hướng dẫn này, chúng ta sẽ đi qua việc tải ảnh cho OCR, chạy nhận dạng OCR, và cuối cùng **cách phân tích json** một cách sạch sẽ, dễ bảo trì.

Khi kết thúc tutorial, bạn sẽ có thể:

* Tải một ảnh cho OCR chỉ với vài dòng code.  
* Chạy nhận dạng OCR bằng một OCR engine C#.  
* **Cách trích xuất văn bản** và các siêu dữ liệu khác từ payload JSON.  
* Xử lý các trường hợp biên thường gặp (thiếu trường, định dạng bất ngờ) mà không bị crash.

Không cần tài liệu bên ngoài—mọi thứ bạn cần đều có ở đây.

## Yêu Cầu Trước

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

* .NET 6.0 hoặc mới hơn (code cũng biên dịch được trên .NET Framework 4.7+).  
* Tham chiếu tới thư viện OCR bạn đang dùng (ví dụ sử dụng lớp giả định `OcrEngine`).  
* Gói NuGet `Newtonsoft.Json` để xử lý JSON (`Install-Package Newtonsoft.Json`).  
* Một file ảnh (ví dụ `passport.png`) được đặt ở vị trí ứng dụng có thể đọc được.

> **Mẹo chuyên nghiệp:** Nếu bạn đang dùng một OCR SDK thương mại, hãy kiểm tra xem định dạng đầu ra JSON đã được bật chưa—hầu hết các nhà cung cấp đều cung cấp tính năng này qua một thuộc tính cấu hình như `ocrEngine.Config.OutputFormat`.

## Bước 1 – Tạo và Cấu Hình OCR Engine (Từ Khóa Chính Trong Hành Động)

Điều đầu tiên bạn cần làm là khởi tạo OCR engine và yêu cầu nó trả về JSON. Đây là nơi cụm từ **cách phân tích json** xuất hiện lần đầu trong code, vì engine sẽ cung cấp cho chúng ta một chuỗi JSON mà sau này chúng ta sẽ phân tích.

```csharp
using System;
using Newtonsoft.Json.Linq;   // For JSON parsing
// Assume OcrEngine, OutputFormat, and ImageStream live in the OCR SDK namespace
using OcrSdk;                  // <-- replace with the real namespace

// Step 1: Create an OCR engine instance and set JSON output
var ocrEngine = new OcrEngine();
ocrEngine.Config.OutputFormat = OutputFormat.Json;
```

**Tại sao điều này quan trọng:** Đặt `OutputFormat` thành `Json` đảm bảo phản hồi chứa cả văn bản đã nhận dạng **và** các siêu dữ liệu hữu ích như điểm tin cậy. Nếu bỏ qua bước này, bạn sẽ chỉ nhận được văn bản thuần và **cách phân tích json** sẽ trở nên vô nghĩa.

## Bước 2 – Tải Ảnh cho OCR

Bây giờ chúng ta tải hình ảnh muốn phân tích. Đây là vị trí chính xác mà từ khóa phụ **load image for OCR** tỏa sáng.

```csharp
// Step 2: Load the image you want to recognize
// Make sure the path points to a real file; otherwise an exception is thrown.
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY\passport.png");
```

> **Nếu file không tồn tại thì sao?** Bao quanh lời gọi trong một `try/catch` và hiển thị thông báo thân thiện—ứng dụng của bạn sẽ không bị crash và người dùng sẽ biết nguyên nhân.

## Bước 3 – Chạy Nhận Dạng OCR

Với engine đã sẵn sàng và ảnh đã được tải, bước tiếp theo hợp lý là thực hiện quá trình nhận dạng. Điều này đáp ứng từ khóa phụ **run OCR recognition**.

```csharp
// Step 3: Execute OCR and get the raw result object
var ocrResult = ocrEngine.Recognize();
```

Thuộc tính `ocrResult.Text` bây giờ chứa một chuỗi JSON. Nếu bạn in nó ra console, sẽ thấy dạng như sau:

```json
{
  "OverallConfidence": 0.92,
  "Pages": [
    {
      "Text": "John Doe\nPassport No: 123456789",
      "Confidence": 0.95
    }
  ]
}
```

## Bước 4 – Cách Trích Xuất Văn Bản (và Các Trường Khác) từ JSON

Đây là phần cốt lõi của tutorial: **cách phân tích json** và **cách trích xuất văn bản** từ payload OCR. Chúng ta sẽ dùng `Newtonsoft.Json.Linq.JObject` vì tính linh hoạt của nó.

```csharp
// Step 4: Output the raw JSON (optional, helps debugging)
Console.WriteLine("Raw OCR JSON:");
Console.WriteLine(ocrResult.Text);
Console.WriteLine();

// Step 5: Parse the JSON into a JObject
JObject jsonObject = JObject.Parse(ocrResult.Text);

// Extract the overall confidence score
var overallConfidence = jsonObject["OverallConfidence"]?.Value<double>() ?? 0.0;
Console.WriteLine($"Overall confidence: {overallConfidence:P0}");

// Extract the text from the first page (how to extract text)
string pageText = jsonObject["Pages"]?[0]?["Text"]?.Value<string>() ?? string.Empty;
Console.WriteLine("Extracted text:");
Console.WriteLine(pageText);
```

**Tại sao dùng `JObject`?** Nó cho phép bạn duyệt cây JSON một cách an toàn mà không cần định nghĩa một lớp mô hình C# đầy đủ. Các toán tử điều kiện null (`?.`) bảo vệ bạn khỏi `NullReferenceException` nếu OCR engine bỏ qua một trường nào đó.

### Xử Lý Các Trường Hợp Biên

* **Thiếu trường:** Mẫu `?.Value<T>() ?? default` trả về giá trị dự phòng hợp lý.  
* **Nhiều trang:** Lặp qua `jsonObject["Pages"]` nếu bạn mong đợi hơn một trang.  
* **Điểm tin cậy không phải số:** Dùng `double.TryParse` nếu SDK đôi khi trả về chuỗi.

## Bước 5 – Đóng Gói Tất Cả Vào Một Phương Thức Tái Sử Dụng

Để tránh sao chép‑dán cùng một đoạn boilerplate, hãy đóng gói toàn bộ luồng công việc vào một phương thức trợ giúp. Điều này cũng minh họa **use OCR engine C#** một cách sạch sẽ, có thể tái sử dụng.

```csharp
public static void RunOcrAndParseJson(string imagePath)
{
    // 1️⃣ Create engine & set JSON output
    var engine = new OcrEngine();
    engine.Config.OutputFormat = OutputFormat.Json;

    // 2️⃣ Load image (load image for OCR)
    engine.Image = ImageStream.FromFile(imagePath);

    // 3️⃣ Run OCR (run OCR recognition)
    var result = engine.Recognize();

    // 4️⃣ Show raw JSON (optional)
    Console.WriteLine("=== Raw JSON ===");
    Console.WriteLine(result.Text);
    Console.WriteLine();

    // 5️⃣ Parse JSON (how to parse json)
    JObject obj = JObject.Parse(result.Text);

    // 6️⃣ Extract useful data (how to extract text)
    double confidence = obj["OverallConfidence"]?.Value<double>() ?? 0.0;
    string text = obj["Pages"]?[0]?["Text"]?.Value<string>() ?? string.Empty;

    Console.WriteLine($"Overall confidence: {confidence:P0}");
    Console.WriteLine("Extracted text:");
    Console.WriteLine(text);
}
```

Bây giờ bạn có thể gọi `RunOcrAndParseJson(@"C:\Images\passport.png");` từ `Main` hoặc bất kỳ phần nào khác của ứng dụng.

## Ví Dụ Hoàn Chỉnh Hoạt Động

Dưới đây là một chương trình console tự chứa đầy đủ, bạn có thể sao chép‑dán vào một `.csproj` mới. Nó bao gồm tất cả các phần chúng ta đã thảo luận, cộng thêm một chút xử lý lỗi.

```csharp
// File: Program.cs
using System;
using Newtonsoft.Json.Linq;
using OcrSdk;               // Replace with the actual namespace of your OCR library

class Program
{
    static void Main()
    {
        try
        {
            // Adjust the path to point at a real image on your machine
            string imagePath = @"YOUR_DIRECTORY\passport.png";

            RunOcrAndParseJson(imagePath);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Unexpected error: {ex.Message}");
        }
    }

    /// <summary>
    /// Demonstrates how to parse JSON returned by an OCR engine,
    /// and how to extract text, confidence, and other metadata.
    /// </summary>
    /// <param name="imagePath">Full path to the image file.</param>
    public static void RunOcrAndParseJson(string imagePath)
    {
        // 1️⃣ Initialize OCR engine (use OCR engine C#)
        var engine = new OcrEngine();
        engine.Config.OutputFormat = OutputFormat.Json;

        // 2️⃣ Load image for OCR
        engine.Image = ImageStream.FromFile(imagePath);

        // 3️⃣ Run OCR recognition
        var result = engine.Recognize();

        // 4️⃣ Print raw JSON (helps debugging)
        Console.WriteLine("=== Raw OCR JSON ===");
        Console.WriteLine(result.Text);
        Console.WriteLine();

        // 5️⃣ Parse JSON (how to parse json)
        JObject json = JObject.Parse(result.Text);

        // 6️⃣ Extract overall confidence
        double overallConf = json["OverallConfidence"]?.Value<double>() ?? 0.0;
        Console.WriteLine($"Overall confidence: {overallConf:P0}");

        // 7️⃣ Extract text from first page (how to extract text)
        string firstPageText = json["Pages"]?[0]?["Text"]?.Value<string>() ?? string.Empty;
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(firstPageText);
    }
}
```

**Kết quả mong đợi** (giả sử OCR thành công):

```
=== Raw OCR JSON ===
{
  "OverallConfidence": 0.92,
  "Pages": [
    {
      "Text": "John Doe\nPassport No: 123456789",
      "Confidence": 0.95
    }
  ]
}

Overall confidence: 92%
=== Extracted Text ===
John Doe
Passport No: 123456789
```

Nếu ảnh không đọc được, SDK sẽ ném một ngoại lệ mà chúng ta bắt trong `Main`, in ra thông báo lỗi thân thiện thay vì crash.

## Câu Hỏi Thường Gặp (FAQs)

**H: Nếu OCR engine trả về một mảng các trang thì sao?**  
Đ: Lặp qua `json["Pages"]` và nối từng giá trị `["Text"]`, hoặc xử lý chúng riêng biệt tùy theo nhu cầu.

**H: Tôi có thể deserialize JSON thành một lớp C# có kiểu không?**  
Đ: Chắc chắn. Định nghĩa một cấu trúc lớp phù hợp với schema JSON và dùng `JsonConvert.DeserializeObject<YourRootClass>(result.Text)`. Cách này mang lại an toàn thời gian biên dịch nhưng yêu cầu bạn phải đồng bộ mô hình với đầu ra của SDK.

**H: Điều này có hoạt động với các API OCR bất đồng bộ không?**  
Đ: Có. Thay `engine.Recognize()` bằng `await engine.RecognizeAsync()` và biến `RunOcrAndParseJson` thành `async Task`. Phần phân tích JSON vẫn giữ nguyên.

**H: Làm sao lưu JSON vào file để phân tích sau?**  
Đ: Sau khi lấy `result.Text`, gọi `File.WriteAllText(@"output.json", result.Text);`. Sau đó bạn có thể tải lại bằng `JObject.Parse(File.ReadAllText(...))`.

## Tiếp Theo

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}