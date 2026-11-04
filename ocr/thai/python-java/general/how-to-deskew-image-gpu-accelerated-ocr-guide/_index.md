---
category: general
date: 2026-01-02
description: เรียนรู้วิธีการแก้ไขการเอียงของภาพและเพิ่มความคมชัดของภาพเพื่อให้ได้ข้อความธรรมดาอย่างรวดเร็ว
  รวมถึงโค้ด Python ทีละขั้นตอนและเคล็ดลับในการสกัดข้อความ
draft: false
keywords:
- how to deskew image
- boost image contrast
- get plain text
- how to boost contrast
- how to extract text
language: th
og_description: วิธีแก้การเอียงของภาพและเพิ่มคอนทราสต์เพื่อให้ได้ข้อความธรรมดา ตัวอย่าง
  Python เต็มรูปแบบพร้อมการดึงตารางและการเร่งด้วย GPU.
og_title: วิธีปรับแนวภาพ – บทเรียน OCR ด้วย GPU อย่างครบถ้วน
tags:
- OCR
- Python
- Image Processing
title: วิธีปรับแนวภาพ – คู่มือ OCR เร่งด้วย GPU
url: /th/python-java/general/how-to-deskew-image-gpu-accelerated-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีการ Deskew รูปภาพ – คู่มือ OCR เร่งความเร็วด้วย GPU

เคยสงสัย **วิธีการ deskew รูปภาพ** เมื่อใบเสร็จของคุณมุมเอียงแปลก ๆ ไหม? คุณไม่ได้อยู่คนเดียว; ภาพเอียงอาจทำให้ใบเสร็จที่อ่านได้ชัดเจนกลายเป็นข้อความสับสน ข่าวดีคือด้วยโค้ด Python เพียงไม่กี่บรรทัดคุณสามารถทำ auto‑deskew, เพิ่มคอนทราสต์, และดึงข้อความล้วนออกมาได้—ไม่ต้องใช้ Photoshop ด้วยตนเอง  

ในบทเรียนนี้เราจะเดินผ่านตัวอย่างที่สมบูรณ์และสามารถรันได้ ซึ่งไม่เพียงแค่ **วิธีการ deskew รูปภาพ** แต่ยังแสดง **วิธีการเพิ่มคอนทราสต์**, **วิธีการดึงข้อความล้วน**, และแม้กระทั่ง **วิธีการสกัดข้อความ** จากตารางที่เครื่อง OCR ค้นพบ เมื่อจบคุณจะได้สคริปต์ที่พร้อมใช้ในโปรเจกต์ใดก็ได้

## สิ่งที่คุณต้องเตรียม

- Python 3.9+ ติดตั้งแล้ว (โค้ดใช้ type hints จึงแนะนำให้ใช้ interpreter เวอร์ชันใหม่)
- ไลบรารี `ocr` ที่ให้ `OcrEngine`, `EngineMode`, `ImageProcessingOptions`, และ `OcrResult` (ติดตั้งด้วย `pip install ocr‑sdk` – แทนด้วยชื่อแพคเกจที่คุณใช้จริง)
- GPU ที่มีไดรเวอร์รองรับ หากต้องการความเร็วเพิ่ม (ไม่บังคับแต่แนะนำ)
- ไฟล์รูปภาพที่มีการหมุนเล็กน้อยหรือคอนทราสต์ต่ำ เช่น `receipt_skewed.jpg`

> **เคล็ดลับ:** หากคุณไม่มี GPU เพียงเปลี่ยน `EngineMode.GPU` เป็น `EngineMode.CPU` แล้วสคริปต์ก็ยังทำงานได้—แต่จะช้ากว่าเล็กน้อย

## การทำงานแบบขั้นตอน

ด้านล่างเราจะแบ่งวิธีแก้เป็นส่วน ๆ แต่ละส่วนมีหัวข้อ **H2** ที่บรรจุคีย์เวิร์ดหลัก *วิธีการ deskew รูปภาพ* หรือคีย์เวิร์ดรองอื่น ๆ โค้ดเต็มรูปแบบ มีคอมเมนต์และพร้อมรัน

### วิธีการ Deskew รูปภาพด้วย GPU‑Accelerated OCR

สิ่งแรกที่ทำคือบอกให้ OCR engine ทำงานบน GPU และเปิดฟีเจอร์ auto‑deskew ซึ่งจะวิเคราะห์เรขาคณิตของภาพและหมุนกลับให้ตรง

```python
# Import the required classes from the OCR SDK
from ocr import OcrEngine, EngineMode, ImageProcessingOptions, OcrResult

# Step 1: Initialize the OCR engine with GPU acceleration
ocr_engine = OcrEngine()
ocr_engine.set_engine_mode(EngineMode.GPU)  # Enables GPU backend for faster processing
```

> **ทำไมถึงสำคัญ:** การเร่งด้วย GPU สามารถลดเวลาประมวลผลจากวินาทีเป็นมิลลิวินาที ซึ่งจำเป็นเมื่อคุณต้องจัดการกับใบเสร็จหลายสิบใบต่อ นาที

### เพิ่มคอนทราสต์ของภาพเพื่อการจดจำที่ดียิ่งขึ้น

ใบเสร็จที่คอนทราสต์ต่ำเป็นอุจจาระสำหรับระบบ OCR ใด ๆ การเพิ่มคอนทราสต์ทำให้ขอบภาพชัดเจนขึ้นสำหรับ engine

```python
# Step 2: Configure image preprocessing (auto‑deskew and contrast boost)
processing_options = ImageProcessingOptions()
processing_options.set_auto_deskew(True)          # Corrects slight rotation
processing_options.set_contrast_boost(30)         # Improves readability
ocr_engine.set_image_processing_options(processing_options)
```

> **วิธีเพิ่มคอนทราสต์:** เมธอด `set_contrast_boost` รับค่าเป็นเปอร์เซ็นต์; 30 % เป็นค่าเริ่มต้นที่ปลอดภัยและทำงานได้กับใบเสร็จส่วนใหญ่ หากภาพของคุณมืดมากให้เพิ่มเป็น 50 % หรือทดลองปรับค่า

### ดึงข้อความล้วนจากภาพที่ผ่านการประมวลผลแล้ว

เมื่อภาพตรงและสว่าง เราจะส่งให้ engine และขอผลลัพธ์เป็นข้อความล้วน

```python
# Step 3: Load the target image and perform OCR
image_path = "YOUR_DIRECTORY/receipt_skewed.jpg"
ocr_result: OcrResult = ocr_engine.recognize_image(image_path)

# Step 4: Output the recognized plain text
print("Detected text:")
print(ocr_result.get_text())
```

**ผลลัพธ์ที่คาดหวัง** (ตัดบางส่วนเพื่อความกระชับ):

```
Detected text:
Store: Coffee Corner
Date: 2025-12-31
Item          Qty   Price
Latte          1    $3.50
Muffin         2    $5.00
Total                $8.50
```

> **วิธีดึงข้อความล้วน:** เมธอด `get_text()` จะลบข้อมูลเลย์เอาต์ทั้งหมดและคืนสตริงที่สะอาด คุณสามารถบันทึกลงฐานข้อมูล ส่งไปยัง API หรือใช้ต่อในระบบวิเคราะห์ได้

### วิธีการสกัดข้อความจากตารางที่ตรวจพบ

บ่อยครั้งที่ใบเสร็จมีข้อมูลเป็นตาราง (รายการ, จำนวน, ราคา) SDK OCR สามารถตรวจจับตารางและให้คุณวนลูปผ่านแถวและเซลล์ได้

```python
# Step 5: If tables are detected, print their contents
if ocr_result.get_tables():
    for idx, table in enumerate(ocr_result.get_tables()):
        print(f"\nTable {idx + 1}:")
        for row in table.get_rows():
            # Join each cell's text with a tab for easy copy‑paste
            print("\t".join(cell.get_text() for cell in row.get_cells()))
```

**ตัวอย่างผลลัพธ์ตาราง**:

```
Table 1:
Item	Qty	Price
Latte	1	$3.50
Muffin	2	$5.00
Total		$8.50
```

> **ทำไมต้องสกัดตาราง:** ข้อมูลเชิงโครงสร้างทำให้คำนวณยอดรวม, สร้างรายงาน, หรือส่งต่อไปยังซอฟต์แวร์บัญชีเป็นเรื่องง่าย

### สคริปต์ทำงานเต็มรูปแบบ

รวมทุกอย่างเข้าด้วยกัน นี่คือสคริปต์ที่คุณสามารถคัดลอก‑วางลงใน `deskew_and_ocr.py`:

```python
# deskew_and_ocr.py
from ocr import OcrEngine, EngineMode, ImageProcessingOptions, OcrResult

def main(image_path: str) -> None:
    # Initialize OCR engine with GPU acceleration
    ocr_engine = OcrEngine()
    ocr_engine.set_engine_mode(EngineMode.GPU)

    # Configure preprocessing: auto‑deskew + contrast boost
    opts = ImageProcessingOptions()
    opts.set_auto_deskew(True)
    opts.set_contrast_boost(30)  # Adjust if needed
    ocr_engine.set_image_processing_options(opts)

    # Perform OCR
    result: OcrResult = ocr_engine.recognize_image(image_path)

    # Print plain text
    print("Detected text:")
    print(result.get_text())

    # Print tables, if any
    if result.get_tables():
        for i, tbl in enumerate(result.get_tables(), start=1):
            print(f"\nTable {i}:")
            for row in tbl.get_rows():
                print("\t".join(cell.get_text() for cell in row.get_cells()))

if __name__ == "__main__":
    # Replace with your actual image location
    main("YOUR_DIRECTORY/receipt_skewed.jpg")
```

รันด้วยคำสั่ง:

```bash
python deskew_and_ocr.py
```

คุณจะเห็นข้อความที่ทำความสะอาดแล้วและตารางที่ตรวจพบแสดงบนคอนโซล

## กรณีขอบทั่วไป & วิธีจัดการ

| สถานการณ์ | วิธีทำ |
|-----------|--------|
| **ภาพกลับหัว** | เพิ่มความมั่นใจของ `set_auto_deskew(True)` ด้วยการเรียก `set_rotation_correction(True)` หาก SDK มีฟังก์ชันนี้ |
| **การเพิ่มคอนทราสต์ทำให้ภาพสว่างเกินไป** | ลดเปอร์เซ็นต์ที่ส่งให้ `set_contrast_boost` (เช่น 15 %) |
| **ไม่มี GPU** | เปลี่ยน `EngineMode.GPU` เป็น `EngineMode.CPU`; ส่วนอื่นของ pipeline ยังคงทำงานตามเดิม |
| **ตารางไม่ถูกตรวจจับ** | ลองสแกนด้วยความละเอียดสูงขึ้นหรือเปิด `set_table_detection(True)` หากไลบรารีรองรับ |

## ขั้นตอนต่อไป: จากข้อความล้วนสู่ข้อมูลเชิงโครงสร้าง

ตอนนี้คุณรู้ **วิธีการ deskew รูปภาพ**, **วิธีการเพิ่มคอนทราสต์**, และ **วิธีการดึงข้อความล้วน** แล้ว คุณอาจต้องการ:

- แยกข้อความล้วนด้วย regular expressions เพื่อดึงคู่ค่า key‑value (เช่น `total`, `date`)
- เก็บผลลัพธ์ในฐานข้อมูล SQLite หรือ PostgreSQL เพื่อใช้ในรายงานต่อไป
- เชื่อมสคริปต์เข้ากับฟังก์ชัน serverless (AWS Lambda, Azure Functions) เพื่อประมวลผลไฟล์อัปโหลดอัตโนมัติ

การต่อยอดทั้งหมดนี้อาศัยพื้นฐานเดียวกันที่เราได้อธิบายไว้ในบทนี้

## สรุป

เราได้อธิบาย **วิธีการ deskew รูปภาพ** ด้วย OCR ที่เร่งด้วย GPU, แสดง **วิธีการเพิ่มคอนทราสต์** เพื่อการจดจำที่คมชัด, สาธิต **วิธีการดึงข้อความล้วน** อย่างแม่นยำ, และแม้กระทั่ง **วิธีการสกัดข้อความ** จากตาราง สคริปต์ที่สมบูรณ์และรันได้เต็มรูปแบบเชื่อมทุกขั้นตอนเข้าด้วยกัน ทำให้คุณสามารถนำไปใส่ในโปรเจกต์ Python ใดก็ได้และเริ่มดึงข้อมูลที่สะอาดจากภาพเอียงหรือคอนทราสต์ต่ำได้ทันที

ลองใช้กับใบเสร็จของคุณเอง ปรับระดับคอนทราสต์ตามต้องการ แล้วปล่อยให้ OCR ทำงานหนัก หากเจอปัญหาให้กลับไปดูตารางกรณีขอบด้านบน—ส่วนใหญ่แก้ได้ด้วยการปรับค่าเล็กน้อย

ขอให้สนุกกับการเขียนโค้ด และขอให้ภาพของคุณตรงและสว่างเสมอ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}