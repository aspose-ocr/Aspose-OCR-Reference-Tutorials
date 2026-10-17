---
category: general
date: 2026-07-05
description: ดึงข้อความจากภาพด้วย Python OCR. เรียนรู้วิธีจดจำข้อความจากภาพ, โหลดภาพสำหรับ
  OCR, และตั้งค่าภาษา OCR เพียงไม่กี่บรรทัด.
draft: false
keywords:
- extract text from image
- how to recognize text from image
- load image for ocr
- create ocr engine python
- set ocr language
language: th
og_description: ดึงข้อความจากภาพด้วย Python OCR คู่มือนี้แสดงวิธีการจดจำข้อความจากภาพ
  โหลดภาพสำหรับ OCR สร้างเครื่องมือ OCR แบบ Python และตั้งค่าภาษา OCR
og_title: สกัดข้อความจากภาพใน Python – จดจำข้อความอย่างรวดเร็ว
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract text from image using Python OCR. Learn how to recognize text
    from image, load image for OCR, and set OCR language in just a few lines.
  headline: Extract Text from Image in Python – Recognize Text Fast
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: สกัดข้อความจากรูปภาพด้วย Python – จดจำข้อความอย่างรวดเร็ว
url: /th/python-java/general/extract-text-from-image-in-python-recognize-text-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ดึงข้อความจากรูปภาพใน Python – จดจำข้อความอย่างรวดเร็ว

เคยต้องการ **ดึงข้อความจากรูปภาพ** แต่ไม่รู้ว่าจะเลือกไลบรารีใด? หากคุณเคยถามตัวเองว่า *วิธีจดจำข้อความจากรูปภาพ* โดยไม่ต้องใช้เครื่องมือภายนอก คุณมาถูกที่แล้ว ในบทแนะนำนี้เราจะสร้างเครื่อง OCR ขนาดเล็ก ชี้ไปที่รูปภาพและดึงข้อความออก—ไม่มีอะไรเพิ่มไม่มีอะไรลด

เราจะเดินผ่านทุกขั้นตอน: **create OCR engine python**, **set OCR language**, **load image for OCR**, เริ่มการจดจำแบบอะซิงโครนัส และสุดท้ายอ่านผลลัพธ์ เมื่อเสร็จคุณจะได้สคริปต์ที่ทำงานได้เองซึ่งสามารถใส่ลงในโปรเจกต์ใดก็ได้ ไม่ว่าจะเป็นตัวแปลงเอกสารเป็นดิจิทัลหรือแชทบอทที่อ่านมีม

## สิ่งที่คุณต้องการ

- Python 3.8+ (โค้ดทำงานได้บน 3.10 และใหม่กว่าเช่นกัน)  
- `ocr` package (wrapper เบา ๆ รอบ Tesseract – ติดตั้งด้วย `pip install ocr` หรือฟอร์กที่คุณชอบ)  
- ไฟล์รูปภาพ (`.jpg`, `.png`, ฯลฯ) ที่มีข้อความที่อ่านได้  
- ความอดทนเล็กน้อยสำหรับส่วน async (มันเร็ว, สัญญา)

เท่านี้—ไม่มีการพึ่งพาที่หนักหน่วง, ไม่มีการคอมไพล์แบบเนทีฟ หากคุณมี Tesseract อยู่ในระบบแล้ว, wrapper `ocr` จะค้นหาโดยอัตโนมัติ

## ขั้นตอนที่ 1: สร้าง OCR Engine – หัวใจของการสกัด

สิ่งแรกที่ต้องทำคือ: คุณต้องมีอ็อบเจกต์ engine ที่รู้วิธีสื่อสารกับ OCR engine ด้านล่าง คิดว่าเป็น “สมอง” ที่จะประมวลผลรูปภาพต่อไป

```python
import ocr

# Step 1: Instantiate the OCR engine
engine = ocr.OcrEngine()
```

*ทำไมสิ่งนี้ถึงสำคัญ*: หากไม่มี engine คุณจะไม่มีบริบทสำหรับการตั้งค่าภาษา หรือความสามารถ async คลาส `OcrEngine` จะซ่อนการเรียกใช้คำสั่งระดับต่ำของ Tesseract ให้คุณได้ API ของ Python ที่สะอาด

## ขั้นตอนที่ 2: ตั้งค่า OCR Language – บอก engine ว่าควรคาดหวังอะไร

หากเอกสารของคุณเป็นภาษาอังกฤษ คุณสามารถใช้ค่าเริ่มต้นได้ แต่ควรตั้งค่าอย่างชัดเจน นี่ยังแสดงวิธี **set OCR language** สำหรับภาษาท้องถิ่นอื่น ๆ

```python
# Step 2: Explicitly set the language to English
engine.language = ocr.Language.ENGLISH
```

> **เคล็ดลับ**: สำหรับ PDF หลายภาษา คุณสามารถส่งรายการเช่น `[ocr.Language.ENGLISH, ocr.Language.FRENCH]` Engine จะพยายามทั้งสองภาษาโดยอัตโนมัติ

## ขั้นตอนที่ 3: โหลดรูปภาพสำหรับ OCR – นำรูปของคุณเข้าสู่หน่วยความจำ

ตอนนี้เราจริง ๆ **load image for OCR**. Wrapper รองรับการโหลดแบบ lazy ดังนั้นไฟล์จะไม่ถูกอ่านจนกว่า engine จะต้องการ

```python
# Step 3: Load the image you want to process
image_path = "YOUR_DIRECTORY/large_document.jpg"
image = ocr.Image.load(image_path)
```

*กรณีขอบ*: หากรูปภาพมีขนาดใหญ่ (เกิน 5 MB) ควรปรับขนาดก่อนเพื่อเร่งการจดจำ คุณสามารถทำได้ด้วย Pillow:

```python
from PIL import Image as PilImage

pil_img = PilImage.open(image_path)
pil_img.thumbnail((2000, 2000))          # keep aspect ratio, max 2000px
pil_img.save("resized.jpg")
image = ocr.Image.load("resized.jpg")
```

## ขั้นตอนที่ 4: เริ่มการจดจำแบบ Asynchronous – ไม่บล็อกแอปของคุณ

การรัน OCR อาจใช้เวลาหนึ่งสองวินาที โดยเฉพาะกับสแกนขนาดใหญ่ เมธอด `recognize_async` จะคืนค่า future ที่คุณสามารถตรวจสอบภายหลัง ทำให้คุณ **ทำงานอื่น ๆ ขณะ OCR ทำงานในพื้นหลัง**

```python
# Step 4: Start the recognition asynchronously
future = engine.recognize_async(image)

# While OCR works, we can do something else
print("Processing other tasks while OCR runs...")
# Example placeholder work
for i in range(3):
    print(f"Task {i+1} done.")
```

ทำไมต้อง async? ในเว็บเซิร์ฟเวอร์คุณไม่ต้องการให้คำขอเดียวทำให้ pool ของ worker หยุดทำงาน วัตถุ future ให้คุณควบคุม: คุณสามารถ `await` ในโค้ด async หรือบล็อกเฉพาะเมื่อคุณต้องการผลลัพธ์จริง ๆ

## ขั้นตอนที่ 5: ดึงผลลัพธ์ – บล็อกเฉพาะเมื่อจำเป็น

เมื่อคุณต้องการข้อความจริง ๆ ให้เรียก `future.get()` การเรียกนี้ **บล็อกเฉพาะที่นี่** หมายความว่าโปรแกรมส่วนอื่นยังตอบสนองได้จนกว่า OCR จะเสร็จ

```python
# Step 5: Get the recognized text (blocks here)
result = future.get()   # blocks only at this point
```

หากคุณอยู่ในลูป `asyncio` คุณสามารถใช้ `await future` แทน – wrapper รองรับทั้งสองรูปแบบ

## ขั้นตอนที่ 6: ใช้ข้อความที่จดจำได้ – ข้อมูลของคุณพร้อมแล้ว

ตอนนี้คุณมีอ็อบเจกต์ `result` แล้ว การดึงสตริงธรรมดาเป็นเรื่องง่าย มาแสดงการพิมพ์และวิธีเขียนลงไฟล์

```python
# Step 6: Output the OCR result
print("OCR completed:")
print(result.text)

# Optional: save to a .txt file
with open("extracted.txt", "w", encoding="utf-8") as f:
    f.write(result.text)
```

**ผลลัพธ์ที่คาดหวัง** (ตัดสั้นเพื่อความกระชับ):

```
OCR completed:
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
```

หากรูปภาพไม่มีข้อความ `result.text` จะเป็นสตริงว่าง—จัดการกรณีนี้อย่างสุภาพ

## ตัวอย่างทำงานเต็มรูปแบบ – ทุกขั้นตอนในสคริปต์เดียว

ด้านล่างเป็นโปรแกรมที่สมบูรณ์พร้อมรัน คัดลอก‑วาง, ปรับ `image_path`, แล้วคุณพร้อมใช้งาน

```python
import ocr
from PIL import Image as PilImage

# -------------------------------------------------
# 1️⃣ Create OCR engine
engine = ocr.OcrEngine()

# 2️⃣ Set language (English)
engine.language = ocr.Language.ENGLISH

# 3️⃣ Load image (optional resize for large files)
original_path = "YOUR_DIRECTORY/large_document.jpg"
pil_img = PilImage.open(original_path)
pil_img.thumbnail((2000, 2000))          # keep aspect ratio
pil_img.save("resized.jpg")
image = ocr.Image.load("resized.jpg")

# 4️⃣ Start async recognition
future = engine.recognize_async(image)
print("Processing other tasks while OCR runs...")
for i in range(3):
    print(f"Task {i+1} done.")

# 5️⃣ Wait for result
result = future.get()

# 6️⃣ Use the text
print("OCR completed:")
print(result.text)
with open("extracted.txt", "w", encoding="utf-8") as f:
    f.write(result.text)
```

> **หมายเหตุ**: แทนที่ `"YOUR_DIRECTORY/large_document.jpg"` ด้วยพาธจริงของรูปภาพของคุณ สคริปต์ทำงานบน Windows, macOS, และ Linux ตราบใดที่ Tesseract ถูกติดตั้งและเข้าถึงได้ใน `PATH` ของคุณ

## ข้อผิดพลาดทั่วไป & วิธีหลีกเลี่ยง

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **อักขระเสีย** | ภาษาไม่ตรงหรือไฟล์ข้อมูลภาษาหายไป. | ตรวจสอบให้ `engine.language` ตรงกับข้อความและไฟล์ `.traineddata` ที่สอดคล้องมีอยู่ในโฟลเดอร์ `tessdata` ของ Tesseract. |
| **ประสิทธิภาพช้าเมื่อภาพใหญ่** | OCR มีการทำงานตามจำนวนพิกเซลโดยประมาณ. | ปรับขนาดหรือทำ down‑sample ก่อนส่งให้ engine (ดูตัวอย่าง Pillow). |
| **Future ไม่เคยสำเร็จ** | ไฟล์ภาพเสียหรือไม่สามารถอ่านได้. | ใส่ `future.get()` ในบล็อก try/except และตรวจสอบ `image.is_valid()` ก่อนการจดจำ. |
| **การสูญเสีย Unicode** |  |  |

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดซึ่งต่อยอดจากเทคนิคในคู่มือนี้ แต่ละแหล่งรวมตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานทางเลือกในโปรเจกต์ของคุณ

- [ดึงข้อความจากรูปภาพด้วย Aspose OCR – คู่มือขั้นตอนต่อขั้นตอน](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [แปลงรูปภาพเป็นข้อความ – ทำ OCR บนรูปจาก URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [ดึงข้อความจากรูปภาพ – การเพิ่มประสิทธิภาพ OCR ด้วย Aspose OCR สำหรับ .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}