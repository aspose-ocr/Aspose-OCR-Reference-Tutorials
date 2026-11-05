---
category: general
date: 2026-05-31
description: เรียนรู้วิธีใช้พื้นที่สนใจของ OCR เพื่อโหลดภาพสำหรับ OCR และดึงข้อความจากสี่เหลี่ยม
  เหมาะอย่างยิ่งสำหรับการจดจำจำนวนเงินในใบแจ้งหนี้
draft: false
keywords:
- ocr region of interest
- extract text from rectangle
- load image for ocr
- how to extract amount
- recognize text from invoice
language: th
og_description: เชี่ยวชาญการกำหนดพื้นที่สนใจของ OCR เพื่อโหลดภาพสำหรับ OCR ดึงข้อความจากสี่เหลี่ยมและจดจำข้อความจากใบแจ้งหนี้ในบทเรียนเดียว
og_title: OCR พื้นที่สนใจ – คู่มือ Python ทีละขั้นตอน
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to use OCR region of interest to load image for OCR and extract
    text from rectangle, perfect for recognizing amount on an invoice.
  headline: OCR Region of Interest – Extract Text from Rectangle in Python
  type: TechArticle
- description: Learn how to use OCR region of interest to load image for OCR and extract
    text from rectangle, perfect for recognizing amount on an invoice.
  name: OCR Region of Interest – Extract Text from Rectangle in Python
  steps:
  - name: Loads an invoice image from disk.
    text: Loads an invoice image from disk.
  - name: Marks a rectangular ROI where the total amount lives.
    text: Marks a rectangular ROI where the total amount lives.
  - name: Runs OCR only inside that ROI.
    text: Runs OCR only inside that ROI.
  - name: Prints the cleaned‑up amount string.
    text: Prints the cleaned‑up amount string.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: OCR พื้นที่สนใจ – ดึงข้อความจากสี่เหลี่ยมใน Python
url: /th/python-java/general/ocr-region-of-interest-extract-text-from-rectangle-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR Region of Interest – ดึงข้อความจากสี่เหลี่ยมใน Python

เคยสงสัยไหมว่า **ocr region of interest** ส่วนใดส่วนหนึ่งของใบแจ้งหนี้ที่สแกนแล้วโดยไม่ต้องส่งทั้งหน้าเข้าไปในเอนจิน? คุณไม่ได้เป็นคนแรกที่มองใบเสร็จที่เบลอแล้วคิดว่า “จะดึงจำนวนเงินที่อยู่ตรงมุมขวาล่างได้อย่างไร?” ข่าวดีคือคุณสามารถบอกไลบรารี OCR ว่าจะมองที่ไหนได้อย่างชัดเจน ทำให้ความเร็วและความแม่นยำเพิ่มขึ้นอย่างมาก

ในคู่มือนี้เราจะเดินผ่านตัวอย่างที่ทำงานได้เต็มรูปแบบซึ่งแสดงให้คุณเห็นวิธี **load image for OCR**, กำหนด **region of interest**, แล้ว **extract text from rectangle** เพื่อสุดท้าย **recognize text from invoice** และตอบคำถามคลาสสิก “วิธีดึงจำนวนเงิน” ไม่มีการอ้างอิงแบบคลุมเครือ—มีโค้ดที่เป็นรูปธรรม คำอธิบายที่ชัดเจน และเคล็ดลับระดับมืออาชีพที่คุณอยากรู้ตั้งแต่แรก

---

## สิ่งที่คุณจะสร้าง

เมื่อจบบทเรียนนี้คุณจะมีสคริปต์ Python เล็ก ๆ ที่ทำสิ่งต่อไปนี้:

1. โหลดรูปใบแจ้งหนี้จากดิสก์  
2. ทำเครื่องหมายสี่เหลี่ยม ROI ที่จำนวนเงินทั้งหมดอยู่  
3. รัน OCR เฉพาะภายใน ROI นั้น  
4. พิมพ์สตริงจำนวนเงินที่ทำความสะอาดแล้ว  

ทั้งหมดนี้ทำงานกับไลบรารี OCR ใด ๆ ที่รองรับ ROI—ในที่นี้เราจะใช้แพ็คเกจ `SimpleOCR` ที่เป็นตัวอย่างจำลองซึ่งทำหน้าที่คล้ายกับ Tesseract หรือ EasyOCR คุณสามารถเปลี่ยนเป็นแพ็คเกจอื่นได้; แนวคิดยังคงเหมือนเดิม

---

## ข้อกำหนดเบื้องต้น

- Python 3.8+ ติดตั้งแล้ว (`python --version` ควรแสดง ≥3.8)  
- แพ็คเกจ OCR ที่ติดตั้งผ่าน pip (เช่น `pip install simpleocr`)  
- รูปใบแจ้งหนี้ (PNG หรือ JPEG) อยู่ในโฟลเดอร์ที่คุณอ้างอิงได้  
- ความคุ้นเคยพื้นฐานกับฟังก์ชันและคลาสของ Python (ไม่มีอะไรซับซ้อน)

ถ้าคุณมีทั้งหมดแล้ว เยี่ยม—มาเริ่มกันเลย หากยังไม่มี ให้ดึงรูปภาพมาไว้ก่อน; ขั้นตอนต่อไปไม่ขึ้นกับเนื้อหาไฟล์จริง

---

## ขั้นตอนที่ 1: Load Image for OCR

สิ่งแรกที่ทุก workflow ของ OCR ต้องการคือบิตแมพเพื่ออ่าน Here’s how you do it with our `SimpleOCR` engine:

```python
# Step 1: Create an OCR engine instance and load the invoice image
from simpleocr import OcrEngine

# Initialize the engine (you can pass language settings here if needed)
ocr_engine = OcrEngine()

# Load the image – replace the path with yours
ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")
```

> **Pro tip:** ใช้เส้นทางแบบ absolute หรือ `os.path.join` เพื่อหลีกเลี่ยงข้อผิดพลาด “file not found” เมื่อรันสคริปต์จากไดเรกทอรีทำงานที่ต่างกัน

---

## ขั้นตอนที่ 2: Define OCR Region of Interest

แทนที่จะให้เอนจินสแกนทั้งหน้า เราบอกให้มัน *ตรง* ว่าจำนวนเงินอยู่ที่ไหน นี่คือขั้นตอน **ocr region of interest** และเป็นกุญแจสำคัญในการดึงข้อมูลที่เชื่อถือได้ โดยเฉพาะเมื่อเอกสารมีหัวหรือท้ายที่มีเสียงรบกวน

```python
# Step 2: Define the region of interest (ROI) where the amount appears
# Rectangle(x, y, width, height) – adjust these values for your layout
from simpleocr import Rectangle

amount_region = Rectangle(120, 340, 200, 40)   # x=120, y=340, w=200, h=40
ocr_engine.add_roi(amount_region)
```

ทำไมต้องใช้ตัวเลขเหล่านั้น? `x` และ `y` คือการออฟเซ็ตพิกเซลจากมุมบน‑ซ้าย ส่วน `width` และ `height` บรรยายขนาดของกล่อง หากคุณไม่แน่ใจ ให้เปิดรูปในโปรแกรมแก้ไขใด ๆ เปิด尺尺 (ruler) แล้วบันทึกพิกัด หลาย IDE ยังสามารถแสดงตำแหน่งเคอร์เซอร์ขณะชี้เม้าส์ได้อีกด้วย

---

## ขั้นตอนที่ 3: Extract Text from Rectangle

เมื่อ ROI ถูกตั้งค่าแล้ว เราขอให้เอนจิน **recognize text from invoice** แต่จำกัดไว้ที่สี่เหลี่ยมที่เรากำหนดไว้ การเรียกนี้จะคืนอ็อบเจ็กต์ผลลัพธ์ที่มักจะมีสตริงดิบ, คะแนนความเชื่อมั่น, และบางครั้งก็มี bounding boxes

```python
# Step 3: Perform OCR on the specified ROI
ocr_result = ocr_engine.recognize()
```

เบื้องหลัง `recognize()` จะวนลูปแต่ละ ROI, ครอบตัดสไลซ์นั้น, รันโมเดล OCR, แล้วต่อผลลัพธ์เข้าด้วยกัน นี่คือเหตุผลที่การกำหนด **extract text from rectangle** ที่กระชับสามารถลดเวลาในการประมวลผลหลายวินาทีสำหรับงานแบตช์

---

## ขั้นตอนที่ 4: How to Extract Amount – Clean the Output

OCR ไม่สมบูรณ์แบบ; คุณมักจะได้ช่องว่าง, line feed, หรืออักขระที่อ่านผิด (เช่น “S” กับ “5”) การใช้ `strip()` ร่วมกับ regex เล็ก ๆ มักจะเพียงพอสำหรับค่าการเงิน

```python
# Step 4: Clean and display the recognized amount
import re

raw_amount = ocr_result.text.strip()
# Simple regex to keep digits, commas, periods, and optional currency symbols
clean_amount = re.search(r'[\d,.]+', raw_amount)
if clean_amount:
    print("Amount:", clean_amount.group())
else:
    print("Could not locate a numeric amount in the ROI.")
```

> **Why this matters:** หากคุณต้องการส่งจำนวนเงินไปยังฐานข้อมูลหรือเกตเวย์การชำระเงิน คุณต้องการรูปแบบที่คาดเดาได้ การลบ whitespace และกรองอักขระที่ไม่ใช่ตัวเลขจะช่วยป้องกันข้อผิดพลาดในขั้นตอนต่อไป

---

## ขั้นตอนที่ 5: Recognize Text from Invoice – Full Script

รวมทุกอย่างเข้าด้วยกัน นี่คือสคริปต์เต็มที่พร้อมรัน บันทึกเป็น `extract_amount.py` แล้วเรียก `python extract_amount.py`

```python
# extract_amount.py
import re
from simpleocr import OcrEngine, Rectangle

def main():
    # Initialize OCR engine
    ocr_engine = OcrEngine()

    # Load the invoice image (adjust the path)
    ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")

    # Define ROI where the amount is located
    amount_region = Rectangle(120, 340, 200, 40)
    ocr_engine.add_roi(amount_region)

    # Run OCR on the ROI
    ocr_result = ocr_engine.recognize()

    # Clean and print the amount
    raw_amount = ocr_result.text.strip()
    match = re.search(r'[\d,.]+', raw_amount)
    if match:
        print("Amount:", match.group())
    else:
        print("Could not locate a numeric amount in the ROI.")

if __name__ == "__main__":
    main()
```

### ผลลัพธ์ที่คาดหวัง

```
Amount: 1,245.67
```

หาก ROI ไม่ตรงตำแหน่ง คุณอาจเห็นอย่างเช่น `Amount: 1245.6S`—สังเกตว่า “S” แปลก ๆ ปรับพิกัดสี่เหลี่ยมแล้วรันใหม่จนผลลัพธ์ดูสะอาด

---

## ปัญหาที่พบบ่อย & กรณีขอบ

| ปัญหา | สาเหตุ | วิธีแก้ |
|-------|--------|---------|
| **ROI เล็กเกินไป** | ข้อความจำนวนเงินถูกตัดขาด ทำให้การรับรู้ไม่ครบ | ขยาย `width`/`height` ประมาณ 10‑20 % แล้วทดสอบใหม่ |
| **DPI ไม่ถูกต้อง** | การสแกนความละเอียดต่ำ (≤150 dpi) ลดความแม่นยำของ OCR | รีแซมพล์ภาพเป็น 300 dpi ก่อนโหลด หรือขอให้สแกนที่ DPI สูงกว่า |
| **หลายสกุลเงิน** | Regex จับกลุ่มตัวเลขแรกซึ่งอาจเป็นหมายเลขใบแจ้งหนี้ | ปรับ regex ให้มองหาสัญลักษณ์สกุลเงิน (`$`, `€`, `£`) ก่อนตัวเลข |
| **ใบแจ้งหนี้หมุน** | OCR สมมติว่าข้อความอยู่ในแนวตั้ง; หน้าเอียงทำให้การรับรู้ล้มเหลว | ใช้การแก้ไขการหมุน (`ocr_engine.rotate(90)`) ก่อนเพิ่ม ROI |
| **สัญญาณรบกวนในพื้นหลัง** | เงาหรือตราประทับทำให้โมเดลสับสน | ทำการพรี‑โปรเซสด้วย threshold (`cv2.threshold`) หรือใช้ฟิลเตอร์ลดนอยส์ |

การจัดการกับกรณีขอบเหล่านี้ตั้งแต่เนิ่น ๆ จะช่วยคุณประหยัดเวลาการดีบักหลายชั่วโมงในภายหลัง

---

## เคล็ดลับระดับมืออาชีพสำหรับโปรเจกต์จริง

- **Batch Processing:** วนลูปโฟลเดอร์ใบแจ้งหนี้ทั้งหมด, คำนวณ ROI แบบไดนามิก (เช่น จากการตรวจจับเทมเพลต) แล้วบันทึกผลลัพธ์เป็น CSV  
- **Template Matching:** หากต้องจัดการหลายรูปแบบใบแจ้งหนี้ ให้เก็บแผนที่ JSON ของ `template_id → ROI coordinates` แล้วสลับ ROI ตามคลาสิฟายเออร์เทมเพลตอย่างรวดเร็ว  
- **Parallel Execution:** ใช้ `concurrent.futures.ThreadPoolExecutor` เพื่อรันหลายอินสแตนซ์ OCR พร้อมกัน—เหมาะกับไพพ์ไลน์แบค‑ออฟฟิศที่ต้องประมวลผลจำนวนมาก  
- **Confidence Filtering:** ผลลัพธ์ OCR ส่วนใหญ่มีคะแนนความเชื่อมั่น กรองผลลัพธ์ที่ต่ำกว่าเกณฑ์ (เช่น 85 %) แล้วทำเครื่องหมายให้ตรวจสอบด้วยมือ

---

## สรุป

เราได้ครอบคลุมทุกอย่างที่คุณต้องการเพื่อ **ocr region of interest**, **load image for OCR**, **extract text from rectangle**, และสุดท้าย **recognize text from invoice** เพื่อให้ตอบคำถามคลาสสิก **how to extract amount** สคริปต์สั้น ๆ นี้ยังยืดหยุ่นพอที่จะปรับให้เข้ากับรูปแบบเอกสาร, ภาษา, และแบ็ค‑เอนด์ OCR ต่าง ๆ

เมื่อคุณเชี่ยวชาญพื้นฐานแล้ว ลองขยาย workflow: เพิ่มการสแกนบาร์โค้ด, ผสานกับ PDF parser, หรือส่งจำนวนเงินที่ดึงได้ไปยัง API ระบบบัญชี ไม่จำกัดอะไรเลย และด้วย ROI ที่กำหนดอย่างชัดเจน คุณจะได้ผลลัพธ์ที่เร็วและสะอาดยิ่งขึ้นเสมอ

หากเจออุปสรรคใด ๆ คอมเมนต์ด้านล่างได้เลย—ขอให้ OCR สนุก!

![ocr region of interest example](https://example.com/ocr_roi_example.png "ocr region of interest example")


## คุณควรเรียนรู้อะไรต่อไป?

- [วิธีดึงข้อความจากรูปภาพโดยการเตรียมสี่เหลี่ยมใน OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [ดึงข้อความจากรูปภาพด้วย Java และ Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [ดึงข้อความจากรูปภาพ – การปรับแต่ง OCR ด้วย Aspose.OCR สำหรับ .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}