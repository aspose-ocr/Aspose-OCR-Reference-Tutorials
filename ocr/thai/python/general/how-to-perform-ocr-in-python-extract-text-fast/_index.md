---
category: general
date: 2026-03-26
description: เรียนรู้วิธีทำ OCR ด้วย Python และดึงข้อความจากภาพได้อย่างง่ายดาย อ่านข้อความจากการสแกน
  หรือดึงข้อความจากใบแจ้งหนี้โดยใช้ OcrEngine อย่างง่าย
draft: false
keywords:
- how to perform OCR
- extract text from image
- read text from scan
- extract text from invoice
- how to use OCR
language: th
og_description: ทำ OCR ด้วย Python อย่างไร? คู่มือนี้จะแสดงวิธีดึงข้อความจากภาพ, อ่านข้อความจากการสแกน,
  และดึงข้อความจากใบแจ้งหนี้ภายในไม่กี่นาที.
og_title: วิธีทำ OCR ด้วย Python – ดึงข้อความอย่างรวดเร็ว
tags:
- OCR
- Python
- Image Processing
title: วิธีทำ OCR ด้วย Python – ดึงข้อความอย่างรวดเร็ว
url: /th/python/general/how-to-perform-ocr-in-python-extract-text-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีทำ OCR ใน Python – ดึงข้อความอย่างรวดเร็ว

เคยสงสัยไหมว่า **how to perform OCR** บนใบเสร็จสแกนหรือ PDF ที่เบลอ? คุณไม่ได้เป็นคนเดียว ในหลายโครงการความต้องการ **extract text from image** ปรากฏขึ้นเร็วกว่าเดิมและวิธี “hand‑type everything” ปกติไม่สามารถขยายได้  

ในบทแนะนำนี้คุณจะได้เห็นตัวอย่างที่สมบูรณ์พร้อมรันที่แสดง **how to use OCR** เพื่ออ่านข้อความจากการสแกน ดึงข้อมูลจากใบแจ้งหนี้ และแม้กระทั่งจัดการการแก้ไขการเอียงอัตโนมัติ—ทั้งหมดด้วยเพียงไม่กี่บรรทัดของ Python.

## สิ่งที่คุณจะได้เรียนรู้

* การพึ่งพาและการ import ที่จำเป็นอย่างแม่นยำ
* วิธีสร้างและกำหนดค่าอินสแตนซ์ของ `OcrEngine`
* วิธี **extract text from image**, **read text from scan**, และ **extract text from invoice** ด้วยเอนจินเดียวกัน
* ข้อผิดพลาดทั่วไป (ภาษาไม่ถูกต้อง, ไฟล์หาย, ภาพขนาดใหญ่) และวิธีหลีกเลี่ยง
* ผลลัพธ์ที่คาดหวังเพื่อให้คุณตรวจสอบว่า OCR ทำงานสำเร็จ

ไม่จำเป็นต้องมีลิงก์เอกสารภายนอก—ทุกอย่างอยู่ในตัวเอง ดังนั้นคุณสามารถคัดลอก‑วางโค้ดและดูผลลัพธ์ได้ทันที.

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะลงลึก ตรวจสอบให้แน่ใจว่าคุณมี:

* ติดตั้ง Python 3.8+ (แพคเกจ `ocr` ทำงานได้กับเวอร์ชันล่าสุดใดก็ได้).
* ไลบรารี `ocr` พร้อมใช้งาน (`pip install ocr‑engine` – แทนที่ด้วยชื่อแพคเกจจริงหากแตกต่าง).
* ไฟล์รูปภาพที่คุณต้องการประมวลผล – สำหรับการสาธิตเราจะใช้ `invoice.png` ที่อยู่ในโฟลเดอร์ชื่อ `YOUR_DIRECTORY`.

แค่นั้นเอง หากคุณมีทั้งหมดแล้ว คุณพร้อมเริ่มทำงาน.

## ขั้นตอน 1: ติดตั้งและนำเข้าโมดูล OCR

สิ่งแรกที่ต้องทำคือ: เราต้องการไลบรารี OCR หากคุณยังไม่ได้ติดตั้ง ให้รันคำสั่งต่อไปนี้ในเทอร์มินัลของคุณ:

```bash
pip install ocr-engine
```

ต่อไปเรานำเข้าโมดูลในสคริปต์ของเรา

```python
# Step 1: Import the OCR module
import ocr
```

> **Pro tip:** รักษาสภาพแวดล้อมเสมือนของคุณให้เป็นระเบียบ; มันช่วยป้องกันการชนกันของเวอร์ชันเมื่อคุณเพิ่มแพคเกจการประมวลผลภาพอื่น ๆ ในภายหลัง.

## ขั้นตอน 2: สร้างและกำหนดค่า OCR Engine

การสร้างเอนจินนั้นง่ายเพียงเรียกคอนสตรัคเตอร์ของมัน แต่พลังที่แท้จริงอยู่ที่การกำหนดค่าอย่างถูกต้อง เราจะตั้งค่าภาษาเป็น English และเปิดการแก้ไขการเอียงอัตโนมัติ ซึ่งจำเป็นเมื่อจัดการกับใบแจ้งหนี้ที่สแกนแล้วที่ไม่ได้จัดเรียงอย่างสมบูรณ์

```python
# Step 2: Create an OCR engine instance
engine = ocr.OcrEngine()

# Step 3: Configure the engine – set language and enable automatic skew correction
engine.language = ocr.Language.English   # any supported language, e.g., Spanish, French
engine.auto_skew = True                 # fixes tilted scans automatically
```

ทำไมต้องเปิด `auto_skew`? เครื่องสแกนหลายเครื่องสร้างภาพที่เอียงไม่กี่องศา หากไม่มีการแก้ไข เอนจินอาจพลาดอักขระ ทำให้ใบแจ้งหนี้ที่อ่านได้ชัดกลายเป็นข้อความไร้สาระ.

## ขั้นตอน 3: ทำ OCR บนภาพเป้าหมายของคุณ

ตอนนี้เรานำไฟล์ภาพเข้าสู่เอนจิน เมธอด `recognize_image` จะคืนค่าอ็อบเจ็กต์ที่เก็บข้อความดิบและคะแนนความมั่นใจ (หากไลบรารีให้)

```python
# Step 4: Perform OCR on the target image
ocr_result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
```

หากคุณทำงานในสถานการณ์ **read text from scan** เพียงเปลี่ยนเส้นทางเป็น PDF ที่สแกนแล้วแปลงเป็น PNG หรือ JPEG การเรียกเดียวกันทำงานกับรูปแบบภาพใด ๆ ที่ไลบรารีรองรับ.

## ขั้นตอน 4: ตรวจสอบและใช้ข้อความที่สกัดออกมา

มาพิมพ์ผลลัพธ์ OCR ดิบกันดู ในกระบวนการประมวลผลใบแจ้งหนี้จริง ๆ คุณอาจจะต้องแยกวิเคราะห์สตริงนี้ ดึงรายการ, ยอดรวม, และวันที่ แต่ตอนนี้การมองอย่างรวดเร็วจะยืนยันว่า OCR ทำงานสำเร็จ

```python
# Step 5: Display the raw extracted text
print("Raw OCR text:\n", ocr_result.text)
```

**Expected output (truncated for brevity):**

```
Raw OCR text:
 Invoice #12345
 Date: 2026‑03‑01
 Bill To: Acme Corp.
 Item          Qty   Price   Total
 ------------------------------------------------
 Widget A      10    5.00    50.00
 Widget B      5     12.00   60.00
 ------------------------------------------------
 Subtotal:                     110.00
 Tax (5%):                     5.50
 Grand Total:                  115.50
```

หากผลลัพธ์ดูเป็นอักขระผสมกัน ให้ตรวจสอบอีกครั้งว่าภาพชัดเจนและ `engine.language` ตรงกับภาษาของเอกสาร.

## ขั้นตอน 5: จัดการกับกรณีขอบที่พบบ่อย

### ภาพขนาดใหญ่

การประมวลผลสแกนขนาด 5000 × 5000 พิกเซลอาจใช้หน่วยความจำมาก วิธีที่เร็วในการลดผลกระทบคือการย่อขนาดภาพก่อนส่งไปยังเอนจิน:

```python
from PIL import Image

def load_and_resize(path, max_dim=2000):
    img = Image.open(path)
    img.thumbnail((max_dim, max_dim), Image.ANTIALIAS)
    return img

scaled_image = load_and_resize("YOUR_DIRECTORY/invoice.png")
ocr_result = engine.recognize_image(scaled_image)
```

### หลายภาษา

หากคุณต้องการ **extract text from image** ที่มีทั้งภาษา English และ Spanish คุณสามารถตั้งค่ารายการภาษาดังนี้:

```python
engine.language = [ocr.Language.English, ocr.Language.Spanish]
```

เอนจินจะพยายามจำแนกอักขระจากทั้งสองชุด.

### การจัดการข้อผิดพลาด

อย่าสมมติว่าไฟล์มีอยู่เสมอ ห่อการเรียกในบล็อก try‑except เพื่อให้ข้อความที่เป็นมิตร:

```python
try:
    ocr_result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
    print("OCR succeeded!")
except FileNotFoundError:
    print("Error: The image file was not found. Check the path and try again.")
except ocr.OcrError as e:
    print(f"OCR failed with error: {e}")
```

## ตัวอย่างภาพอ้างอิง

ด้านล่างเป็นภาพหน้าจอของใบแจ้งหนี้ตัวอย่างที่เราใช้ในสาธิต สังเกตการเอียงเล็กน้อย—สิ่งที่ `auto_skew` แก้ไข

![how to perform OCR on an invoice](/images/ocr-example.png)

*Alt text:* วิธีทำ OCR บนภาพใบแจ้งหนี้ที่แสดงการแก้ไขการเอียงอัตโนมัติ.

## ตัวอย่างเต็มที่สามารถรันได้

เมื่อนำทุกอย่างมารวมกัน นี่คือสคริปต์เดียวที่คุณสามารถรันจากบรรทัดคำสั่ง มันครอบคลุมการติดตั้ง, การกำหนดค่า, การจัดการข้อผิดพลาด, และขั้นตอนการประมวลผลหลังอย่างง่ายที่เขียนข้อความที่สกัดลงไฟล์ชื่อ `output.txt`.

```python
# full_ocr_demo.py
# -------------------------------------------------
# Demonstrates how to perform OCR, extract text from image,
# read text from scan, and extract text from invoice.
# -------------------------------------------------

import ocr
from pathlib import Path

def main(image_path: str, output_path: str = "output.txt"):
    # Create and configure the engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.English
    engine.auto_skew = True

    # Verify the image exists
    if not Path(image_path).is_file():
        print(f"❌  Image not found: {image_path}")
        return

    # Run OCR
    try:
        result = engine.recognize_image(image_path)
    except ocr.OcrError as err:
        print(f"❌  OCR failed: {err}")
        return

    # Output the raw text
    print("✅  OCR completed. Raw text:")
    print(result.text)

    # Save to a text file for later processing
    Path(output_path).write_text(result.text, encoding="utf-8")
    print(f"💾  Text saved to {output_path}")

if __name__ == "__main__":
    # Replace with your actual file location
    main("YOUR_DIRECTORY/invoice.png")
```

การรัน `python full_ocr_demo.py` จะพิมพ์ข้อความที่สกัดลงคอนโซลและบันทึกไว้ใน `output.txt`. จากนั้นคุณสามารถใช้ regular expressions, CSV writers, หรือตรรกะอื่น ๆ ที่คุณต้องการสำหรับการทำ **extract text from invoice** automation.

## สรุป

ตอนนี้คุณมีคำตอบที่ครบถ้วนจากต้นจนจบสำหรับ **how to perform OCR** ใน Python ด้วยการสร้าง `OcrEngine`, กำหนดค่าภาษาและการแก้ไขการเอียง, และจัดการกับกรณีขอบที่ใช้งานได้จริง คุณสามารถ **extract text from image**, **read text from scan**, และ **extract text from invoice** อย่างเชื่อถือได้โดยไม่ต้องค้นหาเอกสารกระ散

ต่อไปคืออะไร? ลองป้อนไฟล์หลายไฟล์ในลูป, ทดลองกับภาษาต่าง ๆ, หรือเชื่อมต่อผลลัพธ์กับไลบรารีการสร้าง PDF เพื่อสร้าง PDF ที่ค้นหาได้ ความเป็นไปได้ไม่มีขีดจำกัด และโค้ดที่คุณเพิ่งเห็นเป็นฐานที่มั่นคง

มีคำถามเกี่ยวกับรูปแบบไฟล์เฉพาะหรืออยากปรับค่าเกณฑ์ความมั่นใจ? แสดงความคิดเห็นด้านล่าง—ยินดีช่วยคุณปรับแต่ง pipeline OCR ของคุณ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}