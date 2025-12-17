---
date: 2025-12-17
description: Tìm hiểu cách trích xuất các hình chữ nhật cho các đoạn văn trong hình
  ảnh OCR bằng Aspose.OCR cho .NET – hướng dẫn chi tiết về cách trích xuất hình chữ
  nhật và tọa độ đoạn văn.
linktitle: Get Rectangles for Paragraphs in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: Cách trích xuất hình chữ nhật cho các đoạn văn trong nhận dạng ảnh OCR
url: /vi/net/image-and-drawing-recognition/get-rectangles-for-paragraphs/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Trích Xuất Hình Chữ Nhật cho Đoạn Văn trong Nhận Diện Ảnh OCR

## Giới thiệu

Chào mừng bạn đến với hướng dẫn toàn diện về **cách trích xuất hình chữ nhật** cho các đoạn văn trong nhận diện ảnh OCR bằng Aspose.OCR cho .NET. Nếu bạn muốn cải thiện quy trình xử lý tài liệu, lấy ra ranh giới đoạn văn và tự động hoá việc trích xuất dữ liệu, bạn đã đến đúng nơi. Chúng tôi sẽ hướng dẫn từng bước—từ việc thiết lập môi trường đến in ra tọa độ hình chữ nhật—để bạn có thể bắt đầu sử dụng kết quả OCR ngay lập tức.

## Câu trả lời nhanh
- **“Trích xuất hình chữ nhật” có nghĩa là gì?** Nó trả về các bounding box (x, y, width, height) của các vùng văn bản được phát hiện.  
- **Phương thức API nào cung cấp các hình chữ nhật?** `AsposeOcr.GetRectangles` với `AreasType.PARAGRAPHS`.  
- **Có cần giấy phép cho việc phát triển không?** Bản dùng thử miễn phí đủ cho việc thử nghiệm; giấy phép thương mại cần thiết cho môi trường sản xuất.  
- **Có thể xử lý nhiều ảnh cùng lúc không?** Có—lặp qua danh sách ảnh của bạn và gọi `GetRectangles` cho mỗi tệp.  
- **Các định dạng nào được hỗ trợ?** PNG, JPEG, TIFF, BMP và nhiều định dạng khác.

## “Cách trích xuất hình chữ nhật” trong OCR là gì?
Trong thuật ngữ OCR, trích xuất hình chữ nhật có nghĩa là xác định các ranh giới hình học bao quanh mỗi đoạn hoặc dòng văn bản trong một ảnh. Những tọa độ này cho phép bạn làm nổi bật, cắt hoặc phân tích sâu hơn các phần cụ thể của tài liệu đã quét.

## Tại sao cần trích xuất tọa độ đoạn văn?
- **Xử lý hậu kỳ chính xác** – bạn có thể đưa mỗi hình chữ nhật vào các quy trình downstream (ví dụ: dịch thuật, che dấu).  
- **Cải thiện UI/UX** – phủ các bounding box lên ảnh gốc để hiển thị cho người dùng vị trí văn bản được tìm thấy.  
- **Tự động hoá hàng loạt** – nhanh chóng định vị và cô lập các đoạn văn trên tập tài liệu lớn.

## Yêu cầu trước

- Kiến thức cơ bản về C# và phát triển .NET.  
- Môi trường phát triển đã cài đặt Aspose.OCR cho .NET – bạn có thể tải xuống [tại đây](https://releases.aspose.com/ocr/net/).  
- Hiểu biết về các khái niệm xử lý ảnh và lý do OCR quan trọng trong việc trích xuất văn bản từ các tệp đã quét.

## Nhập các Namespace

Trong file C# của bạn, nhập các namespace cần thiết để các lớp OCR có sẵn:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Bước 1: Thiết lập Thư mục Tài liệu

Xác định thư mục chứa các ảnh bạn muốn phân tích:

```csharp
string dataDir = "Your Document Directory";
```

## Bước 2: Khởi tạo đối tượng AsposeOcr

Tạo một đối tượng `AsposeOcr` – điều này cho phép bạn truy cập tất cả các chức năng OCR:

```csharp
AsposeOcr api = new AsposeOcr();
```

## Bước 3: Chỉ định Đường dẫn Ảnh

Chỉ tới tệp ảnh cụ thể mà bạn muốn xử lý:

```csharp
string fullPath = dataDir + "sample.png";
```

## Bước 4: Nhận dạng Ảnh và Lấy Hình chữ nhật Đoạn Văn

Gọi phương thức `GetRectangles`. Đặt `detect_areas` thành `true` để engine trả về các hình chữ nhật **đoạn văn**:

```csharp
List<Rectangle> rectangles = api.GetRectangles(fullPath, AreasType.PARAGRAPHS, true);
```

## Bước 5: In Kết quả

Xuất các tọa độ để bạn có thể xem **các tọa độ đoạn văn** đã được phát hiện:

```csharp
Console.WriteLine("Areas coordinates:");
rectangles.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
```

## Các vấn đề thường gặp và Giải pháp

| Vấn đề | Nguyên nhân | Giải pháp |
|-------|------------|----------|
| Không có hình chữ nhật nào được trả về | Chất lượng ảnh quá thấp hoặc `AreasType` sai | Đảm bảo ảnh rõ nét và sử dụng `AreasType.PARAGRAPHS`. |
| Tọa độ lệch một pixel | Không khớp DPI khi tải ảnh | Đặt DPI đúng khi tải ảnh hoặc sử dụng `api.Config.Dpi`. |
| Ngoại lệ giấy phép | Chạy mà không có giấy phép hợp lệ trong môi trường sản xuất | Áp dụng giấy phép tạm thời hoặc vĩnh viễn qua `api.SetLicense`. |

## Câu hỏi thường gặp

**H: Aspose.OCR có tương thích với các định dạng ảnh khác nhau không?**  
Đ: Có, Aspose.OCR hỗ trợ PNG, JPEG, TIFF, BMP và nhiều định dạng phổ biến khác.

**H: Tôi có thể dùng Aspose.OCR để xử lý hàng loạt nhiều ảnh không?**  
Đ: Chắc chắn! Lặp qua một tập hợp các đường dẫn tệp và gọi `GetRectangles` cho mỗi ảnh.

**H: Có bản dùng thử miễn phí cho Aspose.OCR cho .NET không?**  
Đ: Có, bạn có thể khám phá bản dùng thử miễn phí [tại đây](https://releases.aspose.com/).

**H: Làm sao để lấy giấy phép tạm thời cho Aspose.OCR?**  
Đ: Bạn có thể nhận giấy phép tạm thời [tại đây](https://purchase.aspose.com/temporary-license/).

**H: Tôi có thể tìm thêm hỗ trợ và thảo luận về Aspose.OCR ở đâu?**  
Đ: Hãy truy cập [diễn đàn Aspose.OCR](https://forum.aspose.com/c/ocr/16) để nhận hỗ trợ cộng đồng và thảo luận.

## Kết luận

Trong tutorial này, chúng tôi đã trình bày **cách trích xuất hình chữ nhật** cho các đoạn văn bằng Aspose.OCR cho .NET, đi qua từng đoạn mã và giải thích cách diễn giải các tọa độ trả về. Bằng cách tích hợp các bước này vào ứng dụng của bạn, bạn có thể tin cậy lấy ra ranh giới đoạn văn, nâng cao quy trình tài liệu và xây dựng các giải pháp thông minh dựa trên OCR.

---

**Cập nhật lần cuối:** 2025-12-17  
**Kiểm tra với:** Aspose.OCR 24.11 cho .NET  
**Tác giả:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}