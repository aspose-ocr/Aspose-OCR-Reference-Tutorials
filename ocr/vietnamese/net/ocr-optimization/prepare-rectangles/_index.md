---
date: 2025-12-22
description: Tìm hiểu cách trích xuất văn bản từ hình ảnh bằng Aspose.OCR cho .NET.
  Hướng dẫn này sẽ chỉ cho bạn cách chuẩn bị các hình chữ nhật cho nhận dạng hình
  ảnh OCR và nâng cao độ chính xác.
linktitle: Prepare Rectangles in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: Cách trích xuất văn bản từ hình ảnh bằng cách chuẩn bị các hình chữ nhật trong
  OCR
url: /vi/net/ocr-optimization/prepare-rectangles/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Chuẩn bị các hình chữ nhật trong Nhận dạng ký tự quang học (OCR)

## Giới thiệu

Nhận dạng ký tự quang học (OCR) là công cụ thiết yếu để chuyển nội dung hình ảnh thành văn bản có thể tìm kiếm và chỉnh sửa. Trong hướng dẫn này, bạn sẽ **trích xuất văn bản từ hình ảnh** bằng cách chuẩn bị các hình chữ nhật tùy chỉnh, giúp engine OCR tập trung vào các vùng cụ thể. Sử dụng Aspose.OCR cho .NET, chúng tôi sẽ hướng dẫn từng bước — từ thiết lập dự án đến lấy văn bản đã nhận dạng — để bạn có thể tích hợp chức năng chuyển ảnh‑to‑text mạnh mẽ vào các ứng dụng .NET của mình.

## Câu trả lời nhanh
- **“trích xuất văn bản từ hình ảnh” có nghĩa là gì?** Nó có nghĩa là chuyển các ký tự hiển thị trong ảnh thành chuỗi có thể đọc được bởi máy.  
- **Thư viện nào hỗ trợ việc này trong .NET?** Aspose.OCR cho .NET.  
- **Tôi có cần giấy phép cho việc phát triển không?** Bản dùng thử miễn phí đủ cho việc thử nghiệm; giấy phép cần thiết cho môi trường sản xuất.  
- **Tôi có thể nhắm mục tiêu vào các khu vực cụ thể không?** Có, bằng cách định nghĩa các hình chữ nhật giới hạn phạm vi OCR.  
- **Các phiên bản .NET nào được hỗ trợ?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## “trích xuất văn bản từ hình ảnh” với các hình chữ nhật là gì?
Khi bạn xác định các vùng hình chữ nhật trên một hình ảnh, engine OCR sẽ chỉ xử lý những vùng đó. Điều này cải thiện độ chính xác, giảm thời gian xử lý và cho phép bạn bỏ qua nền nhiễu hoặc các phần không liên quan.

## Tại sao cần chuẩn bị các hình chữ nhật trước khi OCR?
- **Tập trung vào nội dung liên quan:** Bỏ qua tiêu đề, chân trang hoặc các đồ họa trang trí.  
- **Tăng hiệu suất:** Các vùng nhỏ hơn đồng nghĩa với việc nhận dạng nhanh hơn.  
- **Cải thiện độ chính xác:** Ít nhiễu hình ảnh hơn sẽ cho kết quả sạch hơn.

## Yêu cầu trước

- Hiểu biết về C# và phát triển .NET.  
- Thư viện Aspose.OCR cho .NET đã được cài đặt – bạn có thể tải xuống **[tại đây](https://releases.aspose.com/ocr/net/)**.  
- Một hình ảnh mẫu (ví dụ: `sample.png`) chứa văn bản bạn muốn trích xuất.

## Nhập các không gian tên

Đầu tiên, đưa các không gian tên cần thiết vào phạm vi:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Bước 1: Thiết lập thư mục tài liệu của bạn

Xác định vị trí lưu trữ các tệp hình ảnh và tạo một thể hiện của engine OCR.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Cách trích xuất văn bản từ hình ảnh bằng nhiều hình chữ nhật

### Bước 2: Nhận dạng hình ảnh với nhiều hình chữ nhật

#### 2.1 Định nghĩa các hình chữ nhật

Tạo một danh sách các đối tượng `Rectangle` mô tả các khu vực bạn muốn engine OCR quét.

```csharp
List<Rectangle> rects = new List<Rectangle>()
{
    new Rectangle(138, 352, 2033, 537),
    new Rectangle(147, 890, 2033, 1157),
    new Rectangle(923, 2045, 465, 102),
    new Rectangle(104, 2147, 2076, 819)
};
```

#### 2.2 Thực hiện nhận dạng OCR

Truyền đường dẫn hình ảnh và danh sách hình chữ nhật vào `RecognizeImage`. Phương thức sẽ trả về một tập hợp các chuỗi — mỗi mục tương ứng với một hình chữ nhật.

```csharp
// first case
List<string> listResult = api.RecognizeImage(dataDir + "sample.png", rects);

// Display the recognized text
foreach (string s in listResult)
{
    Console.WriteLine(s);
}
```

### Bước 3: Nhận dạng hình ảnh với Cài đặt Nhận dạng (Cách tiếp cận thay thế)

Nếu bạn muốn sử dụng `RecognitionSettings`, bạn có thể đạt được kết quả tương tự với một lời gọi API hơi khác.

#### 3.1 Định nghĩa cài đặt nhận dạng

```csharp
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings
{
    RecognitionAreas = rects
});
```

#### 3.2 Hiển thị văn bản đã nhận dạng

```csharp
// Display the recognized text
foreach (string s in result.RecognitionAreasText)
{
    Console.WriteLine(s);
}
```

## Các vấn đề thường gặp & Mẹo

- **Tọa độ hình chữ nhật không chính xác:** Đảm bảo các giá trị `X`, `Y`, `Width`, và `Height` đúng với vùng bạn muốn.  
- **Chất lượng hình ảnh:** Hình ảnh độ phân giải thấp có thể cho kết quả OCR kém; hãy cân nhắc tiền xử lý (ví dụ: nhị phân hoá).  
- **Kết quả rỗng:** Kiểm tra xem các hình chữ nhật có thực sự chứa văn bản không; nếu không, engine sẽ trả về chuỗi rỗng.

## Kết luận

Bạn đã học cách **trích xuất văn bản từ hình ảnh** bằng cách chuẩn bị các hình chữ nhật tùy chỉnh với Aspose.OCR cho .NET. Kỹ thuật này cho phép bạn kiểm soát chi tiết quá trình OCR, giúp xây dựng các tính năng trích xuất văn bản nhanh hơn và chính xác hơn trong ứng dụng của mình.

## Câu hỏi thường gặp

**Hỏi:** Tôi có thể sử dụng Aspose.OCR cho .NET với các framework .NET khác không?  
**Đáp:** Có, Aspose.OCR cho .NET tương thích với nhiều framework .NET khác nhau.

**Hỏi:** Có bản dùng thử miễn phí cho Aspose.OCR cho .NET không?  
**Đáp:** Chắc chắn! Bạn có thể truy cập bản dùng thử **[tại đây](https://releases.aspose.com/)**.

**Hỏi:** Làm sao tôi có thể nhận hỗ trợ cho Aspose.OCR cho .NET?  
**Đáp:** Truy cập **[diễn đàn Aspose.OCR](https://forum.aspose.com/c/ocr/16)** để được hỗ trợ chuyên biệt.

**Hỏi:** Tôi có thể lấy giấy phép tạm thời để thử nghiệm không?  
**Đáp:** Có, bạn có thể nhận giấy phép tạm thời **[tại đây](https://purchase.aspose.com/temporary-license/)**.

**Hỏi:** Tôi có thể tìm tài liệu cho Aspose.OCR cho .NET ở đâu?  
**Đáp:** Tài liệu có sẵn **[tại đây](https://reference.aspose.com/ocr/net/)**.

---

**Cập nhật lần cuối:** 2025-12-22  
**Kiểm tra với:** Aspose.OCR 24.11 for .NET  
**Tác giả:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}