---
category: general
date: 2026-06-19
description: ดึงข้อความจากรูปภาพใน Python ด้วยเครื่องมือ OCR อย่างง่าย เรียนรู้วิธีแปลงรูปสแกนเป็นข้อความ
  จดจำข้อความจากรูปภาพ และแสดงรายการไฟล์รูปภาพใน Python อย่างมีประสิทธิภาพ
draft: false
keywords:
- extract text from images
- convert scanned images to text
- recognize text from pictures
- list image files python
language: th
og_description: ดึงข้อความจากรูปภาพใน Python ด้วยเครื่องมือ OCR ที่มีน้ำหนักเบา คู่มือนี้จะแสดงวิธีแปลงรูปสแกนเป็นข้อความ,
  จดจำข้อความจากภาพ, และแสดงรายการไฟล์รูปภาพใน Python เพียงไม่กี่ขั้นตอน.
og_title: ดึงข้อความจากรูปภาพใน Python – คู่มือ OCR แบบเต็มชุด
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Extract text from images in Python with a simple OCR engine. Learn
    how to convert scanned images to text, recognize text from pictures, and list
    image files python efficiently.
  headline: Extract Text from Images in Python – Full Batch OCR Guide
  type: TechArticle
tags:
- Python
- OCR
- Image Processing
title: สกัดข้อความจากรูปภาพด้วย Python – คู่มือ OCR แบบเต็มชุด
url: /th/python-java/general/extract-text-from-images-in-python-full-batch-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ดึงข้อความจากรูปภาพใน Python – คู่มือ OCR แบบชุดเต็ม

เคยต้อง **ดึงข้อความจากรูปภาพ** แต่ไม่รู้จะเริ่มต้นอย่างไรหรือไม่? คุณไม่ได้เป็นคนเดียว—นักพัฒนาต่าง ๆ มักเผชิญกับความท้าทายในการแปลง PDF ที่สแกน, ใบเสร็จที่ถ่ายรูป, หรือภาพหน้าจอให้เป็นข้อความที่ค้นหาได้ ในบทเรียนนี้เราจะเดินผ่านตัวอย่างที่พร้อมรันเต็มรูปแบบที่แสดงวิธี **แปลงภาพสแกนเป็นข้อความ**, จดจำข้อความจากรูปภาพ, และแม้กระทั่ง **list image files python**‑style. เมื่อเสร็จสิ้นคุณจะได้สคริปต์ที่นำกลับมาใช้ใหม่ได้ซึ่งประมวลผลโฟลเดอร์ทั้งหมดในครั้งเดียว

เราจะครอบคลุมทุกอย่างที่คุณต้องการ: ไลบรารีที่จำเป็น, เหตุผลที่แต่ละขั้นตอนสำคัญ, การจัดการกรณีขอบ, และเคล็ดลับการแก้ปัญหา ไม่ต้องไล่ตามเอกสารภายนอก; โค้ดด้านล่างเป็นอิสระและคำอธิบายตอบทั้ง “อย่างไร” *และ* “ทำไม”. เปิด IDE ที่คุณชอบแล้วเริ่มกันเลย

---

## สิ่งที่คุณจะสร้าง

- เริ่มต้นเครื่อง OCR (เราจะใช้แพ็กเกจ `ocr` เป็นตัวอย่าง)
- สแกนไดเรกทอรีและ **list image files python**‑style, กรอง PNG, JPG, และ TIFF
- รันการทำ **batch OCR** บนรูปภาพทั้งหมดที่พบ
- พิมพ์ข้อความที่ดึงได้สำหรับแต่ละไฟล์พร้อมป้ายกำกับชัดเจน

> **เคล็ดลับมืออาชีพ:** หากคุณยังไม่ได้ติดตั้งไลบรารี `ocr` คุณสามารถสลับเป็น `pytesseract` ด้วยการเปลี่ยนแปลงเล็กน้อย—ตรรกะหลักยังคงเหมือนเดิม

---

## ข้อกำหนดเบื้องต้น

- Python 3.8+ (สคริปต์ใช้ f‑strings และ type hints)
- ไลบรารี OCR ที่เปิดเผย `OcrEngine` พร้อมเมธอด `recognize_batch` สำหรับคู่มือนี้เราจะสมมติว่าใช้แพ็กเกจ `ocr` แต่วิธีการนี้ใช้ได้กับไลบรารีจริงเช่นกัน
- โฟลเดอร์ที่มีไฟล์รูปภาพที่ต้องการประมวลผล (`.png`, `.jpg`, `.tif`)

---

## ขั้นตอนที่ 1 – ติดตั้งและนำเข้าโมดูลที่จำเป็น

ก่อนอื่นให้แน่ใจว่าแพ็กเกจ OCR พร้อมใช้งาน หากคุณใช้ไลบรารีจริงเช่น `pytesseract` ให้เปลี่ยนการนำเข้าให้สอดคล้อง

```python
# Install the fictional OCR package (skip if using pytesseract)
# pip install ocr-package

import os
import ocr  # <-- replace with your actual OCR library
from typing import List
```

> **ทำไมจึงสำคัญ:** การนำเข้า `os` ทำให้เราจัดการเส้นทางแบบข้ามแพลตฟอร์มได้, ส่วน `typing.List` ช่วยให้ IDE แนะนำโค้ดและทำให้โค้ดพร้อมสำหรับอนาคต

---

## ขั้นตอนที่ 2 – **Extract Text from Images**: เริ่มต้นเครื่อง OCR

การสร้างเอนจินเป็นขั้นตอนแรกของงาน OCR ใด ๆ เรายังตั้งค่าภาษาให้ตรวจจับอัตโนมัติเพื่อให้เอนจินจัดการกับเอกสารหลายภาษาได้

```python
def create_engine() -> ocr.OcrEngine:
    """
    Initializes the OCR engine with automatic language detection.
    Returns:
        An instance of ocr.OcrEngine ready for batch processing.
    """
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.Auto  # Auto‑detect language
    return engine
```

> **คำอธิบาย:** การห่อหุ้มการสร้างเอนจินในฟังก์ชันทำให้โค้ดเป็นโมดูลาร์ หากคุณต้องการปรับ DPI หรือโหมด OCR ในภายหลัง เพียงแก้ไขส่วนนี้เท่านั้น

---

## ขั้นตอนที่ 3 – **List Image Files Python**: รวบรวมไฟล์จากไดเรกทอรี

ตอนนี้เราต้องหาภาพทุกไฟล์ที่ต้องการประมวลผล รายการเชิงความเข้าใจด้านล่างเป็นรูปแบบ “list image files python” ที่พบบ่อย

```python
def get_image_files(input_dir: str) -> List[str]:
    """
    Scans `input_dir` and returns a list of absolute paths
    for files ending with .png, .jpg, or .tif (case‑insensitive).
    """
    supported_exts = ('.png', '.jpg', '.jpeg', '.tif', '.tiff')
    return [
        os.path.join(input_dir, f)
        for f in os.listdir(input_dir)
        if f.lower().endswith(supported_exts)
    ]
```

> **การจัดการกรณีขอบ:** ฟังก์ชันนี้ละเว้นโฟลเดอร์ย่อย (คุณสามารถเพิ่มการทำซ้ำในภายหลัง) และกรองไฟล์ที่ซ่อนโดยอัตโนมัติ เนื่องจากไฟล์เหล่านั้นมักไม่มีนามสกุลที่รองรับ

---

## ขั้นตอนที่ 4 – **Convert Scanned Images to Text**: รัน Batch OCR

ไลบรารี OCR ส่วนใหญ่มีเมธอด batch ที่เร็วกว่าเมื่อประมวลผลทีละภาพ นี่คือวิธีเรียกใช้

```python
def run_batch_ocr(engine: ocr.OcrEngine, image_paths: List[str]) -> List[ocr.OcrResult]:
    """
    Sends a list of image file paths to the OCR engine for batch recognition.
    Returns a list of OcrResult objects, preserving order.
    """
    # The fictional `recognize_batch` returns a list of results matching input order
    return engine.recognize_batch(image_paths)
```

> **ทำไมต้อง batch?** การส่งรูปภาพทั้งหมดพร้อมกันลดค่าโอเวอร์เฮด (เช่น การโหลดโมเดล OCR ซ้ำหลายครั้ง) และมักทำให้การใช้ CPU/GPU มีประสิทธิภาพมากขึ้น

---

## ขั้นตอนที่ 5 – **Recognize Text from Pictures**: แสดงผลลัพธ์

สุดท้าย เราวนลูปผ่านชื่อไฟล์และผล OCR คู่กัน แล้วพิมพ์หัวข้อที่สะอาดสำหรับแต่ละรูป

```python
def display_results(image_paths: List[str], ocr_results: List[ocr.OcrResult]) -> None:
    """
    Prints the extracted text for each image, prefixed with the file name.
    """
    for file_path, result in zip(image_paths, ocr_results):
        print(f"--- {os.path.basename(file_path)} ---")
        # Some OCR engines store the plain text in a `.text` attribute
        print(result.text.strip())
        print()  # Blank line for readability
```

> **เคล็ดลับ:** `strip()` ลบช่องว่างต้นและท้ายที่ OCR มักเพิ่มเข้ามา

---

## สคริปต์เต็ม – รวมทุกอย่างไว้ด้วยกัน

ด้านล่างเป็นโปรแกรมที่สมบูรณ์และสามารถรันได้ บันทึกเป็น `batch_ocr.py` แล้วรัน `python batch_ocr.py <your_folder>`

```python
#!/usr/bin/env python3
"""
Batch OCR script – extracts text from images in a given folder.
Usage: python batch_ocr.py /path/to/images
"""

import sys
import os
import ocr  # Replace with your OCR library if different
from typing import List

def create_engine() -> ocr.OcrEngine:
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.Auto
    return engine

def get_image_files(input_dir: str) -> List[str]:
    supported_exts = ('.png', '.jpg', '.jpeg', '.tif', '.tiff')
    return [
        os.path.join(input_dir, f)
        for f in os.listdir(input_dir)
        if f.lower().endswith(supported_exts)
    ]

def run_batch_ocr(engine: ocr.OcrEngine, image_paths: List[str]) -> List[ocr.OcrResult]:
    return engine.recognize_batch(image_paths)

def display_results(image_paths: List[str], ocr_results: List[ocr.OcrResult]) -> None:
    for file_path, result in zip(image_paths, ocr_results):
        print(f"--- {os.path.basename(file_path)} ---")
        print(result.text.strip())
        print()

def main() -> None:
    if len(sys.argv) != 2:
        print("Usage: python batch_ocr.py <input_directory>")
        sys.exit(1)

    input_dir = sys.argv[1]

    if not os.path.isdir(input_dir):
        print(f"Error: '{input_dir}' is not a valid directory.")
        sys.exit(1)

    engine = create_engine()
    image_files = get_image_files(input_dir)

    if not image_files:
        print("No supported image files found in the directory.")
        sys.exit(0)

    ocr_results = run_batch_ocr(engine, image_files)
    display_results(image_files, ocr_results)

if __name__ == "__main__":
    main()
```

### ผลลัพธ์ที่คาดหวัง

สมมติว่าโฟลเดอร์มี `invoice1.png` และ `receipt.jpg` คุณอาจเห็น:

```
--- invoice1.png ---
Invoice #12345
Date: 2024‑04‑01
Total: $256.78

--- receipt.jpg ---
Store: Coffee Corner
Item: Latte
Price: $4.50
```

แต่ละบล็อกจะมีป้ายกำกับชัดเจน ทำให้การประมวลผลต่อไป (เช่น การบันทึกลงฐานข้อมูล) ง่ายดาย

---

## การจัดการกับปัญหาที่พบบ่อย

| ปัญหา | ทำไมเกิดขึ้น | วิธีแก้เร็ว |
|-------|--------------|------------|
| **ไม่มีข้อความปรากฏ** | ภาษา OCR ไม่ถูกตรวจจับหรือภาพมีคอนทราสต์ต่ำ | บังคับใช้ภาษา (`engine.language = ocr.Language.English`) หรือทำการปรับภาพล่วงหน้า (เพิ่มคอนทราสต์) |
| **Memory error เมื่อประมวลผลชุดใหญ่** | เอนจินพยายามโหลดภาพทั้งหมดพร้อมกัน | แบ่ง `image_files` เป็นชิ้นย่อย (`batch_size = 20`) แล้วเรียก `recognize_batch` หลายครั้ง |
| **ไฟล์ฟอร์แมตไม่รองรับ** | คุณใส่ `.gif` หรือ `.bmp` | ขยายทูเพิล `supported_exts` หรือแปลงภาพเป็น PNG/JPG ก่อน |
| **Unicode garbling** | OCR คืนค่าเป็นไบต์แทนสตริง | ตรวจสอบให้ไลบรารี OCR ส่งออก Unicode (`result.text.decode('utf‑8')` หากจำเป็น) |

---

## การขยายเวิร์กโฟลว์

เมื่อคุณ **extract text from images** แล้ว ลองทำขั้นตอนต่อไปเหล่านี้:

- **Export to CSV** – เขียนชื่อไฟล์และข้อความที่ดึงได้ลงสเปรดชีตเพื่อวิเคราะห์
- **Parallel processing** – ใช้ `concurrent.futures.ThreadPoolExecutor` เพื่อจัดการหลาย batch พร้อมกัน
- **Integrate with cloud OCR** – สลับเอนจินโลคัลเป็น Google Vision หรือ Azure OCR เพื่อความแม่นยำสูงกับเลเอาต์ซับซ้อน
- **Add image preprocessing** – ไลบรารีอย่าง Pillow หรือ OpenCV สามารถทำ deskew, denoise, หรือ threshold ภาพก่อน OCR เพื่อเพิ่มผลลัพธ์

แนวคิดทั้งหมดนี้ใช้ฟังก์ชันหลักที่เราสร้างไว้แล้ว จึงไม่ต้องเริ่มจากศูนย์

---

## สรุป

เราได้เดินผ่านโซลูชันเต็มรูปแบบเพื่อ **extract text from images** ใน Python ครอบคลุมตั้งแต่ **list image files python** ถึง **recognize text from pictures** และสุดท้าย **convert scanned images to text** แบบ batch สคริปต์นี้ออกแบบให้เรียบง่ายแต่ยืดหยุ่นพอที่จะเป็นฐานสำหรับโปรเจกต์ขนาดใหญ่—ไม่ว่าจะเป็นการดิจิไทซ์ใบเสร็จ, สร้างคลังข้อมูลที่ค้นหาได้, หรือขับเคลื่อน pipeline การสกัดข้อมูล

ลองใช้งาน ปรับขั้นตอนการพรี‑โปรเซส แล้วดูความแม่นยำของ OCR เพิ่มขึ้น หากเจออุปสรรค ให้กลับไปดูตาราง “การจัดการกับปัญหาที่พบบ่อย” ส่วนใหญ่แก้ได้ด้วยการปรับค่าเล็กน้อย

พร้อมสำหรับความท้าทายต่อไปหรือยัง? ลองเพิ่มขั้นตอนแปลง PDF‑to‑image ด้วย `pdf2image` แล้วส่งภาพเหล่านั้นเข้าสู่ pipeline เดียวกัน ความเป็นไปได้ไม่มีที่สิ้นสุดเมื่อคุณผสาน OCR กับอีโคซิสเต็มของ Python

Happy coding, and may your text be ever legible!

## สิ่งที่คุณควรเรียนต่อไป

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานแบบต่าง ๆ ในโปรเจกต์ของคุณ

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text Images – OCR Basics with Aspose.OCR for Java](/ocr/english/java/ocr-basics/)
- [How to extract text from image from URL using Aspose.OCR for Java](/ocr/english/java/advanced-ocr-techniques/perform-ocr-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}