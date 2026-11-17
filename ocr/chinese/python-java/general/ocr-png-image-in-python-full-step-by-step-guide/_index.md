---
category: general
date: 2026-06-06
description: 使用 Python 对 PNG 图像进行 OCR —— 学习如何从图像中提取文本，运行 Python OCR 示例，甚至轻松读取古希腊文本。
draft: false
keywords:
- ocr png image
- extract text from image
- python ocr example
- read ancient greek
- recognize image text
language: zh
og_description: 在Python中解释OCR PNG图像。本指南展示了如何从图像中提取文本，运行Python OCR示例，并轻松阅读古希腊语。
og_title: Python 中的 PNG 图像 OCR – 完整教程
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: OCR PNG image with Python – learn how to extract text from image, run
    a python OCR example and even read ancient greek text easily.
  headline: OCR PNG Image in Python – Full Step‑by‑Step Guide
  type: TechArticle
- description: OCR PNG image with Python – learn how to extract text from image, run
    a python OCR example and even read ancient greek text easily.
  name: OCR PNG Image in Python – Full Step‑by‑Step Guide
  steps:
  - name: Prerequisites
    text: '| Requirement | Why it matters | |-------------|----------------| | Python
      3.8+ | Modern syntax and type hints | | `pytesseract` package | Thin wrapper
      around the Tesseract engine | | Tesseract OCR binaries (≥ 5.0) | The actual
      engine that does the heavy lifting | | Greek language data (`grc.trained'
  - name: How do I improve accuracy on a noisy PNG?
    text: '- Convert the image to grayscale: `img = img.convert(''L'')` - Apply a
      binary threshold: `img = img.point(lambda x: 0 if x < 128 else 255, ''1'')`
      - Upscale with `img = img.resize((img.width*2, img.height*2), Image.LANCZOS)`'
  - name: Can I process a whole folder of PNGs?
    text: Absolutely. Wrap the `recognize_image` call in a `for` loop over `Path.glob("*.png")`.
      Store each result in a dictionary or write to a CSV for later analysis.
  - name: What if I need to extract numbers only?
    text: 'Pass a custom **config** string to `image_to_string`:'
  - name: Is there a way to get confidence scores?
    text: Yes—use `pytesseract.image_to_data` which returns a TSV with confidence
      per word. You can filter out low‑confidence tokens before assembling the final
      string.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Python 中的 PNG 图像 OCR – 完整逐步指南
url: /zh/python-java/general/ocr-png-image-in-python-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Python 中 OCR PNG 图像 – 完整分步指南

有没有想过如何直接在 Python 脚本中 **OCR PNG image** 文件？也许你有一整文件夹的扫描古籍手稿，需要 **extract text from image** 文件而不必手动逐字输入。好消息是，你不需要计算机视觉博士学位——只需几行代码和合适的库，就能在几秒钟内读取古希腊文。

在本教程中，我们将演示一个 **python OCR example**，它能够识别 PNG 中的文字，将语言设置为希腊文多音调（Greek polytonic），并打印结果。完成后，你将掌握如何 **recognize image text**、处理常见坑点，并能够将脚本扩展到其他语言或图像格式。

## 你将学到

- 安装并配置 Python OCR 库（pytesseract + Tesseract OCR）
- 创建 OCR 引擎实例并加载 PNG 文件
- 将识别语言设置为希腊文多音调，以便 **read ancient greek**
- 输出识别后的文本并排查常见问题
- 将脚本扩展为批量处理多个 PNG，或切换到其他语言

### 前置条件

| 要求 | 为什么重要 |
|------|------------|
| Python 3.8+ | 支持现代语法和类型提示 |
| `pytesseract` 包 | Tesseract 引擎的轻量包装器 |
| Tesseract OCR 二进制文件（≥ 5.0） | 实际执行 OCR 任务的核心引擎 |
| 希腊语语言数据（`grc.traineddata`） | 正确 **read ancient greek** 所必需 |
| 需要分析的 PNG 图像（例如 `ancient_greek.png`） | 本教程 **ocr png image** 示例的目标文件 |

你可以使用以下命令安装 Python 端：

```bash
pip install pytesseract Pillow
```

在 Ubuntu/macOS 上则需要安装引擎本身：

```bash
# Ubuntu
sudo apt-get install tesseract-ocr libtesseract-dev

# macOS (Homebrew)
brew install tesseract
```

别忘了下载希腊文多音调训练数据：

```bash
wget https://github.com/tesseract-ocr/tessdata/blob/main/greek.traineddata -P /usr/share/tesseract-ocr/4.00/tessdata/
```

*（路径可能不同；如有需要请调整 `TESSDATA_PREFIX`。）*

---

## OCR PNG Image：创建引擎实例

我们首先需要一个与 Tesseract 通信的对象。在 `pytesseract` 中，引擎通过模块级函数访问，但为了清晰起见，我们将其封装在一个小类中。这与原始代码片段中的 “engine” 概念相呼应。

```python
from pathlib import Path
from PIL import Image
import pytesseract

class OcrEngine:
    """
    Simple wrapper around pytesseract to keep the API similar to the original example.
    """
    def __init__(self, tess_cmd: str = "tesseract"):
        # You can point pytesseract to a custom binary if you installed it somewhere unusual.
        pytesseract.pytesseract.tesseract_cmd = tess_cmd

    def set_recognition_language(self, language: str):
        """
        Store the language code for later calls.
        Example: 'grc' for Greek polytonic.
        """
        self.lang = language

    def recognize_image(self, image_path: str):
        """
        Open the PNG, run OCR, and return the raw result object.
        """
        img = Image.open(image_path)
        # pytesseract returns a string; we wrap it for consistency with the original code.
        text = pytesseract.image_to_string(img, lang=self.lang)
        return OcrResult(text=text)

class OcrResult:
    """Container for OCR output – mimics the .text attribute used in the example."""
    def __init__(self, text: str):
        self.text = text
```

**为什么要封装？**  
- 保持公共 API 与你最初的代码片段一致，迁移无痛。  
- 以后可以在不改动主流程的情况下加入日志或错误处理。  
- 展示良好的面向对象实践——高级开发者会欣赏。

---

## 从图像中提取文本：设置语言为希腊文多音调

有了引擎后，需要告诉它期待的语言。希腊文多音调使用的变音符号不在标准 “greek” 数据中，因此我们将 Tesseract 指向 `grc` 训练文件。

```python
# Step 2: Set the recognition language to Greek polytonic
engine = OcrEngine()
engine.set_recognition_language("grc")   # 'grc' is the ISO‑639‑2 code for ancient Greek
```

如果你想在其他语言的 **extract text from image** 文件中使用，只需将 `"grc"` 替换为 `"eng"`（英语）、`"fra"`（法语）等。只要已安装对应语言包，这行代码即可通用。

---

## 识别图像文字：对 PNG 运行 OCR

语言设定好后，我们将 PNG 传入引擎。原示例使用硬编码路径，这里改用 `Path` 对象，使代码更灵活。

```python
# Step 3: Recognize text from the image file
image_path = Path("YOUR_DIRECTORY/ancient_greek.png")
ocr_result = engine.recognize_image(str(image_path))
```

**技巧与边缘情况**

- **文件未找到** – 用 `try/except FileNotFoundError` 包裹调用，给出友好提示。  
- **低分辨率 PNG** – 在 OCR 前使用 Pillow 进行预处理（如缩放、二值化）。  
- **非希腊文文本** – Tesseract 仍会尝试解码，但准确率会大幅下降。请务必匹配语言。

---

## 输出识别后的文本

最后，打印结果。在实际项目中，你可能会将结果写入数据库、CSV，或进一步送入翻译流水线。

```python
# Step 4: Output the recognized text
print("=== OCR Result ===")
print(ocr_result.text)
```

当你对一张清晰的古希腊铭文扫描图运行脚本时，应该会看到类似下面的输出：

```
=== OCR Result ===
Ἀνδρὸς ἐστὶν ὁ ἥλιος...
```

如果输出乱码，请再次确认 **greek.traineddata** 文件位于正确目录，并且 PNG 没有过度噪声。

---

## 完整可运行示例（一步到位的脚本）

下面是完整的、可直接运行的程序。保存为 `ocr_greek.py` 并执行 `python ocr_greek.py`。

```python
# ocr_greek.py
from pathlib import Path
from PIL import Image
import pytesseract

class OcrEngine:
    def __init__(self, tess_cmd: str = "tesseract"):
        pytesseract.pytesseract.tesseract_cmd = tess_cmd
        self.lang = "eng"  # default fallback

    def set_recognition_language(self, language: str):
        self.lang = language

    def recognize_image(self, image_path: str):
        img = Image.open(image_path)
        text = pytesseract.image_to_string(img, lang=self.lang)
        return OcrResult(text)

class OcrResult:
    def __init__(self, text: str):
        self.text = text

def main():
    # 1️⃣ Create an OCR engine instance
    engine = OcrEngine()

    # 2️⃣ Set the language to Greek polytonic (read ancient greek)
    engine.set_recognition_language("grc")

    # 3️⃣ Path to the PNG you want to analyse
    png_path = Path("YOUR_DIRECTORY/ancient_greek.png")
    if not png_path.is_file():
        raise FileNotFoundError(f"Cannot find image at {png_path}")

    # 4️⃣ Recognize and retrieve the text
    result = engine.recognize_image(str(png_path))

    # 5️⃣ Print the extracted text
    print("=== OCR PNG Image Result ===")
    print(result.text)

if __name__ == "__main__":
    main()
```

**预期输出**（为简洁起见已截断）：

```
=== OCR PNG Image Result ===
Ἀνδρὸς ἐστὶν ὁ ἥλιος·
Καὶ ὁ ἥλιος ἀνατέλλει·
```

如果看到正确的希腊字符，恭喜你——已经成功在 Python 中完成一次 **ocr png image** 操作！

---

## 常见问题与专业技巧

### 如何提升噪声 PNG 的识别准确率？

- 将图像转为灰度：`img = img.convert('L')`  
- 应用二值阈值：`img = img.point(lambda x: 0 if x < 128 else 255, '1')`  
- 使用 `img = img.resize((img.width*2, img.height*2), Image.LANCZOS)` 放大

这些步骤常能把 **recognize image text** 的噩梦转变为干净的结果。

### 能否一次处理整个 PNG 文件夹？

完全可以。把 `recognize_image` 调用放进 `for` 循环，遍历 `Path.glob("*.png")`。将每个结果存入字典或写入 CSV，便于后续分析。

```python
for png in Path("my_folder").glob("*.png"):
    res = engine.recognize_image(str(png))
    print(f"{png.name}: {res.text[:50]}...")
```

### 如果只想提取数字怎么办？

向 `image_to_string` 传入自定义 **config** 字符串：

```python
digits = pytesseract.image_to_string(img, lang=self.lang, config='outputbase digits')
```

这样就能 **extract text from image** 包含表格、序列号或时间戳的文件，仅保留数字部分。

### 如何获取置信度分数？

使用 `pytesseract.image_to_data`，它会返回包含每个单词置信度的 TSV。你可以在组装最终字符串前过滤低置信度的词。

---

## 扩展本教程

掌握基础后，你可以进一步探索以下相关主题：

- **使用多进程进行批量 OCR** – 加速大规模 PNG 语料库。  
- **OCR + NLP 混合流水线** – 自动将提取的古希腊文翻译为现代英语。  
- **替代引擎** – 尝试 `easyocr` 或基于 `opencv` 的方法，针对特定场景。  
- **云端 OCR 服务** – Google Vision、Azure Computer Vision 或 AWS Textract，实现无服务器扩展。

这些内容都建立在我们刚刚讲解的 **python ocr example** 基础上，帮助你更深入地探索。

---

## 结论

我们把一个简单的代码片段升级为在 Python 中完整、稳健的 **ocr png image** 工作流。通过创建 `OcrEngine`、设置希腊文多音调、读取 PNG 并打印结果，你现在已经掌握了 **extract text from image**、**recognize image text**，甚至可以 **read ancient greek**。

## 接下来该学习什么？

以下教程与本指南紧密相关，帮助你进一步深化所学技术。每篇资源都提供完整可运行的代码示例和逐步解释，助你在项目中灵活运用 API 并探索替代实现方案。

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)
- [recognize text image with Aspose OCR for multiple languages](/ocr/english/net/ocr-settings/working-with-different-languages/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}