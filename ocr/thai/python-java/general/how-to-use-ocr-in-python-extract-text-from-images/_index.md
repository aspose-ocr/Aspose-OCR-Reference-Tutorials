---
category: general
date: 2026-06-16
description: วิธีใช้ OCR ใน Python เพื่อดึงข้อความจากไฟล์ภาพเช่น PNG เรียนรู้ขั้นตอนการแปลงภาพเป็นข้อความด้วย
  Aspose OCR อย่างละเอียด
draft: false
keywords:
- how to use OCR
- extract text from image
- read text from png
- convert image to text
- ocr image to text python
language: th
og_description: วิธีใช้ OCR ใน Python เพื่อดึงข้อความจากภาพ คู่มือนี้จะพาคุณผ่านการแปลงไฟล์
  PNG เป็นข้อความที่สามารถค้นหาได้ด้วย Aspose OCR.
og_title: วิธีใช้ OCR ใน Python – ดึงข้อความจากรูปภาพ
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: How to use OCR in Python to extract text from image files like PNG.
    Learn step‑by‑step conversion of image to text with Aspose OCR.
  headline: How to Use OCR in Python – Extract Text from Images
  type: TechArticle
- description: How to use OCR in Python to extract text from image files like PNG.
    Learn step‑by‑step conversion of image to text with Aspose OCR.
  name: How to Use OCR in Python – Extract Text from Images
  steps:
  - name: Expected Output
    text: '``` Detected language: English Recognized text: Hello, world! This is a
      multi‑language test. こんにちは世界 ```'
  - name: 1. License Not Found
    text: If you see an error like `License file not found`, double‑check the path
      you passed to `set_license`. Using a raw string (`r"..."`) helps avoid escape‑character
      mishaps on Windows.
  - name: 2. Blank Output
    text: 'A blank `ocr_result.text` usually means the image is too noisy or the text
      is too faint. Try increasing the image contrast:'
  - name: 3. Wrong Language Detection
    text: 'If the auto‑detect picks the wrong language, you can force a specific one:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- Aspose
title: วิธีใช้ OCR ใน Python – แยกข้อความจากรูปภาพ
url: /th/python-java/general/how-to-use-ocr-in-python-extract-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีใช้ OCR ใน Python – แยกข้อความจากรูปภาพ

เคยสงสัย **วิธีใช้ OCR** ในโปรเจกต์ Python หรือไม่? คุณไม่ได้เป็นคนเดียว ไม่ว่าคุณจะสร้างสแกนเนอร์ใบเสร็จ, ระบบจัดเก็บเอกสาร, หรือแค่อยากแปลงภาพหน้าจอให้เป็นข้อความที่แก้ไขได้ ความสามารถในการ **แยกข้อความจากรูปภาพ** เป็นการเปลี่ยนเกมอย่างมาก

ในบทเรียนนี้เราจะพาคุณผ่านกระบวนการทั้งหมด — ตั้งแต่การติดตั้งไลบรารี Aspose OCR ไปจนถึงการอ่านข้อความจากไฟล์ PNG — เพื่อให้คุณสามารถ **แปลงรูปภาพเป็นข้อความ** ด้วยเพียงไม่กี่บรรทัดของโค้ด เมื่อเสร็จสิ้นคุณจะรู้วิธี **อ่านข้อความจาก PNG** และแม้กระทั่งจัดการเนื้อหาหลายภาษาโดยอัตโนมัติ

> **Pro tip:** การตรวจจับภาษาของ Aspose OCR แบบอัตโนมัติหมายความว่าคุณไม่ต้องเดาภาษาไว้ล่วงหน้า — เหมาะอย่างยิ่งสำหรับแอปที่เดินทางทั่วโลก

## สิ่งที่คุณต้องเตรียม

- Python 3.8+ (รุ่นเสถียรล่าสุดก็ใช้ได้)
- ไฟล์ใบอนุญาต Aspose OCR ที่ถูกต้อง (`Aspose.OCR.lic`). รุ่นทดลองฟรีใช้สำหรับการทดสอบได้, แต่ใบอนุญาตที่เหมาะสมจะลบข้อจำกัดการประเมินผลออก
- แพคเกจ Aspose OCR ที่ติดตั้งผ่าน `pip`:

```bash
pip install aspose-ocr
```

- ไฟล์รูปภาพที่คุณต้องการประมวลผล — เราจะใช้ `sample-multi-lang.png` เป็นตัวอย่าง

การเตรียมสิ่งเหล่านี้ไว้ล่วงหน้าจะทำให้กระบวนการราบรื่นและหลีกเลี่ยงความประหลาดใจ “module not found” ในภายหลัง

![วิธีใช้ OCR ใน Python workflow](https://example.com/ocr-workflow.png "วิธีใช้ OCR ใน Python – ภาพอธิบายขั้นตอน")

*ข้อความอธิบายภาพ: แผนภาพแสดงวิธีใช้ OCR ใน Python เพื่อแยกข้อความจากรูปภาพ.*

## ขั้นตอนที่ 1: ใช้ใบอนุญาต Aspose OCR ของคุณ (ต้องทำครั้งเดียวต่อแอปพลิเคชัน)

สิ่งแรกที่โครงการ OCR ที่จริงจังทำคือการโหลดใบอนุญาต หากไม่มีใบอนุญาต Aspose จะส่งคำเตือนและจำกัดจำนวนหน้าที่คุณสามารถประมวลผลได้

```python
# Import the license class
from aspose.ocr import License

# Create a License object and point it to your .lic file
ocr_license = License()
ocr_license.set_license(r"C:\Path\To\Your\Aspose.OCR.lic")
```

> **Why this matters:** การโหลดใบอนุญาตล่วงหน้าช่วยให้เครื่องมือ **ocr image to text python** ทำงานเต็มความเร็วและไม่มีลายน้ำ คิดว่าเป็นการปลดล็อกฟีเจอร์พรีเมียมก่อนเริ่มการแปลง

## ขั้นตอนที่ 2: สร้าง OCR Engine และเปิดใช้งานการตรวจจับภาษาอัตโนมัติ

ตอนนี้เราจะสร้างอินสแตนซ์ของเอนจินหลัก การเปิดใช้งาน `language_auto_detect` มีความสำคัญเมื่อคุณไม่ทราบว่าภาพมีภาษาอังกฤษ, สเปน, จีน หรือการผสมผสานของหลายภาษา

```python
from aspose.ocr import OcrEngine

# Initialize the OCR engine
ocr_engine = OcrEngine()

# Turn on auto‑language detection – it works for over 60 languages
ocr_engine.language_auto_detect = True
```

หากคุณ *รู้* ภาษาล่วงหน้า คุณสามารถตั้งค่า `ocr_engine.language = "English"` (หรือรหัส ISO ที่รองรับ) เพื่อเร่งความเร็วได้เล็กน้อย แต่สำหรับยูทิลิตี้ “อ่านข้อความจาก PNG” แบบทั่วไป การตรวจจับอัตโนมัติเป็นตัวเลือกที่ปลอดภัยที่สุด

## ขั้นตอนที่ 3: โหลดภาพที่คุณต้องการประมวลผล

Aspose OCR รองรับรูปแบบต่าง ๆ — PNG, JPEG, BMP, TIFF, ตามที่คุณต้องการ มาโหลดไฟล์ PNG ที่มีหลายภาษา

```python
from aspose.ocr import Image

# Load the image from disk (replace with your actual path)
ocr_image = Image.load_from_file(r"C:\Path\To\sample-multi-lang.png")

# Assign the image to the engine
ocr_engine.image = ocr_image
```

> **กรณีพิเศษ:** หากภาพมีขนาดใหญ่ (เกินหลายเมกะไบต์) คุณอาจต้องลดขนาดลงก่อนเพื่อปรับปรุงประสิทธิภาพ Aspose มีฟังก์ชัน `ocr_image.resize(width, height)` เพื่อใช้ในกรณีนั้น

## ขั้นตอนที่ 4: ทำการรับรู้ OCR

เมื่อทุกอย่างเชื่อมต่อเรียบร้อย การแยกข้อความจริง ๆ เป็นการเรียกเมธอดเดียว วัตถุผลลัพธ์จะให้ทั้งข้อความที่รับรู้และภาษาที่ตรวจพบ

```python
# Run the recognition process
ocr_result = ocr_engine.recognize()
```

เบื้องหลัง Aspose ใช้เครือข่ายประสาทเทียมขั้นสูงและอัลกอริทึมการจับคู่รูปแบบเพื่อแปลงแต่ละกลุ่มพิกเซลเป็นอักขระ การทำงานหนักทั้งหมดทำในโค้ดเนทีฟ ทำให้คุณได้ **OCR ที่เร็วและแม่นยำ** แม้บนฮาร์ดแวร์ระดับกลาง

## ขั้นตอนที่ 5: แสดงภาษาที่ตรวจพบและข้อความที่รับรู้

สุดท้าย เรามาพิมพ์ผลที่ได้ `detected_language` บอกว่าภาษาใดที่ Aspose คาดเดา, และ `text` มีการถอดข้อความเต็มรูปแบบ

```python
print("Detected language:", ocr_result.detected_language)
print("Recognized text:\n", ocr_result.text)
```

### ผลลัพธ์ที่คาดหวัง

```
Detected language: English
Recognized text:
 Hello, world!
 This is a multi‑language test.
 こんにちは世界
```

หากคุณรันสคริปต์บนภาพที่มีทั้งภาษาอังกฤษและญี่ปุ่น คุณจะเห็นการสลับภาษาทำงานอัตโนมัติ — ขอบคุณฟีเจอร์การตรวจจับอัตโนมัติที่เราเปิดไว้ก่อนหน้านี้

## การจัดการกับปัญหาทั่วไป

### 1. ไม่พบใบอนุญาต

หากคุณเห็นข้อผิดพลาดเช่น `License file not found` ให้ตรวจสอบเส้นทางที่ส่งให้ `set_license` อีกครั้ง การใช้ raw string (`r"..."`) ช่วยหลีกเลี่ยงปัญหาอักขระ escape บน Windows

### 2. ผลลัพธ์เป็นค่าว่าง

`ocr_result.text` ที่เป็นค่าว่างมักหมายถึงภาพมีสัญญาณรบกวนมากเกินไปหรือข้อความจางเกินไป ลองเพิ่มความคอนทราสต์ของภาพ:

```python
ocr_image = Image.load_from_file("sample.png")
ocr_image = ocr_image.adjust_contrast(1.5)  # Boost contrast by 50%
ocr_engine.image = ocr_image
```

### 3. การตรวจจับภาษาผิด

หากการตรวจจับอัตโนมัติเลือกภาษาผิด คุณสามารถบังคับให้ใช้ภาษาที่ต้องการได้:

```python
ocr_engine.language = "Japanese"  # ISO code or language name
```

## การขยายตัวอย่าง: ประมวลผลหลายไฟล์ PNG เป็นชุด

บ่อยครั้งคุณอาจต้องการ **แปลงรูปภาพเป็นข้อความ** สำหรับโฟลเดอร์ทั้งหมด ไม่ใช่แค่ไฟล์เดียว นี่คือลูปสั้นที่ประมวลผลทุกไฟล์ PNG ในไดเรกทอรี:

```python
import os
from pathlib import Path

input_folder = Path(r"C:\Images")
output_folder = Path(r"C:\OCR_Output")
output_folder.mkdir(exist_ok=True)

for png_path in input_folder.glob("*.png"):
    # Load and assign image
    ocr_image = Image.load_from_file(str(png_path))
    ocr_engine.image = ocr_image

    # Recognize
    result = ocr_engine.recognize()

    # Write result to a .txt file with the same base name
    txt_path = output_folder / (png_path.stem + ".txt")
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(f"Detected language: {result.detected_language}\n")
        f.write(result.text)

    print(f"Processed {png_path.name} → {txt_path.name}")
```

โค้ดส่วนนี้แสดงวิธีการเชิงปฏิบัติในการ **แยกข้อความจากรูปภาพ** เป็นจำนวนมาก ซึ่งเป็นความต้องการทั่วไปสำหรับกระบวนการดิจิไทเซชันเอกสาร

## สคริปต์ทำงานเต็มรูปแบบ

รวมทุกอย่างเข้าด้วยกัน นี่คือไฟล์เดียวที่คุณสามารถรันจากต้นจนจบ:

```python
# ocr_demo.py
import os
from aspose.ocr import License, OcrEngine, Image

# -------------------------------------------------
# 1️⃣ Apply license (replace with your own path)
# -------------------------------------------------
license_path = r"C:\Path\To\Aspose.OCR.lic"
ocr_license = License()
ocr_license.set_license(license_path)

# -------------------------------------------------
# 2️⃣ Create engine and enable auto‑detect
# -------------------------------------------------
ocr_engine = OcrEngine()
ocr_engine.language_auto_detect = True

# -------------------------------------------------
# 3️⃣ Load image (change to your PNG file)
# -------------------------------------------------
image_path = r"C:\Path\To\sample-multi-lang.png"
ocr_image = Image.load_from_file(image_path)
ocr_engine.image = ocr_image

# -------------------------------------------------
# 4️⃣ Recognize and output results
# -------------------------------------------------
ocr_result = ocr_engine.recognize()
print("Detected language:", ocr_result.detected_language)
print("Recognized text:\n", ocr_result.text)
```

บันทึกเป็น `ocr_demo.py`, รัน `python ocr_demo.py`, แล้วคุณจะเห็นภาษและข้อความที่พิมพ์ออกมาที่คอนโซล

## สรุป

เราได้อธิบาย **วิธีใช้ OCR** ใน Python ตั้งแต่ต้นจนจบ แสดงวิธี **แยกข้อความจากรูปภาพ**, **อ่านข้อความจาก PNG**, และโดยทั่วไป **แปลงรูปภาพเป็นข้อความ** ด้วยเอนจินที่ทรงพลังของ Aspose การโหลดใบอนุญาต, เปิดการตรวจจับภาษาอัตโนมัติ, และป้อนภาพเข้าสู่ `OcrEngine` จะทำให้คุณได้ข้อความที่สะอาดและค้นหาได้ภายในไม่กี่วินาที

ต่อไปคุณจะทำอะไร? ลองเปลี่ยนจาก Aspose ไปใช้ทางเลือกโอเพ่นซอร์สอย่าง Tesseract เพื่อเปรียบเทียบความแม่นยำ, ทดลองกับไฟล์ PDF, หรือรวมขั้นตอน OCR เข้าใน Flask API เพื่อประมวลผลภาพแบบเรียลไทม์ ท้องฟ้าเป็นขอบเขตเมื่อคุณเชี่ยวชาญพื้นฐานของ **ocr image to text python**

มีคำถามเกี่ยวกับการจัดการฟอนต์ที่ซับซ้อน, การเพิ่มประสิทธิภาพ, หรือใบอนุญาต? แสดงความคิดเห็นด้านล่าง แล้วขอให้สนุกกับการเขียนโค้ด!

## คุณควรเรียนรู้อะไรต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดซึ่งต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานแบบอื่นในโปรเจกต์ของคุณ

- [แยกข้อความจากรูปภาพด้วย Aspose OCR – คู่มือขั้นตอน](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [แยกข้อความจากรูปภาพ – การปรับแต่ง OCR ด้วย Aspose.OCR สำหรับ .NET](/ocr/english/net/ocr-optimization/)
- [แยกข้อความจากรูปภาพด้วย C# พร้อมการเลือกภาษาโดยใช้ Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}