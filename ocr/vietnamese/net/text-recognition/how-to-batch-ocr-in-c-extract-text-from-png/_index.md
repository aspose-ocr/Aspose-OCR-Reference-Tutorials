---
category: general
date: 2026-03-26
description: Cách thực hiện OCR hàng loạt trong C# giúp việc trích xuất văn bản từ
  các tệp PNG trở nên dễ dàng. Hãy làm theo hướng dẫn OCR bằng C# từng bước để trích
  xuất văn bản hàng loạt với Aspose OCR.
draft: false
keywords:
- how to batch OCR
- extract text from png
- c# ocr tutorial
- how to create OCR
- batch text extraction
language: vi
og_description: Cách thực hiện OCR hàng loạt trong C# cho phép bạn nhanh chóng trích
  xuất văn bản từ các tệp PNG. Hướng dẫn này sẽ đưa bạn qua một tutorial OCR hoàn
  chỉnh bằng C# với việc trích xuất văn bản hàng loạt.
og_title: Cách thực hiện OCR hàng loạt trong C# – Trích xuất văn bản từ PNG
tags:
- OCR
- C#
- Aspose
title: Cách thực hiện OCR hàng loạt trong C# – Trích xuất văn bản từ PNG
url: /vi/net/text-recognition/how-to-batch-ocr-in-c-extract-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách thực hiện OCR hàng loạt trong C# – Trích xuất văn bản từ PNG

Bạn đã bao giờ tự hỏi **cách thực hiện OCR hàng loạt** một đống ảnh chụp màn hình mà không cần viết một chương trình riêng cho mỗi tệp chưa? Bạn không phải là người duy nhất. Trong nhiều dự án, chúng ta thường có hàng chục tệp PNG cần trích xuất văn bản, và việc làm từng tệp một thật là phiền phức.  

Tin tốt? Với Aspose OCR, bạn có thể tạo một ứng dụng console C# nhỏ gọn xử lý tất cả các hình ảnh này song song, mang lại **trích xuất văn bản hàng loạt** nhanh chóng và một bộ kết quả sạch sẽ. Trong hướng dẫn này, chúng tôi sẽ đi qua một **c# ocr tutorial** đầy đủ, giải thích lý do mỗi phần quan trọng, và cho bạn thấy chính xác kết quả sẽ như thế nào.

Khi đọc xong bài viết này, bạn sẽ có thể:

* Tải danh sách các tệp PNG (hoặc bất kỳ hình ảnh hỗ trợ nào) trong một lần.  
* Cấu hình một `OcrEngine` chung để các thiết lập luôn nhất quán trong toàn bộ lô.  
* Chạy hàng đợi nhận dạng với tối đa bốn worker song song.  
* Lấy văn bản đã nhận dạng cho mỗi trang và in ra console.

Không có phép màu, chỉ có mã nguồn vững chắc mà bạn có thể đưa vào giải pháp của mình ngay hôm nay.

## Những gì bạn cần

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

* .NET 6 SDK (hoặc bất kỳ phiên bản .NET gần đây nào).  
* Giấy phép Aspose OCR hợp lệ hoặc khóa đánh giá tạm thời.  
* Một thư mục chứa các tệp PNG bạn muốn xử lý.  
* Visual Studio 2022 hoặc trình soạn thảo yêu thích của bạn.

Đó là tất cả—không cần thêm gói NuGet nào ngoài `Aspose.OCR` và `System.Collections.Generic` tiêu chuẩn.

## Cách thực hiện OCR hàng loạt – Thiết lập dự án

Điều đầu tiên, tạo một dự án console mới và thêm thư viện Aspose OCR.

```bash
dotnet new console -n BatchOcrDemo
cd BatchOcrDemo
dotnet add package Aspose.OCR
```

Sau khi khôi phục hoàn tất, mở **Program.cs** (hoặc tạo tệp mới) và thêm các chỉ thị `using` thông thường:

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
```

Cấu trúc đơn giản này cho phép chúng ta truy cập vào `OcrEngine`, `RecognitionQueue`, và các lớp trợ giúp mà chúng ta sẽ cần sau này.

## Trích xuất văn bản từ PNG – Chuẩn bị danh sách hình ảnh

Bây giờ chúng ta cần cho chương trình biết **những PNG nào** sẽ được đưa qua OCR. Cách đơn giản nhất là xây dựng một `List<string>` chứa các đường dẫn tuyệt đối hoặc tương đối.

```csharp
// Step 1: Define the image files to be processed
var imagePaths = new List<string>
{
    @"YOUR_DIRECTORY/page1.png",
    @"YOUR_DIRECTORY/page2.png",
    @"YOUR_DIRECTORY/page3.png",
    @"YOUR_DIRECTORY/page4.png"
};
```

Thay `YOUR_DIRECTORY` bằng đường dẫn thư mục thực tế. Nếu bạn có một tập hợp động, bạn cũng có thể dùng `Directory.GetFiles(@"YOUR_DIRECTORY", "*.png")` và đưa kết quả vào danh sách. Điểm quan trọng là **extract text from PNG** chỉ là việc cung cấp đúng tên tệp cho hàng đợi.

![How to batch OCR workflow](https://example.com/placeholder.png "Diagram illustrating how to batch OCR a collection of PNG files")

*Văn bản thay thế hình ảnh: sơ đồ quy trình OCR hàng loạt*

## Hướng dẫn OCR C# – Cấu hình hàng đợi nhận dạng

Trái tim của hoạt động hàng loạt là `RecognitionQueue`. Hãy nghĩ nó như một băng chuyền đưa mỗi hình ảnh tới một `OcrEngine` chung. Bằng cách chia sẻ engine, chúng ta giảm mức sử dụng bộ nhớ và đảm bảo các thiết lập giống hệt cho mọi trang.

```csharp
// Step 2: Create a recognition queue with shared OCR engine and parallelism
var recognitionQueue = new RecognitionQueue
{
    MaxDegreeOfParallelism = 4,          // run up to 4 images at the same time
    Engine = new OcrEngine()            // shared configuration for all images
};
```

Tại sao lại đặt `MaxDegreeOfParallelism` là 4? Trên một laptop quad‑core thông thường, giá trị này cho hiệu suất tốt nhất mà không làm hệ điều hành thiếu tài nguyên. Nếu bạn chạy trên máy chủ có nhiều lõi hơn, hãy tăng số này cho phù hợp.

### Mẹo chuyên nghiệp

Nếu bạn cần các gói ngôn ngữ tùy chỉnh, thiết lập DPI, hoặc cắt vùng quan tâm, hãy thực hiện **một lần** trên `Engine` chung trước khi đưa bất kỳ hình ảnh nào vào hàng đợi. Ví dụ:

```csharp
recognitionQueue.Engine.Language = Language.English;
recognitionQueue.Engine.Dpi = 300;
```

Tất cả các lần nhận dạng sau sẽ tự động kế thừa các tùy chọn này—đây là bản chất của **how to create OCR** pipelines luôn nhất quán.

## Trích xuất văn bản hàng loạt – Đưa hình ảnh vào hàng đợi và chạy hàng đợi

Khi hàng đợi đã sẵn sàng, bước tiếp theo là đưa từng hình ảnh vào. Phương thức `Enqueue` nhận một đối tượng `OcrImage`, mà chúng ta tạo từ đường dẫn tệp.

```csharp
// Step 3: Enqueue each image for OCR processing
foreach (var path in imagePaths)
    recognitionQueue.Enqueue(OcrImage.FromFile(path));
```

Sau khi mọi tệp đã được đưa vào hàng đợi, chúng ta khởi động quá trình:

```csharp
// Step 4: Run the queue and collect OCR results
List<OcrResult> ocrResults = recognitionQueue.ExecuteAll();
```

`ExecuteAll` sẽ chặn cho đến khi mọi hình ảnh hoàn thành, sau đó trả về một danh sách trong đó mỗi phần tử tương ứng với thứ tự đầu vào. Điều này đảm bảo kết quả của trang 1 ở chỉ mục 0, trang 2 ở chỉ mục 1, v.v.—rất tiện khi bạn cần ánh xạ kết quả trở lại các tệp nguồn.

## Cách tạo OCR – Hiển thị kết quả

Cuối cùng, hãy in văn bản đã nhận dạng ra console. Đây là lúc bạn thực sự thấy **batch text extraction** hoạt động.

```csharp
// Step 5: Output the recognized text for each page
for (int i = 0; i < ocrResults.Count; i++)
{
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(ocrResults[i].Text);
}
```

Khi bạn chạy chương trình (`dotnet run`), bạn sẽ thấy một đầu ra giống như:

```
--- Page 1 ---
Welcome to the quarterly report.
--- Page 2 ---
Revenue increased by 12% YoY.
--- Page 3 ---
All figures are provisional.
--- Page 4 ---
Contact finance@example.com for details.
```

Nếu bất kỳ hình ảnh nào thất bại (ví dụ: tệp hỏng), `OcrResult` tương ứng sẽ có thuộc tính `Text` rỗng và bạn có thể kiểm tra `ocrResults[i].Exception` để chẩn đoán.

## Cách tạo OCR – Mẹo, trường hợp đặc biệt và thực tiễn tốt nhất

### Xử lý các lô lớn

Xử lý hàng trăm PNG vẫn có thể tiêu tốn bộ nhớ nếu bạn giữ tất cả các đối tượng `OcrResult` trong bộ nhớ. Trong những trường hợp này, hãy stream kết quả ra file hoặc cơ sở dữ liệu ngay khi mỗi kết quả xuất hiện:

```csharp
recognitionQueue.OnResultReady += (sender, args) =>
{
    File.AppendAllText("OcrOutput.txt",
        $"--- {args.Image.Path} ---{Environment.NewLine}{args.Result.Text}{Environment.NewLine}");
};
```

### Xử lý các định dạng không phải PNG

Aspose OCR cũng hỗ trợ JPEG, BMP và TIFF ngay từ đầu. Chỉ cần thay đổi phần mở rộng tệp trong danh sách hoặc dùng tìm kiếm wildcard. Các bước **c# ocr tutorial** vẫn áp dụng—không cần thay đổi mã.

### Bỏ qua các trang trống

Nếu bạn có các PDF đã quét đôi khi chứa trang trắng, bạn có thể lọc kết quả:

```csharp
if (!string.IsNullOrWhiteSpace(result.Text))
    // process non‑empty text
```

### Lưu ý về giấy phép

Phiên bản đánh giá sẽ dán một watermark lên mỗi trang. Đối với môi trường production, hãy chắc chắn nhúng tệp giấy phép của bạn ở đầu hàm `Main`:

```csharp
License lic = new License();
lic.SetLicense("Aspose.OCR.lic");
```

### Tinh chỉnh song song

`MaxDegreeOfParallelism` mặc định là `Environment.ProcessorCount`. Nếu bạn nhận thấy CPU sử dụng cao hoặc áp lực bộ nhớ, hãy giảm giá trị này. Ngược lại, trên một VM đám mây có nhiều lõi, hãy tăng lên để khai thác tối đa phần cứng.

## Tóm tắt

Bạn giờ đã có một giải pháp **how to batch OCR** hoàn chỉnh trong C# có thể **extract text from PNG** các tệp, chạy chúng song song, và cung cấp kết quả sạch sẽ, có thứ tự. Bằng cách chia sẻ một `OcrEngine` duy nhất, bạn đã học được **how to create OCR** pipelines vừa tiết kiệm bộ nhớ vừa dễ bảo trì. **c# ocr tutorial** này cũng cho bạn thấy cách mở rộng lên **batch text extraction** cho hàng trăm hình ảnh chỉ với vài dòng mã bổ sung.

---

### Tiếp theo là gì?

* Thử thêm phát hiện ngôn ngữ (`Engine.Language = Language.AutoDetect`).  
* Thử nghiệm các định dạng đầu ra—ghi kết quả ra JSON hoặc CSV để phân tích tiếp theo.  
* Kết hợp OCR hàng loạt này với bước chuyển PDF sang hình ảnh để xử lý toàn bộ tài liệu đã quét.

Bạn có thể tự do điều chỉnh mức song song, thay đổi nguồn ảnh của mình, hoặc đưa kết quả vào chỉ mục tìm kiếm. Khi bạn thành thạo **how to batch OCR** trong C#, không gì là không thể.

Chúc lập trình vui vẻ, và chúc các lần chạy OCR của bạn nhanh chóng và không lỗi!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}