---
category: general
date: 2026-03-26
description: เรียนรู้วิธีแก้การเอียงของภาพ, แยกข้อความจากภาพและสร้างกระบวนการเตรียมภาพเพื่อกำจัดสัญญาณรบกวนจากการสแกนและแปลงภาพสแกนเป็นข้อความ.
draft: false
keywords:
- how to deskew image
- recognize text from image
- image preprocessing pipeline
- remove noise from scan
- convert scanned image to text
language: th
og_description: วิธีแก้การเอียงของภาพและแปลงการสแกนที่เอียงให้เป็นข้อความที่ค้นหาได้
  ตามคำแนะนำนี้เพื่อจดจำข้อความจากภาพ, กำจัดสัญญาณรบกวนจากการสแกน, และแปลงภาพสแกนเป็นข้อความ.
og_title: วิธีแก้การเอียงของภาพ – คู่มือ OCR ทีละขั้นตอน
tags:
- OCR
- image-processing
- Python
title: วิธีปรับแนวภาพให้ตรง – คู่มือฉบับสมบูรณ์พร้อม OCR
url: /th/python-java/general/how-to-deskew-image-complete-guide-with-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีแก้ไขการเอียงของภาพ – คู่มือฉบับเต็มกับ OCR

เคยสงสัยไหมว่า **how to deskew image** ที่ได้จากสแกนเนอร์ราคาถูก? คุณไม่ได้เป็นคนเดียว หน้าเอกสารที่เอียงดูไม่เป็นมืออาชีพ และที่สำคัญ การเอียงอาจทำให้เครื่อง OCR ใด ๆ ที่พยายาม **recognize text from image** ทำงานผิดพลาด  

ในบทแนะนำนี้ เราจะพาคุณผ่าน **image preprocessing pipeline** แบบเต็มที่ทำการแก้ไขการเอียง, ทำให้เป็นภาพขาว‑ดำ, และลดสัญญาณรบกวนของสแกน, จากนั้นส่งต่อให้กับเครื่อง OCR เพื่อให้คุณสามารถ **convert scanned image to text** ได้อย่างง่ายดาย ไม่ต้องใช้เวทมนตร์ เพียงแค่ Python ธรรมดาและไลบรารีเล็ก ๆ ที่ทำงานหนักให้

## สิ่งที่คุณต้องเตรียม

- Python 3.9+ (โค้ดทำงานบน 3.10 และใหม่กว่า)
- The `ocr` package (ติดตั้งด้วย `pip install ocr‑toolkit` – แทนที่ด้วยชื่อไลบรารีของคุณ)
- A scanned JPEG or PNG that’s noticeably skewed (เช่น `skewed_scan.jpg`)
- A little curiosity about why each preprocessing step matters (ความอยากรู้อยากเห็นว่าทำไมแต่ละขั้นตอนการเตรียมภาพจึงสำคัญ)

เท่านี้เอง ไม่ต้องพึ่งพาไลบรารีหนัก ๆ อย่าง OpenCV เว้นแต่คุณต้องการเจาะลึกต่อไปในภายหลัง

## ขั้นตอนที่ 1: โหลดภาพสแกน

สิ่งแรกที่ทำคือดึงไฟล์เข้ามาในหน่วยความจำ ขั้นตอนนี้ง่ายแต่สำคัญ—หากพาธผิด ทุกอย่างจะล้มเหลว

```python
# Step 1: Load the scanned image
image_path = "YOUR_DIRECTORY/skewed_scan.jpg"
original_image = ocr.Imaging.Image.load(image_path)
```

> **ทำไม?**  
> การโหลดภาพทำให้เราได้อ็อบเจกต์ที่สามารถจัดการได้ซึ่ง `ocr.ImagePreprocessor` สามารถทำงานกับมันได้ การข้ามขั้นตอนนี้จะทำให้ pipeline ไม่เห็นข้อมูลพิกเซลจริง

## วิธีแก้ไขการเอียงของภาพและเตรียมพร้อมสำหรับ OCR

เมื่อเรามีภาพแล้ว มาตรงกันให้เรียบ `deskew()` จะประเมินมุมเอียงและหมุนภาพกลับเป็นแนวนอน

```python
# Step 2: Create an image preprocessor and correct the orientation
preprocessor = ocr.ImagePreprocessor()
preprocessor.deskew()
```

> **เคล็ดลับ:** หากสแกนของคุณเอียงเล็กน้อย (≤ 3°) อัลกอริทึมเริ่มต้นมักจะแม่นยำ สำหรับมุมที่มากเกินไปคุณอาจต้องปรับพารามิเตอร์ภายใน—ดูเอกสารของไลบรารีสำหรับ `max_angle`

## ทำให้ภาพเป็นแบบ Binary – แปลงเป็นสีขาว‑ดำ

เครื่อง OCR ชอบอินพุตที่คอนทราสต์สูง การแปลงภาพเป็นแบบ binary (สีขาว‑ดำ) จะลบเฉดสีอ่อน ๆ ที่อาจทำให้การจดจำอักขระสับสน

```python
# Step 3: Convert the image to a binary (black‑and‑white) representation
preprocessor.binarize(threshold=128)
```

> **กำลังเกิดอะไรขึ้น?**  
> พิกเซลที่สว่างกว่า 128 จะเป็นสีขาว; ส่วนที่เหลือจะเป็นสีดำ ปรับค่า threshold หากสแกนของคุณมืดหรือสว่างเกินปกติ

## ลบสัญญาณรบกวนจากสแกนก่อน OCR

แม้ภาพที่แก้ไขการเอียงอย่างสมบูรณ์ก็อาจมีจุดรอย, ฝุ่น, หรือ artefacts จากการบีบอัด สิ่งเล็ก ๆ เหล่านี้เป็นศัตรูของเครื่อง OCR ใด ๆ

```python
# Step 4: Reduce noise to improve OCR accuracy
preprocessor.denoise(radius=1)
```

> **ทำไมต้องลบสัญญาณรบกวน?**  
> สัญญาณรบกวนสร้างขอบเท็จที่เครื่อง OCR อาจตีความเป็นอักขระ รัศมีเล็ก ๆ เพียงพอสำหรับสแกนส่วนใหญ่; เพิ่มขึ้นสำหรับเอกสารที่มีเม็ดฝุ่นมาก

## ใช้งาน Image Preprocessing Pipeline

การตั้งค่าทั้งหมดพร้อมแล้ว—ตอนนี้เราจะรัน pipeline กับภาพต้นฉบับ

```python
# Step 5: Apply the preprocessing pipeline to the loaded image
processed_image = preprocessor.apply(original_image)
```

> **ผลลัพธ์:** `processed_image` คือบิตแมพที่ทำความสะอาดแล้ว, เรียงตรง, คอนทราสต์สูง พร้อมสำหรับการสกัดข้อความ

## จดจำข้อความจากภาพด้วย OCR Engine

ถึงเวลาที่จะอ่านข้อความจริง ๆ เราเริ่มต้น OCR engine, ป้อนภาพที่ผ่านการปรับปรุงให้กับมัน, และขอรับสตริงดิบ

```python
# Step 6: Initialise the OCR engine and provide the processed image
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(processed_image)

# Step 7: Recognise text and output the result
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

> **ผลลัพธ์ที่คาดหวัง** (ตัวอย่าง):

```
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

หากคุณเห็นอักขระแปลก ๆ ให้ตรวจสอบขั้นตอนการแก้ไขการเอียงอีกครั้งหรือทดลองใช้ค่า `threshold` ที่ต่างออกไป

## สร้าง Image Preprocessing Pipeline – สคริปต์เต็ม

รวมทุกอย่างเข้าด้วยกัน นี่คือสคริปต์เดียวที่สามารถรันได้ คุณสามารถวางลงในไฟล์ `.py` แล้วเรียกใช้ได้:

```python
import ocr  # Replace with the actual import path of your OCR library

# -------------------------------------------------
# 1️⃣ Load the scanned image
# -------------------------------------------------
image_path = "YOUR_DIRECTORY/skewed_scan.jpg"
original_image = ocr.Imaging.Image.load(image_path)

# -------------------------------------------------
# 2️⃣ Deskew – how to deskew image
# -------------------------------------------------
preprocessor = ocr.ImagePreprocessor()
preprocessor.deskew()

# -------------------------------------------------
# 3️⃣ Binarize – convert to black‑and‑white
# -------------------------------------------------
preprocessor.binarize(threshold=128)

# -------------------------------------------------
# 4️⃣ Denoise – remove noise from scan
# -------------------------------------------------
preprocessor.denoise(radius=1)

# -------------------------------------------------
# 5️⃣ Apply the pipeline
# -------------------------------------------------
processed_image = preprocessor.apply(original_image)

# -------------------------------------------------
# 6️⃣ OCR – recognize text from image
# -------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(processed_image)

# -------------------------------------------------
# 7️⃣ Output – convert scanned image to text
# -------------------------------------------------
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

> **เคล็ดลับ:** ห่อทั้งหมดในฟังก์ชัน (`def ocr_from_file(path): …`) หากคุณวางแผนจะประมวลผลหลายไฟล์เป็นชุด

## คำถามทั่วไป & กรณีขอบ

- **ถ้าภาพอยู่ในแนวตั้งอยู่แล้วล่ะ?**  
  วิธี `deskew()` จะตรวจจับมุมใกล้ศูนย์และไม่ทำการเปลี่ยนแปลงภาพ ดังนั้นคุณสามารถรันได้อย่างปลอดภัยกับทุกไฟล์

- **สแกนของฉันเป็นสี—ควรเก็บไว้หรือไม่?**  
  สีไม่มีประโยชน์สำหรับงาน OCR ส่วนใหญ่ การทำ Binarization จะลบสีออก ทำให้การประมวลผลเร็วขึ้นและใช้หน่วยความจำน้อยลง

- **ฉันสามารถต่อหลายขั้นตอนการเตรียมภาพได้หรือไม่?**  
  แน่นอน คลาส `ImagePreprocessor` ถูกออกแบบมาสำหรับ pipeline; คุณสามารถเพิ่ม `sharpen()`, `contrast_enhance()`, หรือฟิลเตอร์กำหนดเองก่อนเรียก `apply()`

- **ผลลัพธ์ OCR มีการขึ้นบรรทัดใหม่ที่ไม่ต้องการ—จะแก้อย่างไร?**  
  ทำการ post‑process สตริงด้วย `text.replace("\n", " ").strip()` หรือใช้ไลบรารีวิเคราะห์เลย์เอาต์ขั้นสูงเช่นโหมด `--psm` ของ Tesseract

## ขั้นตอนต่อไป

ตอนนี้คุณรู้แล้วว่า **how to deskew image** และมี **image preprocessing pipeline** ที่มั่นคง คุณอาจสำรวจต่อ:

- การบูรณาการ **recognize text from image** เข้าไปใน Flask API เพื่ออัปโหลดเอกสารแบบเรียลไทม์
- ใช้ pipeline เพื่อ **remove noise from scan** ของเอกสารประวัติศาสตร์ที่ต้องการการอนุรักษ์
- ขยายเพื่อประมวลผลเป็นชุดหลายพันหน้าและสร้าง PDF ที่ค้นหาได้โดยใช้ `pdfminer` หรือ `PyMuPDF`

คุณสามารถทดลองกับค่า threshold ต่าง ๆ, รัศมีการลดสัญญาณรบกวน, หรือแม้แต่สลับ backend ของ OCR ไปเป็น Tesseract หากต้องการสนับสนุนหลายภาษา พื้นฐานยังคงเหมือนเดิม: เรียงตรง, ทำความสะอาด, แล้วอ่าน

---

*ขอให้เขียนโค้ดอย่างสนุก! หากคุณเจอปัญหาใด ๆ ฝากคอมเมนต์ไว้ด้านล่าง—ผมยินดีช่วยคุณปรับแต่ง pipeline ให้เหมาะสม*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}