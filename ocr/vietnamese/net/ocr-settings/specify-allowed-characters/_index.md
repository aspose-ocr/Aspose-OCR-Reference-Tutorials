---
description: Tìm hiểu cách chỉ định các ký tự cho phép trong OCR với Aspose.OCR cho
  .NET và nhận dạng hình ảnh chữ số một cách hiệu quả. Thực hiện theo hướng dẫn từng
  bước để giới hạn OCR chỉ nhận dạng chữ số.
linktitle: Specify Allowed Characters OCR – Using Aspose.OCR for .NET
second_title: Aspose.OCR .NET API
title: Chỉ định các ký tự được phép trong OCR – Sử dụng Aspose.OCR cho .NET
url: /vi/net/ocr-settings/specify-allowed-characters/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Xác định các ký tự được phép OCR – Sử dụng Aspose.OCR cho .NET

Trong hướng dẫn này, bạn sẽ học cách **specify allowed characters ocr** với Aspose.OCR cho .NET, cho phép bạn giới hạn đầu ra OCR chỉ ở những ký tự bạn cần. Điều này đặc biệt hữu ích khi bạn cần **recognize digits image** các tệp như số sê-ri, mã hóa đơn, hoặc các chuỗi dạng mã vạch. Chúng tôi sẽ hướng dẫn qua quá trình cài đặt, mã và một vài kịch bản thực tế để bạn có thể áp dụng ngay lập tức.

## Câu trả lời nhanh
- **What does “specify allowed characters ocr” do?** Nó giới hạn OCR chỉ trong một tập hợp ký tự đã định trước, cải thiện độ chính xác cho dữ liệu mục tiêu.  
- **Which characters can I allow?** Bất kỳ tổ hợp nào bạn cần — chữ số, chữ cái, hoặc ký hiệu tùy chỉnh (ví dụ: “0123456789”).  
- **Why limit characters?** Giảm nhận dạng sai và tăng tốc xử lý khi bộ ký tự dự kiến đã biết.  
- **Do I need a license?** Bản dùng thử miễn phí hoạt động cho phát triển; giấy phép thương mại cần thiết cho môi trường sản xuất.  
- **Which .NET versions are supported?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## “specify allowed characters ocr” là gì?
Khi OCR quét một hình ảnh, nó cố gắng khớp mỗi mẫu hình ảnh với toàn bộ bảng chữ cái của các ký tự có thể. Bằng cách **specify allowed characters ocr**, bạn yêu cầu engine bỏ qua mọi thứ ngoài danh sách trắng của bạn, điều này cải thiện đáng kể độ chính xác nhận dạng cho các tập dữ liệu bị hạn chế.

## Tại sao sử dụng Aspose.OCR để nhận dạng hình ảnh chứa chữ số?
Aspose.OCR cung cấp một API sạch sẽ, linh hoạt cho các nhà phát triển .NET. Tùy chọn `AllowedCharacters` tích hợp cho phép bạn tập trung vào các kịch bản chỉ có chữ số mà không cần viết logic xử lý hậu kỳ tùy chỉnh. Điều này hoàn hảo cho:
- Đọc chỉ số đồng hồ, số hóa đơn, hoặc mã sản phẩm.  
- Xác thực dữ liệu do người dùng nhập được ghi lại từ các mẫu quét.  
- Tăng tốc xử lý hàng loạt khi bộ ký tự đã được biết trước.

## Yêu cầu trước

Trước khi bắt đầu viết mã, hãy chắc chắn rằng bạn đã có:

- Kiến thức cơ bản về phát triển .NET.  
- Thư viện **Aspose.OCR for .NET**. Bạn có thể tải xuống [tại đây](https://releases.aspose.com/ocr/net/).  
- Visual Studio (hoặc bất kỳ IDE .NET nào bạn ưa thích).

## Nhập các Namespace

Trong dự án .NET của bạn, nhập các namespace cần thiết để tận dụng chức năng của Aspose.OCR:

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

Bây giờ, chúng ta sẽ phân tích hướng dẫn thành một loạt các bước chi tiết:

## Cách xác định các ký tự được phép OCR – Hướng dẫn từng bước

### Bước 1: Đặt đường dẫn tới thư mục hình ảnh của bạn

Đầu tiên, xác định nơi lưu trữ các hình ảnh mẫu của bạn.

```csharp
string dataDir = "Your Document Directory";
```

### Bước 2: Khởi tạo Aspose.OCR với danh sách trắng chỉ chứa chữ số

Tạo một instance `AsposeOcr` và truyền vào các ký tự bạn muốn cho phép — trong trường hợp này là tất cả các chữ số.

```csharp
AsposeOcr api = new AsposeOcr("0123456789");
```

### Bước 3: Nhận dạng một dòng duy nhất chứa chữ số

Sử dụng phương thức `RecognizeLine` để trích xuất văn bản từ một hình ảnh chỉ chứa số.

```csharp
string result = api.RecognizeLine(dataDir + "0001460985.Jpeg");
```

### Bước 4: Xuất các chữ số đã nhận dạng

In ra kết quả lên console để bạn có thể kiểm tra đầu ra.

```csharp
Console.WriteLine(result);
```

### Bước 5: Sử dụng RecognitionSettings để kiểm soát chi tiết hơn

Nếu bạn cần kiểm soát chi tiết hơn — chẳng hạn buộc nhận dạng một dòng — bạn có thể sử dụng overload chấp nhận `RecognitionSettings`.

```csharp
AsposeOcr api2 = new AsposeOcr();
RecognitionResult result2 = api2.RecognizeImage(dataDir + "0001460985.Jpeg", 
    new RecognitionSettings { 
        AllowedCharacters = CharactersAllowedType.DIGITS,
        RecognizeSingleLine = true
    });
```

### Bước 6: Hiển thị kết quả trường hợp thứ hai

```csharp
Console.WriteLine(result2.RecognitionText);
```

### Bước 7: Xác nhận thực thi thành công

```csharp
Console.WriteLine("SpecifyAllowedCharacters executed successfully");
```

Bằng cách thực hiện các bước này, bạn đã học cách **specify allowed characters ocr** và hiệu quả **recognize digits image** nội dung bằng cách sử dụng Aspose.OCR cho .NET.

## Những lỗi thường gặp và khắc phục

- **Empty result:** Đảm bảo chất lượng hình ảnh đủ (độ tương phản rõ nét, ít nhiễu).  
- **Wrong characters returned:** Kiểm tra lại chuỗi whitelist có khớp chính xác với các ký tự bạn mong đợi.  
- **File not found:** Xác minh `dataDir` trỏ tới thư mục đúng và tên tệp khớp phân biệt chữ hoa/thường.

## Câu hỏi thường gặp

### Câu hỏi 1: Aspose.OCR cho .NET có phù hợp cho cả người mới bắt đầu và các nhà phát triển có kinh nghiệm không?
**A:** Hoàn toàn! API được thiết kế trực quan cho người mới bắt đầu đồng thời cung cấp các tùy chọn nâng cao cho người dùng chuyên nghiệp.

### Câu hỏi 2: Tôi có thể sử dụng Aspose.OCR cho .NET để nhận dạng ký tự trong nhiều ngôn ngữ không?
**A:** Có, Aspose.OCR hỗ trợ nhiều ngôn ngữ. Bạn có thể kết hợp các gói ngôn ngữ với tính năng allowed‑characters cho các kịch bản đa ngôn ngữ.

### Câu hỏi 3: Aspose.OCR cho .NET được cập nhật bao lâu một lần?
**A:** Các bản cập nhật được phát hành thường xuyên để thêm tính năng mới, cải thiện độ chính xác và đảm bảo tính tương thích. Kiểm tra [tài liệu](https://reference.aspose.com/ocr/net/) để biết chi tiết phiên bản mới nhất.

### Câu hỏi 4: Có bản dùng thử miễn phí cho Aspose.OCR cho .NET không?
**A:** Có, bạn có thể khám phá các tính năng bằng cách tải xuống [bản dùng thử miễn phí](https://releases.aspose.com/).

### Câu hỏi 5: Tôi có thể tìm kiếm hỗ trợ hoặc kết nối với cộng đồng ở đâu?
**A:** Truy cập [diễn đàn Aspose.OCR](https://forum.aspose.com/c/ocr/16) để đặt câu hỏi, chia sẻ kinh nghiệm và nhận trợ giúp từ các kỹ sư Aspose cũng như các nhà phát triển khác.

**Cập nhật lần cuối:** 2026-02-15  
**Kiểm tra với:** Aspose.OCR 24.11 cho .NET  
**Tác giả:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}