---
category: general
date: 2026-01-02
description: ดึงตารางจากเอกสารโดยใช้ Python. เรียนรู้วิธีอ่านตารางจาก PDF และวนลูปแถวของตารางด้วยโซลูชันที่สะอาดและนำกลับมาใช้ใหม่ได้.
draft: false
keywords:
- extract table from document
- how to read tables from pdf
- how to iterate table rows
- pdf table extraction python
- document layout detection
language: th
og_description: ดึงตารางจากเอกสารด้วย Python. คู่มือนี้แสดงวิธีอ่านตารางจาก PDF และวนซ้ำแถวของตารางด้วยเครื่องมือที่เชื่อถือได้.
og_title: ดึงตารางจากเอกสาร – คอร์สสอน Python อย่างครบถ้วน
tags:
- Python
- PDF
- Data Extraction
title: สกัดตารางจากเอกสาร – คู่มือ Python ทีละขั้นตอน
url: /th/python/general/extract-table-from-document-step-by-step-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ดึงตารางจากเอกสาร – การสอน Python ฉบับสมบูรณ์

เคยต้อง **ดึงตารางจากเอกสาร** แต่ไม่รู้จะเริ่มต้นอย่างไรหรือไม่? คุณไม่ได้เป็นคนเดียว—นักพัฒนาหลายคนเจออุปสรรคเดียวกันเมื่อต้องจัดการกับ PDF ที่ซ่อนข้อมูลไว้ในตาราง ในบทเรียนนี้เราจะพาคุณผ่านโซลูชันแบบครบวงจรที่ไม่เพียงแสดง **วิธีอ่านตารางจาก pdf** เท่านั้น แต่ยังสาธิต **วิธีวนลูปแถวของตาราง** เพื่อให้คุณสามารถส่งต่อข้อมูลไปยังที่ที่ต้องการได้

ลองนึกภาพว่าคุณมีชุดใบแจ้งหนี้หลายใบ แต่ละใบมีตารางสรุปรายการสินค้า คุณต้องการแปลงแถวเหล่านั้นเป็น CSV เพื่อการวิเคราะห์ต่อไป เมื่อจบบทเรียนนี้คุณจะมีสคริปต์ที่ใช้ซ้ำได้ซึ่งทำสิ่งนั้นได้อย่างแม่นยำ พร้อมเคล็ดลับหลีกเลี่ยงข้อผิดพลาดทั่วไปอีกด้วย

## สิ่งที่คุณจะได้เรียนรู้

- ตรวจจับโครงสร้างของเอกสารด้วย layout engine  
- ปรับปรุงการตรวจจับดิบด้วย post‑processor เพื่อให้ได้โครงสร้างตารางที่สะอาดขึ้น  
- วนลูปแต่ละแถวของตารางที่ตรวจจับได้และพิมพ์ (หรือบันทึก) เนื้อหาของเซลล์  

ไม่มีบริการภายนอก ไม่มีกล่องดำเวทมนต์—ใช้แค่ Python ธรรมดาและไลบรารี OCR/layout ที่เป็นที่นิยม (เช่น **pdfplumber**, **pdfminer.six**, หรือ `engine` ที่คุณใช้แล้ว) หากคุณมีอ็อบเจกต์ `engine` ที่มีเมธอด `recognize_layout()` และ `run_postprocessor()` คุณก็สามารถนำโค้ดนี้ไปใช้ได้ทันที

> **Pro tip:** หากคุณใช้ SDK เชิงพาณิชย์ อย่าลืมเปิดฟีเจอร์ “table detection” มิฉะนั้น layout ดิบอาจพลาดเซลล์ที่รวมกันไว้

---

## ขั้นตอนที่ 1: ตรวจจับโครงสร้างตาราง – ดึงตารางจากเอกสาร

สิ่งแรกที่คุณต้องมีคือ layout ดิบที่บอกตำแหน่งของตารางบนหน้า PDF ไลบรารี PDF สมัยใหม่ส่วนใหญ่มีเมธอดเช่น `recognize_layout()` ที่คืนโครงสร้างแบบลำดับชั้นของบล็อก, เส้น, และเซลล์

```python
# Step 1 – Detect the document layout using the engine
# ---------------------------------------------------
# `engine` is assumed to be an instantiated object from your PDF library.
# It could be pdfplumber, a custom OCR SDK, or any tool that supports layout detection.
raw_layout = engine.recognize_layout()
```

**ทำไมสิ่งนี้ถึงสำคัญ:**  
layout ดิบให้พิกัดของทุกองค์ประกอบข้อความ แต่บ่อยครั้งจะมีสัญญาณรบกวน—เช่นหัวเรื่อง, ส่วนท้าย, หรืออักขระที่ไม่ได้เป็นส่วนของตาราง ดังนั้นขั้นตอนต่อไปจึงเป็นสิ่งจำเป็น

> **คำถามทั่วไป:** *ถ้า PDF ของฉันมีหลายหน้าเป็นอย่างไร?*  
> การเรียก `recognize_layout()` มักจะคืนรายการของอ็อบเจกต์หน้า ให้ลูปผ่านแต่ละหน้าและใช้ตรรกะ post‑processing เดียวกันกับทุกหน้า

---

## ขั้นตอนที่ 2: ปรับปรุงการตรวจจับ – วิธีอ่านตารางจาก pdf

หลังจากที่คุณได้ `raw_layout` แล้ว คุณควรทำความสะอาดมัน ไลบรารีส่วนใหญ่จะมี post‑processor ที่รวมเซลล์ที่แยกส่วน, ลบข้อความที่ไม่เกี่ยวข้อง, และสร้างอ็อบเจกต์ `Table` ที่สมบูรณ์

```python
# Step 2 – Refine the detected layout with the post‑processor
# ----------------------------------------------------------
# The post‑processor returns an enhanced layout where tables are
# represented as a list of rows, each row being a list of Cell objects.
enhanced_layout = engine.run_postprocessor(raw_layout)
```

**ทำไมต้องทำขั้นตอนนี้:**  
layout ดิบอาจรายงานแถวตารางเดียวเป็นหลายชิ้นส่วนเล็ก ๆ post‑processor จะจัดกลุ่มชิ้นส่วนเหล่านั้นเป็นเซลล์ที่มีความหมาย ทำให้การวนลูปในขั้นตอนต่อไปเป็นเรื่องง่าย

> **กรณีขอบ:** บาง PDF ใช้เส้นขอบที่มองไม่เห็น หากคุณพบแถวหายไป ให้เปิดฟีเจอร์ “detect invisible lines” ใน engine ของคุณ (ถ้ามี)

---

## ขั้นตอนที่ 3: วนลูปแถวของตาราง – วิธีวนลูปแถวของตาราง

เมื่อคุณมี `enhanced_layout` ที่สะอาดแล้ว การดึงข้อมูลก็ง่ายดาย ด้านล่างเป็นตัวอย่างการลูปผ่านแต่ละแถว, รวมข้อความของเซลล์ด้วยแท็บ (เพื่อให้ผลลัพธ์จัดแนวสวย) และพิมพ์ผลลัพธ์ คุณสามารถแทนที่ `print` ด้วยตรรกะการบันทึกอื่น ๆ เช่น CSV writer หรือการแทรกลงฐานข้อมูล

```python
# Step 3 – Print the table contents row by row
# --------------------------------------------
# `enhanced_layout.table` is expected to be an iterable of rows.
# Each `row` is a list of Cell objects with a `.text` attribute.
for row in enhanced_layout.table:
    # Join each cell's text with a tab to align columns
    print("\t".join(cell.text for cell in row))
```

**ผลลัพธ์ที่คาดหวัง (ตัวอย่าง):**

```
Item	Qty	Price	Total
Widget A	2	$10.00	$20.00
Widget B	1	$15.00	$15.00
Service C	5	$8.00	$40.00
```

หากต้องการ CSV แทนการแสดงผลแบบแท็บ ให้เปลี่ยน `"\t".join(...)` เป็น `",".join(...)` แล้วเขียนลงไฟล์

---

## ตัวอย่างทำงานเต็มรูปแบบ

รวมทุกส่วนเข้าด้วยกัน นี่คือสคริปต์ที่ทำงานได้เอง ปรับการ import และการสร้าง engine ให้ตรงกับไลบรารีที่คุณใช้

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

**สิ่งที่ต้องเปลี่ยน:**

- `initialize_engine(pdf_path)`: สร้างอินสแตนซ์ engine สำหรับไลบรารีที่คุณเลือก  
- `engine.recognize_layout()` / `engine.run_postprocessor()`: ใช้ชื่อเมธอดที่ถูกต้องหากแตกต่างกัน

รันสคริปต์ด้วย `python extract_table.py invoice.pdf` จะพิมพ์ตารางที่คั่นด้วยแท็บอย่างสวยงาม พร้อมสำหรับการประมวลผลต่อ

---

## ภาพประกอบ

ด้านล่างเป็นสเก็ตช์สั้น ๆ ของกระบวนการตรวจจับ  
![extract table from document diagram showing raw layout → post‑processor → clean table]  

*ข้อความแทนภาพ:* *แผนผังการไหลของการดึงตารางจากเอกสาร*  

---

## คำถามที่พบบ่อย & กรณีขอบ

| คำถาม | คำตอบ |
|----------|--------|
| **ถ้า PDF มีหลายตารางจะทำอย่างไร?** | `enhanced_layout.table` อาจมีเพียงตารางแรกที่ตรวจจับได้ ให้ลูปผ่าน `enhanced_layout.tables` (รูปพหูพจน์) หากไลบรารีรองรับ และใช้ตรรกะการวนลูปแถวกับแต่ละตาราง |
| **จะจัดการกับเซลล์ที่รวมกันได้อย่างไร?** | post‑processor ส่วนใหญ่จะขยายเซลล์ที่รวมเป็นรายการแยก หากไม่ทำ ให้ตรวจสอบ flag `merge_cells` ของ engine หรือรวมเซลล์ที่อยู่ติดกันด้วยการพิจารณาพิกัด |
| **สามารถดึงตารางจาก PDF ที่สแกนได้หรือไม่?** | ทำได้ แต่ต้องทำขั้นตอน OCR ก่อนการตรวจจับ layout หลาย SDK รวม OCR + layout detection ไว้ในเมธอดเดียว (`recognize_layout()` บนเอกสารสแกน) |
| **กังวลเรื่องประสิทธิภาพเมื่อประมวลผลจำนวนมาก?** | ประมวลผลหน้าแบบขนาน (เช่นใช้ `concurrent.futures`) ส่วนที่หนักคือ OCR; ควรเก็บ engine ไว้ใช้งานต่อเนื่องระหว่างไฟล์หลายไฟล์เพื่อหลีกเลี่ยงการโหลดโมเดลซ้ำ |
| **ต้องติดตั้ง dependencies เพิ่มหรือไม่?** | หากใช้ `pdfplumber` ให้ติดตั้งด้วย `pip install pdfplumber` ส่วน SDK เชิงพาณิชย์ให้ปฏิบัติตามคู่มือการติดตั้งของผู้ขาย |

---

## สรุป

เราได้แสดงวิธี **ดึงตารางจากเอกสาร** ด้วยการตรวจจับ layout, ปรับปรุงให้สะอาด, แล้ว **วนลูปแถวของตาราง** เพื่อให้ได้ข้อมูลที่พร้อมใช้งาน ไม่ว่าคุณจะส่งต่อไปยัง data‑warehouse, สร้างรายงาน, หรือแปลง PDF เป็น CSV กระบวนการก็ยังคงเหมือนเดิม: ตรวจจับ → ทำความสะอาด → วนลูป

ขั้นตอนต่อไปที่คุณอาจสนใจ:

- **วิธีอ่านตารางจาก pdf** พร้อมข้อมูลสไตล์ (ฟอนต์, สี) เพิ่มเติม  
- ส่งออกโดยตรงเป็น **pandas DataFrames** เพื่อการวิเคราะห์  
- ใช้ pipeline เดียวกันเพื่อ **เขียนตารางกลับเข้า PDF** (กระบวนการย้อนกลับ)  

ลองใช้สคริปต์กับ PDF ของคุณเองและดูว่าคุณสามารถเปลี่ยนตารางคงที่ให้เป็นข้อมูลที่นำไปใช้ได้เร็วแค่ไหน ขอให้สนุกกับการดึงข้อมูล!  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}