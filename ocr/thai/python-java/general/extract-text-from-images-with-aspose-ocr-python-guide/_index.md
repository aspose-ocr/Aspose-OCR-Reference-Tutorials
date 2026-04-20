---
category: general
date: 2026-03-18
description: เรียนรู้วิธีดึงข้อความจากภาพและแปลงข้อความจากภาพสแกนเป็นสตริงที่แก้ไขได้โดยใช้
  Aspose OCR ใน Python พร้อมโค้ดขั้นตอนโดยละเอียด
draft: false
keywords:
- extract text from images
- convert scanned images text
- Aspose OCR Python
- batch OCR processing
- image to text conversion
language: th
og_description: ดึงข้อความจากภาพโดยใช้ Aspose OCR ใน Python บทเรียนนี้แสดงวิธีแปลงข้อความจากภาพสแกนด้วยเพียงไม่กี่บรรทัดของโค้ด
og_title: ดึงข้อความจากรูปภาพด้วย Aspose OCR – คู่มือ Python
tags:
- OCR
- Python
- Aspose
- Image Processing
title: ดึงข้อความจากรูปภาพด้วย Aspose OCR – คู่มือ Python
url: /th/python-java/general/extract-text-from-images-with-aspose-ocr-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ดึงข้อความจากรูปภาพด้วย Aspose OCR – คู่มือ Python

เคยต้อง **ดึงข้อความจากรูปภาพ** แต่ไม่รู้ว่าจะเริ่มต้นอย่างไรหรือไม่? คุณไม่ได้เป็นคนเดียว—นักพัฒนามักต้องเผชิญกับความยุ่งยากในการแปลง PDF ที่สแกน, ภาพหน้าจอที่มีสัญญาณรบกวน, หรือใบเสร็จที่ถ่ายเป็นรูปให้เป็นสตริงที่ค้นหาและแก้ไขได้  

ข่าวดีคือ? ด้วย Aspose OCR สำหรับ Python คุณสามารถ **แปลงข้อความจากภาพที่สแกน** เป็นจำนวนมากได้โดยไม่ต้องออกจาก IDE ของคุณ ในบทแนะนำนี้เราจะเดินผ่านตัวอย่างที่พร้อมรันเต็มรูปแบบที่แสดงให้เห็นอย่างชัดเจนว่าทำอย่างไร, ทำไมขั้นตอนแต่ละขั้นตอนจึงสำคัญ, และสิ่งที่ควรระวัง

## สิ่งที่คุณจะได้เรียนรู้

- ตั้งค่าไลบรารี Aspose OCR ในสภาพแวดล้อม Python  
- เตรียมรายการไฟล์รูปภาพ (PNG, JPG, TIFF ฯลฯ)  
- รัน OCR แบบแบตช์ด้วยการเรียกเมธอดเดียว  
- เข้าถึงและแสดงข้อความที่ดึงออกมาสำหรับแต่ละไฟล์  
- จัดการกับปัญหาที่พบบ่อยเช่นรูปแบบที่ไม่รองรับและการใช้หน่วยความจำของไฟล์ขนาดใหญ่  

เมื่อจบคุณจะมีสคริปต์ที่นำกลับมาใช้ใหม่ได้เพื่อ **ดึงข้อความจากรูปภาพ** ตามต้องการ—เหมาะสำหรับการทำอัตโนมัติการป้อนข้อมูล, การทำดัชนีเอกสาร, หรือการป้อนข้อมูลให้กับ pipeline NLP ต่อไป

---

![ตัวอย่างการดึงข้อความจากรูปภาพ](/images/ocr-extract-text.png "ดึงข้อความจากรูปภาพ")

*ข้อความแทนภาพ: “ดึงข้อความจากรูปภาพโดยใช้ Aspose OCR ใน Python”*

## ข้อกำหนดเบื้องต้น

- Python 3.8 หรือใหม่กว่า (โค้ดใช้ f‑strings)  
- ใบอนุญาต Aspose OCR สำหรับ Python ที่ถูกต้องหรือคีย์ทดลองฟรี  
- รูปภาพที่คุณต้องการประมวลผลจัดเก็บไว้ในเครื่อง (ผสม PNG, JPG หรือ TIFF ได้)  

หากคุณมี virtual environment อยู่แล้วดีมาก—หากยังไม่มี ให้สร้างด้วย:

```bash
python -m venv ocr-env
source ocr-env/bin/activate   # On Windows: ocr-env\Scripts\activate
```

ตอนนี้คุณพร้อมที่จะติดตั้ง SDK แล้ว

## ขั้นตอนที่ 1: ติดตั้ง Aspose OCR SDK

Aspose แจกจ่ายเอนจิน OCR ผ่าน PyPI ดังนั้นคำสั่ง `pip` เพียงคำสั่งเดียวก็ทำได้:

```bash
pip install aspose-ocr
```

> **เคล็ดลับ:** กำหนดเวอร์ชัน (เช่น `aspose-ocr==22.12`) เพื่อหลีกเลี่ยงการเปลี่ยนแปลงที่ทำให้โค้ดพังในภายหลัง

## ขั้นตอนที่ 2: นำเข้าคลาส OCR Engine

คลาสหลักที่คุณจะทำงานด้วยคือ `OcrEngine` นำเข้าที่ส่วนบนของสคริปต์ของคุณ:

```python
# Step 2: Import the OCR engine class
from asposeocr import OcrEngine
```

> *ทำไมจึงสำคัญ:* การนำเข้าเฉพาะที่จำเป็นทำให้เวลาเริ่มต้นสั้นลง, โดยเฉพาะเมื่อคุณฝังสคริปต์นี้ในแอปพลิเคชันที่ใหญ่กว่า

## ขั้นตอนที่ 3: กำหนดไฟล์รูปภาพที่จะประมวลผล

สร้างรายการ Python ที่บรรจุพาธเต็มของทุกภาพที่คุณต้องการสแกน แทนที่ `YOUR_DIRECTORY` ด้วยพาธโฟลเดอร์จริงของคุณ

```python
# Step 3: Define the image files to be processed
image_files = [
    "YOUR_DIRECTORY/page1.png",
    "YOUR_DIRECTORY/page2.jpg",
    "YOUR_DIRECTORY/page3.tif"
]
```

> **กรณีขอบ:** หากคุณมีไฟล์หลายร้อยไฟล์, พิจารณาสร้างรายการนี้โดยอัตโนมัติด้วย `glob.glob('*.png')` เพื่อหลีกเลี่ยงการแก้ไขด้วยมือ

## ขั้นตอนที่ 4: รัน OCR บนรูปภาพทั้งหมดพร้อมกัน

Aspose OCR มีเมธอด `processMultiple` ที่สะดวกซึ่งคืนค่าเป็นรายการของอ็อบเจ็กต์ `OcrResult`—หนึ่งอ็อบเจ็กต์ต่อไฟล์อินพุต

```python
# Step 4: Run OCR on all images at once
ocr_engine = OcrEngine()               # instantiate the engine
ocr_results = ocr_engine.processMultiple(image_files)
```

> *ทำไมต้องประมวลผลเป็นแบตช์?* การส่งแต่ละภาพแยกกันทำให้เกิดภาระเพิ่ม (การเริ่มต้นเอนจิน, โหลดไลบรารีเนทีฟ) การเรียกแบบแบตช์ช่วยลดการใช้ CPU และเร่งความเร็วของงานโดยรวม

### การจัดการข้อผิดพลาดอย่างสุภาพ

หากภาพไม่สามารถอ่านได้ (ไฟล์เสีย, รูปแบบไม่รองรับ) `processMultiple` จะโยนข้อยกเว้น ใช้ `try/except` เพื่อให้สคริปต์ทำงานต่อได้:

```python
try:
    ocr_results = ocr_engine.processMultiple(image_files)
except Exception as e:
    print(f"⚠️ OCR failed: {e}")
    ocr_results = []   # fallback to empty list
```

## ขั้นตอนที่ 5: แสดงข้อความที่ดึงออกมาสำหรับแต่ละไฟล์

วนลูปผลลัพธ์, จับคู่ `OcrResult` กับชื่อไฟล์ต้นฉบับของมัน เมธอด `getText()` จะคืนสตริงที่รู้จำได้

```python
# Step 5: Output the extracted text for each file
for index, result in enumerate(ocr_results, start=1):
    file_path = image_files[index - 1]
    print(f"--- Text from file {file_path} ---")
    print(result.getText())
    print("\n")   # add a blank line for readability
```

### ผลลัพธ์ที่คาดหวัง

การรันสคริปต์เต็มบนสามสกรีนช็อตง่าย ๆ อาจให้ผลลัพธ์ประมาณนี้:

```
--- Text from file YOUR_DIRECTORY/page1.png ---
Invoice #12345
Date: 2024‑07‑01
Total: $256.78

--- Text from file YOUR_DIRECTORY/page2.jpg ---
Welcome to the Annual Report
Prepared by: Finance Dept.

--- Text from file YOUR_DIRECTORY/page3.tif ---
© 2025 Acme Corp. All rights reserved.
```

หากภาพไม่มีอักขระที่สามารถรับรู้ได้ คุณจะเห็นสตริงว่าง—ไม่มีการพัง, และคุณสามารถตัดสินใจว่าจะแจ้งไฟล์นั้นให้ตรวจสอบด้วยมือหรือไม่

## โบนัส: ปรับแต่งความแม่นยำของ OCR

Aspose OCR มีการตั้งค่าเสริมหลายอย่างที่คุณอาจอยากลอง:

| การตั้งค่า | ทำอะไร | เมื่อใดใช้ |
|-----------|--------|------------|
| `ocr_engine.setLanguage('eng')` | บังคับใช้โมเดลภาษาอังกฤษ (ลดผลบวกเท็จ) | เอกสารส่วนใหญ่เป็นภาษาอังกฤษ |
| `ocr_engine.setResolution(300)` | ปรับปรุงความแม่นยำบนสแกนที่ dpi ต่ำ | สแกนที่ต่ำกว่า 200 dpi |
| `ocr_engine.setPageSegMode('single_block')` | ถือภาพทั้งหมดเป็นบล็อกข้อความเดียว | ใบเสร็จหรือบัตรประชาชนแบบง่าย |

คุณสามารถเพิ่มบรรทัดเหล่านี้ได้ทันทีหลังจากสร้าง `ocr_engine`:

```python
ocr_engine.setLanguage('eng')
ocr_engine.setResolution(300)
ocr_engine.setPageSegMode('single_block')
```

## ปัญหาที่พบบ่อย & วิธีหลีกเลี่ยง

1. **TIFF หลายหน้า** – TIFF แบบหลายหน้าอาจใช้ RAM เป็นกิกะไบต์เมื่อโหลดทั้งหมดพร้อมกัน แยกไฟล์เป็นภาพหน้าเดียวก่อนส่งให้ `processMultiple`  
2. **สคริปต์ที่ไม่ใช่ละติน** – หากต้อง **ดึงข้อความจากรูปภาพ** ที่มีอักขระ Cyrillic, Arabic หรือ Chinese, เปลี่ยนรหัสภาษาให้ตรง (`'rus'`, `'ara'`, `'chi_sim'`)  
3. **พาธไฟล์มีช่องว่าง** – พาธ Windows ที่มีช่องว่างอาจทำให้เกิด `FileNotFoundError` ใช้ raw string (`r"C:\My Folder\image.png"`) หรือ `os.path.abspath`  

การจัดการปัญหาเหล่านี้ตั้งแต่ต้นจะช่วยคุณหลีกเลี่ยงข้อผิดพลาดรันไทม์ที่สับสนในภายหลัง

---

## ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นสคริปต์สมบูรณ์ที่คุณสามารถคัดลอก‑วางลงในไฟล์ชื่อ `batch_ocr.py` รวมการปรับแต่งตามแนวปฏิบัติที่ดีที่สุดที่กล่าวถึงข้างต้น

```python
# batch_ocr.py
# -------------------------------------------------
# Complete example: extract text from images using Aspose OCR (Python)
# -------------------------------------------------

from asposeocr import OcrEngine
import os

# -------------------------------------------------
# Configuration – adjust these values for your environment
# -------------------------------------------------
IMAGE_DIR = "YOUR_DIRECTORY"   # <-- replace with your folder path
SUPPORTED_EXT = (".png", ".jpg", ".jpeg", ".tif", ".tiff")

# Build a list of image file paths automatically
image_files = [
    os.path.join(IMAGE_DIR, f)
    for f in os.listdir(IMAGE_DIR)
    if f.lower().endswith(SUPPORTED_EXT)
]

if not image_files:
    print("⚠️ No supported image files found in the specified directory.")
    exit(1)

# -------------------------------------------------
# Initialize OCR engine with optional tweaks
# -------------------------------------------------
ocr_engine = OcrEngine()
ocr_engine.setLanguage('eng')          # English language model
ocr_engine.setResolution(300)          # Boost low‑dpi accuracy
ocr_engine.setPageSegMode('single_block')  # Treat whole image as one block

# -------------------------------------------------
# Run batch OCR and handle potential errors
# -------------------------------------------------
try:
    ocr_results = ocr_engine.processMultiple(image_files)
except Exception as exc:
    print(f"❌ OCR processing failed: {exc}")
    ocr_results = []

# -------------------------------------------------
# Display extracted text
# -------------------------------------------------
for idx, result in enumerate(ocr_results, start=1):
    file_path = image_files[idx - 1]
    print(f"--- Text from file {file_path} ---")
    print(result.getText())
    print("\n")
```

บันทึก, เปิดใช้งาน virtual environment ของคุณ, แล้วรัน:

```bash
python batch_ocr.py
```

คุณควรเห็นสตริงที่ดึงออกมาถูกพิมพ์ที่คอนโซล, พร้อมสำหรับการประมวลผลต่อ (เช่น บันทึกลงฐานข้อมูลหรือป้อนให้โมเดลภาษาธรรมชาติ)

---

## สรุป

ในคู่มือนี้เราได้แสดงวิธี **ดึงข้อความจากรูปภาพ** ด้วย Aspose OCR สำหรับ Python, ครอบคลุมตั้งแต่การติดตั้งจนถึงการประมวลผลแบบแบตช์และการจัดการข้อผิดพลาด สคริปต์นี้กระชับ, ทำงานเต็มรูปแบบ, และง่ายต่อการขยาย—ไม่ว่าคุณจะต้อง **แปลงข้อความจากภาพที่สแกน** เป็นไฟล์ CSV, ป้อนดัชนีการค้นหา, หรือเพียงอัตโนมัติการป้อนข้อมูล

พร้อมก้าวต่อไปหรือยัง? ลองผสาน pipeline OCR นี้กับเครื่องมือรวม PDF เพื่อสร้าง PDF ที่ค้นหาได้, หรือเชื่อมต่อกับ trigger ของคลาวด์สตอเรจเพื่อให้ทุกการอัปโหลดสแกนถูกประมวลผลทันที ความเป็นไปได้ไม่มีที่สิ้นสุด, และคุณมีพื้นฐานที่มั่นคงเพื่อสร้างต่อ

มีคำถามหรือไอเดียปรับปรุง? แสดงความคิดเห็นด้านล่าง, แล้วขอให้สนุกกับการเขียนโค้ด!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}