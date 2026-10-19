---
category: general
date: 2026-03-18
description: สกัดข้อความจากไฟล์ PNG ด้วย Python และ Aspose OCR. เรียนรู้วิธีโหลดภาพสำหรับ
  OCR, รัน OCR หลายไฟล์, และทำการ OCR แบบชุดพร้อมการจดจำภาพแบบขนาน.
draft: false
keywords:
- extract text from png
- ocr multiple files
- batch ocr images
- load image for OCR
- parallel image recognition
language: th
og_description: ดึงข้อความจากไฟล์ PNG ด้วย Aspose OCR ใน Python บทเรียนนี้แสดงวิธีโหลดภาพสำหรับ
  OCR, ประมวลผล OCR หลายไฟล์, และรัน OCR แบบชุดโดยใช้การจดจำภาพแบบขนาน
og_title: สกัดข้อความจาก PNG – คู่มือ OCR แบบขนาน
tags:
- OCR
- Python
- threading
- Aspose
- image-processing
title: ดึงข้อความจาก PNG – คู่มือ OCR ขนานสำหรับการจดจำภาพแบบชุด
url: /th/python-java/general/extract-text-from-png-parallel-ocr-guide-for-batch-image-rec/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ดึงข้อความจาก PNG – คู่มือ OCR ขนานสำหรับการจดจำภาพแบบแบตช์

เคยต้องการ **ดึงข้อความจากไฟล์ PNG** แต่รู้สึกติดขัดเมื่อภาพเดียวใช้เวลาประมวลผลนานเกินไปหรือไม่? คุณไม่ได้เป็นคนเดียว ในหลายโครงการจริง—เช่น เครื่องสแกนใบแจ้งหนี้, ตัวแปลงใบเสร็จเป็นดิจิทัล, หรือเครื่องมือจัดเก็บเอกสาร—ความเร็วเป็นสิ่งสำคัญ และการประมวลผล PNG ทีละภาพไม่เพียงพอ  

ในคู่มือนี้เราจะพาคุณผ่านโซลูชันที่สมบูรณ์พร้อมใช้งานที่ **โหลดภาพสำหรับ OCR**, รัน **ocr multiple files** ในรูปแบบ **batch OCR images**, และใช้ **parallel image recognition** ด้วยโมดูล `threading` ของ Python. เมื่อเสร็จคุณจะมีสคริปต์ที่ดึงข้อความจาก PNG จำนวนใดก็ได้ในไม่กี่วินาที ไม่ใช่หลายนาที  

## สิ่งที่คุณต้องมี

- Python 3.8 หรือใหม่กว่า (ไวยากรณ์ที่แสดงทำงานได้บน 3.10+ ด้วย).  
- แพคเกจ Aspose OCR สำหรับ Java/​Python (`aspose-ocr`). คุณสามารถติดตั้งได้ผ่าน `pip`.  
- โฟลเดอร์ที่มีไฟล์ PNG จำนวนหนึ่งที่คุณต้องการประมวลผล.  
- RAM ปริมาณพอสมควร—แต่ละเธรดถืออินสแตนซ์ของ OCR engine เล็ก ๆ ทำให้แม้แล็ปท็อปก็สามารถรันหลายสิบเธรดได้  

ไม่มีบริการภายนอก, ไม่มีคีย์คลาวด์, และไม่มีไฟล์กำหนดค่าลึกลับ เพียงโค้ด Python ธรรมดาที่คุณสามารถคัดลอก‑วางและรันได้  

## ทำไมต้องดึงข้อความจาก PNG แบบขนาน?

การประมวลผล PNG เป็นงานที่ใช้ CPU เป็นหลัก: OCR engine ทำงานอัลกอริทึมการวิเคราะห์ภาพหลายขั้นตอนที่ประมวลผลข้อมูลพิกเซล เมื่อคุณมีภาพสิบ, ยี่สิบ หรือร้อยภาพ เวลาโดยรวมจะเท่ากับผลรวมของการรันแต่ละภาพ  

โดยการสร้างเธรดสำหรับแต่ละไฟล์ เราให้ระบบปฏิบัติการจัดตารางงานที่ใช้ CPU หนักเหล่านี้พร้อมกันบนเครื่องหลายคอร์ ซึ่งมักทำให้เวลาในการทำงานลดลงครึ่งหนึ่ง—หรือแม้กระทั่งเหลือสี่ส่วน—ของเวลาจริง ความแลกเปลี่ยนคือการใช้หน่วยความจำเพิ่มเล็กน้อย แต่สำหรับงานแบตช์ส่วนใหญ่ ความเร็วที่เพิ่มขึ้นคุ้มค่ามาก  

> **เคล็ดลับ:** หากคุณต้องจัดการกับภาพหลายร้อยเมกะไบต์ ให้พิจารณาใช้ `concurrent.futures.ProcessPoolExecutor` แทน `threading`. กระบวนการให้การทำงานขนานจริงบน CPython ที่ผูกกับ GIL แม้จะมีค่าใช้จ่ายของโอเวอร์เฮดเพิ่มขึ้นเล็กน้อย  

## ขั้นตอนที่ 1: ติดตั้ง Aspose OCR สำหรับ Python

เริ่มจากขั้นตอนแรก—มาติดตั้งไลบรารี OCR บนระบบของคุณกัน  

```bash
pip install aspose-ocr
```

## ขั้นตอนที่ 2: โหลดภาพสำหรับ OCR – ฟังก์ชัน worker

ตอนนี้เรากำหนดรูทีนหลักที่จะทำงานในแต่ละเธรด มัน **โหลดภาพสำหรับ OCR**, ทำการจดจำ, และพิมพ์ตัวอย่างข้อความที่ดึงได้  

```python
import threading
from asposeocrjava import OcrEngine, OcrResult

def ocr_task(image_path: str):
    """
    Loads a PNG, runs OCR, and prints the first 100 characters of the result.
    Each thread creates its own OcrEngine instance to avoid state clashes.
    """
    # Initialise a fresh engine – this is cheap and thread‑safe.
    engine = OcrEngine()
    # Load image for OCR
    engine.setImageFromFile(image_path)

    # Perform the recognition – this is the CPU‑intensive part.
    result: OcrResult = engine.recognize()

    # Show a preview of the recognized text (first 100 characters)
    preview = result.getText()[:100].replace("\n", " ")
    print(f"[{image_path}] -> {preview}...")
```

- **ทำไมต้องสร้าง `OcrEngine` ใหม่ต่อเธรด?** เนื่องจาก engine มีบัฟเฟอร์ภายใน; การแชร์อินสแตนซ์เดียวกันจะทำให้เกิด race condition และผลลัพธ์เสียหาย.  
- **ทำไมต้องลบ newline?** เพื่อให้การบันทึกลงคอนโซลดูเรียบร้อย.  
- **การจัดการข้อผิดพลาด?** ในการใช้งานจริงคุณควรห่อโค้ดด้วย `try/except` และอาจบันทึกลงไฟล์—ซึ่งเราจะพูดถึงต่อไป.  

## ขั้นตอนที่ 3: รายการไฟล์ PNG ที่ต้องการประมวลผล

คุณอาจกำหนดรายการไฟล์แบบคงที่, แต่วิธีที่ยืดหยุ่นกว่าคือการสแกนไดเรกทอรี ด้านล่างเราแสดงรายการไฟล์สามไฟล์เพื่อความชัดเจน; แทนที่เส้นทางด้วยโฟลเดอร์ของคุณเอง.  

```python
image_files = [
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.png"
]
```

หากคุณต้องการการค้นหาอัตโนมัติ:  

```python
import pathlib

image_dir = pathlib.Path("YOUR_DIRECTORY")
image_files = sorted(str(p) for p in image_dir.glob("*.png"))
```

การปรับเล็กน้อยนี้ทำให้คุณ **ดึงข้อความจากไฟล์ PNG** เป็นจำนวนมากโดยไม่ต้องแก้ไขซอร์สโค้ดทุกครั้ง.  

## ขั้นตอนที่ 4: ตั้งค่า ocr multiple files กับ batch OCR images

ตอนนี้เราจะสร้างเธรดสำหรับแต่ละภาพ นี่คือหัวใจของรูปแบบ **batch OCR images**.  

```python
# Create a thread for each image to run OCR concurrently
thread_list = [
    threading.Thread(target=ocr_task, args=(path,))
    for path in image_files
]
```

การใช้ list comprehension ทำให้โค้ดกระชับ, และแต่ละอ็อบเจ็กต์ `Thread` จะเก็บฟังก์ชันเป้าหมายและอาร์กิวเมนต์ (`image_path`).  

> **หมายเหตุ:** โมดูล `threading` ของ Python ใช้เธรดของระบบปฏิบัติการโดยตรง, ดังนั้นบนแล็ปท็อป 4‑core คุณมักจะเห็นสูงสุดสี่เธรดทำงานพร้อมกัน; ส่วนที่เหลือจะถูกจัดตารางเมื่อคอร์ว่าง.  

## ขั้นตอนที่ 5: รันการจดจำภาพแบบขนาน

การเริ่มต้น worker ทำได้ง่าย: วนลูปรายการและเรียก `start()`. จากนั้นรอให้ทุกเธรดเสร็จโดยใช้ `join()`.  

```python
# Step 5: Start all threads
for thread in thread_list:
    thread.start()

# Step 6: Wait for every thread to finish before exiting
for thread in thread_list:
    thread.join()
```

เมื่อสคริปต์ทำงานเสร็จ, คุณจะเห็นหลายบรรทัดเช่น:  

```
[YOUR_DIRECTORY/doc1.png] -> Invoice #12345 Date: 2024-07-01 Total: $...
[YOUR_DIRECTORY/doc2.png] -> Receipt from Store XYZ Items: 3 Subtotal: $...
[YOUR_DIRECTORY/doc3.png] -> ...
```

ผลลัพธ์นี้ยืนยันว่าแต่ละ PNG ได้รับการประมวลผลและข้อความที่ดึงได้พร้อมสำหรับการจัดการต่อ (เช่น บันทึกลงฐานข้อมูลหรือส่งต่อไปยัง pipeline NLP).  

## ขั้นตอนที่ 6: ตรวจสอบผลลัพธ์และจัดการกรณีขอบ

### ตรวจสอบผลลัพธ์ที่ว่างเปล่า

บางครั้งภาพอาจมีสัญญาณรบกวนมากเกินไป, หรือ OCR engine ไม่สามารถตรวจจับอักขระใด ๆ การตรวจสอบอย่างรวดเร็วสามารถป้องกันข้อผิดพลาดต่อไปได้.  

```python
def ocr_task(image_path: str):
    engine = OcrEngine()
    engine.setImageFromFile(image_path)

    result: OcrResult = engine.recognize()
    text = result.getText().strip()

    if not text:
        print(f"[{image_path}] -> No text detected.")
    else:
        preview = text[:100].replace("\n", " ")
        print(f"[{image_path}] -> {preview}...")
```

### จำกัดจำนวนเธรดพร้อมกัน

หากคุณรันบน VM ที่มีทรัพยากรจำกัด การสร้างเธรดหลายร้อยอาจทำให้ scheduler ทำงานหนักเกินไป คุณสามารถจำกัดการทำงานพร้อมกันด้วย semaphore:  

```python
max_workers = 8
sema = threading.Semaphore(max_workers)

def ocr_task(image_path: str):
    with sema:
        # ... same body as before ...
```

### บันทึกผลลัพธ์ลงไฟล์

แทนการพิมพ์, คุณอาจต้องการ CSV ที่มีชื่อไฟล์และข้อความที่ดึงได้:  

```python
import csv
output_path = "ocr_results.csv"

with open(output_path, "w", newline="", encoding="utf-8") as csvfile:
    writer = csv.writer(csvfile)
    writer.writerow(["filename", "extracted_text"])

    def ocr_task(image_path: str):
        engine = OcrEngine()
        engine.setImageFromFile(image_path)
        text = engine.recognize().getText().strip()
        writer.writerow([image_path, text])
```

ตรวจสอบให้เปิดไฟล์ CSV **ครั้งเดียว** นอกฟังก์ชันเธรดเพื่อหลีกเลี่ยง race condition; ตัวเขียนของโมดูล `csv` ปลอดภัยต่อเธรดสำหรับการเขียนแบบง่าย.  

## ตัวอย่างทำงานเต็มรูปแบบ

รวมทุกอย่างเข้าด้วยกัน, นี่คือสคริปต์เดียวที่คุณสามารถบันทึกเป็นไฟล์ชื่อ `batch_ocr.py` แล้วรันได้:  

```python
import threading
import pathlib
import csv
from asposeocrjava import OcrEngine, OcrResult

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
IMAGE_DIR = pathlib.Path("YOUR_DIRECTORY")   # <-- change this
OUTPUT_CSV = "ocr_results.csv"
MAX_WORKERS = 8                               # adjust based on your CPU

# ----------------------------------------------------------------------
# Helper: OCR worker
# ----------------------------------------------------------------------
sema = threading.Semaphore(MAX_WORKERS)

def ocr_task(image_path: str, writer):
    """
    Extract text from a single PNG using Aspose OCR.
    This function is designed to run inside a thread.
    """
    with sema:                     # limit concurrent threads
        engine = OcrEngine()
        engine.setImageFromFile(image_path)

        result: OcrResult = engine.recognize()
        text = result.getText().strip()

        # Write to CSV (thread‑safe because writer is shared)
        writer.writerow([image_path, text])

        # Also print a short preview for quick debugging
        preview = text[:100].replace("\n", " ")
        print(f"[{image_path}] -> {preview}...")

# ----------------------------------------------------------------------
# Main routine
# ----------------------------------------------------------------------
def main():
    # Discover all PNG files
    image_files = sorted(str(p) for p in IMAGE_DIR.glob("*.png"))
    if not image_files:
        print("No PNG files found in", IMAGE_DIR)
        return

    # Open CSV once, share the writer with all threads
    with open(OUTPUT_CSV, "w", newline="", encoding="utf-8") as csvfile:
        writer = csv.writer(csvfile)
        writer.writerow(["filename", "extracted_text"])

        # Create a thread for each image
        threads = [
            threading.Thread(target=ocr_task, args=(path, writer))
            for path in image_files

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}