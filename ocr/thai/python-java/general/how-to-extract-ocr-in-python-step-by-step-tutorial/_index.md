---
category: general
date: 2026-04-26
description: วิธีดึง OCR จากรูปภาพด้วย Python – ตัวอย่าง OCR ด้วย Python ที่แสดงวิธีโหลดรูปภาพสำหรับ
  OCR และดึงข้อความจากใบเสร็จ
draft: false
keywords:
- how to extract ocr
- python ocr example
- extract text from receipt
- load image for ocr
- how to use OCR
language: th
og_description: วิธีดึง OCR จากภาพด้วย Python. เรียนรู้ตัวอย่าง OCR ด้วย Python, โหลดภาพสำหรับ
  OCR, และดึงข้อความจากใบเสร็จในไม่กี่นาที.
og_title: วิธีดึง OCR ใน Python – คู่มือเต็ม
tags:
- OCR
- Python
- Image Processing
title: วิธีดึง OCR ใน Python – คู่มือทีละขั้นตอน
url: /th/python-java/general/how-to-extract-ocr-in-python-step-by-step-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีดึงข้อมูล OCR ด้วย Python – คู่มือฉบับเต็ม

เคยสงสัย **how to extract ocr** จากใบเสร็จที่เบลอหรือใบแจ้งหนี้ที่สแกนหรือไม่? คุณไม่ได้เป็นคนเดียว—นักพัฒนามักเจออุปสรรคเมื่อจำเป็นต้องได้ข้อความที่สะอาดและอ่านได้โดยเครื่องจากรูปภาพ ข่าวดีคือ? ด้วยเพียงไม่กี่บรรทัดของ Python คุณสามารถแปลงรูปภาพใบเสร็จให้เป็นข้อความที่มีความมั่นใจสูงและสามารถค้นหาได้.

ในบทเรียนนี้เราจะเดินผ่าน **python ocr example** ที่แสดง **how to load image for ocr**, รันเอนจิน, และเก็บเฉพาะอักขระที่ผ่านเกณฑ์ความมั่นใจ 85 % สุดท้ายคุณจะสามารถ **extract text from receipt** จากรูปภาพได้โดยไม่ต้องค้นหาเอกสารหรือเดาพารามิเตอร์ของ API.

## สิ่งที่คุณต้องการ

- Python 3.9 หรือใหม่กว่า (ไวยากรณ์ที่เราใช้ทำงานบน 3.8+)
- แพคเกจ `aocr` (หรือไลบรารี OCR ใด ๆ ที่มีคลาส `OcrEngine`). ติดตั้งด้วย:

```bash
pip install aocr
```

- ตัวอย่างรูปใบเสร็จ (`receipt.png`) ที่วางไว้ในโฟลเดอร์ที่คุณอ้างอิงได้
- โปรแกรมแก้ไขข้อความหรือ IDE—VS Code, PyCharm, หรือแม้แต่โน๊ตบุ๊คง่าย ๆ ก็ใช้ได้

แค่นั้นเอง ไม่ต้องใช้เฟรมเวิร์กหนัก ๆ ไม่ต้องพึ่งบริการภายนอก เพียงแค่ Python ธรรมดา

![ผลลัพธ์ OCR ความมั่นใจสูง – วิธีดึงข้อมูล OCR จากใบเสร็จ](/images/ocr-high-confidence.png)

*ข้อความแทนภาพ: วิธีดึงข้อมูล OCR จากใบเสร็จด้วย Python OCR*

## ขั้นตอนที่ 1 – สร้างอินสแตนซ์ของ OCR Engine (how to extract ocr)

สิ่งแรกที่เราทำคือเปิดใช้งาน OCR engine คิดว่าเป็นสมองที่จะอ่านพิกเซลให้เรา

```python
# Step 1: Initialize the OCR engine
from aocr import OcrEngine

ocr_engine = OcrEngine()
```

**ทำไม?** การสร้างอินสแตนซ์ `OcrEngine` จะให้คุณได้อ็อบเจ็กต์การตั้งค่าใหม่ คุณสามารถปรับโมเดลภาษา, การตั้งค่า DPI, หรือขั้นตอนการเตรียมข้อมูลต่อมา—ทั้งหมดโดยไม่ต้องแก้ไขลูปการประมวลผลหลัก

## ขั้นตอนที่ 2 – โหลดภาพสำหรับ OCR

ต่อไปเราชี้เอนจินไปที่ภาพที่ต้องการวิเคราะห์ นี่คือจุดที่คีย์เวิร์ด **load image for ocr** เข้ามามีบทบาท

```python
# Step 2: Load the receipt image
image_path = "YOUR_DIRECTORY/receipt.png"
ocr_engine.image = OcrEngine.Image.load(image_path)
```

> **เคล็ดลับ:** หากภาพของคุณอยู่ในไดเรกทอรีอื่น ให้ใช้ `os.path.join` เพื่อสร้างพาธที่เป็นอิสระต่อแพลตฟอร์ม

**ทำไมต้องโหลดภาพแบบนี้?** ตัวช่วย `Image.load` จะอ่านไฟล์เป็นรูปแบบที่เอนจินเข้าใจโดยอัตโนมัติ รองรับฟอร์แมตทั่วไป (PNG, JPEG, TIFF) หากข้ามขั้นตอนนี้หรือส่งไบต์ดิบจะทำให้เกิด `ValueError`

## ขั้นตอนที่ 3 – รันกระบวนการ OCR

ตอนนี้เราจะรัน OCR จริง ๆ เมธอด `process` จะคืนอ็อบเจ็กต์ผลลัพธ์ที่มีสัญลักษณ์ที่รู้จำ, คะแนนความมั่นใจ, และกล่องขอบเขต

```python
# Step 3: Execute OCR and capture the result
ocr_result = ocr_engine.process()
```

**`ocr_result` มีอะไรบ้าง?** ในไลบรารีส่วนใหญ่จะรวม:

- `text`: สตริงที่ต่อกันแบบดิบ
- `symbol_confidences`: รายการของทูเพิล `(char, confidence)`
- `boxes`: พิกัดของแต่ละอักขระ (มีประโยชน์สำหรับการดีบักแบบภาพ)

การเข้าถึงความมั่นใจต่ออักขระเป็นสิ่งสำคัญสำหรับขั้นตอนต่อไป

## ขั้นตอนที่ 4 – เก็บเฉพาะสัญลักษณ์ที่มีความมั่นใจสูง (≥ 85 %)

ใบเสร็จมักมีคราบ, พิมพ์สีอ่อน, หรือสัญญาณรบกวนพื้นหลัง การกรองสัญลักษณ์ที่ความมั่นใจต่ำช่วยปรับปรุงการแยกข้อมูลต่อไปอย่างมาก

```python
# Step 4: Filter out low‑confidence characters
high_confidence_text = ''.join(
    char for char, confidence in ocr_result.symbol_confidences
    if confidence >= 0.85
)
```

**ทำไมต้อง 85 %?** จากประสบการณ์ ค่าเกณฑ์ประมาณ 0.85 ให้สมดุลระหว่างรีคอลและพรีซิชันสำหรับใบเสร็จพิมพ์ส่วนใหญ่ หากพบว่าตัวเลขหายไปให้ลดค่าเกณฑ์; หากได้ข้อความไร้สาระให้เพิ่มค่า

## ขั้นตอนที่ 5 – แสดงผลข้อความที่ดึงด้วยความมั่นใจสูง

สุดท้ายเราจะพิมพ์ (หรือบันทึก) สตริงที่ทำความสะอาดแล้ว นี่คือหัวใจของเวิร์กโฟลว์ **extract text from receipt** ของเรา

```python
# Step 5: Show the cleaned result
print("High‑confidence text:", high_confidence_text)
```

ผลลัพธ์ทั่วไปจะเป็นแบบนี้:

```
High‑confidence text: Store XYZ
Date: 2024‑04‑22
Total: $23.45
```

คุณสามารถนำสตริงนี้ไปใส่ใน CSV writer, ฐานข้อมูล, หรือพายไลน์การวิเคราะห์ต่อไปได้เลย

## สคริปต์เต็มพร้อมรัน

ด้านล่างเป็นโค้ดเต็มที่คุณสามารถคัดลอก‑วางลงใน `ocr_receipt.py` แล้วรันได้ทันที

```python
# ocr_receipt.py
# A complete python ocr example that extracts high‑confidence text from a receipt.

from aocr import OcrEngine

def main():
    # 1️⃣ Create the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load the image you want to analyze
    image_path = "YOUR_DIRECTORY/receipt.png"
    ocr_engine.image = OcrEngine.Image.load(image_path)

    # 3️⃣ Run the OCR process
    ocr_result = ocr_engine.process()

    # 4️⃣ Keep only symbols with confidence ≥ 85%
    high_confidence_text = ''.join(
        char for char, confidence in ocr_result.symbol_confidences
        if confidence >= 0.85
    )

    # 5️⃣ Output the result
    print("High‑confidence text:", high_confidence_text)

if __name__ == "__main__":
    main()
```

บันทึกไฟล์, ตรวจสอบให้แน่ใจว่า `receipt.png` มีอยู่, แล้วเรียกใช้:

```bash
python ocr_receipt.py
```

คุณควรเห็นข้อความใบเสร็จที่ทำความสะอาดแล้วแสดงบนคอนโซล

## กรณีขอบและสถานการณ์ที่อาจเกิดขึ้น

| สถานการณ์ | วิธีแก้แนะนำ |
|-----------|----------------|
| **ความมั่นใจต่ำมากทั่วทั้งภาพ** | ทำการพรี‑โปรเซสภาพ: เพิ่มคอนทราสต์, แปลงเป็นระดับสีเทา, หรือใช้ฟิลเตอร์ลดสัญญาณรบกวน (`cv2.GaussianBlur`) |
| **อักขระไม่ใช่ละติน** | ส่งโมเดลภาษาให้ `OcrEngine` (เช่น `ocr_engine.language = "spa"` สำหรับสเปน) |
| **หลายใบเสร็จในภาพเดียว** | รัน OCR ทั้งภาพแล้วแยกผลลัพธ์ด้วย regex ที่ตรวจจับ `\n\n+` (บรรทัดว่างสองบรรทัด) |
| **ต้องการข้อความ OCR ดิบด้วย** | เก็บ `ocr_result.text` ควบคู่กับเวอร์ชันที่กรองแล้วเพื่อการดีบัก |

การปรับเปลี่ยนเหล่านี้ทำให้ความรู้ **how to use OCR** ของคุณขยายออกไปไกลกว่ากรณีง่ายที่สุด

## ข้อผิดพลาดทั่วไป (และวิธีหลีกเลี่ยง)

- **ลืมติดตั้งไลบรารี** – ต้องให้ `pip install aocr` สำเร็จก่อนนำเข้า
- **ใช้ตัวคั่นพาธผิด** บน Windows (`\` vs `/`). ใช้ `os.path.join`
- **กำหนดค่าเกณฑ์ความมั่นใจแบบฮาร์ดโค้ด** โดยไม่ทดสอบ – ควรตรวจสอบภาพอย่างเร็วบนใบเสร็จหลายใบก่อน
- **ละเลยการทำ Normalisation ของ Unicode** – ใบเสร็จบางใบมีอักขระขีดพิเศษ; ใช้ `unicodedata.normalize('NFKC', text)` หากต้องการเก็บผลลัพธ์

## ขั้นตอนต่อไป – ไปไกลกว่าพื้นฐาน

ตอนนี้คุณรู้แล้วว่า **how to extract ocr** จากใบเสร็จเดียว คุณอาจอยากทำต่อ:

1. **ประมวลผลหลายไฟล์ในโฟลเดอร์** – วนลูปไฟล์ PNG/JPG ทั้งหมดและเขียนผลลัพธ์แต่ละไฟล์ลง CSV
2. **เชื่อมต่อกับฐานข้อมูล** – เก็บ `high_confidence_text` ใน SQLite เพื่อการค้นหาเร็ว
3. **ใช้การแยกข้อความตามภาษาธรรมชาติ** – ใช้ regex หรือ `dateutil` ดึงวันที่, ยอดรวม, และจำนวนภาษี
4. **ทดลองไลบรารีอื่น** – `pytesseract`, `easyocr`, หรือบริการคลาวด์ (Google Vision, Azure OCR) หากต้องการรองรับหลายภาษา หรือความแม่นยำสูงกว่า

หัวข้อเหล่านี้สอดคล้องกับคีย์เวิร์ดรองของเรา: *python ocr example*, *extract text from receipt*, *load image for ocr*, และ *how to use OCR*.

## สรุป

เราได้เดินผ่าน **python ocr example** ครบชุดที่แสดง **how to extract ocr** จากภาพใบเสร็จ, กรองสัญลักษณ์ที่ความมั่นใจต่ำ, และส่งออกผลลัพธ์ที่สะอาด ขั้นตอนง่าย ๆ โค้ดครบถ้วน และวิธีการยืดหยุ่นพอที่จะปรับใช้ในโครงการขนาดใหญ่

ลองใช้กับใบเสร็จของคุณเอง ปรับค่าเกณฑ์ความมั่นใจ แล้วขยายเป็นการประมวลผลแบบแบตช์ หากเจอปัญหาเช่นโลโก้จางหรือฟอนต์แปลก ๆ ให้จำวิธีแก้กรณีขอบด้านบน Happy coding, and may your OCR pipelines be ever accurate!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}