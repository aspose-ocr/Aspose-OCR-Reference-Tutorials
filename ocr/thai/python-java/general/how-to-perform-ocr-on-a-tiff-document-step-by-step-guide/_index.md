---
category: general
date: 2026-01-12
description: วิธีทำ OCR อย่างรวดเร็วและแม่นยำ เรียนรู้การรัน OCR บนเอกสาร ดึงข้อความจากไฟล์
  TIFF โหลดภาพสำหรับ OCR และตั้งค่าภาษา OCR ใน Python
draft: false
keywords:
- how to perform ocr
- run ocr on document
- extract text from tiff
- load image for ocr
- set OCR language
language: th
og_description: วิธีทำ OCR ใน Python. บทเรียนนี้จะแสดงวิธีการรัน OCR บนเอกสาร, แยกข้อความจากไฟล์
  TIFF, โหลดภาพสำหรับ OCR และตั้งค่าภาษา OCR.
og_title: วิธีทำ OCR บนเอกสาร TIFF – คู่มือฉบับสมบูรณ์
tags:
- OCR
- Python
- Image Processing
title: วิธีทำ OCR บนเอกสาร TIFF – คู่มือขั้นตอนโดยละเอียด
url: /th/python-java/general/how-to-perform-ocr-on-a-tiff-document-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีทำ OCR บนไฟล์ TIFF – คู่มือฉบับสมบูรณ์

เคยสงสัย **วิธีทำ OCR** บนไฟล์ TIFF ที่สแกนแล้วโดยไม่ต้องเสียเวลาค้นหาไลบรารีที่เหมาะสมหรือไม่? คุณไม่ได้เป็นคนเดียวที่เจอปัญหานี้ นักพัฒนาหลายคนมักเจออุปสรรคเมื่อต้องดึงข้อความจากภาพ TIFF โดยเฉพาะเมื่อประสิทธิภาพและการตั้งค่าภาษาเป็นสิ่งสำคัญ

ในบทเรียนนี้เราจะพาคุณผ่านทุกขั้นตอนที่ต้องรู้: ตั้งแต่การติดตั้งแพคเกจ OCR, การโหลดภาพสำหรับ OCR, การตั้งค่าภาษา OCR, จนถึง **การรัน OCR บนเอกสาร** และดึงข้อความที่สะอาดออกมา เมื่ออ่านจบคุณจะได้สคริปต์พร้อมใช้งานที่สามารถใส่ลงในโปรเจกต์ใดก็ได้

> **เคล็ดลับ:** แม้ตัวอย่างจะใช้โมดูล `ocr` ทั่วไป แนวคิดเดียวกันนี้ใช้ได้กับ Tesseract, EasyOCR หรือเครื่องมือ OCR สมัยใหม่ใด ๆ ที่มี Python API

---

## สิ่งที่คุณต้องมี

- Python 3.8+ (เวอร์ชันล่าสุดใดก็ได้)
- ไลบรารี OCR ที่มีคลาส `OcrEngine` (ตัวอย่างใช้แพคเกจ `ocr` สมมติ; แทนที่ด้วยแพคเกจจริงของคุณ)
- ไฟล์ TIFF แบบหลายหน้า ที่คุณต้องการประมวลผล (เราจะเรียกว่า `big_document.tif`)
- เครื่องที่มีคอร์ CPU อย่างน้อย 4 คอร์ หากคุณต้องการกำหนดจำนวนเธรด

ไม่มีบริการภายนอก ไม่มีคีย์คลาวด์—แค่โค้ดที่ทำงานบนเครื่องของคุณในไม่กี่วินาที

---

![how to perform ocr example](/images/ocr-example.png "how to perform OCR on a TIFF document")

*Image alt text: how to perform OCR on a TIFF document – preview of extracted text.*

---

## ขั้นตอนที่ 1: ติดตั้งและนำเข้าไลบรารี OCR

เริ่มต้นด้วยการติดตั้งไลบรารีบนเครื่องของคุณ แพคเกจ OCR ส่วนใหญ่อยู่บน PyPI จึงใช้ `pip install` เพียงคำสั่งเดียวก็พอ

```bash
pip install ocr‑engine   # replace with the actual package name, e.g., pytesseract
```

จากนั้นนำเข้าคลาสที่จำเป็น หากคุณใช้ Tesseract บรรทัด import จะต่างออกไป แต่โค้ดส่วนอื่นคงเดิม

```python
# Step 1: Import the OCR engine and image helper
import ocr                       # fictional package – swap with your real one
from ocr import OcrEngine, Image
```

*ทำไมต้องทำเช่นนี้:* การนำเข้าสัญลักษณ์ที่ถูกต้องตั้งแต่ต้นช่วยป้องกันการชนกันของ namespace ในภายหลังและทำให้สคริปต์อ่านง่ายขึ้น

---

## ขั้นตอนที่ 2: สร้างและกำหนดค่า OCR Engine (ตั้งค่าภาษา OCR)

การกำหนดค่า engine คือจุดที่คุณ **ตั้งค่าภาษา OCR** เพื่อให้การจดจำแม่นยำ ภาษาอังกฤษเป็นค่าเริ่มต้น แต่คุณสามารถเปลี่ยนเป็นฝรั่งเศส, เยอรมัน หรือโหมดหลายภาษาได้ด้วยบรรทัดเดียว

```python
# Step 2: Initialize the engine and set language
ocr_engine = OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH   # set OCR language to English
ocr_engine.set_thread_count(4)               # limit processing to 4 CPU cores
ocr_engine.set_memory_limit(512 * 1024 * 1024)  # 512 MB internal buffer
```

> **ทำไมต้องใช้ 4 เธรด?** แล็ปท็อปสมัยใหม่ส่วนใหญ่มีคอร์อย่างน้อยสี่คอร์ การจำกัดจำนวนเธรดช่วยไม่ให้กระบวนการ OCR ใช้ทรัพยากรเครื่องทั้งหมด—เป็นประโยชน์เมื่อสคริปต์ทำงานบนเซิร์ฟเวอร์ที่แชร์

หากต้องการภาษาอื่น เพียงเปลี่ยน `ocr.Language.ENGLISH` เป็น `ocr.Language.FRENCH`, `ocr.Language.SPANISH` ฯลฯ

---

## ขั้นตอนที่ 3: โหลดภาพสำหรับ OCR (Load Image for OCR)

ต่อไปเราจะ **โหลดภาพสำหรับ OCR** เมธอด `Image.load` จะอ่านไฟล์ TIFF เข้าเมมโมรีและจัดการกับเอกสารหลายหน้าโดยอัตโนมัติ

```python
# Step 3: Load the TIFF image you want to process
image_path = "YOUR_DIRECTORY/big_document.tif"
image = Image.load(image_path)   # load image for OCR
```

*กรณีขอบ:* หากไฟล์ใหญ่เกินไป คุณอาจหมด RAM ในสถานการณ์นั้น ให้ลองโหลดทีละหน้าโดยใช้ `Image.load_page(page_number)` (ถ้าไลบรารีรองรับ)

---

## ขั้นตอนที่ 4: รัน OCR บนเอกสาร

เมื่อ engine พร้อมและภาพถูกโหลดแล้ว ถึงเวลาที่ **รัน OCR บนเอกสาร** เมธอด `process` จะทำงานหนักและคืนค่าเป็นอ็อบเจกต์ผลลัพธ์

```python
# Step 4: Execute OCR
ocr_result = ocr_engine.process(image)
```

เบื้องหลัง engine จะทำการแบ่งภาพเป็นบล็อกข้อความ, รันโมเดลจดจำ, แล้วรวมผลลัพธ์เข้าด้วยกัน การเรียกนี้เป็นแบบบล็อก หมายความว่าสคริปต์จะรอจนกว่าการประมวลผล TIFF ทั้งหมดเสร็จ—เหมาะกับงานแบบ batch

---

## ขั้นตอนที่ 5: ดึงข้อความจาก TIFF และตรวจสอบผลลัพธ์

สุดท้ายเราจะ **ดึงข้อความจาก TIFF** โดยเข้าถึงแอตทริบิวต์ `text` ของผลลัพธ์ พิมพ์ 200 ตัวอักษรแรกเพื่อเช็คความถูกต้องอย่างรวดเร็ว

```python
# Step 5: Show a preview of the recognized text
preview = ocr_result.text[:200]   # first 200 characters
print("Preview of OCR output:\n", preview)
```

**ผลลัพธ์ที่คาดหวัง (ตัวอย่าง):**

```
Preview of OCR output:
 In the United States, the Constitution guarantees the ...
```

หากต้องการข้อความเต็มให้ใช้ `ocr_result.text` สำหรับการประมวลผลต่อไป คุณอาจต้องการบันทึกลงไฟล์ `.txt`:

```python
with open("extracted_text.txt", "w", encoding="utf-8") as f:
    f.write(ocr_result.text)
```

---

## ตัวอย่างทำงานเต็มรูปแบบ

รวมทุกอย่างเข้าด้วยกัน นี่คือสคริปต์พร้อมรันที่คุณสามารถใช้ได้ เพียงแทนที่ชื่อแพคเกจตัวอย่างด้วยแพคเกจที่คุณติดตั้งจริง

```python
# -*- coding: utf-8 -*-
"""
How to Perform OCR on a TIFF Document – Complete Example
"""

# Install the OCR library first:
# pip install ocr-engine   # adjust to your actual package

import ocr
from ocr import OcrEngine, Image

def main():
    # 1️⃣ Initialize and configure the engine
    engine = OcrEngine()
    engine.language = ocr.Language.ENGLISH
    engine.set_thread_count(4)
    engine.set_memory_limit(512 * 1024 * 1024)

    # 2️⃣ Load the TIFF image
    img_path = "YOUR_DIRECTORY/big_document.tif"
    img = Image.load(img_path)

    # 3️⃣ Run OCR on the loaded image
    result = engine.process(img)

    # 4️⃣ Show a short preview and save the full text
    print("First 200 chars of OCR output:")
    print(result.text[:200])

    with open("extracted_text.txt", "w", encoding="utf-8") as out_file:
        out_file.write(result.text)

    print("\n✅ Extraction complete – see 'extracted_text.txt' for full output.")

if __name__ == "__main__":
    main()
```

รันสคริปต์ด้วยคำสั่ง:

```bash
python ocr_tiff_example.py
```

คุณควรเห็นตัวอย่างข้อความที่พิมพ์บนคอนโซลและไฟล์ชื่อ `extracted_text.txt` ที่มีการถอดข้อความทั้งหมด

---

## คำถามที่พบบ่อย & กรณีขอบ

- **ถ้า TIFF มีหลายหน้า จะทำอย่างไร?**  
  ส่วนใหญ่ OCR engine จะจัดการแต่ละหน้าเป็นภาพแยก `ocr_result.text` จะมีการขึ้นบรรทัดใหม่ระหว่างหน้า หากต้องการจัดการต่อหน้า ให้ใช้ `Image.load_page(page_number)` ในลูป

- **สามารถประมวลผล PNG หรือ JPEG แทน TIFF ได้หรือไม่?**  
  ทำได้เลย เมธอด `Image.load` ส่วนใหญ่รองรับฟอร์แมตใดก็ได้ที่ Pillow หรือไลบรารีพื้นฐานรองรับ เพียงเปลี่ยนนามสกุลไฟล์

- **ข้อความออกมาดูเป็นอักขระแปลก ๆ ควรเปลี่ยนภาษาไหม?**  
  ควรทำเช่นนั้น ขั้นตอน **ตั้งค่าภาษา OCR** มีความสำคัญสำหรับเอกสารที่ไม่ใช่ภาษาอังกฤษ ตรวจสอบให้แน่ใจว่าติดตั้งแพ็คเกจภาษาที่ต้องการ (เช่น `tesseract‑lang‑fra` สำหรับฝรั่งเศส)

- **หมดหน่วยความจำ?**  
  ลดค่า `set_memory_limit` หรือประมวลผลหน้าเป็นหน้า บาง engine ยังให้คุณลดขนาดภาพก่อนจดจำได้อีกด้วย

---

## สรุป

นี่คือคู่มือสั้น ๆ ที่ครบถ้วนเกี่ยวกับ **วิธีทำ OCR** บนไฟล์ TIFF ด้วย Python เราได้ครอบคลุมตั้งแต่การติดตั้งไลบรารี, การกำหนดค่า engine (รวมถึง **ตั้งค่าภาษา OCR**), **โหลดภาพสำหรับ OCR**, **รัน OCR บนเอกสาร**, และสุดท้าย **ดึงข้อความจาก TIFF**  

ลองปรับเปลี่ยนจำนวนเธรด, สลับภาษา, หรือส่งผลลัพธ์ OCR ไปยัง pipeline ประมวลผลภาษาธรรมชาติอื่น ๆ ความเป็นไปได้ไม่มีขีดจำกัดเมื่อคุณเชี่ยวชาญพื้นฐานเหล่านี้

มีคำถามเพิ่มเติม? แสดงความคิดเห็นด้านล่าง แล้วขอให้สนุกกับการเขียนโค้ด!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}