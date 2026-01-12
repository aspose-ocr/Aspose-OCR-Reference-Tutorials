---
category: general
date: 2026-01-12
description: วิธีทำ OCR และแปลงภาพเป็นข้อความอย่างรวดเร็ว เรียนรู้การจดจำอักขระพิเศษ
  การดึงข้อความจากภาพ และการโหลดภาพสำหรับ OCR พร้อมตัวอย่าง Python ฉบับสมบูรณ์
draft: false
keywords:
- how to perform OCR
- convert image to text
- recognize special characters
- extract text from image
- load image for OCR
language: th
og_description: วิธีทำ OCR ด้วย Python แปลงภาพเป็นข้อความและจดจำอักขระพิเศษ ตามคู่มือการทำงานจริงนี้เพื่อสกัดข้อความจากภาพ
og_title: วิธีทำ OCR ใน Python – บทเรียนเต็ม
tags:
- OCR
- Python
- Image Processing
title: วิธีทำ OCR ด้วย Python – คู่มือขั้นตอนโดยละเอียด
url: /th/python/general/how-to-perform-ocr-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีทำ OCR ใน Python – คู่มือขั้นตอน

เคยต้อง **perform OCR** บนภาพหน้าจอที่มีอักขระละตินและซีริลลิกผสมกันหรือไม่? คุณไม่ได้อยู่คนเดียว ในหลายโครงการ—ไม่ว่าจะเป็นการแปลงใบเสร็จเป็นดิจิทัล, การทำดัชนีเอกสารหลายภาษา, หรือการสร้างคลังข้อมูลที่ค้นหาได้—**how to perform OCR** กลายเป็นคำถามที่สำคัญอย่างเร็ว  

ในบทเรียนนี้เราจะเดินผ่านตัวอย่างที่ทำงานได้เต็มรูปแบบและพร้อมรัน ซึ่งจะแสดงให้คุณเห็นวิธี **convert image to text**, **recognize special characters**, และ **extract text from image** ด้วยไลบรารี Python อย่างง่าย สุดท้ายคุณจะได้สคริปต์ที่พร้อมรันเพื่อโหลดภาพสำหรับ OCR, จัดการเนื้อหาหลายภาษา, และพิมพ์ผลลัพธ์ออกมา

## สิ่งที่คุณต้องมี

ก่อนที่เราจะเริ่มลงลึก โปรดตรวจสอบว่าคุณมีสิ่งต่อไปนี้แล้ว:

- Python 3.8+ ติดตั้งบนเครื่องของคุณ  
- แพ็กเกจ `ocr` (หรือไลบรารี OCR ที่เข้ากันได้) ติดตั้งโดยใช้ `pip install ocr`  
- ไฟล์รูปภาพ (`multilingual.png`) ที่มีอักขระละตินและซีริลลิก  
- โปรแกรมแก้ไขข้อความพื้นฐานหรือ IDE—VS Code, PyCharm หรือแม้แต่ Notepad ธรรมดาก็ใช้ได้  

หากคุณไม่มีแพ็กเกจ `ocr` คุณสามารถเปลี่ยนเป็น `pytesseract` พร้อมทำการปรับเปลี่ยนเล็กน้อย; แนวคิดหลักยังคงเหมือนเดิม

## ขั้นตอนที่ 1: ติดตั้งและนำเข้าไลบรารี OCR

ก่อนอื่นเราจะเตรียมเครื่องยนต์ OCR ให้พร้อม เราจะนำเข้าไลบรารี, สร้างอินสแตนซ์ของเครื่องยนต์, และตั้งค่าการสนับสนุนหลายภาษา

```python
# Install the library (run this once in your terminal)
# pip install ocr

import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()

# Optional: Enable language packs for Latin and Cyrillic
engine.set_languages(['eng', 'rus'])  # 'eng' = English, 'rus' = Russian
```

**ทำไมสิ่งนี้สำคัญ:**  
การสร้างเครื่องยนต์เป็นพื้นฐาน—หากไม่มีคุณจะไม่สามารถ **load image for OCR** ได้ในภายหลัง การเปิดใช้งานแพ็คเกจภาษาทำให้เครื่องยนต์สามารถระบุอักขระอย่าง “Ŀ”, “Ҕ”, และ “Ǣ” ได้อย่างถูกต้อง หากข้ามขั้นตอนนี้ คุณจะได้ผลลัพธ์เป็นข้อความเสียหายสำหรับสคริปต์ที่ไม่ใช่ละติน

## ขั้นตอนที่ 2: โหลดภาพที่มีข้อความหลายภาษา

ต่อไปเราจะชี้เครื่องยนต์ไปยังไฟล์ที่ต้องการประมวลผล เส้นทางไฟล์อาจเป็นแบบเต็มหรือแบบสัมพันธ์; เพียงให้แน่ใจว่าไฟล์นั้นสามารถอ่านได้

```python
# Step 2: Load the image containing multilingual text
image_path = "YOUR_DIRECTORY/multilingual.png"  # replace with your actual path
engine.load_image(image_path)
```

> ![ตัวอย่างการทำ OCR](/images/ocr-example.png "วิธีทำ OCR บนภาพหลายภาษา")

**ทำไมสิ่งนี้สำคัญ:**  
คำสั่ง `load_image` จะอ่านข้อมูลพิกเซลเข้าสู่หน่วยความจำเพื่อเตรียมให้พร้อมกับอัลกอริทึม OCR หากภาพมีขนาดใหญ่ เครื่องยนต์อาจทำการลดขนาดอัตโนมัติ; คุณสามารถปรับแต่งต่อไปด้วย `engine.set_max_resolution(3000)` สำหรับการสแกนความละเอียดสูง

## ขั้นตอนที่ 3: รันกระบวนการจดจำ

เมื่อเครื่องยนต์พร้อมและภาพถูกโหลดแล้ว เราจึงสามารถสกัดข้อความจากภาพได้

```python
# Step 3: Perform OCR recognition on the loaded image
result = engine.recognize()
```

**ทำไมสิ่งนี้สำคัญ:**  
`recognize()` ทำงานหนักของเครือข่ายประสาทเทียมเบื้องหลัง มันจะคืนอ็อบเจกต์ที่บรรจุข้อความดิบ, คะแนนความเชื่อมั่น, และแม้กระทั่งกล่องขอบเขต (bounding boxes) หากคุณต้องการใช้สำหรับการดีบักภาพ

## ขั้นตอนที่ 4: แสดงข้อความที่จดจำได้

มาดูว่ากลไกได้พบอะไรบ้าง เราจะพิมพ์ข้อความลงคอนโซล, แต่คุณก็สามารถบันทึกลงไฟล์หรือฐานข้อมูลได้เช่นกัน

```python
# Step 4: Output the recognized text, which should include characters like “Ŀ”, “Ҕ”, “Ǣ”
print("=== OCR Result ===")
print(result.text)
```

### ผลลัพธ์ที่คาดหวัง

```
=== OCR Result ===
Hello, world! Ŀ is a Latin‑extended character.
Привет, мир! Ҕ is a Cyrillic character.
Special combo: Ǣ is a ligature.
```

หากคุณเห็นผลลัพธ์คล้ายกัน ยินดีด้วย—คุณได้ **convert image to text** และ **recognize special characters** อย่างสำเร็จ

## การจัดการกับปัญหาทั่วไป

แม้สคริปต์จะเรียบง่าย คุณอาจเจออุปสรรคบางอย่าง ด้านล่างนี้เป็นเคล็ดลับจากประสบการณ์ของผม

### 1. ขาดแพ็คเกจภาษา

หากคุณเห็นเครื่องหมายคำถาม (`?`) แทนตัวอักษรซีริลลิก ให้ตรวจสอบว่าติดตั้งแพ็คเกจภาษาแล้วหรือยัง สำหรับหลายเครื่องมือ OCR คุณต้องดาวน์โหลดไฟล์ `.traineddata` ที่สอดคล้องและวางไว้ในโฟลเดอร์ `tessdata` ของเครื่องยนต์

```python
# Example for pytesseract
import pytesseract
pytesseract.pytesseract.tesseract_cmd = r"C:\Program Files\Tesseract-OCR\tesseract.exe"
# Ensure 'eng' and 'rus' data files exist in tessdata
```

### 2. คุณภาพภาพต่ำ

ภาพเบลอหรือคอนทราสต์ต่ำทำให้คะแนนความเชื่อมั่นต่ำ ก่อนประมวลผลด้วย OpenCV:

```python
import cv2

# Load, convert to grayscale, and apply thresholding
raw = cv2.imread(image_path)
gray = cv2.cvtColor(raw, cv2.COLOR_BGR2GRAY)
_, thresh = cv2.threshold(gray, 150, 255, cv2.THRESH_BINARY)

# Save a temporary cleaned image and feed it to the OCR engine
cv2.imwrite("cleaned.png", thresh)
engine.load_image("cleaned.png")
```

### 3. ไฟล์ขนาดใหญ่และการใช้หน่วยความจำ

การประมวลผลภาพขนาด 10 MB สามารถทำให้หน่วยความจำพุ่งสูง ใช้ `engine.set_max_image_size(2000)` เพื่อตั้งค่าขีดจำกัดความละเอียด, หรือแบ่งภาพเป็นหลายส่วนแล้ว OCR ทีละส่วน

### 4. การจับกล่องขอบเขต

หากต้องการไฮไลท์ตำแหน่งของแต่ละคำ (มีประโยชน์สำหรับ UI overlay) ให้เข้าถึง `result.boxes`:

```python
for box in result.boxes:
    print(f"Word: {box.text} – Coordinates: {box.x0},{box.y0},{box.x1},{box.y1}")
```

## สคริปต์เต็ม – การรันคลิกเดียว

รวมทุกอย่างเข้าด้วยกัน นี่คือไฟล์เดียวที่คุณสามารถรันด้วย `python ocr_demo.py` มันรวมการจัดการข้อผิดพลาด, การเตรียมภาพแบบเลือก, และคอมเมนต์เพื่อความชัดเจน

```python
#!/usr/bin/env python3
"""
Complete OCR demo: load image, recognize multilingual text,
and print results. Works with the generic 'ocr' library.
"""

import os
import sys
import ocr

def main(image_path: str):
    # Verify the image exists
    if not os.path.isfile(image_path):
        sys.exit(f"Error: File not found – {image_path}")

    # Initialize the OCR engine
    engine = ocr.OcrEngine()
    engine.set_languages(['eng', 'rus'])          # load language packs
    engine.set_max_image_size(2500)               # limit memory usage

    # Load the image
    try:
        engine.load_image(image_path)
    except Exception as e:
        sys.exit(f"Failed to load image: {e}")

    # Perform recognition
    try:
        result = engine.recognize()
    except Exception as e:
        sys.exit(f"OCR failed: {e}")

    # Output the text
    print("\n=== OCR Result ===")
    print(result.text)

    # Optional: display confidence scores
    if hasattr(result, "confidence"):
        avg_conf = sum(result.confidence) / len(result.confidence)
        print(f"\nAverage confidence: {avg_conf:.1%}")

if __name__ == "__main__":
    # Replace with your actual image path or pass as CLI argument
    img = sys.argv[1] if len(sys.argv) > 1 else "YOUR_DIRECTORY/multilingual.png"
    main(img)
```

รันด้วย:

```bash
python ocr_demo.py path/to/multilingual.png
```

คุณควรเห็นผลลัพธ์เดียวกับที่แสดงไว้ก่อนหน้า ยืนยันว่าคุณได้ **extract text from image** อย่างสำเร็จ

## สรุป

เราได้ครอบคลุม **how to perform OCR** ใน Python ตั้งแต่การติดตั้งไลบรารี, การโหลดภาพ, การจดจำเนื้อหาหลายภาษา, และการจัดการกับกรณีขอบที่พบบ่อยที่สุด ด้วยคู่มือนี้คุณสามารถ **convert image to text**, **recognize special characters**, และ **extract text from image** ในโปรเจกต์ของคุณได้แล้ว—ไม่ต้องพิมพ์ด้วยมืออีกต่อไป

ต่อไปคุณอาจลอง:

- เพิ่มแพ็คเกจภาษาอื่น (เช่น `spa` สำหรับสเปน)  
- ส่งออกผลลัพธ์เป็น JSON เพื่อการประมวลผลต่อไป  
- รวมขั้นตอน OCR เข้าใน Flask API เพื่อให้บริการอื่นเรียกใช้ได้  

หากเจอข้อผิดพลาดใด ๆ ชุมชนของไลบรารี OCR ส่วนใหญ่ค่อนข้างกระตือรือร้น—ค้นหา “ocr library language pack installation” หรือแสดงความคิดเห็นด้านล่างได้เลย ขอให้สนุกกับการเขียนโค้ดและแปลงรูปภาพเป็นข้อความที่ค้นหาได้!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}