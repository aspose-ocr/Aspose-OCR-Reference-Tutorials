---
date: 2025-12-17
description: Học cách lấy các hình chữ nhật dòng OCR bằng Aspose.OCR cho .NET để nhận
  dạng các dòng văn bản trong hình ảnh và dễ dàng trích xuất tọa độ của chúng.
linktitle: Get OCR Line Rectangles for Image Text Lines
second_title: Aspose.OCR .NET API
title: Lấy các hình chữ nhật dòng OCR cho các dòng văn bản trong ảnh
url: /vi/net/image-and-drawing-recognition/get-rectangles-for-lines/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lấy Các Hình Chữ Nhật Dòng OCR cho Các Dòng Văn Bản Trong Hình Ảnh

## Introduction

Trong hướng dẫn này, bạn sẽ khám phá **cách lấy các hình chữ nhật dòng OCR** với Aspose.OCR cho .NET. Khi kết thúc hướng dẫn, bạn sẽ có thể **nhận dạng các dòng văn bản trong một hình ảnh** và **trích xuất tọa độ dòng** cho mỗi dòng được phát hiện — hoàn hảo cho việc xử lý tiếp theo như phân tích bố cục, trích xuất dữ liệu, hoặc render tùy chỉnh.

## Quick Answers
- **“Lấy các hình chữ nhật dòng OCR” có nghĩa là gì?** Nó trả về các hộp bao quanh (bounding boxes) của mỗi dòng văn bản được phát hiện trong một hình ảnh.  
- **Phương thức API nào được sử dụng?** `AsposeOcr.GetRectangles(..., AreasType.LINES, ...)`.  
- **Tôi có cần giấy phép không?** Bản dùng thử miễn phí hoạt động cho phát triển; giấy phép thương mại cần thiết cho môi trường sản xuất.  
- **Các định dạng hình ảnh được hỗ trợ?** PNG, JPEG, BMP, TIFF và nhiều hơn nữa.  
- **Tôi có thể chạy trên .NET Core không?** Có, Aspose.OCR hoàn toàn hỗ trợ .NET Core và .NET 5/6.

## Prerequisites

Trước khi bắt đầu hướng dẫn, hãy chắc chắn rằng bạn đã chuẩn bị các yêu cầu sau:

- Kiến thức cơ bản về C# và phát triển .NET.  
- Một môi trường phát triển tích hợp (IDE) như Visual Studio.  
- Thư viện Aspose.OCR cho .NET đã được cài đặt. Bạn có thể tải xuống [tại đây](https://releases.aspose.com/ocr/net/).  
- Một hình ảnh mẫu chứa văn bản để nhận dạng OCR.

## Import Namespaces

Đảm bảo bạn đã nhập các namespace cần thiết vào dự án của mình. Thêm các dòng sau vào đầu file C# của bạn:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

Bây giờ, chúng ta sẽ phân tích quy trình lấy các hình chữ nhật cho các dòng trong nhận dạng OCR hình ảnh thành các bước dễ‑theo.

## Step 1: Set Up Your Document Directory

```csharp
// ExStart:3
string dataDir = "Your Document Directory";
// ExEnd:3
```

Thay thế `"Your Document Directory"` bằng đường dẫn thực tế tới thư mục chứa hình ảnh mẫu của bạn.

## Step 2: Initialize Aspose.OCR

```csharp
// ExStart:4
AsposeOcr api = new AsposeOcr();
// ExEnd:4
```

Tạo một thể hiện của lớp `AsposeOcr` để truy cập chức năng OCR.

## Step 3: Specify Image Path

```csharp
// ExStart:5
string fullPath = dataDir + "sample.png";
// ExEnd:5
```

Xác định đường dẫn đầy đủ tới hình ảnh bạn muốn thực hiện OCR.

## Step 4: Recognize Image and Get Rectangles

```csharp
// ExStart:6
List<Rectangle> lines = api.GetRectangles(fullPath, AreasType.LINES, false);
// ExEnd:6
```

Phương thức `GetRectangles` trả về một danh sách các đối tượng `Rectangle`, mỗi đối tượng đại diện cho tọa độ của một dòng văn bản được phát hiện. Đây là phần cốt lõi của **việc lấy các hình chữ nhật dòng OCR**.

## Step 5: Print Result

```csharp
// ExStart:7
Console.WriteLine("Areas coordinates:");
lines.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
// ExEnd:7
```

In ra tọa độ của các vùng được phát hiện lên console. Bạn sẽ thấy các giá trị mà sau này có thể dùng để **trích xuất tọa độ dòng** cho quá trình xử lý tùy chỉnh.

## Why Use Aspose.OCR for Line Rectangles?

- **Độ chính xác cao** – Thuật toán tiên tiến phát hiện các dòng ngay cả trong hình ảnh nhiễu hoặc lệch.  
- **Đa nền tảng** – Hoạt động trên .NET Framework, .NET Core và .NET 5/6.  
- **Không phụ thuộc bên ngoài** – Thư viện .NET thuần, không có DLL gốc cần triển khai.  
- **Đầu ra phong phú** – Ngoài các hình chữ nhật dòng, bạn còn có thể lấy các từ, ký tự và điểm tin cậy.

## Common Issues and Solutions

| Issue | Solution |
|-------|----------|
| **Không có hình chữ nhật nào được trả về** | Đảm bảo hình ảnh chứa văn bản rõ ràng, ngang và đã chỉ định `AreasType.LINES`. |
| **Tọa độ không chính xác** | Kiểm tra DPI của hình ảnh; hình ảnh độ phân giải thấp có thể gây ra giới hạn không chính xác. |
| **Nút thắt hiệu năng trên hình ảnh lớn** | Thay đổi kích thước hình ảnh tới độ phân giải hợp lý trước khi gọi `GetRectangles`. |
| **Ngoại lệ giấy phép** | Sử dụng giấy phép dùng thử để thử nghiệm; áp dụng giấy phép đầy đủ cho môi trường sản xuất để tránh giới hạn đánh giá. |

## Câu Hỏi Thường Gặp

### Câu hỏi 1: Tôi có thể sử dụng Aspose.OCR cho .NET với bất kỳ loại hình ảnh nào không?

A1: Aspose.OCR hỗ trợ nhiều định dạng hình ảnh, đảm bảo tính linh hoạt trong các ứng dụng OCR của bạn.

### Câu hỏi 2: Độ chính xác của nhận dạng OCR như thế nào?

A2: Aspose.OCR sử dụng các thuật toán tiên tiến để đạt độ chính xác cao, phù hợp với nhiều kịch bản nhận dạng văn bản.

### Câu hỏi 3: Có phiên bản dùng thử không?

A3: Có, bạn có thể khám phá khả năng của Aspose.OCR cho .NET với [bản dùng thử miễn phí](https://releases.aspose.com/).

### Câu hỏi 4: Tôi có thể tìm tài liệu chi tiết ở đâu?

A4: Tham khảo [tài liệu](https://reference.aspose.com/ocr/net/) để biết thông tin chi tiết và hướng dẫn sử dụng.

### Câu hỏi 5: Cần hỗ trợ hoặc có câu hỏi cụ thể?

A5: Truy cập [diễn đàn Aspose.OCR](https://forum.aspose.com/c/ocr/16) để được cộng đồng hỗ trợ và thảo luận.

## Các Câu Hỏi Thường Gặp

**Q: Tôi có thể trích xuất các từ riêng lẻ thay vì toàn bộ dòng không?**  
A: Có, sử dụng `AreasType.WORDS` với cùng phương thức `GetRectangles` để lấy các hộp bao quanh ở mức từ.

**Q: API có hỗ trợ PDF đa trang không?**  
A: Đầu tiên chuyển mỗi trang PDF thành hình ảnh, sau đó gọi `GetRectangles` trên mỗi hình ảnh.

**Q: Làm thế nào để xử lý văn bản bị xoay?**  
A: Bật tùy chọn tự động xoay trong cài đặt OCR hoặc xoay trước hình ảnh trước khi xử lý.

**Q: Có cách nào để lấy điểm tin cậy cho mỗi dòng không?**  
A: Sau khi lấy các hình chữ nhật, gọi `api.RecognizeImage(...).Lines` để truy cập các đối tượng dòng có chứa giá trị tin cậy.

**Q: Các phiên bản .NET nào tương thích?**  
A: Thư viện hoạt động với .NET Framework 4.5+, .NET Core 3.1+, và .NET 5/6.

## Kết Luận

Chúc mừng! Bạn đã thành công **lấy các hình chữ nhật dòng OCR** cho một hình ảnh bằng Aspose.OCR cho .NET. Với các hộp bao quanh trong tay, bạn có thể đưa tọa độ dòng vào các quy trình downstream như render tùy chỉnh, trích xuất dữ liệu, hoặc phân tích bố cục.

---

**Cập nhật lần cuối:** 2025-12-17  
**Kiểm tra với:** Aspose.OCR 24.11 for .NET  
**Tác giả:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}