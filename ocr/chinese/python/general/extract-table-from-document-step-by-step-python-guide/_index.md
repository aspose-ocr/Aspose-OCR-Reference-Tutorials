---
category: general
date: 2026-01-02
description: 使用 Python 从文档中提取表格。学习如何从 PDF 中读取表格并使用简洁、可复用的方案遍历表格行。
draft: false
keywords:
- extract table from document
- how to read tables from pdf
- how to iterate table rows
- pdf table extraction python
- document layout detection
language: zh
og_description: 在 Python 中从文档提取表格。本指南展示了如何使用可靠的引擎读取 PDF 表格并遍历表格行。
og_title: 从文档中提取表格 – 完整的 Python 教程
tags:
- Python
- PDF
- Data Extraction
title: 从文档中提取表格——一步一步的 Python 指南
url: /zh/python/general/extract-table-from-document-step-by-step-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从文档中提取表格 – 完整 Python 教程

是否曾经需要 **从文档中提取表格**，却不知从何入手？你并不孤单——许多开发者在处理隐藏在表格中的 PDF 数据时都会遇到同样的难题。在本教程中，我们将一步步演示一个实用的端到端解决方案，既展示 **如何读取 PDF 表格**，又演示 **如何遍历表格行**，帮助你将数据导入任意下游系统。

想象一下，你有一批发票，每张发票都有一张包含明细的汇总表。你希望将这些行导出为 CSV，以便后续分析。阅读完本指南后，你将拥有一个可复用的代码片段，实现上述功能，并附带一些避免常见坑点的技巧。

## 您将学习

- 使用布局引擎检测文档的布局。  
- 使用后处理器优化原始检测，以获得更清晰的表格结构。  
- 遍历检测到的表格的每一行，并打印（或存储）单元格内容。  

无需外部服务，无需神秘黑盒——只需普通的 Python 和一个流行的 OCR/布局库（例如 **pdfplumber**、**pdfminer.six**，或你已经在使用的专有 `engine`）。如果你已经有实现了 `recognize_layout()` 和 `run_postprocessor()` 的 `engine` 对象，只需直接使用下面的代码即可。

> **专业提示：** 如果你使用的是商业 SDK，请确保开启 “table detection” 功能；否则原始布局可能会漏掉合并单元格。

---

## 第一步：检测表格结构 – 从文档中提取表格

首先，你需要获取一个原始布局，告诉你页面上表格所在的位置。大多数现代 PDF 库都提供类似 `recognize_layout()` 的方法，返回块、行和单元格的层级结构。

```python
# Step 1 – Detect the document layout using the engine
# ---------------------------------------------------
# `engine` is assumed to be an instantiated object from your PDF library.
# It could be pdfplumber, a custom OCR SDK, or any tool that supports layout detection.
raw_layout = engine.recognize_layout()
```

**为什么这很重要：**  
原始布局为每个文本元素提供坐标，但通常会包含噪声——标题、页脚或不属于表格的零散字符。这就是为什么下一步至关重要。

> **常见问题：** *如果我的 PDF 有多页怎么办？*  
> `recognize_layout()` 通常返回一个页面对象列表。遍历这些页面，并对每一页应用相同的后处理逻辑即可。

---

## 第二步：优化检测 – 如何读取 PDF 表格

得到 `raw_layout` 后，需要对其进行清理。大多数引擎都自带后处理器，能够合并碎片化的单元格、去除无关文本，并构建完整的 `Table` 对象。

```python
# Step 2 – Refine the detected layout with the post‑processor
# ----------------------------------------------------------
# The post‑processor returns an enhanced layout where tables are
# represented as a list of rows, each row being a list of Cell objects.
enhanced_layout = engine.run_postprocessor(raw_layout)
```

**为什么需要这一步：**  
原始布局可能把一行表格报告为数十个微小碎片。后处理器会将这些碎片归并为逻辑单元格，后续遍历时就变得轻而易举。

> **边缘情况：** 某些 PDF 使用不可见的边框。如果发现缺少行，请在引擎中启用 “detect invisible lines” 标志（如果支持）。

---

## 第三步：遍历表格行 – 如何遍历表格行

现在拥有了干净的 `enhanced_layout`，提取数据就非常简单。下面的代码遍历每一行，将单元格文本用制表符连接（使输出对齐），并打印结果。你可以将 `print` 替换为任意存储逻辑——CSV 写入、数据库插入等。

```python
# Step 3 – Print the table contents row by row
# --------------------------------------------
# `enhanced_layout.table` is expected to be an iterable of rows.
# Each `row` is a list of Cell objects with a `.text` attribute.
for row in enhanced_layout.table:
    # Join each cell's text with a tab to align columns
    print("\t".join(cell.text for cell in row))
```

**预期输出（示例）：**

```
Item	Qty	Price	Total
Widget A	2	$10.00	$20.00
Widget B	1	$15.00	$15.00
Service C	5	$8.00	$40.00
```

如果需要 CSV 而不是制表符分隔的视图，只需将 `"\t".join(...)` 替换为 `",".join(...)` 并写入文件即可。

---

## 完整工作示例

将上述步骤整合在一起，下面是一个独立运行的脚本。根据你使用的库，调整导入和引擎初始化代码。

```python
# --------------------------------------------------------------
# Full script: extract table from document and iterate rows
# --------------------------------------------------------------
import sys

# -----------------------------------------------------------------
# 1️⃣  Import or instantiate your PDF layout engine.
# Replace the placeholder with the actual library you use.
# -----------------------------------------------------------------
# Example with a fictional `pdf_engine` package:
# from pdf_engine import LayoutEngine
# engine = LayoutEngine(api_key="YOUR_KEY")
# -----------------------------------------------------------------
# For pdfplumber (open‑source) you could do:
# import pdfplumber
# engine = pdfplumber.open("sample.pdf")
# -----------------------------------------------------------------
# We'll keep it generic for the tutorial.
# -----------------------------------------------------------------

def extract_table(engine):
    """
    Detect, refine, and iterate over a table in a PDF document.
    Returns a list of rows, where each row is a list of cell strings.
    """
    # Detect layout
    raw_layout = engine.recognize_layout()

    # Refine layout
    enhanced_layout = engine.run_postprocessor(raw_layout)

    # Collect rows
    rows = []
    for row in enhanced_layout.table:
        rows.append([cell.text for cell in row])
    return rows

def main(pdf_path):
    # Initialise your engine – this will differ per library
    # Below is a stub; replace with real initialization.
    engine = initialize_engine(pdf_path)   # <-- implement this

    try:
        table_rows = extract_table(engine)
        for row in table_rows:
            print("\t".join(row))
    except Exception as e:
        print(f"❌ Extraction failed: {e}", file=sys.stderr)

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python extract_table.py <path-to-pdf>")
    else:
        main(sys.argv[1])
```

**需要替换的部分：**

- `initialize_engine(pdf_path)`: 为你选择的库创建引擎实例。  
- `engine.recognize_layout()` / `engine.run_postprocessor()`: 如有不同，请使用对应的方法名。

使用 `python extract_table.py invoice.pdf` 运行脚本，将会打印出整齐的制表符分隔表格，便于后续处理。

---

## 图示说明

下面是一张快速示意图，展示检测流水线的工作流程。  
![extract table from document diagram showing raw layout → post‑processor → clean table]  

*Alt text:* *从文档中提取表格流程图*  

---

## 常见问题 & 边缘案例

| 问题 | 答案 |
|------|------|
| **如果 PDF 中有多个表格怎么办？** | `enhanced_layout.table` 可能只包含第一个检测到的表格。若库支持，遍历 `enhanced_layout.tables`（注意复数形式），对每个表格都使用相同的行遍历逻辑。 |
| **如何处理合并单元格？** | 后处理器通常会将合并单元格展开为独立条目。如果没有，请检查引擎的 `merge_cells` 标志，或根据坐标手动合并相邻单元格。 |
| **能从扫描版 PDF 中提取表格吗？** | 可以，但需要在布局检测前先进行 OCR。许多 SDK 将 OCR 与布局检测合二为一，只需对扫描文档调用 `recognize_layout()`。 |
| **大批量处理时性能如何？** | 可使用 `concurrent.futures` 并行处理页面。最耗时的是 OCR；保持引擎实例在多个文件之间复用，可避免重复加载大型模型。 |
| **需要额外安装依赖吗？** | 若使用 `pdfplumber`，请运行 `pip install pdfplumber`。商业 SDK 请参考供应商的安装指南。 |

---

## 结论

我们已经展示了如何通过 **从文档中提取表格**：先检测布局，再优化，最后 **遍历表格行**，得到干净可用的数据。无论是喂入数据仓库、生成报告，还是仅仅将 PDF 转为 CSV，这一模式始终不变：检测 → 清理 → 遍历。

后续可以进一步探索的方向：

- 使用 **如何读取 PDF 表格** 时获取额外的样式信息（字体、颜色）。  
- 直接导出为 **pandas DataFrames** 进行分析。  
- 使用相同流水线 **将表格写回新 PDF**（逆向流程）。  

尝试用自己的几份 PDF 运行脚本，感受将静态表格转化为可操作数据的速度。祝你提取愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}