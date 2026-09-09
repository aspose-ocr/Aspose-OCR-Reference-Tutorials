---
category: general
date: 2026-01-12
description: บทเรียน OCR ด้วย Python แสดงวิธีดึงข้อความตารางจากภาพ เรียนรู้การอ่านตารางจากภาพและดึงข้อความที่เลือกด้วย
  Aspose OCR.
draft: false
keywords:
- python ocr tutorial
- extract table text
- read table from image
- extract selected text
- how to extract table
language: th
og_description: บทเรียน OCR ด้วย Python ที่สอนวิธีดึงข้อความตารางจากภาพ, อ่านตารางจากภาพและดึงข้อความที่เลือกโดยใช้
  Aspose OCR.
og_title: 'บทเรียน OCR ด้วย Python: การดึงข้อความตารางจากรูปภาพ'
tags:
- OCR
- Python
- AsposeOCR
title: 'บทเรียน OCR ด้วย Python: ดึงข้อความตารางจากรูปภาพ'
url: /th/python-java/general/python-ocr-tutorial-extract-table-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# บทแนะนำ Python OCR: ดึงข้อความตารางจากรูปภาพ

เคยต้องการ **python ocr tutorial** ที่จริงจังแสดงวิธีดึงตารางออกจากแบบฟอร์มที่สแกนหรือไม่? คุณไม่ได้เป็นคนเดียว ส่วนใหญ่ของบทแนะนำจะหยุดที่การดึงข้อความทั่วไป ทำให้คุณต้องเดาว่าจะแยกกริดข้อมูลที่ต้องการอย่างไร  

ในคู่มือนี้ เราจะพาคุณผ่านสถานการณ์จริง: อ่านตารางจากรูปภาพ, ดึงข้อความที่เลือกที่คุณต้องการเท่านั้น, และสุดท้ายพิมพ์ผลลัพธ์ ระหว่างทางเราจะเพิ่มเคล็ดลับเกี่ยวกับ **how to extract table** อย่างเชื่อถือได้ เพื่อให้คุณไม่ต้องสร้างใหม่ทุกครั้ง

## สิ่งที่คุณจะได้เรียนรู้

- วิธีตั้งค่า Aspose OCR สำหรับ Python.
- วิธีกำหนดพื้นที่สี่เหลี่ยมที่มีตาราง.
- ขั้นตอนที่แน่นอนเพื่อ **extract table text** และ **read table from image**.
- เคล็ดลับในการจัดการหลายภาษา หรือรูปแบบตารางที่ไม่เป็นระเบียบ.
- สคริปต์ที่สมบูรณ์และสามารถรันได้ที่คุณสามารถนำไปใช้ในโปรเจคของคุณวันนี้.

**ข้อกำหนดเบื้องต้น**  
- Python 3.8 หรือใหม่กว่า.  
- ความคุ้นเคยพื้นฐานกับแนวคิด OCR (ไม่จำเป็นต้องเชี่ยวชาญลึก).  
- รูปภาพ PNG หรือ JPEG ที่มีตารางชัดเจน (เราจะเรียกมันว่า `form_with_table.png`).  

ถ้าคุณมีทั้งหมดนี้แล้ว, มาเริ่มกันเลย—ไม่มีเรื่องฟุ่มเฟือย, มีโค้ดที่ทำได้จริงเท่านั้น

![python ocr tutorial example of table region](table_region_example.png){alt="python ocr tutorial ตัวอย่างแสดงพื้นที่ตาราง"}

## ขั้นตอนที่ 1: ติดตั้งและนำเข้า Aspose OCR

สิ่งแรกที่ต้องทำ: คุณต้องการไลบรารี Aspose OCR แพคเกจนี้อยู่บน PyPI ดังนั้นคำสั่ง `pip` เพียงหนึ่งคำสั่งก็ทำได้

```bash
pip install aspose-ocr
```

ต่อไปให้นำเข้ามอดูลและตัวช่วยใด ๆ ที่คุณต้องการ

```python
# Step 1: Import the Aspose OCR package
import asposeocr as ocr
```

*เคล็ดลับ:* เก็บ dependencies ของคุณในไฟล์ `requirements.txt` จะทำให้การสร้างสภาพแวดล้อมซ้ำง่ายมาก

## ขั้นตอนที่ 2: เริ่มต้น OCR Engine (Python OCR Tutorial Core)

การสร้าง engine คือหัวใจของ **python ocr tutorial** ใด ๆ ที่นี่เรายังตั้งค่าภาษาเริ่มต้นเป็น English—คุณสามารถเปลี่ยนได้ในภายหลัง

```python
# Step 2: Create an OCR engine and set the default language
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

ทำไมต้องตั้งค่าภาษา? ความแม่นยำของ OCR สามารถเพิ่มขึ้นอย่างมากเมื่อ engine รู้ว่าตัวอักษรใดที่คาดหวัง หากคุณทำงานกับแบบฟอร์มหลายภาษา คุณสามารถตั้งค่ารายการภาษาหรือกำหนดทับต่อพื้นที่ (ดูต่อไป)

## ขั้นตอนที่ 3: โหลดรูปภาพของคุณ

Aspose OCR ทำงานกับรูปแบบภาพส่วนใหญ่ เพียงชี้ไปที่เส้นทางไฟล์ แล้วคุณจะได้อ็อบเจ็กต์ `Image` พร้อมสำหรับการประมวลผล

```python
# Step 3: Load the image that contains the form with the table
image_page = ocr.Image.load("YOUR_DIRECTORY/form_with_table.png")
```

*กรณีขอบ:* รูปภาพขนาดใหญ่ (มากกว่า 5 MB) อาจทำให้การประมวลผลช้าลง พิจารณาเปลี่ยนขนาดหรือบีบอัดก่อน OCR หากประสิทธิภาพเป็นปัญหา

## ขั้นตอนที่ 4: กำหนดพื้นที่ตาราง (Read Table from Image)

ต่อไปคือส่วนสนุก: บอก engine ว่า *ที่ไหน* ที่ตารางอยู่ คุณให้ `OcrRegion` พร้อม `Rectangle` (x, y, width, height) พิกัดเป็นหน่วยพิกเซล ดังนั้นคุณอาจต้องทดลองเล็กน้อย

```python
# Step 4: Define the rectangular area where the table is located
# (x, y, width, height) – adjust these values for your image
table_region = ocr.OcrRegion(
    image_page,
    ocr.Rectangle(120, 340, 800, 450)
)

# Optional: override language for this specific region
table_region.language = ocr.Language.ENGLISH
```

ทำไมต้องใช้พื้นที่? การจำกัด OCR เฉพาะพื้นที่ตารางทำให้เรา **extract selected text** เร็วขึ้นและหลีกเลี่ยงสัญญาณรบกวนจากป้ายหรือกราฟิกรอบ ๆ อีกทั้งยังเพิ่มความแม่นยำเพราะ engine สามารถโฟกัสที่เลย์เอาต์ที่สม่ำเสมอ

## ขั้นตอนที่ 5: รัน OCR บนพื้นที่ที่กำหนด

เมื่อกำหนดพื้นที่แล้ว เราเรียก `process_region` เมธอดนี้คืนค่าอ็อบเจ็กต์ `OcrResult` ที่บรรจุข้อความดิบ, คะแนนความเชื่อมั่น, และแม้แต่กล่องขอบเขตหากคุณต้องการในภายหลัง

```python
# Step 5: Run OCR only on the defined region
region_result = ocr_engine.process_region(table_region)
```

หากคุณต้องการดึงหลายตาราง เพียงทำซ้ำขั้นตอน 4‑5 ด้วยสี่เหลี่ยมต่าง ๆ

## ขั้นตอนที่ 6: แสดงผลข้อความตารางที่ดึงมา

สุดท้าย พิมพ์—หรือบันทึก—การแสดงผลข้อความของตาราง Aspose OCR คืนค่าข้อความธรรมดาพร้อมการขึ้นบรรทัดใหม่ที่มักสอดคล้องกับแถว ทำให้การประมวลผลต่อเนื่องง่าย

```python
# Step 6: Output the extracted table text
print("Table text:\n", region_result.text)
```

**ผลลัพธ์ที่คาดหวัง** (example):

```
Table text:
 Item        Qty   Price
 Apple       10    $1.20
 Banana      5     $0.80
 Orange      8     $1.00
```

คุณสามารถนำสตริงนี้ไปใช้กับตัวแยก `csv`, pandas DataFrames, หรือ pipeline การวิเคราะห์ต่อไปได้

## ตัวอย่างทำงานเต็มรูปแบบ

รวมทุกอย่างเข้าด้วยกัน นี่คือสคริปต์เต็มที่คุณสามารถรันได้ทันที แทนที่ `YOUR_DIRECTORY/form_with_table.png` ด้วยเส้นทางจริงของรูปภาพของคุณ

```python
# -*- coding: utf-8 -*-
"""
Python OCR Tutorial: Extract Table Text from Images
---------------------------------------------------
A self‑contained example that demonstrates how to read a table from an image
using Aspose OCR for Python.
"""

# Install the library first:
# pip install aspose-ocr

import asposeocr as ocr

def extract_table(image_path, rect):
    """
    Extracts text from a rectangular region that contains a table.

    :param image_path: Path to the PNG/JPEG image.
    :param rect: Tuple (x, y, width, height) defining the table region.
    :return: Plain‑text representation of the table.
    """
    # Initialise OCR engine with English language
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # Load the image
    img = ocr.Image.load(image_path)

    # Define the region (override language if needed)
    region = ocr.OcrRegion(img, ocr.Rectangle(*rect))
    region.language = ocr.Language.ENGLISH  # optional per‑region override

    # Process only this region
    result = engine.process_region(region)

    return result.text

if __name__ == "__main__":
    # Adjust these coordinates to match your table location
    table_rect = (120, 340, 800, 450)   # x, y, width, height

    # Path to your image file
    img_file = "YOUR_DIRECTORY/form_with_table.png"

    extracted_text = extract_table(img_file, table_rect)
    print("=== Extracted Table Text ===")
    print(extracted_text)
```

รันสคริปต์ด้วย `python extract_table.py` หากทุกอย่างตรงกัน คุณจะเห็นตารางพิมพ์บนคอนโซล

## คำถามทั่วไป & การจัดการกรณีขอบ

**ถ้าตารางไม่เป็นสี่เหลี่ยมที่สมบูรณ์?**  
คุณสามารถแบ่งตารางเป็นหลายพื้นที่ที่ทับซ้อนกันหรือใช้สี่เหลี่ยมใหญ่ที่ครอบคลุมทั้งพื้นที่แล้วทำการประมวลผลต่อข้อความ (เช่น แยกตามการขึ้นบรรทัดใหม่)

**ฉันสามารถดึงเฉพาะคอลัมน์ที่ต้องการได้ไหม?**  
หลังจากที่คุณมีข้อความตารางเต็ม ใช้ `csv` หรือ `pandas` ของ Python เพื่อตัดคอลัมน์ที่ต้องการ ขั้นตอน OCR เองจะคืนค่าทุกอย่างภายในสี่เหลี่ยม

**ฉันจะทำงานกับตารางที่ไม่ใช่ภาษาอังกฤษอย่างไร?**  
ตั้งค่า `ocr_engine.language` (หรือ `region.language`) ให้เป็น enum ที่เหมาะสม เช่น `ocr.Language.FRENCH` หรือรวมหลายภาษาโดยใช้ `ocr.Language.ENGLISH | ocr.Language.SPANISH`.

**มีวิธีใดบ้างที่จะได้กล่องขอบเขตของแต่ละเซลล์?**  
Aspose OCR สามารถคืนค่า `region_result.words` ซึ่งแต่ละคำมีกล่องขอบเขต คุณต้องแมปกล่องเหล่านั้นกลับเป็นกริด—มีประโยชน์สำหรับการวิเคราะห์เลย์เอาต์ขั้นสูง

## เคล็ดลับเพื่อความแม่นยำที่ดียิ่งขึ้น

- **Clean the image**: ทำการไบนารีหรือเพิ่มคอนทราสต์ก่อนส่งให้ OCR ไลบรารีอย่าง Pillow ช่วยได้
- **Avoid compression artifacts**: บันทึกการสแกนเป็น PNG เมื่อทำได้
- **Mind DPI**: 300 dpi เป็นค่าที่เหมาะสม; ค่าต่ำกว่าสามารถทำให้พลาดอักขระ
- **Test different rectangle sizes**: สี่เหลี่ยมที่ใหญ่กว่านิดหน่อยมักจะจับอักขระที่หลุดออกจากตารางได้

## ขั้นตอนต่อไป

ตอนนี้คุณได้เชี่ยวชาญการดึงข้อมูล **how to extract table** ด้วย Aspose OCR แล้ว คุณอาจสำรวจต่อไป:

- แปลงข้อความที่ดึงมาเป็นไฟล์ CSV ด้วยโมดูล `csv` ของ Python
- ส่งข้อมูลเข้า **pandas** DataFrame เพื่อการวิเคราะห์
- ใช้ OCR อ่านแบบฟอร์มที่เขียนด้วยมือ (ต้องใช้ engine ที่แตกต่างหรือการฝึกเพิ่มเติม)
- ทำอัตโนมัติการประมวลผลแบบแบตช์ของหลายสิบแบบฟอร์มสแกนโดยใช้ `for` loop ง่าย ๆ

แต่ละส่วนขยายเหล่านี้สร้างบนแนวคิดหลักที่ครอบคลุมใน **python ocr tutorial** นี้ ทำให้คุณพร้อมที่จะขยายขนาดได้

*ขอให้เขียนโค้ดอย่างสนุก! หากคุณเจอปัญหาใด ๆ ฝากคอมเมนต์ด้านล่าง—ฉันยินดีช่วยคุณปรับการดึงข้อมูล*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}