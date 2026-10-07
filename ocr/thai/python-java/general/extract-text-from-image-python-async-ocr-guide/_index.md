---
category: general
date: 2026-01-12
description: ดึงข้อความจากรูปภาพด้วย Python โดยใช้ Aspose OCR. เรียนรู้วิธีแปลงภาพสแกนเป็นข้อความด้วยโค้ดแบบอะซิงโครนัสในเวลาเพียงไม่กี่นาที.
draft: false
keywords:
- extract text from image python
- convert scanned image to text
language: th
og_description: ดึงข้อความจากภาพด้วย Python และ Aspose OCR. บทเรียนนี้แสดงวิธีแปลงภาพสแกนเป็นข้อความโดยใช้ฟังก์ชันแบบอะซิงค์.
og_title: การสกัดข้อความจากรูปภาพด้วย Python – คู่มือ OCR แบบอะซิงโครนัส
tags:
- python
- ocr
- async
title: ดึงข้อความจากภาพด้วย Python – คู่มือ OCR แบบอะซิงค์
url: /th/python-java/general/extract-text-from-image-python-async-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สกัดข้อความจากรูปภาพด้วย Python – คู่มือ Async OCR

เคยต้องการ **extract text from image Python** สคริปต์แต่รู้สึกติดขัดที่ส่วน OCR ไหม? คุณไม่ได้เป็นคนเดียว นักพัฒนาจำนวนมากเจออุปสรรคเมื่อมีเอกสารสแกนและต้องการแปลงเป็นข้อความที่ค้นหาได้โดยไม่ต้องบิดหัวของตัวเอง

ในบทเรียนนี้เราจะเดินผ่านตัวอย่างที่สมบูรณ์และสามารถรันได้ ซึ่งจะแสดงให้คุณเห็นวิธี **convert scanned image to text** ด้วย Aspose OCR API แบบ asynchronous. เมื่อจบคุณจะมีฟังก์ชันเดียวที่สามารถนำไปใช้ในโปรเจกต์ใดก็ได้ และคุณจะเข้าใจว่าการประมวลผลแบบ async ทำให้แอปของคุณตอบสนองได้แม้ OCR จะใช้เวลาหลายวินาที

## ข้อกำหนดเบื้องต้น

- Python 3.8+ ติดตั้งแล้ว (ฟีเจอร์ async ต้องการอย่างน้อย 3.7)
- แพคเกจ `asposeocr` (`pip install asposeocr`) – นี่คือไลบรารีที่เราจะใช้
- ไฟล์รูปสแกน (TIFF, PNG, JPEG – สิ่งใดที่ Aspose OCR รองรับ)
- ความคุ้นเคยพื้นฐานกับ `asyncio` (ถ้ายังไม่รู้ก็ไม่ต้องกังวล – เราจะอธิบายทุกขั้นตอน)

ไม่มีการพึ่งพาระบบเพิ่มเติม; Aspose OCR รวมทุกอย่างที่คุณต้องการไว้แล้ว

![แผนภาพแสดงกระบวนการ async OCR – สกัดข้อความจากรูปภาพด้วย Python](https://example.com/async-ocr-diagram.png "async OCR flow – extract text from image python")

## ขั้นตอนที่ 1 – ตั้งค่า Asynchronous Helper Function  

หัวใจของวิธีแก้คือฟังก์ชัน `async` ที่โหลดรูปภาพ, เริ่ม OCR, แล้วรอผลลัพธ์ การทำฟังก์ชันเป็น async หมายความว่าคุณสามารถรัน coroutine อื่น ๆ (เช่น ดาวน์โหลดไฟล์เพิ่มเติม) ในขณะที่เอนจิน OCR ทำงานเบื้องหลัง

```python
import asposeocr as ocr
import asyncio

async def async_ocr(image_path: str) -> str:
    """
    Extracts text from the given image file using Aspose OCR asynchronously.
    
    Parameters
    ----------
    image_path: str
        Path to the scanned image (e.g., 'input.tif')
    
    Returns
    -------
    str
        Recognized plain‑text string
    """
    # Initialize the OCR engine and set the language to English.
    ocr_engine = ocr.OcrEngine()
    ocr_engine.language = ocr.Language.ENGLISH

    # Start the OCR operation. process_async returns a Future‑like object.
    ocr_future = ocr_engine.process_async(ocr.Image.load(image_path))

    # Here you could perform other async work – we just yield control.
    await asyncio.sleep(0)

    # Await the OCR result and pull out the recognized text.
    ocr_result = await ocr_future
    return ocr_result.text
```

**Why this matters:** By returning a `Future`, Aspose OCR does the heavy lifting on a separate thread pool. `await` releases the event loop, so your app stays snappy. If you ever need to process many images concurrently, you can simply schedule several `async_ocr` calls with `asyncio.gather`.

## ขั้นตอนที่ 2 – เรียกใช้ Coroutine ใน Event Loop  

ตอนนี้เรามี helper แล้ว เราต้องเรียกใช้มัน `asyncio.run` จะสร้าง event loop ใหม่, รัน coroutine, และปิดทุกอย่างอย่างเรียบร้อย

```python
if __name__ == "__main__":
    # Replace with the actual path to your scanned file.
    image_file = "YOUR_DIRECTORY/input.tif"

    # Run the async OCR function and capture the output.
    recognized_text = asyncio.run(async_ocr(image_file))

    # Print the extracted text to the console.
    print("=== OCR RESULT ===")
    print(recognized_text)
```

**Pro tip:** If you’re integrating this into a larger async application (e.g., FastAPI), you’d call `await async_ocr(...)` directly instead of `asyncio.run`.

## ขั้นตอนที่ 3 – ตรวจสอบผลลัพธ์  

เมื่อคุณรันสคริปต์ คุณควรเห็นอะไรประมาณนี้:

```
=== OCR RESULT ===
Lorem ipsum dolor sit amet,
consectetur adipiscing elit.
```

หากผลลัพธ์ดูเป็นอักขระผสม, ให้ตรวจสอบอีกครั้งว่า:

1. รูปภาพชัดเจนและไม่ได้บีบอัดเกินไป  
2. คุณได้เลือกภาษาอย่างถูกต้อง (`ocr.Language.ENGLISH` ทำงานได้กับข้อความลาตินส่วนใหญ่)  
3. เส้นทางไฟล์ถูกต้องและไฟล์สามารถอ่านได้

## ขั้นตอนที่ 4 – จัดการกรณีขอบ

### หลายภาษา  

หากคุณต้องการ **convert scanned image to text** ในภาษาที่ไม่ใช่ภาษาอังกฤษ เพียงเปลี่ยนคุณสมบัติ language:

```python
ocr_engine.language = ocr.Language.FRENCH   # or ocr.Language.SPANISH, etc.
```

### ไฟล์ขนาดใหญ่  

สำหรับ TIFF ขนาดใหญ่มาก ให้พิจารณาเปลี่ยนขนาดหรือแปลงเป็น PNG ความละเอียดต่ำก่อนส่งให้ OCR วิธีนี้ลดความกดดันของหน่วยความจำและเร่งการประมวลผล

```python
# Example: downscale a huge image (requires Pillow)
from PIL import Image as PilImage

pil_img = PilImage.open(image_path)
pil_img.thumbnail((2000, 2000))  # max dimension 2000px
pil_img.save("temp_resized.png")
ocr_future = ocr_engine.process_async(ocr.Image.load("temp_resized.png"))
```

### การจัดการข้อผิดพลาด  

ห่อการเรียก OCR ด้วยบล็อก `try/except` เพื่อจับข้อผิดพลาดที่เกี่ยวกับเครือข่ายหรือใบอนุญาต

```python
try:
    ocr_result = await ocr_future
except ocr.OcrException as exc:
    print(f"OCR failed: {exc}")
    return ""
```

## ขั้นตอนที่ 5 – ขยายการประมวลผล: ประมวลผลหลายรูปภาพพร้อมกัน  

เนื่องจากฟังก์ชันเป็น async คุณสามารถส่งงาน OCR หลายสิบงานพร้อมกันได้:

```python
async def batch_ocr(image_paths):
    tasks = [async_ocr(p) for p in image_paths]
    return await asyncio.gather(*tasks)

if __name__ == "__main__":
    files = ["doc1.tif", "doc2.tif", "doc3.tif"]
    results = asyncio.run(batch_ocr(files))
    for i, text in enumerate(results):
        print(f"--- Result for {files[i]} ---")
        print(text)
```

รูปแบบนี้ทำให้ CPU ทำงานเต็มที่ในขณะที่เอนจิน OCR ทำงานแบบขนาน, ลดเวลาการประมวลผลโดยรวมอย่างมาก

## สรุป  

คุณมีโซลูชัน **extract text from image Python** ที่แข็งแกร่งและใช้ Aspose OCR API แบบ asynchronous ตัวอย่างเต็มแสดงวิธี:

1. เริ่มต้นเอนจิน OCR และเลือกภาษา  
2. เรียก OCR อย่าง asynchronous ด้วย `process_async`  
3. รอผลลัพธ์โดยไม่บล็อก event loop  
4. จัดการกับปัญหาทั่วไปเช่นไฟล์ขนาดใหญ่และการสนับสนุนหลายภาษา  

คุณสามารถปรับโค้ดให้เข้ากับ pipeline ของคุณได้ ไม่ว่าจะเป็นระบบจัดการเอกสาร, ตัวสร้างดัชนีการค้นหา, หรือยูทิลิตี้บรรทัดคำสั่ง ขั้นตอนต่อไปอาจรวมถึง:

- เก็บข้อความที่สกัดไว้ในฐานข้อมูลเพื่อการค้นหาแบบเต็มข้อความ  
- เพิ่มการสร้าง PDF (เช่น ใช้ `PyPDF2`) เพื่อสร้าง PDF ที่ค้นหาได้  
- ผสานกับเว็บเฟรมเวิร์กอย่าง FastAPI เพื่อสร้างบริการ OCR แบบ RESTful  

ขอให้เขียนโค้ดอย่างสนุกและเพลิดเพลินกับการแปลงรูปสแกนให้เป็นข้อความที่ค้นหาและแก้ไขได้!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}