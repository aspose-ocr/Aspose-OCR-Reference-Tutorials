---
category: general
date: 2026-06-28
description: เรียนรู้วิธีจดจำภาพข้อความด้วย Python OCR, แยกไฟล์ PNG ที่มีข้อความ,
  และพิมพ์ข้อความที่จดจำได้พร้อมการจัดการข้อผิดพลาดอย่างแข็งแรง.
draft: false
keywords:
- recognize text image
- extract text png
- load image ocr
- process image ocr
- print recognized text
language: th
og_description: บทเรียนสอนขั้นตอนการจดจำภาพข้อความใน Python, แยกข้อความจากไฟล์ PNG,
  และพิมพ์ข้อความที่จดจำได้อย่างปลอดภัย.
og_title: จดจำข้อความจากภาพด้วย Python OCR – คู่มือฉบับสมบูรณ์
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Learn how to recognize text image using Python OCR, extract text png
    files, and print recognized text with robust error handling.
  headline: recognize text image with Python OCR – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: จดจำข้อความในภาพด้วย Python OCR – คู่มือฉบับสมบูรณ์
url: /th/python/general/recognize-text-image-with-python-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# การจดจำข้อความจากรูปภาพด้วย Python OCR – คู่มือฉบับสมบูรณ์

เคยสงสัยไหมว่า **การจดจำข้อความจากรูปภาพ** ในสคริปต์ Python สามารถทำได้โดยไม่ต้องดึงเฟรมเวิร์กขนาดใหญ่? คุณไม่ได้เป็นคนเดียว นักพัฒนาจำนวนมากต้องการวิธีที่รวดเร็วในการ *load image OCR* เช่น ภาพหน้าจอ ใบเสร็จสแกน หรือ PNG ธรรมดาและดึงข้อความกลับมา  

ในบทเรียนนี้เราจะเชื่อมต่อเครื่องมือ OCR ขั้นต่ำ, แนบ logger แบบกำหนดเอง, **load image OCR**, เรียกใช้ **process image OCR**, และสุดท้าย **print recognized text**. เมื่อเสร็จคุณจะมีสคริปต์ที่ทำงานอิสระซึ่งยังสามารถ **extract text png** ได้ตามต้องการ  

## สิ่งที่คุณจะได้เรียนรู้

- สคริปต์ Python ที่ทำงานเต็มรูปแบบซึ่งสร้าง OCR engine, บันทึกทุกขั้นตอน, และจัดการข้อผิดพลาดอย่างราบรื่น.  
- คำอธิบายที่ชัดเจนว่าทำไมแต่ละบรรทัดถึงสำคัญ — เพื่อให้คุณปรับโค้ดไปใช้กับ Tesseract, EasyOCR หรือ backend ใดก็ได้.  
- เคล็ดลับสำหรับปัญหาที่พบบ่อย (ฟอนต์หาย, PNG เสีย) และวิธีดีบัก.  

### ข้อกำหนดเบื้องต้น

- Python 3.8+ ที่ติดตั้งแล้ว  
- ไลบรารี OCR ที่มีคลาส `OcrEngine` (ตัวอย่างใช้ API สมมติ; แทนที่ด้วย `pytesseract`, `easyocr` เป็นต้น).  
- ไฟล์ PNG ที่ต้องการวิเคราะห์, บันทึกเป็น `input.png` ในโฟลเดอร์ที่คุณควบคุม.  

> **Pro tip:** หากคุณใช้ `pytesseract`, ติดตั้งไบนารี Tesseract ของระบบก่อน (`sudo apt install tesseract-ocr` บน Linux) แล้วตามด้วย `pip install pytesseract pillow`.  

---

## ## การจดจำข้อความจากรูปภาพ: ตั้งค่า Logger

```python
# Step 1: Define a simple logger for the OCR engine
def my_logger(level, message):
    """
    level: str – e.g., "INFO", "WARN", "ERROR"
    message: str – human‑readable description of the event
    """
    print(f"[{level}] {message}")
```

*ทำไมสิ่งนี้จึงสำคัญ:*  
Logger แยกการแสดงผลการวินิจฉัยออกจากแกน OCR ทำให้สามารถส่งต่อ log ไปยังไฟล์, บริการมอนิเตอร์, หรือแม้แต่ UI ในภายหลังได้อย่างง่ายดาย.  

---

## ## โหลดภาพ OCR: ส่ง PNG ให้ Engine

```python
from PIL import Image

# Step 2: Create the OCR engine and attach the logger
ocr_engine = OcrEngine(logging=my_logger)

# Step 3: Load the image to be processed
image_path = "YOUR_DIRECTORY/input.png"
ocr_engine.set_image(Image.from_file(image_path))
my_logger("INFO", f"Loaded image from {image_path}")
```

*จุดสำคัญ:*  

- **load image ocr** – `Image.from_file` แยกรายละเอียดการถอดรหัส PNG ออก.  
- เก็บเส้นทางให้กำหนดค่าได้; การกำหนดค่าคงที่ทำให้สคริปต์อ่อนแอ.  
- การเรียก logger ยืนยันว่าภาพถูกอ่านสำเร็จ, มีประโยชน์เมื่อไฟล์หายหรือเสีย.  

---

## ## ประมวลผลภาพ OCR: การจดจำข้อความ

```python
# Step 4: Recognize text from the image
try:
    extracted_text = ocr_engine.recognize()
    my_logger("INFO", "OCR succeeded")
except OcrException as e:
    # Step 5: Handle OCR errors gracefully
    my_logger("ERROR", f"OCR failed with code {e.code}: {e.message}")
    extracted_text = None
```

*ทำไมเราถึงใส่ใน `try/except`:*  
OCR อาจล้มเหลวกับ PNG ความละเอียดต่ำ, พื้นที่สีที่ไม่รองรับ, หรือข้อมูลภาษาไม่ครบ. การจับ `OcrException` ทำให้คุณ **print recognized text** เฉพาะเมื่อมีข้อความจริง, ป้องกัน stack trace ที่ซับซ้อนสำหรับผู้ใช้.  

---

## ## พิมพ์ข้อความที่จดจำได้ & แยกข้อความจาก PNG

```python
if extracted_text:
    # Step 6: Print the recognized text
    print("Recognized text:", extracted_text)
    my_logger("INFO", "Printed recognized text to console")

    # Optional: Save extracted text for later use
    txt_path = image_path.rsplit(".", 1)[0] + ".txt"
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(extracted_text)
    my_logger("INFO", f"Saved extracted text to {txt_path}")
```

*สิ่งที่คุณจะได้:*  

- **print recognized text** – แสดงผลทันทีในเทอร์มินัล.  
- ไฟล์ `.txt` คู่ข้างที่ทำหน้าที่ **extract text png** สำหรับการประมวลผลต่อ (การทำดัชนีค้นหา, การป้อนข้อมูล ฯลฯ).  

---

## ## กรณีขอบที่พบบ่อย & วิธีจัดการ

| สถานการณ์ | อาการ | วิธีแก้ |
|-----------|---------|-----|
| PNG เป็นระดับสีเทาเท่านั้น | OCR คืนสตริงว่าง | แปลงเป็น RGB (`Image.convert("RGB")`) ก่อนส่งให้ engine. |
| ภาษาที่ไม่รองรับ | `OcrException` พร้อมโค้ด `LANG_NOT_FOUND` | ติดตั้งแพ็คเกจภาษา (เช่น `tesseract‑lang‑fra` สำหรับภาษาฝรั่งเศส) และตั้งค่า `ocr_engine.language = "fra"`. |
| ภาพขนาดใหญ่มาก ( > 5 MB ) | การจดจำช้า หรือข้อผิดพลาดหน่วยความจำ | ลดขนาดด้วย `image.thumbnail((2000, 2000))` ก่อน `set_image`. |
| อักขระที่ไม่คาดคิด | ผลลัพธ์เป็นข้อความเสียหาย | ตรวจสอบว่าภาพเป็น PNG จริง; บางไฟล์ทำตัวเป็น PNG แต่จริงๆ เป็น JPEG. ใช้ `Image.verify()` เพื่อตรวจสอบ. |

---

## ## ตัวอย่างทำงานเต็ม (พร้อมคัดลอก‑วาง)

```python
# -*- coding: utf-8 -*-
"""
Complete script to recognize text image using a generic OCR engine.
Replace OcrEngine, OcrException with the concrete classes from your library.
"""

from PIL import Image

# ----------------------------------------------------------------------
# 1️⃣  Logger definition
# ----------------------------------------------------------------------
def my_logger(level: str, message: str) -> None:
    """Simple console logger."""
    print(f"[{level}] {message}")

# ----------------------------------------------------------------------
# 2️⃣  Engine creation & image loading
# ----------------------------------------------------------------------
ocr_engine = OcrEngine(logging=my_logger)   # <- adapt to your library

image_path = "YOUR_DIRECTORY/input.png"
try:
    img = Image.open(image_path)
    img.verify()                     # sanity check the PNG
    img = Image.open(image_path)     # reopen after verify
    ocr_engine.set_image(img)
    my_logger("INFO", f"Loaded image from {image_path}")
except Exception as load_err:
    my_logger("ERROR", f"Failed to load image: {load_err}")
    raise SystemExit(1)

# ----------------------------------------------------------------------
# 3️⃣  Text recognition
# ----------------------------------------------------------------------
try:
    extracted_text = ocr_engine.recognize()
    my_logger("INFO", "OCR succeeded")
except OcrException as e:            # replace with actual exception class
    my_logger("ERROR", f"OCR failed ({e.code}): {e.message}")
    extracted_text = None

# ----------------------------------------------------------------------
# 4️⃣  Output handling
# ----------------------------------------------------------------------
if extracted_text:
    print("Recognized text:", extracted_text)          # ✅ print recognized text
    txt_path = image_path.rsplit(".", 1)[0] + ".txt"
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(extracted_text)
    my_logger("INFO", f"Saved extracted text to {txt_path}")
else:
    my_logger("WARN", "No text extracted; check image quality.")
```

**ผลลัพธ์คอนโซลที่คาดหวัง (เส้นทางที่ทำงานได้ดี):**

```
[INFO] Loaded image from YOUR_DIRECTORY/input.png
[INFO] OCR succeeded
Recognized text: Invoice #12345
Total Amount: $1,250.00
Date: 2026‑06‑01
[INFO] Saved extracted text to YOUR_DIRECTORY/input.txt
```

หากเกิดข้อผิดพลาด, คุณจะเห็นบรรทัด `[ERROR]` ชัดเจนพร้อมเหตุผล, ขอบคุณ logger ที่กำหนดเอง.  

---

## ## ขั้นตอนต่อไป & หัวข้อที่เกี่ยวข้อง

- **extract text png** จากชุดหลายไฟล์: ห่อสคริปต์ด้วย `for` loop ที่เดินผ่านโครงสร้างไดเรกทอรี.  
- **process image ocr** ด้วยการเตรียมข้อมูลล่วงหน้า (แก้ไขการเอียง, เพิ่มคอนทราสต์) โดยใช้ OpenCV ก่อนส่งให้ engine.  
- สลับไปใช้บริการ OCR คลาวด์ (Google Vision, Azure Read) โดยเปลี่ยนการทำงานของ `OcrEngine` — โค้ดส่วนอื่นยังคงเหมือนเดิม.  
- เรียนรู้วิธี **print recognized text** ลงใน PDF ด้วย `reportlab` สำหรับการสร้างรายงานอัตโนมัติ.  

---

## สรุป

เราได้เดินผ่านวิธีการที่กะทัดรัดและพร้อมใช้งานในระดับ production เพื่อ **recognize text image** ด้วย Python, ตั้งแต่การโหลด PNG ไปจนถึง **print recognized text** และการบันทึกผลลัพธ์. ด้วยการเพิ่ม logger เล็ก ๆ, การจัดการข้อยกเว้น, และการบันทึกผลลัพธ์ตามต้องการ, สคริปต์นี้พร้อมสำหรับการทดลองอย่างรวดเร็วและการผสานเข้ากับ pipeline ขนาดใหญ่  

ลองใช้กับสกรีนช็อตของคุณ, ปรับแต่งการเตรียมภาพ, แล้วคุณจะสามารถแยกข้อความจาก PNG ใดก็ได้ที่คุณต้องการ. มีคำถาม? แสดงความคิดเห็น—ขอให้ OCR สนุก!  

![recognize text image example](placeholder.png)


## สิ่งที่คุณควรเรียนต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้. แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอนเพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโปรเจกต์ของคุณ.

- [แยกข้อความจากรูปภาพด้วย Aspose OCR – คู่มือขั้นตอน](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [วิธีทำการแยกข้อความจากสตรีมโดยใช้ Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [แปลงรูปภาพเป็นข้อความ – ทำ OCR บนรูปภาพจาก URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}