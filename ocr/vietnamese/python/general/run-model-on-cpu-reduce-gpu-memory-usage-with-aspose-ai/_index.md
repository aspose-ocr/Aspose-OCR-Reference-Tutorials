---
category: general
date: 2026-06-22
description: Chạy mô hình trên CPU và học cách giảm việc sử dụng bộ nhớ GPU bằng cách
  cấu hình các lớp GPU trong Aspose AI. Hướng dẫn từng bước kèm đoạn mã.
draft: false
keywords:
- run model on cpu
- reduce gpu memory usage
- limit gpu layers
- configure gpu layers
language: vi
og_description: Chạy mô hình trên CPU và giảm tiêu thụ bộ nhớ GPU bằng cách cấu hình
  các lớp GPU. Hướng dẫn đầy đủ cho việc thiết lập mô hình Aspose AI.
og_title: Chạy mô hình trên CPU – Giảm việc sử dụng bộ nhớ GPU
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Run model on CPU and learn to reduce GPU memory usage by configuring
    GPU layers in Aspose AI. Step-by-step guide with code snippets.
  headline: Run Model on CPU – Reduce GPU Memory Usage with Aspose AI
  type: TechArticle
- description: Run model on CPU and learn to reduce GPU memory usage by configuring
    GPU layers in Aspose AI. Step-by-step guide with code snippets.
  name: Run Model on CPU – Reduce GPU Memory Usage with Aspose AI
  steps:
  - name: Attach any required post‑processors.
    text: Attach any required post‑processors.
  - name: Choose a configuration (`gpu_layers=0` for pure CPU, or a modest number
      for mixed mode).
    text: Choose a configuration (`gpu_layers=0` for pure CPU, or a modest number
      for mixed mode).
  - name: Initialize the model with that configuration.
    text: Initialize the model with that configuration.
  - name: Verify placement and run a test inference.
    text: Verify placement and run a test inference.
  type: HowTo
tags:
- AsposeAI
- CPU inference
- GPU optimization
title: Chạy mô hình trên CPU – Giảm việc sử dụng bộ nhớ GPU với Aspose AI
url: /vi/python/general/run-model-on-cpu-reduce-gpu-memory-usage-with-aspose-ai/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Chạy Mô Hình trên CPU – Giảm Sử Dụng Bộ Nhớ GPU với Aspose AI

Bạn đã bao giờ tự hỏi làm thế nào để **run model on CPU** khi máy chủ của bạn không có GPU sẵn có? Hoặc có thể bạn đang gặp lỗi hết bộ nhớ trên một GPU khiêm tốn và cần **reduce GPU memory usage** mà không làm giảm quá nhiều tốc độ. Trong hướng dẫn này, chúng tôi sẽ đi qua chính xác những bước đó: gắn một post‑processor, khởi tạo Aspose AI trên CPU, và tinh chỉnh số lượng lớp GPU để giữ dấu chân bộ nhớ ở mức tối thiểu.

Chúng tôi sẽ bao phủ mọi thứ từ dòng code đầu tiên cho tới việc xác nhận rằng mô hình thực sự đang sử dụng cấu hình bạn yêu cầu. Khi kết thúc, bạn sẽ có thể **run model on CPU**, **limit GPU layers**, và **configure GPU layers** cho bất kỳ khối lượng công việc nào—không có ma thuật, chỉ là Python thuần túy.

## Yêu Cầu Trước

- Python 3.8+ đã được cài đặt (code sử dụng type hints nhưng vẫn hoạt động trên các phiên bản cũ hơn).
- `asposeai` package (install via `pip install asposeai`)
- Kiến thức cơ bản về các khái niệm suy luận mạng nơ‑ron (bạn không cần bằng tiến sĩ, chỉ cần tò mò).
- Tùy chọn: một máy có GPU để thử nghiệm sự khác biệt giữa chạy trên CPU và GPU runs

![Sơ đồ minh họa cách chạy mô hình trên CPU thay vì GPU](run-model-on-cpu-diagram.png)

## Bước 1: Gắn Post‑Processor Kiểm Tra Chính Tả (Không Cần Cài Đặt Tùy Chỉnh)

Trước khi chúng ta nghĩ đến CPU hay GPU, hãy kết nối post‑processor kiểm tra chính tả mà Aspose AI cung cấp. Đây là thói quen tốt để gắn post‑processor sớm để chúng trở thành một phần của mọi lời gọi suy luận.

```python
from asposeai import AI, spell_check_processor

# Create the AI client
ai = AI()

# Attach the built‑in spell‑check processor; no custom settings required
ai.set_post_processor(spell_check_processor, custom_settings={})
```

*​Tại sao điều này quan trọng:* Post‑processors chạy **after** mô hình tạo ra các token thô. Bằng cách kết nối chúng ngay bây giờ, bạn đảm bảo rằng bất kỳ văn bản nào bạn tạo sau này—cho dù trên CPU hay GPU—đều được tự động làm sạch. Đó là một bước nhỏ ngăn ngừa các lỗi ở các bước sau.

## Bước 2: Chạy Mô Hình trên CPU – Khởi Tạo Aspose AI mà Không Dùng GPU

Bây giờ là phần cốt lõi của hướng dẫn: yêu cầu Aspose AI **run model on CPU**. SDK cung cấp `AsposeAIModelConfig`, trong đó tham số `gpu_layers` điều khiển số lượng lớp vẫn ở trên GPU. Đặt nó thành `0` buộc toàn bộ mạng chạy trên CPU.

```python
from asposeai import AsposeAIModelConfig

# Initialize the model configuration to use zero GPU layers (i.e., CPU only)
cpu_config = AsposeAIModelConfig(gpu_layers=0)

# Apply the configuration; this will load the model onto the CPU
ai.initialize(cpu_config)

print("✅ Model initialized on CPU – ready for inference.")
```

*​Điều gì đang diễn ra phía sau?* Khi `gpu_layers=0`, runtime cấp phát tất cả các tensor trong bộ nhớ host. Điều này loại bỏ nhu cầu về driver CUDA, cho phép script chạy trên hầu hết mọi máy chủ. Nhược điểm là tốc độ xử lý chậm hơn, nhưng đối với các công việc batch hoặc prototype độ trễ thấp, sự đơn giản thường vượt trội hơn tốc độ thuần túy.

## Bước 3: Giới Hạn Các Lớp GPU Để Giảm Sử Dụng Bộ Nhớ GPU

Nếu bạn có GPU nhưng bộ nhớ bị chật, bạn có thể **limit GPU layers** thay vì chuyển toàn bộ sang CPU. Bằng cách giữ lại một vài lớp đầu tiên trên GPU, bạn vẫn được hưởng lợi từ tăng tốc phần cứng trong khi giảm đáng kể việc tiêu thụ bộ nhớ.

```python
# Example: keep only the first 10 layers on the GPU; the rest run on CPU
limited_gpu_config = AsposeAIModelConfig(gpu_layers=10)

ai.initialize(limited_gpu_config)

print("✅ Model initialized with 10 GPU layers – memory usage trimmed.")
```

*​Tại sao việc giới hạn các lớp GPU lại hữu ích:* Các mô hình transformer hiện đại phân bổ phần lớn bộ nhớ cho mỗi lớp. Việc loại bỏ ngay cả một vài lớp khỏi GPU có thể giải phóng hàng trăm megabyte. Cách tiếp cận này hoàn hảo cho các “công việc bị giới hạn bộ nhớ” nơi bạn vẫn muốn tăng tốc cho các phép tính nặng nhất.

## Bước 4: Cấu Hình Các Lớp GPU Để Quản Lý Bộ Nhớ Linh Hoạt

Đôi khi bạn cần một cách tiếp cận chi tiết hơn—có thể bạn muốn **configure GPU layers** dựa trên kích thước công việc cụ thể. SDK cho phép bạn đọc tổng số lớp của mô hình và tính toán số lượng lớp GPU an toàn tại thời gian chạy.

```python
# Determine total number of layers (this is model‑specific; assume 36 for illustration)
total_layers = ai.model_info.total_layers  

# Choose a safe percentage, e.g., 25% of layers on GPU
gpu_layer_fraction = 0.25
desired_gpu_layers = int(total_layers * gpu_layer_fraction)

# Build the config dynamically
dynamic_config = AsposeAIModelConfig(gpu_layers=desired_gpu_layers)

ai.initialize(dynamic_config)

print(f"✅ Configured {desired_gpu_layers}/{total_layers} layers on GPU.")
```

*​Mẹo chuyên nghiệp:* Khi chạy trên máy chủ chia sẻ, hãy truy vấn bộ nhớ GPU khả dụng trước (`torch.cuda.get_device_properties(0).total_memory`) và điều chỉnh `desired_gpu_layers` cho phù hợp. Bước bổ sung này đảm bảo bạn không bao giờ quá tải GPU, điều mà nếu không sẽ gây ra lỗi OOM.

## Bước 5: Xác Minh Cấu Hình và Kiểm Tra Suy Luận

Sau khi thiết lập cấu hình, nên kiểm tra lại vị trí của từng lớp. Aspose AI cung cấp một phương pháp chẩn đoán trả về bản đồ các lớp tới các thiết bị.

```python
# Retrieve the device placement map
placement = ai.get_layer_placement()

cpu_layers = [l for l, dev in placement.items() if dev == "cpu"]
gpu_layers = [l for l, dev in placement.items() if dev == "gpu"]

print(f"Layers on CPU: {len(cpu_layers)}")
print(f"Layers on GPU: {len(gpu_layers)}")
```

Khi bạn đã hài lòng, chạy một lần suy luận nhanh để xem mọi thứ hoạt động:

```python
input_text = "The quick brown fox jumps over the lazy dog."
output = ai.process(input_text)

print("Model output:", output)
```

Nếu script in ra văn bản mong đợi và báo cáo vị trí khớp với cấu hình của bạn, bạn đã thành công **run model on CPU**, **reduce GPU memory usage**, và **configure GPU layers** cho kịch bản của mình.

## Những Rủi Ro Thường Gặp & Cách Tránh

| Triệu chứng | Nguyên nhân có thể | Cách khắc phục |
|------------|--------------------|----------------|
| `CUDA out of memory` error | Quá nhiều lớp GPU | Giảm `gpu_layers` hoặc chuyển sang `gpu_layers=0` |
| No output from `ai.process` | Mô hình chưa được khởi tạo | Đảm bảo `ai.initialize` được gọi **after** sau khi gắn post‑processor |
| Slow inference on GPU | Tất cả các lớp vẫn ở trên CPU | Kiểm tra `gpu_layers` > 0 và bản đồ thiết bị hiển thị việc sử dụng GPU |
| Unexpected spelling errors | Post‑processor chưa được gắn | Gọi `set_post_processor` trước `initialize` |

## Thêm: Chuyển Đổi Giữa CPU và GPU Khi Cần

Vì SDK khởi tạo lại mô hình mỗi khi bạn gọi `initialize`, bạn có thể chuyển đổi giữa CPU và GPU mà không cần khởi động lại script.

```python
def switch_to_cpu():
    ai.initialize(AsposeAIModelConfig(gpu_layers=0))
    print("🔄 Switched to CPU mode.")

def switch_to_gpu(layers=12):
    ai.initialize(AsposeAIModelConfig(gpu_layers=layers))
    print(f"🔄 Switched to GPU mode with {layers} layers.")
```

Chỉ cần gọi `switch_to_cpu()` khi bạn cần chạy với bộ nhớ thấp, và `switch_to_gpu(12)` khi bạn đã sẵn sàng cho tăng tốc.

## Kết Luận

Chúng tôi đã đi qua một ví dụ thực tế đầy đủ về cách **run model on CPU**, **reduce GPU memory usage**, **limit GPU layers**, và **configure GPU layers** với Aspose AI. Các bước rất đơn giản:

1. Gắn bất kỳ post‑processor cần thiết nào.  
2. Chọn một cấu hình (`gpu_layers=0` cho CPU thuần, hoặc một số vừa phải cho chế độ hỗn hợp).  
3. Khởi tạo mô hình với cấu hình đó.  
4. Xác minh vị trí và chạy một lần suy luận thử.  

Với những kỹ thuật này, bạn có thể giữ cho các pipeline suy luận của mình nhẹ nhàng, tránh các lỗi OOM tốn kém, và vẫn khai thác hiệu năng từ một GPU khiêm tốn khi có sẵn. Tiếp theo, bạn có thể khám phá các chiến lược batch, quantization, hoặc thậm chí chuyển một phần mô hình sang CPU trong khi giữ các attention head trên GPU—mỗi chủ đề này đều dựa trực tiếp trên nền tảng **configure GPU layers** mà bạn vừa nắm vững.

Có câu hỏi về kiến trúc mô hình cụ thể nào hoặc cần trợ giúp điều chỉnh số lượng lớp cho một

## Bạn Nên Học Gì Tiếp Theo?

Các hướng dẫn sau đây bao phủ các chủ đề liên quan chặt chẽ, xây dựng dựa trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ code hoàn chỉnh với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Hướng Dẫn Aspose OCR – Nhận Diện Ký Tự Quang Ánh](/ocr/english/)
- [Trích Xuất Văn Bản Từ Hình Ảnh với Aspose OCR – Hướng Dẫn Từng Bước](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Cách OCR Văn Bản Hình Ảnh Theo Ngôn Ngữ Sử Dụng Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}