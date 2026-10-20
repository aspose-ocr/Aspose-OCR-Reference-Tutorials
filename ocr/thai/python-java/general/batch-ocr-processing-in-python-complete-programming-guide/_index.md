---
category: general
date: 2026-06-25
description: การประมวลผล OCR แบบชุดใน Python ง่ายขึ้น เรียนรู้วิธีดึงข้อความจากชุดรูปภาพและเชี่ยวชาญการดึงข้อความจากรูปภาพแบบชุดด้วยเธรดขนาน
draft: false
keywords:
- batch OCR processing
- extract text from image batch
- batch image text extraction
language: th
og_description: การประมวลผล OCR แบบชุดใน Python ช่วยให้คุณดึงข้อความจากชุดภาพได้อย่างรวดเร็ว
  บทเรียนนี้จะพาคุณผ่านการทำ OCR แบบขนานพร้อมตัวอย่างโค้ดที่ชัดเจน
og_title: การประมวลผล OCR แบบชุดใน Python – คู่มือฉบับสมบูรณ์
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Batch OCR processing in Python made easy. Learn how to extract text
    from image batch and master batch image text extraction with parallel threads.
  headline: Batch OCR Processing in Python – Complete Programming Guide
  type: TechArticle
- description: Batch OCR processing in Python made easy. Learn how to extract text
    from image batch and master batch image text extraction with parallel threads.
  name: Batch OCR Processing in Python – Complete Programming Guide
  steps:
  - name: Missing or Corrupt Images
    text: If an image can’t be opened, most OCR libraries raise an exception that
      aborts the whole batch. Wrap the call in a `try/except` inside the batch function
      or filter out problematic files beforehand (see the sanity check in Step 1).
  - name: Language & DPI Settings
    text: For multilingual documents, pass a `langs` parameter (e.g., `langs=['en',
      'de']`). If your scans are low‑resolution, consider pre‑processing with `Pillow`
      to upscale to 300 DPI before OCR—this often boosts accuracy.
  - name: Memory Constraints
    text: 'Eight threads can eat RAM, especially with large images. If you hit memory
      errors, lower `max_threads` or process the list in smaller chunks:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: การประมวลผล OCR แบบชุดใน Python – คู่มือการเขียนโปรแกรมครบถ้วน
url: /th/python-java/general/batch-ocr-processing-in-python-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# การประมวลผล OCR แบบชุดใน Python – คู่มือการเขียนโปรแกรมฉบับสมบูรณ์

เคยต้องการ **การประมวลผล OCR แบบชุด** แต่ไม่แน่ใจว่าจะรันอย่างมีประสิทธิภาพบนหลายสิบหน้าแบบสแกนหรือไม่? คุณไม่ได้เป็นคนเดียว—นักพัฒนามักเจออุปสรรคเมื่อต้องสกัดข้อความจากชุดภาพโดยไม่ทำให้ CPU ทำงานหนักเกินไป  

ในคู่มือนี้เราจะสาธิตวิธีที่ง่ายต่อการ **สกัดข้อความจากชุดภาพ** ด้วยเครื่องมือ OCR ของ Python, รันงานพร้อมกับสูงสุดถึงแปดเธรด, และสุดท้ายดูว่าภาพแต่ละภาพให้จำนวนอักขระเท่าไหร่ สิ้นสุดแล้วคุณจะได้สคริปต์ที่นำกลับมาใช้ใหม่ได้สำหรับ **การสกัดข้อความจากภาพแบบชุด** อย่างมืออาชีพ

## สิ่งที่บทเรียนนี้ครอบคลุม

เราจะเดินผ่านสามขั้นตอนที่ใช้งานได้จริง:

1. สร้างรายการไฟล์ภาพที่ต้องการให้ OCR จดจำ  
2. เรียกใช้เครื่องมือ OCR แบบขนานด้วย `max_threads=8`  
3. วนลูปผลลัพธ์และพิมพ์สรุปสั้น ๆ  

ไม่มีบริการภายนอก, ไม่มีไลบรารีที่ซับซ้อน—เพียง Python ธรรมดาและ wrapper OCR ปกติ (เช่น `ocr` จาก `easyocr` หรือ wrapper ที่กำหนดเอง) หากคุณมี Python 3.8+ และติดตั้งแพคเกจ OCR แล้ว คุณก็พร้อมคัดลอก‑วางและรันได้ทันที

---

## ขั้นตอนที่ 1: เตรียมรายการไฟล์ภาพสำหรับการประมวลผล OCR แบบชุด

สิ่งแรกที่คุณต้องมีคือคอลเลกชันของเส้นทางไฟล์ภาพ คิดว่าเป็นรายการช็อปปิ้งสำหรับเครื่อง OCR; แต่ละรายการชี้ไปที่ไฟล์ PNG, JPEG หรือ TIFF ที่มีข้อความที่คุณต้องการอ่าน

```python
# Step 1: Prepare a list of image files to be recognized
image_files = [
    "YOUR_DIRECTORY/page1.png",
    "YOUR_DIRECTORY/page2.png",
    "YOUR_DIRECTORY/page3.png",
    "YOUR_DIRECTORY/page4.png",
    "YOUR_DIRECTORY/page5.png"
]

# Quick sanity check – make sure the files exist
import os
missing = [p for p in image_files if not os.path.isfile(p)]
if missing:
    raise FileNotFoundError(f"These files are missing: {missing}")
```

**ทำไมสิ่งนี้สำคัญ:**  
การสร้างรายการล่วงหน้าช่วยให้เครื่อง OCR ทำงานในโหมดชุดจริง ๆ อีกทั้งยังให้จุดเดียวที่คุณสามารถเพิ่มหรือเอาไฟล์ออกได้โดยไม่ต้องแก้ไขตรรกะการประมวลผลในภายหลัง การตรวจสอบความสมบูรณ์ช่วยป้องกันการพัง “ไฟล์ไม่พบ” กลางทางเมื่อรันงานยาว ๆ

---

## ขั้นตอนที่ 2: รัน OCR บนชุดภาพด้วยเธรดขนาน (สกัดข้อความจากชุดภาพ)

ต่อไปเราจะส่งรายการให้กับเครื่อง OCR ส่วนใหญ่ที่มีเมธอด `recognize_batch` ที่รับอาร์กิวเมนต์ `max_threads` การตั้งค่าเป็น `8` บอกไลบรารีให้สร้างเธรดทำงานแปดตัว ซึ่งบน CPU ควอด‑คอร์ที่มี hyper‑threading จะช่วยลดเวลาประมวลผลอย่างมาก

```python
# Step 2: Run OCR on the batch, allowing up to 8 parallel threads
# Assuming `ocr` is a module that provides OcrEngine with recognize_batch()
import ocr

batch_results = ocr.OcrEngine.recognize_batch(image_files, max_threads=8)

# batch_results is a list of Result objects, each with a .text attribute
```

**ทำไมการทำขนานจึงช่วยได้:**  
OCR ใช้ CPU อย่างหนัก; แต่ละภาพต้องผ่านเครือข่ายประสาทเทียมหรือเอนจินเก่า การรันต่อเนื่องกันอาจช้าอย่างน่าเจ็บปวด โดยเฉพาะกับสแกนความละเอียดสูง เธรดขนานทำให้ทุกคอร์ทำงานเต็มที่ แปลงงาน 5 นาทีให้เหลือ 1 นาทีบนฮาร์ดแวร์ทั่วไป

**เคล็ดลับ:** หากคุณใช้ `easyocr` การเรียกดูจะเป็น `reader.readtext(image_path, detail=0)` ภายในลูป abstraction `recognize_batch` ของเราซ่อนความซับซ้อนนี้ไว้ แต่คุณก็สามารถแทนที่ด้วย `ThreadPoolExecutor` ของคุณเองได้หากไลบรารีไม่มีการสนับสนุน batch

---

## ขั้นตอนที่ 3: วนลูปผลลัพธ์และสรุปการสกัดข้อความจากภาพแบบชุด

เมื่อ OCR เสร็จสิ้น คุณจะได้รายการอ็อบเจ็กต์ผลลัพธ์ มา zip เส้นทางไฟล์ต้นฉบับกับผลลัพธ์ OCR ที่สอดคล้องกันและพิมพ์บรรทัดสรุปสำหรับแต่ละภาพที่บอกจำนวนอักขระที่ถูกจดจำ

```python
# Step 3: Iterate through the results and display character counts
for file_path, result in zip(image_files, batch_results):
    # result.text holds the raw extracted string
    char_count = len(result.text)
    print(f"{file_path} → {char_count} characters recognized")
```

**สิ่งที่คุณจะเห็น:**  

```
YOUR_DIRECTORY/page1.png → 1245 characters recognized
YOUR_DIRECTORY/page2.png → 987 characters recognized
YOUR_DIRECTORY/page3.png → 1103 characters recognized
YOUR_DIRECTORY/page4.png → 1320 characters recognized
YOUR_DIRECTORY/page5.png → 845 characters recognized
```

**ทำไมขั้นตอนนี้มีประโยชน์:**  
การนับอักขระอย่างรวดเร็วช่วยให้คุณเห็นได้ทันทีว่าภาพใดประมวลผลถูกต้องหรือไม่ จำนวนที่ต่ำกว่าที่คาดอาจบ่งบอกว่าภาพเบลอ, ตั้งค่าภาษาไม่ถูกต้อง, หรือไฟล์เสีย—ปัญหาที่คุณสามารถแก้ไขก่อนดำเนินการวิเคราะห์ต่อไป

---

## โบนัส: การจัดการกรณีขอบและข้อผิดพลาดทั่วไป

### ภาพหายหรือไฟล์เสีย  
หากไม่สามารถเปิดภาพได้ ส่วนใหญ่ไลบรารี OCR จะโยนข้อยกเว้นที่ทำให้ชุดทั้งหมดหยุดทำงาน ห่อการเรียกใน `try/except` ภายในฟังก์ชัน batch หรือกรองไฟล์ที่มีปัญหาก่อน (ดูการตรวจสอบความสมบูรณ์ในขั้นตอน 1)

### การตั้งค่าภาษา & DPI  
สำหรับเอกสารหลายภาษา ให้ส่งพารามิเตอร์ `langs` (เช่น `langs=['en', 'de']`) หากสแกนของคุณความละเอียดต่ำ ให้พิจารณา preprocess ด้วย `Pillow` เพื่ออัปสเกลเป็น 300 DPI ก่อน OCR—มักช่วยเพิ่มความแม่นยำ

### ข้อจำกัดด้านหน่วยความจำ  
แปดเธรดอาจกิน RAM มาก โดยเฉพาะกับภาพขนาดใหญ่ หากเจอข้อผิดพลาดหน่วยความจำ ให้ลด `max_threads` หรือประมวลผลรายการเป็นชิ้นเล็ก ๆ:

```python
from itertools import islice

def chunked(iterable, size):
    it = iter(iterable)
    while True:
        chunk = list(islice(it, size))
        if not chunk:
            break
        yield chunk

for chunk in chunked(image_files, 3):  # process three images at a time
    results = ocr.OcrEngine.recognize_batch(chunk, max_threads=3)
    # handle results...
```

---

## สคริปต์ทำงานเต็มรูปแบบ

รวมทุกอย่างเข้าด้วยกัน นี่คือตัวอย่างที่พร้อมรัน แทนที่ `"YOUR_DIRECTORY"` ด้วยเส้นทางที่มีไฟล์ PNG ของคุณและตรวจสอบให้แน่ใจว่าโมดูล `ocr` ถูกติดตั้งแล้ว

```python
#!/usr/bin/env python3
"""
Batch OCR Processing Script
Extracts text from an image batch using parallel threads and prints character counts.
"""

import os
import ocr  # Replace with your OCR library import, e.g., from easyocr import Reader

# -------------------------------------------------
# Step 1: Define the list of image files
# -------------------------------------------------
image_dir = "YOUR_DIRECTORY"
image_files = [
    os.path.join(image_dir, f"page{i}.png") for i in range(1, 6)
]

# Verify that all files exist
missing = [p for p in image_files if not os.path.isfile(p)]
if missing:
    raise FileNotFoundError(f"Missing image files: {missing}")

# -------------------------------------------------
# Step 2: Run OCR in parallel (max 8 threads)
# -------------------------------------------------
# The OcrEngine is a placeholder – adapt to your library's API
batch_results = ocr.OcrEngine.recognize_batch(image_files, max_threads=8)

# -------------------------------------------------
# Step 3: Report how many characters each image yielded
# -------------------------------------------------
for file_path, result in zip(image_files, batch_results):
    char_count = len(result.text)
    print(f"{file_path} → {char_count} characters recognized")
```

**ผลลัพธ์ที่คาดหวัง** (ตัวเลขของคุณอาจแตกต่าง)

```
YOUR_DIRECTORY/page1.png → 1245 characters recognized
YOUR_DIRECTORY/page2.png → 987 characters recognized
YOUR_DIRECTORY/page3.png → 1103 characters recognized
YOUR_DIRECTORY/page4.png → 1320 characters recognized
YOUR_DIRECTORY/page5.png → 845 characters recognized
```

รันสคริปต์ด้วย `python batch_ocr.py` แล้วดูเทอร์มินัลเต็มไปด้วยสถิติสรุปสั้น ๆ

---

## ภาพรวมเชิงภาพ

![ภาพแผนผังการประมวลผล OCR แบบชุด](image-placeholder.png "แผนผังแสดงขั้นตอนการประมวลผล OCR แบบชุด")

*ข้อความแทนภาพ:* *แผนผังการประมวลผล OCR แบบชุดแสดงการสร้างรายการไฟล์, การทำ OCR ขนาน, และการสรุปผลลัพธ์*

---

## สรุป

ตอนนี้คุณมีพื้นฐานที่มั่นคงสำหรับ **การประมวลผล OCR แบบชุด** ด้วย Python โดยการเตรียมรายการภาพที่สะอาด, ใช้เธรดขนานสำหรับ **สกัดข้อความจากชุดภาพ**, และสรุปผลลัพธ์ คุณสามารถเปลี่ยนงานที่ต้องทำด้วยมือให้เป็นกระบวนการที่เร็วและทำซ้ำได้  

ต่อจากนี้คุณอาจ:

- บันทึก `result.text` แต่ละรายการเป็นไฟล์ `.txt` เพื่อใช้ต่อใน NLP  
- ผสานจำนวนอักขระกับคะแนนความเชื่อมั่นเพื่อกรองหน้าที่คุณภาพต่ำ  
- ผสานสคริปต์เข้ากับเวิร์กโฟลว์การนำเข้าข้อความขนาดใหญ่ เช่น การสร้างดัชนีการค้นหา  

ไม่ว่าคุณจะกำลังดิจิไทซ์เอกสารเก่า, สร้างแอปสแกนใบเสร็จ, หรือเตรียมข้อมูลฝึกโมเดลภาษา แนวคิดในบทนี้สามารถขยายได้ถึงหลายร้อยหรือหลายพันไฟล์โดยปรับแต่งเล็กน้อย  

มีคำถามเกี่ยวกับการตั้งค่าภาษา, การ preprocess ภาพ, หรือการปรับใช้บนคลาวด์? แสดงความคิดเห็นหรือดูบทเรียนที่เกี่ยวข้องเกี่ยวกับ *การ preprocess ภาพใน Python* และ *OCR แบบอะซิงโครนัสด้วย asyncio* ขอให้สนุกกับการเขียนโค้ด!

## สิ่งที่คุณควรเรียนต่อ

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโปรเจกต์ของคุณ

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}