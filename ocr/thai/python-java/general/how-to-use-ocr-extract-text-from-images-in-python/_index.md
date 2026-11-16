---
category: general
date: 2026-03-18
description: วิธีใช้ OCR เพื่อดึงข้อความจากภาพ – คู่มือสั้นสำหรับการจดจำข้อความจากไฟล์
  PNG และการโหลดภาพสำหรับ OCR.
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from png
- how to extract text
- load image for OCR
language: th
og_description: วิธีใช้ OCR เพื่อดึงข้อความจากภาพ – เรียนรู้การจดจำข้อความจากไฟล์
  PNG, โหลดภาพสำหรับ OCR, และดึงข้อความด้วยสคริปต์ Python ง่าย ๆ
og_title: 'วิธีใช้ OCR: แยกข้อความจากรูปภาพใน Python'
tags:
- OCR
- Python
- Image Processing
title: 'วิธีใช้ OCR: แยกข้อความจากรูปภาพใน Python'
url: /th/python-java/general/how-to-use-ocr-extract-text-from-images-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีใช้ OCR: ดึงข้อความจากรูปภาพใน Python

เคยสงสัย **วิธีใช้ OCR** เมื่อคุณมีภาพหน้าจอที่รกหรือใบเสร็จสแกนไหม? คุณไม่ได้อยู่คนเดียว—นักพัฒนาต้องดึงข้อความที่อ่านได้ออกจากรูปภาพอยู่เสมอ โดยเฉพาะ PNG ที่มาจากแอปมือถือหรือการอัปโหลดบนเว็บ ในบทเรียนนี้เราจะเดินผ่านตัวอย่างที่ทำงานได้เต็มรูปแบบซึ่งจะแสดงให้คุณเห็น **วิธีดึงข้อความจากไฟล์รูปภาพ** , **วิธีจดจำข้อความจาก PNG** และแม้กระทั่ง **วิธีโหลดรูปภาพสำหรับ OCR** ด้วยเพียงไม่กี่บรรทัดของ Python

เราจะครอบคลุมทุกอย่างตั้งแต่การติดตั้งไลบรารีที่เหมาะสมจนถึงการจัดการเอกสารหลายภาษา ดังนั้นเมื่อจบคุณจะรู้ *วิธีดึงข้อความ* จากรูปภาพใด ๆ ที่คุณใส่เข้าไปในเครื่องยนต์ OCR ไม่ใช่การอ้างอิงที่คลุมเครือ แต่เป็นวิธีแก้ปัญหาแบบขั้นตอน‑ต่อ‑ขั้นตอนที่คุณสามารถคัดลอก‑วางและรันได้

## สิ่งที่คุณจะได้เรียนรู้

ในไม่กี่ส่วนต่อไปเราจะ:

1. ตั้งค่าเครื่องมือ OCR ที่เบา (ไม่ต้องพึ่งพาไลบรารีหนัก)  
2. โหลดไฟล์รูปภาพ—โดยเฉพาะ PNG—เข้าสู่เครื่องมือ  
3. เปิดการตรวจจับภาษาอัตโนมัติเพื่อให้เครื่องมือจัดการเนื้อหาหลายภาษาได้  
4. รันกระบวนการจดจำและดึงผลลัพธ์เป็นข้อความธรรมดา  
5. ปรับแต่งขั้นตอนทำงานสำหรับกรณีขอบเช่นไฟล์หายหรือรูปแบบที่ไม่รองรับ

หากคุณคุ้นเคยกับ Python เบื้องต้นก็พร้อมแล้ว ไม่จำเป็นต้องมีประสบการณ์ OCR มาก่อน แม้แต่การสแกนด็อกเมนต์สั้น ๆ ก็ช่วยได้

---

![วิธีใช้ OCR บนภาพ PNG](placeholder.png "วิธีใช้ OCR บนภาพ PNG – คู่มือขั้นตอน‑ต่อ‑ขั้นตอน")

## วิธีใช้ OCR – โหลดรูปภาพและจดจำข้อความ {#how-to-use-ocr}

### ขั้นตอน 1: ติดตั้งไลบรารี OCR

ก่อนอื่นคุณต้องมีแพ็กเกจ Python ที่ให้คลาส `OcrEngine` สำหรับบทเรียนนี้เราจะใช้แพ็กเกจ **SimpleOCR** (สมมติ) ซึ่งคุณสามารถติดตั้งผ่าน pip:

```bash
pip install simple-ocr
```

> **เคล็ดลับ:** หากคุณทำงานใน virtual environment (แนะนำอย่างยิ่ง) ให้เปิดใช้งานก่อนรันคำสั่งติดตั้ง เพื่อให้การจัดการ dependencies ของโปรเจคเป็นระเบียบ

### ขั้นตอน 2: นำเข้า engine และสร้างอินสแตนซ์

การสร้าง engine ทำได้ง่ายเพียงเรียกคอนสตรัคเตอร์ของมัน คิดว่า engine คือ “สมอง” ที่จะประมวลผลรูปภาพที่คุณป้อนให้

```python
# Step 2: Import and instantiate the OCR engine
from simple_ocr import OcrEngine

# Create a fresh engine instance – this allocates internal buffers
engine = OcrEngine()
```

ทำไมต้องสร้างอินสแตนซ์ใหม่ทุกครั้ง? เพื่อความเป็นอิสระ อินสแตนซ์ใหม่รับประกันว่าไม่มีสถานะที่เหลือจากการรันก่อนหน้ามารบกวนการจดจำครั้งนี้ ซึ่งสำคัญเมื่อคุณประมวลผลไฟล์จำนวนมากเป็นชุด

### ขั้นตอน 3: โหลดรูปภาพที่ต้องการประมวลผล

ตอนนี้เราจะ **โหลดรูปภาพสำหรับ OCR** จริง ๆ เมธอด `setImageFromFile` รับพาธไปยังไฟล์ raster ใดก็ได้; เราจะชี้ไปที่ PNG ชื่อ `mixed_doc.png`

```python
# Step 3: Load the PNG image you want to read
image_path = "YOUR_DIRECTORY/mixed_doc.png"
engine.setImageFromFile(image_path)
```

หากไฟล์ไม่พบ `SimpleOCR` จะโยน `FileNotFoundError` ที่ชัดเจน คุณสามารถดักจับเพื่อแสดงข้อความผิดพลาดที่เป็นมิตรได้:

```python
try:
    engine.setImageFromFile(image_path)
except FileNotFoundError:
    print(f"❗️ Unable to locate '{image_path}'. Check the path and try again.")
    raise
```

### ขั้นตอน 4: เปิดการตรวจจับภาษาอัตโนมัติ

เครื่องมือ OCR สมัยใหม่ส่วนใหญ่มาพร้อมกับ language pack โดยการส่งค่า `"multilingual"` เราบอก engine ให้ sniff ข้อความและเลือกโมเดลภาษาที่เหมาะสมโดยอัตโนมัติ ซึ่งสะดวกมากเมื่อ PNG ของคุณมีการผสมภาษาอังกฤษและสเปนเป็นตัวอย่าง

```python
# Step 4: Turn on auto‑language detection (covers all installed packs)
engine.setLanguage("multilingual")
```

หากคุณทราบภาษาล่วงหน้า สามารถแทน `"multilingual"` ด้วย locale เฉพาะเช่น `"eng"` หรือ `"spa"` เพื่อเร่งความเร็วการประมวลผล

### ขั้นตอน 5: รันกระบวนการจดจำ

นี่คือจุดที่ทำงานหนัก `recognize()` จะสแกนภาพ, ทำ segmentation, รัน neural net, และสร้าง buffer ของข้อความภายใน

```python
# Step 5: Execute OCR – this may take a moment for large images
engine.recognize()
```

เบื้องหลัง engine ทำงานดังนี้:

- **Pre‑processing** (deskewing, binarization)  
- **Layout analysis** (detecting columns, tables)  
- **Character classification** (using a deep‑learning model)  

ทั้งหมดนี้ถูกซ่อนอยู่ ทำให้คุณต้องใช้เพียงบรรทัดเดียว

### ขั้นตอน 6: ดึงและพิมพ์ข้อความที่จดจำได้

สุดท้ายเราดึงอ็อบเจกต์ผลลัพธ์และแยกสตริงธรรมดาออกมา นี่คือส่วนที่คุณ **ดึงข้อความจากรูปภาพ** จริง ๆ

```python
# Step 6: Get the OCR result and display the plain text
result = engine.getResult()
text = result.getText()
print("📝 Recognized Text:\n")
print(text)
```

**ผลลัพธ์ที่คาดหวัง** (ตัดให้สั้นลงเพื่อความกระชับ):

```
📝 Recognized Text:

Invoice #12345
Date: 2026‑03‑15
Total: $89.99
Thank you for your purchase!
```

หากภาพไม่มีอักขระที่จดจำได้ `text` จะเป็นสตริงว่าง คุณสามารถตรวจสอบได้ดังนี้:

```python
if not text.strip():
    print("⚠️ No text detected – try a higher‑resolution image or adjust preprocessing.")
```

---

## ดึงข้อความจากรูปภาพ – จัดการกรณีขอบทั่วไป

### หลายภาษาในไฟล์เดียว

เมื่อเอกสารถูกผสมหลายภาษา การตั้งค่า `"multilingual"` มักทำงานได้ดี อย่างไรก็ตาม หากพบการจดจำผิดพลาด คุณสามารถระบุรายการ fallback ด้วยตนเองได้:

```python
engine.setLanguage(["eng", "spa", "fra"])  # English, Spanish, French
```

### รูปแบบที่ไม่ใช่ PNG

แม้ว่าเราจะเน้น **จดจำข้อความจาก PNG** แต่ `SimpleOCR` ยังรองรับ JPEG, BMP, และ TIFF เพียงเปลี่ยนนามสกุลไฟล์ใน `setImageFromFile` สำหรับ TIFF stack คุณอาจต้องเลือกหน้าเฉพาะ:

```python
engine.setImageFromFile("scanned.tif", page=0)  # first page only
```

### ไฟล์ขนาดใหญ่และการใช้หน่วยความจำ

หากคุณประมวลผลสแกนขนาดกิกะพิกเซล ควรปรับขนาดภาพก่อนทำ OCR:

```python
from PIL import Image

with Image.open(image_path) as img:
    img.thumbnail((2000, 2000))  # keep aspect ratio, max 2000px
    img.save("temp_resized.png")
engine.setImageFromFile("temp_resized.png")
```

การปรับขนาดช่วยลดความกดดันของหน่วยความจำในขณะที่ยังคงรักษารายละเอียดที่เพียงพอสำหรับการจดจำที่แม่นยำ

### การดีบักการโหลดที่ล้มเหลว

บางครั้งภาพดูโอเคต่อสายตาแต่ภายในอาจเสียหาย เปิดการบันทึก verbose เพื่อดูว่า engine เห็นอะไร:

```python
engine.enableDebug(True)   # prints internal steps to stdout
engine.recognize()
```

---

## สคริปต์เต็มพร้อมรัน

ด้านล่างเป็นโปรแกรมเต็มที่รวมทุกส่วนเข้าด้วยกัน คัดลอกไปไฟล์ชื่อ `ocr_demo.py` ปรับค่า placeholder `YOUR_DIRECTORY` แล้วรันด้วย `python ocr_demo.py`

```python
# ocr_demo.py
# Full example showing how to use OCR to extract text from a PNG image.
# Requires: pip install simple-ocr pillow

from simple_ocr import OcrEngine
import os
from PIL import Image

def main():
    # 1️⃣ Create the OCR engine
    engine = OcrEngine()

    # 2️⃣ Define the image path – change this to your actual file location
    image_path = os.path.join("YOUR_DIRECTORY", "mixed_doc.png")

    # 3️⃣ Load the image (with a safety net for missing files)
    try:
        engine.setImageFromFile(image_path)
    except FileNotFoundError:
        print(f"❗️ Cannot find image at '{image_path}'. Exiting.")
        return

    # Optional: resize large images to keep memory usage low
    # (uncomment if you deal with huge scans)
    # with Image.open(image_path) as img:
    #     img.thumbnail((2000, 2000))
    #     resized_path = "temp_resized.png"
    #     img.save(resized_path)
    #     engine.setImageFromFile(resized_path)

    # 4️⃣ Enable automatic language detection (covers all installed packs)
    engine.setLanguage("multilingual")

    # 5️⃣ Run the OCR engine
    engine.recognize()

    # 6️⃣ Retrieve and print the recognized text
    result = engine.getResult()
    text = result.getText()

    if text.strip():
        print("\n📝 Recognized Text:\n")
        print(text)
    else:
        print("⚠️ No recognizable text found. Try a clearer image or adjust preprocessing.")

if __name__ == "__main__":
    main()
```

เมื่อรันสคริปต์นี้ควรแสดงข้อความธรรมดาของสิ่งที่อยู่ใน `mixed_doc.png` คุณสามารถเปลี่ยนไฟล์เป็นรูปอื่นได้—**วิธีดึงข้อความ** จะทำงานเช่นเดียวกัน

---

## สรุป

เราได้เดินผ่าน **วิธีใช้ OCR** ใน Python เพื่อ **ดึงข้อความจากไฟล์รูปภาพ** โดยเฉพาะการ **จดจำข้อความจาก PNG** และขั้นตอนปฏิบัติในการ **โหลดรูปภาพสำหรับ OCR** โค้ดตัวอย่างข้างต้นเป็นโซลูชันครบวงจร: ติดตั้งแพ็กเกจ, ป้อนไฟล์, เปิดการตรวจจับหลายภาษา, รัน engine, และดึงผลลัพธ์

ต่อจากนี้คุณอาจ:

- ผสานสคริปต์เข้ากับเว็บเซอร์วิสที่รับอัปโหลดจากผู้ใช้  
- ประมวลผลเป็นชุดของโฟลเดอร์ PDF ที่แปลงเป็น PNG  
- เพิ่มการประมวลผลหลัง (เช่น ทำความสะอาดด้วย regex, ตรวจสอบการสะกด) เพื่อเพิ่มความแม่นยำ

จำไว้ว่า คุณภาพของ OCR ขึ้นกับความชัดเจนของภาพ, language pack ที่เหมาะสม, และบางครั้งการทำ pre‑processing เล็กน้อย—ลองทดลองดู

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}