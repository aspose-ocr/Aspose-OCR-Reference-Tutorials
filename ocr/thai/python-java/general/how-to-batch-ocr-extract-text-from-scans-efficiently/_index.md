---
category: general
date: 2026-04-26
description: วิธีทำ OCR เอกสารเป็นชุดและดึงข้อความจากสแกนใน Python เรียนรู้การประมวลผลเป็นชุดแบบขั้นตอนด้วย
  OcrEngine เพื่อรับผลลัพธ์เป็น JSON
draft: false
keywords:
- how to batch OCR
- extract text from scans
- OCR batch processing
- Python OCR automation
- JSON OCR output
language: th
og_description: วิธีทำ OCR เป็นชุดกับไฟล์สแกนของคุณและดึงข้อความจากการสแกนในสคริปต์เดียว
  โค้ดเต็ม, เคล็ดลับ, และการจัดการกรณีขอบ
og_title: วิธีทำ OCR แบบแบตช์ – คู่มือ Python อย่างรวดเร็ว
tags:
- OCR
- Python
- Automation
title: วิธีทำ OCR แบบกลุ่ม – ดึงข้อความจากการสแกนอย่างมีประสิทธิภาพ
url: /th/python-java/general/how-to-batch-ocr-extract-text-from-scans-efficiently/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีทำ Batch OCR – แยกข้อความจากการสแกนอย่างมีประสิทธิภาพ

เคยสงสัย **how to batch OCR** กอง PDF ที่สแกนไว้จำนวนมหาศาลโดยไม่ทำให้คุณบ้าหรือไม่? คุณไม่ได้เป็นคนเดียว—นักพัฒนามักถามบ่อยว่า *“จะดึงข้อความจากการสแกนทั้งหมดในครั้งเดียวได้อย่างไร?”* ข่าวดีคือเพียงไม่กี่บรรทัดของ Python ก็สามารถเปลี่ยนงานที่น่าเบื่อให้เป็นกระบวนการอัตโนมัติที่ราบรื่นได้

ในบทแนะนำนี้เราจะเดินผ่านโซลูชันที่สมบูรณ์พร้อมรันได้ทันทีที่ **extracts text from scans**, บันทึกผลเป็น JSON, และให้การตรวจสอบความถูกต้องอย่างรวดเร็วในตอนท้าย ไม่ต้องพึ่งบริการภายนอก ไม่ต้องใช้เวทมนตร์—แค่ Python ธรรมดา, คลาส `OcrEngine`, และการจัดการโฟลเดอร์เล็กน้อย

## สิ่งที่คุณจะได้เรียนรู้

- สคริปต์ที่ทำงานเต็มรูปแบบซึ่ง **batches OCR** บนโฟลเดอร์รูปภาพใด ๆ
- คำอธิบายที่ชัดเจนว่าทำไมแต่ละบรรทัดถึงมีอยู่ ไม่ใช่แค่ทำอะไร
- เคล็ดลับการจัดการโฟลเดอร์ว่าง, ไฟล์ที่ไม่ใช่รูปภาพ, และแบชขนาดใหญ่
- วิธีตรวจสอบว่าไฟล์ JSON มีข้อความที่ดึงออกมาจริง ๆ

### ข้อกำหนดเบื้องต้น (ขั้นต่ำที่สุด)

| Requirement | Why it matters |
|-------------|----------------|
| Python 3.8+ | ไวยากรณ์สมัยใหม่ & type hints |
| `OcrEngine` library (or a compatible wrapper) | ฟังก์ชัน OCR หลัก |
| โฟลเดอร์ที่มีไฟล์สแกนเป็นรูปภาพ (PNG, JPG, TIFF) | ข้อมูลเข้า |
| สิทธิ์การเขียนสำหรับโฟลเดอร์ผลลัพธ์ | บันทึกไฟล์ JSON |

หากคุณมีทั้งหมดนี้แล้ว เยี่ยม—มาเริ่มกันเลย

![วิธีทำ batch OCR workflow](image-placeholder.png){alt="วิธีทำ batch OCR workflow"}

## ขั้นตอนที่ 1 – เริ่มต้น OCR Engine (how to batch OCR)

ก่อนที่เราจะประมวลผลอะไรได้ เราต้องมีอินสแตนซ์ของ OCR engine คิดว่าเป็น “สมอง” ที่จะอ่านแต่ละภาพและแปลงเป็นข้อความ การสร้างครั้งเดียวแล้วใช้ซ้ำตลอดแบชเป็นรูปแบบที่มีประสิทธิภาพที่สุด

```python
# Step 1: Create an OCR engine instance
# The OcrEngine class abstracts the low‑level OCR library (Tesseract, EasyOCR, etc.)
ocr_engine = OcrEngine()
```

> **ทำไมต้องใช้อินสแตนซ์เดียว?**  
> การสร้างเอนจินใหม่สำหรับทุกไฟล์จะทำให้ต้องโหลดโมเดลหนัก ๆ เข้า RAM ซ้ำ ๆ ทำให้แบชช้าลงอย่างมาก อินสแตนซ์เดียวจะเก็บโมเดลใน RAM และให้คุณประมวลผลภาพหลายพันรูปโดยไม่รู้สึกช้าลง

## ขั้นตอนที่ 2 – ระบุตำแหน่งโฟลเดอร์สแกนของคุณ (extract text from scans)

สแกนของคุณอยู่ที่ไหนบนดิสก์ ให้บอกสคริปต์ว่าไปหาได้ที่ไหน การใช้พาธแบบ absolute จะหลีกเลี่ยงปัญหา “ไฟล์ไม่พบ” เมื่อสคริปต์รันจากโฟลเดอร์ทำงานอื่น

```python
import os

# Step 2: Specify the folder that contains scanned images
# Replace YOUR_DIRECTORY with the actual base path on your machine.
input_dir = os.path.abspath("YOUR_DIRECTORY/scans/")
```

> **เคล็ดลับมือโปร:**  
> หากคุณใช้ Windows, เครื่องหมายทับ (`/`) ทำงานได้ดีกับ `os.path.abspath` ดังนั้นไม่จำเป็นต้อง escape backslashes

## ขั้นตอนที่ 3 – เลือกตำแหน่งที่ผลลัพธ์ JSON ควรจะไป

คุณอาจต้องการโฟลเดอร์ที่เป็นระเบียบสำหรับผลลัพธ์ OCR การแยกเอาต์พุตออกจากแหล่งข้อมูลทำให้ทำความสะอาดได้ง่ายหรือส่งต่อ JSON ไปยัง pipeline อื่น

```python
# Step 3: Specify where the JSON results should be saved
output_dir = os.path.abspath("YOUR_DIRECTORY/json_output/")
os.makedirs(output_dir, exist_ok=True)   # Ensure the folder exists
```

> **ทำไมต้องสร้างโฟลเดอร์ด้วยโปรแกรม?**  
> มันรับประกันว่าสคริปต์จะไม่พังหากโฟลเดอร์ไม่มีอยู่, และ `exist_ok=True` ทำให้การดำเนินการเป็น idempotent—รันสคริปต์หลายครั้งก็ไม่มีข้อผิดพลาด

## ขั้นตอนที่ 4 – รันกระบวนการแบช (how to batch OCR)

นี่คือหัวใจของเรื่อง: บอก `ocr_engine` ให้เดินผ่านทุกไฟล์ใน `input_dir`, ทำ OCR, แล้วบันทึกเป็น JSON ไปที่ `output_dir` ธง `format="json"` บอกเอนจินให้จัดผลลัพธ์ในรูปแบบโครงสร้างที่เครื่องมือ downstream ชอบ

```python
# Step 4: Run batch processing to convert all scans to JSON format
ocr_engine.batch_process(
    input_folder=input_dir,
    output_folder=output_dir,
    format="json"
)
```

### สิ่งที่เกิดขึ้นเบื้องหลัง?

1. **การค้นหาไฟล์** – เอนจินสแกน `input_folder` อย่าง recursive, ข้ามไฟล์ที่ซ่อนอยู่
2. **การตรวจสอบไฟล์** – เฉพาะไฟล์รูปภาพที่รองรับ (`.png`, `.jpg`, `.tif`, ฯลฯ) เท่านั้นที่ส่งให้โมเดล OCR
3. **การทำ OCR** – ส่งแต่ละภาพไปยัง OCR engine; ดึงข้อความ, คะแนนความมั่นใจ, และข้อมูลเลย์เอาต์
4. **การแปลงเป็น JSON** – ผลลัพธ์จะถูกเขียนเป็นไฟล์ที่มีชื่อฐานเดียวกันแต่ต่อด้วย `.json` ใน `output_folder`

> **การจัดการกรณีขอบ:**  
> - **โฟลเดอร์ว่าง:** เอนจินบันทึก “No files found” แล้วจบอย่างสุภาพ  
> - **ภาพเสีย:** ข้ามไฟล์, บันทึกข้อผิดพลาดใน `batch_errors.log`, แล้วดำเนินต่อ  
> - **แบชขนาดใหญ่ (10k+ ไฟล์):** การใช้หน่วยความจำคงที่ต่ำเพราะแต่ละภาพประมวลผลแยกกัน

## ขั้นตอนที่ 5 – ยืนยันการแปลงเสร็จสิ้น

คำสั่ง `print` ง่าย ๆ จะให้ฟีดแบ็กทันทีในคอนโซล สำหรับ pipeline ผลิตจริงคุณอาจเปลี่ยนเป็นการล็อกหรือส่งอีเมลแจ้ง

```python
# Step 5: Inform the user that the batch conversion has finished
print("Batch conversion complete.")
```

เมื่อคุณเห็นบรรทัดนั้น, คุณสามารถตรวจสอบโฟลเดอร์ `json_output` ได้อย่างปลอดภัย แต่ละไฟล์ JSON จะมีลักษณะประมาณนี้:

```json
{
  "file_name": "invoice_001.png",
  "text": "Invoice #001\nDate: 2024‑12‑01\nTotal: $1,234.56",
  "confidence": 0.97,
  "layout": [
    {"line": 1, "bbox": [10, 20, 200, 40]},
    {"line": 2, "bbox": [10, 50, 180, 70]},
    {"line": 3, "bbox": [10, 80, 150, 100]}
  ]
}
```

คุณสามารถนำไฟล์ JSON เหล่านี้ไปใส่ในฐานข้อมูล, ดัชนีการค้นหา, หรือเครื่องมือวิเคราะห์ downstream ใด ๆ ก็ได้

## คำถามที่พบบ่อย (และคำตอบสั้น)

**Q: ถ้าต้องการประมวลผล PDF แทนรูปภาพล่ะ?**  
A: แปลงแต่ละหน้า PDF เป็นรูปภาพก่อน (เช่น ใช้ `pdf2image`) แล้ววางไฟล์ PNG/JPG ที่ได้ลงใน `input_dir` โค้ดแบช OCR จะไม่ต้องเปลี่ยนแปลง

**Q: สามารถเปลี่ยนรูปแบบเอาต์พุตเป็นข้อความธรรมดาได้ไหม?**  
A: ทำได้เลย แค่เปลี่ยน `format="json"` เป็น `format="txt"` แล้วเอนจินจะเขียนไฟล์ `.txt` ที่มีเฉพาะข้อความที่ดึงออกมา

**Q: สแกนของฉันอยู่หลายโฟลเดอร์ย่อย—สคริปต์จะทำการ recurse หรือไม่?**  
A: ใช่ `batch_process` จะเดินทางผ่านโครงสร้างโฟลเดอร์โดยค่าเริ่มต้น หากต้องการเอาต์พุตแบบแบน ให้ตั้งค่า `flatten=True` (ถ้าห้องสมุดรองรับ) หรือทำ post‑process ชื่อไฟล์ JSON เอง

**Q: จะจัดการกับสคริปต์ที่ไม่ใช่ละตินอย่างไร?**  
A: เริ่มต้น `OcrEngine` ด้วยพารามิเตอร์ภาษา, เช่น `OcrEngine(lang="spa+eng")` ส่วนลูปแบชไม่ต้องเปลี่ยนแปลงใด ๆ

## เคล็ดลับระดับมืออาชีพ & จุดหลบหลีกทั่วไป

- **ขนาดแบชสำคัญ:** หากเห็น CPU พุ่งสูง ให้ใส่ `time.sleep(0.1)` ระหว่างไฟล์เพื่อชะลอ
- **การล็อก:** แทนที่ `print` ด้วยโมดูล `logging` ของ Python เพื่อบันทึกเวลาและระดับข้อผิดพลาด
- **การชนชื่อไฟล์:** หากสองสแกนมีชื่อฐานเดียวกันแต่อยู่ในโฟลเดอร์ย่อยต่างกัน, ไฟล์ JSON จะเขียนทับกัน ให้เพิ่มแฮชของพาธสัมพันธ์ลงในชื่อเอาต์พุตเพื่อหลีกเลี่ยง
- **การรั่วของหน่วยความจำ:** บาง backend ของ OCR จะเก็บทรัพยากรเนทีฟไว้ ให้เรียก `ocr_engine.close()` ตอนจบสคริปต์หากไลบรารีมีเมธอดทำความสะอาด

## สคริปต์เต็ม – พร้อมคัดลอก & วาง

```python
import os
from ocr_engine import OcrEngine   # Replace with the actual import path

def main():
    # Step 1: Initialize the OCR engine (how to batch OCR)
    ocr_engine = OcrEngine()

    # Step 2: Directory with scanned images (extract text from scans)
    input_dir = os.path.abspath("YOUR_DIRECTORY/scans/")
    if not os.path.isdir(input_dir):
        raise FileNotFoundError(f"Input folder not found: {input_dir}")

    # Step 3: Destination for JSON results
    output_dir = os.path.abspath("YOUR_DIRECTORY/json_output/")
    os.makedirs(output_dir, exist_ok=True)

    # Step 4: Run the batch OCR process
    ocr_engine.batch_process(
        input_folder=input_dir,
        output_folder=output_dir,
        format="json"
    )

    # Step 5: Confirmation message
    print("Batch conversion complete.")

if __name__ == "__main__":
    main()
```

**ผลลัพธ์ที่คาดว่าจะเห็นในคอนโซล**

```
Scanning folder: /home/user/YOUR_DIRECTORY/scans/
Found 42 image files.
Processing file 1/42: invoice_001.png … done.
Processing file 2/42: receipt_2024-03.jpg … done.
…
Batch conversion complete.
```

คุณสามารถตรวจสอบ JSON ได้โดยเปิดไฟล์ใดไฟล์หนึ่งใน `json_output` ด้วยโปรแกรมแก้ไขข้อความหรือโหลดใน Python:

```python
import json, pathlib

sample = pathlib.Path(output_dir) / "invoice_001.json"
data = json.loads(sample.read_text())
print(data["text"])
```

คุณควรเห็นข้อความดิบที่ OCR‑extract มาแสดงในคอนโซล

## สรุป

เราได้อธิบาย **how to batch OCR** โฟลเดอร์เต็มของภาพสแกนและ **extract text from scans** ไปเป็นไฟล์ JSON ที่อ่านได้โดยเครื่องจักร วิธีการนี้ออกแบบให้เรียบง่าย: ตั้งค่าเอนจินครั้งเดียว, ชี้ไปที่โฟลเดอร์, แล้วให้ไลบรารีทำงานหนักจากนั้นคุณสามารถ:

- เชื่อมต่อ JSON

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}