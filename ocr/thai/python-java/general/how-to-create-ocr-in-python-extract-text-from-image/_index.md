---
category: general
date: 2026-04-26
description: วิธีสร้าง OCR อย่างรวดเร็วและเชื่อถือได้ เรียนรู้การสกัดข้อความจากภาพ
  โหลดภาพสำหรับ OCR และรัน OCR บนไฟล์ PNG ด้วยพจนานุกรมที่กำหนดเอง
draft: false
keywords:
- how to create OCR
- extract text from image
- extract text scanned document
- load image for OCR
- run OCR on png
language: th
og_description: วิธีสร้าง OCR ด้วย Python และดึงข้อความจากภาพ คู่มือนี้แสดงวิธีโหลดภาพสำหรับ
  OCR, รัน OCR บนไฟล์ PNG, และใช้พจนานุกรมกำหนดเอง.
og_title: วิธีสร้าง OCR ด้วย Python – การสกัดข้อความอย่างรวดเร็ว
tags:
- OCR
- Python
- Image Processing
title: วิธีสร้าง OCR ด้วย Python – แยกข้อความจากรูปภาพ
url: /th/python-java/general/how-to-create-ocr-in-python-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีสร้าง OCR ด้วย Python – คู่มือขั้นตอนต่อขั้นตอน

เคยสงสัย **วิธีสร้าง OCR** ที่สามารถอ่านไฟล์ PDF ที่สแกน, ภาพหน้าจอ, หรือบันทึกมือของคุณหรือไม่? คุณไม่ได้เป็นคนเดียว ในหลายโครงการจริง ๆ เราต้องการ *ดึงข้อความจากไฟล์ภาพ* แต่เครื่องมือสำเร็จรูปมักจะสับสนกับคำเฉพาะโดเมน  

ในบทเรียนนี้คุณจะได้เห็นตัวอย่างที่สมบูรณ์และสามารถรันได้ ซึ่งโหลดภาพสำหรับ OCR, ใช้พจนานุกรมกำหนดเอง, และสุดท้าย **run OCR on PNG** คุณจะสามารถดึงข้อความจากภาพใด ๆ และปรับแต่งเอนจินให้สอดคล้องกับศัพท์ของคุณเองได้

## สิ่งที่บทเรียนนี้ครอบคลุม

เราจะเดินผ่านทุกขั้นตอนที่คุณต้องทำ:

* การติดตั้งแพ็กเกจ `aocr` ที่เล็กแต่ทรงพลัง (หรือไลบรารีที่เข้ากันได้)  
* การกำหนด **พจนานุกรมกำหนดเอง** เพื่อให้คำเช่น `aspocorp` หรือ `licensekey` ถูกจดจำ  
* **Loading an image for OCR**, ไม่ว่าจะเป็น PNG, JPEG หรือหน้าสแกนของ PDF  
* การรันกระบวนการ OCR และพิมพ์ผลลัพธ์  

ไม่มีลิงก์เอกสารภายนอก เพียงโซลูชันที่สามารถคัดลอก‑วางและรันได้ทันที

### ข้อกำหนดเบื้องต้น

* Python 3.8 หรือใหม่กว่า (โค้ดใช้ f‑strings)  
* ความคุ้นเคยพื้นฐานกับ command line – คุณจะต้องพิมพ์คำสั่ง `pip install` สองสามครั้ง  
* ไฟล์ภาพ (`technical_doc.png` ในตัวอย่าง) ที่วางไว้ในตำแหน่งที่คุณสามารถอ้างอิงได้  

หากคุณมีสามสิ่งนี้ครบ คุณก็พร้อมเริ่มแล้ว  

---

## Step 1: Install the OCR Library

ก่อนอื่นเราต้องการ OCR engine ที่รองรับการกำหนดค่าแบบโปรแกรมได้ แพ็กเกจ `aocr` เป็น wrapper ที่เบาและทำงานได้ดีสำหรับการสาธิต

```bash
# Install the library (run once)
pip install aocr
```

> **Pro tip:** หากคุณใช้ Windows แล้วเจอข้อผิดพลาดการคอมไพล์ ให้ลอง `pip install aocr‑binary` ซึ่งมี wheel ที่สร้างไว้ล่วงหน้า

### ทำไมต้องติดตั้งไลบรารีนี้?

`aocr` ให้เราถึง `config` object โดยตรงที่สามารถใส่ **custom dictionary** เข้าไปได้ นี่คือเคล็ดลับสำคัญสำหรับการเพิ่มความแม่นยำบนคำศัพท์เฉพาะ

---

## Step 2: Create the OCR Engine Instance & Add a Custom Dictionary

ตอนนี้เราจะสร้าง engine และบอกให้มันรู้จักคำที่ควรถือว่าเป็นที่รู้จัก

```python
from aocr import OcrEngine

# Step 2: Create an OCR engine instance
ocr_engine = OcrEngine()

# Provide a custom dictionary to improve recognition of domain‑specific terms
ocr_engine.config.custom_dictionary = [
    "aspocorp",      # our company's brand name
    "ocrengine",    # the library name itself
    "licensekey"    # a common field in our contracts
]
```

### ทำไมพจนานุกรมกำหนดเองถึงสำคัญ

โมเดล OCR มาตรฐานฝึกจากข้อมูลทั่วไป เมื่อโมเดลเจอ “aspocorp” มันอาจจะแยกเป็น “aspo corp” หรือทิ้งอักษรบางตัวไปได้ การใส่รายการกำหนดเองทำให้ recognizer มีแนวโน้มจดจำการสะกดที่เราต้องการ ลดความพยายามในการประมวลผลต่อไปอย่างมาก

---

## Step 3: Load the Image You Want to Process

นี่คือจุดที่เราจะ **load image for OCR** เมธอด `Image.load` รับพาธเป็นสตริงและกำหนดประเภทไฟล์โดยอัตโนมัติ

```python
import aocr

# Step 3: Load the image that contains the text you want to extract
ocr_engine.image = aocr.Image.load("YOUR_DIRECTORY/technical_doc.png")
```

> **Edge case:** หากแหล่งข้อมูลของคุณเป็น PDF หลายหน้า ให้แปลงแต่ละหน้าเป็น PNG ก่อน (เช่นด้วย `pdf2image`) แล้วส่งเข้า engine ทีละหน้า

### เคล็ดลับเพื่อคุณภาพภาพที่ดียิ่งขึ้น

* รักษาความละเอียดอย่างน้อย 300 dpi  
* ตรวจสอบให้ภาพอยู่ในแนวตั้ง; หากต้องหมุนให้ใช้ `Pillow`  
* แปลงสแกนสีเป็น grayscale เพื่อลดสัญญาณรบกวน

---

## Step 4: Run the OCR Process on the PNG File

เมื่อ engine ถูกกำหนดค่าและภาพถูกโหลดแล้ว เราจะ **run OCR on PNG** สุดท้าย

```python
# Step 4: Run the OCR process
ocr_result = ocr_engine.process()
```

การเรียก `process()` จะคืนค่าเป็นอ็อบเจกต์ที่มีข้อความที่จดจำได้, คะแนนความมั่นใจ, และ bounding box ของแต่ละคำ

---

## Step 5: Output the Recognized Text

วิธีง่ายที่สุดเพื่อดูผลลัพธ์คือพิมพ์แอตทริบิวต์ `text`

```python
# Step 5: Output the recognized text
print(ocr_result.text)
```

### ผลลัพธ์ที่คาดหวัง

หาก `technical_doc.png` มีประโยค *“The Aspocorp licensekey expires on 2025‑12‑31.”* คอนโซลจะพิมพ์:

```
The Aspocorp licensekey expires on 2025-12-31.
```

สังเกตว่าพจนานุกรมกำหนดเองทำให้ชื่อแบรนด์คงอยู่โดยไม่ถูกแปลงผิดเหมือน OCR ปกติ

---

## Full Working Example (Copy‑Paste Ready)

ด้านล่างเป็นสคริปต์ทั้งหมด พร้อมบันทึกเป็น `run_ocr.py` เพียงเปลี่ยนพาธตัวอย่างให้ตรงกับตำแหน่งภาพของคุณ

```python
# run_ocr.py
# -------------------------------------------------
# Complete example showing how to create OCR,
# load an image, apply a custom dictionary,
# and extract text from a PNG file.
# -------------------------------------------------

from aocr import OcrEngine
import aocr

def main():
    # 1️⃣ Create the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Add domain‑specific words
    ocr_engine.config.custom_dictionary = [
        "aspocorp",
        "ocrengine",
        "licensekey"
    ]

    # 3️⃣ Load the image you want to process
    #    (Make sure the path points to a real file)
    image_path = "YOUR_DIRECTORY/technical_doc.png"
    ocr_engine.image = aocr.Image.load(image_path)

    # 4️⃣ Run the OCR engine
    ocr_result = ocr_engine.process()

    # 5️⃣ Print the extracted text
    print("=== Extracted Text ===")
    print(ocr_result.text)

if __name__ == "__main__":
    main()
```

รันจากเทอร์มินัล:

```bash
python run_ocr.py
```

คุณควรเห็นข้อความที่ดึงออกมาปรากฏบนคอนโซล ตามที่แสดงในตัวอย่างก่อนหน้า

---

## Frequently Asked Questions (FAQ)

| Question | Answer |
|----------|--------|
| **Can I extract text from a scanned PDF?** | ใช่. ให้แปลงแต่ละหน้าเป็น PNG (หรือ TIFF) ก่อน แล้วส่งภาพเหล่านั้นไปยังสคริปต์เดียวกัน |
| **What if my image is a JPEG instead of PNG?** | เมธอด `Image.load` รองรับ JPEG, BMP, TIFF, และ PNG อยู่แล้ว เพียงเปลี่ยนนามสกุลไฟล์ |
| **How do I improve accuracy on low‑contrast scans?** | ทำการพรี‑โปรเซสด้วย `Pillow` – เพิ่มความคอนทราสต์, ทำ binarization, หรือใช้ `opencv` เพื่อลบการเอียง |
| **Is there a way to get confidence scores for each word?** | `ocr_result` มี `words` – แต่ละคำมีแอตทริบิวต์ `confidence` ที่คุณสามารถวนลูปได้ |
| **Can I run this on a headless server?** | แน่นอน. `aocr` ไม่มี dependency ของ GUI ทำให้เหมาะกับ CI pipelines |

---

## Next Steps & Related Topics

ตอนนี้คุณรู้ **how to create OCR** และ **extract text from image** แล้ว ลองสำรวจต่อ:

* **Pre‑processing techniques** – `load image for OCR` เป็นแค่ขั้นตอนแรก; ใช้ `opencv` เพื่อลดสัญญาณรบกวนหรือเพิ่มความคมชัด  
* **Batch processing** – วนลูปผ่านโฟลเดอร์ของ PNG เพื่อสร้างคลังข้อมูลที่ค้นหาได้  
* **Multi‑language support** – เพิ่ม language pack ให้ engine หากต้องอ่านเอกสารภาษาฝรั่งเศสหรือเยอรมัน  
* **Integrating with Elasticsearch** – ทำดัชนีข้อความที่ดึงได้เพื่อการค้นหาเต็มข้อความในเอกสารสแกนทั้งหมด  

แต่ละหัวข้อขยายจากรูปแบบพื้นฐานที่เราได้ครอบคลุมแล้ว ทำให้การต่อยอดเป็นเรื่องง่าย

---

## Wrap‑Up

ในเวลาไม่กี่นาที เราได้ตอบ **how to create OCR** ที่สามารถ **extract text from image** ได้อย่างเชื่อถือได้ โดยเฉพาะ PNG เราแสดงวิธี **load image for OCR**, ใช้ **custom dictionary**, และ **run OCR on PNG** โดยไม่ต้องพึ่งบริการภายนอก  

ลองรันสคริปต์ ปรับพจนานุกรมให้ตรงกับศัพท์ของคุณเอง แล้วคุณจะมีพื้นฐานที่แข็งแกร่งสำหรับโครงการดิจิไทเซชันเอกสารใด ๆ  

หากเจอปัญหาใด ๆ คอมเมนต์ด้านล่างได้ เราพร้อมช่วยเหลือ อย่าลืมแชร์เรื่องราวความสำเร็จของคุณ; ชุมชนเรียนรู้ดีที่สุดจากตัวอย่างจริง  

**พร้อมจะทำให้กระบวนการเอกสารอัตโนมัติหรือยัง?** ดึงโค้ดมาใช้ ปรับให้เข้ากับความต้องการของคุณ แล้วเริ่มแปลงพิกเซลเป็นข้อความที่ค้นหาได้วันนี้!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}