---
category: general
date: 2026-06-25
description: 加载图像进行 OCR，并使用 aocr 的逐步 Python 教程对 PNG 执行 OCR。学习调试、日志记录和最佳实践。
draft: false
keywords:
- load image for OCR
- perform OCR on PNG
- aocr logging setup
- OCR debugging Python
- image preprocessing OCR
language: zh
og_description: 加载图像进行 OCR，并使用 aocr 对 PNG 执行 OCR。本指南将带您了解日志记录、图像加载和识别，并提供完整代码。
og_title: 加载图像进行 OCR – 步骤分步 Python 教程
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Load image for OCR and perform OCR on PNG with a step‑by‑step Python
    tutorial using aocr. Learn debugging, logging, and best practices.
  headline: Load Image for OCR – Complete Guide to Perform OCR on PNG Files
  type: TechArticle
- questions:
  - answer: Usually not. `aocr` handles PNG natively, but if the image is huge (>10
      MP) you might want to downscale first to speed up processing.
    question: Do I need to convert the PNG to another format?
  - answer: Rotate the log after each run or limit the level to `INFO` once you’re
      confident the pipeline works.
    question: What if the logger file grows too large?
  - answer: Absolutely. Just call `ocr_png` for each file; the function creates a
      fresh logger each time, keeping logs isolated.
    question: Can I process multiple images in a loop?
  - answer: Yes – `engine.result` also contains `boxes` and `confidences`. Explore
      the `aocr` docs for `result.boxes` if you need layout information.
    question: Is there a way to get bounding boxes instead of plain text?
  type: FAQPage
tags:
- OCR
- Python
- aocr
title: 加载图像进行 OCR – 完整指南：在 PNG 文件上执行 OCR
url: /zh/python/general/load-image-for-ocr-complete-guide-to-perform-ocr-on-png-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 加载图像进行 OCR – 完整指南：在 PNG 文件上执行 OCR

是否曾经需要**加载图像进行 OCR**却不确定如何进行合适的调试？你并不孤单。在许多项目中，第一道难题就是将 PNG 导入引擎，同时还能看到内部的运行情况。

在本教程中，我们将手把手教你使用 `aocr` 库**在 PNG 上执行 OCR**的全部步骤——从设置详细输出的日志记录器到实际识别文本。完成后，你将拥有一个可在任何 Python 项目中直接使用的可复用脚本，并且了解每个环节为何重要。

## 你将学到的内容

- 如何初始化 `aocr` 日志记录器，以便追踪每一步。
- 使用 `aocr.OcrEngine` **加载图像进行 OCR**的完整代码。
- 如何配置日志级别以获取细粒度的调试信息。
- 运行引擎**在 PNG 上执行 OCR**并获取结果。
- 处理常见问题的技巧，如文件缺失或不支持的格式。

不需要事先了解 `aocr`；只要有可用的 Python 3 环境和一张想要读取的图片即可。让我们开始吧。

![load image for OCR example](assets/load-image-ocr.png "Illustration of loading an image for OCR in Python")

## 前置条件

| 要求 | 为什么重要 |
|------|------------|
| Python 3.8+ | `aocr` 面向现代解释器并使用类型提示。 |
| 已安装 `aocr` 库（`pip install aocr`） | 没有该包我们使用的类将不存在。 |
| 需要读取的 PNG 图像 | 本教程聚焦于**在 PNG 上执行 OCR**，因此 PNG 是必需的。 |
| 对日志目录的写权限 | 日志记录器需要创建 `ocr_debug.log`。 |

如果缺少上述任意项，请立即安装——只需一分钟。

```bash
pip install aocr
```

## 步骤 1：加载图像进行 OCR – 初始化日志记录

在处理图像之前，先设置日志记录器。调试 OCR 时，如果看不到引擎的内部操作会非常头疼。`aocr.Logging` 类会将所有信息写入文件，将级别设为 `DEBUG` 后，你可以看到每一次内部调用。

```python
import aocr

# Create a logger instance
ocr_logger = aocr.Logging()
# Choose where the log file will live – adjust the path to suit your project
ocr_logger.set_output_file("logs/ocr_debug.log")

# DEBUG gives you the most detail; you can switch to INFO for less noise
ocr_logger.set_level(aocr.LoggingLevel.DEBUG)
```

**为什么重要：**  
如果 OCR 引擎找不到文件或图像格式不受支持，日志记录器会捕获异常堆栈信息，帮助你避免后期的无尽猜测。

## 步骤 2：在 PNG 上执行 OCR – 配置引擎

日志记录器准备好后，将其绑定到 OCR 引擎。此步骤将两者关联，使每一次引擎操作都被记录。

```python
# Initialise the OCR engine
ocr_engine = aocr.OcrEngine()
# Plug the logger into the engine
ocr_engine.logging = ocr_logger
```

**小贴士：**  
同一个 `ocr_engine` 实例可以重复用于多张图片。批量处理时记得清除之前的状态。

## 步骤 3：加载图像进行 OCR – 读取 PNG 文件

下面进入教程核心：实际**加载图像进行 OCR**。`load_image` 方法接受文件路径；它会在内部将 PNG 解码为引擎可识别的位图。

```python
# Path to the PNG you want to read
image_path = "samples/invoice.png"

# Load the image – this is where we “load image for OCR”
ocr_engine.load_image(image_path)
```

### 需要注意的边缘情况

1. **文件未找到** – 若路径错误，`aocr` 会抛出 `FileNotFoundError`。日志会记录此信息，你也可以自行捕获：

   ```python
   try:
       ocr_engine.load_image(image_path)
   except FileNotFoundError as e:
       print(f"❌ Could not locate {image_path}: {e}")
       raise
   ```

2. **不支持的格式** – 虽然 PNG 通常受支持，但损坏的文件可能触发 `UnsupportedFormatError`。此时可先使用 Pillow 将图像转换为干净的 PNG 再加载。

## 步骤 4：在 PNG 上执行 OCR – 运行识别

图像已加载到内存后，终于可以**在 PNG 上执行 OCR**。`recognize` 方法会启动引擎的流水线（预处理、分割、分类），并填充结果对象。

```python
# Execute the OCR process
ocr_engine.recognize()
```

调用完毕后，引擎会持有识别出的文本。你可以通过 `result` 属性访问它：

```python
# Retrieve the plain text output
recognized_text = ocr_engine.result.text
print("📝 OCR Result:")
print(recognized_text)
```

**为什么要检查结果：**  
某些 OCR 引擎在低对比度图像上会返回空字符串。立即看到结果可以帮助你决定是否需要先进行预处理（例如提升对比度）再重新运行。

## 步骤 5：封装为可复用函数

将上述步骤整合成一个函数，便于在其他脚本或 Web 服务中调用。这也展示了如何在一次调用中**加载图像进行 OCR**并**在 PNG 上执行 OCR**。

```python
def ocr_png(image_path: str, log_dir: str = "logs") -> str:
    """
    Load a PNG image, run aocr OCR, and return the extracted text.
    
    Parameters
    ----------
    image_path : str
        Full path to the PNG file.
    log_dir : str, optional
        Directory where the debug log will be written.
    
    Returns
    -------
    str
        The plain‑text OCR result.
    """
    import os
    import aocr

    # Ensure the log directory exists
    os.makedirs(log_dir, exist_ok=True)

    # ---------- Logging ----------
    logger = aocr.Logging()
    logger.set_output_file(os.path.join(log_dir, "ocr_debug.log"))
    logger.set_level(aocr.LoggingLevel.DEBUG)

    # ---------- Engine ----------
    engine = aocr.OcrEngine()
    engine.logging = logger

    # ---------- Load Image ----------
    try:
        engine.load_image(image_path)
    except Exception as exc:
        logger.error(f"Failed to load image {image_path}: {exc}")
        raise

    # ---------- Recognize ----------
    engine.recognize()
    return engine.result.text

# Example usage
if __name__ == "__main__":
    txt = ocr_png("samples/invoice.png")
    print("\n--- Extracted Text ---\n")
    print(txt)
```

运行脚本后，会在 `logs` 文件夹生成详细的 `ocr_debug.log`，并在控制台打印识别出的文本。现在你拥有了一个**在 PNG 上执行 OCR**的实用工具，可以在任意项目中直接导入使用。

## 常见问题与注意事项

- **需要把 PNG 转换成其他格式吗？**  
  通常不需要。`aocr` 原生支持 PNG，但如果图像非常大（>10 MP），可以先缩小以加快处理速度。

- **日志文件会不会变得太大？**  
  可以在每次运行后轮转日志，或在确认流水线正常后将日志级别调回 `INFO`。

- **可以在循环中处理多张图片吗？**  
  完全可以。对每个文件调用 `ocr_png` 即可；函数会为每次运行创建独立的日志记录器，保持日志互不干扰。

- **如何获取文本框而不是纯文本？**  
  可以。`engine.result` 同时包含 `boxes` 和 `confidences`。如果需要布局信息，请查阅 `aocr` 文档中的 `result.boxes`。

## 结论

现在，你已经掌握了使用 `aocr` 库**加载图像进行 OCR**并**在 PNG 上执行 OCR**的完整流程，配合稳健的日志设置，使调试变得轻而易举。示例函数封装了整个工作流，随时可以放入任何项目并立即开始提取文本。

下一步可以尝试使用不同的图像类型（JPEG、TIFF）观察准确率变化，或实验阈值化等预处理技术，以提升噪声扫描的识别效果。如果对结构化数据（表格、表单）提取感兴趣，查看 `aocr` 的版面分析章节——它们与本教程构建的基础完美契合。

祝编码愉快，愿你的 OCR 流程永远无错！

## 接下来你可以学习什么？

以下教程涵盖与本指南紧密相关的主题，帮助你在已有技术之上进一步扩展。每篇资源都提供完整可运行的代码示例，并配有逐步解释，助你掌握更多 API 功能并在项目中探索替代实现方案。

- [使用 Aspose OCR 从图像中提取文本 – 步骤指南](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [如何对图像进行 OCR – 在 OCR 图像识别中执行 OCR](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)
- [从图像中提取文本 – 使用 Aspose.OCR for .NET 进行 OCR 优化](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}