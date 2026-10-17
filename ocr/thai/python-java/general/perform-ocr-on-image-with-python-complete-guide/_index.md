---
category: general
date: 2026-07-05
description: ทำ OCR บนภาพด้วย Python อย่างรวดเร็ว เรียนรู้วิธีโหลดภาพสำหรับ OCR ดึงข้อความจากแบบฟอร์มที่สแกน
  และใช้ OCR จดจำภาพใน Python.
draft: false
keywords:
- perform OCR on image
- load image for OCR
- how to use OCR Python
- extract text from scanned form
- OCR recognize image Python
language: th
og_description: ทำ OCR บนรูปภาพด้วย Python บทเรียนนี้แสดงวิธีโหลดรูปภาพสำหรับ OCR,
  ดึงข้อความจากแบบฟอร์มที่สแกน, และใช้ OCR เพื่อจดจำรูปภาพใน Python.
og_title: ทำ OCR บนภาพด้วย Python – คู่มือครบถ้วน
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Perform OCR on image in Python quickly. Learn how to load image for
    OCR, extract text from scanned form, and use OCR recognize image Python.
  headline: Perform OCR on Image with Python – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: ทำ OCR บนภาพด้วย Python – คู่มือครบวงจร
url: /th/python-java/general/perform-ocr-on-image-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ทำ OCR บนรูปภาพด้วย Python – คู่มือฉบับสมบูรณ์

เคยต้อง **perform OCR on image** ไฟล์แต่ไม่รู้จะเริ่มจากตรงไหนใน Python หรือไม่? คุณไม่ได้เป็นคนเดียว ไม่ว่าคุณจะกำลังดิจิไทซ์ใบเสร็จ, ดึงข้อมูลจากแบบสอบถามที่มีสัญญาณรบกวน, หรือแค่แปลง PDF ที่สแกนเป็นข้อความที่ค้นหาได้ ความสามารถในการ **extract text from a scanned form** เป็นปัญหาประจำวันของนักพัฒนาหลายคน

ในบทเรียนนี้เราจะพาคุณผ่าน **how to use OCR Python** ไลบรารีขั้นตอน‑ต่อ‑ขั้นตอน ตั้งแต่การโหลดรูปภาพจนถึงการแสดงผลลัพธ์ที่กรองแล้ว เมื่อจบคุณจะรู้วิธี **load image for OCR**, ตั้งค่า confidence thresholds, และเรียกใช้เมธอด **OCR recognize image Python** ที่ทำงานหนักจริง ๆ

> **สิ่งที่คุณจะได้:** สคริปต์พร้อมรันที่โหลดรูปภาพ, ทำ OCR, และพิมพ์ข้อความที่กรองด้วย confidence แล้ว ไม่มีการอ้างอิงที่คลุมเครือ, ไม่มีการ import ที่หายไป—เพียงโซลูชันคัดลอก‑วางที่สมบูรณ์

---

## สิ่งที่คุณต้องมี

ก่อนที่เราจะลงลึก, ตรวจสอบให้แน่ใจว่าคุณมี:

* Python 3.9 หรือใหม่กว่า (โค้ดทำงานบน 3.10+ ด้วย)  
* แพคเกจ OCR ที่สอดคล้องกับ API `ocr` ที่ใช้ด้านล่าง – ตัวอย่างเช่นไลบรารีสมมติ `simple-ocr` หรือ wrapper ใด ๆ ที่เปิดเผย `OcrEngine`, `Language`, และ `Image`  
* ไฟล์รูปภาพ (`.png`, `.jpg`, ฯลฯ) ที่มีข้อความที่คุณต้องการสกัดออก  
* เทอร์มินัลหรือ IDE ที่คุณสามารถรันสคริปต์ Python เพียงไฟล์เดียวได้

ถ้าคุณมีทั้งหมดแล้ว, เยี่ยม—มาเริ่มกันเลย

---

## Perform OCR on Image – Setting Up the Engine

สิ่งแรกที่คุณต้องทำคือสร้างอินสแตนซ์ของ OCR engine คิดว่า engine คือสมองที่ทำงานเบื้องหลัง; มันรู้วิธีแปลพิกเซลเป็นอักขระ

```python
# Import the OCR library – replace `ocr` with your actual package name
import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*ทำไมเรื่องนี้สำคัญ:* หากไม่มี engine จะไม่มีอะไรให้ประมวลผล วัตถุ `OcrEngine` จะเก็บการตั้งค่าต่าง ๆ ที่คุณจะปรับในภายหลัง, เช่น ภาษาและ confidence threshold

---

## Load Image for OCR – Preparing Your Scanned Form

เมื่อ engine มีแล้ว, เราต้อง **load image for OCR** วิธี `Image.load()` ของไลบรารีจะอ่านไฟล์จากดิสก์และแปลงเป็นรูปแบบภายในที่ engine เข้าใจได้

```python
# Step 2: Load the image you want to process
# Replace the path with the actual location of your noisy form
image_path = "YOUR_DIRECTORY/noisy_form.png"
image = ocr.Image.load(image_path)
```

> **เคล็ดลับ:** หากคุณทำงานกับ PDF, ให้แปลงแต่ละหน้าเป็นรูปภาพก่อน (เช่น ใช้ `pdf2image`). OCR engine รับเฉพาะ raster images เท่านั้น

---

## How to Use OCR Python – Configuring Language and Confidence

ส่วนใหญ่ OCR engine รองรับหลายภาษาและให้คุณกรองอักขระที่ confidence ต่ำ การตั้งค่าพารามิเตอร์เหล่านี้ตั้งแต่ต้นจะทำให้คุณได้ข้อความที่เชื่อถือได้เท่านั้น

```python
# Step 3: Choose language and set a confidence threshold
engine.language = ocr.Language.ENGLISH          # you can switch to FR, DE, etc.
engine.min_confidence = 85                     # accept only characters >85 % confidence
```

*ทำไมต้อง 85 %?* ในการปฏิบัติ, threshold ประมาณ 80‑90 % จะกำจัดข้อความไร้สาระส่วนใหญ่ในขณะที่ยังคงรักษาข้อความที่ดีไว้ ปรับตามคุณภาพของสแกนของคุณได้ตามต้องการ

---

## Extract Text from Scanned Form – Recognizing the Image

เมื่อ engine พร้อมและรูปภาพโหลดแล้ว, ถึงเวลาที่จะ **perform OCR on image** เมธอด `recognize()` จะคืนค่าอ็อบเจ็กต์ผลลัพธ์ที่มีข้อความที่สกัดออกและ (ถ้ามี) ข้อมูล bounding‑box

```python
# Step 4: Perform OCR recognition on the image
result = engine.recognize(image)
```

หากไลบรารีรองรับ, `result` อาจเปิดเผย `result.confidences` (รายการคะแนน confidence ต่ออักขระ) และ `result.words` (อ็อบเจ็กต์คำที่จัดโครงสร้าง) สำหรับคู่มือนี้เราจะเน้นที่ผลลัพธ์ข้อความธรรมดา

---

## OCR Recognize Image Python – Displaying Filtered Results

สุดท้าย, พิมพ์ข้อความที่กรองแล้ว สัญลักษณ์ที่ confidence ต่ำจะแสดงเป็นเครื่องหมายคำถาม (`?`) เพราะเราได้ตั้งค่า `min_confidence` เป็น 85 %

```python
# Step 5: Show the filtered text
print("Filtered text:")
print(result.text)
```

### ผลลัพธ์ที่คาดหวัง

```
Filtered text:
Name: John Doe
Date: 2023‑04‑15
Amount: $123.45
Signature: ?
```

สังเกตว่าลายเซ็นที่อ่านไม่ออกกลายเป็น `?` นั่นคือสิ่งที่ filter confidence ถูกออกแบบมาให้ทำ — ทำให้ผลลัพธ์สะอาดสำหรับการประมวลผลต่อไป

---

## Common Pitfalls and Pro Tips

| Issue | Why it Happens | Quick Fix |
|-------|----------------|-----------|
| **Blank output** | Image is too dark or low‑resolution. | Pre‑process with OpenCV: increase contrast, resize to ≥300 dpi. |
| **Garbage characters** | Wrong language selected. | Set `engine.language` to match the document (e.g., `ocr.Language.FRENCH`). |
| **Too many `?` symbols** | Confidence threshold too high. | Lower `engine.min_confidence` to 70‑80 % for noisy scans. |
| **Unicode errors** | Output contains non‑ASCII characters but console encoding is wrong. | Run `python -X utf8` or set `PYTHONIOENCODING=utf-8`. |

**Pro tip:** หากต้องการสกัดตาราง, ให้รัน pass ที่สองด้วย OCR engine ที่รับรู้ layout (เช่น Tesseract `--psm 6`) หลังจากกรองข้อความดิบแล้ว

---

## Full Script – Ready to Run

ด้านล่างเป็นสคริปต์สมบูรณ์ที่รวมทุกขั้นตอนที่อธิบายไว้ บันทึกเป็น `perform_ocr.py`, ปรับเส้นทางรูปภาพ, แล้วรัน `python perform_ocr.py`

```python
# perform_ocr.py
# -------------------------------------------------
# Complete Python script to perform OCR on image,
# load image for OCR, configure engine, and display
# filtered results. Works with any OCR library that
# follows the simple `ocr` API shown here.
# -------------------------------------------------

import ocr  # Replace with your actual OCR package name

def main():
    # 1️⃣ Create the engine
    engine = ocr.OcrEngine()

    # 2️⃣ Configure language and confidence
    engine.language = ocr.Language.ENGLISH
    engine.min_confidence = 85  # Only keep chars >85 % confidence

    # 3️⃣ Load the image (adjust the path)
    image_path = "YOUR_DIRECTORY/noisy_form.png"
    image = ocr.Image.load(image_path)

    # 4️⃣ Recognize the text
    result = engine.recognize(image)

    # 5️⃣ Print the filtered output
    print("Filtered text:")
    print(result.text)

if __name__ == "__main__":
    main()
```

รันสคริปต์และคุณจะเห็นข้อความที่กรองแล้วพิมพ์บนคอนโซล — ตรงตามที่ขั้นตอน **extract text from scanned form** สัญญาไว้

---

## What’s Next?

ตอนนี้คุณรู้วิธี **perform OCR on image** และ **extract text from scanned form**, คุณอาจอยากสำรวจต่อ:

* **Batch processing** – วนลูปผ่านไดเรกทอรีของรูปภาพเพื่อสร้าง CSV ของผลลัพธ์  
* **Post‑processing** – ใช้ regex หรือ spaCy เพื่อดึงฟิลด์เช่น วันที่, จำนวนเงิน, หรือ ID  
* **Integrations** – ส่งออกผล OCR ไปยังฐานข้อมูล, Google Sheets, หรือ REST API  

แนวคิดทั้งหมดนี้ใช้ฟังก์ชันหลักเดียวกันที่เราได้ครอบคลุม: โหลดรูปภาพ, ตั้งค่า engine, และเรียกเมธอด **OCR recognize image Python**

---

## Conclusion

เราได้เดินผ่านตัวอย่างเต็มรูปแบบที่พร้อมใช้งานในระดับ production เพื่อ **perform OCR on image** ด้วย Python ตั้งแต่ **loading image for OCR** ไปจนถึงการตั้งค่าภาษา, กำหนด confidence threshold, และสุดท้าย **extracting text from scanned form** ทุกขั้นตอนถูกอธิบายด้วยโค้ดและคำอธิบายที่ชัดเจน ตอนนี้คุณมีพื้นฐานที่มั่นคงเพื่อรับมือกับสถานการณ์ที่ซับซ้อนกว่า — ไม่ว่าจะเป็นงาน batch, รองรับหลายภาษา, หรือสกัดตาราง

ลองรันสคริปต์, ปรับ threshold, และดูเอกสารของคุณกลายเป็นค้นหาได้ในไม่กี่นาที มีคำถามหรือแบบฟอร์มที่ยากต่อการทำงาน? แสดงความคิดเห็นด้านล่างและมาช่วยกันแก้ไขกันเถอะ Happy coding!

![Perform OCR on image example](example.png "Perform OCR on image")


## What Should You Learn Next?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคในคู่มือนี้ แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอน‑ต่อ‑ขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการนำไปใช้ในโปรเจกต์ของคุณเอง

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}