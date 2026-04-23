---
category: general
date: 2026-03-17
description: Cách thực hiện OCR hàng loạt cho các ảnh PNG trong C# một cách nhanh
  chóng. Học cách trích xuất văn bản từ các tệp PNG, chuyển đổi PNG sang văn bản và
  đọc ảnh từ thư mục bằng một script đơn giản.
draft: false
keywords:
- how to batch OCR
- extract text png
- convert png to text
- read images from directory
language: vi
og_description: Cách thực hiện OCR hàng loạt ảnh PNG trong C# với mã từng bước. Trích
  xuất văn bản từ các tệp PNG, chuyển đổi PNG sang văn bản và đọc ảnh từ thư mục một
  cách dễ dàng.
og_title: Cách thực hiện OCR hàng loạt cho ảnh PNG trong C# – Hướng dẫn đầy đủ
tags:
- OCR
- C#
- Image Processing
title: Cách thực hiện OCR hàng loạt cho ảnh PNG trong C# – Hướng dẫn chi tiết
url: /vi/net/text-recognition/how-to-batch-ocr-png-images-in-c-complete-guide/
---

markdown formatting.

Check for any other markdown links: none.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách thực hiện OCR hàng loạt cho ảnh PNG trong C# – Hướng dẫn đầy đủ

Bạn đã bao giờ tự hỏi **how to batch OCR** cho một thư mục đầy các ảnh chụp màn hình mà không cần mở từng tệp một không? Bạn không phải là người duy nhất—các nhà phát triển luôn hỏi cách thực hiện OCR hàng loạt cho các bộ sưu tập PNG lớn, đặc biệt khi mục tiêu là **extract text PNG** files for downstream analysis.  

Trong hướng dẫn này, chúng tôi sẽ đi qua một ví dụ C# sẵn sàng chạy mà **extracts text PNG** files, **converts PNG to text**, và cho bạn cách tốt nhất để **read images from directory**. Khi kết thúc, bạn sẽ có một script duy nhất tạo ra một tệp `.txt` bên cạnh mỗi ảnh, giúp bạn tiết kiệm hàng giờ sao chép‑dán thủ công.

## Những gì bạn sẽ đạt được

- Khởi tạo một engine OCR một lần và tái sử dụng cho toàn bộ batch.  
- Quét mọi `*.png` trong một thư mục cho trước mà không cần tự viết vòng lặp.  
- Ghi mỗi kết quả OCR vào một tệp văn bản riêng, giữ nguyên tên tệp gốc.  
- Xử lý các trường hợp biên thường gặp như thư mục trống hoặc tệp không phải ảnh một cách nhẹ nhàng.

### Yêu cầu trước

- .NET 6.0 hoặc mới hơn (mã này hoạt động trên .NET Core và .NET Framework cũng được).  
- Một thư viện OCR cung cấp các kiểu `OcrEngine`, `ImageStream`, và `OcrResult` (ví dụ, SDK **FastOCR** giả tưởng được sử dụng trong các đoạn mã).  
- Kiến thức cơ bản về C#—không yêu cầu các mẫu nâng cao.

---

## Cách thực hiện OCR hàng loạt cho ảnh PNG – Tổng quan

Dưới đây là **chương trình đầy đủ, có thể chạy được**. Bạn có thể sao chép‑dán nó vào một dự án console mới, thay thế các đường dẫn placeholder, và nhấn **F5**.

```csharp
using System;
using System.IO;
using System.Linq;
using FastOCR;               // <-- Replace with your actual OCR namespace

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Initialize the OCR engine (language = English)
        // -------------------------------------------------
        var ocrEngine = new OcrEngine();
        ocrEngine.Config.Language = Language.English;

        // -------------------------------------------------
        // Step 2: Locate every PNG file in the input folder
        // -------------------------------------------------
        string inputFolder = @"YOUR_DIRECTORY\images";
        string[] imagePaths = Directory.GetFiles(inputFolder, "*.png");

        if (imagePaths.Length == 0)
        {
            Console.WriteLine("No PNG files found – nothing to process.");
            return;
        }

        // -------------------------------------------------
        // Step 3: Convert file paths to ImageStream objects
        // -------------------------------------------------
        var imageStreams = imagePaths
            .Select(path => ImageStream.FromFile(path))
            .ToList();

        // -------------------------------------------------
        // Step 4: Recognize text in the entire batch
        // -------------------------------------------------
        IReadOnlyList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);

        // -------------------------------------------------
        // Step 5: Write each result to a .txt file next to the image
        // -------------------------------------------------
        string outputFolder = @"YOUR_DIRECTORY\output";
        Directory.CreateDirectory(outputFolder); // ensures the folder exists

        for (int i = 0; i < ocrResults.Count; i++)
        {
            string originalFileName = Path.GetFileNameWithoutExtension(imagePaths[i]);
            string outputPath = Path.Combine(outputFolder, $"{originalFileName}.txt");
            File.WriteAllText(outputPath, ocrResults[i].Text);
            Console.WriteLine($"✅ {originalFileName}.txt created");
        }

        Console.WriteLine("All done! Check the output folder for your text files.");
    }
}
```

> **Kết quả mong đợi:** Đối với mỗi `image01.png` bạn sẽ tìm thấy một `image01.txt` chứa các ký tự đã được nhận dạng. Console sẽ liệt kê mỗi tệp khi nó được ghi.

![How to batch OCR diagram](how-to-batch-ocr-diagram.png "Diagram illustrating how to batch OCR PNG images using C#")

---

## Giải thích từng bước

### 1. Khởi tạo OCR Engine – Trái tim của quy trình  

Dòng `var ocrEngine = new OcrEngine();` tạo một thể hiện engine duy nhất sẽ được tái sử dụng cho toàn bộ batch. Việc tái sử dụng engine là **cực kỳ quan trọng** vì hầu hết các thư viện OCR cấp phát tài nguyên nặng (như mô hình ngôn ngữ) khi khởi tạo. Khởi tạo một lần cải thiện hiệu năng đáng kể—đặc biệt khi bạn có hàng chục hoặc hàng trăm PNG.  

> **Mẹo chuyên nghiệp:** Nếu bạn cần ngôn ngữ khác tiếng Anh, hãy đặt `ocrEngine.Config.Language = Language.Spanish;` (hoặc bất kỳ enum nào được hỗ trợ).  

### 2. Đọc ảnh từ thư mục – tìm mọi PNG  

`Directory.GetFiles(@"YOUR_DIRECTORY\images", "*.png")` làm chính xác những gì từ khóa phụ *read images from directory* hứa hẹn. Nó trả về một mảng các đường dẫn tuyệt đối, mà chúng ta sẽ truyền vào OCR engine sau này.  

> **Tại sao không dùng `SearchOption.AllDirectories`?** Nếu ảnh của bạn nằm trong các thư mục con, bạn có thể chuyển sang `GetFiles(path, "*.png", SearchOption.AllDirectories)`. Chỉ cần nhớ rằng việc quét sâu hơn có thể đưa vào các tệp không mong muốn, vì vậy hãy lọc cho phù hợp.  

### 3. Chuyển đổi đường dẫn tệp thành đối tượng ImageStream  

Hầu hết các SDK OCR yêu cầu một stream thay vì đường dẫn thô. Biểu thức LINQ `Select(path => ImageStream.FromFile(path)).ToList()` tạo ra một **danh sách các stream** mà bộ nhận dạng batch có thể tiêu thụ trong một lần gọi. Bước này cũng đảm bảo các handle tệp chỉ được mở một lần, giảm tải I/O.  

> **Trường hợp biên:** Nếu tệp bị hỏng, `ImageStream.FromFile` có thể ném ngoại lệ. Hãy bọc việc chuyển đổi trong `try/catch` nếu bạn cần độ bền.  

### 4. Nhận dạng văn bản trong toàn bộ batch  

`ocrEngine.RecognizeBatch(imageStreams)` là điểm mạnh cho *how to batch OCR*. Thay vì lặp qua từng ảnh và gọi phương thức một‑ảnh, chúng ta truyền toàn bộ bộ sưu tập cho engine. Nội bộ thư viện có thể thực hiện song song, mang lại tăng tốc trên máy đa nhân.  

> **Mẹo:** Nếu thư viện OCR của bạn không cung cấp phương thức batch, bạn vẫn có thể đạt hiệu năng tương tự bằng cách sử dụng `Parallel.ForEach` quanh lời gọi `Recognize` cho từng ảnh.  

### 5. Ghi mỗi kết quả OCR – chuyển PNG sang văn bản  

Vòng lặp `for` cuối cùng ghi `ocrResults[i].Text` vào một tệp `.txt` có tên phản chiếu PNG gốc. Điều này chính là mô tả của từ khóa phụ *convert PNG to text*. Lệnh `Path.Combine` đảm bảo thư mục đầu ra tồn tại và ngăn ngừa lỗi traversal đường dẫn.  

> **Cạm bẫy phổ biến:** Quên tạo thư mục đầu ra trước sẽ gây ra `DirectoryNotFoundException`. Dòng `Directory.CreateDirectory(outputFolder);` giải quyết vấn đề này trước.  

## Xử lý các biến thể thực tế

| Tình huống | Cần thay đổi gì | Lý do |
|-----------|----------------|-----|
| **Thư mục đầu vào trống** | Giữ guard `if (imagePaths.Length == 0)` ở đầu | Ngăn ngừa cuộc gọi OCR không cần thiết và đưa ra thông báo thân thiện |
| **Các loại tệp hỗn hợp** | Sử dụng `Directory.EnumerateFiles(..., "*.*", SearchOption.TopDirectoryOnly).Where(f => f.EndsWith(".png", StringComparison.OrdinalIgnoreCase))` | Đảm bảo chỉ xử lý PNG, đáp ứng *extract text png* mà không có lỗi |
| **Ảnh lớn ( > 5 MB )** | Thu nhỏ trước khi đưa vào OCR: `ImageStream.FromFile(path).Resize(1920, 1080)` (nếu API hỗ trợ) | Giảm áp lực bộ nhớ và thường cải thiện độ chính xác nhận dạng |
| **Ngôn ngữ OCR khác** | Đặt `ocrEngine.Config.Language = Language.French;` | Điều chỉnh engine phù hợp với ngôn ngữ của ảnh nguồn |

## Câu hỏi thường gặp (FAQ)

**Q: Điều này có hoạt động với tệp JPEG hoặc TIFF không?**  
A: Logic cốt lõi vẫn giống nhau; chỉ cần thay đổi mẫu tìm kiếm thành `"*.jpg"` hoặc `"*.tif"` và đảm bảo thư viện OCR có thể giải mã các định dạng đó.

**Q: Làm sao tôi có thể xử lý hàng ngàn ảnh mà không hết bộ nhớ?**  
A: Thay thế lời gọi batch bằng cách tiếp cận streaming—xử lý một khối, ví dụ 50 ảnh mỗi lần, rồi giải phóng các stream trước khi tải khối tiếp theo.

**Q: Tôi cần điểm tin cậy (confidence) của OCR. Tôi tìm ở đâu?**  
A: Hầu hết các đối tượng `OcrResult` đều cung cấp thuộc tính `Confidence`. Bạn có thể mở rộng bước ghi ra:

```csharp
var result = ocrResults[i];
string content = $"Confidence: {result.Confidence:P2}\n{result.Text}";
File.WriteAllText(outputPath, content);
```

## Tổng kết

Chúng tôi vừa trình bày **cách thực hiện OCR hàng loạt** cho ảnh PNG trong C# từ đầu đến cuối. Bằng cách khởi tạo một engine duy nhất, đọc ảnh từ thư mục, chuyển chúng thành stream, nhận dạng toàn bộ batch, và cuối cùng ghi mỗi kết quả vào tệp văn bản, bạn hiện có một mẫu vững chắc, sẵn sàng cho sản xuất cho các nhiệm vụ **extract text PNG**, **convert PNG to text**, và **read images from directory**.  

Tiếp theo? Hãy thử thay đổi nhà cung cấp OCR, thêm xử lý hậu kỳ đa luồng (ví dụ, kiểm tra chính tả), hoặc đưa các tệp `.txt` vào chỉ mục tìm kiếm. Không gì là không thể khi bạn đã nắm vững quy trình batch.  

Có cách tiếp cận nào bạn muốn chia sẻ? Hãy để lại bình luận, chúc bạn lập trình vui vẻ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}