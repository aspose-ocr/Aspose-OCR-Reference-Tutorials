---
category: general
date: 2026-06-22
description: 使用 OCR 在 Python 中创建可搜索的 PDF —— 学习如何将图像转换为 PDF，识别文本 PDF，并自动化工作流程。
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- ocr image to pdf
- recognize text pdf
- python ocr pdf
language: zh
og_description: 使用 OCR 在 Python 中创建可搜索的 PDF。按照本分步教程，将图像转换为 PDF，识别文本 PDF，并实现文档处理自动化。
og_title: 在 Python 中创建可搜索的 PDF – 完整 OCR 指南
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Create searchable PDF in Python using OCR – learn how to convert image
    to PDF, recognize text PDF, and automate your workflow.
  headline: Create searchable PDF in Python – Complete OCR Guide
  type: TechArticle
- description: Create searchable PDF in Python using OCR – learn how to convert image
    to PDF, recognize text PDF, and automate your workflow.
  name: Create searchable PDF in Python – Complete OCR Guide
  steps:
  - name: Initialise the OCR engine
    text: The first thing you do is spin up an `OcrEngine` object. Think of it as
      turning on a scanner that’s ready to read your image.
  - name: Load the image you want to convert
    text: Next we feed the engine with an image stream. The `ImageStream.from_file`
      helper reads the file and wraps it in a format the OCR engine understands.
  - name: Tell the engine to output a searchable PDF
    text: By default many OCR SDKs output plain text. We need to switch the output
      format to PDF so the resulting file is both visual and searchable.
  - name: Prepare an in‑memory stream for the PDF data
    text: Instead of writing directly to disk, we capture the PDF in a `MemoryStream`.
      This keeps I/O fast and lets you pipe the bytes elsewhere (e.g., upload to S3)
      if you wish.
  - name: Run the recognition and write the PDF
    text: Now the heavy lifting happens. The `recognize` call reads the image, runs
      OCR, and streams the searchable PDF into `pdf_stream`.
  - name: Save the generated PDF to a file
    text: Finally, we dump the bytes from the memory stream onto disk. The resulting
      file can be opened in Adobe Reader, Preview, or any PDF viewer with full‑text
      search.
  type: HowTo
tags:
- OCR
- Python
- PDF
title: 在 Python 中创建可搜索的 PDF – 完整 OCR 指南
url: /zh/python-java/general/create-searchable-pdf-in-python-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Python 中创建可搜索的 PDF – 完整 OCR 指南

是否曾需要从扫描的合同中**创建可搜索的 PDF**但不知从何入手？你并不孤单——许多开发者在首次尝试将位图图像转换为可文本搜索的文档时都会遇到同样的难题。好消息是，只需一个小巧的 Python 脚本，你就可以**将图像转换为 PDF**，让 OCR 引擎识别每个单词，最终得到一个完美可搜索的文件。

在本教程中，我们将完整演示整个过程，从安装合适的库到处理多页文档等边缘情况。完成后，你将能够**ocr image to pdf**、**recognize text pdf**，并将工作流集成到更大的自动化流水线中。

## 所需条件

在深入之前，请确保你的机器上具备以下条件：

| 需求 | 为什么重要 |
|------|------------|
| Python 3.8 或更高 | 现代语法和更好的类型提示 |
| `ocr` Python 包（或任何兼容的 OCR SDK） | 提供 `OcrEngine`、`ImageStream` 和 PDF 输出 |
| 扫描图像（JPEG、PNG 或 TIFF） | 你将要转换的源文件 |
| 对输出 PDF 文件夹的写入权限 | 以便保存生成的文件 |

如果你尚未安装 SDK，请运行：

```bash
pip install ocr-sdk   # replace with the actual package name
```

> **专业提示：** 使用虚拟环境（`python -m venv .venv`）来保持依赖整洁。

## 工作流概览

1. **创建 OCR 引擎实例** – 识别的核心大脑。  
2. **加载图像** 你想要处理的图像。  
3. **配置引擎** 以输出可搜索的 PDF 而非纯文本。  
4. **准备内存流** 用于保存 PDF 字节。  
5. **运行识别** – 引擎读取图像，提取文本并写入 PDF。  
6. **将 PDF 持久化到磁盘**，以便在任何查看器中打开。

这就是全部，只需六行代码。让我们逐步拆解每个步骤。

---

## 创建可搜索的 PDF – 步骤详解 Python OCR 教程

### 步骤 1：初始化 OCR 引擎

首先，你需要实例化一个 `OcrEngine` 对象。可以把它想象成打开一台准备读取图像的扫描仪。

```python
import ocr

# Initialise the OCR engine – this is where all the magic begins
engine = ocr.OcrEngine()
```

> **原因说明：** 实例化引擎会分配内部缓冲区并加载语言数据。如果跳过此步骤，后续尝试设置图像时会导致 `NoneType` 错误。

### 步骤 2：加载要转换的图像

接下来，我们向引擎提供图像流。`ImageStream.from_file` 辅助方法读取文件并将其包装成 OCR 引擎能够理解的格式。

```python
# Load the source image – replace the path with your own file
image_path = "YOUR_DIRECTORY/contract.jpg"
engine.set_image(ocr.ImageStream.from_file(image_path))
```

> **边缘情况：** 如果你的源文件是多页 TIFF，请改用 `ocr.MultiPageImageStream.from_file`。引擎会自动将每页视为单独的 PDF 页面。

### 步骤 3：指示引擎输出可搜索的 PDF

默认情况下，许多 OCR SDK 输出纯文本。我们需要将输出格式切换为 PDF，这样生成的文件既有可视化效果，又可搜索。

```python
# Configure the engine to produce a searchable PDF
engine.get_settings().set_output_format(ocr.OutputFormat.PDF)
```

> **内部原理是什么？** 引擎现在在位图后面嵌入一个不可见的文字层，使你能够像在原生 PDF 中一样搜索单词。

### 步骤 4：为 PDF 数据准备内存流

我们不直接写入磁盘，而是将 PDF 捕获到 `MemoryStream` 中。这保持了 I/O 的高速，并且如果需要，可以将字节流传输到其他位置（例如上传到 S3）。

```python
# Create a memory buffer that will receive the PDF bytes
pdf_stream = ocr.MemoryStream()
```

### 步骤 5：运行识别并写入 PDF

现在繁重的工作开始了。`recognize` 调用读取图像，执行 OCR，并将可搜索的 PDF 流式写入 `pdf_stream`。

```python
# Perform OCR and write the searchable PDF into the memory stream
engine.recognize(pdf_stream)
```

> **常见陷阱：** 忘记调用 `engine.recognize` 会导致 `pdf_stream` 为空，尝试保存时会抛出 `ValueError`。如果需要验证是否生成了数据，请始终检查 `pdf_stream.length`。

### 步骤 6：将生成的 PDF 保存到文件

最后，我们将内存流中的字节写入磁盘。生成的文件可以在 Adobe Reader、Preview 或任何支持全文搜索的 PDF 查看器中打开。

```python
output_path = "YOUR_DIRECTORY/contract_searchable.pdf"

# Write the PDF bytes to a file
with open(output_path, "wb") as f:
    f.write(pdf_stream.to_bytes())
print(f"✅ Searchable PDF saved to {output_path}")
```

> **你将看到的结果：** 打开 PDF，按 `Ctrl+F`，输入原始扫描中出现的单词，查看器会立即高亮显示。这正是 **searchable PDF** 的标志。

## 将图像转换为 PDF – 调整设置以获得最佳效果

如果你的主要目标是仅**将图像转换为 PDF**而不进行 OCR，可以跳过第 3 步并将输出格式设为 `ocr.OutputFormat.IMAGE_PDF`。引擎会将位图嵌入为 PDF 页面，但不包含隐藏的文字层。

```python
engine.get_settings().set_output_format(ocr.OutputFormat.IMAGE_PDF)
```

当你需要忠实的视觉复制但不在乎可搜索性时，请使用此模式——例如用于归档且不需要 OCR 的场景。

## 识别文本 PDF – 添加语言包和 DPI 控制

为了获得强大的 **recognize text PDF** 体验，请考虑以下可选调整：

```python
settings = engine.get_settings()
settings.set_language("eng+spa")          # English + Spanish support
settings.set_dpi(300)                     # Higher DPI improves accuracy
settings.enable_auto_rotate(True)         # Auto‑rotate skewed scans
```

> **为什么要调整 DPI？** 更高的分辨率为 OCR 引擎提供更多像素进行分析，减少低质量扫描的误识别。

## Python OCR PDF – 集成到更大的流水线中

现在你已经可以用几行代码实现 **python ocr pdf**，想象一下将此逻辑嵌入 Flask API：

```python
from flask import Flask, request, send_file
import io, ocr

app = Flask(__name__)

@app.route("/upload", methods=["POST"])
def upload():
    file = request.files["image"]
    engine = ocr.OcrEngine()
    engine.set_image(ocr.ImageStream.from_bytes(file.read()))
    engine.get_settings().set_output_format(ocr.OutputFormat.PDF)
    pdf_stream = ocr.MemoryStream()
    engine.recognize(pdf_stream)

    return send_file(
        io.BytesIO(pdf_stream.to_bytes()),
        mimetype="application/pdf",
        as_attachment=True,
        download_name="searchable.pdf"
    )
```

这个小型端点允许客户端 POST 一张图像并即时收到 **searchable PDF**——非常适合 SaaS 文档处理服务。

## 常见陷阱：当你 **ocr image to pdf** 时

| 症状 | 可能原因 | 解决方案 |
|------|----------|----------|
| 空白 PDF 页面 | 图像未加载（`engine.set_image` 使用了错误路径） | 验证路径并使用 `os.path.abspath` |
| 没有可搜索的文本 | 输出格式仍为 `IMAGE_PDF` | 明确调用 `set_output_format(ocr.OutputFormat.PDF)` |
| 字符乱码 | 语言包错误 | 使用 `settings.set_language("eng")` 加载正确的语言 |
| 大文件处理慢 | 在高分辨率图像上使用默认 DPI（72） | 将 DPI 提升至 300 或对页面进行批处理 |

## 完整、可运行的示例（可直接复制粘贴）

```python
import ocr

def create_searchable_pdf(image_path: str, output_path: str) -> None:
    """
    Convert a scanned image to a searchable PDF using the ocr SDK.
    """
    # 1️⃣ Initialise engine
    engine = ocr.OcrEngine()

    # 2️⃣ Load image
    engine.set_image(ocr.ImageStream.from_file(image_path))

    # 3️⃣ Set output to searchable PDF
    engine.get_settings().set_output_format(ocr.OutputFormat.PDF)

    # Optional: improve accuracy
    settings = engine.get_settings()
    settings.set_language("eng")   # adjust as needed
    settings.set_dpi(300)

    # 4️⃣ Prepare in‑memory stream
    pdf_stream = ocr.MemoryStream()

    # 5️⃣ Run OCR
    engine.recognize(pdf_stream)

    # 6️⃣ Persist PDF
    with open(output_path, "wb") as f:
        f.write(pdf_stream.to_bytes())
    print(f"✅ Searchable PDF created at: {output_path}")

if __name__ == "__main__":
    create_searchable_pdf(
        image_path="YOUR_DIRECTORY/contract.jpg",
        output_path="YOUR_DIRECTORY/contract_searchable.pdf"
    )
```

运行脚本，打开生成的 PDF，尝试搜索原始扫描中出现的单词。如果一切顺利，你已经掌握了使用 Python **create searchable pdf** 的技巧。

## 结论

我们已经介绍了使用 Python OCR 库 **create searchable PDF** 所需的全部内容：初始化引擎、加载图像、配置 PDF 输出、流式处理结果，最后保存到磁盘。你还了解了如何 **convert image to PDF**，以及微调 **

## 接下来你应该学习什么？

以下教程涵盖与本指南技术密切相关的主题。每个资源都包含完整的可运行代码示例和逐步解释，帮助你掌握更多 API 功能，并在自己的项目中探索替代实现方案。

- [识别 PDF 文本 – 使用 Aspose.OCR for Java 的 OCR 操作](/ocr/english/java/ocr-operations/)
- [如何在 .NET 中使用 Aspose.OCR OCR PDF](/ocr/english/net/text-recognition/recognize-pdf/)
- [将图像转换为 PDF C# – 保存多页 OCR 结果](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}