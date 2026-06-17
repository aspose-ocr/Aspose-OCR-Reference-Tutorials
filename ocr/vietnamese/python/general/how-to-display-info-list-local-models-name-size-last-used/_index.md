---
category: general
date: 2026-01-12
description: Tìm hiểu cách hiển thị thông tin từ AsposeAI bằng cách liệt kê các mô
  hình cục bộ, hiển thị tên mô hình, kích thước và thời gian sử dụng lần cuối trong
  một ví dụ Python rõ ràng.
draft: false
keywords:
- how to display info
- list local models
- display model name
- show model size
- show last used
language: vi
og_description: 'Cách hiển thị thông tin từ AsposeAI: liệt kê các mô hình cục bộ,
  hiển thị tên mô hình, kích thước và thời gian sử dụng lần cuối với hướng dẫn Python
  đầy đủ.'
og_title: Cách hiển thị thông tin – Liệt kê các mô hình cục bộ, Tên, Kích thước, Lần
  cuối sử dụng
tags:
- AsposeAI
- Python
- Model Management
title: Cách hiển thị thông tin – Liệt kê các mô hình cục bộ, Tên, Kích thước, Lần
  cuối sử dụng
url: /vi/python/general/how-to-display-info-list-local-models-name-size-last-used/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Hiển Thị Thông Tin – Liệt Kê Các Mô Hình Cục Bộ, Tên, Kích Thước, Lần Sử Dụng Cuối Cùng

Bạn đã bao giờ tự hỏi **cách hiển thị thông tin** từ cài đặt AsposeAI của mình mà không cần dò tìm trong log hay giao diện UI chưa? Bạn không phải là người duy nhất. Trong nhiều pipeline khoa học dữ liệu, điều đầu tiên bạn cần là một cái nhìn nhanh về những mô hình nào đang có trên máy, chúng được đặt tên gì, kích thước bao nhiêu, và lần cuối bạn thao tác chúng khi nào.

Đó chính là những gì chúng ta sẽ đề cập: một đoạn mã Python ngắn gọn, end‑to‑end, **liệt kê các mô hình cục bộ**, sau đó **hiển thị tên mô hình**, **hiển thị kích thước mô hình**, và **hiển thị thời gian lần cuối sử dụng**. Không cần thư viện bên ngoài, không có phép màu ẩn—chỉ cần client AsposeAI mà bạn đã có.

Sau khi hoàn thành tutorial này, bạn sẽ có thể chèn đoạn mã vào bất kỳ script nào, chạy nó và ngay lập tức nhận được một bảng gọn gàng về các mô hình đã được cache cục bộ. Nó hoàn hảo để kiểm tra môi trường, xây dựng dashboard sức khỏe, hoặc chỉ đơn giản là thỏa mãn sự tò mò về những gì đang ẩn nấp trên đĩa.

## Yêu Cầu Trước

- Python 3.8 hoặc mới hơn (ví dụ sử dụng f‑strings, vì vậy 3.6+ là bắt buộc)
- Gói `asposeai` đã được cài đặt (`pip install asposeai`)
- Một giấy phép AsposeAI hợp lệ hoặc key dùng thử (client sẽ tự động lấy thông tin xác thực từ biến môi trường hoặc file cấu hình)

Nếu bạn đã đáp ứng các mục trên, tuyệt vời—cùng bắt đầu.

## Bước 1: Cách Hiển Thị Thông Tin – Khởi Tạo Client AsposeAI

Trước khi chúng ta có thể **liệt kê các mô hình cục bộ**, chúng ta cần một đối tượng client để giao tiếp với runtime của AsposeAI. Bước này là nền tảng; nếu thiếu sẽ gây ra `NameError` cho phần còn lại của mã.

```python
# Step 1: Create an instance of the AsposeAI client
# The client automatically reads credentials from the environment
aspose_ai = AsposeAI()
```

*Lý do quan trọng*: Khởi tạo client thiết lập một phiên làm việc với engine suy luận cục bộ, tải các thư viện native cần thiết. Nó cũng xác thực rằng giấy phép của bạn đang hoạt động, ngăn ngừa các lỗi khó hiểu khi bạn truy vấn mô hình sau này.

> **Mẹo chuyên nghiệp**: Nếu chạy trên máy CI, hãy đặt biến môi trường `ASPOSEAI_LICENSE` để client có thể khởi động mà không cần prompt tương tác.

## Bước 2: Liệt Kê Các Mô Hình Cục Bộ – Lấy Danh Sách Các Mô Hình Có Sẵn

Khi client đã sẵn sàng, chúng ta có thể **liệt kê các mô hình cục bộ**. Phương thức `list_local()` trả về một collection các đối tượng, mỗi đối tượng cung cấp các thuộc tính như `name`, `size_mb`, và `last_used`.

```python
# Step 2: Retrieve the list of locally available models
local_models = aspose_ai.list_local()
```

*Điều gì đang diễn ra phía sau*: `list_local()` quét thư mục nơi AsposeAI cache các file mô hình (`~/.asposeai/models` theo mặc định) và tạo ra các đối tượng metadata nhẹ. Quá trình này nhanh vì không tải trọng số mô hình—chỉ đọc một file JSON manifest nhỏ.

Nếu bạn muốn kiểm tra nhanh một mô hình nào đó đã được cache chưa, lời gọi này là cách nhanh nhất để xác nhận.

## Bước 3: Hiển Thị Tên Mô Hình, Kích Thước Mô Hình, và Lần Cuối Sử Dụng

Với danh sách mô hình trong tay, chúng ta cuối cùng **hiển thị thông tin** bằng cách duyệt collection và in ra từng thuộc tính. Đây là nơi chúng ta **hiển thị tên mô hình**, **hiển thị kích thước mô hình**, và **hiển thị thời gian lần cuối sử dụng** trong một dòng gọn gàng.

```python
# Step 3: Print each model's name, size (in MB), and last‑used timestamp
print("Available local models:")
print("-" * 50)
for model_info in local_models:
    # Using an f‑string to format the output cleanly
    print(f"{model_info.name} – {model_info.size_mb} MB – last used {model_info.last_used}")
```

**Kết quả mong đợi** (thời gian của bạn sẽ khác):

```
Available local models:
--------------------------------------------------
gpt‑tiny‑en – 120 MB – last used 2025-11-02 14:23:11
bert‑base‑fr – 420 MB – last used 2025-10-18 09:07:45
whisper‑large‑audio – 1580 MB – last used 2025-09-30 22:41:02
```

*Lý do chúng ta định dạng như vậy*: Dấu gạch ngang (`–`) ngăn cách các trường để dễ đọc, và dòng tiêu đề giúp đầu ra console trở nên thân thiện với mắt. Nếu bạn cần định dạng máy đọc được sau này (CSV, JSON), có thể dễ dàng thay `print` bằng `writer.writerow` hoặc `json.dump`.

### Xử Lý Các Trường Hợp Cạnh

- **Không có mô hình nào được cache** – `list_local()` trả về danh sách rỗng. Vòng lặp sẽ bỏ qua, chỉ in ra tiêu đề. Bạn có thể thêm một guard:

  ```python
  if not local_models:
      print("No local models found. Use aspose_ai.download(...) to fetch one.")
  ```

- **Thiếu thuộc tính** – Trong trường hợp hiếm khi manifest bị hỏng, việc truy cập `model_info.last_used` có thể gây `AttributeError`. Hãy bọc lệnh `print` trong `try/except` nếu bạn dự đoán có vấn đề như vậy.

- **Thư mục mô hình lớn** – Nếu có hàng trăm mô hình, hãy cân nhắc phân trang đầu ra hoặc ghi vào file thay vì in ra console.

## Tổng Quan Hình Ảnh (Tùy Chọn)

Nếu bạn thích một gợi ý nhanh bằng hình ảnh, sơ đồ dưới đây minh họa luồng từ khởi tạo client đến hiển thị cuối cùng.  

![Sơ đồ minh họa cách hiển thị thông tin từ client AsposeAI](/images/how-to-display-info.png "sơ đồ cách hiển thị thông tin")

*Alt text*: **cách hiển thị thông tin** – sơ đồ khởi tạo client AsposeAI, liệt kê mô hình, và hiển thị thông tin.

## Script Hoàn Chỉnh

Kết hợp tất cả lại, đây là script đầy đủ, sẵn sàng chạy:

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

"""
How to display info from AsposeAI:
List local models and show each model's name, size, and last‑used timestamp.
"""

from asposeai import AsposeAI

def main():
    # Initialize client
    aspose_ai = AsposeAI()

    # Retrieve local models
    local_models = aspose_ai.list_local()

    # Header
    print("Available local models:")
    print("-" * 50)

    if not local_models:
        print("No local models found. Use aspose_ai.download(...) to fetch one.")
        return

    # Display each model's details
    for model_info in local_models:
        try:
            print(f"{model_info.name} – {model_info.size_mb} MB – last used {model_info.last_used}")
        except AttributeError:
            # Fallback if any attribute is missing
            print(f"{model_info.name} – info incomplete")

if __name__ == "__main__":
    main()
```

Lưu lại dưới tên `list_models.py`, cấp quyền thực thi (`chmod +x list_models.py`), và chạy:

```bash
./list_models.py
```

Bạn sẽ thấy danh sách gọn gàng như đã trình bày ở trên.

## Kết Luận

Chúng ta đã đi qua **cách hiển thị thông tin** từ AsposeAI bằng cách **liệt kê các mô hình cục bộ**, sau đó **hiển thị tên mô hình**, **hiển thị kích thước mô hình**, và **hiển thị thời gian lần cuối sử dụng**. Cách tiếp cận này nhẹ, chỉ yêu cầu gói `asposeai` tiêu chuẩn, và có thể được chèn vào bất kỳ pipeline tự động hoá hay phiên gỡ lỗi nào.

Từ đây bạn có thể:

- Xuất kết quả ra CSV để phân tích trong bảng tính (`csv` module).
- Đưa các timestamp vào dashboard giám sát để cảnh báo mô hình lỗi thời.
- Kết hợp script này với `aspose_ai.download()` để tự động làm mới các mô hình chưa được sử dụng trong một thời gian.

Hãy nhớ, việc có cái nhìn rõ ràng về kho mô hình của bạn giúp tiết kiệm thời gian, giảm lãng phí dung lượng lưu trữ, và giữ cho các dịch vụ AI của bạn luôn hoạt động trơn tru. Hãy chạy thử script, tùy chỉnh định dạng theo sở thích, và biến nó thành công cụ không thể thiếu trong bộ công cụ của bạn.

Chúc lập trình vui vẻ, và mong các mô hình của bạn luôn luôn tươi mới!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}