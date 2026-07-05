---
category: general
date: 2026-07-05
description: ดึงตารางจากภาพด้วย Python OCR. เรียนรู้วิธีดึงตาราง, แปลงภาพเป็น TSV,
  และเชี่ยวชาญเทคนิค OCR ตารางภาพด้วย Python.
draft: false
keywords:
- extract table from image
- how to extract table
- convert image to tsv
- ocr table image python
language: th
og_description: ดึงตารางจากภาพด้วย Python OCR คู่มือนี้แสดงวิธีดึงตาราง, แปลงภาพเป็น
  TSV, และใช้เครื่องมือ OCR ตารางภาพใน Python
og_title: สกัดตารางจากรูปภาพ – แปลงรูปภาพเป็น TSV ด้วย Python
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract table from image using Python OCR. Learn how to extract table,
    convert image to TSV, and master ocr table image python techniques.
  headline: Extract Table from Image – Convert Image to TSV in Python
  type: TechArticle
- description: Extract table from image using Python OCR. Learn how to extract table,
    convert image to TSV, and master ocr table image python techniques.
  name: Extract Table from Image – Convert Image to TSV in Python
  steps:
  - name: Initialise the aocr OCR engine.
    text: Initialise the aocr OCR engine.
  - name: Attach the AI post‑processor.
    text: Attach the AI post‑processor.
  - name: Load a table image.
    text: Load a table image.
  - name: Perform structured OCR.
    text: Perform structured OCR.
  - name: Clean the results.
    text: Clean the results.
  - name: Export the table as a TSV file.
    text: Export the table as a TSV file.
  type: HowTo
tags:
- OCR
- Python
- Table Extraction
title: ดึงตารางจากรูปภาพ – แปลงรูปภาพเป็น TSV ด้วย Python
url: /th/python/general/extract-table-from-image-convert-image-to-tsv-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ดึงตารางจากรูปภาพ – แปลงรูปภาพเป็น TSV ด้วย Python

เคยสงสัยไหมว่าจะแยกตารางจากรูปภาพโดยไม่ต้องบีบหัวของคุณ? ในบทแนะนำนี้เราจะอธิบายขั้นตอน **how to extract table** จากรูปภาพโดยใช้ไลบรารี `aocr` แล้วแปลงข้อมูลนั้นเป็นไฟล์ TSV ที่เรียบร้อย ไม่ต้องใช้เวทมนตร์ เพียงไม่กี่บรรทัดของ Python และการประมวลผลหลังจาก AI‑powered

หากคุณเคยพยายามคัดลอก‑วางตารางจากใบแจ้งหนี้ที่สแกนหรือสกรีนช็อตแล้วได้ผลลัพธ์เป็นกองข้อมูลที่สับสน คุณจะเข้าใจว่าทำไมวิธีการที่ขับเคลื่อนด้วย OCR จึงคุ้มค่าในการเรียนรู้ เมื่อจบคุณจะสามารถป้อนรูปภาพของตารางใด ๆ ให้ Python แล้วได้ค่า TSV ที่สะอาดพร้อมใช้ในสเปรดชีตหรือฐานข้อมูล

---

## สิ่งที่คุณต้องการ

ก่อนที่เราจะดำเนินการต่อ ให้ตรวจสอบว่าคุณมีสิ่งต่อไปนี้บนเครื่องของคุณ:

| Requirement | Why it matters |
|-------------|----------------|
| Python 3.9+ | แพคเกจ `aocr` รองรับรันไทม์ Python รุ่นใหม่ |
| `aocr` library (`pip install aocr`) | ให้เครื่องมือ OCR และ AI post‑processor ที่เราจะใช้ |
| An image file containing a table (PNG, JPG, etc.) | ข้อมูลต้นทางที่เราจะดึง |
| Optional: a virtual environment | ทำให้การจัดการ dependencies แยกจากกัน—แนะนำอย่างยิ่ง |

การเตรียมสิ่งเหล่านี้ไว้ล่วงหน้าจะช่วยให้คุณไม่ต้องหยุดกลางทางระหว่างทำตามคู่มือ

---

## Install the Dependencies

ก่อนอื่น ให้ติดตั้งเครื่องมือ OCR เปิดเทอร์มินัลแล้วรัน:

```bash
# Create and activate a virtual environment (optional but clean)
python -m venv ocr-env
source ocr-env/bin/activate   # On Windows: ocr-env\Scripts\activate

# Install the aocr package
pip install aocr
```

> **Pro tip:** หากเจอข้อผิดพลาดเรื่องสิทธิ์ ให้เพิ่ม `--user` ไปที่คำสั่ง `pip install` หรือใช้ `pipx` เพื่อติดตั้งแบบทั่วโลก

---

## Step 1 – Initialise the OCR Engine

เอนจินเป็นหัวใจของกระบวนการ คิดว่าเป็น “สมอง” ที่มองแต่ละพิกเซลและตัดสินว่าตัวอักษรใดควรอยู่ที่ไหน

```python
import aocr

# Create an OCR engine instance – this sets up the model and default settings
engine = aocr.OcrEngine()
```

ทำไมเราต้องสร้างอินสแตนซ์ของเอนจินแทนการเรียกฟังก์ชันเดียว? วัตถุเอนจินทำให้เราสามารถแนบ post‑processor ที่กำหนดเองในภายหลัง ให้การควบคุมผลลัพธ์อย่างละเอียด—จำเป็นเมื่อคุณต้องการความแม่นยำ **ocr table image python**

---

## Step 2 – Attach the AI Post‑Processor

`aocr` มาพร้อม AI post‑processor ที่เบาและทำความสะอาดผลลัพธ์ OCR ดิบขณะยังคงรักษาขอบเซลล์ไว้ ไม่ต้องระบุอาร์กิวเมนต์เพิ่มเติม ทำให้โค้ดดูเรียบร้อย

```python
# Hook the AI post‑processor into the engine
engine.set_post_processor(ai.run_postprocessor, None)
```

หากข้ามขั้นตอนนี้ คุณยังจะได้ข้อความดิบ แต่โครงสร้างตารางจะเป็นเสียงรบกวน—เหมือนสเปรดชีตที่ทุกเซลล์เป็นปริศนา Post‑processor จะทำหน้าที่จัดเรียงข้อความให้ตรงกับกริดเดิม

---

## Step 3 – Load Your Table Image

คุณสามารถโหลดรูปภาพจากพาธใดก็ได้ แต่เพื่อความชัดเจน เราจะอ้างอิงไดเรกทอรีตัวอย่าง แทนที่ `"YOUR_DIRECTORY/invoice_table.png"` ด้วยพาธจริงของไฟล์ของคุณ

```python
# Load the image that contains the table
image_path = "YOUR_DIRECTORY/invoice_table.png"
image = aocr.Image.from_file(image_path)
```

> **Note:** `aocr.Image` ตรวจจับรูปแบบไฟล์โดยอัตโนมัติและทำให้ช่องสีเป็นมาตรฐาน จึงไม่จำเป็นต้องทำการพรี‑โปรเซสไฟล์เว้นแต่ไฟล์จะเสื่อมสภาพอย่างรุนแรง

---

## Step 4 – Perform Structured OCR

ตอนนี้เอนจินจะสแกนรูปภาพและคืนค่าอ็อบเจ็กต์ตารางดิบ ซึ่งอ็อบเจ็กต์นี้มีแถว, คอลัมน์ และข้อความดิบของแต่ละเซลล์

```python
# Recognise the table structure and extract raw cell data
raw_table = engine.recognize_structured(image)
```

ทำไมต้องใช้ `recognize_structured` แทนการเรียก `recognize` แบบทั่วไป? เวอร์ชันโครงสร้างพยายามสรุปขอบเขตแถว/คอลัมน์ ให้ผลลัพธ์คล้ายเมทริกซ์ที่แปลงเป็น TSV ได้ง่ายกว่าในภายหลัง

---

## Step 5 – Clean the Data with the AI Post‑Processor

การรัน post‑processor จะทำให้ผลลัพธ์ดิบสะอาดขึ้น: ลบอักขระรบกวน, รวมส่วนที่แยกออก, และทำให้ข้อความของแต่ละเซลล์จัดตำแหน่งอย่างถูกต้อง

```python
# Apply the AI post‑processor to tidy up the table
processed_table = engine.run_postprocessor(raw_table)
```

หากคุณตรวจสอบ `processed_table.table` คุณจะเห็นรายการของแถว แต่ละแถวเป็นรายการของอ็อบเจ็กต์ `Cell` แต่ละ `Cell` มีแอตทริบิวต์ `.text` ที่เก็บสตริงที่ทำความสะอาดแล้ว

---

## Step 6 – Export the Table as TSV

ขั้นตอนสุดท้ายคือการแปลงข้อมูลที่ทำความสะอาดเป็นไฟล์ค่าแยกด้วยแท็บ (TSV)—สิ่งที่คุณต้องการเมื่ออยาก **convert image to TSV** สำหรับ Excel หรือ Google Sheets

```python
import csv

# Define the output TSV path
tsv_path = "extracted_table.tsv"

# Open the file and write rows as tab‑separated values
with open(tsv_path, "w", newline="", encoding="utf-8") as tsv_file:
    writer = csv.writer(tsv_file, delimiter="\t")
    for row in processed_table.table:
        # Extract text from each cell and write the row
        writer.writerow([cell.text for cell in row])

print(f"✅ Table successfully saved to {tsv_path}")
```

การรันสคริปต์จะพิมพ์แต่ละแถวลงคอนโซล (หากคุณต้องการ) และเขียนไฟล์ TSV ที่สะอาดซึ่งสามารถเปิดในโปรแกรมสเปรดชีตใดก็ได้

### Quick verification

```python
# Print the TSV to the console for a sanity check
for row in processed_table.table:
    print("\t".join(cell.text for cell in row))
```

คุณควรเห็นคอลัมน์ที่จัดเรียงอย่างเป็นระเบียบ เช่น:

```
Item	Qty	Price	Total
Apple	10	0.50	5.00
Banana	5	0.30	1.50
```

หากผลลัพธ์ดูสับสน ให้ตรวจสอบคุณภาพของรูปภาพ (ความคมชัด, คอนทราสต์) และลองปรับการตั้งค่าเอนจิน OCR—`engine.set_config(...)` ให้คุณปรับโมเดลภาษาและเกณฑ์ความเชื่อมั่นได้

---

## Handling Common Edge Cases

| Situation | Suggested Fix |
|-----------|---------------|
| **Skewed image** | หมุนล่วงหน้าด้วย `Pillow` (`Image.rotate`) ก่อนส่งให้ `aocr` |
| **Low contrast** | ใช้การทำสมดุลฮิสโตแกรม (`cv2.equalizeHist`) เพื่อเพิ่มความอ่านได้ |
| **Merged cells** | ประมวลผล TSV ต่อเพื่อแยกเซลล์ตามตัวคั่นที่รู้จักหรือใช้แฟล็ก `merge_cells=False` หากมี |
| **Multi‑page PDFs** | แปลงแต่ละหน้าเป็นรูปภาพก่อน (`pdf2image`) แล้วรันพายไลน์ในลูป |

การปรับแต่งเหล่านี้ทำให้เวิร์กโฟลว์ **ocr table image python** ของคุณแข็งแรงแม้กับแหล่งข้อมูลที่หลากหลาย

---

## Full Script – One‑Stop Solution

ด้านล่างเป็นสคริปต์เต็มที่พร้อมรันซึ่งรวมทุกขั้นตอนที่อธิบายไว้ บันทึกเป็น `extract_table.py` แล้วรันด้วย `python extract_table.py`

```python
#!/usr/bin/env python3
"""
Extract Table from Image – Convert Image to TSV (Python)

This script demonstrates how to:
1. Initialise the aocr OCR engine.
22. Attach the AI post‑processor.
3. Load a table image.
4. Perform structured OCR.
5. Clean the results.
6. Export the table as a TSV file.

Author: Your Name
Date: 2026-07-05
"""

import aocr
import csv
import sys
from pathlib import Path

def main(image_path: str, output_tsv: str = "extracted_table.tsv"):
    # Step 1 – Initialise engine
    engine = aocr.OcrEngine()

    # Step 2 – Attach AI post‑processor
    engine.set_post_processor(ai.run_postprocessor, None)

    # Step 3 – Load image
    if not Path(image_path).is_file():
        sys.exit(f"❌ Image not found: {image_path}")
    image = aocr.Image.from_file(image_path)

    # Step 4 – Structured OCR
    raw_table = engine.recognize_structured(image)

    # Step 5 – Clean with post‑processor
    processed_table = engine.run_postprocessor(raw_table)

    # Step 6 – Write TSV
    with open(output_tsv, "w", newline="", encoding="utf-8") as tsv_file:
        writer = csv.writer(tsv_file, delimiter="\


## What Should You Learn Next?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอน‑ต่อ‑ขั้นตอน เพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานอื่น ๆ ในโปรเจกต์ของคุณ

- [ดึงข้อความจากรูปภาพด้วย Aspose OCR – คู่มือขั้นตอนโดยขั้นตอน](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [วิธีดึงตารางจากรูปภาพโดยใช้ Aspose.OCR สำหรับ .NET](/ocr/english/net/text-recognition/recognize-table/)
- [วิธีดึงข้อความจากรูปภาพโดยการเตรียมสี่เหลี่ยมใน OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}