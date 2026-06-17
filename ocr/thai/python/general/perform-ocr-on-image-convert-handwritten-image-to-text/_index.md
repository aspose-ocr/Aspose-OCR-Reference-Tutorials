---
category: general
date: 2026-03-18
description: ทำ OCR บนภาพและดึงข้อความที่เขียนด้วยมือจากรูปถ่าย เรียนรู้วิธีแปลงภาพที่เขียนด้วยมือ
  ดึงข้อความจากไฟล์ JPG และจดจำข้อความจากรูปถ่าย
draft: false
keywords:
- perform OCR on image
- convert handwritten image
- extract text from jpg
- extract handwritten text
- recognize text from photo
language: th
og_description: ทำ OCR บนภาพเพื่อดึงข้อความที่เขียนด้วยมือจากรูปถ่าย บทเรียนนี้แสดงวิธีแปลงภาพที่เขียนด้วยมือและจดจำข้อความจากไฟล์
  JPG
og_title: ทำ OCR บนภาพ – คู่มือเต็มสำหรับข้อความลายมือ
tags:
- OCR
- Python
- Handwriting Recognition
title: ทำ OCR บนภาพ – แปลงภาพที่เขียนด้วยมือเป็นข้อความ
url: /th/python/general/perform-ocr-on-image-convert-handwritten-image-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ทำ OCR บนรูปภาพ – การสกัดข้อความที่เขียนด้วยมือแบบ Full‑Stack

เคยต้องการ **perform OCR on image** ไฟล์แต่ไม่แน่ใจว่าเอนจินจะอ่านลายมือที่ยุ่งยากได้หรือไม่? คุณไม่ได้เป็นคนเดียว ในแอปพลิเคชันหลายกรณีในโลกจริง—เช่นสแกนเนอร์ใบเสร็จค่าใช้จ่ายหรือเครื่องมือจดบันทึก—คุณจะเจอรูปถ่ายของลายมือที่ต้องแปลงเป็นข้อความธรรมดา  

ในคู่มือนี้เราจะสาธิตวิธี **convert handwritten image** ไฟล์, **extract text from jpg**, และแม้กระทั่ง **recognize text from photo** สตรีมโดยใช้ไลบรารีสไตล์ Python เล็ก ๆ ชื่อ `ocr` เมื่อเสร็จคุณจะมีสคริปต์พร้อมรันที่ดึงทุกคำจากโน้ตที่เขียนด้วยมือ ไม่ว่าปากกาจะเขียนสั่นเท่าใดก็ตาม  

## สิ่งที่คุณต้องการ

- Python 3.8+ (โค้ดทำงานบนอินเทอร์พรีเตอร์รุ่นล่าสุดใดก็ได้)
- แพคเกจ `ocr` สมมติ – ติดตั้งด้วย `pip install ocr-lib` (เปลี่ยนเป็นชื่อแพคเกจจริงที่คุณใช้)
- ภาพถ่ายที่ชัดเจนของโน้ตที่เขียนด้วยมือที่บันทึกเป็น `note.jpg` (หรือรูปแบบไฟล์อื่นใด)
- ความอยากรู้อยากเห็นระดับปานกลาง—ไม่ต้องมีพื้นฐาน ML ขั้นสูง

แค่นั้นเอง ไม่ต้องใช้บริการภายนอก ไม่ต้องมี API key เพียงแค่เอนจินในเครื่องที่สามารถ **perform OCR on image** ข้อมูลได้  

![ภาพหน้าจอการทำ OCR บนรูปภาพ](example.png)

*ข้อความแทนภาพ: ภาพหน้าจอการทำ OCR บนรูปภาพที่แสดงตัวแก้ไขโค้ดพร้อมสคริปต์ OCR.*  

## การดำเนินการแบบขั้นตอน

ด้านล่างเราจะแบ่งกระบวนการเป็นชิ้นส่วนขนาดเล็ก แต่ละหัวข้อมีคีย์เวิร์ดเพื่อให้คุณสแกนได้เร็ว และแต่ละบล็อกอธิบาย **ทำไม** เราถึงทำเช่นนั้น—not just **what**.  

### ขั้นตอนที่ 1: ติดตั้งและตรวจสอบไลบรารี OCR

ก่อนที่คุณจะ **perform OCR on image** ไฟล์ ไลบรารีต้องมีอยู่ในสภาพแวดล้อมของคุณ เปิดเทอร์มินัลและรัน:

```bash
pip install ocr-lib
```

> **Pro tip:** หากคุณทำงานใน virtual environment (แนะนำอย่างยิ่ง) ให้เปิดใช้งานก่อน จะทำให้การจัดการ dependencies เป็นระเบียบและหลีกเลี่ยงการชนกันของเวอร์ชัน  

หลังการติดตั้ง ให้ตรวจสอบว่า Python สามารถ import แพคเกจได้:

```python
try:
    import ocr
    print("OCR library loaded successfully.")
except ImportError as e:
    raise SystemExit("Failed to import ocr library. Did you run pip install?") from e
```

หากคุณเห็นข้อความสำเร็จ คุณพร้อมที่จะ **convert handwritten image** ข้อมูลแล้ว  

### ขั้นตอนที่ 2: สร้างอินสแตนซ์ของเอนจินและเลือกโหมดการเขียนมือ

ส่วนใหญ่ OCR engine จะตั้งค่าเริ่มต้นเป็นการจดจำข้อความพิมพ์ เนื่องจากเราต้องการ **extract handwritten text** เราจำเป็นต้องสลับโหมดอย่างชัดเจน ขั้นตอนนี้สำคัญเพราะลายมือมักต้องการการ preprocessing ที่แตกต่าง (เช่นการทำให้เส้นเรียบ)

```python
# Step 2: Initialize the OCR engine
engine = ocr.OcrEngine()

# Tell the engine we’re dealing with handwriting
engine.set_recognition_mode(ocr.RecognitionMode.HANDWRITTEN)

print("Engine configured for handwritten recognition.")
```

*Why this matters:* ตัวอักษรที่เขียนด้วยมืออาจมีขนาดและความเอียงแตกต่างกันอย่างมาก โดยการตั้งค่า `RecognitionMode.HANDWRITTEN` เอนจินจะใช้โมเดลที่ฝึกด้วยตัวอย่างลายมือเชิงโค้ง เพิ่มความแม่นยำอย่างมาก  

### ขั้นตอนที่ 3: โหลดรูปภาพที่ต้องการวิเคราะห์

ตอนนี้เราจริง ๆ แล้ว **perform OCR on image** เนื้อหา วิธี `load_image` รับพาธหรืออ็อบเจกต์ที่คล้ายไฟล์ สำหรับการสาธิต เราจะโหลด JPEG แต่คำสั่งเดียวกันทำงานกับ PNG, BMP หรือแม้แต่หน้า PDF

```python
# Step 3: Load the image file (replace the path with yours)
image_path = "YOUR_DIRECTORY/note.jpg"
engine.load_image(image_path)

print(f"Image '{image_path}' loaded into the OCR engine.")
```

หากรูปของคุณอยู่ในคลาวด์บัคเก็ต ให้ดาวน์โหลดก่อนหรือส่งสตรีม `BytesIO`—`ocr` ยืดหยุ่นพอที่จะจัดการทั้งสองกรณี  

### ขั้นตอนที่ 4: เรียกกระบวนการจดจำ

เมื่อเอนจินพร้อมและรูปภาพอยู่ในหน่วยความจำ เราจึง **perform OCR on image** และดึงข้อความดิบออกมา

```python
# Step 4: Execute recognition
extracted_text = engine.recognize()

print("=== Extracted Text ===")
print(extracted_text)
```

การเรียก `recognize()` จะคืนค่าเป็นสตริง Unicode ธรรมดา สำหรับการใช้ส่วนใหญ่คุณสามารถเขียนลงไฟล์ `.txt` ได้โดยตรง ส่งต่อไปยัง pipeline การประมวลผลภาษาธรรมชาติ หรือแสดงใน GUI  

### ขั้นตอนที่ 5: ตัวเลือก – ทำความสะอาดหรือประมวลผลผลลัพธ์เพิ่มเติม

OCR ลายมือไม่สมบูรณ์แบบ; คุณมักจะเจอการขึ้นบรรทัดใหม่ที่ไม่ต้องการหรืออักขระที่อ่านผิด การทำความสะอาดอย่างรวดเร็วสามารถปรับปรุงผลลัพธ์ต่อไปได้

```python
# Step 5: Simple post‑processing (optional)
def tidy(text):
    # Collapse multiple spaces, strip leading/trailing whitespace
    return "\n".join(line.strip() for line in text.splitlines() if line.strip())

clean_text = tidy(extracted_text)

print("\n=== Cleaned Text ===")
print(clean_text)
```

อย่าลังเลที่จะต่อเชื่อม spell‑checkers, language models, หรือ regex ที่กำหนดเองตามโดเมนของคุณ  

### สคริปต์เต็ม – พร้อมคัดลอกและวาง

รวมทุกอย่างเข้าด้วยกัน นี่คือโปรแกรมที่ทำงานได้เต็มรูปแบบซึ่ง **extracts handwritten text** จาก JPEG และพิมพ์ผลลัพธ์ที่เรียบร้อย

```python
# -*- coding: utf-8 -*-
"""
Complete example: Perform OCR on image to extract handwritten text.
"""

# -------------------------------------------------
# Step 1: Import the OCR library and create an engine
# -------------------------------------------------
import ocr

engine = ocr.OcrEngine()

# -------------------------------------------------
# Step 2: Set the engine to recognize handwritten text
# -------------------------------------------------
engine.set_recognition_mode(ocr.RecognitionMode.HANDWRITTEN)

# -------------------------------------------------
# Step 3: Load the image you want to analyze
# -------------------------------------------------
image_path = "YOUR_DIRECTORY/note.jpg"   # <-- change this to your file
engine.load_image(image_path)

# -------------------------------------------------
# Step 4: Perform recognition and output the extracted text
# -------------------------------------------------
raw_text = engine.recognize()
print("=== Raw OCR Output ===")
print(raw_text)

# -------------------------------------------------
# Step 5: Optional cleanup for nicer display
# -------------------------------------------------
def tidy(text):
    return "\n".join(line.strip() for line in text.splitlines() if line.strip())

clean_text = tidy(raw_text)
print("\n=== Cleaned OCR Output ===")
print(clean_text)
```

**Expected output** (ข้อความจริงของคุณจะต่างออกไปแน่นอน):

```
=== Raw OCR Output ===
Meeting notes:
- Discuss project timeline
- Assign tasks to John, Ana
- Review budget Q3

=== Cleaned OCR Output ===
Meeting notes:
- Discuss project timeline
- Assign tasks to John, Ana
- Review budget Q3
```

หากคุณเห็นข้อความเป็นอักขระไร้ความหมาย ให้ตรวจสอบคุณภาพของภาพ (แสงดี, เบลอต่ำ) และตรวจสอบว่าคุณอยู่ในโหมด `HANDWRITTEN` ทั้งสองปัจจัยนี้เป็นสาเหตุหลักของข้อผิดพลาดในการจดจำส่วนใหญ่  

## คำถามที่พบบ่อย (FAQ)

| Question | Answer |
|----------|--------|
| **Can I use this to extract text from a PNG?** | แน่นอน `engine.load_image("scan.png")` ทำงานเช่นเดียวกัน |
| **What if my image is a PDF page?** | แปลงหน้าดังกล่าวเป็นภาพก่อน (เช่นด้วย `pdf2image`) แล้วจึงส่งให้เอนจิน |
| **Is the library thread‑safe?** | ใช่ คุณสามารถสร้างอ็อบเจกต์ `OcrEngine` แยกต่างหากต่อแต่ละเธรด |
| **How does this differ from `pytesseract`?** | `ocr` แยกการทำงานของไบนารี Tesseract ออกและรวมโมเดลลายมือในตัว ทำให้ไม่ต้องติดตั้งไฟล์ executable ภายนอก |
| **What if I need to **extract text from JPG** files in bulk?** | ห่อสคริปต์ในลูป หรือใช้ `engine.load_image` กับแต่ละไฟล์และเก็บผลลัพธ์ในรายการหรือ CSV |

## กรณีขอบและแนวทางปฏิบัติที่ดีที่สุด

1. **Low‑contrast photos** – เพิ่มความคอนทราสต์โดยโปรแกรมก่อนโหลด, หรือใช้ `engine.apply_preprocessing('contrast', level=2)`  
2. **Mixed printed & handwritten** – รันสองรอบ: ครั้งแรกด้วย `HANDWRITTEN`, ครั้งที่สองด้วย `PRINTED` แล้วรวมผลลัพธ์เข้าด้วยกัน  
3. **Large images** – ลดขนาดลงประมาณความกว้าง ~1500 px; OCR engine มักทำงานเร็วขึ้นกับบัฟเฟอร์ขนาดเล็กโดยไม่สูญเสียความแม่นยำ  
4. **Unicode characters** – ไลบรารีคืนค่าเป็นสตริง UTF‑8 จึงสามารถจัดการอีโมจิ, ตัวอักษรที่มีสำเนียง, หรือสัญลักษณ์คณิตศาสตร์ได้โดยตรง  

## สรุป

เราเพิ่งเดินผ่านตัวอย่างจริงของการ **perform OCR on image** ไฟล์โดยมุ่งเน้นที่โน้ตที่เขียนด้วยมือ โดยการติดตั้งแพคเกจ `ocr`, ตั้งค่าเอนจินเป็นโหมด `HANDWRITTEN`, โหลดรูปภาพ, และเรียก `recognize()` คุณสามารถ **convert handwritten image** เป็นข้อความที่สะอาดและค้นหาได้  

จากนี้คุณอาจ **extract text from jpg** ไฟล์เป็นจำนวนมาก, ส่งผลลัพธ์ไปยังแอปจดบันทึก, หรือรวมกับการสังเคราะห์เสียงสำหรับการเข้าถึง ความเป็นไปได้ไม่มีขีดจำกัด และโค้ดข้างบนให้พื้นฐานที่มั่นคงสำหรับการทดลอง  

มีวิธีการหรือฟอร์แมตไฟล์อื่นที่คุณอยากแชร์? หรือเทคนิค preprocessing ที่แปลกใหม่? แสดงความคิดเห็นและเราจะคุยต่อกันต่อไป ขอให้สนุกกับการเขียนโค้ดและเปลี่ยนลายมือเป็นทองดิจิทัล!  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}