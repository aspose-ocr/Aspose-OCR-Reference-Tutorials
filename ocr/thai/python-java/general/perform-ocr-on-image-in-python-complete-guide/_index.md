---
category: general
date: 2026-06-22
description: ทำ OCR บนภาพด้วย Python เพียงไม่กี่บรรทัด เรียนรู้วิธีโหลดภาพสำหรับ OCR,
  แยกข้อความจาก PNG, และใช้เครื่องมือ OCR อย่างมีประสิทธิภาพ
draft: false
keywords:
- perform OCR on image
- recognize text from PNG
- load image for OCR
- use OCR engine
language: th
og_description: ทำ OCR บนรูปภาพอย่างรวดเร็วด้วย Python บทเรียนนี้จะแสดงวิธีโหลดรูปภาพสำหรับ
  OCR, แยกข้อความจากไฟล์ PNG, และใช้เครื่องมือ OCR พร้อมระดับความเชื่อมั่น.
og_title: ทำ OCR บนรูปภาพด้วย Python – คู่มือขั้นตอนโดยละเอียด
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Perform OCR on image using Python in just a few lines. Learn how to
    load image for OCR, recognize text from PNG, and use OCR engine efficiently.
  headline: Perform OCR on Image in Python – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: ทำ OCR บนรูปภาพด้วย Python – คู่มือครบวงจร
url: /th/python-java/general/perform-ocr-on-image-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ทำ OCR บนรูปภาพด้วย Python – คู่มือครบถ้วน

เคยต้องการ **perform OCR on image** ไฟล์แต่รู้สึกติดขัดตั้งแต่บรรทัดแรกของโค้ดหรือไม่? คุณไม่ได้เป็นคนเดียว ในบทแนะนำนี้เราจะสาธิตให้คุณเห็นวิธี **load image for OCR**, ตั้งค่า **OCR engine** ที่เบาและสุดท้าย **recognize text from PNG** ด้วยเพียงไม่กี่คำสั่ง.

เราจะครอบคลุมทุกอย่างตั้งแต่การติดตั้งไลบรารีจนถึงการปรับแต่ง whitelist เพื่อให้มีเฉพาะตัวเลขและอักษรพิมพ์ใหญ่เท่านั้นที่ผ่านการสแกน สิ้นสุดคุณจะได้สคริปต์พร้อมใช้งานที่สามารถใส่ลงในโปรเจกต์ใดก็ได้—ไม่มีความลับ ไม่มีของเพิ่มเกินจำเป็น.

## สิ่งที่คุณจะได้เรียนรู้

- วิธี **use OCR engine** อย่างโปรแกรมใน Python.  
- ขั้นตอนที่แน่นอนในการ **load image for OCR** จากโฟลเดอร์ในเครื่อง.  
- เหตุผลและวิธีการจำกัดการรับรู้ให้เป็นชุดอักขระที่กำหนดเอง.  
- วิธี **recognize text from PNG** และจัดการผลลัพธ์อย่างปลอดภัย.  

**Prerequisites:** ติดตั้ง Python 3.7+ แล้ว, มีเทอร์มินัลที่คุณคุ้นเคย, และมีรูปภาพ (เช่น `serial-number.png`) ที่ต้องการอ่าน ไม่จำเป็นต้องมีประสบการณ์ OCR มาก่อน.

---

## ทำ OCR บนรูปภาพ – เริ่มต้น OCR Engine

สิ่งแรกที่คุณต้องทำคือสร้างอินสแตนซ์ของ OCR engine คิดว่า engine คือสมองที่วิเคราะห์พิกเซลและแปลงเป็นอักขระ.

```python
import ocr  # Assuming the OCR library is named `ocr`

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*Why this matters:* หากไม่มี engine จะไม่มีอะไรประมวลผลภาพ คลาส `OcrEngine` รวมการทำงานหนักทั้งหมด—pre‑processing, segmentation, และ character classification—ไว้ในอ็อบเจกต์เดียวที่คุณสามารถใช้ซ้ำได้.

---

## โหลดรูปภาพสำหรับ OCR – ระบุไฟล์ PNG

เมื่อ engine มีอยู่แล้ว คุณต้องป้อนรูปภาพที่ต้องการอ่านให้มัน ไลบรารีคาดหวังอ็อบเจกต์ `ImageStream` ซึ่งคุณสามารถสร้างโดยตรงจากเส้นทางไฟล์.

```python
# Step 2: Load the image to be processed
image_path = "YOUR_DIRECTORY/serial-number.png"
engine.set_image(ocr.ImageStream.from_file(image_path))
```

*Pro tip:* เก็บภาพในรูปแบบคอนทราสต์สูง (ข้อความสีดำบนพื้นหลังสีขาว) และหลีกเลี่ยงอาร์ติแฟกต์จากการบีบอัด; สิ่งเหล่านี้อาจทำให้ OCR algorithm ทำงานผิดพลาด.

---

## จำกัดอักขระ – Whitelist ตัวเลขและอักษรพิมพ์ใหญ่

บ่อยครั้งคุณสนใจเพียงส่วนย่อยของอักขระเท่านั้น—เช่น หมายเลขซีเรียลที่มีเฉพาะ A‑Z และ 0‑9 การตั้งค่า whitelist จะบอก engine ให้ละเว้นสิ่งอื่นทั้งหมด ซึ่งช่วยเพิ่มความแม่นยำอย่างมาก.

```python
# Step 3: Restrict recognition to digits and uppercase letters
whitelist = "ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789"
engine.get_settings().set_whitelist(whitelist)
```

*What’s happening under the hood?* engine สร้างฟิลเตอร์ที่ตัด glyph ที่ไม่อยู่ใน whitelist ก่อนขั้นตอนการจำแนกขั้นสุดท้าย ซึ่งเป็นประโยชน์มากเมื่อภาพมีสัญญาณรบกวนหรือข้อความตกแต่งที่คุณไม่ต้องการ.

---

## จำแนกข้อความจาก PNG – รันกระบวนการ OCR

เมื่อ engine พร้อมและภาพถูกโหลดแล้ว คุณสามารถ **perform OCR on image** ได้ในที่สุด การเรียก `recognize()` จะรัน pipeline ทั้งหมดและคืนค่าอ็อบเจกต์ผลลัพธ์.

```python
# Step 4: Perform OCR on the image
result = engine.recognize()
```

หากคุณสนใจเรื่องประสิทธิภาพ วิธีนี้มักจะเสร็จภายในไม่กี่ร้อยมิลลิวินาทีสำหรับ PNG ขนาด 300 × 200 px บนแล็ปท็อปสมัยใหม่.

---

## แสดงผลและตรวจสอบ – รับข้อความที่จำแนก

ขั้นตอนสุดท้ายคือดึงข้อความธรรมดาจากอ็อบเจกต์ผลลัพธ์ สิ่งที่ไม่ตรงกับ whitelist จะถูกตัดออกโดยอัตโนมัติ ดังนั้นคุณจะได้สตริงที่สะอาดพร้อมสำหรับการประมวลผลต่อไป.

```python
# Step 5: Output the recognized text (characters outside the whitelist are ignored)
recognized_text = result.get_text()
print(recognized_text)
```

*Typical output:* `AB12C3D4E5` (สมมติว่าภาพมีหมายเลขซีเรียลดังกล่าว).  

หากผลลัพธ์เป็นค่าว่างหรืออ่านไม่ออก ให้ตรวจสอบคุณภาพของภาพและ whitelist อีกครั้ง; ข้อผิดพลาดทั่วไปคือการลบอักขระที่จำเป็นโดยบังเอิญ.

---

## กรณีขอบและข้อผิดพลาดทั่วไป

| Situation | What to Check | Suggested Fix |
|-----------|---------------|---------------|
| **ไฟล์ไม่พบ** | พิมพ์เส้นทางผิดหรือไฟล์หาย | ใช้ `os.path.abspath` เพื่อตรวจสอบเส้นทางเต็มก่อนเรียก `set_image`. |
| **ภาพคอนทราสต์ต่ำ** | ข้อความผสมกับพื้นหลัง | ใช้ threshold อย่างง่าย (`Pillow` หรือ `OpenCV`) ก่อนป้อนภาพให้ engine. |
| **อักขระที่ไม่คาดคิด** | Whitelist จำกัดเกินไป | เพิ่มอักขระที่หายไปในสตริง whitelist. |
| **ภาพขนาดใหญ่** | การจำแนกช้า | ปรับขนาดภาพให้กว้างสูงสุด 1024 px; คุณภาพ OCR มักคงที่. |

---

## สคริปต์เต็ม – พร้อมรัน

ด้านล่างเป็นสคริปต์เต็มที่รวมทุกส่วนเข้าด้วยกัน บันทึกเป็น `ocr_demo.py`, แทนที่ `YOUR_DIRECTORY` ด้วยโฟลเดอร์จริง, แล้วรัน `python ocr_demo.py`.

```python
import ocr
import os

def perform_ocr(image_path: str) -> str:
    """
    Perform OCR on a PNG image and return the recognized text.
    Only uppercase letters and digits are allowed.
    """
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")

    # Initialize the OCR engine
    engine = ocr.OcrEngine()

    # Load the PNG image
    engine.set_image(ocr.ImageStream.from_file(image_path))

    # Whitelist: A-Z and 0-9
    engine.get_settings().set_whitelist("ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789")

    # Run recognition
    result = engine.recognize()

    # Return clean text
    return result.get_text()

if __name__ == "__main__":
    # Adjust the path to point to your PNG file
    png_path = "YOUR_DIRECTORY/serial-number.png"
    try:
        text = perform_ocr(png_path)
        print("Recognized text:", text)
    except Exception as e:
        print("Error during OCR:", e)
```

*Expected console output* (เมื่อ PNG มี `SN12345`):

```
Recognized text: SN12345
```

---

## สรุป

ตอนนี้คุณรู้วิธี **perform OCR on image** ไฟล์ใน Python อย่างแม่นยำ ตั้งแต่ **loading image for OCR** ไปจนถึง **recognize text from PNG** และสุดท้ายการดึงผลลัพธ์ที่สะอาดด้วย **OCR engine** ที่ปรับแต่งได้ วิธีนี้ตรงไปตรงมา ขยายได้ และทำงานได้ทันทีสำหรับการสแกนแบบหมายเลขซีเรียลส่วนใหญ่.

ต่อไปทำอะไร? ลองเปลี่ยน whitelist เป็นอักษรพิมพ์เล็ก, ทดลองรูปแบบภาพต่าง ๆ (JPEG, BMP), หรือรวมสคริปต์เข้ากับ pipeline การประมวลผลแบบแบตช์ รูปแบบเดียวกัน—engine → image → settings → recognize → output—ใช้ได้กับงาน OCR ใด ๆ ที่คุณเจอ.

มีคำถามหรือภาพแปลก ๆ ที่ไม่ทำงาน? แสดงความคิดเห็นด้านล่าง แล้วขอให้สนุกกับการเขียนโค้ด! 

![แผนภาพแสดงขั้นตอนการทำ OCR บนรูปภาพด้วย Python](https://example.com/ocr-flow.png "แผนภาพแสดงวิธีทำ OCR บนรูปภาพด้วย Python OCR engine")


## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดซึ่งต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมตัวอย่างโค้ดที่ทำงานได้เต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานแบบอื่นในโปรเจกต์ของคุณ.

- [แปลงรูปภาพเป็นข้อความ – ทำ OCR บนรูปภาพจาก URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [วิธีใช้ AspOCR: ตัวกรองการเตรียมภาพ OCR สำหรับ .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [วิธีดึงข้อความจากรูปภาพโดยการเตรียมสี่เหลี่ยมใน OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}