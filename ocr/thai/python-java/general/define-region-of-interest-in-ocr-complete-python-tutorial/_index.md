---
category: general
date: 2026-06-16
description: กำหนดพื้นที่สนใจใน OCR เพื่อดึงข้อความสเปนจากบัตรประจำตัว เรียนรู้วิธีโหลดภาพสำหรับ
  OCR และระบุ ROI อย่างมีประสิทธิภาพ
draft: false
keywords:
- define region of interest
- load image for ocr
- how to specify roi
- extract id card text
- extract spanish text image
language: th
og_description: กำหนดบริเวณที่สนใจใน OCR เพื่อดึงข้อความภาษาสเปนจากบัตรประจำตัว แนะนำขั้นตอนการโหลดภาพและการระบุ
  ROI.
og_title: กำหนดพื้นที่สนใจใน OCR – บทเรียน Python ฉบับเต็ม
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Define region of interest in OCR to extract Spanish text from ID cards.
    Learn how to load image for OCR and specify ROI efficiently.
  headline: Define region of interest in OCR – Complete Python Tutorial
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: กำหนดพื้นที่สนใจใน OCR – บทเรียน Python ฉบับสมบูรณ์
url: /th/python-java/general/define-region-of-interest-in-ocr-complete-python-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# กำหนดพื้นที่สนใจใน OCR – บทเรียน Python ฉบับสมบูรณ์

เคยสงสัยไหมว่าคุณจะ **define region of interest in OCR** อย่างไรเพื่อให้คุณอ่านเฉพาะส่วนของภาพที่ต้องการ? ในบทเรียนนี้เราจะพาคุณผ่านขั้นตอนนั้น รวมถึงแสดงวิธี **load image for OCR** และสกัดข้อความภาษาสเปนจากบัตรประจำตัวด้วยเพียงไม่กี่บรรทัดของ Python.  

หากคุณเคยจ้องมองสแกนที่มีสัญญาณรบกวนและคิดว่า “ต้องมีวิธีที่สะอาดกว่านี้ในการดึงฟิลด์ชื่อ” คุณอยู่ในที่ถูกต้อง. โดยตอนจบคุณจะสามารถดึงข้อความบัตรประจำตัวที่ต้องการโดยไม่ต้องเจอกับสิ่งรบกวนจากพื้นหลัง.

## สิ่งที่คุณจะได้เรียนรู้

- ทำไมคุณควร **define region of interest** ก่อนรัน OCR.  
- ขั้นตอนที่แม่นยำในการ **load image for OCR** ด้วย Python OCR wrapper ที่นิยม.  
- วิธี **how to specify ROI** ด้วยพิกเซลพิกัด.  
- วิธีการ **extract id card text** อย่างเชื่อถือได้ แม้แหล่งภาษาจะเป็นสเปน.  
- เคล็ดลับการจัดการกรณีขอบเช่นบัตรที่หมุนหรือสแกนที่คอนทราสต์ต่ำ.  

ไม่จำเป็นต้องมีความเชี่ยวชาญ OCR มาก่อน—เพียงมีสภาพแวดล้อม Python 3 ที่ทำงานได้และไฟล์ JPEG ของบัตรประจำตัวที่คุณต้องการทดสอบ

![Define region of interest illustration](placeholder.png){alt="ตัวอย่างการกำหนดพื้นที่สนใจที่แสดงสี่เหลี่ยมไฮไลท์บนภาพบัตรประจำตัว"}

## ขั้นตอนที่ 1: ติดตั้งและนำเข้าไลบรารี OCR

อันดับแรกคุณต้องการไลบรารีที่เปิดเผยคลาส `OcrEngine` คล้ายกับโค้ดตัวอย่างที่คุณเห็น สำหรับคู่มือนี้เราจะใช้แพคเกจสมมติ `ocr` แต่แนวคิดเดียวกันสามารถใช้กับ `pytesseract`, `easyocr` หรือ wrapper ใด ๆ ที่ให้คุณตั้งค่าภาษาและ ROI.

```bash
pip install ocr   # Replace with the actual package name you use
```

```python
# Import the library and any helper classes
import ocr
from ocr import Rectangle, Image
```

*เคล็ดลับ:* หากคุณใช้ `pytesseract` คลาส `Rectangle` จะกลายเป็นทูเพิลง่าย ๆ `(left, top, width, height)` ส่วนที่เหลือของกระบวนการยังคงเหมือนเดิม.

## ขั้นตอนที่ 2: โหลดภาพสำหรับ OCR

ตอนนี้เราจะ **load image for OCR**. เอนจินคาดหวังอ็อบเจ็กต์ `ocr.Image` ดังนั้นเราจึงชี้ไปที่ไฟล์ที่มีบัตรประจำตัว ตรวจสอบให้แน่ใจว่าเส้นทางเป็นแบบ absolute หรือ relative ต่อไดเรกทอรีทำงานของสคริปต์ของคุณ.

```python
# Create the OCR engine instance
engine = ocr.OcrEngine()

# Tell the engine which language we’re interested in – Spanish in this case
engine.language = ocr.Language.SPANISH

# Load the source image that contains the text to be recognized
engine.image = Image.load_from_file("YOUR_DIRECTORY/id-card.jpg")
```

หากภาพมีขนาดใหญ่ ควรปรับขนาดก่อน; เอนจิน OCR ทำงานเร็วขึ้นกับภาพที่กว้างต่ำกว่า 1500 px.

## ขั้นตอนที่ 3: วิธีระบุ ROI (Define Region of Interest)

นี่คือหัวใจของบทเรียน: **how to specify ROI**. พื้นที่สนใจคือสี่เหลี่ยมที่บอกเอนจิน OCR ว่า “ให้ดูเฉพาะภายในขอบพิกเซลเหล่านี้” คิดว่าเป็นการวาดกล่องรอบฟิลด์ชื่อบนบัตรประจำตัว.

```python
# Define the region of interest – left, top, width, height (all in pixels)
engine.region_of_interest = Rectangle(
    left=120,   # X‑coordinate of the left edge
    top=80,     # Y‑coordinate of the top edge
    width=340,  # Width of the box
    height=200  # Height of the box
)
```

ทำไมถึงใช้ตัวเลขเหล่านั้น? ในภาพตัวอย่างของเรา ชื่ออยู่ประมาณ 120 px จากขอบซ้ายและ 80 px จากด้านบน ปรับค่าเหล่านี้ให้ตรงกับเลย์เอาต์ของบัตรที่คุณกำลังประมวลผล.  

*กรณีขอบ:* หากบัตรหมุน 90° ให้สลับ `width` กับ `height` และปรับ `left`/`top` ตามนั้น หรือทำการหมุนภาพล่วงหน้าด้วย Pillow ก่อนส่งให้เอนจิน.

## ขั้นตอนที่ 4: ทำ OCR ภายใน ROI

เมื่อกำหนด ROI แล้ว เอนจินจะละเลยทุกอย่างนอกสี่เหลี่ยม นี้ไม่เพียงทำให้การประมวลผลเร็วขึ้น แต่ยังลดผลบวกเท็จจากกราฟิกพื้นหลัง.

```python
# Run OCR only inside the defined ROI
roi_result = engine.recognize()
```

การเรียก `recognize()` จะคืนค่าอ็อบเจ็กต์ที่บรรจุข้อความที่รับรู้, คะแนนความมั่นใจ, และกล่องขอบเขตสำหรับแต่ละคำ.

## ขั้นตอนที่ 5: สกัดข้อความบัตรประจำตัว (และตรวจสอบผลลัพธ์สเปน)

สุดท้าย เรา **extract id card text** จากผลลัพธ์ ROI และพิมพ์ออกมา เนื่องจากเราได้ตั้งค่าภาษาเป็นสเปนก่อนหน้า เอนจิน OCR จะใช้พจนานุกรมเฉพาะภาษา ทำให้ความแม่นยำสูงขึ้นสำหรับอักขระที่มีสำเนียงเช่น “ñ” หรือ “á”.

```python
# Output the recognized text from the ROI
print("ROI text:", roi_result.text)
```

### ผลลัพธ์ที่คาดหวัง

```
ROI text: JUAN PÉREZ GARCÍA
```

หากคุณเห็นอักขระเสียหาย ตรวจสอบอีกครั้งว่าภาพเป็นภาษาสเปนจริง ๆ และไฟล์ข้อมูลภาษาของไลบรารี OCR ได้ถูกติดตั้งแล้ว.

## ข้อผิดพลาดทั่วไป & วิธีหลีกเลี่ยง

| อาการ | สาเหตุที่เป็นไปได้ | วิธีแก้ |
|---------|--------------|-----|
| สตริงว่างถูกส่งคืน | ROI ไม่ตัดกับข้อความใด | ตรวจสอบพิกัดด้วยโปรแกรมดูภาพ; ใช้ `engine.debug_draw_roi()` หากมี. |
| มีอักขระขยะจำนวนมาก | แพ็คภาษาผิด | ติดตั้งใหม่ข้อมูลภาษาสเปนหรือสลับเป็น `ocr.Language.AUTO`. |
| คะแนนความมั่นใจต่ำ | ภาพเบลอหรือคอนทราสต์ต่ำ | ทำการประมวลผลล่วงหน้าด้วย OpenCV – ใช้ `cv2.GaussianBlur` และ `cv2.threshold`. |
| OCR ทำงานบนภาพทั้งหมดแม้มี ROI | ใช้เวอร์ชันไลบรารีเก่า | อัปเกรดเป็นแพคเกจ `ocr` ล่าสุด; เวอร์ชันเก่ามักละเลย ROI. |

## ขยายตัวอย่าง: หลาย ROI

บางครั้งคุณต้องดึงหลายฟิลด์ (เช่น ชื่อและหมายเลขบัตร). รูปแบบยังคงเหมือนเดิม: เปลี่ยน `engine.region_of_interest` แล้วเรียก `recognize()` อีกครั้ง.

```python
# ROI for the ID number (different coordinates)
engine.region_of_interest = Rectangle(120, 300, 340, 80)
id_result = engine.recognize()
print("ID Number:", id_result.text)
```

คุณยังสามารถประมวลผลเป็นชุดของรายการสี่เหลี่ยมได้หากไลบรารีรองรับ ซึ่งช่วยลดการติดต่อกับเอนจิน OCR.

## สคริปต์ทำงานเต็มรูปแบบ

รวมทุกอย่างเข้าด้วยกัน นี่คือสคริปต์พร้อมรันที่ **defines region of interest**, **loads image for OCR**, และ **extracts Spanish text** จากบัตรประจำตัว.

```python
import ocr
from ocr import Rectangle, Image

def extract_name_from_id(image_path):
    """
    Loads an image, defines a ROI around the name field,
    runs OCR in Spanish, and returns the recognized text.
    """
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.SPANISH
    engine.image = Image.load_from_file(image_path)

    # Adjust these numbers to match your card layout
    engine.region_of_interest = Rectangle(left=120, top=80, width=340, height=200)

    result = engine.recognize()
    return result.text.strip()

if __name__ == "__main__":
    name = extract_name_from_id("YOUR_DIRECTORY/id-card.jpg")
    print("Extracted Name:", name)
```

รันสคริปต์และคุณควรเห็นชื่อพิมพ์บนคอนโซล เปลี่ยนค่าสี่เหลี่ยมเพื่อเจาะจงฟิลด์อื่น ๆ แล้วคุณจะมียูทิลิตี้ที่ใช้ซ้ำได้สำหรับเอกสารประเภทบัตรประจำตัวใด ๆ

## ขั้นตอนต่อไป

- **Batch processing:** วนลูปผ่านโฟลเดอร์ของบัตรประจำตัวและบันทึกชื่อที่สกัดได้แต่ละรายการลงไฟล์ CSV.  
- **Language detection:** ให้ผู้ใช้เลือกภาษาตามต้องการ; `ocr.Language.AUTO` มีประโยชน์.  
- **Post‑processing:** ใช้รูปแบบ regex เพื่อล้างข้อผิดพลาด OCR ที่พบบ่อย (เช่น แทนที่ “0” ด้วย “O” เมื่อปรากฏในชื่อ).  

ด้วยการเชี่ยวชาญวิธี **define region of interest** คุณได้เปิดวิธีที่ทรงพลังในการ **extract id card text** อย่างรวดเร็วและแม่นยำ โดยเฉพาะเมื่อจัดการกับเอกสารภาษาสเปน.

### TL;DR

เราได้แสดงวิธี **define region of interest in OCR**, **load image for OCR**, และ **how to specify ROI** เพื่อ **extract spanish text image** จากบัตรประจำตัว ตัวอย่างเต็มทำงานภายในไม่ถึงหนึ่งนาทีและสามารถปรับให้เข้ากับเลย์เอาต์ใด ๆ ด้วยการปรับพิกัดเล็กน้อย ลองดู ปรับสี่เหลี่ยม และดู OCR ทำงานเหมือนเลเซอร์.

เขียนโค้ดให้สนุก!

## คุณควรเรียนรู้อะไรต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดซึ่งต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานแบบอื่นในโครงการของคุณ.

- [วิธีสกัดข้อความจากภาพโดยการเตรียมสี่เหลี่ยมใน OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [สกัดข้อความภาพด้วย C# พร้อมการเลือกภาษาโดยใช้ Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [สกัดข้อความจากภาพ – การเพิ่มประสิทธิภาพ OCR ด้วย Aspose.OCR สำหรับ .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}