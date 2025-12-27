---
date: 2025-12-27
description: Tìm hiểu cách sử dụng chuyển đổi hình ảnh OCR sang văn bản với Aspose.OCR
  cho .NET, chỉ định các ký tự cho phép và tinh chỉnh cài đặt nhận dạng OCR. Bao gồm
  mã cho việc nhận dạng hình ảnh chữ số.
linktitle: 'ocr image to text: Specify Allowed Characters in OCR'
second_title: Aspose.OCR .NET API
title: 'ocr hình ảnh sang văn bản: Chỉ định các ký tự được phép trong OCR'
url: /vi/net/ocr-settings/specify-allowed-characters/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ocr image to text: Chỉ định các ký tự được phép trong OCR

## Introduction

Trong bối cảnh công nghệ không ngừng phát triển, Nhận dạng ký tự quang học (OCR) – hoặc chuyển đổi **ocr image to text** – đã trở thành một công cụ mang tính chuyển đổi, cho phép máy móc hiểu được văn bản từ hình ảnh. Aspose.OCR cho .NET nổi bật như một giải pháp mạnh mẽ, cung cấp tích hợp liền mạch cho các nhà phát triển muốn có khả năng OCR mạnh mẽ trong các ứng dụng .NET của họ.

## Quick Answers
- **“Specify Allowed Characters” làm gì?** Nó giới hạn đầu ra của OCR chỉ trong một tập hợp ký tự đã định, chẳng hạn chỉ các chữ số.  
- **Phương thức nào trích xuất một dòng văn bản duy nhất?** `RecognizeLine` trả về dòng đầu tiên mà nó phát hiện.  
- **Tôi có thể thay đổi cài đặt nhận dạng OCR ngay lập tức không?** Có – sử dụng `RecognitionSettings` để điều chỉnh các tùy chọn như `AllowedCharacters`.  
- **Có phiên bản dùng thử không?** Chắc chắn, tải bản dùng thử miễn phí từ trang Aspose.  
- **Các phiên bản .NET nào được hỗ trợ?** Tất cả các phiên bản .NET Framework và .NET Core/5/6 hiện đại.

## Prerequisites

Trước khi bắt đầu hướng dẫn, hãy đảm bảo bạn đã chuẩn bị các yêu cầu sau:

- Kiến thức vững về phát triển .NET.  
- Thư viện Aspose.OCR cho .NET. Bạn có thể tải xuống [tại đây](https://releases.aspose.com/ocr/net/).  
- Quen thuộc với Visual Studio hoặc bất kỳ môi trường phát triển .NET nào bạn ưa thích.

## Import Namespaces

Trong dự án .NET của bạn, nhập các namespace cần thiết để tận dụng hiệu quả các chức năng của Aspose.OCR cho .NET:

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

Bây giờ, hãy chia nhỏ hướng dẫn thành một loạt các bước chi tiết:

## Step 1: Specify Allowed Characters in ocr image to text

Bước 1: Chỉ định các ký tự được phép trong ocr image to text

Đầu tiên, thiết lập đường dẫn tới thư mục tài liệu của bạn:

```csharp
string dataDir = "Your Document Directory";
```

## Step 2: Initialize Aspose.OCR with Allowed Symbols (recognize digits image)

Bước 2: Khởi tạo Aspose.OCR với các ký hiệu được phép (nhận dạng hình ảnh chữ số)

Tạo một thể hiện của `AsposeOcr`, chỉ định các ký hiệu được phép. Trong trường hợp này, chúng ta chỉ cho phép các chữ số (0‑9):

```csharp
AsposeOcr api = new AsposeOcr("0123456789");
```

## Step 3: Recognize Image

Bước 3: Nhận dạng hình ảnh

Sử dụng thể hiện `AsposeOcr` để nhận dạng văn bản từ một hình ảnh:

```csharp
string result = api.RecognizeLine(dataDir + "0001460985.Jpeg");
```

## Step 4: Display Recognized Text

Bước 4: Hiển thị văn bản đã nhận dạng

In văn bản đã nhận dạng ra console:

```csharp
Console.WriteLine(result);
```

## Step 5: Second Case – Recognize Image with Specific OCR Recognition Settings

Bước 5: Trường hợp thứ hai – Nhận dạng hình ảnh với Cài đặt Nhận dạng OCR cụ thể

Khởi tạo một thể hiện `AsposeOcr` khác, lần này với các cài đặt chi tiết hơn để minh họa cách sử dụng **ocr recognition settings**:

```csharp
AsposeOcr api2 = new AsposeOcr();
RecognitionResult result2 = api2.RecognizeImage(dataDir + "0001460985.Jpeg", 
    new RecognitionSettings { 
        AllowedCharacters = CharactersAllowedType.DIGITS,
        RecognizeSingleLine = true
    });
```

## Step 6: Display Second Case Recognized Text

Bước 6: Hiển thị văn bản đã nhận dạng của trường hợp thứ hai

In văn bản đã nhận dạng từ trường hợp thứ hai ra console:

```csharp
Console.WriteLine(result2.RecognitionText);
```

## Step 7: Successful Execution

Bước 7: Thực thi thành công

Cuối cùng, xác nhận việc thực thi thành công của hướng dẫn **SpecifyAllowedCharacters**:

```csharp
Console.WriteLine("SpecifyAllowedCharacters executed successfully");
```

Bằng cách thực hiện các bước này, bạn đã mở khóa khả năng **chỉ định các ký tự được phép** trong nhận dạng hình ảnh OCR bằng Aspose.OCR cho .NET, cho phép chuyển đổi **ocr image to text** chính xác cho các kịch bản chỉ chứa chữ số.

## Why Use Allowed‑Character Filtering?

Tại sao nên sử dụng lọc ký tự được phép?

- **Độ chính xác cao hơn:** Giới hạn tập ký tự giúp giảm nhận dạng sai, đặc biệt trong các hình ảnh nhiễu.  
- **Tăng hiệu năng:** Engine OCR bỏ qua các glyph không liên quan, tăng tốc quá trình xử lý.  
- **Tuân thủ:** Áp dụng định dạng dữ liệu (ví dụ: số hóa đơn, mã seri) ngay ở giai đoạn OCR.  

## Common Pitfalls & Tips

Những sai lầm thường gặp & Mẹo

- **Pitfall:** Cung cấp một chuỗi rỗng cho các ký tự được phép sẽ tắt bộ lọc.  
  **Tip:** Luôn truyền một chuỗi không rỗng hoặc sử dụng enum `CharactersAllowedType`.  

- **Pitfall:** Sử dụng `RecognizeLine` trên tài liệu đa dòng có thể bỏ lỡ dữ liệu.  
  **Tip:** Chuyển sang `RecognizeImage` với `RecognizeSingleLine = false` để trích xuất toàn trang.  

- **Pitfall:** Quên kết hợp đúng đường dẫn thư mục có thể gây `FileNotFoundException`.  
  **Tip:** Sử dụng `Path.Combine(dataDir, "file.jpg")` để có đường dẫn độc lập với nền tảng.  

## Frequently Asked Questions

Câu hỏi thường gặp

**Q:** Aspose.OCR cho .NET có phù hợp cho cả người mới bắt đầu và các nhà phát triển có kinh nghiệm không?  
**A:** Chắc chắn! API trực quan cho người mới, đồng thời cung cấp các cài đặt nâng cao cho người dùng chuyên nghiệp.

**Q:** Tôi có thể sử dụng Aspose.OCR cho .NET để nhận dạng ký tự trong nhiều ngôn ngữ không?  
**A:** Có, Aspose.OCR hỗ trợ nhiều ngôn ngữ; bạn cũng có thể kết hợp các gói ngôn ngữ cho dự án đa ngôn ngữ.

**Q:** Aspose.OCR cho .NET được cập nhật bao lâu một lần?  
**A:** Các bản cập nhật được phát hành thường xuyên để bắt kịp các phiên bản .NET mới và cải tiến OCR. Kiểm tra [tài liệu](https://reference.aspose.com/ocr/net/) để biết phiên bản mới nhất.

**Q:** Có bản dùng thử miễn phí cho Aspose.OCR cho .NET không?  
**A:** Có, bạn có thể khám phá các tính năng bằng cách tải xuống [bản dùng thử miễn phí](https://releases.aspose.com/).

**Q:** Tôi có thể tìm trợ giúp hoặc kết nối với cộng đồng để được hỗ trợ ở đâu?  
**A:** Truy cập [diễn đàn Aspose.OCR](https://forum.aspose.com/c/ocr/16) để giao lưu với các chuyên gia và các nhà phát triển khác.

---

**Cập nhật lần cuối:** 2025-12-27  
**Đã kiểm tra với:** Aspose.OCR 24.11 cho .NET  
**Tác giả:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}