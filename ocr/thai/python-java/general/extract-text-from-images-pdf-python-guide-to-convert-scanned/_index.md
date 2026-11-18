---
category: general
date: 2026-06-06
description: ดึงข้อความจากไฟล์ PDF ที่เป็นรูปภาพโดยใช้ Python OCR. เรียนรู้วิธีแปลงเอกสารสแกนเป็นข้อความอย่างรวดเร็วด้วยการจดจำแบบแบตช์แบบอะซิงโครนัส.
draft: false
keywords:
- extract text from images pdf
- convert scanned documents to text
- python ocr batch processing
- asynchronous OCR python
- image to text conversion
language: th
og_description: ดึงข้อความจากไฟล์ภาพ PDF ด้วย Python คู่มือขั้นตอนต่อขั้นตอนนี้แสดงวิธีแปลงเอกสารสแกนเป็นข้อความโดยใช้
  OCR แบบอะซิงค์
og_title: สกัดข้อความจากไฟล์ PDF ที่เป็นรูปภาพ – บทเรียน OCR ด้วย Python
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Extract text from images pdf using Python OCR. Learn how to convert
    scanned documents to text quickly with async batch recognition.
  headline: Extract Text from Images PDF – Python Guide to Convert Scanned Documents
    to Text
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: ดึงข้อความจากไฟล์ PDF ภาพ – คู่มือ Python เพื่อแปลงเอกสารสแกนเป็นข้อความ
url: /th/python-java/general/extract-text-from-images-pdf-python-guide-to-convert-scanned/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ดึงข้อความจากไฟล์ PDF รูปภาพ – คู่มือ Python เพื่อแปลงเอกสารสแกนเป็นข้อความ

เคยต้องการ **ดึงข้อความจากไฟล์ PDF รูปภาพ** โดยไม่ต้องใช้เวลาหลายชั่วโมงในการพิมพ์ซ้ำหรือไม่? ในคู่มือนี้เราจะสาธิตวิธี **แปลงเอกสารสแกนเป็นข้อความ** ด้วยกระบวนการ OCR แบบอะซิงโครนัสที่ง่ายใน Python.  

หากคุณเคยมองดูกอง PDF สแกนแล้วคิดว่า “ต้องมีวิธีที่เร็วกว่า” คุณมาถูกที่แล้ว เราจะเดินผ่านทุกบรรทัดของโค้ด, อธิบายว่าทำไมแต่ละส่วนจึงสำคัญ, และแม้แต่ครอบคลุมกรณีขอบที่คุณอาจเจอ.

## สิ่งที่คุณจะได้เรียนรู้

- วิธีสร้างเครื่อง OCR และตั้งค่าภาษาในการจดจำ  
- กลไกการป้อนรายการผสมของ PNG และ PDF ไปยังตัวจดจำแบบแบช  
- การรันงาน OCR แบบอะซิงโครนัสเพื่อให้แอปของคุณตอบสนองได้  
- ดึงผลลัพธ์กลับมา, จับคู่กับไฟล์ต้นฉบับ, และพิมพ์ผลลัพธ์ที่สะอาด  

**Prerequisites**: Python 3.8+, ความเข้าใจพื้นฐานเกี่ยวกับ `asyncio` หรือ `concurrent.futures`, และไลบรารี OCR ที่เปิดเผยคลาส `OcrEngine` คล้ายกับตัวอย่าง (เช่น Aspose.OCR, ตัวห่อ Tesseract, หรือห่อแบบกำหนดเอง). ไม่ต้องตั้งค่าซับซ้อน—เพียงติดตั้งไลบรารีแล้วคุณก็พร้อมใช้งาน.

![ดึงข้อความจากไฟล์ PDF รูปภาพ](https://example.com/placeholder.png "ภาพหน้าจอของผลลัพธ์ OCR – ดึงข้อความจากไฟล์ PDF รูปภาพ")

## ดึงข้อความจากไฟล์ PDF รูปภาพ – การตั้งค่าเครื่อง OCR

สิ่งแรกที่คุณต้องการคืออินสแตนซ์ของเครื่อง OCR ที่กำหนดค่าภาษาของเอกสารของคุณ ในกรณีของเราเราจะใช้ภาษาฝรั่งเศส, แต่คุณสามารถเปลี่ยนเป็นภาษาที่รองรับอื่นได้.

```python
# Import the OCR library – replace with your actual import
from ocr import OcrEngine, Language

# Step 1: Create and configure the OCR engine
engine = OcrEngine()
engine.set_recognition_language(Language.FRENCH)   # Change to Language.ENGLISH, etc.
```

**ทำไมเรื่องนี้ถึงสำคัญ**: การตั้งค่าภาษาไว้ล่วงหน้าช่วยเพิ่มความแม่นยำอย่างมาก. เครื่องใช้พจนานุกรมและโมเดลอักขระเฉพาะภาษา; การป้อนภาษาไม่ตรงเป็นสาเหตุทั่วไปของผลลัพธ์ที่อ่านไม่ออก.

## เตรียมรายการไฟล์ – รูปภาพและ PDF ร่วมกัน

ตัวจดจำแบบแบชของเราสามารถจัดการทั้งภาพเรสเตอร์ (`.png`, `.jpg`) และคอนเทนเนอร์ PDF. เพียงแค่ป้อนรายการ Python ธรรมดาของเส้นทางไฟล์.

```python
# Step 2: Define the files to be processed (use your own directory)
files = [
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.pdf"
]
```

**Tip**: รักษารายการให้เป็นแบน; เครื่องจะทำการแยกแต่ละหน้า PDF เป็นภาพภายในก่อนการจดจำ. หากคุณมีไฟล์หลายพันไฟล์, พิจารณาแบ่งรายการเป็นแบชเล็ก ๆ เพื่อหลีกเลี่ยงการกระตุ้นหน่วยความจำ.

## เริ่มต้นการจดจำแบบแบชแบบอะซิงโครนัส

แทนที่จะบล็อกเธรดหลัก, เราจะเปิดงาน OCR ในพื้นหลัง. เมธอดจะคืนค่า `Future` ที่ในที่สุดจะเก็บรายการของอ็อบเจ็กต์ `OcrResult`.

```python
# Step 3: Start asynchronous batch recognition
future = engine.recognize_batch_async(files)   # returns a Future[List[OcrResult]]
```

**How it works**: ภายใต้ผิวเครื่องจะสร้าง thread pool (หรือ async task, ขึ้นกับการนำไปใช้). สิ่งนี้ทำให้คุณสามารถทำงานอื่นต่อได้—เช่นอัปเดต UI, ดึงไฟล์เพิ่ม, หรือบันทึกความคืบหน้า—ในขณะที่การประมวลผลหนักเกิดขึ้นที่อื่น.

## ทำสิ่งที่เป็นประโยชน์ขณะ OCR ทำงาน

ข้อผิดพลาดทั่วไปคือการนั่งรอและโพล `future` อย่างต่อเนื่อง. แทนที่จะทำเช่นนั้น, คุณสามารถทำงานที่ไม่เกี่ยวข้องอื่น ๆ ได้. เพื่อสาธิต, เราจะพิมพ์บรรทัดสถานะเท่านั้น.

```python
# Step 4: Perform other work while OCR runs
print("Batch started – doing other work...")
# Imagine you could be uploading files, sending heartbeats, etc.
```

## รวบรวมผลลัพธ์เมื่อ Future เสร็จสิ้น

เมื่อคุณพร้อมที่จะเก็บผลลัพธ์ OCR, ใช้ `as_completed` จาก `concurrent.futures`. แพทเทิร์นนี้ทำงานได้ไม่ว่าจะมี future หนึ่งหรือหลายอัน.

```python
from concurrent.futures import as_completed

# Step 5: Wait for the batch to finish and retrieve the results
for completed in as_completed([future]):
    ocr_results = completed.result()   # List[OcrResult] in the same order as `files`
    for path, result in zip(files, ocr_results):
        print(f"{path} →\n{result.text}\n")
```

**What you’ll see**: เส้นทางไฟล์แต่ละอันตามด้วยข้อความที่ดึงออกมาเป็น plain‑text. สำหรับ PDF, `result.text` จะมีข้อความที่ต่อเนื่องจากทุกหน้า.

### ผลลัพธ์ที่คาดหวัง (ตัวอย่าง)

```
YOUR_DIRECTORY/doc1.png →
Bonjour, ceci est un test d’OCR.

YOUR_DIRECTORY/doc2.png →
Le texte de la deuxième image apparaît ici.

YOUR_DIRECTORY/doc3.pdf →
Page 1 du PDF : Lorem ipsum dolor sit amet…
Page 2 du PDF : Consectetur adipiscing elit…
```

หากคุณสังเกตเห็นอักขระหายไป, ตรวจสอบให้แน่ใจว่าภาษาที่ตั้งตรงกับภาษาของเอกสาร, และพิจารณาการพรี‑โปรเซสภาพ (deskew, เพิ่มความคอนทราสต์) ก่อนป้อนให้กับเครื่อง.

## จัดการกรณีขอบและข้อผิดพลาดทั่วไป

| สถานการณ์ | วิธีการทำ |
|-----------|------------|
| **ภาษาผสม** | ทำการตรวจจับภาษาก่อน, จากนั้นสร้างเครื่อง OCR แยกตามแต่ละภาษา. |
| **PDF ขนาดใหญ่ (> 100 MB)** | แยก PDF เป็นหน้าเดี่ยวบนดิสก์ (เช่น ใช้ `PyPDF2`) แล้วป้อนเป็นรายการแยก. |
| **สคริปต์ที่ไม่ใช่ละติน** | ตรวจสอบว่าไลบรารี OCR มีแพ็คเกจภาษาที่ต้องการ; บางไลบรารีต้องดาวน์โหลดไฟล์ข้อมูลเพิ่มเติม. |
| **คอขวดด้านประสิทธิภาพ** | เพิ่มขนาดของ thread pool (`engine.set_thread_pool_size(8)`) หรือเปลี่ยนไปใช้ backend ที่เร่งด้วย GPU หากมี. |
| **ข้อความหายในภาพความละเอียดต่ำ** | ทำการพรี‑โปรเซสด้วย OpenCV: `cv2.resize`, `cv2.threshold`, และ `cv2.medianBlur` เพื่อปรับปรุงความอ่านได้. |

## ตัวอย่างทำงานเต็ม (พร้อมคัดลอก‑วาง)

```python
# ------------------------------------------------------------
# Full script: extract text from images pdf – async OCR batch
# ------------------------------------------------------------
import os
from concurrent.futures import as_completed
# Replace the import below with the actual OCR library you use
from ocr import OcrEngine, Language, OcrResult

def main():
    # 1️⃣ Initialize OCR engine
    engine = OcrEngine()
    engine.set_recognition_language(Language.FRENCH)   # Change as needed

    # 2️⃣ Build list of files (images + PDFs)
    base_dir = "YOUR_DIRECTORY"
    files = [
        os.path.join(base_dir, "doc1.png"),
        os.path.join(base_dir, "doc2.png"),
        os.path.join(base_dir, "doc3.pdf")
    ]

    # 3️⃣ Launch async batch recognition
    future = engine.recognize_batch_async(files)

    # 4️⃣ Do other work – here we just print a placeholder
    print("Batch started – doing other work...")

    # 5️⃣ Retrieve results when ready
    for completed in as_completed([future]):
        ocr_results = completed.result()   # List[OcrResult]
        for path, result in zip(files, ocr_results):
            print(f"{path} →\n{result.text}\n")

if __name__ == "__main__":
    main()
```

บันทึกไฟล์นี้เป็น `extract_text_async.py`, แทนที่ `YOUR_DIRECTORY` ด้วยเส้นทางไปยังไฟล์ของคุณ, ติดตั้งแพคเกจ OCR (`pip install your-ocr-lib`), แล้วรัน `python extract_text_async.py`. คุณควรเห็นผลลัพธ์บนคอนโซลตามที่แสดงไว้ก่อนหน้า.

## ขั้นตอนต่อไป – ไปไกลกว่าการดึงข้อความพื้นฐาน

- **การประมวลผลต่อ**: ลบช่องว่างเพิ่มเติม, ทำให้ Unicode ปกติ (`unicodedata.normalize`), หรือใช้ตัวตรวจสอบการสะกดเพื่อทำความสะอาดเสียงรบกวนจาก OCR.  
- **ผลลัพธ์แบบโครงสร้าง**: ส่งออกผลลัพธ์เป็น CSV, JSON, หรือบันทึกโดยตรงลงฐานข้อมูลเพื่อการค้นหาในขั้นต่อไป.  
- **แบชแบบขนาน**: หากคุณมีไฟล์หลายร้อยไฟล์, สร้างหลาย futures พร้อมใช้คิวเพื่อให้ CPU ทำงานต่อเนื่องโดยไม่ทำให้หน่วยความจำเต็ม.  
- **รวมเข้ากับเว็บเฟรมเวิร์ก**: เชื่อมสคริปต์นี้กับ endpoint ของ Flask หรือ FastAPI เพื่อให้บริการ OCR ตามความต้องการ.

---

### สรุปย่อ

คุณตอนนี้รู้วิธี **ดึงข้อความจากไฟล์ PDF รูปภาพ** ด้วยสคริปต์ Python ขั้นต่ำที่รัน OCR แบบอะซิงโครนัส, ทำให้คุณ **แปลงเอกสารสแกนเป็นข้อความ** ขณะโปรแกรมของคุณยังคงตอบสนองได้. ทดลองปรับตั้งค่าภาษา, ขนาดแบช, และเทคนิคพรี‑โปรเซสเพื่อให้ได้ความแม่นยำสูงสุดของทุกอักขระ.

มีไอเดียหรือวิธีการพิเศษที่อยากแชร์—เช่น OCR บนโน้ตมือเขียนหรือบริการคลาวด์? แสดงความคิดเห็นได้เลย, และขอให้สนุกกับการเขียนโค้ด!

## คุณควรเรียนรู้อะไรต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้. แต่ละแหล่งรวมตัวอย่างโค้ดทำงานครบถ้วนพร้อมคำอธิบายขั้นตอนเพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการนำไปใช้ทางเลือกในโปรเจกต์ของคุณ.

- [ดึงข้อความจากรูปภาพด้วย Aspose OCR – คู่มือขั้นตอนต่อขั้นตอน](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [ดึงข้อความจากรูปภาพโดยใช้การทำงาน OCR บนโฟลเดอร์](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [ดึงข้อความจากรูปภาพโดยใช้ Aspose.OCR – ตัวอักษรที่อนุญาต](/ocr/english/java/advanced-ocr-techniques/specify-allowed-characters/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}