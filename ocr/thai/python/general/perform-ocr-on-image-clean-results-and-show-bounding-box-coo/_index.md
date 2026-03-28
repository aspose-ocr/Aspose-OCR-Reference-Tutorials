---
category: general
date: 2026-03-28
description: ทำ OCR บนภาพและรับข้อความที่สะอาดพร้อมพิกัดของกล่องขอบเขต เรียนรู้วิธีดึง
  OCR ทำความสะอาด OCR และแสดงผลลัพธ์ขั้นตอนต่อขั้นตอน.
draft: false
keywords:
- perform OCR on image
- how to extract OCR
- how to clean OCR
- display bounding box coordinates
- OCR post‑processing
- OCR bounding boxes
language: th
og_description: ทำ OCR บนภาพ ทำความสะอาดผลลัพธ์ และแสดงพิกัดกล่องขอบเขตในบทแนะนำสั้น
  ๆ
og_title: ทำ OCR บนภาพ – ผลลัพธ์ที่สะอาดและกล่องขอบเขต
tags:
- OCR
- Computer Vision
- Python
title: ทำ OCR บนภาพ – ทำความสะอาดผลลัพธ์และแสดงพิกัดกล่องขอบ
url: /th/python/general/perform-ocr-on-image-clean-results-and-show-bounding-box-coo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ทำ OCR บนรูปภาพ – ทำความสะอาดผลลัพธ์และแสดงพิกัด Bounding Box

เคยต้อง **perform OCR on image** แต่ผลลัพธ์เป็นข้อความที่ยุ่งยากและไม่แน่ใจว่าคำแต่ละคำอยู่ที่ไหนบนรูปหรือไม่? คุณไม่ได้เป็นคนเดียว ในหลายโครงการ—การแปลงใบแจ้งหนี้เป็นดิจิทัล, การสแกนใบเสร็จ, หรือการดึงข้อความอย่างง่าย—การได้ผลลัพธ์ OCR ดิบเป็นเพียงอุปสรรคแรก ข่าวดีคือ คุณสามารถทำความสะอาดผลลัพธ์นั้นและดูพิกัด Bounding Box ของแต่ละพื้นที่ได้ทันทีโดยไม่ต้องเขียนโค้ดซ้ำซ้อนมาก

ในคู่มือนี้เราจะอธิบายขั้นตอน **how to extract OCR**, รัน **how to clean OCR** post‑processor, และสุดท้าย **display bounding box coordinates** สำหรับแต่ละพื้นที่ที่ทำความสะอาดแล้ว. เมื่อเสร็จคุณจะได้สคริปต์เดียวที่สามารถรันได้ซึ่งแปลงรูปภาพเบลอให้เป็นข้อความที่เป็นระเบียบและมีโครงสร้างพร้อมสำหรับการประมวลผลต่อไป

## สิ่งที่คุณต้องการ

- Python 3.9+ (ไวยากรณ์ด้านล่างทำงานบน 3.8 และใหม่กว่า)
- OCR engine ที่รองรับ `recognize(..., return_structured=True)` – ตัวอย่างเช่นไลบรารี `engine` สมมติที่ใช้ในโค้ดตัวอย่าง. แทนที่ด้วย Tesseract, EasyOCR, หรือ SDK ใด ๆ ที่คืนค่าข้อมูลพื้นที่
- ความคุ้นเคยพื้นฐานกับฟังก์ชันและลูปของ Python
- ไฟล์รูปภาพที่คุณต้องการสแกน (PNG, JPG, ฯลฯ)

> **เคล็ดลับ:** หากคุณใช้ Tesseract, ฟังก์ชัน `pytesseract.image_to_data` จะให้ Bounding Box อยู่แล้ว. คุณสามารถห่อผลลัพธ์นั้นด้วยอะแดปเตอร์เล็ก ๆ ที่จำลอง API `engine.recognize` ด้านล่าง

![ตัวอย่างการทำ OCR บนรูปภาพ](image-placeholder.png "ตัวอย่างการทำ OCR บนรูปภาพ")

*ข้อความแทน: แผนภาพแสดงวิธีทำ OCR บนรูปภาพและแสดงพิกัด Bounding Box*

## ขั้นตอนที่ 1 – ทำ OCR บนรูปภาพและรับโครงสร้างพื้นที่

สิ่งแรกคือการขอให้ OCR engine คืนค่าไม่ใช่แค่ข้อความธรรมดา แต่เป็นรายการโครงสร้างของพื้นที่ข้อความ. รายการนี้ประกอบด้วยสตริงดิบและสี่เหลี่ยมที่ล้อมรอบมัน.

```python
import engine   # replace with your actual OCR library
from pathlib import Path

# Load the image you want to process
image_path = Path("sample_invoice.jpg")
image = engine.load_image(image_path)

# Step 1: Perform OCR and request a structured list of text regions
raw_result = engine.recognize(image, return_structured=True)
```

**ทำไมเรื่องนี้ถึงสำคัญ:**  
เมื่อคุณขอแค่ข้อความธรรมดา คุณจะสูญเสียบริบทเชิงพื้นที่. ข้อมูลเชิงโครงสร้างทำให้คุณสามารถ **display bounding box coordinates** ในภายหลัง, จัดตำแหน่งข้อความกับตาราง, หรือส่งตำแหน่งที่แม่นยำให้กับโมเดลต่อไป.

## ขั้นตอนที่ 2 – วิธีทำความสะอาดผลลัพธ์ OCR ด้วย Post‑Processor

OCR engine มีความสามารถในการตรวจจับอักขระได้ดี, แต่บ่อยครั้งจะเหลือช่องว่างเกิน, สิ่งกีดขวางจากการตัดบรรทัด, หรือสัญลักษณ์ที่อ่านผิด. Post‑processor จะทำให้ข้อความเป็นมาตรฐาน, แก้ไขข้อผิดพลาด OCR ที่พบบ่อย, และตัดช่องว่างส่วนเกิน.

```python
# Step 2: Clean the plain‑text of each region using the post‑processor
processed_result = engine.run_postprocessor(raw_result)
```

หากคุณกำลังสร้างตัวทำความสะอาดของคุณเอง, ควรพิจารณา:

- ลบอักขระที่ไม่ใช่ ASCII (`re.sub(r'[^\x00-\x7F]+',' ', text)`)
- ทำให้หลายช่องว่างต่อเนื่องกลายเป็นช่องว่างเดียว
- ใช้ spell‑checker อย่าง `pyspellchecker` เพื่อตรวจสอบการพิมพ์ผิดที่ชัดเจน

**ทำไมคุณควรใส่ใจ:**  
สตริงที่เป็นระเบียบทำให้การค้นหา, การทำดัชนี, และ pipeline NLP ต่อไปทำงานได้เชื่อถือได้มากขึ้น. กล่าวคือ, **how to clean OCR** มักเป็นความแตกต่างระหว่างชุดข้อมูลที่ใช้ได้และปัญหาต่าง ๆ.

## ขั้นตอนที่ 3 – แสดงพิกัด Bounding Box สำหรับแต่ละพื้นที่ที่ทำความสะอาดแล้ว

เมื่อข้อความเป็นระเบียบแล้ว, เราจะวนลูปผ่านแต่ละพื้นที่, พิมพ์สี่เหลี่ยมและสตริงที่ทำความสะอาด. นี่คือส่วนที่เราจะ **display bounding box coordinates** ในที่สุด.

```python
# Step 3 – Iterate over the cleaned regions and display their bounding box and text
for text_region in processed_result.regions:
    # Each region has a .bounding_box attribute (x, y, width, height)
    bbox = text_region.bounding_box
    print(f"[{bbox}] {text_region.text}")
```

**ตัวอย่างผลลัพธ์**

```
[(34, 120, 210, 30)] Invoice #12345
[(34, 160, 420, 28)] Date: 2026‑03‑01
[(34, 200, 380, 28)] Total Amount: $1,254.00
```

คุณสามารถนำพิกัดเหล่านั้นไปใช้กับไลบรารีการวาด (เช่น OpenCV) เพื่อวางกล่องบนรูปภาพต้นฉบับ, หรือเก็บไว้ในฐานข้อมูลเพื่อการสืบค้นในภายหลัง.

## สคริปต์เต็มพร้อมรัน

ด้านล่างเป็นโปรแกรมเต็มที่เชื่อมโยงขั้นตอนทั้งสามเข้าด้วยกัน. แทนที่การเรียก `engine` ตัวอย่างด้วย SDK OCR ของคุณจริง.

```python
#!/usr/bin/env python3
"""
Perform OCR on image → clean results → display bounding box coordinates.
Author: Your Name
Date: 2026‑03‑28
"""

import engine               # <-- replace with your OCR library
from pathlib import Path
import sys

def main(image_path: str):
    # Load image
    image = engine.load_image(Path(image_path))

    # 1️⃣ Perform OCR and ask for structured output
    raw_result = engine.recognize(image, return_structured=True)

    # 2️⃣ Clean the raw text using the built‑in post‑processor
    processed_result = engine.run_postprocessor(raw_result)

    # 3️⃣ Show each region's bounding box and cleaned text
    print("\n=== Cleaned OCR Regions ===")
    for region in processed_result.regions:
        bbox = region.bounding_box  # (x, y, w, h)
        print(f"[{bbox}] {region.text}")

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python perform_ocr.py <image_file>")
        sys.exit(1)
    main(sys.argv[1])
```

### วิธีการรัน

```bash
python perform_ocr.py sample_invoice.jpg
```

คุณควรเห็นรายการของ Bounding Box ที่จับคู่กับข้อความที่ทำความสะอาด, เหมือนกับตัวอย่างผลลัพธ์ด้านบน.

## คำถามที่พบบ่อยและกรณีขอบ

| คำถาม | คำตอบ |
|----------|--------|
| **ถ้า OCR engine ไม่รองรับ `return_structured` จะทำอย่างไร?** | เขียน wrapper เล็ก ๆ ที่แปลงผลลัพธ์ดิบของ engine (โดยทั่วไปเป็นรายการคำพร้อมพิกัด) ให้เป็นอ็อบเจกต์ที่มีแอตทริบิวต์ `text` และ `bounding_box`. |
| **ฉันสามารถรับคะแนนความเชื่อมั่นได้หรือไม่?** |หลาย SDK จะเปิดเผยเมตริกความเชื่อมั่นต่อแต่ละพื้นที่. เพิ่มลงในคำสั่งพิมพ์: `print(f"[{bbox}] {region.text} (conf: {region.confidence:.2f})")`. |
| **จะจัดการข้อความที่หมุนได้อย่างไร?** | ทำการพรี‑โปรเซสรูปภาพด้วย `cv2.minAreaRect` ของ OpenCV เพื่อแก้ไขการเอียงก่อนเรียก `recognize`. |
| **ถ้าฉันต้องการผลลัพธ์ในรูปแบบ JSON จะทำอย่างไร?** |ทำการซีเรียลไลซ์ `processed_result.regions` ด้วย `json.dumps([r.__dict__ for r in processed_result.regions], indent=2)`. |
| **มีวิธีใดในการแสดงภาพกล่องบ้าง?** | ใช้ OpenCV: `cv2.rectangle(img, (x, y), (x+w, y+h), (0,255,0), 2)` ภายในลูป, จากนั้น `cv2.imwrite("annotated.jpg", img)`. |

## สรุป

คุณเพิ่งเรียนรู้ **how to perform OCR on image**, ทำความสะอาดผลลัพธ์ดิบ, และ **display bounding box coordinates** สำหรับทุกพื้นที่. กระบวนการสามขั้นตอน—recognize → post‑process → iterate—เป็นแพทเทิร์นที่นำกลับมาใช้ได้ในโปรเจกต์ Python ใด ๆ ที่ต้องการการดึงข้อความที่เชื่อถือได้.

### ขั้นตอนต่อไปคืออะไร?

- **สำรวจ OCR back‑ends ต่าง ๆ** (Tesseract, EasyOCR, Google Vision) และเปรียบเทียบความแม่นยำ.
- **รวมเข้ากับฐานข้อมูล** เพื่อเก็บข้อมูลพื้นที่สำหรับคลังข้อมูลที่สามารถค้นหาได้.
- **เพิ่มการตรวจจับภาษา** เพื่อส่งแต่ละพื้นที่ผ่าน spell‑checker ที่เหมาะสม.
- **วางกล่องบนรูปภาพต้นฉบับ** เพื่อการตรวจสอบภาพ (ดูโค้ด OpenCV ด้านบน).

หากคุณเจอข้อผิดพลาด, จำไว้ว่าการชนะใหญ่ที่สุดมาจากขั้นตอน post‑processing ที่แข็งแรง; สตริงที่สะอาดง่ายต่อการทำงานมากกว่าการดัมพ์อักขระดิบ.

ขอให้สนุกกับการเขียนโค้ด, และขอให้ pipeline OCR ของคุณเป็นระเบียบเสมอ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}