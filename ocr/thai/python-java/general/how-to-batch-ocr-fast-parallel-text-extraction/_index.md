---
category: general
date: 2026-03-26
description: วิธีทำ OCR เป็นชุดอย่างมีประสิทธิภาพด้วย Python—เรียนรู้การดึงข้อความจากภาพและการแปลง
  OCR ของ PDF ด้วยการประมวลผลแบบขนาน
draft: false
keywords:
- how to batch ocr
- extract text from images
- pdf ocr conversion
- batch ocr processing
- parallel ocr processing
language: th
og_description: วิธีทำ OCR แบบแบตช์อย่างมีประสิทธิภาพ—คู่มือขั้นตอนต่อขั้นตอนสำหรับการดึงข้อความจากภาพ,
  การแปลง OCR PDF และการประมวลผล OCR แบบแบตช์โดยใช้ Python.
og_title: 'วิธีทำ OCR แบบแบตช์: การสกัดข้อความแบบขนานอย่างรวดเร็ว'
tags:
- OCR
- Python
- Parallel Computing
title: 'วิธีทำ OCR แบบแบตช์: การสกัดข้อความแบบขนานเร็ว'
url: /th/python-java/general/how-to-batch-ocr-fast-parallel-text-extraction/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีทำ batch OCR: การสกัดข้อความแบบขนานที่เร็ว

เคยสงสัย **how to batch ocr** หรือไม่เมื่อคุณมีหน้าสแกนหลายสิบหน้า, ภาพหน้าจอ, และ PDF กระจัดกระจายอยู่? คุณไม่ได้เป็นคนเดียว—นักพัฒนาส่วนใหญ่เจออุปสรรคเดียวกัน: การประมวลผลไฟล์แต่ละไฟล์ทีละหนึ่งกลายเป็นคอขวดที่เจ็บปวด  

ข่าวดีคือคุณสามารถสร้าง worker threads จำนวนหนึ่ง, ป้อนไฟล์ทั้งหมดให้พวกมัน, และดู OCR engine ทำงานผ่าน batch แบบขนานได้ ในบทเรียนนี้เราจะเดินผ่านตัวอย่างที่สมบูรณ์พร้อมรันที่แสดง **extract text from images**, ทำ **pdf ocr conversion**, และใช้ **parallel ocr processing** เพื่อความเร็ว

> **สิ่งที่คุณจะได้เรียนรู้**  
> * สคริปต์ Python ที่ทำงานเต็มรูปแบบที่ประมวลผลรายการไฟล์ PNG, TIFF, PDF, และ JPG ที่ผสมกันได้ในครั้งเดียว.  
> * ความเข้าใจว่าทำไม thread pool จึงทำให้การทำ OCR ที่จำกัดโดย I/O เร็วขึ้น.  
> * เคล็ดลับในการจัดการข้อผิดพลาด, PDF ขนาดใหญ่, และจำนวน thread ที่กำหนดเอง.  

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะดำดิ่ง, ตรวจสอบให้แน่ใจว่าคุณมี:

| ข้อกำหนด | เหตุผล |
|-------------|--------|
| Python 3.8+ | ไวยากรณ์สมัยใหม่ & `concurrent.futures` |
| `ocr` library (or any compatible OCR wrapper) | ให้ `OcrBatchProcessor` และอ็อบเจ็กต์ผลลัพธ์ |
| ไฟล์ตัวอย่างจำนวนหนึ่ง (PNG, TIFF, PDF, JPG) | เพื่อดู **extract text from images** ทำงานจริง |
| ความคุ้นเคยพื้นฐานกับ threads (ไม่บังคับ) | เป็นประโยชน์แต่ไม่จำเป็น |

หากคุณยังไม่ได้ติดตั้งแพคเกจ `ocr` ให้รัน:

```bash
pip install ocr-lib   # replace with the actual package name
```

เมื่อสภาพแวดล้อมพร้อมแล้ว, มาวิเคราะห์ปัญหากัน

## ขั้นตอนที่ 1: นำเข้า helper และสร้าง batch processor

สิ่งแรกที่เราต้องการคือที่เก็บงาน OCR ทั้งหมด คลาส `OcrBatchProcessor` ทำเช่นนั้น—มันจัดคิวงานและส่งกลับรายการของอ็อบเจ็กต์ `Future` ให้คุณ.

```python
# Step 1 – set up imports and create the batch processor
from concurrent.futures import as_completed   # helps us retrieve results as they finish
import ocr                                      # the OCR library you installed

# Create a processor that will manage the whole batch
ocr_batch = ocr.OcrBatchProcessor()
```

*ทำไมสิ่งนี้ถึงสำคัญ*: การนำเข้า `as_completed` ทำให้เราตอบสนองต่อแต่ละงานที่เสร็จทันที, แทนการรอไฟล์ที่ช้าที่สุด. นี่คือหัวใจของ **batch ocr processing**.

## ขั้นตอนที่ 2: ปรับแต่ง worker pool สำหรับการทำงานขนาน

โดยค่าเริ่มต้น processor อาจใช้ thread เดียว, ซึ่งทำให้การ batch ไม่มีประโยชน์. เราเรียกขอให้ใช้ worker สี่คน—คุณสามารถเพิ่มจำนวนนี้ให้เท่ากับจำนวน core ของ CPU ที่คุณมีได้.

```python
# Step 2 – configure parallelism (four threads in this example)
ocr_batch.set_thread_count(4)   # Adjust based on your machine’s capabilities
```

*เคล็ดลับ*: สำหรับงาน I/O‑bound เช่น OCR, คุณมักจะได้ผลตอบแทนที่ลดลงหลังจาก `CPU cores * 2`. ทดลองค่าต่าง ๆ แล้วเลือกจุดที่เหมาะสม.

## ขั้นตอนที่ 3: คิวไฟล์ทุกไฟล์ที่คุณต้องการ OCR

ที่นี่เราจะเพิ่มไฟล์รูปภาพและ PDF ที่ผสมกัน. เมธอด `add` เพียงบันทึกเส้นทาง; งานจริงจะไม่เริ่มจนกว่าเราจะส่ง batch.

```python
# Step 3 – add files to the batch (feel free to glob a directory instead)
ocr_batch.add("YOUR_DIRECTORY/page1.png")
ocr_batch.add("YOUR_DIRECTORY/page2.tif")
ocr_batch.add("YOUR_DIRECTORY/page3.pdf")
ocr_batch.add("YOUR_DIRECTORY/page4.jpg")
```

หากคุณต้องการประมวลผลโฟลเดอร์ทั้งหมด, ลูป `glob` อย่างรวดเร็วก็ทำได้:

```python
import pathlib, fnmatch
for path in pathlib.Path("YOUR_DIRECTORY").rglob("*"):
    if fnmatch.fnmatch(path.suffix.lower(), ".png") or \
       fnmatch.fnmatch(path.suffix.lower(), ".tif") or \
       fnmatch.fnmatch(path.suffix.lower(), ".pdf") or \
       fnmatch.fnmatch(path.suffix.lower(), ".jpg"):
        ocr_batch.add(str(path))
```

## ขั้นตอนที่ 4: เริ่มงานและเก็บ futures

การเรียก `submit_all` ให้สัญญาณสีเขียวกับ processor. มันคืนรายการของอ็อบเจ็กต์ `Future`—คิดว่าเป็นตัวแทนของผลลัพธ์ที่จะปรากฏในภายหลัง.

```python
# Step 4 – submit all jobs at once; get back a list of futures
ocr_futures = ocr_batch.submit_all()
```

ในจุดนี้ OCR engine กำลังทำงานเบื้องหลัง, แต่ละ thread กำลังกินไฟล์หนึ่งไฟล์.

## ขั้นตอนที่ 5: ดึงผลลัพธ์ทันทีที่เสร็จ

โดยใช้ `as_completed` เราวนลูป futures ตามลำดับที่เสร็จ, ไม่ใช่ตามลำดับที่ส่ง. นี้ทำให้สคริปต์ของเราตอบสนองได้ดี, โดยเฉพาะเมื่อบาง PDF ใช้เวลานานกว่า PNG ธรรมดา.

```python
# Step 5 – retrieve each result as it completes
for future in as_completed(ocr_futures):
    try:
        ocr_result = future.result()          # May raise if the job failed
        print("Batch result:\n", ocr_result.get_text())
    except Exception as exc:
        # Graceful error handling – you can log or retry here
        print(f"An OCR job failed: {exc}")
```

**ผลลัพธ์ที่คาดหวัง** (ตัดทอนเพื่อความกระชับ):

```
Batch result:
 The quick brown fox jumps over the lazy dog.
...
Batch result:
 Invoice #12345
 Date: 2026-03-01
 Total: $1,234.56
...
```

แต่ละบล็อกสอดคล้องกับการแสดงผลเป็นข้อความธรรมดาของไฟล์ต้นฉบับ. หากคุณทำ **pdf ocr conversion**, ข้อความจะรวมทุกอย่างที่ OCR engine สามารถถอดรหัสจากแต่ละหน้า.

## การจัดการกรณีขอบและข้อผิดพลาดทั่วไป

| สถานการณ์ | สิ่งที่ควรระวัง | วิธีแก้เร็ว |
|-----------|-------------------|-----------|
| รูปภาพเสีย | `future.result()` ทำให้เกิด `OSError` | ห่อด้วย `try/except` (ดูโค้ดด้านบน) |
| PDF ขนาดใหญ่มาก ( > 100 MB ) | ความกดดันของหน่วยความจำ, threads ช้าลง | เพิ่ม `thread_count` อย่างพอสมควรหรือแยก PDF เป็นบทก่อน |
| เอกสารหลายภาษา | โมเดล OCR เริ่มต้นอาจตรวจจับผิด | ส่งคำแนะนำภาษาไปยัง `OcrBatchProcessor` หากไลบรารีรองรับ |
| ต้องการรักษาเลย์เอาต์ | `get_text()` ธรรมดาจะสูญเสียคอลัมน์ | ใช้ `ocr_result.get_hocr()` หรือเมธอดที่รับรู้เลย์เอาต์ที่คล้ายกัน |

### เคล็ดลับ: จำนวน thread ที่กำหนดเองตามประเภทไฟล์

หากคุณรู้ว่างานส่วนใหญ่เป็น PDF, คุณอาจจัดสรร thread มากกว่าสำหรับ PDF และน้อยกว่าสำหรับ PNG ขนาดเล็ก. ไลบรารีบางตัวให้คุณส่ง `priority` ต่อ job; หากไม่, คุณสามารถสร้าง batch แยกสองชุด—หนึ่งสำหรับรูปภาพ, หนึ่งสำหรับ PDF—และรันพร้อมกัน.

## ภาพรวมโดยภาพ (ตัวเลือก)

![แผนภาพการทำงาน batch OCR](https://example.com/ocr-workflow.png "แผนภาพการทำงาน batch OCR")

*แผนภาพแสดงกระบวนการจากการค้นหาไฟล์ → การสร้าง batch → การทำงานขนาน → การรวมผลลัพธ์.*

## สคริปต์เต็มที่คุณสามารถคัดลอก‑วางได้

ด้านล่างเป็นโปรแกรมทั้งหมด, พร้อมใส่ลงในไฟล์ `.py`. มันรวมทุก snippet ด้านบน, พร้อม helper เล็ก ๆ ที่ค้นหาไฟล์ที่รองรับในไดเรกทอรีโดยอัตโนมัติ.

```python
#!/usr/bin/env python3
"""
How to Batch OCR – Complete Example
-----------------------------------
This script demonstrates parallel OCR processing of mixed image and PDF files.
It shows how to extract text from images, perform pdf ocr conversion, and
handle errors gracefully.
"""

from concurrent.futures import as_completed
import pathlib, fnmatch, sys
import ocr  # replace with your actual OCR library import

def discover_files(root_dir):
    """Yield paths of supported OCR files under *root_dir*."""
    for path in pathlib.Path(root_dir).rglob("*"):
        if fnmatch.fnmatch(path.suffix.lower(), ".png") \
           or fnmatch.fnmatch(path.suffix.lower(), ".tif") \
           or fnmatch.fnmatch(path.suffix.lower(), ".pdf") \
           or fnmatch.fnmatch(path.suffix.lower(), ".jpg"):
            yield str(path)

def main(directory, workers=4):
    # 1️⃣ Initialise batch processor
    ocr_batch = ocr.OcrBatchProcessor()
    ocr_batch.set_thread_count(workers)

    # 2️⃣ Queue every discovered file
    for file_path in discover_files(directory):
        ocr_batch.add(file_path)

    # 3️⃣ Submit all jobs
    futures = ocr_batch.submit_all()

    # 4️⃣ Process results as they arrive
    for fut in as_completed(futures):
        try:
            result = fut.result()
            print("=== OCR RESULT ===")
            print(result.get_text())
            print("\n---\n")
        except Exception as e:
            print(f"[ERROR] OCR failed for a job: {e}", file=sys.stderr)

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python batch_ocr.py <directory-with-files>")
        sys.exit(1)
    main(sys.argv[1])
```

บันทึกเป็น `batch_ocr.py`, ชี้ไปที่โฟลเดอร์ที่มีสแกนของคุณ, แล้วดูคอนโซลเต็มไปด้วยข้อความที่สกัดออก.  

### ทำไมวิธีนี้ถึงได้ผล

* **Thread pool** – OCR ส่วนใหญ่รอ I/O ของดิสก์และการเรียก engine ภายนอก, ดังนั้นหลาย thread ทำให้ CPU ทำงานต่อเนื่อง.  
* **`as_completed`** – คุณจะได้รับผลลัพธ์ทันทีที่พร้อม, ซึ่งเหมาะกับการตอบสนอง UI หรือ pipeline แบบสตรีมมิง.  
* **Error isolation** – ไฟล์ที่เสียหนึ่งไฟล์จะไม่ทำให้ batch ทั้งหมดล่ม; บล็อก `try/except` แยกข้อผิดพลาดออก.  

## สรุป

โดยสรุป, ตอนนี้คุณรู้แล้วว่า **how to batch ocr** ด้วย `concurrent.futures` ของ Python ร่วมกับไลบรารี OCR ที่รองรับการประมวลผลแบบ batch. ด้วยการตั้งค่า thread pool ขนาดพอเหมาะ, คิวไฟล์ที่รองรับทั้งหมด, และดึงผลลัพธ์เมื่อเสร็จ, คุณจะได้ **parallel ocr processing** ที่เร็วโดยไม่เสียความน่าเชื่อถือ.  

จากนี้คุณอาจ:

* เชื่อมผลลัพธ์เข้ากับดัชนีการค้นหาเพื่อการดึงเอกสารอย่างรวดเร็ว.  
* ขยายสคริปต์เพื่อเขียนผลลัพธ์แต่ละอันเป็นไฟล์ `.txt` ข้างไฟล์ต้นฉบับ.  
* แทนที่ thread pool ที่สร้างไว้ด้วย `asyncio` หากไลบรารี OCR ของคุณมี API แบบ async.  

ทดลองต่อไป—เปลี่ยนเป็น Tesseract, Azure Cognitive Services, หรือ Google Vision, แล้วคุณจะเห็นรูปแบบเดียวกันทำงาน. ขอให้สนุกกับ OCR!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}