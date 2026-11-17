---
category: general
date: 2026-06-06
description: ดึงข้อความจากภาพด้วย Python OCR ภายในไม่กี่นาที ค้นพบ OCR ภาพหลายภาษา
  การตรวจจับภาษาอัตโนมัติด้วย OCR และวิธีดึงข้อความ OCR อย่างแม่นยำ.
draft: false
keywords:
- extract text from image
- how to extract OCR text
- multilingual image OCR
- detect language OCR
- auto detect language OCR
language: th
og_description: ดึงข้อความจากรูปภาพด้วย Python OCR อย่างรวดเร็ว เรียนรู้การทำ OCR
  ภาพหลายภาษา การตรวจจับภาษาที่อัตโนมัติด้วย OCR และวิธีการดึงข้อความ OCR ทีละขั้นตอน
og_title: สกัดข้อความจากภาพโดยใช้ Python OCR – คู่มือฉบับสมบูรณ์
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Extract text from image with Python OCR in minutes. Discover multilingual
    image OCR, auto detect language OCR, and how to extract OCR text accurately.
  headline: Extract Text from Image Using Python OCR – Complete Guide
  type: TechArticle
- description: Extract text from image with Python OCR in minutes. Discover multilingual
    image OCR, auto detect language OCR, and how to extract OCR text accurately.
  name: Extract Text from Image Using Python OCR – Complete Guide
  steps:
  - name: '**Low‑resolution images** – OCR accuracy drops sharply below 150 dpi. Upscale
      or request a higher‑resolution scan.'
    text: '**Low‑resolution images** – OCR accuracy drops sharply below 150 dpi. Upscale
      or request a higher‑resolution scan.'
  - name: '**Noise and compression artifacts** – Apply a simple threshold filter (`opencv`
      or `Pillow`) before feeding the image to the engine.'
    text: '**Noise and compression artifacts** – Apply a simple threshold filter (`opencv`
      or `Pillow`) before feeding the image to the engine.'
  - name: '**Mixed scripts on one page** – Some engines struggle with simultaneous
      Latin and CJK characters. Split the page into regions and run separate recognitions
      if needed.'
    text: '**Mixed scripts on one page** – Some engines struggle with simultaneous
      Latin and CJK characters. Split the page into regions and run separate recognitions
      if needed.'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- Multilingual
title: สกัดข้อความจากภาพด้วย Python OCR – คู่มือครบวงจร
url: /th/python-java/general/extract-text-from-image-using-python-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ดึงข้อความจากภาพด้วย Python OCR – คู่มือฉบับเต็ม

เคยต้อง **ดึงข้อความจากภาพ** แต่ไม่แน่ใจว่าห้องสมุดใดสามารถจัดการหลายภาษาโดยอัตโนมัติได้หรือไม่? คุณไม่ได้อยู่คนเดียว—นักพัฒนามักถามว่า *วิธีดึงข้อความ OCR* อย่างไรเมื่อทำงานกับเอกสารระหว่างประเทศ, ใบเสร็จ, หรือโบรชัวร์ที่สแกนไว้ ในบทเรียนนี้เราจะเดินผ่านตัวอย่าง Python ที่ใช้งานได้จริง ซึ่งไม่เพียงดึงข้อความจากภาพเท่านั้น แต่ยัง **ตรวจจับภาษา** ไปพร้อมกัน ทำให้ OCR ภาพหลายภาษากลายเป็นเรื่องง่าย

เราจะครอบคลุมตั้งแต่การติดตั้งแพคเกจ OCR ไปจนถึงการเปิดใช้งาน **auto detect language OCR**, การรันเอนจินบนภาพตัวอย่าง, และสุดท้ายการพิมพ์ทั้งภาษาที่ตรวจจับได้และสตริงที่ดึงออกมา เมื่อจบคุณจะมีสคริปต์ที่นำกลับไปใช้ได้ในทุกโปรเจกต์ ไม่ว่าจะเป็นการสร้าง pipeline แปลภาษา หรือบริการ ingest ข้อมูล

## ดึงข้อความจากภาพ – การตั้งค่าสภาพแวดล้อม

ก่อนที่เราจะลงลึกในโค้ด ให้ตรวจสอบว่าเครื่องของคุณตรงตามข้อกำหนดขั้นต่ำเหล่านี้:

- Python 3.8 หรือใหม่กว่า (ไลบรารีใช้ type hints ที่เวอร์ชันเก่าจะไม่รองรับ)
- `pip` สำหรับจัดการแพคเกจ
- ไฟล์ภาพที่มีข้อความอย่างน้อยสองภาษา (เช่น English + Spanish)

คุณยังต้องการไลบรารี OCR ที่เป็นหัวใจของเดโมนี้ สำหรับคู่มือนี้เราจะใช้แพคเกจสมมติ `ocr` ซึ่งทำหน้าที่คล้ายเครื่องมือจริงเช่น Tesseract หรือ EasyOCR แต่มี API ของ Python ที่เรียบง่าย

```bash
# Install the OCR package and its optional image dependencies
pip install ocr[image]
```

> **Pro tip:** หากเจอข้อผิดพลาดเรื่องสิทธิ์ ให้ใส่ `python -m` ไว้หน้าคำสั่งหรือใช้ virtual environment—จะทำให้แพคเกจในระบบหลักของคุณสะอาดขึ้น

## สร้างอินสแตนซ์ของ OCR Engine

เมื่อไลบรารีพร้อมแล้ว ขั้นตอนแรกที่มีเหตุผลคือ **สร้างอินสแตนซ์ของ OCR engine** คิดว่าเอนจินเป็นสแกนเนอร์อัจฉริยะที่คุณสามารถตั้งค่าก่อนใส่ภาพเข้าไป

```python
import ocr

# Step 1: Initialize the OCR engine
engine = ocr.OcrEngine()
```

ทำไมต้องสร้างอินสแตนซ์แยกจากการเรียกเมธอดแบบสแตติก? อินสแตนซ์นี้เก็บสถานะการตั้งค่า (เช่น การตั้งค่าภาษา) ที่คุณอาจต้องการใช้ซ้ำหลายภาพ ลดภาระการสร้างใหม่ทุกครั้ง

## เปิดใช้งาน Auto Detect Language OCR

เครื่องมือ OCR ส่วนใหญ่ต้องระบุรหัสภาษา—`eng` สำหรับอังกฤษ, `spa` สำหรับสเปน, ฯลฯ การคาดเดาภาษาเองทำให้เสียจุดประสงค์ของ **multilingual image OCR** โชคดีที่แพคเกจ `ocr` มีโหมด *auto detect language OCR* ที่ตรวจสอบภาพและเลือกโมเดลภาษาที่เหมาะสมโดยอัตโนมัติ

```python
# Step 2: Turn on automatic language detection
engine.set_recognition_language(ocr.Language.AUTO_DETECT)
```

การเปิด **detect language OCR** แบบนี้หมายความว่าคุณไม่ต้องดูแลรายการรหัสภาษายาว ๆ เอนจินจะพยายามจับสคริปต์ที่พบ—Latin, Cyrillic, Han ฯลฯ—และโหลดโมเดลที่ตรงกันโดยอัตโนมัติ

## ทำ Multilingual Image OCR

เมื่อเอนจินพร้อมแล้ว ถึงเวลาที่จะ **ดึงข้อความจากภาพ** จริง ๆ เมธอด `recognize_image` รับพาธไฟล์และคืนค่าอ็อบเจ็กต์ผลลัพธ์ที่มีทั้งข้อความดิบและภาษาที่ตรวจจับได้

```python
# Step 3: Run OCR on a multilingual image
image_path = "YOUR_DIRECTORY/multilang_page.png"
result = engine.recognize_image(image_path)
```

ถ้าคุณสงสัยว่า *วิธีดึงข้อความ OCR* จาก PDF แทน PNG คืออะไร เอนจินเดียวกันมี `recognize_pdf`—เพียงเปลี่ยนชื่อเมธอด การทำงานของการตรวจจับพื้นฐานยังคงเหมือนเดิม ดังนั้นคุณจะได้ประโยชน์จากฟีเจอร์ **auto detect language OCR** เหมือนกัน

## แสดงภาษาที่ตรวจจับและข้อความที่ดึงออกมา

สุดท้าย เราจะพิมพ์สิ่งที่เอนจินค้นพบ อ็อบเจ็กต์ผลลัพธ์เปิดเผย `detected_language` (แท็ก BCP‑47 เช่น `en` หรือ `es`) และ `text` ซึ่งเป็นผลลัพธ์ OCR ดิบ

```python
# Step 4: Show the language and the extracted string
print(f"Detected language: {result.detected_language}")
print("Extracted text:")
print(result.text)
```

การรันสคริปต์บนภาพตัวอย่างของเราควรให้ผลลัพธ์คล้ายกับ:

```
Detected language: en
Extracted text:
Welcome to our multilingual brochure.
¡Bienvenidos a nuestro folleto multilingüe!
```

สังเกตว่าเอนจินระบุอังกฤษเป็นภาษาหลักได้อย่างถูกต้อง แต่ก็ยังจับบรรทัดสเปนได้—พฤติกรรมที่คุณคาดหวังจากโซลูชัน **multilingual image OCR** ที่แข็งแกร่ง

### ถ้าการตรวจจับล้มเหลวจะทำอย่างไร?

บางครั้งเอนจิน OCR อาจย้อนกลับไปใช้ภาษาดีฟอลต์ (มักเป็นอังกฤษ) หากภาพเบลอหรือสคริปต์แปลกเกินไป ในกรณีนั้นคุณสามารถบังคับให้ใช้รายการภาษาได้:

```python
engine.set_recognition_language([ocr.Language.ENGLISH, ocr.Language.SPANISH])
```

แต่จำไว้ว่า การบังคับภาษาอาจทำให้เสียความสะดวกของ **auto detect language OCR** ดังนั้นให้ใช้เฉพาะเมื่อคุณรู้ชุดภาษาที่ต้องการเท่านั้น

## ปัญหาที่พบบ่อยและวิธีดึง OCR Text อย่างเชื่อถือได้

แม้จะเปิด auto‑detection แล้ว ยังมีอุปสรรคเล็กน้อยที่อาจทำให้คุณติดขัด:

1. **ภาพความละเอียดต่ำ** – ความแม่นยำของ OCR ลดลงอย่างชัดเจนเมื่อต่ำกว่า 150 dpi ให้ทำการอัปสเกลหรือขอสแกนความละเอียดสูงขึ้น
2. **นอยส์และอาร์ติแฟคต์จากการบีบอัด** – ใช้ฟิลเตอร์ threshold ง่าย ๆ (`opencv` หรือ `Pillow`) ก่อนส่งภาพให้เอนจิน
3. **สคริปต์ผสมบนหน้าเดียว** – บางเอนจินทำงานได้ยากกับอักษร Latin และ CJK พร้อมกัน ให้แบ่งหน้าเป็นโซนและรันการจดจำแยกส่วนตามต้องการ

การแก้ไขปัญหาเหล่านี้จะทำให้กระบวนการ **extract text from image** มีคุณภาพดีขึ้นอย่างมาก โดยเฉพาะเมื่อจัดการกับเอกสารหลายภาษาในโลกจริง

## ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นสคริปต์สมบูรณ์พร้อมรันที่รวมทุกขั้นตอนที่เราได้อธิบายไว้ บันทึกเป็น `multilingual_ocr.py` แล้วเรียกจาก command line

```python
import ocr

def main():
    # Initialize engine with auto language detection
    engine = ocr.OcrEngine()
    engine.set_recognition_language(ocr.Language.AUTO_DETECT)

    # Path to your multilingual image
    image_path = "YOUR_DIRECTORY/multilang_page.png"

    # Perform OCR
    result = engine.recognize_image(image_path)

    # Output results
    print(f"Detected language: {result.detected_language}")
    print("Extracted text:")
    print(result.text)

if __name__ == "__main__":
    main()
```

**ผลลัพธ์ที่คาดหวัง** (สมมติว่าภาพตัวอย่างมีข้อความอังกฤษและสเปน):

```
Detected language: en
Extracted text:
Welcome to our multilingual brochure.
¡Bienvenidos a nuestro folleto multilingüe!
```

คุณสามารถเปลี่ยน `multilang_page.png` เป็นภาพใดก็ได้ที่มีข้อความในภาษาต่าง ๆ — ด้วย **auto detect language OCR** สคริปต์จะยังคงให้แท็กภาษาที่เหมาะสมและข้อความที่สอดคล้องกัน

![Extract text from image example](https://example.com/ocr-sample.png "Extract text from image")

## สรุป

ตอนนี้คุณรู้แล้วว่า **วิธีดึง OCR text** จากภาพอย่างไร, วิธีเปิด **auto detect language OCR**, และวิธีจัดการกับสถานการณ์ **multilingual image OCR** ด้วยโค้ดเพียงไม่กี่บรรทัด โดยการสร้างอินสแตนซ์ OCR engine, เปิดการตรวจจับภาษาอัตโนมัติ, และเรียก `recognize_image` คุณสามารถดึงทั้งตัวระบุภาษาและข้อความดิบได้อย่างน่าเชื่อถือ

ต่อไปคุณจะทำอะไร? ลองส่งสตริงที่ดึงมาไปยัง API แปลภาษา, เก็บไว้ในฐานข้อมูลที่ค้นหาได้, หรือรวมหลายหน้าเป็น PDF รายงานเดียว คุณยังสามารถทดลองใช้ backend OCR ต่าง ๆ (Tesseract, EasyOCR, Google Vision) โดยคง workflow ระดับสูงเดียวกัน—ขอบคุณอินเทอร์เฟซ **detect language OCR** ที่สอดคล้องกัน

หากเจอข้อผิดพลาดใด ๆ ให้กลับไปอ่านส่วน “ปัญหาที่พบบ่อย” หรือปรับขั้นตอนการเตรียมภาพ Happy coding, และขอให้โปรเจกต์ต่อไปของคุณเต็มไปด้วยข้อความที่ตรวจจับได้ถูกต้องและดึงออกมาอย่างสมบูรณ์!

## คุณควรเรียนรู้อะไรต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคในคู่มือนี้ แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโปรเจกต์ของคุณ

- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [recognize text image with Aspose OCR for multiple languages](/ocr/english/net/ocr-settings/working-with-different-languages/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}