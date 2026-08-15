---
category: general
date: 2026-03-26
description: เรียนรู้วิธีการหมุนภาพและทำ OCR ด้วย Python คู่มือนี้ยังแสดงวิธีการเตรียมภาพสำหรับ
  OCR และสกัดข้อความจากภาพอย่างมีประสิทธิภาพ
draft: false
keywords:
- how to rotate image
- how to perform ocr
- preprocess image for ocr
- recognize text from image
- how to extract text from image
language: th
og_description: วิธีหมุนภาพให้ถูกต้องแล้วจดจำข้อความจากภาพด้วย Aspose OCR. ทำตามบทแนะนำขั้นตอนต่อขั้นตอนนี้เพื่อเตรียมภาพสำหรับ
  OCR และดึงข้อความจากภาพ.
og_title: วิธีหมุนรูปภาพและทำ OCR – คู่มือ Python ฉบับสมบูรณ์
tags:
- Aspose
- Python
- Image Processing
- OCR
title: วิธีหมุนรูปภาพและทำ OCR ด้วย Aspose ใน Python
url: /th/python-java/general/how-to-rotate-image-and-perform-ocr-with-aspose-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีการหมุนภาพและทำ OCR ด้วย Aspose ใน Python

เคยสงสัย **วิธีการหมุนภาพ** เพื่อให้เครื่อง OCR สามารถอ่านข้อความได้จริงหรือไม่? บางครั้งคุณอาจสแกนแบบฟอร์มแล้วได้ภาพที่เอียง sideways หรือการจับภาพด้วยกล้องที่หมุน 90° ตามเข็มนาฬิกา ในกรณีนั้นข้อความอาจดูปกติต่อสายตามนุษย์ แต่เครื่อง OCR จะมองเป็นความยุ่งยาก ข่าวดีคือ การแก้ไขทิศทาง การครอปส่วนที่ต้องการ และการดึงข้อความออกมานั้นทำได้ง่ายดายด้วยไม่กี่บรรทัดของ Python และไลบรารี Aspose

ในบทแนะนำนี้เราจะเดินผ่านขั้นตอนทั้งหมด: ตั้งแต่การโหลดไฟล์ TIFF ที่หมุนแล้ว, แก้ไขทิศทาง, **เตรียมภาพสำหรับ OCR**, และสุดท้าย **จดจำข้อความจากภาพ**. เมื่อเสร็จสิ้นคุณจะรู้ **วิธีทำ OCR** บนภาพใด ๆ และสามารถ **ดึงข้อความจากไฟล์ภาพ** ได้อย่างมั่นใจ

## สิ่งที่คุณต้องมี

- Python 3.8+ (โค้ดทำงานกับเวอร์ชันล่าสุดทั้งหมด)
- แพ็กเกจ `asposeocrjava` และ `asposeimaging` ติดตั้งผ่าน `pip`
- ตัวอย่างภาพที่ต้องการหมุน (เช่น `rotated_form.tif`)
- ความสนใจเล็กน้อยเกี่ยวกับการประมวลผลภาพ

ไม่ต้องใช้เฟรมเวิร์กหนัก ๆ—แค่สองแพ็กเกจของ Aspose และโค้ด Python เล็กน้อย

---

## ขั้นตอนที่ 1: ติดตั้งแพ็กเกจ Aspose (วิธีทำ OCR)

ก่อนที่เราจะ **หมุนภาพ** หรือ **จดจำข้อความจากภาพ** เราต้องมีไลบรารีที่ทำงานหนักจริง ๆ

```bash
pip install asposeocrjava asposeimaging
```

> **เคล็ดลับ:** หากคุณอยู่หลังพร็อกซีขององค์กร ให้เพิ่ม `--proxy http://proxy:port` ลงในคำสั่ง. แพ็กเกจเหล่านี้เป็นเพียง wrapper ของ Python รอบคอร์ Aspose .NET/Java จึงมักติดตั้งได้ทันที

---

## ขั้นตอนที่ 2: โหลดไฟล์ต้นฉบับและหมุนมัน – ขั้นตอนหลัก “วิธีการหมุนภาพ”

```python
from asposeocrjava import OcrEngine, Rectangle
from asposeimaging import Image, RotateFlipType

# Load the original, incorrectly oriented image
source_image = Image.load("YOUR_DIRECTORY/rotated_form.tif")

# Rotate 90° clockwise – this fixes the orientation for OCR
rotated_image = source_image.rotate_flip(RotateFlipType.ROTATE_90_CLOCKWISE)
```

> **ทำไมต้องหมุน?** เครื่อง OCR ส่วนใหญ่สมมติว่าข้อความอ่านจากซ้ายไปขวาและจากบนลงล่าง. หากบิตแมพเอียงด้านข้าง เครื่องจะให้ผลลัพธ์เป็นอักขระไร้สาระหรือไม่มีผลลัพธ์เลย. การหมุนทำให้กริดพิกเซลสอดคล้องกับลำดับการอ่านที่คาดหวัง, เพิ่มความแม่นยำอย่างมาก

> **กรณีขอบ:** หากคุณไม่แน่ใจว่าภาพต้องการการหมุน 90°, 180° หรือ 270°, สามารถตรวจสอบ `source_image.width` กับ `source_image.height` หรือใช้แท็ก `exif` เพื่อหาทิศทาง. เมธอด `rotate_flip` ของ Aspose ยังรองรับ `ROTATE_180` และ `ROTATE_270_CLOCKWISE`

> **ตัวอย่างภาพ (ไม่บังคับ):**  
> ![how to rotate image example](/assets/rotate-demo.png "How to rotate image – before and after rotation")

---

## ขั้นตอนที่ 3: ครอปส่วนที่สนใจ – เตรียมภาพสำหรับ OCR

บ่อยครั้งคุณต้องการเพียงส่วนเล็กของหน้า—เช่นฟิลด์ลายเซ็นหรือบล็อกตัวเลข. การครอปช่วยกำจัดสัญญาณรบกวนและเร่งการ **ทำ OCR**.

```python
# Define the rectangle that encloses the text you care about
# (x=100, y=200, width=800, height=300) – adjust to your form
roi = Rectangle(100, 200, 800, 300)

# Crop the rotated image to that rectangle
roi_image = rotated_image.crop(roi)
```

> **ทำไมต้องครอป?** การลดขนาดภาพจะจำกัดพื้นที่การค้นหาของเครื่อง OCR, ลดผลบวกเท็จและลดเวลาในการประมวลผล. นอกจากนี้ยังช่วยกรณีที่ไฟล์ต้นฉบับมีลายน้ำหรือกราฟิกอื่น ๆ ที่อาจทำให้เครื่องสับสน

> **เคล็ดลับ:** หากต้องจัดการหลายฟิลด์ ให้ทำขั้นตอนครอปซ้ำด้วยสี่เหลี่ยมต่าง ๆ และเรียก OCR แยกแต่ละส่วน

---

## ขั้นตอนที่ 4: เริ่มต้น Engine OCR – แกน “วิธีทำ OCR”

```python
# Create an instance of the OCR engine
ocr_engine = OcrEngine()
```

> **เบื้องหลัง:** Aspose OCR ใช้การผสมผสานระหว่าง Tesseract และการวิเคราะห์ภาพแบบเฉพาะของบริษัท. การสร้างอ็อบเจกต์ Engine ครั้งเดียวและใช้ซ้ำสำหรับหลายภาพจะมีประสิทธิภาพกว่าการสร้างใหม่ทุกครั้ง

---

## ขั้นตอนที่ 5: ป้อนภาพที่ครอปแล้วและจดจำข้อความ – วิธีดึงข้อความจากภาพ

```python
# Set the cropped image as the input for OCR
ocr_engine.set_image(roi_image)

# Run the recognition process
result = ocr_engine.recognize()

# Extract the plain text
extracted_text = result.get_text()
print(extracted_text)
```

### ผลลัพธ์ที่คาดหวัง

หาก ROI มีข้อความ “Invoice #12345 – Paid”, คุณจะเห็นประมาณนี้:

```
Invoice #12345 – Paid
```

หาก OCR ทำงานยาก คุณอาจได้ช่องว่างเพิ่มหรืออักขระอ่านผิด (เช่น “Invo1ce #I2345 – Pa1d”). นั่นคือจุดที่เทคนิค **เตรียมภาพสำหรับ OCR** เช่น การปรับคอนทราสต์หรือการทำไบนารีไลเซชัน จะมีประโยชน์. Aspose มีฟิลเตอร์เพิ่มเติมที่คุณสามารถต่อเชื่อมก่อนขั้นตอน 5, แต่กระบวนการพื้นฐานด้านบนทำงานได้กับสแกนที่ค่อนข้างสะอาด

---

## ขั้นตอนที่ 6: ตัวเลือก – ปรับแต่งการตั้งค่า OCR (ขั้นสูง “วิธีทำ OCR”)

หากต้องการความแม่นยำสูงขึ้นสำหรับภาษาที่เฉพาะเจาะจงหรืออยากละเว้นอักขระบางตัว, คุณสามารถปรับ Engine ได้:

```python
# Example: Restrict recognition to English alphanumerics only
ocr_engine.get_recognition_settings().set_recognition_language("en")
ocr_engine.get_recognition_settings().set_characters_blacklist("!@#$%^&*()")
```

> **เมื่อใดใช้:** ใช้เมื่อตัวเอกสารมีสัญลักษณ์ตกแต่งจำนวนมากที่คุณไม่สนใจ. การทำ Blacklist จะลดการตรวจจับเท็จ

---

## สคริปต์เต็มแบบ End‑to‑End

รวมทุกอย่างเข้าด้วยกัน, นี่คือสคริปต์ที่พร้อมรันเพื่อ **หมุนภาพ**, **เตรียมภาพสำหรับ OCR**, และสุดท้าย **จดจำข้อความจากภาพ**:

```python
# -*- coding: utf-8 -*-
"""
Complete example: rotate, crop, and OCR an image with Aspose.
Author: Your Name
Date: 2026-03-26
"""

from asposeocrjava import OcrEngine, Rectangle
from asposeimaging import Image, RotateFlipType

def ocr_rotated_image(
    input_path: str,
    output_path: str = None,
    crop_rect: Rectangle = Rectangle(100, 200, 800, 300)
) -> str:
    """
    Loads an image, rotates it 90° clockwise, crops the region of interest,
    runs OCR, and returns the extracted text.

    Parameters
    ----------
    input_path : str
        Path to the original (possibly rotated) image file.
    output_path : str, optional
        If provided, saves the processed (rotated + cropped) image for inspection.
    crop_rect : Rectangle, optional
        Rectangle defining the ROI. Adjust to match your document layout.

    Returns
    -------
    str
        The plain text extracted from the ROI.
    """
    # Load and rotate
    src = Image.load(input_path)
    rotated = src.rotate_flip(RotateFlipType.ROTATE_90_CLOCKWISE)

    # Crop to region of interest
    roi = rotated.crop(crop_rect)

    # Optionally save the processed image for debugging
    if output_path:
        roi.save(output_path)

    # OCR
    engine = OcrEngine()
    engine.set_image(roi)
    result = engine.recognize()
    return result.get_text()

if __name__ == "__main__":
    text = ocr_rotated_image(
        "YOUR_DIRECTORY/rotated_form.tif",
        output_path="processed_roi.png"
    )
    print("=== Extracted Text ===")
    print(text)
```

การรันสคริปต์นี้จะพิมพ์ข้อความที่จดจำได้ลงคอนโซลและบันทึกภาพ ROI ที่ประมวลผลเป็น `processed_roi.png`. คุณสามารถเปิดไฟล์ PNG นี้เพื่อตรวจสอบว่าการหมุนและการครอปทำงานตามที่คาดหวังหรือไม่

---

## คำถามที่พบบ่อย & ข้อควรระวัง

| คำถาม | คำตอบ |
|----------|--------|
| **ถ้าภาพอยู่ในแนวตั้งแล้วจะทำอย่างไร?** | ขั้นตอนการหมุนเป็นแบบ idempotent—การหมุนภาพที่ถูกต้องแล้ว 90° จะทำให้ภาพเสีย, ดังนั้นควรตรวจสอบ `source_image.width` กับ `height` หรือใช้ข้อมูล EXIF ก่อนเรียก `rotate_flip` |
| **ผลลัพธ์ OCR มีการขึ้นบรรทัดใหม่เกินไป** | ใช้ `result.get_text().replace("\n", " ").strip()` เพื่อลบบรรทัดใหม่, หรือเปิดใช้ `ocr_engine.get_recognition_settings().set_remove_line_breaks(True)` |
| **สามารถประมวลผล PDF โดยตรงได้หรือไม่?** | ได้—Aspose Imaging สามารถโหลดหน้า PDF เป็นภาพ (`Image.load("file.pdf")`) แล้วทำตามขั้นตอนการหมุนและ OCR เดียวกัน |
| **มีวิธีประมวลผลหลายไฟล์พร้อมกันหรือไม่?** | ห่อ `ocr_rotated_image` ไว้ในลูปที่อ่านโฟลเดอร์, หรือใช้ `concurrent.futures` ของ Python เพื่อทำแบบขนาน |
| **จะจัดการกับภาษาที่ไม่ใช่อังกฤษอย่างไร?** | ตั้งค่าภาษาโดยใช้ `ocr_engine.get_recognition_settings().set_recognition_language("fr")` สำหรับภาษาฝรั่งเศส เป็นต้น |

---

## สรุป

เราได้ครอบคลุม **วิธีการหมุนภาพ** อย่างถูกต้อง, **เตรียมภาพสำหรับ OCR** ด้วยการครอป, และสุดท้าย **วิธีทำ OCR** เพื่อ **จดจำข้อความจากภาพ** และ **ดึงข้อความจากภาพ** ด้วยไลบรารี Python ของ Aspose. สคริปต์เต็มแสดงกระบวนการทำงานที่พร้อมใช้งานในสภาพแวดล้อมการผลิตที่คุณสามารถนำไปใส่ใน pipeline ใดก็ได้

หากต้องการก้าวต่อไป, ลองทดลองกับ:

- **การปรับปรุงภาพ** (คอนทราสต์, ไบนารีไลเซชัน) ก่อน OCR
- **การดึงหลาย ROI** สำหรับฟอร์มที่มีหลายฟิลด์
- **การประมวลผลเป็นชุด** ของโฟลเดอร์เอกสารสแกนทั้งหมด
- **การเชื่อมต่อ** กับระบบ downstream (เช่น ส่งข้อมูลที่ดึงมาใส่ฐานข้อมูล)

ปรับโค้ดให้เข้ากับกรณีการใช้งานของคุณได้ตามต้องการ, และขอให้สนุกกับการเขียนโค้ด! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}