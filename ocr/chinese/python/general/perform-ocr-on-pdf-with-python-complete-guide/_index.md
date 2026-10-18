---
category: general
date: 2026-06-25
description: 使用 Python 对 PDF 执行 OCR——学习如何加载 PDF 进行 OCR、从 PDF 页面提取文本，并高效预览识别的文本。
draft: false
keywords:
- perform OCR on PDF
- extract text from PDF pages
- load PDF for OCR
- how to OCR large PDF
- preview recognized text
language: zh
og_description: 在 Python 中对 PDF 执行 OCR。本指南展示了如何加载 PDF 进行 OCR、从 PDF 页面提取文本，以及快速预览识别的文本。
og_title: 使用 Python 对 PDF 进行 OCR – 步骤教程
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Perform OCR on PDF using Python—learn how to load PDF for OCR, extract
    text from PDF pages, and preview recognized text efficiently.
  headline: Perform OCR on PDF with Python – Complete Guide
  type: TechArticle
- description: Perform OCR on PDF using Python—learn how to load PDF for OCR, extract
    text from PDF pages, and preview recognized text efficiently.
  name: Perform OCR on PDF with Python – Complete Guide
  steps:
  - name: '**Parallelize per page** – Use `concurrent.futures.ThreadPoolExecutor`
      if the OCR engine is thread‑safe.'
    text: '**Parallelize per page** – Use `concurrent.futures.ThreadPoolExecutor`
      if the OCR engine is thread‑safe.'
  - name: '**Cache intermediate images** – Some engines let you store rasterized pages
      on SSD, dramatically cutting CPU load on re‑runs.'
    text: '**Cache intermediate images** – Some engines let you store rasterized pages
      on SSD, dramatically cutting CPU load on re‑runs.'
  - name: '**Batch write output** – Instead of appending to a Python list, open the
      output file once and write each page’s text as soon as it’s ready.'
    text: '**Batch write output** – Instead of appending to a Python list, open the
      output file once and write each page’s text as soon as it’s ready.'
  - name: '**Adjust DPI** – Lowering the DPI during rasterization reduces memory but
      may affect accuracy; find a sweet spot (usually 200‑300 DPI).'
    text: '**Adjust DPI** – Lowering the DPI during rasterization reduces memory but
      may affect accuracy; find a sweet spot (usually 200‑300 DPI).'
  type: HowTo
tags:
- OCR
- Python
- PDF processing
title: 使用Python对PDF进行OCR – 完整指南
url: /zh/python/general/perform-ocr-on-pdf-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Python 对 PDF 执行 OCR – 完整指南

是否曾需要 **对 PDF 执行 OCR**，却不知从何入手？也许你手头有一堆扫描的合同，或是一本体积庞大的手册，拒绝配合你平常的文本提取工具。简而言之，你想 **加载 PDF 进行 OCR**，提取文本，并快速预览——且不让机器内存爆炸。

好消息，你来对地方了。在本教程中，我们将逐步演示一个完整可用的 Python 脚本，**从 PDF 页面提取文本**，展示如何 **预览识别后的文本**，并解决 **如何高效 OCR 大型 PDF** 的经典难题。

阅读完本教程后，你将拥有一个可直接运行的程序，清晰了解每个配置项的作用，并掌握一系列避免新手常踩坑的技巧。

---

## 你将学到

- 如何使用 `aocr` 库 **加载 PDF 进行 OCR**。
- 对 PDF 页面 **逐页执行 OCR** 的完整步骤。
- 在控制内存使用的前提下 **从 PDF 页面提取文本** 的方法。
- 如何 **预览识别文本** 以检查结果的合理性。
- 处理 **大型 PDF** 而不耗尽 RAM 的策略。

> **技巧：** 本指南假设你已安装 Python 3.9+，并对虚拟环境有基本了解。如果你是 Python 新手，请先创建一个 virtualenv——相信我，这会为后续省去很多麻烦。

---

## 前置条件

| 要求 | 为什么重要 |
|------|------------|
| `aocr` Python 包（或任何兼容的 OCR 引擎） | 提供脚本中使用的 `OcrEngine` 类。 |
| `pip` 与虚拟环境 | 将依赖与系统 Python 隔离。 |
| 足够的磁盘空间用于临时图像提取 | 某些 OCR 引擎会在处理前将页面图像写入磁盘。 |
| 可选：`tqdm` 用于进度条 | 在处理 **如何 OCR 大型 PDF** 任务时提升用户体验。 |

使用以下命令安装必备依赖：

```bash
python -m venv ocr-env
source ocr-env/bin/activate   # Windows: ocr-env\Scripts\activate
pip install aocr tqdm
```

如果你的 PDF 设置了密码，稍后需要提供密码——请参阅 “边缘情况” 小节。

---

## 第一步：执行 OCR on PDF – 初始化 OCR 引擎

首先，需要创建一个 OCR 引擎实例。可以把它想象成读取每页图像并输出纯文本的大脑。

```python
import aocr                     # The OCR library
from tqdm import tqdm           # Optional, for a nice progress bar

def create_engine():
    """
    Initialise the OcrEngine with sensible defaults.
    Returns the configured engine ready for processing.
    """
    engine = aocr.OcrEngine()
    # Limit memory usage – crucial when tackling how to OCR large PDF files
    engine.max_memory_mb = 200               # 200 MB cap, adjust if needed
    # Choose a recognition mode that matches your source material
    engine.recognition_mode = aocr.RecognitionMode.PRINTED
    return engine
```

> **为什么要设置 `max_memory_mb`？**  
> OCR 引擎通常会在 RAM 中缓存页面图像。通过限制内存上限，可防止在处理 500 页合同时脚本崩溃。

---

## 第二步：加载 PDF for OCR 并配置设置

现在我们真正 **加载 PDF for OCR**。路径可以是绝对路径也可以是相对路径，只要确保文件真实存在即可。

```python
def load_pdf(engine, pdf_path):
    """
    Loads the PDF into the OCR engine.
    Raises FileNotFoundError if the file does not exist.
    """
    try:
        engine.load_pdf(pdf_path)
        print(f"✅ Loaded '{pdf_path}' – {engine.page_count} pages ready.")
    except Exception as e:
        raise RuntimeError(f"Failed to load PDF: {e}")
```

如果 PDF 被加密，`engine.load_pdf` 通常会抛出异常。此时可以调用 `engine.load_pdf(pdf_path, password="secret")`——后文会详细说明。

---

## 第三步：从 PDF 页面提取文本 – 核心循环

下面是 **对 PDF 页面逐页执行 OCR** 的核心代码。我们还会 **预览识别文本** 的前几百字符，以便你验证一切正常。

```python
def ocr_pages(engine, preview_len=200):
    """
    Iterates over each page, runs OCR, and yields the recognized text.
    Also prints a short preview for each page.
    """
    for page_index in tqdm(range(engine.page_count), desc="Processing pages"):
        # Select the current page – essential for multi‑page PDFs
        engine.select_page(page_index)

        # Perform the actual OCR
        page_text = engine.recognize()

        # Preview the first `preview_len` characters (helps with debugging)
        print(f"\n--- Page {page_index + 1} Preview ---")
        print(page_text[:preview_len] + ("…" if len(page_text) > preview_len else ""))

        yield page_text
```

> **专业提示：** `tqdm` 进度条能提供可视化提示，尤其在处理 **如何 OCR 大型 PDF**、需要数分钟才能完成的文档时非常有用。

---

## 第四步：整合代码 – 完整可运行脚本

下面给出完整、可直接运行的示例。将其保存为 `pdf_ocr.py`，然后使用 `python pdf_ocr.py path/to/your/file.pdf` 执行。

```python
#!/usr/bin/env python3
"""
Complete script to perform OCR on PDF, extract text from PDF pages,
and preview recognized text. Works for both small and large PDFs.
"""

import sys
import aocr
from tqdm import tqdm

def create_engine():
    engine = aocr.OcrEngine()
    engine.max_memory_mb = 200
    engine.recognition_mode = aocr.RecognitionMode.PRINTED
    return engine

def load_pdf(engine, pdf_path):
    try:
        engine.load_pdf(pdf_path)
        print(f"✅ Loaded '{pdf_path}' – {engine.page_count} pages.")
    except Exception as exc:
        raise RuntimeError(f"Unable to load PDF: {exc}")

def ocr_pages(engine, preview_len=200):
    for page_index in tqdm(range(engine.page_count), desc="OCR progress"):
        engine.select_page(page_index)
        page_text = engine.recognize()
        print(f"\n--- Page {page_index + 1} Preview ---")
        print(page_text[:preview_len] + ("…" if len(page_text) > preview_len else ""))
        yield page_text

def main(pdf_path):
    engine = create_engine()
    load_pdf(engine, pdf_path)

    all_text = []
    for txt in ocr_pages(engine):
        all_text.append(txt)

    # Optional: write the combined output to a .txt file
    out_path = pdf_path.rsplit(".", 1)[0] + "_ocr.txt"
    with open(out_path, "w", encoding="utf-8") as f:
        f.write("\n\n".join(all_text))
    print(f"\n✅ OCR complete. Full text saved to: {out_path}")

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python pdf_ocr.py <path_to_pdf>")
        sys.exit(1)
    pdf_file = sys.argv[1]
    main(pdf_file)
```

### 预期输出（摘录）

```
✅ Loaded 'large_contract.pdf' – 342 pages.

--- Page 1 Preview ---
Contract Agreement between Party A and Party B ... 

--- Page 2 Preview ---
Recitals: Whereas, the parties desire to ...

...
✅ OCR complete. Full text saved to: large_contract_ocr.txt
```

你会看到每页的简短预览，随后是一条确认信息，表明已将合并后的文本写入文件。

---

## 边缘情况与实用技巧

| 场景 | 处理办法 |
|------|----------|
| **加密 PDF** | 传入密码：`engine.load_pdf(pdf_path, password="mySecret")`。 |
| **超大 PDF（> 1000 页）** | 谨慎提升 `max_memory_mb`，或分块处理（例如一次处理 200 页）。 |
| **混合内容（印刷 + 手写）** | 若库支持，可将 `engine.recognition_mode` 切换为 `aocr.RecognitionMode.MIXED`。 |
| **缺失字体或扫描质量差** | 在调用 `recognize()` 前，用图像增强库（如 Pillow）对页面进行预处理。 |
| **内存溢出崩溃** | 减少 `preview_len`，或将每页文本直接写入磁盘，而不是全部保存在列表中。 |

---

## 如何高效 OCR 大型 PDF – 高级策略

在处理 **如何 OCR 大型 PDF** 时，速度与稳定性尤为关键。下面提供几条可在脚本中加入的技巧：

1. **按页并行** – 若 OCR 引擎线程安全，可使用 `concurrent.futures.ThreadPoolExecutor`。  
2. **缓存中间图像** – 部分引擎允许将光栅化页面存储在 SSD 上，显著降低重复运行时的 CPU 负担。  
3. **批量写入输出** – 与其把所有文本追加到 Python 列表，不如一次打开输出文件，随时写入每页文本。  
4. **调整 DPI** – 降低光栅化时的 DPI 可减少内存占用，但可能影响准确率；通常 200‑300 DPI 是一个折中点。

下面是一个展示如何并行化 OCR 步骤的简短代码片段（可选，使用前请取消注释）：

```python
# from concurrent.futures import ThreadPoolExecutor

# def ocr_page(engine, idx):
#     engine.select_page(idx)
#     return engine.recognize()

# with ThreadPoolExecutor(max_workers=4) as executor:
#     results = list(tqdm(executor.map(lambda i: ocr_page(engine, i),
#                                    range(engine.page_count)),
#                     total=engine.page_count,
#                     desc="Parallel OCR"))
```

记住：并行化会提升 CPU 使用率，长时间运行时请监控系统温度。

---

## 常见问答

**问：我可以把这个脚本用于其他 OCR 库（如 Tesseract）吗？**  
答：完全可以。只需将 `aocr` 的调用替换为 `pytesseract.image_to

## 接下来该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助你在已有技巧的基础上进一步深入。每篇资源都提供完整可运行的代码示例，并配有逐步解释，帮助你掌握更多 API 功能并探索替代实现方式。

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [How to Perform Image Text Extraction from Stream Using Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [How to extract text from image from URL using Aspose.OCR for Java](/ocr/english/java/advanced-ocr-techniques/perform-ocr-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}