---
category: general
date: 2026-03-26
description: จดจำข้อความจากภาพอย่างรวดเร็วโดยเรียนรู้วิธีโหลดภาพเพื่อทำ OCR และดึงข้อมูลจากพื้นที่เฉพาะ
  ตามคู่มือเชิงปฏิบัตินี้
draft: false
keywords:
- recognize text from image
- load image for ocr
- OCR region of interest
- extract text from ROI
- Python OCR library
- image preprocessing for OCR
language: th
og_description: จดจำข้อความจากภาพใน Python โดยโหลดภาพเพื่อทำ OCR กำหนดพื้นที่สนใจ
  และสกัดข้อความที่สะอาด เรียนรู้ขั้นตอนการทำงานทั้งหมด
og_title: แยกข้อความจากภาพ – คู่มือ OCR ด้วย Python อย่างครบถ้วน
tags:
- OCR
- Python
- Image Processing
title: แยกข้อความจากรูปภาพ – บทแนะนำ OCR ด้วย Python ทีละขั้นตอน
url: /th/python-java/general/recognize-text-from-image-step-by-step-python-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# จดจำข้อความจากรูปภาพ – คู่มือ Python OCR ฉบับเต็ม

เคยต้องการ **recognize text from image** แต่ไม่แน่ใจว่าจะเริ่มต้นอย่างไรไหม? บางทีคุณอาจมีแบบฟอร์มสแกน, ใบเสร็จ, หรือภาพหน้าจอและต้องการข้อความภายในกล่องเฉพาะ ข่าวดีคือด้วยไม่กี่บรรทัดของ Python คุณสามารถ **load image for OCR**, โฟกัสที่พื้นที่เดียว, แล้วดึงข้อความที่ต้องการออกมาได้โดยไม่ต้องคัดลอกด้วยมือ

ในบทเรียนนี้เราจะเดินผ่านกระบวนการทั้งหมด: โหลดภาพ, กำหนดพื้นที่สนใจ (ROI), รันเครื่องมือ OCR, และพิมพ์ผลลัพธ์ออกมา เมื่อเสร็จคุณจะสามารถฝังโค้ดสั้น ๆ นี้ลงในโปรเจกต์ใด ๆ ที่ต้องการดึงข้อความจากส่วนเฉพาะของภาพได้ ไม่ต้องใช้ pipeline การประมวลผลภาพที่ซับซ้อน เพียงแค่โค้ดที่อ่านง่ายและทำงานได้ทันที

## ข้อกำหนดเบื้องต้น

- ติดตั้ง Python 3.8+  
- แพคเกจ `ocr` (หรือไลบรารี OCR ที่เข้ากันได้) – ติดตั้งด้วย `pip install ocr-lib` (เปลี่ยนเป็นชื่อแพคเกจที่คุณใช้จริง)  
- รูปภาพ PNG/JPEG ที่มีแบบฟอร์มที่ต้องการอ่าน  
- ความคุ้นเคยพื้นฐานกับฟังก์ชันและคลาสของ Python  

หากคุณคุ้นเคยกับสิ่งเหล่านี้แล้ว ดีมาก—คุณสามารถข้ามไปได้ หากยังไม่พร้อม ให้หยิบกาแฟมาดื่มแล้วตรวจสอบให้แน่ใจว่าทุกอย่างพร้อมใช้งาน; ขั้นตอนต่อไปจะสมมติว่ามีพร้อมแล้ว

## ขั้นตอนที่ 1: สร้างอินสแตนซ์ของ OCR Engine – แกน “recognize text from image”

สิ่งแรกที่เราต้องการคืออ็อบเจกต์ที่รู้วิธีสื่อสารกับ OCR engine คิดว่าเป็นสมองที่จะทำการ **recognize text from image** ในภายหลัง

```python
import ocr  # Import the OCR library

# Initialize the engine
ocr_engine = ocr.OcrEngine()
```

> **ทำไมเรื่องนี้ถึงสำคัญ:** การเริ่มต้น engine เพียงครั้งเดียวทำให้คุณสามารถใช้การตั้งค่า (เช่น language packs) ซ้ำได้หลายภาพ ซึ่งช่วยเพิ่มประสิทธิภาพและทำให้โค้ดเป็นระเบียบ

## ขั้นตอนที่ 2: โหลดภาพสำหรับ OCR – นำรูปภาพเข้าสู่หน่วยความจำ

ตอนนี้เราจะ **load image for OCR** จริง ๆ ไลบรารีมีเมธอดสแตติกที่สะดวกซึ่งอ่านไฟล์และคืนค่าอ็อบเจกต์ที่ engine เข้าใจได้

```python
# Load the source image (replace the path with your own)
image_path = "YOUR_DIRECTORY/form.png"
ocr_engine.set_image(ocr.Imaging.Image.load(image_path))
```

> **เคล็ดลับ:** หากภาพของคุณมีขนาดใหญ่ ควรปรับขนาดให้เล็กลงก่อนโหลด ภาพที่เล็กลงทำให้ OCR เร็วขึ้นโดยไม่สูญเสียความแม่นยำสำหรับข้อความที่พิมพ์ทั่วไป

## ขั้นตอนที่ 3: กำหนด OCR Region of Interest (ROI)

บ่อยครั้งคุณไม่จำเป็นต้องประมวลผลทั้งหน้า—เพียงกล่องเฉพาะที่ผู้ใช้กรอกข้อมูล การกำหนด **OCR region of interest** บอก engine ให้ละเว้นส่วนอื่น ๆ ซึ่งช่วยลดสัญญาณรบกวนและเร่งการประมวลผล

```python
# Define ROI: (left, top, width, height) in pixels
region_of_interest = ocr.Rectangle(120, 340, 560, 90)

# Register the ROI with the engine
ocr_engine.add_region_of_interest(region_of_interest)
```

> **ทำไมต้องโฟกัสที่ ROI?**  
> - **Speed:** Engine สแกนพิกเซลน้อยลง  
> - **Accuracy:** กราฟิกพื้นหลังนอก ROI สามารถทำให้การจดจำอักขระสับสนได้  
> - **Simplicity:** คุณจะได้สตริงที่สะอาดตรงกับฟิลด์ที่ต้องการอย่างแม่นยำ

## ขั้นตอนที่ 4: รันกระบวนการ OCR – ช่วงเวลาที่รอคอย

เมื่อทุกอย่างพร้อม เราจึง **recognize text from image** ภายใน ROI ที่กำหนดไว้

```python
# Execute OCR on the specified region
ocr_result = ocr_engine.recognize()
```

หาก engine รองรับหลายพื้นที่ `ocr_result` จะเป็นรายการ; ในกรณี ROI เดียวของเราจะเป็นอ็อบเจกต์ง่าย ๆ ที่มีเมธอด `get_text()`

## ขั้นตอนที่ 5: ดึงและพิมพ์ข้อความ – รับผลลัพธ์สุดท้าย

ตอนนี้เราจะดึงสตริงธรรมดาจากอ็อบเจกต์ผลลัพธ์และแสดงออกมา นี่คือจุดที่คุณสามารถนำผลลัพธ์ไปบันทึกในฐานข้อมูล, ไฟล์ CSV, หรือโลจิกต่อไปได้

```python
# Retrieve the recognized text
extracted_text = ocr_result.get_text()

# Show the result
print("Text inside ROI:\n", extracted_text)
```

**ผลลัพธ์ที่คาดหวัง** (ตัวอย่างสำหรับฟิลด์ชื่อที่กรอกแล้ว):

```
Text inside ROI:
 John Doe
```

หาก OCR engine คืนค่าพื้นที่ว่างหรือการขึ้นบรรทัดใหม่เพิ่มเติม คุณสามารถทำความสะอาดด้วย `.strip()` หรือ regular expression

## การจัดการกับกรณีขอบทั่วไป

| Situation                              | What to Do                                                               |
|----------------------------------------|--------------------------------------------------------------------------|
| **Low‑resolution image**               | Upscale with `Pillow` (`Image.resize`) before loading.                  |
| **Skewed or rotated text**             | Apply a rotation correction (`ocr.Imaging.Image.rotate`).               |
| **Multiple languages**                | Set the language pack on the engine: `ocr_engine.set_language('eng+spa')`. |
| **No ROI defined**                     | Skip `add_region_of_interest`; the engine will process the whole image. |
| **Unexpected characters (e.g., commas)** | Post‑process the string: `extracted_text.replace(',', '')`.            |

เคล็ดลับเหล่านี้ทำให้ pipeline **load image for OCR** ของคุณแข็งแรงแม้แหล่งข้อมูลจะไม่สมบูรณ์

## ตัวอย่างทำงานเต็มรูปแบบ – คัดลอก, วาง, รัน

ด้านล่างเป็นสคริปต์เต็มที่คุณสามารถวางลงในไฟล์ `.py` แล้วรันได้ รวมการ import ทั้งหมด, การจัดการข้อผิดพลาด, และตัวช่วยเล็ก ๆ ที่ตรวจสอบว่าภาพมีอยู่จริงหรือไม่

```python
import os
import ocr

def recognize_text_from_image(image_path: str,
                              roi: tuple = (120, 340, 560, 90)):
    """
    Recognize text from a specific region of an image.

    Parameters
    ----------
    image_path : str
        Full path to the image file.
    roi : tuple
        (left, top, width, height) defining the region of interest.

    Returns
    -------
    str
        The extracted text, stripped of surrounding whitespace.
    """
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")

    # Step 1 – create engine
    engine = ocr.OcrEngine()

    # Step 2 – load image for OCR
    engine.set_image(ocr.Imaging.Image.load(image_path))

    # Step 3 – define ROI
    left, top, width, height = roi
    engine.add_region_of_interest(ocr.Rectangle(left, top, width, height))

    # Step 4 – run OCR
    result = engine.recognize()

    # Step 5 – extract text
    text = result.get_text().strip()
    return text


if __name__ == "__main__":
    # Adjust the path to point at your form image
    img_path = "YOUR_DIRECTORY/form.png"

    try:
        roi_text = recognize_text_from_image(img_path)
        print("Text inside ROI:\n", roi_text)
    except Exception as e:
        print("OCR failed:", e)
```

การรันสคริปต์นี้จะพิมพ์สตริงที่ทำความสะอาดจาก ROI ให้คุณได้ข้อมูลที่พร้อมใช้งานทันที

## สรุป

คุณมีวิธีที่ชัดเจนและครบวงจรเพื่อ **recognize text from image** โดยเริ่มจาก **load image for OCR**, กำหนด **OCR region of interest** อย่างแม่นยำ, แล้วสกัดข้อความที่สะอาด วิธีนี้ทำงานกับไลบรารี OCR ของ Python ใด ๆ ที่สอดคล้องกับรูปแบบที่แสดงข้างต้น และคุณสามารถขยายให้รองรับหลาย ROI, หลายภาษา, หรือขั้นตอนการเตรียมภาพล่วงหน้าได้ง่าย

ต่อไปคุณอาจสำรวจ:

- **image preprocessing for OCR** (thresholding, denoising) เพื่อเพิ่มความแม่นยำบนสแกนที่มีเสียงรบกวน  
- ใช้ผลลัพธ์ **extract text from ROI** เพื่อเติมข้อมูลลงใน pandas DataFrame สำหรับการวิเคราะห์ข้อมูลจำนวนมาก  
- เปลี่ยนไปใช้บริการ OCR บนคลาวด์ (Google Vision, Azure Computer Vision) เมื่อคุณต้องการความน่าเชื่อถือสูงในระดับสเกล

ลองใช้งาน ปรับพิกัดสี่เหลี่ยมให้ตรงกับฟอร์มของคุณเอง แล้วดูการทำงานอัตโนมัติของคุณทำงานอย่างไร ขอให้เขียนโค้ดสนุกนะ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}