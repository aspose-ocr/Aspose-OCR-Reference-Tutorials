---
category: general
date: 2026-03-26
description: ดึงตารางจากภาพและแปลงภาพเป็นสเปรดชีตโดยใช้ Python OCR. เรียนรู้วิธีโหลดภาพสำหรับ
  OCR, อ่านตารางและดึงข้อมูลตาราง.
draft: false
keywords:
- extract tables from image
- convert image to spreadsheet
- load image for ocr
- ocr read tables
- ocr extract table data
language: th
og_description: ดึงตารางจากภาพด้วย Python OCR คู่มือนี้แสดงวิธีโหลดภาพสำหรับ OCR,
  อ่านตาราง, และแปลงเป็นสเปรดชีต.
og_title: สกัดตารางจากภาพ – บทเรียน OCR ฉบับสมบูรณ์
tags:
- OCR
- Python
- Data Extraction
title: ดึงตารางจากภาพ – คู่มือ OCR ทีละขั้นตอน
url: /th/python-java/general/extract-tables-from-image-step-by-step-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สกัดตารางจากรูปภาพ – คู่มือ OCR ฉบับสมบูรณ์

เคยต้อง **สกัดตารางจากรูปภาพ** แต่ไม่รู้จะเริ่มต้นอย่างไรหรือไม่? คุณไม่ได้อยู่คนเดียว นักพัฒนาหลายคนเจออุปสรรคเมื่อ PDF หรือสกรีนช็อตมีข้อมูลในรูปแบบตารางที่ต้องการแปลงเป็นแถวและคอลัมน์ที่แก้ไขได้ ข่าวดีคือ? เพียงไม่กี่บรรทัดของโค้ด Python ร่วมกับ OCR engine ที่แข็งแรงก็สามารถเปลี่ยนรูปภาพนั้นให้เป็นสเปรดชีตที่ใช้ได้ภายในไม่กี่วินาที

ในบทเรียนนี้เราจะเดินผ่านขั้นตอนการโหลดรูปภาพสำหรับ OCR, รัน engine เพื่อทำการจดจำ, แล้วดึงข้อมูลตารางออกมาเป็นแถว‑ต่อ‑แถว เมื่อเสร็จคุณจะสามารถ **แปลงรูปภาพเป็นสเปรดชีต** ได้ และคุณจะได้เห็นวิธี **ocr read tables** และ **ocr extract table data** สำหรับการประมวลผลต่อไป ไม่มีเวทมนตร์ลับ แค่โค้ดที่ชัดเจนและรันได้ที่คุณสามารถนำไปใช้ในโปรเจกต์ของคุณได้ทันที

---

## สิ่งที่คุณต้องเตรียม

ก่อนที่เราจะลงลึก ให้แน่ใจว่าคุณมีสิ่งต่อไปนี้พร้อมใช้งาน:

- **Python 3.9+** – เวอร์ชันล่าสุดที่เสถียรทำงานได้ดีที่สุด
- ไลบรารี **`ocr`** (หรือ SDK OCR ที่เข้ากันได้ซึ่งเปิดให้ใช้ `OcrEngine`, `Image` และเมธอดที่เกี่ยวกับตาราง) ติดตั้งด้วย `pip install ocr‑sdk` (เปลี่ยนเป็นชื่อแพคเกจจริง)
- ไฟล์รูปภาพ (`.png`, `.jpg`, ฯลฯ) ที่มีตารางพิมพ์อย่างชัดเจน  
- ตัวเลือก: **pandas** หากคุณต้องการเขียนข้อมูลที่สกัดออกมาโดยตรงเป็นไฟล์ CSV หรือ Excel (`pip install pandas`)

ทุกอย่างพร้อมหรือยัง? ดีมาก—มาเริ่มกันเลย

---

## ขั้นตอนที่ 1: นำเข้า OCR SDK และเตรียมสภาพแวดล้อมของคุณ

สิ่งแรกที่ต้องทำคือ นำคลาสของ OCR เข้ามาในสคริปต์และตั้งค่า helper เล็ก ๆ ที่จะเปลี่ยนข้อมูลตารางดิบให้เป็น DataFrame

```python
# Step 1 – Imports and basic setup
import ocr                     # The OCR SDK
from pathlib import Path      # Handy for file paths
import pandas as pd           # For converting tables to spreadsheets

# Optional: configure logging to see what the engine is doing
import logging
logging.basicConfig(level=logging.INFO)
```

**ทำไมต้องทำเช่นนี้:** การนำเข้า `ocr` ทำให้เรามีสิทธิ์เข้าถึง `OcrEngine`, `Imaging.Image` และอ็อบเจกต์ตารางที่เราจะวนลูป `pandas` ไม่จำเป็นสำหรับการสกัดข้อมูล แต่ช่วยให้ขั้นตอน **แปลงรูปภาพเป็นสเปรดชีต** ง่ายดายมากขึ้น

---

## ขั้นตอนที่ 2: โหลดรูปภาพที่ต้องการประมวลผล

ต่อไปเราจะ **โหลดรูปภาพสำหรับ OCR** SDK ต้องการอ็อบเจกต์ `Image` ดังนั้นเราจะห่อพาธไฟล์ด้วยเมธอดช่วย `Image.load()`

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

**เคล็ดลับ:** เก็บไฟล์รูปภาพไว้ในโฟลเดอร์เฉพาะ (`assets/` หรือ `data/`) แล้วใช้พาธแบบ relative วิธีนี้สคริปต์จะพกพาได้ง่ายบนเครื่องต่าง ๆ

---

## ขั้นตอนที่ 3: รันกระบวนการจดจำ

เมื่อแนบรูปภาพแล้ว เราก็สามารถบอก engine ให้ **ocr read tables** ได้แล้ว การเรียก `recognize()` จะคืนอ็อบเจกต์ผลลัพธ์ที่บรรจุทุกอย่างที่ engine ค้นพบ—บล็อกข้อความ, เส้น, และที่สำคัญที่สุดคือตาราง

```python
# Step 3 – Perform OCR and obtain results
ocr_result = ocr_engine.recognize()

# Quick sanity check: did the engine find any tables?
if not ocr_result.get_tables():
    logging.warning("No tables detected in the image.")
else:
    logging.info(f"Found {len(ocr_result.get_tables())} table(s).")
```

**ทำไมต้องตรวจสอบ:** รูปภาพบางรูปอาจมีสัญญาณรบกวนหรือเส้นขอบตารางจาง ทำให้ engine พลาด การบันทึกคำเตือนจะให้ฟีดแบ็กตั้งแต่ต้นโดยไม่ทำให้สคริปต์หยุดทำงาน

---

## ขั้นตอนที่ 4: สกัดแถวและเซลล์ของแต่ละตาราง

นี่คือจุดที่ “เวทมนตร์” เกิดขึ้น เราจะวนลูปทุกตารางที่ตรวจจับได้ ดึงแต่ละแถว แล้วดึงข้อความของแต่ละเซลล์ การใช้ list comprehension ภายในทำให้โค้ดกระชับ แต่เราจะอธิบายขั้นตอนให้เข้าใจ

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

**กำลังเกิดอะไรขึ้น?**  

- `enumerate(..., start=1)` ให้หมายเลขตารางที่เป็นมิตรสำหรับการล็อก  
- `row_obj.get_cells()` คืนอ็อบเจกต์เซลล์แต่ละอัน; `cell.get_text()` ดึงสตริงที่ OCR ถอดรหัสได้  
- เราเก็บแถวไว้ใน `rows_data` แล้วส่งต่อให้ `pandas.DataFrame` ซึ่งจัดคอลัมน์ให้โดยอัตโนมัติ  
- บล็อก `print` แสดง **ผลลัพธ์สำคัญ** ตามตัวอย่างในสคริปต์ต้นฉบับ เพื่อให้คุณตรวจสอบผลได้ทันที

**การจัดการกรณีขอบ:** หากแถวหนึ่งมีจำนวนเซลล์ต่างจากแถวอื่น `pandas` จะเติมค่า `NaN` ให้ช่องที่ขาด คุณสามารถทำความสะอาด DataFrame ด้วย `df.fillna('')` หากต้องการให้เป็นสตริงว่าง

---

## ขั้นตอนที่ 5: บันทึกตารางที่สกัดเป็นสเปรดชีต

เมื่อเรามีรายการ DataFrames แล้ว การแปลงเป็นไฟล์ Excel (หรือ CSV) ทำได้ง่ายมาก สิ่งนี้ตอบโจทย์เป้าหมาย **แปลงรูปภาพเป็นสเปรดชีต** ของเรา

```python
# Step 5 – Export tables to Excel (one sheet per table)
output_path = Path("extracted_tables.xlsx")
with pd.ExcelWriter(output_path, engine="openpyxl") as writer:
    for idx, df in enumerate(all_tables, start=1):
        sheet_name = f"Table_{idx}"
        df.to_excel(writer, sheet_name=sheet_name, index=False)

logging.info(f"All tables saved to {output_path}")
```

**ทำไมต้องเป็น Excel?** ผู้ใช้ธุรกิจส่วนใหญ่ชอบ `.xlsx` หากคุณต้องการ CSV เพียงเปลี่ยนลูปเป็น `df.to_csv(f"table_{idx}.csv", index=False)`

---

## สคริปต์เต็มพร้อมรัน

รวมทุกส่วนเข้าด้วยกัน นี่คือโปรแกรมสมบูรณ์ที่คุณสามารถคัดลอก‑วางและรันได้

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

**ผลลัพธ์ที่คาดว่าจะเห็นในคอนโซล** (สมมติว่าตารางเป็น 2×3):

```
=== New Table ===
Header1    Header2    Header3
Row1Col1   Row1Col2   Row1Col3
Row2Col1   Row2Col2   Row2Col3
```

และคุณจะพบไฟล์ `extracted_tables.xlsx` อยู่ในโฟลเดอร์ของสคริปต์ โดยแต่ละตารางจะอยู่บนชีตแยกกัน

---

## คำถามที่พบบ่อย & เคล็ดลับ

| คำถาม | คำตอบ |
|----------|--------|
| **สามารถใช้ไลบรารี OCR ตัวอื่นได้หรือไม่?** | ได้เลย รูปแบบการทำงานยังคงเหมือนเดิม: โหลดรูปภาพ → จดจำ → วนลูป `get_tables()` เพียงเปลี่ยนการนำเข้าและชื่ออ็อบเจกต์ |
| **ถ้ารูปภาพของฉันมีสัญญาณรบกวนล่ะ?** | ทำการพรี‑โปรเซสด้วย OpenCV (thresholding, deskew) ก่อนส่งให้ OCR การลดสัญญาณรบกวนมักช่วยเพิ่มความแม่นยำของ **ocr extract table data** |
| **ต้องติดตั้ง `openpyxl` หรือไม่?** | ต้องการ `pandas` ใช้มันเป็น backend สำหรับการส่งออกเป็น Excel ติดตั้งด้วย `pip install openpyxl` |
| **จะจัดการกับเซลล์ที่รวมกันได้อย่างไร?** | SDK บางตัวให้ `cell.is_merged()` คุณสามารถตรวจจับและกระจายค่าดังกล่าวไปยังช่วงที่รวมด้วยตนเอง |
| **มีวิธีสกัดเฉพาะตารางที่ต้องการหรือไม่?** | สามารถกรองด้วย `table_obj.get_confidence()` หรือเช็คคีย์เวิร์ดในหัวตารางก่อนประมวลผล |

---

## สรุป

คุณได้มีโซลูชันครบวงจรจากต้นจนจบสำหรับ **สกัดตารางจากรูปภาพ**, แปลงผลลัพธ์เป็นสเปรดชีตที่เรียบร้อย, และแม้กระทั่งจัดการหลายตารางในภาพเดียว สคริปต์นี้สาธิตวิธี **โหลดรูปภาพสำหรับ OCR**, **ocr read tables**, และ **ocr extract table data** พร้อมความยืดหยุ่นสำหรับการปรับใช้ในสถานการณ์จริง

ต่อไปคุณจะลองใช้ OCR กับหน้า PDF ที่แปลงเป็นรูปภาพ, ทดลองกับภาษาและฟอนต์ต่าง ๆ หรือแม้กระทั่งส่ง DataFrames ตรงเข้าสู่ฐานข้อมูลหรือเครื่องมือรายงาน—จินตนาการของคุณคือขีดจำกัด

หากคุณพบว่าคู่มือนี้เป็นประโยชน์ อย่าลืมแชร์, กดดาวที่รีโพซิทอรีของ SDK, หรือแสดงความคิดเห็นพร้อมเทคนิคของคุณเอง ขอให้เขียนโค้ดอย่างสนุกสนานและตารางของคุณถูกแยกข้อมูลอย่างสมบูรณ์!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}