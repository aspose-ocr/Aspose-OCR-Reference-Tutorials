---
category: general
date: 2026-03-29
description: Trích xuất văn bản từ hình ảnh bằng Aspose OCR trong C#. Tìm hiểu OCR
  tự động xoay và cách chỉnh nghiêng ảnh quét để đạt kết quả hoàn hảo.
draft: false
keywords:
- extract text from image
- auto rotate ocr
- how to deskew scanned image
- Aspose OCR C#
- image preprocessing OCR
language: vi
og_description: Trích xuất văn bản từ hình ảnh bằng Aspose OCR. Hướng dẫn này trình
  bày OCR tự động xoay và cách chỉnh nghiêng ảnh quét trong C#.
og_title: Trích xuất văn bản từ hình ảnh trong C# – OCR tự động xoay và chỉnh nghiêng
tags:
- C#
- OCR
- Aspose
- Image Processing
title: Trích xuất văn bản từ hình ảnh trong C# – Hướng dẫn OCR tự xoay và cân chỉnh
  nghiêng
url: /vi/net/ocr-optimization/extract-text-from-image-in-c-auto-rotate-ocr-deskew-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Trích xuất văn bản từ hình ảnh trong C# – Hướng dẫn Auto‑Rotate OCR & Deskew

Bạn đã bao giờ cần **trích xuất văn bản từ hình ảnh** nhưng tệp lại được chụp ở góc kỳ lạ? Đó là một vấn đề phổ biến—đặc biệt khi bạn làm việc với hoá đơn đã quét, biên lai chụp ảnh, hoặc các PDF lệch. Tin tốt là bạn không cần tự viết thuật toán xoay. Bằng cách sử dụng tính năng *auto rotate OCR* tích hợp sẵn của Aspose OCR, bạn có thể để engine tự chỉnh thẳng ảnh và sau đó **trích xuất văn bản từ hình ảnh** trong một bước liền mạch.

Trong hướng dẫn này, chúng ta sẽ đi qua một chương trình C# hoàn chỉnh, sẵn sàng chạy, thực hiện:

* Khởi tạo engine OCR với chế độ tự động xác định hướng và cân chỉnh (deskew),
* Nhận dạng một ảnh đã quay hoặc lệch,
* Trả về cả góc quay được phát hiện và văn bản đã trích xuất.

Không cần dịch vụ bên ngoài, không cần tính toán phức tạp—chỉ vài dòng code và giải thích rõ ràng về *cách cân chỉnh (deskew) ảnh đã quét* khi cần.

## Những gì bạn cần

| Yêu cầu | Lý do |
|--------------|----------------|
| .NET 6.0 hoặc mới hơn (hoặc .NET Framework 4.6+) | Aspose OCR được cung cấp dưới dạng gói NuGet hỗ trợ các runtime này. |
| Visual Studio 2022 (hoặc bất kỳ trình soạn thảo C# nào) | Giúp dễ dàng thêm gói NuGet và chạy ứng dụng console. |
| Một ảnh mẫu (`rotated_document.jpg`) | Tệp phải là JPEG, PNG, BMP hoặc TIFF và không phải đứng thẳng hoàn hảo. |
| Gói NuGet Aspose.OCR (`Install-Package Aspose.OCR`) | Cung cấp `OcrEngine`, `PreprocessingFilters` và các kiểu liên quan. |

Nếu bạn đã có đầy đủ các mục trên, bạn đã sẵn sàng. Nếu chưa, hãy tải Aspose OCR mới nhất từ NuGet—cài đặt chỉ một cú nhấp chuột.

---

## Bước 1 – Khởi tạo Engine OCR (Từ khóa chính trong hành động)

Điều đầu tiên chúng ta làm là tạo một thể hiện `OcrEngine` và chỉ định cho nó **auto rotate OCR** và **deskew** mọi ảnh đầu vào. Hai cờ này được kết hợp bằng phép OR bitwise (`|`) vì `PreprocessingFilters` là một enum có thuộc tính `[Flags]`.

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Initialise the OCR engine with English language and preprocessing options
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.English,
            // Enable both auto‑rotate and auto‑deskew
            Preprocessing = PreprocessingFilters.AutoRotate | PreprocessingFilters.AutoDeskew
        };
```

> **Tại sao lại quan trọng:**  
> *Auto‑rotate OCR* kiểm tra đường cơ sở văn bản của ảnh, đoán hướng đúng và xoay ảnh nội bộ trước khi nhận dạng. *Auto‑deskew* làm tương tự cho những góc nghiêng nhẹ thường xuất hiện trong tài liệu đã quét. Bằng cách bật cả hai, bạn đảm bảo kết quả **trích xuất văn bản từ hình ảnh** tốt nhất mà không cần chỉnh sửa ảnh thủ công.

---

## Bước 2 – Nhận dạng ảnh và lấy kết quả

Bây giờ chúng ta truyền đường dẫn tệp cho engine. Phương thức `RecognizeImage` trả về một đối tượng `OcrResult` chứa góc quay được phát hiện, điểm tin cậy và văn bản thu được.

```csharp
        // Recognise the image file and obtain the OCR result
        OcrResult ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/rotated_document.jpg");
```

> **Mẹo:** Nếu bạn làm việc với một stream (ví dụ, tệp tải lên), hãy dùng `ocrEngine.RecognizeImage(Stream)` thay thế. Các cờ tiền xử lý vẫn áp dụng, vì vậy bạn vẫn nhận được lợi ích của **auto rotate OCR**.

---

## Bước 3 – Hiển thị góc quay và văn bản đã trích xuất

Cuối cùng, chúng ta in ra hai thông tin trên console: góc mà engine cho rằng ảnh cần quay, và văn bản thực tế đã được lấy ra.

```csharp
        // Show the detected rotation and the recognised text
        Console.WriteLine($"Detected rotation: {ocrResult.RotationAngle}°");
        Console.WriteLine("----- Extracted Text -----");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Kết quả mong đợi** (các số của bạn sẽ khác tùy vào ảnh đầu vào):

```
Detected rotation: 12.3°
----- Extracted Text -----
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
Thank you for your business!
```

Nếu ảnh đã đứng thẳng, góc quay sẽ là `0°`, và bạn vẫn sẽ nhận được văn bản sạch nhờ thuật toán *auto‑deskew*.

---

## Bước 4 – Hiểu cách cân chỉnh (deskew) ảnh đã quét (Từ khóa phụ, khám phá sâu)

Bạn có thể thắc mắc *cách cân chỉnh (deskew) ảnh đã quét* khi engine OCR báo cáo góc quay khác 0. Ở mức độ bên trong, Aspose OCR áp dụng **biến đổi Hough** để phát hiện hướng của dòng văn bản chiếm ưu thế. Sau đó nó xoay bitmap ngược lại góc đã phát hiện, thực sự làm thẳng văn bản.

**Khi nào điều này quan trọng?**  
* Máy quét đưa giấy vào với một góc nhẹ (phổ biến trong môi trường văn phòng).  
* Ảnh chụp bằng điện thoại di động—đường chân trời hiếm khi hoàn hảo.  

**Xử lý các trường hợp biên:**  
Nếu `RotationAngle` trong kết quả bất thường lớn (ví dụ, > 45°), engine có thể đã hiểu sai ảnh (có thể là logo hoặc đồ họa không phải văn bản). Trong trường hợp đó bạn có thể:

1. Tự xoay ảnh bằng `System.Drawing` trước khi đưa vào engine, hoặc  
2. Tắt `AutoRotate` và chỉ giữ `AutoDeskew` nếu bạn biết tài liệu đã đứng thẳng.

```csharp
// Example: manually rotate 90° clockwise before OCR
using (var img = Aspose.OCR.Image.Load("rotated_document.jpg"))
{
    img.Rotate(90);
    OcrResult result = ocrEngine.RecognizeImage(img);
    Console.WriteLine(result.Text);
}
```

---

## Bước 5 – Những lỗi thường gặp & Mẹo chuyên nghiệp (E‑E‑A‑T trong hành động)

| Lỗi thường gặp | Nguyên nhân | Cách khắc phục |
|---------|----------------|-----|
| **Ảnh mờ hoặc độ phân giải thấp** | Độ chính xác OCR giảm mạnh; phát hiện góc quay có thể thất bại. | Sử dụng ảnh quét ít nhất 300 dpi; áp dụng bộ lọc làm nét trước khi OCR. |
| **Nhiều ngôn ngữ** | Engine mặc định tiếng Anh; ký tự ngoại ngữ sẽ bị lỗi. | Đặt `Language = Language.English | Language.Spanish` (hoặc kết hợp phù hợp). |
| **Tệp lớn (> 10 MB)** | Áp lực bộ nhớ có thể gây `OutOfMemoryException`. | Thu nhỏ ảnh trước, hoặc xử lý theo khối bằng `OcrEngine.RecognizeRegion`. |
| **Đường dẫn tệp không đúng** | `FileNotFoundException` dừng chương trình. | Dùng `Path.Combine(Environment.CurrentDirectory, "rotated_document.jpg")` để tăng độ bền. |

> **Mẹo chuyên nghiệp:** Luôn ghi lại `ocrResult.RotationAngle` và `ocrResult.Confidence` (nếu có). Những chỉ số này giúp bạn quyết định có nên thử lại với cài đặt tiền xử lý khác hay không.

---

## Bước 6 – Mở rộng ví dụ (Tiếp theo là gì?)

Khi bạn đã có thể **trích xuất văn bản từ hình ảnh** với tự động xoay và cân chỉnh, hãy cân nhắc các bước tiếp theo:

* **Xử lý hàng loạt** – Duyệt qua một thư mục ảnh, lưu mỗi kết quả vào cơ sở dữ liệu, và đánh dấu những ảnh có `RotationAngle > 5°` để kiểm tra thủ công.  
* **Chuyển đổi PDF** – Kết hợp văn bản đã trích xuất với ảnh gốc để tạo PDF có thể tìm kiếm bằng Aspose.PDF.  
* **Phát hiện ngôn ngữ** – Sử dụng cờ `AutoDetectLanguage` của Aspose.OCR để để engine tự chọn ngôn ngữ phù hợp.  

Mỗi mục trên dựa trên nguyên tắc cốt lõi: để thư viện xử lý hướng, còn bạn tập trung vào logic nghiệp vụ.

---

## Ví dụ hoàn chỉnh (Sẵn sàng sao chép)

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialise the OCR engine with auto‑rotate and auto‑deskew
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.English,
            Preprocessing = PreprocessingFilters.AutoRotate | PreprocessingFilters.AutoDeskew
        };

        // 2️⃣ Recognise the image – replace the path with your own file
        string imagePath = "YOUR_DIRECTORY/rotated_document.jpg";
        OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

        // 3️⃣ Output the rotation angle and the recognised text
        Console.WriteLine($"Detected rotation: {ocrResult.RotationAngle}°");
        Console.WriteLine("----- Extracted Text -----");
        Console.WriteLine(ocrResult.Text);
    }
}
```

Lưu file dưới tên `Program.cs`, chạy `dotnet add package Aspose.OCR`, sau đó `dotnet run`. Bạn sẽ thấy góc quay và văn bản sạch được in ra console.

---

## Kết luận

Chúng ta vừa minh họa cách **trích xuất văn bản từ hình ảnh** trong C# đồng thời để Aspose OCR tự động thực hiện *auto rotate OCR* và giải quyết vấn đề khó khăn *cách cân chỉnh (deskew) ảnh đã quét*. Bằng cách bật hai cờ tiền xử lý, engine tự động làm thẳng ảnh lệch, xác định đúng hướng và cung cấp văn bản chính xác—không cần chỉnh sửa ảnh thủ công.

Hãy thử nghiệm với các batch lớn hơn, ngôn ngữ khác nhau, hoặc thậm chí tích hợp kết quả vào PDF có thể tìm kiếm. Khi engine OCR chịu trách nhiệm phần nặng, bạn có thể tập trung vào những gì thực sự quan trọng.

**Sẵn sàng nâng cấp quy trình tài liệu của mình?** Lấy mã nguồn, chỉ định tới các ảnh của bạn, và xem các góc quay biến mất. Nếu gặp khó khăn, hãy để lại bình luận bên dưới—chúc lập trình vui!  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}