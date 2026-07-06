---
category: general
date: 2026-05-03
description: 使用 Aspose OCR 在 Python 中提取图像文字。学习一步步的 Python OCR 教程，支持混合的拉丁文和西里尔文。
draft: false
keywords:
- extract text from image python
- Aspose OCR Python
- image to text conversion
- mixed language OCR
- Python OCR tutorial
language: zh
og_description: 快速使用 Python 从图像中提取文本。本指南展示了如何在 Python 中使用 Aspose OCR 处理混合拉丁‑西里尔字母的图像。
og_title: 使用 Python 从图像提取文本 – 完整 Aspose OCR 演练
tags:
- OCR
- Python
- Aspose
title: 使用 Python 从图像提取文本 – 完整的 Aspose OCR 指南
url: /zh/python-java/general/extract-text-from-image-python-complete-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从图像中提取文本 Python – 完整的 Aspose OCR 指南

是否曾经需要 **extract text from image python**，但不确定哪个库能够同时处理拉丁字符和西里尔字符的混合？你并不是唯一遇到这种情况的人——开发者在对多语言截图进行 OCR 时经常会卡在这一步。

好消息是，Aspose OCR for Python 让整个过程几乎无痛。在本教程中，我们将演示如何安装包、应用许可证、加载包含多语言的图像，最后用几行代码提取识别出的文本。完成后，你将拥有一个可直接运行的脚本，随时可以放入任何项目中使用。

## 你将学到

- 如何在虚拟环境中设置 **Aspose OCR Python**。  
- 为什么提示语言（如拉丁文和西里尔文）可以加速检测。  
- 使用单一函数调用 **extract text from image python** 所需的完整代码。  
- 处理混合语言 OCR 时的常见陷阱以及规避方法。  

### 前置条件

- 已在机器上安装 Python 3.8 或更高版本。  
- 一份 Aspose OCR 许可证文件（`Aspose.OCR.Java.lic`）。免费试用可用于测试，但正式许可证会去除水印。  
- 一张包含拉丁字符和西里尔字符的 PNG/JPEG 图像（这里称为 `mixed_latin_cyrillic.png`）。  

只要上述条件满足，你就可以开始——无需额外框架或沉重的依赖。

---

## 第一步 – Extract Text from Image Python：安装 Aspose OCR

首先，从 PyPI 获取库，并确保环境能够找到许可证文件。

```bash
# Create a clean virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate

# Install the Aspose OCR package
pip install asposeocrcloud
```

> **专业提示：** 如果遇到权限错误，请在 `pip install` 命令后添加 `--user`，或以管理员身份运行终端。

库安装完毕后，我们将导入它并将引擎指向我们的许可证。

```python
import asposeocrcloud as ocr   # the library we just installed

# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Apply your license – replace the path with the actual location of your .lic file
ocr_engine.license = ocr.License()
ocr_engine.license.set_license(r"YOUR_DIRECTORY/Aspose.OCR.Java.lic")
```

为什么此时需要许可证？如果没有许可证，引擎会以 **评估模式** 运行，限制页面数量并在输出中添加水印。提前提供许可证可确保后续的 `recognize` 调用返回干净的文本。

---

## 第二步 – 加载包含混合拉丁‑西里尔内容的图像

接下来，将图片加载到内存中。Aspose OCR 使用其自有的 `Image` 类，屏蔽底层文件格式的差异。

```python
# Load the image that contains both Latin and Cyrillic characters
input_image = ocr.Image.from_file(r"YOUR_DIRECTORY/mixed_latin_cyrillic.png")
```

如果你在想其他格式是否支持——答案是肯定的，JPEG、BMP、TIFF 甚至 PDF 都受支持。只需更改文件扩展名，`from_file` 方法会自动处理其余工作。

---

## 第三步 – 为更快检测提供语言提示（可选但有帮助）

当你知道图像中包含哪些语言时，可以提前给引擎一个提示。这不是强制要求，但 **显著降低处理时间** 并提升混合语言 OCR 的准确性。

```python
# Provide language hints: Latin and Cyrillic
ocr_engine.config.language_hints = ["Latin", "Cyrillic"]
```

提示列表接受 Aspose OCR 支持的任何语言（例如 `"Arabic"`、`"Japanese"`）。如果跳过此步骤，引擎会尝试所有内置语言，在大批量处理时会更慢。

---

## 第四步 – 运行 OCR 引擎并提取文本

现在是关键时刻：真正进行字符识别。`recognize` 方法返回一个 `OcrResult` 对象，里面包含纯文本、置信度分数，甚至还有需要时的边界框信息。

```python
# Perform OCR on the loaded image
ocr_result = ocr_engine.recognize(input_image)

# The recognised text is available via the .text attribute
extracted_text = ocr_result.text
```

> **工作原理：** 在内部，Aspose OCR 将神经网络文本检测器与语言特定分类器相结合。通过传入 `Image` 对象，你无需手动进行二值化等预处理。

---

## 第五步 – 查看提取的文本

最后，将结果打印到控制台。在实际应用中，你可能会将其写入文件、写入数据库，或传递给翻译 API。

```python
print("Recognised text:")
print(extracted_text)
```

运行脚本后，你应该会看到类似以下的输出：

```
Recognised text:
Hello мир! This is a test.
```

该输出证明我们成功 **extract text from image python**，在一次调用中同时处理了拉丁和西里尔字符。

---

## 完整可运行示例

下面是完整脚本，可直接复制粘贴到名为 `extract_ocr.py` 的文件中。只需将占位路径替换为实际目录即可。

```python
import asposeocrcloud as ocr   # package installed via pip

# ------------------------------------------------------------
# Step 1 – Initialise engine and apply license
# ------------------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.license = ocr.License()
ocr_engine.license.set_license(r"YOUR_DIRECTORY/Aspose.OCR.Java.lic")   # path to your license file

# ------------------------------------------------------------
# Step 2 – Load the image (mixed Latin‑Cyrillic)
# ------------------------------------------------------------
input_image = ocr.Image.from_file(r"YOUR_DIRECTORY/mixed_latin_cyrillic.png")

# ------------------------------------------------------------
# Step 3 – (Optional) Hint the languages present
# ------------------------------------------------------------
ocr_engine.config.language_hints = ["Latin", "Cyrillic"]

# ------------------------------------------------------------
# Step 4 – Run OCR
# ------------------------------------------------------------
ocr_result = ocr_engine.recognize(input_image)

# ------------------------------------------------------------
# Step 5 – Display the recognised text
# ------------------------------------------------------------
print("Recognised text:")
print(ocr_result.text)
```

保存文件，激活虚拟环境，然后运行：

```bash
python extract_ocr.py
```

你应当会看到识别出的文本打印出来，证明脚本端到端工作正常。

---

## 常见问题与边缘情况

**如果图像模糊怎么办？**  
Aspose OCR 内置去倾斜和降噪功能，但对于严重退化的照片，你可能需要使用 OpenCV 进行预处理（例如，先做高斯模糊再阈值化）。`Image` 类也可以接受 NumPy 数组，这样就能在调用 `recognize` 前链式自定义滤镜。

**能一次处理整个文件夹的图像吗？**  
完全可以。将逻辑包装在 `for` 循环中，将 `from_file` 换成读取每个文件名，并把结果存入字典。如果使用云版，请注意遵守 API 速率限制。

**每种语言需要单独的许可证吗？**  
不需要，单个 Aspose OCR 许可证覆盖所有受支持语言。`language_hints` 列表仅用于性能提示。

**PDF 输入怎么办？**  
将 `Image.from_file` 替换为 `ocr.Image.from_file("document.pdf")`。OCR 引擎会自动对每页进行光栅化并返回合并后的文本。

---

## 结论

我们已经展示了一种简洁、可投产的方式，使用 Aspose OCR **extract text from image python**。从安装、授权、加载、语言提示、识别到显示，这几步涵盖了获取可靠的拉丁‑西里尔混合内容所需的全部要点。

接下来，你可以探索批量 **image to text conversion**、将输出集成到 **Python OCR tutorial** 的自然语言处理流程，或尝试其他语言提示以处理多语言文档。可能性无限，代码已经在你手中。

有其他使用场景或遇到问题？欢迎留言分享经验，让我们一起讨论。祝编码愉快！  

![Extract text from image python example](/images/extract-text-from-image-python.png "Screenshot showing OCR output – extract text from image python")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}