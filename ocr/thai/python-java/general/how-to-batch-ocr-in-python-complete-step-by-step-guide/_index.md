---
category: general
date: 2026-06-28
description: วิธีทำ OCR เป็นชุดโดยใช้ Python เรียนรู้การทำ OCR หลายภาพ แยกข้อความจากไฟล์
  PNG และแปลงภาพเป็นข้อความด้วยบทเรียน OCR แบบเต็มใน Python
draft: false
keywords:
- how to batch OCR
- ocr multiple images
- extract text from png
- convert image to text
- python ocr tutorial
language: th
og_description: วิธีทำ OCR แบบชุดใน Python ได้อธิบายไว้ในประโยคแรก ติดตามบทแนะนำ OCR
  ด้วย Python นี้เพื่อดึงข้อความจากไฟล์ PNG อย่างมีประสิทธิภาพ.
og_title: วิธีทำ OCR แบบกลุ่มใน Python – คู่มือการเขียนโปรแกรมเต็ม
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: How to batch OCR using Python. Learn to OCR multiple images, extract
    text from PNG, and convert image to text with a full Python OCR tutorial.
  headline: How to Batch OCR in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: How to batch OCR using Python. Learn to OCR multiple images, extract
    text from PNG, and convert image to text with a full Python OCR tutorial.
  name: How to Batch OCR in Python – Complete Step‑by‑Step Guide
  steps:
  - name: '**Why set the language?**'
    text: '**Why set the language?**'
  - name: '**Why use a batch operation?**'
    text: '**Why use a batch operation?**'
  - name: '**Why a ThreadPoolExecutor?**'
    text: '**Why a ThreadPoolExecutor?**'
  - name: '**Why enumerate the results?**'
    text: '**Why enumerate the results?**'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: วิธีทำ OCR แบบแบตช์ใน Python – คู่มือขั้นตอนเต็ม
url: /th/python-java/general/how-to-batch-ocr-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีทำ Batch OCR ด้วย Python – คู่มือขั้นตอนครบถ้วน

เคยสงสัย **วิธีทำ batch OCR** กองหน้าเอกสารสแกนหลายหน้าโดยไม่ต้องเขียนลูปที่ทำให้ UI ค้างหรือไม่? คุณไม่ได้เป็นคนเดียว การประมวลผลไฟล์ PNG หลายสิบไฟล์ทีละหนึ่งอาจรู้สึกเหมือนดูสีแห้ง โดยเฉพาะเมื่อแต่ละภาพต้องใช้เวลาหนึ่งสองวินาทีในการถอดรหัส  

ในบทเรียนนี้เราจะสาธิตวิธีที่สะอาดและไม่บล็อก UI เพื่อ **OCR หลายภาพ** พร้อมกัน, **extract text from PNG** files, และ **convert image to text** ด้วยเอนจิน OCR ของ Python สมัยใหม่ เมื่อจบคุณจะได้สคริปต์พร้อมรันที่สามารถนำไปใช้ในโปรเจกต์ใดก็ได้ – เหมาะสำหรับ *python ocr tutorial* อย่างรวดเร็วหรืองาน batch ระดับ production

## สิ่งที่คุณจะสร้าง

- เริ่มต้นเอนจิน OCR และตั้งค่าภาษาเป็น Latin (หรือภาษาอื่นที่คุณต้องการ)  
- ส่งรายการเส้นทางไฟล์ภาพ (PNG ในตัวอย่างของเรา) ให้กับเอนจิน  
- เรียกการทำงานแบบ batch ที่จะคืนออบเจ็กต์แบบ Future  
- ดึงผลลัพธ์ทั้งหมดพร้อมกันด้วย thread pool เพื่อให้เธรดหลักของคุณว่างอยู่  
- พิมพ์ข้อความที่ถูกจดจำสำหรับแต่ละหน้า โดยแยกอย่างชัดเจน

ไม่มีเวทมนตร์ลับ เพียง Python ธรรมดาและไลบรารี OCR ของบุคคลที่สาม (เราจะใช้แพ็กเกจ `pyocr` สมมติสำหรับการอธิบาย)

**Prerequisites**  
- Python 3.8+ ติดตั้งแล้ว  
- คุ้นเคยพื้นฐานกับฟังก์ชันของ Python และ `concurrent.futures`  
- เข้าถึงไลบรารี OCR ที่เปิดเผยคลาส `OcrEngine` (เช่น `pip install pyocr`)  

หากคุณยังไม่มีสิ่งใดข้างต้น ให้ติดตั้งตอนนี้ – ง่ายกว่าที่คิด

---

## How to Batch OCR in Python – Core Concepts

ก่อนที่เราจะลงลึกในโค้ด มาตอบ “ทำไม” ของแต่ละขั้นตอนกัน

1. **ทำไมต้องตั้งค่าภาษา?**  
   ความแม่นยำของ OCR พุ่งสูงขึ้นเมื่อเอนจินรู้ว่าตัวอักษรที่คาดหวังคืออะไร Latin ใช้ได้กับ English, French, Spanish เป็นต้น หากต้องการเปลี่ยนเป็น `Language.Japanese` หรือ `Language.Arabic` ก็ทำได้ตามต้องการ  

2. **ทำไมต้องใช้การทำงานแบบ batch?**  
   การเรียก batch ทำให้เอนจินจัดตารางงานภายในเอง บางครั้งใช้เธรดเนทีฟหรือการเร่งความเร็วด้วย GPU มันจะคืน handle ที่คุณสามารถสอบถามได้ภายหลัง หมายความว่าคุณไม่ต้องบล็อกขณะแต่ละภาพกำลังประมวลผล  

3. **ทำไมต้องใช้ ThreadPoolExecutor?**  
   ออบเจ็กต์ Future ที่เราจะได้กลับมานั้น *lazy* – จะเริ่มดึงผลลัพธ์เมื่อเราถามเท่านั้น โดยการส่ง thread pool ให้ `getAll` เราให้ Python ดึงข้อความของแต่ละหน้าแบบขนาน ทำให้เวลารวมลดลงอย่างมาก  

4. **ทำไมต้อง enumerate ผลลัพธ์?**  
   ลำดับของผลลัพธ์ตรงกับลำดับของเส้นทางไฟล์ที่ส่งเข้าไป จึงสามารถระบุหมายเลขหน้าได้อย่างปลอดภัย  

การเข้าใจ “ทำไม” เหล่านี้จะช่วยให้คุณปรับใช้รูปแบบนี้กับไลบรารีอื่นหรือชุดข้อมูลขนาดใหญ่ได้ง่ายขึ้น

---

## Step 1: Install and Import Required Packages

ก่อนอื่นให้แน่ใจว่าได้ติดตั้งไลบรารี OCR แล้ว ตัวอย่างใช้แพ็กเกจ `pyocr` ทั่วไป; เปลี่ยนเป็นไลบรารีที่คุณต้องการ (เช่น `pytesseract`, `easyocr`)

```bash
pip install pyocr
```

จากนั้น import สิ่งที่ต้องใช้ทั้งหมด

```python
# Standard library imports
import concurrent.futures
from pathlib import Path

# Third‑party OCR library (hypothetical)
from pyocr import OcrEngine, Language
```

> **Pro tip:** การใช้ `Path` จาก `pathlib` ทำให้สคริปต์ของคุณเป็น OS‑agnostic และอ่านง่ายขึ้น

---

## Step 2: Create the OCR Engine and Set Language

การสร้างเอนจินทำได้ง่าย เราจะล็อกไว้ที่ Latin สำหรับการสาธิตนี้

```python
# Step 2: Initialise the OCR engine
engine = OcrEngine()
engine.setLanguage(Language.Latin)   # Change to Language.YourChoice if needed
```

การเรียก `setLanguage` เป็นขั้นตอนเลือกใช้สำหรับบางเอนจิน แต่เป็นนิสัยที่ดี มันบอกโมเดล OCR ให้โฟกัสที่ชุดอักขระที่คุณต้องการ ทำให้ความเร็วและความแม่นยำดีขึ้น

---

## Step 3: List the Image Files to Process (Extract Text from PNG)

รวบรวมไฟล์ PNG ทั้งหมดที่ต้องการแปลง การใช้ `Path.glob` ทำให้คุณสามารถวางโฟลเดอร์เต็มๆ ลงไปโดยไม่ต้องแก้สคริปต์

```python
# Step 3: Gather PNG images – this is the “extract text from png” part
image_dir = Path("YOUR_DIRECTORY")   # Replace with your actual folder
image_paths = sorted(image_dir.glob("*.png"))   # Returns a list of Path objects

# Convert Path objects to strings for the OCR library (if required)
image_paths = [str(p) for p in image_paths]

if not image_paths:
    raise FileNotFoundError("No PNG files found in the specified directory.")
```

> **ทำไมต้องทำแบบนี้:** การเรียงลำดับรายการทำให้เรามั่นใจว่าลำดับผลลัพธ์จะสอดคล้องกับหมายเลขหน้าอย่างแม่นยำ

---

## Step 4: Launch a Batch OCR Operation (Convert Image to Text)

ต่อไปเราจะส่งรายการให้กับเอนจิน วิธีนี้จะคืนคอนเทนเนอร์แบบ Future‑like ที่เราจะสอบถามภายหลัง

```python
# Step 4: Start batch OCR – returns a Future‑like object
batch_future = engine.ocrBatch(image_paths)
```

ภายใต้พื้นฐานเอนจินอาจสร้างเธรดของตัวเองหรือแม้กระทั่ง pipeline บน GPU สิ่งที่สำคัญคือเรามี handle (`batch_future`) ที่รู้วิธีดึงผลลัพธ์แต่ละรายการ

---

## Step 5: Retrieve All Results Concurrently (OCR Multiple Images)

นี่คือจุดที่เราจริงๆ *batch* งานโดยให้ `ThreadPoolExecutor` กับ `getAll` เพื่อให้ข้อความของแต่ละหน้าได้มาพร้อมกันในเธรดของมันเอง

```python
# Step 5: Pull results using a thread pool – this speeds up OCR multiple images
with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
    # getAll returns a list of Result objects in the same order as image_paths
    results = batch_future.getAll(executor)
```

คุณสามารถปรับ `max_workers` ตามจำนวนคอร์ CPU หรือคำแนะนำของไลบรารี OCR ของคุณ การเพิ่ม workers ไม่ได้หมายความว่าจะเร็วขึ้นเสมอ – ควรตรวจสอบการใช้ CPU

---

## Step 6: Output the Recognised Text (Python OCR Tutorial Finale)

สุดท้ายพิมพ์ข้อความของแต่ละหน้า `Result` มีเมธอด `getText()` – ปรับให้ตรงกับเมธอดของไลบรารีที่คุณใช้หากแตกต่าง

```python
# Step 6: Display the recognised text for each page
for i, result in enumerate(results):
    print(f"--- Page {i + 1} ---")
    print(result.getText())
    print()   # Blank line for readability
```

**ผลลัพธ์ที่คาดหวัง (ตัวอย่าง)**

```
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...

--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore magna...

--- Page 3 ---
Ut enim ad minim veniam, quis nostrud exercitation ullamco...
```

หากภาพใดภาพหนึ่งล้มเหลว ส่วนใหญ่เอนจินจะคืนสตริงว่างหรือโยน exception – คุณสามารถห่อ loop ด้วย `try/except` เพื่อจัดการกรณีขอบอย่างราบรื่น

---

## Full Script – Ready to Run

ด้านล่างเป็นสคริปต์เต็มที่พร้อมใช้งาน คัดลอกวางลงในไฟล์ชื่อ `batch_ocr.py` ปรับ `YOUR_DIRECTORY` แล้วรันด้วย `python batch_ocr.py`

```python
#!/usr/bin/env python3
"""
Batch OCR script – processes all PNG files in a directory.
Demonstrates how to batch OCR, OCR multiple images, extract text from PNG,
and convert image to text using a Python OCR engine.
"""

import concurrent.futures
from pathlib import Path

# Replace with your actual OCR library import
from pyocr import OcrEngine, Language

def main():
    # Initialise OCR engine
    engine = OcrEngine()
    engine.setLanguage(Language.Latin)

    # Locate PNG files
    image_dir = Path("YOUR_DIRECTORY")          # <‑‑ change this
    image_paths = sorted(image_dir.glob("*.png"))
    image_paths = [str(p) for p in image_paths]

    if not image_paths:
        raise FileNotFoundError("No PNG files found in the specified directory.")

    # Start batch OCR
    batch_future = engine.ocrBatch(image_paths)

    # Retrieve results concurrently
    with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
        results = batch_future.getAll(executor)

    # Print each page's recognised text
    for i, result in enumerate(results):
        print(f"--- Page {i + 1} ---")
        print(result.getText())
        print()

if __name__ == "__main__":
    main()
```

บันทึก, รัน, แล้วดูคอนโซลเต็มไปด้วยข้อความที่สกัดออกมา ง่าย, เร็ว, และทำงานแบบ asynchronous อย่างเต็มที่

---

## Common Pitfalls & How to Avoid Them

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **No output** – empty strings | เอนจิน OCR ไม่พบข้อความ (ภาพมีสัญญาณรบกวนมาก) | เตรียมภาพล่วงหน้า: ทำ binarize, deskew, หรือเพิ่ม DPI |
| **`FileNotFoundError`** | เส้นทางโฟลเดอร์ผิดหรือไฟล์ PNG ขาดหาย | ตรวจสอบ `YOUR_DIRECTORY` อีกครั้งและให้ไฟล์ลงท้ายด้วย `.png` |
| **High CPU usage** | `max_workers` ตั้งค่าสูงเกินกว่าคอมพิวเตอร์ | ลด `max_workers` หรือเปิดใช้งาน GPU acceleration หากสนับสนุน |
| **Unicode garble** | เอนจินใช้ภาษาเริ่มต้นที่ไม่ตรง | เรียก `engine.setLanguage(Language.Latin)` (หรือภาษาอื่นที่เหมาะ) ก่อนทำ batch OCR |

การแก้ไขปัญหาเหล่านี้ตั้งแต่ต้นจะช่วยคุณประหยัดเวลาการดีบักหลายชั่วโมง

---

## Extending the Tutorial – Next Steps

- **OCR multiple images** ในฟอร์แมตอื่น (JPEG, TIFF) – เพียงเปลี่ยน pattern ของ glob  
- **Extract text from PNG** แล้วส่งต่อไปยัง search index (เช่น Elasticsearch)  
- **Convert image to text** เพื่อสร้าง PDF ด้วย `reportlab` หรือ `PyPDF2`  
- **Parallelize across machines** ด้วย `multiprocessing` หรือคิวงานอย่าง Celery สำหรับชุดข้อมูลขนาดมหาศาล  

หัวข้อเหล่านี้ต่อเนื่องจาก **python ocr tutorial** ที่คุณทำเสร็จแล้ว

---

## Conclusion

เราได้อธิบาย **วิธีทำ batch OCR** ของไฟล์ PNG จำนวนหลายไฟล์ แสดงพลังของ API แบบ batch และสาธิตการ **extract text from PNG** ด้วยการใช้ thread‑pool ผลลัพธ์เต็มที่ด้านบนพร้อมใช้งานใน production และคุณมีพื้นฐานแข็งแกร่งสำหรับโปรเจกต์ Python ที่ต้องพึ่งพา OCR ใดๆ  

ลองรัน ปรับตั้งค่าภาษา หรือแม้เปลี่ยน `pyocr` เป็น `pytesseract` – รูปแบบการทำงานยังคงเหมือนเดิม มีคำถามหรืออยากแชร์กรณีการใช้งานที่เจ๋ง? แสดงความคิดเห็นได้เลย แล้วเราจะต่อสนทนาต่อไป

*Happy coding!*

## What Should You Learn Next?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}