---
category: general
date: 2026-03-26
description: 如何在 OCR 引擎中设置语言并从图像中提取手写文本——一步一步的教程，将图像转换为文本。
draft: false
keywords:
- how to set language
- extract handwritten text
- convert image to text
- how to extract handwritten
- recognize handwritten notes
language: zh
og_description: 如何在 OCR 引擎中设置语言并从图像中提取手写笔记。学习在几分钟内将图像转换为文本。
og_title: 如何设置 OCR 语言 – 轻松提取手写文本
tags:
- OCR
- Python
- Image Processing
title: 如何为 OCR 设置语言并提取手写文本——完整指南
url: /zh/python/general/how-to-set-language-for-ocr-and-extract-handwritten-text-com/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何为 OCR 设置语言并提取手写文本 – 完整指南

是否曾想过 **如何设置语言** 让你的 OCR 引擎真正理解你需要的字符？也许你有一张杂货清单的照片、会议记录，或是一张草图模糊的图表，却始终无法提取文字。好消息是？你不需要计算机视觉博士学位——只需几行 Python 代码和正确的标志。

在本教程中，我们将逐步演示如何 **提取手写文本**（handwritten text）从 PNG，如何将图像转换为纯文本，并解释每个设置背后的 “为什么”。完成后，你将能够在任何项目中识别手写笔记，无论是记事应用还是批处理流水线。

> **你需要的环境**  
> • Python 3.8+（代码在 3.10 上同样可用）  
> • `ocr` 库（或任何提供 `OcrEngine` 的兼容包装器）  
> • 一张示例图片，例如 `note_handwritten.png` —— 任意包含扩展拉丁字符的图像均可。

让我们开始吧。

---

## 如何设置语言并启用手写识别

首先，你必须告诉 OCR 引擎它应该期待哪套字母表。如果跳过此步骤，引擎会默认使用一套通用字符集，常常误识带重音的字母或特殊符号。

```python
import ocr  # Assuming the library is named `ocr`

# Step 1: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()

# Step 2: Choose the language that includes extended Latin characters
ocr_engine.language = ocr.Language.ExtendedLatin

# Step 3: Turn on the handwritten‑text flag
ocr_engine.recognize_handwritten = True
```

**为什么这很重要：**  
- **ExtendedLatin** 包含 “ñ”、 “ø”、 “ç” 等字符，这些在许多欧洲笔记中很常见。  
- `recognize_handwritten` 标志会将底层模型从印刷体 OCR 切换为经过手写笔画训练的神经网络。若不启用，它会把你的涂鸦当作噪声。

> **专业提示：** 如果你要处理多语言文档，建议为每种语言实例化一个独立的引擎，或在每次调用前动态切换 `ocr_engine.language`。这样可以避免加载不需要的字符集所带来的开销。

![OCR 引擎配置截图，展示如何设置语言](/images/ocr-set-language.png "在 OCR 引擎上设置语言")

*图片替代文字：“在 OCR 引擎配置屏幕上设置语言”。*

---

## 从 PNG 图像中提取手写文本

现在引擎已经知道要寻找什么了，接下来把图像喂进去吧。`recognize_image` 方法返回一个丰富的结果对象，`text` 属性即为你关心的纯字符串。

```python
# Step 4: Perform OCR on the input image
handwritten_result = ocr_engine.recognize_image("YOUR_DIRECTORY/note_handwritten.png")

# Step 5: Print the extracted text
print(handwritten_result.text)
```

运行脚本时，你应该会看到类似如下的输出：

```
Buy milk
Call Dr. García at 5 pm
Pick up résumé
```

该输出证明你已经成功 **将图像转换为文本**，并且引擎遵循了你提供的语言设置。

**常见坑点**  
- **路径错误** – 再次确认文件位置；缺失文件会抛出 `FileNotFoundError`。  
- **低分辨率图像** – 手写 OCR 在低于 300 dpi 时表现不佳。若输出乱码，请放大或重新扫描。  
- **颜色反转** – 若背景为深色而墨水为浅色，请先反转颜色（`Pillow` 可帮助实现）。

---

## 使用辅助函数将图像转换为文本

如果你计划对数十个文件执行 OCR，建议将逻辑封装成可复用函数。这也让代码更易于测试并集成到其他流水线中。

```python
def extract_handwritten_text(image_path: str) -> str:
    """
    Loads an image, sets the OCR engine to ExtendedLatin,
    enables handwritten recognition, and returns the plain text.
    """
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ExtendedLatin
    engine.recognize_handwritten = True

    result = engine.recognize_image(image_path)
    return result.text.strip()   # Remove leading/trailing whitespace


# Example usage
if __name__ == "__main__":
    txt = extract_handwritten_text("YOUR_DIRECTORY/note_handwritten.png")
    print("📝 Handwritten notes:\n", txt)
```

该辅助函数将 **如何提取手写文本** 的逻辑隔离出来，之后你可以在 Flask 接口、CLI 工具或批处理任务中调用，而无需每次都重新配置。

---

## 在真实场景中识别手写笔记

下面列出了一些你可能需要 **识别手写笔记** 的情形，以及该设置的适配方式：

| 场景 | 语言为何重要 | 建议的调整 |
|----------|---------------------|-----------------|
| **多语言杂货清单** | 条目可能包含重音字符（例如 “crème”） | 根据清单切换 `ocr_engine.language`，或在支持时使用 `ocr.Language.AutoDetect` |
| **课堂白板照片** | 粉笔可能产生淡淡的笔画 | 在送入引擎前提升图像对比度 |
| **医疗处方** | 手写字极其潦草 | 将 OCR 与药品名称的拼写纠正词典配合使用 |

在每种情况下，核心步骤——**如何设置语言**、启用手写模式以及调用 `recognize_image`——保持不变。这种一致性使得方法既稳健又易于维护。

---

## 边缘情况与高级调优

1. **批量处理** – 只加载一次引擎，遍历文件时仅在需要时更改 `language` 属性，可显著降低初始化开销。  
2. **非拉丁脚本** – 若需处理西里尔文或阿拉伯文，请将 `ExtendedLatin` 替换为相应的枚举（例如 `ocr.Language.Cyrillic`），同样的模式适用。  
3. **部分识别** – 有时引擎会对极短的笔画返回空字符串。快速的健全性检查 (`if not result.text.strip(): …`) 可让你回退到次要模型或提示用户重新扫描。  
4. **性能分析** – 对大数据集时，计时 `recognize_image` 调用。如果成为瓶颈，可考虑使用 `concurrent.futures.ThreadPoolExecutor` 并行化处理。

---

## 完整工作示例

下面是完整脚本，你可以复制粘贴到名为 `handwritten_ocr.py` 的文件中。脚本包含参数解析，便于在命令行指定任意图像。

```python
#!/usr/bin/env python3
"""
handwritten_ocr.py – Convert an image containing handwritten notes
to plain text using the OCR library.

Usage:
    python handwritten_ocr.py path/to/image.png
"""

import sys
import argparse
import ocr  # Replace with the actual import if the library name differs


def extract_handwritten_text(image_path: str) -> str:
    """Extracts handwritten text from the given image."""
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ExtendedLatin
    engine.recognize_handwritten = True

    result = engine.recognize_image(image_path)
    return result.text.strip()


def main():
    parser = argparse.ArgumentParser(
        description="Convert handwritten image to text (how to set language, extract handwritten text)."
    )
    parser.add_argument("image", help="Path to the PNG/JPG image containing handwritten notes")
    args = parser.parse_args()

    try:
        text = extract_handwritten_text(args.image)
        if text:
            print("✅ Extracted text:\n", text)
        else:
            print("⚠️ No text detected – try a higher‑resolution image.")
    except Exception as e:
        print(f"❌ Error processing {args.image}: {e}", file=sys.stderr)
        sys.exit(1)


if __name__ == "__main__":
    main()
```

运行方式如下：

```bash
python handwritten_ocr.py YOUR_DIRECTORY/note_handwritten.png
```

你应当看到与前面代码片段相同的输出，确认已经成功 **将图像转换为文本** 并 **识别手写笔记**。

---

## 结论

我们已经介绍了 **如何在 OCR 引擎上设置语言**、开启手写文本标志，并构建了一个可复用的函数来 **提取手写文本**。按照上述步骤，你可以可靠地 **将图像转换为文本**，无论是处理单个笔记还是海量扫描文档。

接下来，尝试使用不同的语言包、批量处理文件夹，或将此逻辑集成到返回 JSON 结果的 Web 服务中。基本原理保持不变，而 `ocr` 库的灵活性让你几乎可以适配任何使用场景。

对边缘情况、性能或扩展到其他语言有疑问？在 GitHub 上留言或私信我——祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}