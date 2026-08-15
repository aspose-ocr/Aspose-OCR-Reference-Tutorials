---
category: general
date: 2026-03-28
description: ดึงข้อความจากไฟล์ PNG อย่างรวดเร็วด้วย Aspose OCR ใน Python. เรียนรู้การแปลงข้อความจากหน้าสแกนด้วยการจดจำภาพแบบขนานใน
  Python เพื่อผลลัพธ์ที่มีประสิทธิภาพสูง.
draft: false
keywords:
- extract text from png
- convert scanned pages text
- parallel image recognition python
- recognize image text python
- async OCR batch processing
- Aspose OCR Python
language: th
og_description: ดึงข้อความจากไฟล์ PNG อย่างรวดเร็วด้วย Aspose OCR ใน Python คู่มือนี้แสดงวิธีแปลงข้อความจากหน้าสแกนด้วยการจดจำภาพแบบขนานใน
  Python เพื่อให้ได้ผลลัพธ์ความเร็วสูง
og_title: สกัดข้อความจาก PNG – OCR ขนานเร็วด้วย Python
tags:
- OCR
- Python
- Image Processing
- Concurrency
title: สกัดข้อความจาก PNG – OCR ขนานเร็วด้วย Python และ Aspose
url: /th/python-java/general/extract-text-from-png-fast-parallel-ocr-with-python-and-aspo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ดึงข้อความจาก PNG – OCR แบบขนานเร็วด้วย Python

เคยต้อง **extract text from PNG** ไฟล์แล้วพบว่า OCR แบบใช้เธรดเดียวช้าเกินไปหรือไม่? คุณไม่ได้อยู่คนเดียว ไม่ว่าคุณจะกำลังแปลงสแกนใบเสร็จหลายใบหรือแปลงสไลด์การบรรยายให้เป็น PDF ที่ค้นหาได้ จุดคอขวดมักจะอยู่ที่ขั้นตอน OCR เอง  

ในบทเรียนนี้เราจะสาธิตโซลูชันที่พร้อมรันครบชุดที่ **converts scanned pages text** แบบขนานโดยใช้โหมด batch แบบอะซิงโครนัสของ Aspose OCR ร่วมกับ `ThreadPoolExecutor` ของ Python เมื่อเสร็จคุณจะสามารถ **recognize image text python**‑style ได้อย่างมีประสิทธิภาพ จัดการหลายสิบรูปภาพในเวลาที่สั้นกว่าการวนลูปแบบธรรมดามาก

> **สิ่งที่คุณจะได้เรียนรู้**  
> * สคริปต์ทำงานเต็มรูปแบบที่ดึงข้อความจากภาพ PNG พร้อมกันหลายไฟล์  
> * ทำความเข้าใจว่าทำไมโหมด async batch ถึงทำให้เร็วขึ้น  
> * เคล็ดลับการขยายโซลูชันให้รองรับงานปริมาณมาก

## สิ่งที่คุณต้องเตรียม

| ความต้องการ | เหตุผล |
|--------------|--------|
| Python 3.9+ | ไวยากรณ์สมัยใหม่และ type hints |
| แพคเกจ `aspose-ocr` และ `aspose-storage` | ให้เครื่องมือ OCR และตัวโหลดภาพ |
| โฟลเดอร์ที่มีไฟล์ PNG (เช่น หน้าเอกสารสแกน) | วัสดุต้นฉบับที่คุณต้องการประมวลผล |
| ความรู้พื้นฐานเกี่ยวกับการทำ concurrency ใน Python | มีประโยชน์แต่ไม่จำเป็น เราจะอธิบายทุกอย่าง |

คุณสามารถติดตั้งไลบรารี Aspose ด้วยคำสั่ง:

```bash
pip install aspose-ocr aspose-storage
```

> **Pro tip:** คอยอัปเดตแพคเกจของคุณ (`pip list --outdated`) เพื่อรับประโยชน์จากการปรับปรุงประสิทธิภาพล่าสุด

## ขั้นตอนที่ 1: เริ่มต้น Aspose OCR Engine ในโหมด Async Batch

สิ่งแรกที่เราทำคือสร้างอินสแตนซ์ `OcrEngine` แล้วสลับเป็น **asynchronous batch mode** โหมดนี้จะจัดคิวคำขอการจดจำภายใน ทำให้เอนจินสามารถประมวลผลหลายภาพโดยไม่บล็อกเธรดของ Python

```python
import aspose.ocr as aocr
import aspose.storage as storage

# Create the OCR engine
ocr_engine = aocr.OcrEngine()
# Enable async batch processing – crucial for parallel speed‑up
ocr_engine.batch_mode = aocr.BatchMode.ASYNC
```

*ทำไมต้อง async?*  
เมื่อคุณเรียก `recognize` ในโหมด synchronous การเรียกจะบล็อกจนกว่าภาพจะประมวลผลเสร็จสมบูรณ์ ในโหมด async เอนจินสามารถเริ่มทำงานกับภาพถัดไปได้ขณะที่ภาพปัจจุบันยังอยู่ระหว่างการถอดรหัส ทำให้การทำ I/O และการประมวลผล CPU ทำงานทับซ้อนกัน

## ขั้นตอนที่ 2: รายการไฟล์ PNG ที่ต้องการประมวลผล

ที่นี่เรากำหนดคอลเลกชันของภาพ ในโปรเจกต์จริงคุณอาจสร้างรายการนี้แบบไดนามิก (เช่น `glob.glob("*.png")`) แต่การระบุอย่างชัดเจนทำให้ตัวอย่างง่ายต่อการตาม

```python
input_images = [
    "YOUR_DIRECTORY/page1.png",
    "YOUR_DIRECTORY/page2.png",
    "YOUR_DIRECTORY/page3.png"
]
```

> **Note:** แทนที่ `YOUR_DIRECTORY` ด้วยพาธจริงที่เก็บไฟล์ PNG สแกนของคุณ หากมีไฟล์หลายร้อยไฟล์ ควรใช้ `os.listdir` แล้วกรองไฟล์ที่มีส่วนขยาย `.png`

## ขั้นตอนที่ 3: เขียน Helper ที่โหลดภาพและคืนข้อความ

Helper นี้แยกกระบวนการสองขั้นตอนของการโหลดไฟล์ผ่าน **Aspose Storage** แล้วส่งให้ OCR engine การเพิ่ม docstring เล็ก ๆ ทำให้ฟังก์ชันอธิบายตัวเองได้—เป็นประโยชน์สำหรับการบำรุงรักษาในอนาคต

```python
def recognize_image(path: str) -> str:
    """
    Load a PNG image from `path` and return the recognized text.
    """
    # Load the image using Aspose Storage (handles many formats)
    img = storage.Image.load(path)
    # Perform OCR; the result object contains the extracted text
    result = ocr_engine.recognize(img)
    return result.text
```

*ทำไมต้องแยกเป็นฟังก์ชัน?*  
ทำให้โค้ดของ thread‑pool สะอาดและสามารถนำตรรกะนี้ไปใช้ซ้ำได้ที่อื่น (เช่น ใน endpoint ของ Flask) อีกทั้งการแยก I/O ทำให้ดีบักง่ายขึ้น—หากไฟล์ใดไฟล์หนึ่งล้มเหลว คุณจะเห็นชื่อไฟล์ใน stack trace ของ exception

## ขั้นตอนที่ 4: รันการจดจำภาพแบบขนานด้วย Thread Pool

ตอนนี้เรานำ `ThreadPoolExecutor` เข้ามาโดยค่าเริ่มต้นจะสร้าง worker สี่ตัว แต่คุณสามารถปรับ `max_workers` ตามจำนวนคอร์ CPU และขนาดของชุดภาพได้

```python
from concurrent.futures import ThreadPoolExecutor, as_completed

with ThreadPoolExecutor(max_workers=4) as pool:
    # Submit each image to the pool; map futures back to filenames
    future_to_file = {pool.submit(recognize_image, f): f for f in input_images}
    
    # Process results as they finish (order may differ from input order)
    for future in as_completed(future_to_file):
        file_name = future_to_file[future]
        try:
            text = future.result()
        except Exception as exc:
            print(f"--- {file_name} ---")
            print(f"Error during OCR: {exc}")
        else:
            print(f"--- {file_name} ---")
            print(text)
```

### วิธีที่ทำให้คุณได้ Parallel Image Recognition Python

* **ThreadPoolExecutor** สร้างพูลของเธรดทำงานที่แต่ละเธรดเรียก `recognize_image`  
* เนื่องจาก OCR engine อยู่ในโหมด async batch แต่ละเธรดจึงสามารถส่งงานให้เอนจินทำต่อได้โดยยังคงตอบสนอง  
* `as_completed` คืน futures ตามลำดับที่ทำเสร็จ ทำให้คุณได้รับผลลัพธ์ทันทีที่พร้อม—เหมาะกับการสตรีมแบตช์ขนาดใหญ่

> **Common pitfall:** การใช้ `max_workers=1` ทำให้เสียประโยชน์ของการทำขนานบนเครื่อง 8‑core การตั้งค่า `max_workers=8` มักให้ throughput ที่ดีที่สุด แต่ควรทดสอบหลายค่าเพื่อหาจุดที่เหมาะสมกับฮาร์ดแวร์ของคุณ

## ขั้นตอนที่ 5: ตรวจสอบผลลัพธ์และจัดการกรณีขอบ

เมื่อรันสคริปต์ คุณควรเห็นบล็อกข้อความสำหรับแต่ละ PNG ที่ขึ้นต้นด้วยชื่อไฟล์:

```
--- YOUR_DIRECTORY/page1.png ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...

--- YOUR_DIRECTORY/page2.png ---
Sed do eiusmod tempor incididunt ut labore et dolore...

--- YOUR_DIRECTORY/page3.png ---
Ut enim ad minim veniam, quis nostrud exercitation...
```

หากภาพใดภาพหนึ่งล้มเหลว (ไฟล์เสียหาย, ฟอร์แมตไม่รองรับ) บล็อก `except` จะพิมพ์ข้อความข้อผิดพลาดที่เป็นประโยชน์แทนการทำให้แบตช์ทั้งหมดหยุดทำงาน

### ขยายโซลูชัน

| สถานการณ์ | คำแนะนำ |
|----------|----------|
| **Thousands of pages** | เปลี่ยนเป็น `ProcessPoolExecutor` เพื่อใช้หลายโปรเซส CPU, หรือแบ่งรายการเป็นชิ้นย่อยแล้วประมวลผลเป็น batch ทีละส่วน |
| **Different image formats (JPG, TIFF)** | เมธอด `storage.Image.load` ตรวจจับฟอร์แมตอัตโนมัติ เพียงเพิ่มไฟล์เหล่านั้นลงใน `input_images` |
| **Need to store results** | เขียน `text` ลงไฟล์ `.txt` หรือบันทึกลงฐานข้อมูลภายในบล็อก `else` |
| **Performance monitoring** | ห่อ `recognize_image` ด้วยตัวจับเวลา (`time.perf_counter`) แล้วบันทึกระยะเวลาต่อไฟล์ |

## ตัวอย่างทำงานเต็มรูปแบบ (Copy‑Paste Ready)

ด้านล่างเป็นสคริปต์สมบูรณ์พร้อมคัดลอกไปใช้ในไฟล์ชื่อ `parallel_ocr.py` ไม่มีส่วนใดหาย—ทุกอย่างที่คุณต้องการอยู่ที่นี่

```python
# parallel_ocr.py
import aspose.ocr as aocr
import aspose.storage as storage
from concurrent.futures import ThreadPoolExecutor, as_completed

# -------------------------------------------------
# Step 1: Initialize OCR engine in async batch mode
# -------------------------------------------------
ocr_engine = aocr.OcrEngine()
ocr_engine.batch_mode = aocr.BatchMode.ASYNC   # enable asynchronous batch processing

# -------------------------------------------------
# Step 2: Define the PNG files you want to recognize
# -------------------------------------------------
input_images = [
    "YOUR_DIRECTORY/page1.png",
    "YOUR_DIRECTORY/page2.png",
    "YOUR_DIRECTORY/page3.png"
]

# -------------------------------------------------
# Step 3: Helper that loads an image and returns the recognized text
# -------------------------------------------------
def recognize_image(path: str) -> str:
    """
    Load a PNG image from `path` and return the OCR‑extracted text.
    """
    img = storage.Image.load(path)
    result = ocr_engine.recognize(img)
    return result.text

# -------------------------------------------------
# Step 4: Run OCR on all images concurrently using a thread pool
# -------------------------------------------------
with ThreadPoolExecutor(max_workers=4) as pool:
    future_to_file = {pool.submit(recognize_image, f): f for f in input_images}
    for future in as_completed(future_to_file):
        file_name = future_to_file[future]
        try:
            text = future.result()
        except Exception as exc:
            print(f"--- {file_name} ---")
            print(f"Error during OCR: {exc}")
        else:
            print(f"--- {file_name} ---")
            print(text)

# -------------------------------------------------
# Step 5: Output is printed to the console.
# -------------------------------------------------
```

บันทึกไฟล์ ปรับค่า placeholder `YOUR_DIRECTORY` แล้วรัน:

```bash
python parallel_ocr.py
```

คุณจะเห็นข้อความที่ดึงจากแต่ละ PNG ปรากฏในคอนโซลตามที่แสดงไว้ก่อนหน้า

## สรุป

เราได้สาธิตวิธี **extract text from PNG** อย่างมีประสิทธิภาพโดยผสานโหมด async batch ของ Aspose OCR กับ `ThreadPoolExecutor` ของ Python สคริปต์นี้แปลงข้อความจากหน้าเอกสารสแกนแบบขนาน ให้คุณมีวิธีที่ขยายได้สำหรับ **recognize image text python**‑style โดยไม่ต้องเขียน thread‑pool เองจากศูนย์  

หากคุณพร้อมจะต่อยอดต่อไป ลอง:

* เก็บผลลัพธ์ในฐานข้อมูล SQLite ที่ค้นหาได้  
* เพิ่มการพรี‑โปรเซสภาพ (deskew, denoise) ด้วย OpenCV ก่อน OCR  
* ปรับสคริปต์ให้เป็น microservice ผ่าน Flask หรือ FastAPI endpoint  

จำไว้ว่า กุญแจสู่ OCR ประสิทธิภาพสูงไม่ได้อยู่แค่เครื่องยนต์ที่เร็วกว่าเท่านั้น—แต่ยังต้องส่งงานให้เครื่องยนต์ทำงานอย่างเต็มที่ด้วยการทำ concurrency ที่เหมาะสม ด้วยแพทเทิร์นที่แสดงในนี้ คุณสามารถจัดการกับหลายสิบหรือแม้แต่หลายร้อยสแกน PNG ด้วยการเปลี่ยนแปลงโค้ดเพียงเล็กน้อย  

Happy coding, and may your PDFs always be searchable!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}