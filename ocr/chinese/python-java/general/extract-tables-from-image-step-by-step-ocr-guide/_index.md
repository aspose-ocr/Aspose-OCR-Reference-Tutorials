---
category: general
date: 2026-03-26
description: 使用 Python OCR 从图像中提取表格并将图像转换为电子表格。学习如何加载图像进行 OCR、读取表格并提取表格数据。
draft: false
keywords:
- extract tables from image
- convert image to spreadsheet
- load image for ocr
- ocr read tables
- ocr extract table data
language: zh
og_description: 使用 Python OCR 从图像中提取表格。本指南展示了如何加载图像进行 OCR、读取表格并将其转换为电子表格。
og_title: 从图像中提取表格 – 完整 OCR 教程
tags:
- OCR
- Python
- Data Extraction
title: 从图像中提取表格 – 步骤式 OCR 指南
url: /zh/python-java/general/extract-tables-from-image-step-by-step-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从图像中提取表格 – 完整 OCR 教程

是否曾经需要**从图像中提取表格**却不知从何入手？你并不孤单。很多开发者在面对包含表格数据的 PDF 或截图时都会卡住，因为这些数据必须转换为可编辑的行列。好消息是，只需几行 Python 代码，配合强大的 OCR 引擎，就能在几秒钟内把图片变成可用的电子表格。

在本教程中，我们将逐步演示如何加载用于 OCR 的图像、运行识别引擎，并逐行提取每个表格。完成后，你将能够**将图像转换为电子表格**，并了解如何**ocr read tables**以及**ocr extract table data**以进行后续处理。没有隐藏的魔法，只有清晰可运行的代码，今天就可以直接放入你的项目中使用。

---

## 你需要准备什么

在开始之前，请确保手头有以下内容：

- **Python 3.9+** – 最新的稳定版效果最佳。  
- **`ocr`** 库（或任何提供 `OcrEngine`、`Image` 和表格相关方法的兼容 OCR SDK）。使用 `pip install ocr‑sdk` 安装（请替换为实际的包名）。  
- 一张包含清晰打印表格的图像文件（`.png`、`.jpg` 等）。  
- 可选：如果想直接将提取的数据写入 CSV 或 Excel 文件，请安装 **pandas**（`pip install pandas`）。

准备好了吗？太好了——我们开始吧。

---

## 步骤 1：导入 OCR SDK 并准备环境

首先，需要把 OCR 类导入脚本，并设置一个小助手，以便后续将原始表格数据转换为 DataFrame。

```python
# Step 1 – Imports and basic setup
import ocr                     # The OCR SDK
from pathlib import Path      # Handy for file paths
import pandas as pd           # For converting tables to spreadsheets

# Optional: configure logging to see what the engine is doing
import logging
logging.basicConfig(level=logging.INFO)
```

**为什么重要：** 导入 `ocr` 后我们即可使用 `OcrEngine`、`Imaging.Image` 以及将要遍历的表格对象。`pandas` 并非提取必需，但它能让“将图像转换为电子表格”变得非常简单。

---

## 步骤 2：加载待处理的图像

现在我们真正**加载用于 OCR 的图像**。SDK 需要一个 `Image` 对象，因此我们使用 `Image.load()` 方法包装文件路径。

```python
# Step 2 – Load the image that contains a table
image_path = Path("YOUR_DIRECTORY/table_image.png")

# Verify the file exists early to avoid cryptic SDK errors
if not image_path.is_file():
    raise FileNotFoundError(f"Image not found: {image_path}")

# Create an OCR engine instance
ocr_engine = ocr.OcrEngine()

# Attach the image to the engine
ocr_engine.set_image(ocr.Imaging.Image.load(str(image_path)))
```

**小贴士：** 将图像文件放在专用文件夹（如 `assets/` 或 `data/`）并使用相对路径，这样脚本在不同机器之间更易移植。

---

## 步骤 3：运行识别过程

图像准备好后，我们可以让引擎**ocr read tables**。`recognize()` 调用会返回一个结果对象，里面包含引擎发现的所有内容——文本块、行以及对我们最重要的表格。

```python
# Step 3 – Perform OCR and obtain results
ocr_result = ocr_engine.recognize()

# Quick sanity check: did the engine find any tables?
if not ocr_result.get_tables():
    logging.warning("No tables detected in the image.")
else:
    logging.info(f"Found {len(ocr_result.get_tables())} table(s).")
```

**为什么要检查：** 有些图像可能噪声较大或表格边框模糊，导致引擎漏检。记录警告可以让你在脚本崩溃前获得早期反馈。

---

## 步骤 4：提取每个表格的行和单元格

真正的魔法就在这里。我们会遍历每个检测到的表格，逐行提取，再获取每个单元格的文本。内部的列表推导让代码简洁，同时我们仍会解释其流程。

```python
# Step 4 – Iterate over detected tables and collect data
all_tables = []   # Will hold a list of pandas DataFrames

for table_idx, table_obj in enumerate(ocr_result.get_tables(), start=1):
    logging.info(f"Processing Table #{table_idx}")

    rows_data = []   # Temporary storage for this table's rows

    for row_obj in table_obj.get_rows():
        # Extract text from each cell in the current row
        cell_texts = [cell.get_text() for cell in row_obj.get_cells()]
        rows_data.append(cell_texts)

    # Convert the raw list of rows into a DataFrame
    df = pd.DataFrame(rows_data)
    all_tables.append(df)

    # Print a human‑readable version to the console
    print("\n=== New Table ===")
    for row in rows_data:
        print("\t".join(row))
```

**代码在做什么？**  

- `enumerate(..., start=1)` 为日志提供友好的表格编号。  
- `row_obj.get_cells()` 返回每个单元格对象；`cell.get_text()` 获取 OCR 解码后的字符串。  
- 我们把行数据存入 `rows_data`，再交给 `pandas.DataFrame` 自动对齐列。  
- `print` 代码块对应原示例中的**关键输出**，便于你即时验证结果。

**异常情况处理：** 如果某行的单元格数量与其他行不同，`pandas` 会用 `NaN` 填充缺失位置。后续可使用 `df.fillna('')` 将其替换为空字符串。

---

## 步骤 5：将提取的表格保存为电子表格

现在我们已经拥有一个 DataFrame 列表，将它们写入 Excel 工作簿（或 CSV 文件）轻而易举。这正好实现了“将图像转换为电子表格”的目标。

```python
# Step 5 – Export tables to Excel (one sheet per table)
output_path = Path("extracted_tables.xlsx")
with pd.ExcelWriter(output_path, engine="openpyxl") as writer:
    for idx, df in enumerate(all_tables, start=1):
        sheet_name = f"Table_{idx}"
        df.to_excel(writer, sheet_name=sheet_name, index=False)

logging.info(f"All tables saved to {output_path}")
```

**为什么选择 Excel？** 大多数业务用户更喜欢 `.xlsx` 格式。如果你更倾向于 CSV，只需将循环改为 `df.to_csv(f"table_{idx}.csv", index=False)`。

---

## 完整、可直接运行的脚本

把所有步骤整合在一起，下面就是可以复制粘贴并执行的完整程序。

```python
import ocr
from pathlib import Path
import pandas as pd
import logging

logging.basicConfig(level=logging.INFO)

# ---------- Configuration ----------
image_path = Path("YOUR_DIRECTORY/table_image.png")
output_path = Path("extracted_tables.xlsx")
# ----------------------------------

# Verify image exists
if not image_path.is_file():
    raise FileNotFoundError(f"Image not found: {image_path}")

# Initialize OCR engine
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(ocr.Imaging.Image.load(str(image_path)))

# Run recognition
ocr_result = ocr_engine.recognize()

if not ocr_result.get_tables():
    logging.warning("No tables detected in the image.")
    exit(0)

all_tables = []

for table_idx, table_obj in enumerate(ocr_result.get_tables(), start=1):
    logging.info(f"Processing Table #{table_idx}")
    rows_data = []

    for row_obj in table_obj.get_rows():
        cell_texts = [cell.get_text() for cell in row_obj.get_cells()]
        rows_data.append(cell_texts)

    df = pd.DataFrame(rows_data)
    all_tables.append(df)

    print("\n=== New Table ===")
    for row in rows_data:
        print("\t".join(row))

# Save to Excel
with pd.ExcelWriter(output_path, engine="openpyxl") as writer:
    for idx, df in enumerate(all_tables, start=1):
        df.to_excel(writer, sheet_name=f"Table_{idx}", index=False)

logging.info(f"All tables saved to {output_path}")
```

**预期的控制台输出**（假设是一个 2×3 的简单表格）：

```
=== New Table ===
Header1    Header2    Header3
Row1Col1   Row1Col2   Row1Col3
Row2Col1   Row2Col2   Row2Col3
```

运行后，你会在脚本所在目录看到 `extracted_tables.xlsx`，每个表格占一个工作表。

---

## 常见问题与技巧

| Question | Answer |
|----------|--------|
| **Can I use a different OCR library?** | Absolutely. The pattern stays the same: load image → recognize → iterate over `get_tables()`. Just replace the import and object names. |
| **What if my image is noisy?** | Pre‑process with OpenCV (thresholding, deskew) before feeding it to the OCR engine. Noise reduction often improves **ocr extract table data** accuracy. |
| **Do I need to install `openpyxl`?** | Yes, `pandas` uses it under the hood for Excel output. Install with `pip install openpyxl`. |
| **How do I handle merged cells?** | Some SDKs expose `cell.is_merged()`; you can detect and propagate the value across the merged range manually. |
| **Is there a way to extract only specific tables?** | Filter by `table_obj.get_confidence()` or by checking header keywords before processing. |

---

## 结束语

现在，你已经拥有一个完整的端到端解决方案，能够**从图像中提取表格**、将结果转换为整洁的电子表格，并且能够处理单张图片中的多个表格。该脚本演示了如何**load image for OCR**、**ocr read tables**以及**ocr extract table data**，同时保持对实际场景的灵活适配。

接下来可以尝试将 PDF 页面渲染为图像后再喂给 OCR，引入不同语言和字体进行实验。你甚至可以把 DataFrame 直接写入数据库或报表工具——想象力就是唯一的限制。

如果你觉得本指南对你有帮助，欢迎分享、给托管 SDK 的仓库加星，或在评论区留下你的技巧。祝编码愉快，愿你的表格始终被完美解析！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}