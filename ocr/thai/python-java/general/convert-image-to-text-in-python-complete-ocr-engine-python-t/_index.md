---
category: general
date: 2026-07-05
description: แปลงรูปภาพเป็นข้อความด้วย Python OCR – ตัวอย่าง Python OCR ขั้นตอนต่อขั้นตอนที่แสดงวิธีดึงข้อความจากรูปภาพและจดจำข้อความจากไฟล์
  JPG.
draft: false
keywords:
- convert image to text
- extract text from image
- python ocr example
- ocr engine python
- recognize text from jpg
language: th
og_description: แปลงรูปภาพเป็นข้อความด้วย Python OCR. ทำตามตัวอย่าง Python OCR นี้เพื่อดึงข้อความจากรูปภาพและจดจำข้อความจากไฟล์
  JPG ภายในไม่กี่นาที.
og_title: แปลงรูปภาพเป็นข้อความด้วย Python – คู่มือเครื่องมือ OCR ฉบับเต็ม
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Convert image to text with Python OCR – a step‑by‑step python ocr example
    that shows how to extract text from image and recognize text from jpg.
  headline: Convert Image to Text in Python – Complete OCR Engine Python Tutorial
  type: TechArticle
tags:
- ocr
- python
- image-processing
- text-extraction
title: แปลงรูปภาพเป็นข้อความใน Python – บทเรียน Python การทำ OCR Engine อย่างครบถ้วน
url: /th/python-java/general/convert-image-to-text-in-python-complete-ocr-engine-python-t/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# แปลงรูปภาพเป็นข้อความใน Python – บทเรียนเต็มของ OCR Engine ด้วย Python

เคยต้องการ **แปลงรูปภาพเป็นข้อความ** แต่ไม่แน่ใจว่าจะใช้ไลบรารีไหน? คุณไม่ได้เป็นคนเดียว—นักพัฒนาหลายคนเจออุปสรรคนี้เมื่อลองดึงอักขระจากใบเสร็จสแกนหรือรูปป้าย. ข่าวดี? ระบบ OCR ของ Python ทำให้การทำงานนี้ง่ายเกือบไม่มีปัญหา.

ใน **python ocr example** นี้ เราจะเดินผ่านสถานการณ์จริง: คุณมีไฟล์ JPEG ที่มีอักขระ Cyrillic และต้องการ **extract text from image** อย่างเชื่อถือได้. เมื่อจบคุณจะรู้วิธี **recognize text from jpg** ไฟล์, ทำไมแต่ละขั้นตอนสำคัญ, และวิธีปรับโค้ดสำหรับภาษาอื่นหรือรูปแบบภาพอื่น.

## สิ่งที่คุณต้องการ

* ติดตั้ง Python 3.8+ (รุ่นล่าสุดที่เสถียรที่สุดเป็นที่แนะนำ)
* มีการเชื่อมต่ออินเทอร์เน็ตที่ทำงานได้เพื่อทำการติดตั้งแพคเกจ OCR
* ไฟล์รูปภาพ (เช่น `cyrillic_sample.jpg`) ที่มีข้อความที่คุณต้องการดึง
* ตัวเลือกที่สะดวก: สร้าง virtual environment เพื่อจัดการ dependencies อย่างเป็นระเบียบ

ไม่มี dependencies ระดับ OS ที่หนักหน่วง, ไม่มีเครื่องมือ build ที่ซับซ้อน—แค่คำสั่ง pip ไม่กี่คำสั่งและบรรทัดโค้ดไม่กี่บรรทัด

## ขั้นตอนที่ 1: ติดตั้งแพคเกจ OCR Engine สำหรับ Python

สิ่งแรกที่คุณต้องทำคือหา OCR engine ที่ทำงานได้ดีกับ Python. สำหรับบทเรียนนี้เราจะใช้แพคเกจ `ocr` ที่เป็นตัวอย่างเพราะ API ของมันคล้ายกับหลายไลบรารีจริง (เช่น `pytesseract` หรือ `easyocr`). ติดตั้งด้วย:

```bash
pip install ocr
```

> **ทำไมขั้นตอนนี้สำคัญ:** การติดตั้งแพคเกจจะดึงไบนารีเนทีฟและไฟล์ข้อมูลภาษาที่ทำงานหนักจริง ๆ. หากข้ามขั้นตอนนี้จะทำให้เกิด `ImportError` ทันทีที่คุณพยายาม `import ocr`.

## ขั้นตอนที่ 2: นำเข้าโมดูลและตั้งค่าสภาพแวดล้อม

เมื่อไลบรารีอยู่บนเครื่องของคุณแล้ว ให้นำเข้าชิ้นส่วนที่จำเป็น. เราจะตั้งค่า logging เพื่อให้คุณเห็นว่า engine ทำอะไรอยู่เบื้องหลัง—มีประโยชน์เมื่อคุณต่อมาจะ **extract text from image** ไฟล์ที่ไม่สะอาดสมบูรณ์.

```python
import ocr
import logging

# Enable debug output (optional but recommended for first runs)
logging.basicConfig(level=logging.INFO)
```

> **เคล็ดลับ:** หากคุณทำงานใน Jupyter notebook, คุณอาจต้องการตั้งค่า `logging.getLogger().setLevel(logging.DEBUG)` เพื่อดูรายละเอียดเพิ่มเติม.

## ขั้นตอนที่ 3: สร้างอินสแตนซ์ของ OCR Engine

การสร้าง engine เป็นหัวใจหลักของ workflow **ocr engine python** ใด ๆ. คิดว่าเป็นการเปิดไฟในห้องมืด; หากไม่มีมัน pipeline ส่วนอื่นจะมองไม่เห็นอะไร.

```python
# Step 3: Instantiate the OCR engine
ocr_engine = ocr.OcrEngine()
```

> **ทำไมขั้นตอนนี้สำคัญ:** วัตถุ `OcrEngine` เก็บการตั้งค่าเช่น language packs, ตัวเลือกการ preprocessing, และ flag การเร่งความเร็วด้วยฮาร์ดแวร์. การเปลี่ยนแปลงใด ๆ หลังจากนี้จะส่งผลต่อการจดจำทั้งหมดต่อไป.

## ขั้นตอนที่ 4: เลือกภาษาที่เหมาะสม – รองรับ Cyrillic

หากคุณทำงานกับข้อความ Cyrillic (หรือสคริปต์ที่ไม่ใช่ Latin ใด ๆ) คุณต้องบอก engine ว่าจะโหลด language model ใด. มิฉะนั้นคุณจะได้ผลลัพธ์เป็นข้อความเสียหายหรือแย่กว่าเป็นสตริงว่าง.

```python
# Step 4: Set language to Cyrillic (enables Cyrillic block support)
ocr_engine.language = ocr.Language.CYRILLIC
```

> **กรณีพิเศษ:** บาง engine ต้องให้คุณดาวน์โหลดข้อมูลภาษาแยกต่างหาก. หากคุณเห็นข้อผิดพลาดเช่น `LanguageDataNotFound`, ให้รัน `ocr.download_language('CYRILLIC')` ก่อนกำหนดภาษา.

## ขั้นตอนที่ 5: โหลดภาพที่คุณต้องการแปลงเป็นข้อความจาก

นี่คือจุดที่วลี **convert image to text** เริ่มทำงานจริง. OCR engine ทำงานกับอ็อบเจ็กต์ `Image`, ไม่ใช่เส้นทางไฟล์ดิบ, ดังนั้นเราต้องห่อ JPEG ก่อน.

```python
# Step 5: Load the image containing the text
cyrillic_image = ocr.Image.load("YOUR_DIRECTORY/cyrillic_sample.jpg")
```

> **ทำไมสิ่งนี้สำคัญ:** การโหลดภาพทำให้ engine สามารถตรวจสอบขนาด, ความลึกสี, และ DPI. คุณสมบัติเหล่านี้ส่งผลต่อความสามารถของ engine ในการ **recognize text from jpg** ไฟล์.

## ขั้นตอนที่ 6: จดจำข้อความ – แกนหลักของ Python OCR Example

ตอนนี้เราขอให้ engine ทำในสิ่งที่มันสร้างมา: แปลงพิกเซลเป็นอักขระ. เมธอด `recognize` จะคืนวัตถุผลลัพธ์ที่เก็บสตริงที่ดึงออกมา, คะแนนความเชื่อมั่น, และ bounding boxes.

```python
# Step 6: Run OCR and capture the result
ocr_result = ocr_engine.recognize(cyrillic_image)
```

> **สิ่งที่คุณได้รับกลับ:** `ocr_result.text` เป็นสตริง Python ธรรมดาที่คงการขึ้นบรรทัดใหม่. หากต้องการตำแหน่งระดับคำ, สำรวจ `ocr_result.boxes`.

## ขั้นตอนที่ 7: แสดงข้อความที่จดจำได้ – ตรวจสอบความสำเร็จของการ **convert image to text** ของคุณ

วิธีที่ง่ายที่สุดเพื่อดูว่าคุณได้ **convert image to text** สำเร็จหรือไม่คือการพิมพ์ผลลัพธ์. ในแอปพลิเคชันจริงคุณอาจบันทึกลงฐานข้อมูลหรือไฟล์ข้อความแทน.

```python
# Step 7: Print the extracted text
print("=== OCR OUTPUT ===")
print(ocr_result.text)
```

### ผลลัพธ์ที่คาดหวัง

สมมติว่า `cyrillic_sample.jpg` มีวลี “Привет, мир!” คอนโซลจะแสดง:

```
=== OCR OUTPUT ===
Привет, мир!
```

หากผลลัพธ์ดูว่างเปล่าหรือไม่มีความหมาย, ตรวจสอบการตั้งค่าภาษาและคุณภาพของภาพอีกครั้ง. ภาพเบลอหรือคอนทราสต์ต่ำมักทำให้ผลลัพธ์ **extract text from image** แย่.

## การจัดการกับปัญหาที่พบบ่อย

| ปัญหา | สาเหตุ | วิธีแก้เร็ว |
|---------|----------------|-----------|
| **สตริงว่าง** | โมเดลภาษาไม่ได้โหลดหรือภาพมืดเกินไป | ตรวจสอบให้ `ocr_engine.language` ตรงกับสคริปต์; เพิ่มคอนทราสต์ของภาพด้วย `ocr.Image.adjust_contrast()` |
| **อักขระเสีย** | ภาษาไม่ถูกต้องหรือสคริปต์ผสมกัน | ตั้งค่า `ocr_engine.language = ocr.Language.MULTI` หรือทำสองรอบ (Latin แล้ว Cyrillic) |
| **ประสิทธิภาพช้าเมื่อประมวลผลชุดใหญ่** | Engine ประมวลผลภาพแบบต่อเนื่อง | เปิดใช้งาน multi‑threading: `ocr_engine.set_threads(4)` |
| **การรั่วไหลของหน่วยความจำ** | ไม่ได้ปล่อยทรัพยากรภาพ | เรียก `cyrillic_image.close()` หลังจากการจดจำ |

> **เคล็ดลับ:** สำหรับการประมวลผลเป็นชุด, ห่อ loop การจดจำด้วยบล็อก `try/except` เพื่อจับข้อยกเว้น `ocr.EngineError` ที่เกิดเป็นครั้งคราวโดยไม่หยุดงานทั้งหมด.

## การขยายตัวอย่าง – จาก JPEG ไปยัง PDF, จาก Cyrillic ไปยังหลายภาษา

รูปแบบที่เราใช้เพื่อ **convert image to text** สามารถใช้กับฟอร์แมตราสเตอร์ใดก็ได้: PNG, BMP, TIFF, แม้กระทั่ง PDF ที่สแกน (เพียงแค่ดึงหน้ามาเป็นภาพก่อน). หากคุณต้องการ **extract text from image** ไฟล์ที่มีหลายภาษา, คุณสามารถส่งรายการได้:

```python
ocr_engine.language = [ocr.Language.CYRILLIC, ocr.Language.ENGLISH]
```

และหากคุณทำงานกับรูปถ่ายความละเอียดสูงที่ถ่ายด้วยสมาร์ทโฟน, พิจารณาขั้นตอนการ preprocessing:

```python
# Denoise and binarize for better OCR accuracy
clean_image = cyrillic_image.filter(ocr.Filter.GAUSSIAN_BLUR, radius=1)
clean_image = clean_image.binarize(threshold=127)
ocr_result = ocr_engine.recognize(clean_image)
```

การปรับแต่งเหล่านี้มักทำให้ **python ocr example** ธรรมดากลายเป็นโค้ดระดับ production.

## สคริปต์ทำงานเต็มรูปแบบ

ด้านล่างเป็นสคริปต์ที่สมบูรณ์พร้อมรันที่รวมส่วนต่าง ๆ เข้าด้วยกัน. บันทึกเป็น `convert_image_to_text.py` แล้วรันด้วย `python convert_image_to_text.py`.



## คุณควรเรียนรู้อะไรต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้. แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอนเพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานทางเลือกในโครงการของคุณ.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}