---
category: general
date: 2026-01-12
description: วิธีตั้งค่าภาษาใน Aspose OCR Python และดึงข้อความจากภาพโดยใช้พจนานุกรมกำหนดเอง
  ขั้นตอนโดยละเอียดสำหรับนักพัฒนา
draft: false
keywords:
- how to set language
- extract text from image
- how to extract text
- how to add dictionary
- how to process image
language: th
og_description: วิธีตั้งค่าภาษาใน Aspose OCR Python และสกัดข้อความจากภาพด้วยพจนานุกรมที่กำหนดเอง
  เรียนรู้กระบวนการทำงานทั้งหมดในไม่กี่นาที
og_title: วิธีตั้งค่าภาษาใน Aspose OCR Python – คู่มือฉบับสมบูรณ์
tags:
- OCR
- Python
- Aspose
- Image Processing
title: วิธีตั้งค่าภาษาใน Aspose OCR Python – คู่มือเต็ม
url: /th/python-java/general/how-to-set-language-in-aspose-ocr-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีตั้งค่าภาษาใน Aspose OCR Python – คู่มือฉบับสมบูรณ์

เคยสงสัย **วิธีตั้งค่าภาษา** เมื่อใช้ Aspose OCR กับ Python หรือไม่? คุณไม่ได้อยู่คนเดียว—นักพัฒนาหลายคนเจอปัญหาเมื่อโมเดลภาษาอังกฤษเริ่มต้นไม่สามารถอ่านรหัสสินค้า หมายเลขซีเรียล หรือข้อความหลายภาษาได้ ข่าวดีคือวิธีแก้ง่ายและทรงพลัง ในบทแนะนำนี้เราจะพาคุณผ่านการกำหนดค่าภาษา การเพิ่มพจนานุกรมแบบกำหนดเอง การดึงข้อความจากรูปภาพ และสุดท้ายการประมวลผลรูปภาพเพื่อให้ได้ผลลัพธ์ OCR ที่ดีที่สุด

เราจะครอบคลุมทุกอย่างที่คุณต้องรู้ ตั้งแต่การติดตั้งไลบรารีจนถึงการรันตัวอย่างเต็มที่พิมพ์ข้อความที่ดึงออกมา เมื่อจบคุณจะสามารถ **ดึงข้อความจากรูปภาพ** ได้อย่างมั่นใจ แม้เนื้อหาจะมีรหัสแปลกหรือหลายภาษา

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะดำดิ่งลงไป ตรวจสอบให้แน่ใจว่าคุณมี:

* Python 3.8+ ติดตั้งแล้ว (โค้ดใช้ f‑strings ดังนั้นเวอร์ชันเก่าจะไม่ทำงาน)
* ไลเซนส์ Aspose OCR for Python ที่ใช้งานได้หรือคีย์ทดลองฟรี
* แพ็กเกจ `asposeocr` ติดตั้งผ่าน `pip install asposeocr`
* ตัวอย่างรูปภาพ (`product_label.png`) ที่มีข้อความที่คุณต้องการอ่าน

ถ้าคุณมีทั้งหมดแล้ว เยี่ยม—ไปต่อกันเถอะ ถ้ายังไม่มี ให้รับทดลองฟรีจากเว็บไซต์ของ Aspose แล้วรันคำสั่งติดตั้ง; ใช้เวลาเพียงนาทีเดียว

## ขั้นตอนที่ 1: นำเข้าโมดูล Aspose OCR

สิ่งแรกที่คุณต้องทำคือดึงคลาส OCR เข้ามาในสคริปต์ของคุณ นี่คือพื้นฐานสำหรับ **วิธีตั้งค่าภาษา** ต่อไป

```python
# Step 1: Import the Aspose OCR module
import asposeocr as ocr
```

> **เคล็ดลับ:** เก็บการนำเข้าที่ส่วนบนของไฟล์ จะทำให้สคริปต์อ่านง่ายขึ้น โดยเฉพาะเมื่อคุณกลับมาดูใหม่ในภายหลัง

## ขั้นตอนที่ 2: วิธีตั้งค่าภาษา

โดยค่าเริ่มต้น Aspose OCR จะสมมติว่าเป็นภาษาอังกฤษ หากรูปของคุณมีข้อความเป็นภาษาฝรั่งเศส เยอรมัน หรือภาษาอื่นใด คุณต้องบอกให้เอนจินรู้ว่าจะใช้ภาษาอะไร นี่คือจุดที่คีย์เวิร์ดหลักทำงาน

```python
# Step 2: Create an OCR engine and set the recognition language
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH   # change to ocr.Language.FRENCH, etc.
```

ทำไมเรื่องนี้ถึงสำคัญ? เอนจิน OCR พึ่งพาโมเดลอักขระที่เฉพาะเจาะจงตามภาษา การระบุภาษาที่ถูกต้องจะเพิ่มความแม่นยำอย่างมาก—โดยเฉพาะกับอักขระที่มีสำเนียงหรือการเชื่อมตัวอักษรเฉพาะภาษา

> **หมายเหตุ:** หากต้องการรองรับหลายภาษาในเวลาเดียวกัน สามารถส่งรายการเช่น `ocr.Language.ENGLISH | ocr.Language.SPANISH`

## ขั้นตอนที่ 3: วิธีเพิ่มพจนานุกรม (คำที่กำหนดโดยผู้ใช้)

บางครั้งเอนจิน OCR จะอ่านรหัสสินค้าอย่าง “AB‑1234” ผิด คุณสามารถเพิ่มความมั่นใจได้โดยใส่พจนานุกรมแบบกำหนดเอง ซึ่งตอบโดยตรงกับ **วิธีเพิ่มพจนานุกรม** ใน Aspose OCR

```python
# Step 3: Supply product codes that must be recognized with higher confidence
ocr_engine.set_user_defined_words(["AB-1234", "ZX-9876", "SKU-001"])
```

เอนจินจะถือคำเหล่านี้ว่าเป็น “รู้จัก” และจะให้ความสำคัญกับมันเหนืออักขระที่คล้ายกัน สิ่งนี้มีประโยชน์อย่างยิ่งสำหรับหมายเลข SKU, รหัสซีเรียล หรือชื่อแบรนด์ที่ไม่ได้อยู่ในภาษาธรรมชาติ

## ขั้นตอนที่ 4: วิธีประมวลผลรูปภาพ

เมื่อเอนจินถูกตั้งค่าแล้ว คุณต้องโหลดรูปภาพที่ต้องการวิเคราะห์ นี่คือการตอบ **วิธีประมวลผลรูปภาพ** อย่างเป็นระบบและทำซ้ำได้

```python
# Step 4: Load the image containing the product label
image = ocr.Image.load("YOUR_DIRECTORY/product_label.png")
```

หากคุณทำงานกับ PDF สามารถแปลงแต่ละหน้าเป็นรูปภาพก่อน—Aspose OCR รองรับโดยตรง

## ขั้นตอนที่ 5: วิธีดึงข้อความจากรูปภาพ

เมื่อทุกอย่างพร้อม ขั้นตอนสุดท้ายคือรัน OCR และดึงข้อความ นี่คือหัวใจของ **วิธีดึงข้อความ** จากรูปภาพ

```python
# Step 5: Run the OCR process on the loaded image
ocr_result = ocr_engine.process(image)

# Step 6: Print the extracted text
print(ocr_result.text)
```

เมื่อคุณรันสคริปต์ ควรเห็นผลลัพธ์ประมาณนี้:

```
Product: AB-1234
Batch: ZX-9876
SKU: SKU-001
```

หากผลลัพธ์ดูเป็นอักขระผสมกัน ให้ตรวจสอบว่าคุณตั้งค่าภาษาอย่างถูกต้องและพจนานุกรมที่กำหนดเองมีสตริงที่ต้องการครบถ้วนหรือไม่

## ตัวอย่างการทำงานเต็มรูปแบบ

รวมทุกอย่างเข้าด้วยกัน นี่คือสคริปต์เต็มที่คุณสามารถคัดลอก‑วางลงในไฟล์ชื่อ `extract_label.py` อย่าลืมเปลี่ยน `YOUR_DIRECTORY` ให้เป็นพาธจริงของรูปภาพของคุณ

```python
import asposeocr as ocr

# Create OCR engine and set language
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH   # Change if needed

# Add custom dictionary entries
ocr_engine.set_user_defined_words(["AB-1234", "ZX-9876", "SKU-001"])

# Load the target image
image = ocr.Image.load("YOUR_DIRECTORY/product_label.png")

# Perform OCR
ocr_result = ocr_engine.process(image)

# Output the result
print("=== OCR Extraction Result ===")
print(ocr_result.text)
```

### ผลลัพธ์ที่คาดหวัง

```
=== OCR Extraction Result ===
Product: AB-1234
Batch: ZX-9876
SKU: SKU-001
```

หากคุณเห็นรหัสที่เพิ่มเข้าไปในพจนานุกรมอย่างแม่นยำ คุณได้เชี่ยวชาญ **วิธีตั้งค่าภาษา**, **วิธีเพิ่มพจนานุกรม**, และ **วิธีดึงข้อความจากรูปภาพ** ด้วย Aspose OCR แล้ว

## การจัดการกรณีขอบที่พบบ่อย

| สถานการณ์ | วิธีทำ |
|-----------|--------|
| **ภาพเบลอ** | ทำการประมวลผลล่วงหน้าด้วย `ocr.Image.apply_filter()` เพื่อทำให้คมก่อนเรียก `process()` |
| **หลายภาษาในภาพเดียว** | ตั้งค่า `ocr_engine.language = ocr.Language.ENGLISH | ocr.Language.SPANISH` |
| **PDF ขนาดใหญ่** | วนลูปแต่ละหน้า แปลงเป็น `ocr.Image` และเรียก `process()` สำหรับแต่ละหน้า |
| **อักขระที่ไม่คาดคิด** | เพิ่มลงในรายการคำที่กำหนดโดยผู้ใช้; Aspose OCR จะถือว่ามันเป็นโทเคนที่มีความมั่นใจสูง |

## อ้างอิงภาพ

![ภาพหน้าจอแสดงวิธีตั้งค่าภาษาใน Aspose OCR example](image.png "ภาพหน้าจอแสดงวิธีตั้งค่าภาษาในตัวอย่าง Aspose OCR Python")

*ข้อความแทนภาพ:* **วิธีตั้งค่าภาษา** ภาพหน้าจอที่แสดงการกำหนดคุณสมบัติ language ใน IDE ของ Python

## สรุป

คุณตอนนี้รู้แล้วว่า **วิธีตั้งค่าภาษา** ใน Aspose OCR Python, วิธี **เพิ่มพจนานุกรม** และขั้นตอนที่แม่นยำในการ **ดึงข้อความจากรูปภาพ** และ **ประมวลผลรูปภาพ** เพื่อผลลัพธ์ที่ดีที่สุด ตัวอย่างเต็มที่ให้ไว้ข้างต้นสามารถนำไปใช้ในโปรเจกต์ใดก็ได้ ปรับเปลี่ยนสำหรับภาษาต่าง ๆ และขยายเพื่อรองรับการประมวลผลเป็นชุดหรือไฟล์ PDF

พร้อมรับความท้าทายต่อไปหรือยัง? ลองสลับ `ocr.Language.ENGLISH` เป็น `ocr.Language.FRENCH` แล้วสังเกตการเพิ่มความแม่นยำบนป้ายที่เป็นภาษาฝรั่งเศส หรือทดลองใช้เมธอด `set_user_defined_words` เพื่อใส่แคตตาล็อกสินค้าทั้งหมด—เอนจิน OCR ของคุณจะถือทุกรายการเป็นการจับคู่ที่มีความมั่นใจสูง

ขอให้เขียนโค้ดอย่างสนุกสนานและผลลัพธ์ OCR ของคุณใสเหมือนคริสตัล! 

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}