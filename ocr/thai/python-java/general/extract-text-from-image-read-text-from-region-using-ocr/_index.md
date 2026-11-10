---
category: general
date: 2026-07-05
description: ดึงข้อความจากรูปภาพด้วย Python OCR. เรียนรู้วิธีโหลดรูปภาพสำหรับ OCR,
  อ่านข้อความจากพื้นที่, และดึงข้อความจากใบแจ้งหนี้ด้วยไม่กี่บรรทัดของโค้ด.
draft: false
keywords:
- extract text from image
- read text from region
- load image for ocr
- extract text from invoice
- ocr on region
language: th
og_description: ดึงข้อความจากภาพด้วย Python OCR คู่มือนี้จะแสดงวิธีโหลดภาพสำหรับ OCR,
  อ่านข้อความจากพื้นที่, และดึงข้อความจากใบแจ้งหนี้อย่างรวดเร็ว.
og_title: ดึงข้อความจากภาพ – อ่านข้อความจากพื้นที่ด้วย OCR
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract text from image using Python OCR. Learn how to load image for
    OCR, read text from region, and extract text from invoice with a few lines of
    code.
  headline: Extract Text from Image – Read Text from Region Using OCR
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: ดึงข้อความจากภาพ – อ่านข้อความจากพื้นที่โดยใช้ OCR
url: /th/python-java/general/extract-text-from-image-read-text-from-region-using-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ดึงข้อความจากรูปภาพ – อ่านข้อความจากพื้นที่โดยใช้ OCR

เคยต้องการ **extract text from image** แต่ส่วนที่สำคัญมีแค่บางส่วน—เช่นจำนวนเงินรวมในใบแจ้งหนี้หรือไม่? คุณไม่ได้เป็นคนเดียว ในหลายโครงการจริง ๆ คุณจะพบว่าต้อง **read text from region** แทนการอ่านทั้งภาพทั้งหมด โชคดีที่ด้วยไม่กี่บรรทัดของ Python คุณสามารถโหลดภาพสำหรับ OCR กำหนดพื้นที่สนใจ (ROI) และดึงอักขระที่ต้องการออกมาได้อย่างแม่นยำ

ในบทเรียนนี้เราจะเดินผ่านตัวอย่างที่ทำงานได้เต็มรูปแบบซึ่งแสดงวิธี **load image for OCR** ตั้งค่า ROI และสุดท้าย **extract text from invoice** เมื่อจบคุณจะได้สคริปต์พร้อมใช้ที่ทำงานกับไลบรารี OCR ใด ๆ ที่รองรับการจดจำแบบพื้นที่

---

## สิ่งที่คุณต้องการ

- Python 3.8+ (โค้ดทำงานได้บน 3.10 ด้วย)  
- แพ็กเกจ OCR ที่เปิดเผยคลาส `OcrEngine` (สำหรับสาธิตเราจะใช้โมดูล `ocr` สมมติ; แทนที่ด้วย `pytesseract`, `easyocr` หรือไลบรารีใด ๆ ที่รองรับ ROI)  
- ตัวอย่างรูปภาพ—เช่น `invoice.png`—ที่มีข้อความพิมพ์ชัดเจน  
- ความคุ้นเคยพื้นฐานกับฟังก์ชันและคลาสของ Python (ไม่จำเป็นต้องมีพื้นฐาน deep learning)

หากคุณมีทั้งหมดแล้ว เยี่ยม—มาเริ่มกันเลย หากยังไม่มี ให้ดาวน์โหลด Python เวอร์ชันล่าสุดจาก python.org และติดตั้งแพ็กเกจ OCR ผ่าน `pip install your-ocr-lib`

![Extract text from image example](extract-text-from-image.png "Extract text from image – region based OCR demo")

*รูปด้านบนแสดงพื้นที่ (สี่เหลี่ยมสีแดง) ที่เราจะมุ่งเป้าเพื่อ **extract text from image**.*

---

## ขั้นตอนที่ 1: ติดตั้งและนำเข้าไลบรารี OCR

ก่อนอื่นให้แน่ใจว่าไลบรารี OCR พร้อมใช้งานในสภาพแวดล้อมของคุณ รูปแบบการนำเข้าด้านล่างทำงานกับแพ็กเกจส่วนใหญ่ที่เปิดเผยคลาสระดับสูง `OcrEngine`

```python
# Install the library (uncomment if you haven't yet)
# pip install your-ocr-lib

import ocr  # replace `ocr` with the actual module name, e.g., `import easyocr`
```

> **Pro tip:** หากคุณใช้ `pytesseract` คุณจะต้องติดตั้งไบนารี Tesseract แยกต่างหากและตั้งค่า `pytesseract.pytesseract.tesseract_cmd` ให้ชี้ไปยังตำแหน่งของมัน

---

## ขั้นตอนที่ 2: สร้าง OCR Engine และตั้งค่าภาษา

การสร้าง engine ทำได้ง่าย แต่การระบุภาษาอย่างชัดเจนจะเพิ่มความแม่นยำอย่างมาก โดยเฉพาะสำหรับใบแจ้งหนี้ที่มีตัวเลขและคำภาษาอังกฤษ

```python
# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Set the language to English – this is crucial for invoice text
ocr_engine.language = ocr.Language.ENGLISH
```

ทำไมต้องทำเช่นนี้? OCR engine ใช้โมเดลภาษาเพื่อทำนายอักขระ; การบอกให้คาดหวังภาษาอังกฤษช่วยลด false positives เช่นการอ่าน “0” เป็น “O”

---

## ขั้นตอนที่ 3: โหลดรูปภาพสำหรับ OCR

ตอนนี้เราจะ **load image for OCR** จริง ๆ ไลบรารีส่วนใหญ่รับพาธไฟล์หรืออ็อบเจ็กต์ Pillow ที่เป็นรูปภาพ ที่นี่เราใช้ตัวโหลดในตัวของไลบรารีเพื่อความง่าย

```python
# Load the source image that contains the text
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)   # replace with cv2.imread or PIL.Image.open if needed
```

ตรวจสอบให้แน่ใจว่าพาธชี้ไปยังไดเรกทรีที่ถูกต้อง; ความผิดพลาดทั่วไปคือลืมพาธสัมพัทธ์เมื่อสคริปต์รันจากโฟลเดอร์ทำงานที่ต่างกัน

---

## ขั้นตอนที่ 4: กำหนด Region of Interest (ROI)

การกำหนด ROI คือหัวใจของ **read text from region** คิดว่าเป็นการวาดสี่เหลี่ยมรอบส่วนของใบแจ้งหนี้ที่มีจำนวนเงินรวม

```python
# Define the ROI (left, top, width, height) in pixels
# Adjust these numbers to match your invoice layout
region_of_interest = ocr.Rectangle(100, 200, 400, 150)
```

- `left` และ `top` แทนพิกัด X และ Y ของมุมซ้ายบนของสี่เหลี่ยม  
- `width` และ `height` กำหนดขนาดของกล่อง  
- คุณสามารถทดลองค่าต่าง ๆ ด้วยโปรแกรมดูรูปที่แสดงพิกเซลได้

> **Why ROI matters:** การรัน OCR ทั้งหน้าเสีย CPU อย่างมากและมักทำให้เกิดสัญญาณรบกวนจากข้อความ ตาราง หรือกราฟิกที่ไม่เกี่ยวข้อง การโฟกัสที่พื้นที่ทำให้ผลลัพธ์สะอาดขึ้นและประมวลผลเร็วขึ้น

---

## ขั้นตอนที่ 5: ทำ OCR บนพื้นที่ที่กำหนด

เมื่อทุกอย่างพร้อม เราจะ **extract text from image**—แต่เฉพาะภายใน ROI ที่กำหนดไว้เท่านั้น

```python
# Recognize text only within the defined ROI
ocr_result = ocr_engine.recognize(image, region_of_interest)
```

เมธอด `recognize` จะคืนอ็อบเจ็กต์ที่มักจะมีสตริงดิบ, คะแนนความเชื่อมั่น, และบางครั้งบ็อกซ์ขอบของแต่ละคำ สำหรับงานของเราเราต้องการเพียงข้อความธรรมดาเท่านั้น

---

## ขั้นตอนที่ 6: แสดงผลข้อความที่ดึงออกมา

พิมพ์ผลลัพธ์และดูว่าเราได้อะไรบ้าง ขั้นตอนนี้สาธิต **extract text from invoice** ในสถานการณ์จริง

```python
# Output the extracted text
print("Text inside ROI:")
print(ocr_result.text)
```

### ผลลัพธ์ที่คาดหวัง

```
Text inside ROI:
Total Amount: $1,245.67
```

หากใบแจ้งหนี้ของคุณมีเลย์เอาต์แตกต่าง คุณจะเห็นข้อความใด ๆ ที่อยู่ภายในสี่เหลี่ยม—อาจเป็นหมายเลขใบแจ้งหนี้, วันที่, หรืออ้างอิง PO

---

## ขั้นตอนที่ 7: รวมทุกอย่างเป็นฟังก์ชันที่ใช้ซ้ำได้ (ทางเลือก)

เพื่อให้โซลูชันใช้ซ้ำได้กับหลายใบแจ้งหนี้ ให้ห่อหุ้มตรรกะไว้ในฟังก์ชัน ซึ่งยังแสดงตัวอย่าง **ocr on region** เป็นยูทิลิตี้ทั่วไป

```python
def extract_text_from_region(image_path: str,
                             left: int,
                             top: int,
                             width: int,
                             height: int,
                             language: str = "ENGLISH") -> str:
    """
    Load an image, define a ROI, and return the OCR result as plain text.
    
    Parameters
    ----------
    image_path : str
        Path to the image file.
    left, top, width, height : int
        Coordinates defining the region of interest.
    language : str, optional
        Language code for the OCR engine (default is ENGLISH).
    
    Returns
    -------
    str
        Recognized text inside the ROI.
    """
    # Initialise engine
    engine = ocr.OcrEngine()
    engine.language = getattr(ocr.Language, language.upper(), ocr.Language.ENGLISH)

    # Load image
    img = ocr.Image.load(image_path)

    # Define ROI
    roi = ocr.Rectangle(left, top, width, height)

    # Recognise text
    result = engine.recognize(img, roi)

    return result.text.strip()
```

คุณสามารถเรียกฟังก์ชันนี้กับใบแจ้งหนี้ใดก็ได้:

```python
total_text = extract_text_from_region(
    "invoices/2024-03-15.png",
    left=100, top=200, width=400, height=150
)
print("Extracted total:", total_text)
```

---

## ปัญหาที่พบบ่อยและวิธีหลีกเลี่ยง

| ปัญหา | ทำไมถึงเกิด | วิธีแก้ |
|-------|------------|--------|
| **ผลลัพธ์ว่าง** | ROI ไม่ได้ครอบคลุมข้อความจริง (พิกัดผิด) | ตรวจสอบค่าพิกเซลด้วยโปรแกรมแก้ไขรูป; เพิ่มการแสดงผลดีบักแบบภาพ |
| **อักขระแปลก** | ความละเอียดภาพต่ำหรือคอนทราสต์แย่ | ทำการพรี‑โปรเซสภาพ: แปลงเป็น grayscale, ใช้ thresholding (`cv2.threshold`) |
| **ภาษาไม่ถูกต้อง** | Engine ตั้งค่าเป็นภาษาที่ไม่มีชุดอักขระที่ต้องการ | ตั้งค่า `ocr_engine.language` ให้เป็น `ENGLISH` หรือ locale ที่เหมาะ |
| **ความช้า** | รัน OCR บนภาพขนาดใหญ่บ่อยครั้ง | ปรับขนาดภาพก่อนโหลด, หรือครอปเฉพาะ ROI ก่อนประมวลผล |

---

## ขยายตัวอย่าง: หลาย ROI

บางครั้งใบแจ้งหนี้มีหลายฟิลด์ที่ต้องการ—เช่น **extract text from invoice** สำหรับจำนวนเงินรวมและวันที่ใบแจ้งหนี้ คุณสามารถวนลูปผ่านรายการสี่เหลี่ยมได้:

```python
fields = {
    "total": ocr.Rectangle(100, 200, 400, 150),
    "date":  ocr.Rectangle(500, 200, 200, 80)
}

for name, rect in fields.items():
    txt = ocr_engine.recognize(image, rect).text.strip()
    print(f"{name.title()} → {txt}")
```

รูปแบบนี้ทำให้โค้ดของคุณสะอาดและง่ายต่อการเพิ่มพื้นที่ใหม่ในภายหลัง

---

## สรุป

เราได้อธิบายขั้นตอนทำงานแบบครบวงจรเพื่อ **extract text from image** ด้วย Python OCR โดยเน้นที่พื้นที่เฉพาะ ด้วยการ **load image for OCR**, กำหนด **region of interest** และเรียกใช้ engine คุณสามารถ **read text from region** ได้อย่างเชื่อถือได้—เหมาะสำหรับดึงยอดรวมจากใบแจ้งหนี้, วันที่จากใบเสร็จ, หรือข้อมูลตำแหน่งอื่น ๆ ที่ต้องการ  

อย่าลังเลที่จะทดลอง

## คุณควรเรียนรู้อะไรต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโปรเจกต์ของคุณ

- [ดึงข้อความจากรูปภาพด้วย Aspose OCR – คู่มือขั้นตอน](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [ดึงข้อความจากรูปภาพ – การปรับแต่ง OCR ด้วย Aspose.OCR สำหรับ .NET](/ocr/english/net/ocr-optimization/)
- [วิธีดึงข้อความจากรูปภาพโดยเตรียมสี่เหลี่ยมใน OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}