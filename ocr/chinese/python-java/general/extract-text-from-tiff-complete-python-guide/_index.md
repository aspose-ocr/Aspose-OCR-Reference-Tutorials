---
category: general
date: 2026-06-16
description: 使用 Python OCR 从 TIFF 文件中提取文本。学习如何一步步将 TIFF 转换为文本，轻松处理多页文档。
draft: false
keywords:
- extract text from tiff
- convert tiff to text
- Python OCR multi‑page TIFF
- OCR language settings
- OCR engine Python
language: zh
og_description: 使用 Python OCR 从 TIFF 文件中提取文本。按照本指南将 TIFF 转换为文本，处理多页扫描，并获得干净的结果。
og_title: 从 TIFF 中提取文本 – 完整的 Python 指南
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Extract text from TIFF files using Python OCR. Learn how to convert
    TIFF to text step‑by‑step, handling multi‑page documents with ease.
  headline: Extract Text from TIFF – Complete Python Guide
  type: TechArticle
- description: Extract text from TIFF files using Python OCR. Learn how to convert
    TIFF to text step‑by‑step, handling multi‑page documents with ease.
  name: Extract Text from TIFF – Complete Python Guide
  steps:
  - name: '**Batch conversion** – Wrap the whole flow in a function `def ocr_tiff(path):`
      and iterate over a directory of TIFF files.'
    text: '**Batch conversion** – Wrap the whole flow in a function `def ocr_tiff(path):`
      and iterate over a directory of TIFF files.'
  - name: '**Output to files** – Instead of printing, write each page’s text to `page_{i}.txt`
      or concatenate everything into a single document.'
    text: '**Output to files** – Instead of printing, write each page’s text to `page_{i}.txt`
      or concatenate everything into a single document.'
  - name: '**Alternative OCR engines** – If you need higher accuracy, swap `ocr.OcrEngine()`
      for Tesseract (`pytesseract`) or Azure Cognitive Services—just keep the same
      “extract text from TIFF” logic.'
    text: '**Alternative OCR engines** – If you need higher accuracy, swap `ocr.OcrEngine()`
      for Tesseract (`pytesseract`) or Azure Cognitive Services—just keep the same
      “extract text from TIFF” logic.'
  - name: '**Post‑processing** – Run spell‑check, language detection, or regex cleanup
      to tidy up the raw OCR output.'
    text: '**Post‑processing** – Run spell‑check, language detection, or regex cleanup
      to tidy up the raw OCR output.'
  type: HowTo
tags:
- OCR
- Python
- TIFF
- Text extraction
title: 从 TIFF 中提取文本 – 完整的 Python 指南
url: /zh/python-java/general/extract-text-from-tiff-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从 TIFF 中提取文本 – 完整 Python 指南

是否曾需要 **从 TIFF 中提取文本**，却不知从何入手？你并不孤单——许多开发者在处理扫描档案或旧版文档时都会遇到这个难题。好消息是，只需几行 Python 代码，你就可以 **将 TIFF 转换为文本**，即使文件包含数十页也不在话下。

在本教程中，我们将通过一个真实案例演示：加载多页 TIFF、将 OCR 语言设置为法语，并从每页中提取识别后的文本。完成后，你将拥有一段可直接运行的脚本，了解每一步的意义，并知道如何将其迁移到其他语言或图像格式。

## 前置条件

在开始之前，请确保你具备以下条件：

- 已安装 Python 3.8 或更高版本。
- 已安装 `ocr` 包（或任何提供 `OcrEngine` 类的兼容 OCR 库）。可以使用 `pip install ocr-lib` 安装——请替换为你实际使用的包名。
- 一个多页 TIFF 文件（例如 `french-scans.tif`），是你想要处理的目标。
- 对 Python 脚本有基本了解。

无需繁重的依赖，也不需要外部服务——仅需纯 Python 与 OCR 引擎。

---

## 步骤 1：设置 OCR 引擎以 **从 TIFF 中提取文本**

首先，我们需要创建一个 OCR 引擎实例，并告知它使用哪种语言。这里的源材料是法语，所以我们相应地设置语言。

```python
import ocr  # Replace with the actual import if your OCR library uses a different name

# Create the OCR engine
engine = ocr.OcrEngine()

# Tell the engine to look for French characters
engine.language = ocr.Language.FRENCH
```

**为什么这很重要：**  
语言设置能显著提升识别准确度。如果引擎默认使用英语，法语字符如 “é” 或 “ç” 会被误读为通用符号。显式选择法语即可为引擎提供正确的字符映射。

> **小技巧：** 如果你需要处理多语言文档，可以在每次调用 `recognize()` 之前动态修改 `engine.language`。

---

## 步骤 2：加载要 **将 TIFF 转换为文本** 的多页 TIFF

TIFF 可以包含多个帧——把每个帧视作单独的一页。OCR 库为我们抽象了这一点，只需指向文件即可。

```python
# Path to your multi‑page TIFF
tiff_path = "YOUR_DIRECTORY/french-scans.tif"

# Load the file; the engine now knows how many pages it contains
engine.load_from_file(tiff_path)
```

**边缘情况提示：**  
如果文件路径错误或 TIFF 已损坏，`load_from_file` 方法会抛出异常。生产代码中请使用 `try/except` 包裹：

```python
try:
    engine.load_from_file(tiff_path)
except Exception as e:
    print(f"Failed to load TIFF: {e}")
    raise
```

---

## 步骤 3：对整个文档运行 OCR – **从 TIFF 中提取文本** 的核心

现在让引擎发挥魔力。`recognize()` 调用一次性处理所有页面，并返回一个丰富的结果对象。

```python
# Perform OCR on all pages at once
multi_result = engine.recognize()
```

**底层发生了什么？**  
引擎会遍历每个帧，执行预处理（去倾斜、二值化），运行神经网络，并汇总输出。因为我们只调用一次 `recognize()`，库能够在页面之间共享资源，速度比手动循环更快。

---

## 步骤 4：从 JSON 结果中提取识别文本 – **将 TIFF 转换为文本**（逐页）

结果对象可以序列化为 JSON。在该 JSON 中，你会找到一个 `pages` 数组，每个元素都有一个 `text` 字段。

```python
# Convert the result to a Python dict (JSON-like)
result_dict = multi_result.to_json()

# Extract the list of pages
pages = result_dict["pages"]
```

现在我们得到一个干净的 Python 列表，列表的每个元素对应一页的 OCR 输出。

---

## 步骤 5：打印或保存每页文本 – **从 TIFF 中提取文本** 的最后一步

让我们遍历页面并显示提取的文本。如果愿意，也可以将每页写入单独的 `.txt` 文件。

```python
for i, page in enumerate(pages, start=1):
    print(f"--- Page {i} ---")
    print(page["text"])
    print()  # Blank line for readability
```

### 预期输出（示例）

```
--- Page 1 ---
Bonjour, ceci est un exemple de texte extrait d'une image TIFF.

--- Page 2 ---
Le deuxième page contient davantage d'informations en français.
```

如果 OCR 成功，你会看到每页的法语句子整齐呈现。若出现乱码，请再次检查语言设置，或考虑在 OCR 前提升图像分辨率。

---

## 处理常见问题时的 **将 TIFF 转换为文本** 方法

| 问题 | 产生原因 | 快速解决方案 |
|------|----------|--------------|
| **`pages` 数组为空** | TIFF 未正确加载或没有帧。 | 核实文件路径，并确保 TIFF 不是伪装成 TIFF 的单页 PNG。 |
| **乱码字符** | 语言不匹配或图像质量低。 | 设置正确的 `engine.language`，并对图像进行预处理（如提升 DPI）。 |
| **大尺寸 TIFF 导致内存暴涨** | 一次性加载所有页面会占用大量 RAM。 | 分块处理：加载单帧、识别、丢弃后再加载下一帧。 |
| **打印时出现 Unicode 错误** | 控制台编码不支持带重音的字符。 | 使用 `print(page["text"].encode('utf-8').decode('utf-8'))` 或将终端配置为 UTF‑8。 |

---

## 扩展脚本：从 **从 TIFF 中提取文本** 到批量处理

有了坚实的基础后，你可以考虑以下进阶步骤：

1. **批量转换** – 将整个流程封装为函数 `def ocr_tiff(path):`，并遍历目录中的 TIFF 文件。
2. **输出到文件** – 与其打印，不如将每页文本写入 `page_{i}.txt`，或将所有页面合并为单个文档。
3. **替换 OCR 引擎** – 若需更高准确率，可将 `ocr.OcrEngine()` 替换为 Tesseract (`pytesseract`) 或 Azure Cognitive Services——保持相同的 “从 TIFF 中提取文本” 逻辑即可。
4. **后处理** – 运行拼写检查、语言检测或正则清理，以整理原始 OCR 输出。

---

## 完整、可直接运行的脚本

下面是完整代码，复制粘贴即可使用。它包含基本的错误处理，并可选地将每页文本保存为单独文件。

```python
import ocr  # Adjust import based on your OCR library
import os

def extract_text_from_tiff(tiff_path: str, output_dir: str = None) -> list:
    """
    Loads a multi‑page TIFF, runs OCR, and returns a list of strings,
    one per page. Optionally saves each page to a .txt file.
    """
    # Initialize engine and set language
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.FRENCH

    # Load the TIFF file
    try:
        engine.load_from_file(tiff_path)
    except Exception as e:
        raise RuntimeError(f"Unable to load {tiff_path}: {e}")

    # Run OCR on all pages
    multi_result = engine.recognize()

    # Parse JSON result
    pages = multi_result.to_json()["pages"]
    texts = [page["text"] for page in pages]

    # If an output directory is provided, write each page to a file
    if output_dir:
        os.makedirs(output_dir, exist_ok=True)
        for i, text in enumerate(texts, start=1):
            file_path = os.path.join(output_dir, f"page_{i}.txt")
            with open(file_path, "w", encoding="utf-8") as f:
                f.write(text)

    return texts

if __name__ == "__main__":
    # Example usage – replace with your actual TIFF path
    tiff_file = "YOUR_DIRECTORY/french-scans.tif"
    # Optional: where to store per‑page text files
    out_folder = "extracted_pages"

    page_texts = extract_text_from_tiff(tiff_file, out_folder)

    for i, txt in enumerate(page_texts, start=1):
        print(f"--- Page {i} ---")
        print(txt)
        print()
```

运行此脚本，将 `tiff_file` 指向你的文档，控制台会填满整洁的法语句子。如果提供了 `out_folder`，你还会在该文件夹中看到一系列 `page_#.txt` 文件，供后续处理使用。

---

## 结论

我们刚刚使用简洁的 Python OCR 工作流 **从 TIFF 中提取文本**，并掌握了可靠的 **将 TIFF 转换为文本** 方法。从使用正确语言初始化引擎，到遍历每页的 JSON 结果，每一步都解释了背后的 “为什么”，便于你将该模式迁移到其他语言、图像格式或更大规模的批处理任务。

接下来可以尝试将 OCR 后端换成 Tesseract，实验不同的语言包，或将输出集成到可搜索的数据库中。只要能可靠地将扫描图像转为可检索文本，可能性无限。

如果在使用过程中遇到问题或有进一步的改进想法，欢迎留言交流。祝编码愉快！

## 接下来你应该学习什么？

以下教程与本指南紧密相关，帮助你在已有技巧的基础上进一步深化。每篇资源都提供完整可运行的代码示例，并配有逐步解释，帮助你掌握更多 API 功能并探索替代实现方式。

- [使用 Aspose OCR 从图像提取文本 – 步骤指南](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [使用文件夹进行 OCR 操作提取图像文本](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [将图像转换为文本 – 从 URL 执行 OCR](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}