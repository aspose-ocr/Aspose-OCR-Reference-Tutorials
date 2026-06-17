---
category: general
date: 2026-04-29
description: 使用 Aspose OCR 在 Python 中提取 PDF 文本。了解批量 OCR PDF 处理，转换扫描 PDF 文本，并处理低置信度页面。
draft: false
keywords:
- extract text from pdf
- ocr pdf with python
- convert scanned pdf text
- batch ocr pdf processing
language: zh
og_description: 使用 Aspose OCR 在 Python 中提取 PDF 文本。本指南展示批量 OCR PDF 处理、将扫描的 PDF 转换为文本，以及处理低置信度结果。
og_title: 从 PDF 中提取文本 – 使用 Python 进行 OCR
tags:
- OCR
- Python
- PDF processing
title: 从 PDF 中提取文本 – 使用 Python 进行 OCR
url: /zh/python/general/extract-text-from-pdf-ocr-pdf-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从 PDF 中提取文本 – 使用 Python 进行 OCR PDF

是否曾经需要 **从 PDF 中提取文本**，但文件只是扫描的图像？你并不孤单——很多开发者在尝试将 PDF 转换为可搜索数据时都会遇到这个难题。好消息是：使用 Aspose OCR for Python，你可以在几行代码内转换扫描的 PDF 文本，甚至在处理数十个文件时进行 **批量 OCR PDF 处理**。

在本教程中，我们将完整演示工作流：设置库、对单个 PDF 进行 OCR、扩展为批量处理，并处理低置信度页面，以便在需要人工审查时及时发现。完成后，你将拥有一个可直接运行的脚本，能够从任何扫描的 PDF 中提取文本，并且了解每一步背后的原理。

## 您需要的条件

在开始之前，请确保你具备：

- Python 3.8 或更高版本（代码使用 f‑strings，3.6+ 可运行，但推荐 3.8+）
- Aspose OCR for Python 许可证或免费试用密钥（可从 Aspose 官网获取）
- 一个或多个待处理的扫描 PDF 所在文件夹
- 用于生成 *.txt* 报告的适量磁盘空间

就这些——无需繁重的外部依赖，也不需要 OpenCV 之类的技巧。Aspose OCR 引擎会为你完成所有繁重工作。

## 设置环境

首先，从 PyPI 安装 Aspose OCR 包：

```bash
pip install aspose-ocr
```

如果你有许可证文件 (`Aspose.OCR.lic`)，请将其放在项目根目录，并按如下方式激活：

```python
# Activate Aspose OCR license (optional but removes trial watermark)
from aspose.ocr import License

license = License()
license.set_license("Aspose.OCR.lic")
```

> **小贴士：** 将许可证文件排除在版本控制之外；将其加入 `.gitignore`，以避免意外泄露。

## 对单个 PDF 执行 OCR

现在让我们从单个扫描 PDF 中提取文本。核心步骤如下：

1. 创建 `OcrEngine` 实例。  
2. 指定 PDF 文件路径。  
3. 为每一页获取 `OcrResult`。  
4. 将纯文本输出写入磁盘。  
5. 释放引擎以清理本地资源。

以下是完整、可运行的脚本：

```python
# Step 1: Import the OCR engine and create an instance
from aspose.ocr import OcrEngine

# Optional: activate license (see previous section)
# from aspose.ocr import License
# License().set_license("Aspose.OCR.lic")

ocr_engine = OcrEngine()

# Step 2: Specify the PDF file to be processed
pdf_file_path = r"YOUR_DIRECTORY/input.pdf"

# Step 3: Extract OCR results – one OcrResult object per page
ocr_pages = ocr_engine.extract_from_pdf(pdf_file_path)

# Step 4: Iterate through the results, show confidence, flag low‑confidence pages, and save the plain text
for ocr_page in ocr_pages:
    print(f"Page {ocr_page.page_number}: confidence {ocr_page.confidence:.2%}")

    # If confidence is below 80 %, flag it for manual review
    if ocr_page.confidence < 0.80:
        print("  Low confidence – consider manual review")

    # Build the output filename
    output_txt = f"YOUR_DIRECTORY/Report_page{ocr_page.page_number}.txt"
    with open(output_txt, "w", encoding="utf-8") as f:
        f.write(ocr_page.text)

# Step 5: Release resources used by the engine
ocr_engine.dispose()
```

**您将看到：** 脚本会为每页打印类似 `Page 1: confidence 97.45%` 的信息。如果某页的置信度低于 80 %，会出现警告，提示 OCR 可能遗漏了字符。

### 为什么这样有效

- **`OcrEngine`** 是通向本地 Aspose OCR 库的入口，负责从图像预处理到字符识别的全部工作。  
- **`extract_from_pdf`** 会自动将每页 PDF 栅格化，无需自行将 PDF 转为图像。  
- **置信度分数** 让你能够自动化质量检查——在处理法律或医疗文档等对准确性要求极高的场景时尤为关键。

## 使用 Python 批量 OCR PDF 处理

大多数真实项目都会涉及多个文件。下面我们把单文件脚本扩展为 **批量 OCR PDF 处理** 流程，遍历目录、处理每个 PDF，并将结果存入对应的子文件夹。

```python
import os
from pathlib import Path
from aspose.ocr import OcrEngine

def ocr_pdf_file(pdf_path: Path, output_dir: Path, engine: OcrEngine, confidence_threshold: float = 0.80):
    """Extract text from a single PDF and write per‑page .txt files."""
    ocr_pages = engine.extract_from_pdf(str(pdf_path))
    for page in ocr_pages:
        print(f"{pdf_path.name} – Page {page.page_number}: {page.confidence:.2%}")
        if page.confidence < confidence_threshold:
            print("  ⚠️ Low confidence – manual review may be needed")

        out_file = output_dir / f"{pdf_path.stem}_page{page.page_number}.txt"
        out_file.write_text(page.text, encoding="utf-8")

def batch_ocr_pdf(input_folder: str, output_folder: str):
    """Iterate over all PDFs in input_folder and run OCR."""
    engine = OcrEngine()
    input_path = Path(input_folder)
    output_path = Path(output_folder)
    output_path.mkdir(parents=True, exist_ok=True)

    pdf_files = list(input_path.glob("*.pdf"))
    if not pdf_files:
        print("🚫 No PDF files found in the specified folder.")
        return

    for pdf_file in pdf_files:
        # Create a sub‑folder for each PDF to keep pages organized
        pdf_out_dir = output_path / pdf_file.stem
        pdf_out_dir.mkdir(exist_ok=True)
        ocr_pdf_file(pdf_file, pdf_out_dir, engine)

    # Clean up native resources
    engine.dispose()
    print("✅ Batch OCR completed.")

# Example usage:
if __name__ == "__main__":
    batch_ocr_pdf("YOUR_DIRECTORY/input_pdfs", "YOUR_DIRECTORY/ocr_output")
```

#### 此功能的帮助

- **可扩展性：** 该函数一次遍历文件夹，为每个 PDF 创建专属输出子文件夹。当文档数量达到数十甚至上百时，文件结构依然整洁。  
- **可复用性：** `ocr_pdf_file` 可以被其他脚本（例如 Web 服务）调用，因为它是纯函数。  
- **错误处理：** 若输入文件夹为空，脚本会打印友好提示，避免静默失败。

## 转换扫描 PDF 文本 – 处理边缘情况

虽然上述代码能适用于大多数 PDF，但仍可能遇到以下特殊情况：

| 情况 | 产生原因 | 解决方案 |
|-----------|----------------|-----------------|
| **加密 PDF** | PDF 受密码保护。 | 使用 `extract_from_pdf(pdf_path, password="yourPwd")` 传入密码。 |
| **多语言文档** | Aspose OCR 默认使用英文。 | 设置 `ocr_engine.language = "spa"` 以识别西班牙语，或提供语言列表以处理混合语言。 |
| **超大 PDF（>500 页）** | 每页加载到内存导致内存占用激增。 | 使用 `engine.extract_from_pdf(pdf_path, start_page=1, end_page=100)` 分块处理，并在循环中调用。 |
| **扫描质量差** | DPI 过低或噪点过多导致置信度下降。 | 开启 `engine.image_preprocessing = True` 进行图像预处理，或通过 `engine.dpi = 300` 提高 DPI。 |

> **注意：** 开启图像预处理会显著增加 CPU 耗时。如果你在夜间运行批处理，请预留足够时间或启用独立的工作节点。

## 验证输出

脚本执行完毕后，你会看到类似以下的文件夹结构：

```
ocr_output/
├─ invoice_2023/
│  ├─ invoice_2023_page1.txt
│  ├─ invoice_2023_page2.txt
│  └─ …
└─ contract_A/
   ├─ contract_A_page1.txt
   └─ …
```

打开任意 `.txt` 文件，你应该能看到干净的 UTF‑8 编码文本，内容与原始扫描文档相匹配。如果出现乱码，请再次检查 PDF 的语言设置，并确保机器上已安装相应的字体包。

## 清理资源

Aspose OCR 依赖本地 DLL，完成后务必调用 `engine.dispose()` 释放资源。忘记此步骤会导致内存泄漏，尤其在长时间运行的批处理任务中更为严重。

```python
# Always the last line of your script
engine.dispose()
```

## 完整端到端示例

把所有内容组合在一起，下面是一个完整的示例脚本：

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}