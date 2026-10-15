---
category: general
date: 2026-04-26
description: 如何在 Python 中进行 OCR：学习使用基本 OCR 示例从图像提取文本并读取 TIFF 文件。附带快速可运行的代码。
draft: false
keywords:
- how to ocr python
- extract text from image
- read tiff file python
- basic ocr example
- convert scanned image text
language: zh
og_description: 如何使用 Python 进行 OCR：一步步指南，展示如何从图像中提取文本、在 Python 中读取 TIFF 文件，以及使用简单可运行的脚本转换扫描图像文本。
og_title: 如何使用 Python 进行 OCR – 基础 OCR 示例，提取文本
tags:
- OCR
- Python
- Image Processing
title: 如何在 Python 中进行 OCR – 基本 OCR 示例用于提取文本
url: /zh/python-java/general/how-to-ocr-python-basic-ocr-example-for-extracting-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# how to ocr python – 基础 OCR 示例：提取文本

有没有想过 **how to ocr python**，当你桌面上摆着一张扫描的 TIFF 时该怎么做？你并不是唯一一个盯着一堆图像文件并自问“怎么把文字取出来？”的人。好消息是，只要使用合适的库并遵循几个清晰的步骤，把图片转换成纯文本其实轻而易举。

在本教程中，我们将演示一个 **basic OCR example**，读取 TIFF 文件，提取文本，并将其打印到控制台。完成后，你将清楚地知道如何 **extract text from image** 文件，如何处理 TIFF 格式的特殊情况，以及在需要 **convert scanned image text** 为更有用的形式时该如何调整。没有隐藏的魔法——只有可以直接复制粘贴并立即运行的 Python 代码。

## 你需要准备的东西

在开始之前，请确保你已经拥有：

- 已安装 Python 3.9+（推荐使用最新的稳定版）。
- 一个可以通过 pip 安装的 OCR 库。本指南使用一个虚构的 `aocr` 包，它模拟了 Tesseract 等流行工具的行为；你以后可以换成 `pytesseract` 或 `easyocr`。
- 一张你想处理的 TIFF 图像——命名为 `input.tiff` 并放入代码中引用的文件夹。
- 对命令行有基本的了解（仅用于安装包）。

就这些。没有笨重的依赖，没有 Docker 容器，只需几行代码。

## 第一步 – 安装并导入依赖（how to ocr python）

首先，获取 OCR 包。打开终端并运行：

```bash
pip install aocr
```

如果你更倾向于使用真实的库，只需将 `aocr` 替换为 `pytesseract`，并单独安装 Tesseract 引擎。

接下来导入我们需要的内容。`pathlib` 中的 `Path` 类为跨操作系统处理文件路径提供了简洁的方式。

```python
# Step 1: Import the Path class for handling file paths
from pathlib import Path

# Import the OCR engine and image loader from the chosen library
from aocr import OcrEngine, Image
```

*为什么使用 `Path`？* 因为它抽象了斜杠（`/` 与 `\`）的差异，让你在拼接目录时无需担心底层操作系统。这一点在后期将脚本迁移到 CI 服务器时常常能省去很多麻烦。

## 第二步 – 创建 OCR 引擎实例（basic ocr example）

接下来，实例化 OCR 引擎。把 `OcrEngine` 想象成读取图片并输出字符的大脑。

```python
# Step 2: Create an instance of the OCR engine
ocr_engine = OcrEngine()
```

大多数 OCR 库都允许你在此处调整语言、DPI 或置信度阈值。对于这个 **basic OCR example**，我们使用默认设置，但如果需要处理多语言文档，可以稍后探索 `ocr_engine.config`。

## 第三步 – 加载你的 TIFF 图像（read tiff file python）

这一步对应 **read tiff file python** 的部分。TIFF 可以是多页的，但 `Image.load` 默认只读取第一页——这正好适用于单页扫描。

```python
# Step 3: Load the image you want to recognize
# Using a generic placeholder path makes it easy to adapt the example
ocr_engine.image = Image.load(Path("YOUR_DIRECTORY/input.tiff"))
```

将 `"YOUR_DIRECTORY"` 替换为实际存放 `input.tiff` 的文件夹。如果不确定脚本的运行目录，`Path.cwd()` 会打印当前工作目录，便于调试路径问题。

## 第四步 – 运行 OCR 过程（extract text from image）

现在魔法开始了。调用 `process()` 会把图像送入 OCR 流程并返回一个结果对象。

```python
# Step 4: Run the OCR process to extract text from the image
ocr_result = ocr_engine.process()
```

在幕后，引擎可能会先将图像转为灰度、应用阈值处理，然后送入神经网络。你无需管理这些步骤，库已经帮你抽象掉了。

## 第五步 – 打印识别出的文本（convert scanned image text）

最后，输出文本。在真实项目中，你可能会把它写入文件或数据库，但这里直接打印可以让示例保持简洁。

```python
# Step 5: Print the recognized text to the console
print(ocr_result.text)
```

运行脚本后，你应该会看到类似如下的输出：

```
Hello, world!
This is a sample scanned document.
```

如果输出乱码，请再次确认源图像是否清晰，以及 OCR 语言是否与文本匹配。

## 完整可运行脚本

将上述所有代码组合起来，就是下面这段完整、可直接运行的程序：

```python
# Full script: how to ocr python – basic OCR example

from pathlib import Path
from aocr import OcrEngine, Image  # Replace with your OCR library if needed

def main():
    # Initialize the OCR engine
    ocr_engine = OcrEngine()

    # Load the TIFF image (adjust the path as needed)
    image_path = Path("YOUR_DIRECTORY/input.tiff")
    if not image_path.is_file():
        raise FileNotFoundError(f"Could not find {image_path}. Make sure the file exists.")
    
    ocr_engine.image = Image.load(image_path)

    # Perform OCR
    ocr_result = ocr_engine.process()

    # Output the extracted text
    print("=== OCR Output ===")
    print(ocr_result.text)

if __name__ == "__main__":
    main()
```

### 预期输出

```
=== OCR Output ===
Your scanned document’s text appears here, line by line.
```

如果你需要 **convert scanned image text** 为可搜索的 PDF，可以将 `ocr_result.text` 通过 `reportlab` 等 PDF 生成器进行管道处理——但这又是另一个完整的教程了。

## 常见坑点与专业提示

- **低分辨率扫描**：OCR 在低于 150 DPI 时表现不佳。如果你的 TIFF 模糊，请先使用 Pillow (`Image.open(...).resize(...)`) 进行上采样。
- **多页文件**：对于多页 TIFF，遍历 `Image.load_multi_page()`（如果你的库支持）并将结果拼接起来。
- **语言支持**：多数引擎默认英文。比如将 `ocr_engine.language = "spa"` 设置为西班牙语。
- **空白处理**：OCR 常会产生多余的换行。可使用 `str.splitlines()` 或正则表达式清理输出。
- **性能**：批量处理时，复用同一个 `OcrEngine` 实例，而不是为每个文件重新创建。

## 扩展示例

既然已经掌握了单张图片的 **how to ocr python**，可以尝试以下进阶：

1. **批量处理** – 循环遍历一个 TIFF 文件夹，将每个结果写入对应的 `.txt` 文件。
2. **与 Pandas 集成** – 将提取的文本与元数据一起存入 DataFrame，便于快速分析。
3. **混合方案** – 将 OCR 与 `spaCy` 等 NLP 库结合，抽取发票中的实体（姓名、日期、金额）等信息。
4. **其他文件格式** – 将 `Image.load` 替换为 `Image.from_bytes`，以处理来自 API 或数据库的图像数据。

所有这些都基于 **extract text from image** 与 **convert scanned image text** 的核心思路，将扫描的文档转化为机器可读的内容。

## 结论

我们完整演示了一个清晰的 **basic OCR example**，展示了 **how to ocr python**、**read tiff file python** 以及 **extract text from image** 的完整流程，仅需几行代码。该脚本自包含、带有错误处理，并直接打印结果，是任何需要将扫描文档转换为可编辑文本的项目的坚实基础。

欢迎随意实验——更换 OCR 后端、调整预处理步骤，或将输出接入下游工作流。只要能够可靠地 **convert scanned image text** 为可搜索的数据，想象空间就无限。

有关于边缘案例、语言包或性能调优的问题吗？在下方留言吧，祝编码愉快！

![如何使用 OCR Python 示例](/images/ocr-python-example.png "how to ocr python 脚本输出的截图")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}