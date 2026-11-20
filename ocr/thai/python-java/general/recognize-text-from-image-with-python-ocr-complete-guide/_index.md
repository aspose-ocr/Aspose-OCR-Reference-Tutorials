---
category: general
date: 2026-06-16
description: จดจำข้อความจากภาพด้วยเครื่องมือ OCR ของ Python – เรียนรู้วิธีดึงข้อความจากใบเสร็จและเพิ่มความแม่นยำของ
  OCR ภายในไม่กี่นาที.
draft: false
keywords:
- recognize text from image
- extract text from receipt
- improve ocr accuracy
- python ocr tutorial
- image preprocessing for OCR
language: th
og_description: จดจำข้อความจากภาพอย่างรวดเร็ว คู่มือนี้แสดงวิธีดึงข้อความจากใบเสร็จและปรับปรุงความแม่นยำของ
  OCR ด้วย Python.
og_title: การจดจำข้อความจากภาพด้วย Python OCR – คู่มือฉบับสมบูรณ์
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: recognize text from image using a Python OCR engine – learn how to
    extract text from receipt and improve OCR accuracy in minutes.
  headline: recognize text from image with Python OCR – Complete Guide
  type: TechArticle
- description: recognize text from image using a Python OCR engine – learn how to
    extract text from receipt and improve OCR accuracy in minutes.
  name: recognize text from image with Python OCR – Complete Guide
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed on your machine. - Basic familiarity with pip and
      virtual environments. - A sample receipt image (JPEG or PNG) that you want to
      process. - The `ocr` package (the example uses a fictional `ocr` module for
      illustration; replace it with `pytesseract`, `easyocr`, or any library t'
  - name: Expected Output
    text: 'Running the script on a typical grocery receipt yields something like:'
  - name: H3 – Crop to the Receipt Region
    text: 'If your image contains a lot of background (e.g., a photo of a desk), crop
      it first:'
  - name: H3 – Use a Custom Language Pack
    text: 'For receipts that contain foreign characters (e.g., “€” or “¥”), load the
      appropriate language data:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: แยกข้อความจากภาพด้วย Python OCR – คู่มือฉบับสมบูรณ์
url: /th/python-java/general/recognize-text-from-image-with-python-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# จดจำข้อความจากรูปภาพด้วย Python OCR – คู่มือฉบับสมบูรณ์

เคยต้อง **จดจำข้อความจากรูปภาพ** แล้วผลลัพธ์ออกมาดูเหมือนอักขระไร้สาระหรือไม่? คุณไม่ได้เป็นคนเดียว ในหลายสถานการณ์ของธุรกิจขนาดเล็ก—เช่นการสแกนใบเสร็จ, การแปลงใบแจ้งหนี้เป็นดิจิทัล, หรือการดึงข้อมูลจากบัตรประจำตัว—การได้ผลลัพธ์ที่สะอาดและเชื่อถือได้คือความแตกต่างระหว่างกระบวนการทำงานที่ราบรื่นและความวุ่นวาย

ในบทเรียนนี้เราจะพาคุณผ่านวิธีปฏิบัติจริงเพื่อ **จดจำข้อความจากรูปภาพ** ด้วยไลบรารี OCR ของ Python ที่มีขนาดเบา เราจะสาธิตวิธี **ดึงข้อความจากใบเสร็จ** อย่างละเอียดและแชร์เคล็ดลับเพื่อ **ปรับปรุงความแม่นยำของ OCR** โดยไม่ต้องซื้อซอฟต์แวร์ราคาแพง พร้อมหรือยัง? ไปดูกันเลย

## สิ่งที่คุณจะสร้าง

เมื่อจบคู่มือนี้คุณจะมีสคริปต์พร้อมรันที่:

1. สร้างอินสแตนซ์ของ OCR engine.  
2. เปิดใช้งานการพรีโพรเซสอัจฉริยะ (deskew, despeckle, binarization).  
3. โหลดรูปใบเสร็จที่มีสัญญาณรบกวน.  
4. รัน pipeline การจดจำโดยอัตโนมัติ.  
5. พิมพ์ข้อความที่สะอาดและค้นหาได้ลงคอนโซล.

ไม่มีบริการภายนอก ไม่มีคีย์ API ที่ซ่อนอยู่—แค่โค้ด Python ธรรมดาที่คุณสามารถปรับใช้กับโปรเจกต์ใดก็ได้

### ข้อกำหนดเบื้องต้น

- Python 3.8+ ติดตั้งบนเครื่องของคุณ  
- มีความคุ้นเคยพื้นฐานกับ pip และ virtual environments  
- มีรูปใบเสร็จตัวอย่าง (JPEG หรือ PNG) ที่ต้องการประมวลผล  
- แพ็กเกจ `ocr` (ตัวอย่างใช้โมดูล `ocr` สมมุติสำหรับอธิบาย; ให้แทนที่ด้วย `pytesseract`, `easyocr` หรือไลบรารีอื่นที่มี API คล้ายกัน)

> **Pro tip:** หากเจอการพึ่งพาที่ขาดหาย ให้ติดตั้งด้วย `pip install ocr` (หรือชื่อแพ็กเกจจริง) ก่อนดำเนินการต่อ

## ขั้นตอนที่ 1 – จดจำข้อความจากรูปภาพ: ตั้งค่า Engine

อย่างแรกที่ต้องทำ เราต้องมีอ็อบเจกต์ที่รู้วิธีอ่านข้อมูลพิกเซลและแปลงเป็นอักขระ คิดว่า engine คือสมองของกระบวนการ; ทุกอย่างอื่นจะส่งข้อมูลให้มัน

```python
import ocr  # Replace with your actual OCR library import

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

ทำไมต้องสร้าง engine ด้วยตนเอง? ไลบรารีบางตัวให้เรียกฟังก์ชันเดียวก็ได้ แต่การสร้างอินสแตนซ์อย่างชัดเจนทำให้คุณควบคุมการพรีโพรเซสได้ละเอียด—ซึ่งเป็นสิ่งที่จำเป็นเพื่อ **ปรับปรุงความแม่นยำของ OCR** ในขั้นต่อไป

## ขั้นตอนที่ 2 – ดึงข้อความจากใบเสร็จ: เปิดใช้งานการพรีโพรเซส

ใบเสร็จที่สแกนด้วยกล้องโทรศัพท์มักไม่สมบูรณ์ มันอาจเอียงเล็กน้อย มีฝุ่น หรือแสงไม่สม่ำเสมอ การเปิดใช้งานการพรีโพรเซสทำให้ทำงานหนักก่อนที่ engine จะมองตัวอักษร

```python
# Step 2: Enable preprocessing to improve recognition quality
preprocess = engine.preprocessing
preprocess.deskew = True        # Auto‑rotate slightly tilted pages
preprocess.despeckle = True     # Remove isolated noise pixels
preprocess.binarization = True  # Convert image to pure black‑white
```

*Deskew* ทำให้หน้าเรียบตรง, *despeckle* ลบจุดรบกวน, และ *binarization* ทำให้พิกเซลเป็นสีดำหรือสีขาวเท่านั้น ทั้งสามฟลักนี้สามารถ **ปรับปรุงความแม่นยำของ OCR** ได้ 20‑30 % บนใบเสร็จที่มีสัญญาณรบกวน

## ขั้นตอนที่ 3 – โหลดรูปภาพที่ต้องการจดจำ

ต่อไปเราชี้ engine ไปที่ไฟล์จริง พาธสามารถเป็นแบบ absolute หรือ relative; เพียงแค่ตรวจสอบให้แน่ใจว่ารูปภาพมีอยู่

```python
# Step 3: Load the scanned receipt image
engine.image = ocr.Image.load_from_file("YOUR_DIRECTORY/receipt-noisy.jpg")
```

หากคุณสงสัยว่า engine รองรับ PDF หรือ TIFF หลายหน้าไหม ไลบรารีสมัยใหม่ส่วนใหญ่รองรับ—แค่ตรวจสอบเอกสารของมัน สำหรับ JPEG หน้าหนึ่งบรรทัดด้านบนก็เพียงพอ

## ขั้นตอนที่ 4 – รัน OCR – Engine ทำส่วนที่เหลือ

เมื่อตั้งค่าการพรีโพรเซสและโหลดรูปแล้ว การเรียกครั้งต่อไปจะทำทุกอย่าง: พรีโพรเซส, รันอัลกอริทึมจดจำ, และคืนอ็อบเจกต์ผลลัพธ์

```python
# Step 4: Run OCR – the configured preprocessing is applied automatically
ocr_result = engine.recognize()
```

เบื้องหลัง engine อาจใช้ Tesseract, neural network, หรือ engine ที่เป็นกรรมสิทธิ์ คุณไม่จำเป็นต้องรู้รายละเอียดภายใน; คุณแค่ได้รับผลลัพธ์ที่สะอาด

## ขั้นตอนที่ 5 – แสดงข้อความที่จดจำได้

สุดท้ายเราดึง plain‑text จากผลลัพธ์และพิมพ์ออก หากเป็นแอปพลิเคชันจริงคุณอาจบันทึกลงฐานข้อมูล, ไฟล์ CSV, หรือส่งต่อไปยัง pipeline การวิเคราะห์ต่อไป

```python
# Step 5: Output the recognized text
print(ocr_result.text)
```

### ผลลัพธ์ที่คาดหวัง

รันสคริปต์บนใบเสร็จของร้านขายของชำทั่วไปจะได้ผลลัพธ์ประมาณนี้:

```
WALMART STORE #1234
123 Main St.
Anytown, USA

Date: 06/15/2026   Time: 14:32
Cashier: J. Doe

Item                Qty   Price
---------------------------------
Milk                1     2.99
Bread               2     5.48
Eggs                1     3.20
---------------------------------
Subtotal                    11.67
Tax                         0.93
Total                       12.60
```

หากผลลัพธ์ดูเป็นอักขระผสมกัน ให้ตรวจสอบว่าฟลักการพรีโพรเซสเปิดอยู่และรูปภาพไม่ได้มืดเกินไป การปรับค่า threshold ของ binarization (บางไลบรารีให้ตั้งค่าที่กำหนดเอง) สามารถ **ปรับปรุงความแม่นยำของ OCR** ได้อีก

## ขั้นสูง: ปรับจูนเพื่อดึงข้อความจากใบเสร็จให้เร็วขึ้น

แม้กระบวนการ 5 ขั้นตอนจะทำงานได้ดีในหลายกรณี แต่คุณอาจต้องการเร่งความเร็วเมื่อต้องประมวลผลหลายร้อยใบเสร็จต่อคืน นี่คือเคล็ดลับเสริมสองอย่าง:

### H3 – ครอบตัดส่วนที่เป็นใบเสร็จ

หากรูปของคุณมีพื้นหลังมาก (เช่น ภาพโต๊ะทำงาน) ให้ครอบตัดก่อน:

```python
engine.image = engine.image.crop((50, 200, 800, 1200))  # left, top, right, bottom
```

### H3 – ใช้แพ็คเกจภาษาแบบกำหนดเอง

สำหรับใบเสร็จที่มีอักขระต่างประเทศ (เช่น “€” หรือ “¥”) ให้โหลดข้อมูลภาษาที่เหมาะสม:

```python
engine.set_language('eng+deu+fra')  # English, German, French
```

ทั้งสองวิธีช่วยให้ engine **จดจำข้อความจากรูปภาพ** ได้แม่นยำยิ่งขึ้น โดยเฉพาะเมื่อแหล่งข้อมูลมีความหลากหลาย

## ข้อผิดพลาดทั่วไปและวิธีหลีกเลี่ยง

- **Missing Fonts:** OCR engine บางตัวต้องการไฟล์ฟอนต์สำหรับฟอนต์ใบเสร็จเฉพาะ ให้ติดตั้ง language pack ที่เหมาะสม  
- **Too Much Noise:** แม้จะตั้ง `despeckle=True` แล้ว สแกนที่มีเม็ดฝุ่นมากอาจยังทำให้ engine สับสนได้ การกรองด้วย Pillow (`Image.filter(ImageFilter.MedianFilter)`) ช่วยได้  
- **Incorrect DPI:** OCR engine คาดว่าภาพอยู่ที่ประมาณ 300 dpi หากภาพของคุณต่ำกว่า ให้ปรับขนาดก่อน: `engine.image = engine.image.resize((width*2, height*2))`

การแก้ไขปัญหาเหล่านี้โดยตรง **ปรับปรุงความแม่นยำของ OCR** โดยไม่ต้องพึ่งบริการภายนอกที่มีค่าใช้จ่ายสูง

## สคริปต์เต็ม – พร้อมรัน

ด้านล่างเป็นโปรแกรม Python ที่ทำงานได้เต็มรูปแบบและรวมทุกอย่างที่เราได้พูดถึง บันทึกเป็น `receipt_ocr.py` แล้วรันด้วย `python receipt_ocr.py`

```python
import ocr  # Replace with the actual library you use

def main():
    # Initialize the OCR engine
    engine = ocr.OcrEngine()

    # Enable preprocessing steps
    preprocess = engine.preprocessing
    preprocess.deskew = True
    preprocess.despeckle = True
    preprocess.binarization = True

    # Load the receipt image (change the path to your file)
    engine.image = ocr.Image.load_from_file("YOUR_DIRECTORY/receipt-noisy.jpg")

    # Optional: crop out unnecessary background
    # engine.image = engine.image.crop((50, 200, 800, 1200))

    # Run the recognition pipeline
    result = engine.recognize()

    # Print the extracted text
    print("=== Recognized Text ===")
    print(result.text)

if __name__ == "__main__":
    main()
```

การรันสคริปต์นี้จะ **จดจำข้อความจากรูปภาพ** และพิมพ์บล็อกข้อมูลใบเสร็จที่จัดรูปแบบอย่างสวยงาม คุณสามารถปรับพิกัดการครอบตัด, การตั้งค่าภาษา, หรือฟลักการพรีโพรเซสให้ตรงกับรูปแบบใบเสร็จของคุณเองได้

## สรุป

เราได้อธิบายวิธีง่าย ๆ เพื่อ **จดจำข้อความจากรูปภาพ** ด้วย Python, แสดงวิธี **ดึงข้อความจากใบเสร็จ** และแชร์เคล็ดลับหลายอย่างเพื่อ **ปรับปรุงความแม่นยำของ OCR** แนวคิดหลักคือ: ตั้งค่า OCR engine, เปิดการพรีโพรเซสอัจฉริยะ, ป้อนภาพที่สะอาด, แล้วให้ไลบรารีทำงานหนักให้

ขั้นตอนต่อไป? ลองทำลูปประมวลผลหลายใบเสร็จ, เก็บผลลัพธ์แต่ละรายการใน CSV, หรือเชื่อมต่อผลลัพธ์กับระบบบัญชีคุณ คุณอาจทดลองใช้ไลบรารี OCR ที่ใช้ deep‑learning อย่าง `easyocr` เพื่อความแม่นยำสูงขึ้นกับฟอนต์ที่ซับซ้อน

มีคำถามเกี่ยวกับรูปแบบใบเสร็จเฉพาะหรืออยากรู้วิธีจัดการกับ PDF หลายหน้า? แสดงความคิดเห็นด้านล่าง แล้วขอให้สนุกกับการเขียนโค้ด!

## คุณควรเรียนรู้อะไรต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอนเพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโปรเจกต์ของคุณ

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}