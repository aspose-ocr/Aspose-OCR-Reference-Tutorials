---
category: general
date: 2026-01-12
description: ทำ OCR บนไฟล์ PNG อย่างรวดเร็วด้วย Python. เรียนรู้วิธีดึงข้อความจากภาพและใบแจ้งหนี้
  และโหลดภาพสำหรับ OCR ด้วย Aspose.OCR.
draft: false
keywords:
- run OCR on PNG
- extract text from image
- extract text from invoice
- load image for OCR
- Aspose OCR Python
- JSON to CSV conversion
language: th
og_description: ทำ OCR บนไฟล์ PNG ได้ทันที. คู่มือนี้แสดงวิธีการดึงข้อความจากภาพและใบแจ้งหนี้,
  โหลดภาพเพื่อทำ OCR, และบันทึกผลลัพธ์เป็น JSON และ CSV.
og_title: ทำ OCR บน PNG – บทเรียน Python เต็มรูปแบบ
tags:
- OCR
- Python
- Image Processing
title: เรียกใช้ OCR บน PNG – คู่มือ Python ฉบับเต็มสำหรับการดึงข้อความจากภาพ
url: /th/python-java/general/run-ocr-on-png-complete-python-guide-to-extract-text-from-im/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ทำ OCR บน PNG – คู่มือ Python ฉบับสมบูรณ์เพื่อดึงข้อความจากรูปภาพ

เคยต้องการ **run OCR on PNG** ไฟล์แต่ไม่แน่ใจว่าห้องสมุดใดจะให้ผลลัพธ์ที่สะอาดและเป็นโครงสร้าง? คุณไม่ได้อยู่คนเดียว ในหลายโครงการจริง—เช่นการทำอัตโนมัติใบแจ้งหนี้หรือการสแกนใบเสร็จ—ขั้นตอนแรกคือการ **extract text from image** ไฟล์ และ PNG เป็นรูปแบบที่พบบ่อยเพราะรักษาคุณภาพแบบไม่มีการสูญเสีย

ในบทแนะนำนี้ เราจะเดินผ่านตัวอย่างเชิงปฏิบัติด้วยแพคเกจ Aspose.OCR สำหรับ Python. เมื่อจบคู่มือคุณจะรู้วิธี **load image for OCR**, ดึงข้อความทุกบรรทัด, แปลงข้อมูลนั้นเป็นอ็อบเจกต์ JSON ที่เรียบร้อย, และแม้กระทั่งบันทึกเป็น CSV เพื่อการประมวลผลต่อไป ไม่มีเนื้อหาเกินความจำเป็น เพียงโซลูชันที่ใช้งานได้จริงและพร้อมรัน

## สิ่งที่คุณจะได้เรียนรู้

- วิธีการติดตั้งและนำเข้าไลบรารี Aspose.OCR.  
- ขั้นตอนที่แน่นอนเพื่อ **run OCR on PNG** และจัดการกับอ็อบเจกต์ผลลัพธ์.  
- วิธีการ **extract text from invoice** ไฟล์และจัดรูปแบบผลลัพธ์เป็น JSON หรือ CSV.  
- เคล็ดลับสำหรับการจัดการกับภาพที่คอนทราสต์ต่ำ, เอกสารหลายภาษา, และคะแนนความเชื่อมั่น.  
- ตัวอย่างโค้ดที่ครบถ้วนพร้อมคัดลอก‑วางที่คุณสามารถรันได้ทันที

> **Prerequisite:** Python 3.8+ และความคุ้นเคยพื้นฐานกับ pip. หากคุณไม่เคยใช้ Aspose มาก่อน ไม่ต้องกังวล—คู่มือนี้ครอบคลุมทุกอย่างที่คุณต้องการเพื่อเริ่มต้น

---

## ขั้นตอนที่ 1 – ติดตั้ง Aspose.OCR และเตรียมสภาพแวดล้อมของคุณ

ก่อนที่เราจะ **run OCR on PNG** ไลบรารีต้องถูกติดตั้งบนระบบของคุณก่อน

```bash
pip install aspose-ocr
```

> **Pro tip:** ใช้ virtual environment (`python -m venv venv`) เพื่อแยกการพึ่งพาออกจากกัน จะช่วยป้องกันการชนกันของเวอร์ชันเมื่อคุณทำหลายโครงการพร้อมกัน

เมื่อติดตั้งเสร็จแล้ว ให้นำเข้าโมดูลที่เราต้องการใช้:

```python
# Step 1: Import the OCR and JSON modules
import asposeocr as ocr
import json
```

ที่นี่เรานำเข้า `asposeocr` เพื่อทำงานหนักและไลบรารี `json` ในตัวสำหรับการแปลงข้อมูลในภายหลัง

## ขั้นตอนที่ 2 – สร้าง OCR Engine และตั้งค่าภาษา

OCR engine คือส่วนประกอบหลักที่อ่านพิกเซลจริง ๆ สำหรับใบแจ้งหนี้ภาษาอังกฤษส่วนใหญ่ คุณจะต้องการแพ็คภาษาอังกฤษ:

```python
# Step 2: Create an OCR engine and set the language to English
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

> **Why this matters:** การระบุภาษา จะจำกัดชุดอักขระ ซึ่งช่วยเพิ่มความแม่นยำและเร่งการประมวลผล หากคุณต้องการจัดการใบแจ้งหนี้หลายภาษา เพียงเปลี่ยน `ocr.Language.ENGLISH` เป็น enum ที่เหมาะสม

## ขั้นตอนที่ 3 – โหลดภาพสำหรับ OCR

ตอนนี้เราจะ **load image for OCR** เมธอด `Image.load` รับพาธไฟล์และรองรับ PNG, JPEG, BMP, และอื่น ๆ

```python
# Step 3: Load the image you want to analyze
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)
```

> **Edge case:** หากไฟล์ PNG มีขนาดใหญ่ผิดปกติ (เกิน 5 MB) ควรปรับขนาดก่อนเพื่อให้การใช้หน่วยความจำอยู่ในระดับที่เหมาะสม Pillow สามารถทำได้ในบรรทัดเดียว:

```python
# Optional: Resize large PNGs
from PIL import Image as PilImage
pil_img = PilImage.open(image_path)
pil_img.thumbnail((2000, 2000), PilImage.ANTIALIAS)
pil_img.save("temp_resized.png")
image = ocr.Image.load("temp_resized.png")
```

## ขั้นตอนที่ 4 – Run OCR on PNG และจับผลลัพธ์

เมื่อ engine พร้อมและภาพถูกโหลดแล้ว ถึงเวลาที่จะ **run OCR on PNG** และดึงผลลัพธ์ที่เป็นโครงสร้าง

```python
# Step 4: Run the OCR process on the loaded image
ocr_result = ocr_engine.process(image)
```

อ็อบเจกต์ `ocr_result` มีคอลเลกชันของรายการ `OcrRegion` แต่ละรายการมีข้อความที่ถูกจดจำและคะแนนความเชื่อมั่น (0‑100) นี่คือที่ที่คุณจะได้ข้อมูลละเอียดที่จำเป็นสำหรับการ **extract text from invoice**

## ขั้นตอนที่ 5 – แปลงผลลัพธ์เป็น JSON และพิมพ์อย่างสวยงาม

ระบบส่วนใหญ่ที่ต่อจากนี้ชอบ JSON ดังนั้นเราจะเปลี่ยนผลลัพธ์ OCR ให้เป็นสตริงที่จัดรูปแบบอย่างสวยงาม

```python
# Step 5: Convert the OCR result to a formatted JSON string and display it
json_str = ocr_result.to_json()
ocr_data = json.loads(json_str)

# Pretty‑print with indentation
print(json.dumps(ocr_data, indent=2))
```

### ตัวอย่างผลลัพธ์

```json
{
  "pages": [
    {
      "regions": [
        {
          "text": "Invoice #12345",
          "confidence": 98.7,
          "bounds": { "x": 50, "y": 20, "width": 200, "height": 30 }
        },
        {
          "text": "Date: 2025‑12‑01",
          "confidence": 96.4,
          "bounds": { "x": 50, "y": 60, "width": 180, "height": 25 }
        },
        {
          "text": "Total Amount: $1,250.00",
          "confidence": 99.1,
          "bounds": { "x": 50, "y": 300, "width": 250, "height": 30 }
        }
      ]
    }
  ]
}
```

สังเกตว่าทุกบรรทัดมีเมตริกความเชื่อมั่น—เหมาะสำหรับกรองรายการที่ความเชื่อมั่นต่ำ หากคุณวางแผนจะ **extract text from invoice** โดยอัตโนมัติ

## ขั้นตอนที่ 6 – บันทึกข้อมูล OCR เป็น CSV (หนึ่งบรรทัดต่อข้อความ + ความเชื่อมั่น)

CSV เหมาะสำหรับสเปรดชีตหรือการนำเข้าข้อมูลอย่างรวดเร็ว Aspose มีคำสั่งหนึ่งบรรทัดเพื่อบันทึกทุกอย่างลงไฟล์ CSV

```python
# Step 6: Save the OCR result as a CSV file (each line → text + confidence)
csv_path = "YOUR_DIRECTORY/invoice_output.csv"
ocr_result.save_as_csv(csv_path)
```

CSV ที่สร้างขึ้นจะมีลักษณะดังนี้:

```
"Invoice #12345",98.7
"Date: 2025-12-01",96.4
"Total Amount: $1,250.00",99.1
```

คุณสามารถเปิดไฟล์นี้ใน Excel, Google Sheets, หรือป้อนเข้าสู่ฐานข้อมูลได้แล้ว

## โบนัส – การจัดการข้อความความเชื่อมั่นต่ำและ PDF หลายหน้า

### การกรองตามความเชื่อมั่น

หากคุณต้องการเฉพาะบรรทัดที่ความเชื่อมั่นสูง ให้กรอง JSON ก่อนบันทึกออก:

```python
high_confidence = [
    region for page in ocr_data["pages"]
    for region in page["regions"]
    if region["confidence"] >= 95
]
print(json.dumps(high_confidence, indent=2))
```

### เอกสารหลายหน้า

Aspose.OCR จะสร้างรายการ `page` ใหม่อัตโนมัติสำหรับแต่ละหน้าใน PNG หรือ PDF ที่มีหลายหน้า ให้วนลูปผ่าน `ocr_data["pages"]` เพื่อประมวลผลทั้งหมด—ไม่ต้องเขียนโค้ดเพิ่มเติม

## ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็น **complete script** ที่คุณสามารถคัดลอก, วาง, และรันได้ทันที แทนที่ `YOUR_DIRECTORY` ด้วยโฟลเดอร์ที่เก็บไฟล์ PNG ของคุณ

```python
import asposeocr as ocr
import json

# 1️⃣ Initialize OCR engine
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH

# 2️⃣ Load the PNG image
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)

# 3️⃣ Perform OCR
result = engine.process(image)

# 4️⃣ Convert to JSON and pretty‑print
json_str = result.to_json()
data = json.loads(json_str)
print("=== OCR JSON Output ===")
print(json.dumps(data, indent=2))

# 5️⃣ Save as CSV (text + confidence)
csv_path = "YOUR_DIRECTORY/invoice_output.csv"
result.save_as_csv(csv_path)
print(f"\n✅ CSV saved to {csv_path}")

# 6️⃣ (Optional) Filter high‑confidence lines
high_conf = [
    r for page in data["pages"]
    for r in page["regions"]
    if r["confidence"] >= 95
]
print("\n=== High‑Confidence Regions ===")
print(json.dumps(high_conf, indent=2))
```

รันสคริปต์ด้วย `python run_ocr.py` แล้วคุณจะเห็นการ dump JSON ในคอนโซล, ไฟล์ CSV บนดิสก์, และรายการที่กรองแล้วของรายการความเชื่อมั่นสูง

## คำถามที่พบบ่อย

**Q: ฉันสามารถใช้วิธีนี้เพื่อดึงข้อความจากใบเสร็จสแกนแทนใบแจ้งหนี้ได้หรือไม่?**  
A: แน่นอน กระบวนการเดียวกันใช้ได้—เพียงชี้ `image_path` ไปที่ PNG ของใบเสร็จของคุณ หากใบเสร็จใช้ภาษาต่างกัน ให้เปลี่ยน `engine.language` ตามนั้น

**Q: ถ้า PNG ของฉันมีข้อความที่หมุน?**  
A: Aspose.OCR จะตรวจจับการหมุนโดยอัตโนมัติ แต่ในกรณีที่ยาก คุณสามารถหมุนภาพด้วย Pillow ด้วยตนเองก่อนส่งให้ engine

**Q: ฉันต้องมีไลเซนส์แบบชำระเงินสำหรับ Aspose.OCR หรือไม่?**  
A: ไลบรารีมีโหมดประเมินผลฟรีพร้อมลายน้ำบนผลลัพธ์ สำหรับการใช้งานในผลิตภัณฑ์คุณจะต้องมีไลเซนส์ ซึ่งสามารถรับได้จากเว็บไซต์ของ Aspose

## สรุป

เราได้ครอบคลุมทุกอย่างที่คุณต้องการเพื่อ **run OCR on PNG** ด้วย Python: การติดตั้ง SDK, การโหลดภาพ, การดึงข้อความที่เป็นโครงสร้าง, และการบันทึกผลลัพธ์เป็น JSON หรือ CSV ไม่ว่าคุณจะต้องการ **extract text from image** สำหรับสคริปต์ง่าย ๆ หรือ **extract text from invoice** สำหรับสายงานบัญชีอัตโนมัติ ขั้นตอนข้างต้นให้พื้นฐานที่มั่นคงและพร้อมใช้งานในผลิตภัณฑ์

ต่อไปคุณอาจสำรวจ:

- การรวมผลลัพธ์ CSV กับฐานข้อมูลเพื่อจัดเก็บใบแจ้งหนี้จำนวนมาก.  
- การเพิ่มการประมวลผลหลังด้วย regular expressions เพื่อดึงวันที่, จำนวนเงิน, หรือรหัสภาษี.  
- การใช้ฟีเจอร์ `ocr_engine.recognize_barcode` หากใบแจ้งหนี้ของคุณมี QR code

ลองใช้ดู ปรับค่าขีดจำกัดความเชื่อมั่น และดูกระบวนการประมวลผลเอกสารของคุณกลายเป็นเรื่องง่าย หากมีคำถามเพิ่มเติมหรือกรณีการใช้งานที่น่าสนใจ อย่าลังเลที่จะแสดงความคิดเห็นด้านล่าง—ขอให้สนุกกับการ OCR!

![ตัวอย่างการทำ OCR บน PNG](run-ocr-on-png.png "run OCR on PNG – ตัวอย่างภาพผลลัพธ์ OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}