---
category: general
date: 2026-08-12
description: ใช้ Python และ Aspose AI ทำ OCR บนภาพเพื่อสกัดข้อความจากภาพและเพิ่มความแม่นยำของ
  OCR ด้วยตัวประมวลผลหลังการตรวจสอบการสะกดคำ
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- run OCR on image
- extract text from image
- OCR text correction
- improve OCR accuracy
- load image for OCR
language: th
lastmod: 2026-08-12
og_description: ทำ OCR บนภาพด้วย Python และดึงข้อความจากภาพได้ทันที พร้อมปรับปรุงความแม่นยำของ
  OCR ด้วยการประมวลผลหลังจาก AI ของ Aspose
og_image_alt: Diagram showing the run OCR on image workflow in Python
og_title: ทำ OCR บนภาพด้วย Python – คู่มือเต็ม
schemas:
- author: Aspose
  dateModified: '2026-08-12'
  description: Run OCR on image using Python and Aspose AI to extract text from image
    and improve OCR accuracy with a spell‑checking post‑processor.
  headline: Run OCR on image with Python – step‑by‑step guide
  type: TechArticle
tags:
- OCR
- Python
- Aspose
- Image Processing
title: ทำ OCR บนภาพด้วย Python – คู่มือขั้นตอนโดยละเอียด
url: /th/python/general/run-ocr-on-image-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# รัน OCR บนรูปภาพด้วย Python – คู่มือขั้นตอนโดยละเอียด

หากคุณต้องการ **run OCR on image** ไฟล์ใน Python, คู่มือนี้จะพาคุณผ่านขั้นตอนทั้งหมด คุณจะได้เรียนรู้วิธี **extract text from image**, ใช้ **OCR text correction**, และ **improve OCR accuracy** ด้วยเพียงไม่กี่บรรทัดของโค้ด

การประมวลผลเอกสารสแกน, ใบเสร็จ, หรือภาพหน้าจอมักให้ผลลัพธ์เป็นข้อความที่มีเสียงรบกวน ด้วยการแนบ post‑processing ตรวจสอบการสะกด คุณสามารถเปลี่ยนผลลัพธ์ OCR ดิบให้เป็นเนื้อหาที่สะอาดและค้นหาได้โดยไม่ต้องเปลี่ยนไปใช้เครื่องมืออื่น คู่มือนี้ครอบคลุมทุกอย่างที่คุณต้องการ—ตั้งแต่การโหลดรูปภาพจนถึงการแสดงผลลัพธ์ที่แก้ไขแล้ว

## ข้อกำหนดเบื้องต้น

* ติดตั้ง Python 3.9 หรือใหม่กว่า
* เข้าถึงแพ็กเกจ Aspose.OCR และ Aspose.AI สำหรับ Python (หรือ wrapper แบบโอเพ่นซอร์สที่เทียบเท่า)
* รูปภาพตัวอย่าง (เช่น `sample.png`) ที่วางไว้ในไดเรกทอรีที่รู้จัก
* ความคุ้นเคยพื้นฐานกับฟังก์ชันของ Python และโค้ดเชิงวัตถุ

```bash
pip install aspose-ocr aspose-ai
```

> **เคล็ดลับ:** ใช้ virtual environment (`python -m venv .venv`) เพื่อแยกการพึ่งพาออกจากกัน

## ขั้นตอนที่ 1: Run OCR on image – สร้างอินสแตนซ์ของเอนจิน

ขั้นตอนแรกคือการสร้างอ็อบเจ็กต์ `OcrEngine` อ็อบเจ็กต์นี้บรรจุการกำหนดค่า OCR engine และให้เมธอดสำหรับการจัดการรูปภาพและการจดจำ

```python
from aspose.ocr import OcrEngine

# Initialize the OCR engine with default settings
ocr_engine = OcrEngine()
```

การสร้างเอนจินเพียงครั้งเดียวและนำมาใช้ซ้ำกับหลายรูปภาพช่วยลดภาระการเริ่มต้นและทำให้การตั้งค่าคงที่ตลอดเซสชัน

## ขั้นตอนที่ 2: Load image for OCR

ก่อนที่การจดจำจะเกิดขึ้น เอนจินต้องรู้ว่าต้องวิเคราะห์รูปภาพใด เมธอด `load_image` รับพาธไฟล์หรือสตรีมไบนารี

```python
# Provide the full path to your image file
image_path = "YOUR_DIRECTORY/sample.png"
ocr_engine.load_image(image_path)
```

> **ทำไมเรื่องนี้ถึงสำคัญ:** การโหลดรูปภาพอย่างถูกต้องเป็นพื้นฐานสำหรับ OCR ที่แม่นยำ การใช้รูปภาพความละเอียดสูง (300 dpi หรือมากกว่า) มักจะ **improves OCR accuracy** เพราะเอนจินสามารถแยกอักขระได้ชัดเจนขึ้น

## ขั้นตอนที่ 3: Extract text from image – ทำการจดจำพื้นฐาน

เมื่อโหลดรูปภาพแล้ว คุณสามารถเรียก `recognize()` เพื่อรับอ็อบเจ็กต์ผลลัพธ์ ผลลัพธ์จะมีข้อความดิบ, คะแนนความมั่นใจ, และอาจมีกรอบล้อมรอบแต่ละคำ

```python
# Run the OCR process
plain_result = ocr_engine.recognize()   # returns a Result object

# The raw OCR output is accessible via the .text attribute
print("Raw OCR output:")
print(plain_result.text)
```

ในขั้นตอนนี้คุณได้ **run OCR on image** สำเร็จและดึงอักขระดิบออกมาแล้ว อย่างไรก็ตาม ข้อความอาจมีการสะกดผิด โดยเฉพาะสำหรับการสแกนคุณภาพต่ำ

## ขั้นตอนที่ 4: OCR text correction – แนบ post‑processing spell‑checker

Aspose AI มี pipeline post‑processing ที่ยืดหยุ่น โดยการเชื่อมต่อ spell‑checker ที่กำหนดเอง คุณสามารถแก้ไขข้อผิดพลาด OCR ทั่วไป (เช่น “l” กับ “1”, “O” กับ “0”)

```python
from aspose.ai import AsposeAI
from my_spellchecker import MySpellChecker   # your own implementation

# Initialize the AI engine and set the post‑processor
ai_engine = AsposeAI()
ai_engine.set_post_processor(MySpellChecker())

# Run the post‑processor on the plain OCR result
corrected_result = ai_engine.run_postprocessor(plain_result)
```

**วิธีการทำงานของ spell‑checker:** `MySpellChecker` ควรทำเมธอด `process(text: str) -> str` ภายในคุณสามารถใช้ไลบรารีเช่น `pyspellchecker` หรือ `symspellpy` เพื่อแทนที่ลำดับคำที่ไม่น่าเป็นไปได้ด้วยคำที่ตรวจสอบจากพจนานุกรม

```python
# Example implementation (very simple)
from spellchecker import SpellChecker

class MySpellChecker:
    def __init__(self):
        self.spell = SpellChecker()

    def process(self, text: str) -> str:
        corrected = []
        for word in text.split():
            corrected.append(self.spell.correction(word))
        return " ".join(corrected)
```

## ขั้นตอนที่ 5: แสดงข้อความ OCR ดั้งเดิมและที่แก้ไขแล้ว

สุดท้าย ให้เปรียบเทียบผลลัพธ์ดิบและที่แก้ไขแล้ว สิ่งนี้ช่วยให้คุณตรวจสอบว่า **OCR text correction** จริงๆ แล้ว **improved OCR accuracy** สำหรับกรณีการใช้งานของคุณ

```python
print("\nOriginal :", plain_result.text)
print("Corrected:", corrected_result.text)
```

### ผลลัพธ์ที่คาดหวัง

```
Original : Th1s is a s4mpl3 rec3pt with som3 err0rs.
Corrected: This is a simple receipt with some errors.
```

บรรทัดที่แก้ไขแสดงว่า spell‑checker แทนที่การจดจำ OCR ที่ผิดพลาดทั่วไป (`Th1s` → `This`, `s4mpl3` → `simple`, `rec3pt` → `receipt`, `som3` → `some`, `err0rs` → `errors`).

## ขั้นตอนที่ 6: Improve OCR accuracy – รายการตรวจสอบแนวปฏิบัติที่ดีที่สุด

แม้จะมี post‑processing แล้ว คุณก็ยังสามารถเพิ่มคุณภาพพื้นฐานของ OCR engine ได้:

| รายการตรวจสอบ | ทำไมถึงช่วย |
|----------------|--------------|
| **ใช้ภาพความละเอียดสูง (≥300 dpi)** | ข้อมูลพิกเซลที่มากขึ้นช่วยลดความคลุมเงือของอักขระ |
| **แปลงภาพสีเป็นระดับสีเทา** | กำจัดสัญญาณรบกวนสีที่อาจทำให้เอนจินสับสน |
| **ทำการ deskew ภาพ** | ทำให้ข้อความเอียงตรงขึ้น ป้องกันข้อผิดพลาดการตัดบรรทัด |
| **กำหนดภาษา/โลคัลอย่างชัดเจน** | ชี้นำตัวจดจำไปสู่ชุดอักขระที่ถูกต้อง |
| **เปิดใช้งาน language model** (หากไลบรารีรองรับ) | ให้การพยากรณ์ที่รับรู้บริบท ช่วย **improving OCR accuracy** เพิ่มเติม |

คุณสามารถดำเนินการขั้นตอน preprocessing เหล่านี้ด้วย Pillow หรือ OpenCV ก่อนส่งภาพให้กับ `ocr_engine`.

```python
from PIL import Image, ImageOps
import cv2
import numpy as np

def preprocess_image(path: str) -> str:
    # Load with Pillow, convert to grayscale, and increase contrast
    img = Image.open(path).convert("L")
    img = ImageOps.autocontrast(img, cutoff=2)

    # Save a temporary preprocessed file
    temp_path = "temp_preprocessed.png"
    img.save(temp_path)
    return temp_path

# Use the preprocessor
preprocessed_path = preprocess_image(image_path)
ocr_engine.load_image(preprocessed_path)
```

## สคริปต์ที่สามารถรันได้เต็มรูปแบบ

เมื่อรวมทุกอย่างเข้าด้วยกัน สคริปต์ต่อไปนี้พร้อมให้คัดลอก‑วางลงในไฟล์ชื่อ `run_ocr.py` และรัน

```python
# run_ocr.py
from aspose.ocr import OcrEngine
from aspose.ai import AsposeAI
from my_spellchecker import MySpellChecker
from PIL import Image, ImageOps

def preprocess_image(path: str) -> str:
    img = Image.open(path).convert("L")
    img = ImageOps.autocontrast(img, cutoff=2)
    temp_path = "temp_preprocessed.png"
    img.save(temp_path)
    return temp_path

def main():
    # 1️⃣ Initialize OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load and preprocess the image
    raw_path = "YOUR_DIRECTORY/sample.png"
    processed_path = preprocess_image(raw_path)
    ocr_engine.load_image(processed_path)

    # 3️⃣ Perform basic OCR
    plain_result = ocr_engine.recognize()

    # 4️⃣ Run OCR text correction
    ai_engine = AsposeAI()
    ai_engine.set_post_processor(MySpellChecker())
    corrected_result = ai_engine.run_postprocessor(plain_result)

    # 5️⃣ Show both results
    print("\nOriginal :", plain_result.text)
    print("Corrected:", corrected_result.text)

if __name__ == "__main__":
    main()
```

การรันสคริปต์จะแสดงข้อความดั้งเดิมและที่แก้ไข ยืนยันว่าคุณได้ **run OCR on image**, **extracted text from image**, และ **improved OCR accuracy** ผ่าน **OCR text correction** อย่างสำเร็จ

## สรุป

ตอนนี้คุณรู้วิธี **run OCR on image** ไฟล์ใน Python, ดึงข้อความดิบ, และใช้ post‑processing spell‑checker เพื่อให้ได้ผลลัพธ์ที่สะอาดยิ่งขึ้น โดยทำตามรายการตรวจสอบสำหรับ **improve OCR accuracy** คุณสามารถปรับใช้กระบวนการนี้กับใบเสร็จ, ใบแจ้งหนี้, บัตรประจำตัว, หรือเอกสารสแกนใด ๆ

### ขั้นตอนต่อไปคืออะไร?

* สำรวจ **language‑specific dictionaries** สำหรับ OCR หลายภาษา.
* ผสาน pipeline กับฐานข้อมูลหรือดัชนีการค้นหา (เช่น Elasticsearch) เพื่อทำให้ข้อความที่ดึงออกมาสามารถค้นหาได้.
* แทนที่ spell‑checker แบบง่ายด้วยโมเดลภาษาแบบ neural (เช่น การแก้ไขแบบ GPT) เพื่อความแม่นยำที่สูงขึ้น

คุณสามารถทดลองใช้เทคนิคการ preprocessing รูปภาพต่าง ๆ, post‑processor ต่าง ๆ, หรือ OCR engine ทางเลือกอื่นได้ตามต้องการ แพทเทิร์นหลัก—**run OCR on image → extract text from image → OCR text correction → improve OCR accuracy**—ยังคงเหมือนเดิม ให้พื้นฐานที่แข็งแรงสำหรับโครงการดิจิไทเซชันเอกสารใด ๆ

## สิ่งที่คุณควรเรียนต่อไป

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดซึ่งต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานครบถ้วนพร้อมคำอธิบายขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการนำไปใช้แบบต่าง ๆ ในโครงการของคุณ

- [Convert Image to Text: Extract Text from Image Using Aspose OCR (Python)](/ocr/english/python/general/convert-image-to-text-extract-text-from-image-using-aspose-o/)
- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}