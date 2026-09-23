---
date: 2026-02-22
description: Tìm hiểu cách thực hiện phân tích bố cục OCR bằng cách nhận dạng các
  dòng văn bản trong hình ảnh và trích xuất các hình chữ nhật của dòng bằng Aspose.OCR
  cho .NET.
linktitle: Layout Analysis OCR – Get Line Rectangles from Images
second_title: Aspose.OCR .NET API
title: Phân tích bố cục OCR – Lấy hình chữ nhật các dòng từ ảnh
url: /vi/net/image-and-drawing-recognition/get-rectangles-for-lines/
weight: 10
---

.

Let's write.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Phân tích bố cục OCR – Lấy các hình chữ nhật dòng từ hình ảnh

## Giới thiệu

Trong hướng dẫn này, bạn sẽ khám phá **cách lấy các hình chữ nhật dòng OCR** với Aspose.OCR cho .NET. Khi kết thúc hướng dẫn, bạn sẽ có thể **nhận dạng các dòng văn bản trong một hình ảnh** và **trích xuất tọa độ dòng** cho mỗi dòng được phát hiện — hoàn hảo cho xử lý tiếp theo như **phân tích bố cục OCR**, trích xuất dữ liệu, hoặc render tùy chỉnh.

## Câu trả lời nhanh
- **“get OCR line rectangles” có nghĩa là gì?** Nó trả về các hộp bao (bounding boxes) của mỗi dòng văn bản được phát hiện trong một hình ảnh.  
- **Phương thức API nào được sử dụng?** `AsposeOcr.GetRectangles(..., AreasType.LINES, ...)`.  
- **Tôi có cần giấy phép không?** Bản dùng thử miễn phí hoạt động cho việc phát triển; giấy phép thương mại cần thiết cho môi trường sản xuất.  
- **Các định dạng hình ảnh được hỗ trợ?** PNG, JPEG, BMP, TIFF và nhiều định dạng khác.  
- **Có thể chạy trên .NET Core không?** Có, Aspose.OCR hoàn toàn hỗ trợ .NET Core và .NET 5/6.

## Yêu cầu trước

Trước khi bắt đầu, hãy đảm bảo bạn đã chuẩn bị các yêu cầu sau:

- Kiến thức cơ bản về C# và phát triển .NET.  
- Môi trường phát triển tích hợp (IDE) như Visual Studio.  
- Thư viện Aspose.OCR cho .NET đã được cài đặt. Bạn có thể tải xuống [tại đây](https://releases.aspose.com/ocr/net/).  
- Một hình ảnh mẫu chứa văn bản để nhận dạng OCR.

## Nhập các namespace

Đảm bảo bạn đã nhập các namespace cần thiết vào dự án. Thêm các dòng sau vào đầu tệp C# của bạn:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

Bây giờ, chúng ta sẽ phân tích quy trình lấy các hình chữ nhật cho các dòng trong nhận dạng OCR hình ảnh thành các bước dễ‑hiểu.

## layout analysis ocr – Hướng dẫn từng bước

### Bước 1: Thiết lập Thư mục Tài liệu của Bạn

```csharp
// ExStart:3
string dataDir = "Your Document Directory";
// ExEnd:3
```

Thay thế `"Your Document Directory"` bằng đường dẫn thực tế tới thư mục chứa hình ảnh mẫu của bạn.

### Bước 2: Khởi tạo Aspose.OCR

```csharp
// ExStart:4
AsposeOcr api = new AsposeOcr();
// ExEnd:4
```

Tạo một thể hiện của lớp `AsposeOcr` để truy cập chức năng OCR.

### Bước 3: Xác định Đường dẫn Hình ảnh

```csharp
// ExStart:5
string fullPath = dataDir + "sample.png";
// ExEnd:5
```

Xác định đường dẫn đầy đủ tới hình ảnh bạn muốn thực hiện OCR.

### Bước 4: Nhận dạng Hình ảnh và Lấy Các Hình chữ nhật

```csharp
// ExStart:6
List<Rectangle> lines = api.GetRectangles(fullPath, AreasType.LINES, false);
// ExEnd:6
```

Phương thức `GetRectangles` trả về một danh sách các đối tượng `Rectangle`, mỗi đối tượng đại diện cho tọa độ của một dòng văn bản được phát hiện. Đây là phần cốt lõi của **lấy các hình chữ nhật dòng OCR** và cho phép **phân tích bố cục OCR**.

### Bước 5: In Kết quả

```csharp
// ExStart:7
Console.WriteLine("Areas coordinates:");
lines.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
// ExEnd:7
```

In tọa độ của các vùng được phát hiện ra console. Bạn sẽ thấy các giá trị mà sau này có thể dùng để **trích xuất tọa độ dòng** cho các quy trình tùy chỉnh.

## Tại sao nên dùng Aspose.OCR để lấy Hình chữ nhật Dòng?

- **Độ chính xác cao** – Các thuật toán tiên tiến phát hiện dòng ngay cả trong ảnh nhiễu hoặc nghiêng.  
- **Đa nền tảng** – Hoạt động trên .NET Framework, .NET Core và .NET 5/6.  
- **Không phụ thuộc bên ngoài** – Thư viện .NET thuần, không cần DLL gốc để phân phối.  
- **Đầu ra phong phú** – Ngoài các hình chữ nhật dòng, bạn còn có thể lấy các từ, ký tự và điểm tin cậy.

## Các vấn đề thường gặp và Giải pháp

| Vấn đề | Giải pháp |
|-------|----------|
| **Không trả về hình chữ nhật** | Đảm bảo hình ảnh chứa văn bản rõ ràng, ngang và đã chỉ định `AreasType.LINES`. |
| **Tọa độ không chính xác** | Kiểm tra DPI của hình ảnh; hình ảnh độ phân giải thấp có thể gây ra giới hạn không chính xác. |
| **Tắc nghẽn hiệu năng với ảnh lớn** | Thu nhỏ ảnh về độ phân giải hợp lý trước khi gọi `GetRectangles`. |
| **Lỗi giấy phép** | Sử dụng giấy phép dùng thử để kiểm tra; áp dụng giấy phép đầy đủ cho môi trường sản xuất để tránh giới hạn đánh giá. |

## Câu hỏi thường gặp

**H: Tôi có thể trích xuất các từ riêng lẻ thay vì toàn bộ dòng không?**  
Đ: Có, sử dụng `AreasType.WORDS` cùng phương thức `GetRectangles` để lấy các hộp bao cấp độ từ.

**H: API có hỗ trợ PDF đa trang không?**  
Đ: Chuyển mỗi trang PDF thành hình ảnh trước, sau đó gọi `GetRectangles` trên từng hình ảnh.

**H: Làm thế nào xử lý văn bản bị quay?**  
Đ: Bật tùy chọn tự động quay trong cài đặt OCR hoặc quay trước hình ảnh trước khi xử lý.

**H: Có cách nào lấy điểm tin cậy cho mỗi dòng không?**  
Đ: Sau khi có các hình chữ nhật, gọi `api.RecognizeImage(...).Lines` để truy cập các đối tượng dòng bao gồm giá trị tin cậy.

**H: Các phiên bản .NET nào tương thích?**  
Đ: Thư viện hoạt động với .NET Framework 4.5+, .NET Core 3.1+, và .NET 5/6.

## Các trường hợp sử dụng thực tế

- **Phân tích bố cục tài liệu OCR** – Cung cấp các hình chữ nhật dòng cho engine bố cục để tái tạo cấu trúc cột.  
- **Trích xuất dữ liệu tự động** – Sử dụng tọa độ để cắt các dòng riêng lẻ cho các pipeline NLP tiếp theo.  
- **Render tùy chỉnh** – Đặt lớp phủ các hộp bao lên hình ảnh gốc để kiểm tra trực quan hoặc hiển thị trên giao diện người dùng.  

## Kết luận

Chúc mừng! Bạn đã thành công **lấy các hình chữ nhật dòng OCR** cho một hình ảnh bằng Aspose.OCR cho .NET. Với các hộp bao trong tay, bạn có thể đưa tọa độ dòng vào các quy trình downstream như render tùy chỉnh, trích xuất dữ liệu, hoặc **phân tích bố cục OCR**.

---

**Cập nhật lần cuối:** 2026-02-22  
**Kiểm tra với:** Aspose.OCR 24.11 cho .NET  
**Tác giả:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}