---
category: general
date: 2026-03-26
description: วิธีรัน OCR บนไฟล์ PNG และดึงข้อความจากภาพด้วยพจนานุกรมกำหนดเองเพื่อเพิ่มความแม่นยำของ
  OCR เรียนรู้การโหลดภาพสำหรับ OCR อย่างรวดเร็ว
draft: false
keywords:
- how to run OCR
- extract text from image
- recognize text from png
- improve OCR accuracy
- load image for OCR
language: th
og_description: วิธีใช้ OCR กับไฟล์ PNG และดึงข้อความจากภาพด้วยพจนานุกรมกำหนดเองเพื่อเพิ่มความแม่นยำของ
  OCR คู่มือขั้นตอนโดยละเอียด
og_title: วิธีใช้งาน OCR – แยกข้อความจากรูปภาพด้วย Python
tags:
- OCR
- Python
- Image Processing
title: วิธีเรียกใช้ OCR – ดึงข้อความจากรูปภาพด้วย Python
url: /th/python-java/general/how-to-run-ocr-extract-text-from-image-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีการรัน OCR – แยกข้อความจากรูปภาพใน Python

เคยสงสัย **วิธีการรัน OCR** บนใบแจ้งหนี้ที่สแกนหรือภาพหน้าจอและได้ข้อความที่สะอาดและค้นหาได้หรือไม่? คุณไม่ได้เป็นคนเดียว ในหลายโครงการอุปสรรคหลักคือการโหลดภาพสำหรับ OCR แล้วทำให้เอนจินเข้าใจคำเฉพาะโดเมน  

ในบทเรียนนี้เราจะเดินผ่านตัวอย่างที่พร้อมรันครบวงจรที่ **แยกข้อความจากไฟล์รูปภาพ** แสดงวิธี **จดจำข้อความจาก PNG** และแม้กระทั่งสาธิตเทคนิคเพื่อ **ปรับปรุงความแม่นยำของ OCR** ด้วยพจนานุกรมกำหนดเองและอักขระพิเศษ เมื่อจบคุณจะมีสคริปต์อิสระที่สามารถใส่ลงในโค้ด Python ใดก็ได้

## สิ่งที่คุณต้องมี

- Python 3.8+ (โค้ดใช้ type hints แต่ทำงานได้กับเวอร์ชัน 3.x ก่อนหน้า)
- ไลบรารี `ocr` ที่มาพร้อมกับเอนจิน OCR ที่คุณต้องการ (ติดตั้งด้วย `pip install ocr‑engine` – แทนด้วยชื่อแพคเกจจริง)
- ไฟล์รูปภาพ (`input.png`) ที่คุณต้องการประมวลผล
- ตัวเลือก: ไฟล์ข้อความธรรมดา (`invoice_terms.txt`) ที่มีคำเฉพาะโดเมน หนึ่งบรรทัดต่อหนึ่งคำ

ไม่มีการพึ่งพาไลบรารีภายนอกหนัก ๆ ไม่มีคีย์ API ของคลาวด์ เพียงเอนจิน OCR ที่ทำงานบนเครื่องเท่านั้น

---

## ขั้นตอนที่ 1: ติดตั้งและนำเข้าไลบรารี OCR

ก่อนอื่น ตรวจสอบให้แน่ใจว่าได้ติดตั้งแพคเกจ OCR แล้ว หากคุณใช้แพคเกจสมมติ `ocr-engine` ให้รัน:

```bash
pip install ocr-engine
```

จากนั้นนำเข้าคลาสที่จำเป็น:

```python
# Step 1: Import the OCR SDK
import ocr
from ocr import Imaging
```

> **เคล็ดลับ:** หากคุณใช้ virtual environment ให้เปิดใช้งานก่อนติดตั้งเพื่อให้ Python ทั่วโลกของคุณสะอาด

## ขั้นตอนที่ 2: สร้างอินสแตนซ์ของ OCR Engine

การสร้างอ็อบเจ็กต์เอนจินเป็นจุดเริ่มต้นของทุกงาน OCR คิดว่าเป็นการเปิดฮาร์ดแวร์สแกนเนอร์ในซอฟต์แวร์

```python
# Step 2: Initialise the OCR engine
ocr_engine = ocr.OcrEngine()
```

ทำไมจึงสำคัญ: เอนจินเก็บการตั้งค่าเช่น language packs, recognition modes, และทรัพยากรกำหนดเองที่คุณจะแนบต่อไป หากไม่มีเอนจิน คุณไม่สามารถ **load image for OCR** หรือรัน pipeline การจดจำได้

## ขั้นตอนที่ 3: โหลดภาพที่ต้องการจดจำ

ที่นี่เราจะ **load image for OCR** จริง ๆ เมธอด `Imaging.Image.load()` จะอ่านไฟล์และแปลงเป็นรูปแบบบิตแมพภายในที่เอนจินคาดหวัง

```python
# Step 3: Load the PNG image you want to process
image_path = "YOUR_DIRECTORY/input.png"
ocr_engine.set_image(Imaging.Image.load(image_path))
```

หากคุณมี JPEG หรือ TIFF เมธอดเดียวกันก็ทำงาน—เพียงเปลี่ยนนามสกุลไฟล์ เอนจินจะตรวจจับรูปแบบโดยอัตโนมัติ

> **กรณีขอบ:** ภาพขนาดใหญ่มาก (เกิน 5 MP) อาจทำให้ใช้หน่วยความจำสูง พิจารณาลดขนาดด้วย Pillow ก่อนโหลดหากเจอปัญหาประสิทธิภาพ

## ขั้นตอนที่ 4: ใส่พจนานุกรมกำหนดเองเพื่อเพิ่มความแม่นยำ

ส่วนใหญ่เอนจิน OCR จะมาพร้อมโมเดลภาษาแบบทั่วไป สำหรับใบแจ้งหนี้, ใบเสร็จ, หรือเอกสารกฎหมายมักพบคำที่พลาด การให้รายการคำกำหนดเองบอกเอนจินว่า “คำเหล่านี้เป็นคำที่ถูกต้อง”

```python
# Step 4: Attach a custom dictionary (one word per line)
custom_dict_path = "YOUR_DIRECTORY/invoice_terms.txt"
ocr_engine.set_custom_dictionary(custom_dict_path)
```

ตัวอย่างรายการอาจเป็น:

```
VAT
InvoiceNumber
Øre
ß
Ħ
```

การเพิ่มรายการเหล่านี้ทำให้เมตริก **improve OCR accuracy** ดีขึ้นอย่างมาก—โดยเฉพาะสำหรับสัญลักษณ์ที่ไม่ใช่ ASCII

## ขั้นตอนที่ 5: เพิ่มอักขระพิเศษที่ไม่ได้อยู่ในชุดเริ่มต้น

หากโดเมนของคุณใช้สัญลักษณ์เช่นสัญลักษณ์ยูโร (€) หรือ Ø ของสแกนดิเนเวีย คุณสามารถเพิ่มได้โดยตรง:

```python
# Step 5: Register additional characters
ocr_engine.add_custom_characters("ØßĦ")
```

เอนจินจะถือ glyph เหล่านี้ว่าเป็นอักขระที่ถูกต้องในขั้นตอนการจดจำ ลดโอกาสที่ผลลัพธ์จะเป็น “ขยะ”

## ขั้นตอนที่ 6: รันกระบวนการ OCR และดึงข้อความออกมา

สุดท้าย เรียกตัว recognizer แล้วดึงผลลัพธ์เป็นข้อความธรรมดา เมธอด `recognize()` จะคืนอ็อบเจ็กต์ที่มีข้อมูลหลายอย่าง เราต้องการแค่สตริงดิบสำหรับกรณีใช้งานส่วนใหญ่

```python
# Step 6: Execute OCR and print the result
result = ocr_engine.recognize()
print("=== Recognized Text ===")
print(result.get_text())
```

**ผลลัพธ์ที่คาดหวัง** (ตัดสั้นเพื่อความกระชับ):

```
=== Recognized Text ===
Invoice #12345
Date: 2026-03-01
Total: €1,250.00
VAT: 25%
...
```

หากผลลัพธ์ดูเป็นอักขระผสม ให้ตรวจสอบว่าพจนานุกรมกำหนดเองและอักขระพิเศษโหลดอย่างถูกต้องหรือไม่

---

## ภาพรวมเชิงภาพ

![how to run OCR diagram](ocr-workflow.png){alt="แผนภาพวิธีการรัน OCR"}

แผนภาพด้านบนแสดงกระบวนการตั้งแต่การโหลดภาพจนถึงการได้ข้อความที่สะอาด โดยเน้นจุดที่คุณสามารถแทรกพจนานุกรมกำหนดเองและชุดอักขระ

---

## คำถามที่พบบ่อย & ข้อควรระวัง

### ทำงานกับ PDF หลายหน้าได้หรือไม่?

ได้—เพียงแปลงแต่ละหน้าเป็น PNG (ใช้ `pdf2image` หรือวิธีอื่น) แล้วส่งต่อไปยังอินสแตนซ์ `ocr_engine` เดียวกัน เอนจินจะประมวลผลแต่ละภาพแยกกัน ทำให้คุณได้รายการสตริงที่สามารถต่อเข้าด้วยกันได้

### ถ้าภาพถูกหมุน?

เอนจิน OCR สมัยใหม่ส่วนใหญ่ตรวจจับทิศทางอัตโนมัติ แต่คุณสามารถบังคับหมุนด้วย:

```python
ocr_engine.set_image(Imaging.Image.load(image_path).rotate(90))
```

### จะจัดการกับภาษาที่ไม่ใช่อังกฤษอย่างไร?

สลับโมเดลภาษา ก่อนโหลดภาพ:

```python
ocr_engine.set_language("de")  # German
```

ตรวจสอบให้แน่ใจว่าได้ติดตั้ง language pack ที่สอดคล้องกันแล้ว

---

## สคริปต์เต็ม – คัดลอกและวางได้ทันที

ด้านล่างเป็นโปรแกรมทั้งหมด พร้อมรันหลังจากแทนที่พาธตัวแปร

```python
#!/usr/bin/env python3
"""
How to Run OCR – Complete example that extracts text from a PNG,
uses a custom dictionary, and adds special characters for better accuracy.
"""

# Install the OCR package first:
# pip install ocr-engine

import ocr
from ocr import Imaging

def main():
    # 1️⃣ Initialise the OCR engine
    ocr_engine = ocr.OcrEngine()

    # 2️⃣ Load the image you want to recognize
    image_path = "YOUR_DIRECTORY/input.png"      # <-- change this
    ocr_engine.set_image(Imaging.Image.load(image_path))

    # 3️⃣ Provide a custom dictionary (optional but recommended)
    dict_path = "YOUR_DIRECTORY/invoice_terms.txt"   # one word per line
    ocr_engine.set_custom_dictionary(dict_path)

    # 4️⃣ Add any special characters not covered by the default set
    ocr_engine.add_custom_characters("ØßĦ")   # e.g., currency symbols

    # 5️⃣ Run the OCR process
    result = ocr_engine.recognize()

    # 6️⃣ Output the recognized text
    print("=== Recognized Text ===")
    print(result.get_text())

if __name__ == "__main__":
    main()
```

รันด้วยคำสั่ง:

```bash
python run_ocr.py
```

คุณควรเห็นข้อความที่แยกออกมาปรากฏบนคอนโซล จากนั้นสามารถบันทึกลงไฟล์ ส่งไปยังฐานข้อมูล หรือส่งต่อไปยัง pipeline NLP ต่อได้

---

## สรุป & ขั้นตอนต่อไป

เราได้ครอบคลุม **วิธีการรัน OCR** บน PNG, วิธี **แยกข้อความจากรูปภาพ**, และแสดงวิธีการ **จดจำข้อความจาก PNG** พร้อม **ปรับปรุงความแม่นยำของ OCR** ด้วยพจนานุกรมและอักขระกำหนดเอง  

ต่อไปให้พิจารณา:

- **การประมวลผลเป็นชุด:** วนลูปผ่านโฟลเดอร์ของภาพ
- **การหลังประมวลผล:** ใช้ regex ดึงหมายเลขใบแจ้งหนี้หรือวันที่
- **การบูรณาการ:** เชื่อมสคริปต์เข้ากับ Flask API เพื่อให้บริการ OCR ตามต้องการ

หากสนใจหัวข้อขั้นสูงเพิ่มเติม ตรวจสอบบทเรียนเกี่ยวกับ **load image for OCR** ด้วยการเตรียมภาพด้วย OpenCV หรือสำรวจโมเดล OCR แบบ deep‑learning อย่าง Tesseract 4+ ที่ใช้ LSTM

---

### อย่าหยุดทดลอง!

ลองเปลี่ยน `invoice_terms.txt` เป็นรายการคำศัพท์ทางการแพทย์ เพิ่มอักขระกรีก หรือใส่ภาพความละเอียดต่ำเพื่อดูว่าความแม่นยำจะยืดหยุ่นได้แค่ไหน การทดลองมากเท่าไหร่ คุณจะเข้าใจการแลกเปลี่ยนระหว่างการเตรียมภาพ, พจนานุกรมกำหนดเอง, และการตั้งค่าเอนจินได้ดียิ่งขึ้น

ขอให้เขียนโค้ดสนุกและ OCR ของคุณแม่นยำเสมอ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}