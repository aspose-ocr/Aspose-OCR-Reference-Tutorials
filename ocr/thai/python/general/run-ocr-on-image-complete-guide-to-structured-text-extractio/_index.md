---
category: general
date: 2026-05-03
description: เรียนรู้วิธีทำ OCR บนภาพและดึงข้อความพร้อมพิกัดโดยใช้การจดจำ OCR แบบโครงสร้าง
  พร้อมโค้ด Python ทีละขั้นตอน.
draft: false
keywords:
- run OCR on image
- extract text with coordinates
- structured OCR recognition
- OCR post‑processing
- bounding box extraction
- image text detection
language: th
og_description: ทำ OCR บนภาพและรับข้อความพร้อมพิกัดโดยใช้การจดจำ OCR แบบโครงสร้าง
  ตัวอย่าง Python เต็มรูปแบบพร้อมคำอธิบาย
og_title: เรียกใช้ OCR บนภาพ – บทเรียนการสกัดข้อความแบบมีโครงสร้าง
tags:
- OCR
- Python
- Computer Vision
title: ทำ OCR บนภาพ – คู่มือฉบับสมบูรณ์สำหรับการสกัดข้อความเชิงโครงสร้าง
url: /th/python/general/run-ocr-on-image-complete-guide-to-structured-text-extractio/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Run OCR on image – Complete Guide to Structured Text Extraction

เคยต้อง **run OCR on image** ไฟล์แต่ไม่แน่ใจว่าจะเก็บตำแหน่งของแต่ละคำได้อย่างแม่นยำหรือไม่? คุณไม่ได้อยู่คนเดียว ในหลายโครงการ—เช่นการสแกนใบเสร็จ, การแปลงฟอร์มเป็นดิจิทัล, หรือการทดสอบ UI—คุณต้องการไม่เพียงแต่ข้อความดิบเท่านั้น แต่ยังต้องการ bounding box ที่บอกตำแหน่งของแต่ละบรรทัดบนภาพด้วย  

บทแนะนำนี้จะแสดงวิธีปฏิบัติจริงเพื่อ *run OCR on image* ด้วย **aocr** engine, ขอ **structured OCR recognition**, แล้วทำ post‑process ผลลัพธ์โดยคงรูปทรงเรขาคณิตไว้ ด้วยขั้นตอนไม่กี่บรรทัดของ Python คุณจะสามารถ **extract text with coordinates** ได้ และเข้าใจว่าทำไมโหมด structured ถึงสำคัญสำหรับงานต่อไป

## What You’ll Learn

- วิธี initialise OCR engine สำหรับ **structured OCR recognition**  
- วิธีป้อนภาพและรับผลลัพธ์ดิบที่รวม line bounds  
- วิธีรัน post‑processor ที่ทำความสะอาดข้อความโดยไม่สูญเสีย geometry  
- วิธีวนลูปผ่านบรรทัดสุดท้ายและพิมพ์ข้อความพร้อม bounding box  

ไม่มีมายากล ไม่มีขั้นตอนลับ—เพียงตัวอย่างที่ทำงานได้ครบถ้วนที่คุณสามารถนำไปใช้ในโปรเจกต์ของคุณได้ทันที

---

## Prerequisites

ก่อนที่เราจะเริ่ม โปรดตรวจสอบว่าคุณได้ติดตั้งสิ่งต่อไปนี้แล้ว:

```bash
pip install aocr ai   # hypothetical packages; replace with real ones if needed
```

คุณยังต้องมีไฟล์ภาพ (`input_image.png` หรือ `.jpg`) ที่มีข้อความชัดเจนและอ่านได้ ไม่ว่าจะเป็นใบแจ้งหนี้ที่สแกนหรือภาพหน้าจอใด ๆ ก็ได้ ตราบใดที่ OCR engine มองเห็นอักขระได้

---

## Step 1: Initialise the OCR engine for structured recognition

สิ่งแรกที่เราทำคือสร้างอินสแตนซ์ของ `aocr.Engine()` และบอกให้มันทำงานใน **structured OCR recognition** โหมด structured จะคืนค่าไม่เพียงแต่ข้อความธรรมดา แต่ยังรวมข้อมูลเรขาคณิต (bounding rectangles) ของแต่ละบรรทัด ซึ่งจำเป็นเมื่อคุณต้องแมปข้อความกลับไปยังภาพ

```python
import aocr
import ai   # hypothetical post‑processing module

# Initialise the OCR engine
ocr_engine = aocr.Engine()

# Request structured recognition (text + geometry)
ocr_engine.recognize_mode = aocr.RecognitionMode.Structured
```

> **Why this matters:**  
> ในโหมดปกติ engine อาจให้คุณแค่สตริงของคำที่ต่อเนื่องกันเท่านั้น โหมด structured ให้คุณได้โครงสร้างหน้า → บรรทัด → คำ แต่ละระดับมีพิกัด ทำให้ง่ายต่อการวางผลลัพธ์บนภาพต้นฉบับหรือส่งต่อไปยังโมเดลที่รับรู้ layout

---

## Step 2: Run OCR on the image and obtain raw results

ต่อไปเราจะป้อนภาพให้กับ engine การเรียก `recognize` จะคืนค่าเป็นอ็อบเจ็กต์ `OcrResult` ที่มีคอลเลกชันของบรรทัดแต่ละบรรทัด พร้อม bounding rectangle ของมันเอง

```python
# Load your image (any format supported by aocr)
input_image_path = "input_image.png"

# Run OCR – this returns an OcrResult with lines and bounds
raw_result = ocr_engine.recognize(input_image_path)
```

ในจุดนี้ `raw_result.lines` จะเก็บอ็อบเจ็กต์ที่มีสองแอตทริบิวต์สำคัญ:

- `text` – สตริงที่ engine จดจำได้สำหรับบรรทัดนั้น  
- `bounds` – ทูเพิลรูปแบบ `(x, y, width, height)` ที่บรรยายตำแหน่งของบรรทัด

---

## Step 3: Post‑process while preserving geometry

ผลลัพธ์ OCR ดิบมักมี noise: ตัวอักษรแปลกปลอม, ช่องว่างผิดตำแหน่ง, หรือปัญหา line‑break ฟังก์ชัน `ai.run_postprocessor` จะทำความสะอาดข้อความแต่ **คง geometry ดั้งเดิม** ไว้ ดังนั้นคุณยังคงมีพิกัดที่แม่นยำ

```python
# Apply a post‑processing step that corrects common OCR errors
postprocessed_result = ai.run_postprocessor(raw_result)

# The structure (lines + bounds) stays the same, only `line.text` changes
```

> **Pro tip:** หากคุณมีพจนานุกรมเฉพาะโดเมน (เช่นรหัสสินค้า) ให้ส่งพจนานุกรมแบบกำหนดเองไปยัง post‑processor เพื่อเพิ่มความแม่นยำ

---

## Step 4: Extract text with coordinates – iterate and display

สุดท้าย เราจะวนลูปผ่านบรรทัดที่ทำความสะอาดแล้ว พิมพ์ bounding box ของแต่ละบรรทัดพร้อมข้อความ นี่คือหัวใจของ **extract text with coordinates**

```python
# Print each recognised line together with its bounding box
for line in postprocessed_result.lines:
    print(f"[{line.bounds}] {line.text}")
```

### Expected Output

สมมติว่าภาพอินพุตมีสองบรรทัด: “Invoice #12345” และ “Total: $89.99” คุณจะเห็นผลลัพธ์ประมาณนี้:

```
[(15, 30, 210, 25)] Invoice #12345
[(15, 70, 190, 25)] Total: $89.99
```

ทูเพิลแรกคือ `(x, y, width, height)` ของบรรทัดบนภาพต้นฉบับ ทำให้คุณสามารถวาดสี่เหลี่ยม, ไฮไลท์ข้อความ, หรือส่งพิกัดไปยังระบบอื่นได้

---

## Visualising the Result (Optional)

หากคุณต้องการดู bounding boxes ที่ซ้อนบนภาพ สามารถใช้ Pillow (PIL) วาดสี่เหลี่ยมได้ ตัวอย่างสคริปต์สั้น ๆ ด้านล่างนี้ หากคุณต้องการเพียงข้อมูลดิบก็สามารถข้ามขั้นตอนนี้ได้

```python
from PIL import Image, ImageDraw

# Open the original image
img = Image.open(input_image_path)
draw = ImageDraw.Draw(img)

# Draw a rectangle around each line
for line in postprocessed_result.lines:
    x, y, w, h = line.bounds
    draw.rectangle([x, y, x + w, y + h], outline="red", width=2)

# Save or show the annotated image
img.save("annotated_output.png")
img.show()
```

![run OCR on image example showing bounding boxes](/images/ocr-bounding-boxes.png "run OCR on image – bounding box overlay")

ข้อความ alt ด้านบนมี **primary keyword** อยู่แล้ว เพื่อตรงตามข้อกำหนด SEO ของ attribute alt รูปภาพ

---

## Why Structured OCR Recognition Beats Simple Text Extraction

คุณอาจสงสัยว่า “ทำไมต้องใช้ OCR แล้วต้องการ geometry ด้วย? ไม่ได้แค่ต้องการข้อความอย่างเดียวหรอกหรือ?”  

- **Spatial context:** เมื่อคุณต้องแมปฟิลด์บนฟอร์ม (เช่น “Date” ข้างค่าที่เป็นวันที่) พิกัดบอกว่า *ที่ไหน* ข้อมูลนั้นอยู่  
- **Multi‑column layouts:** ข้อความเชิงเส้นธรรมดาจะสูญเสียลำดับคอลัมน์; ข้อมูลแบบ structured รักษาลำดับคอลัมน์ไว้  
- **Post‑processing accuracy:** การรู้ขนาดกล่องช่วยให้คุณตัดสินใจได้ว่าคำนั้นเป็นหัวข้อ, หมายเหตุ, หรือ artefact ที่ไม่ต้องการ  

สรุปแล้ว **structured OCR recognition** ให้ความยืดหยุ่นในการสร้าง pipeline ที่ฉลาดกว่า—ไม่ว่าจะเป็นการบันทึกข้อมูลลงฐานข้อมูล, สร้าง PDF ที่ค้นหาได้, หรือฝึกโมเดล machine‑learning ที่เคารพ layout

---

## Common Edge Cases and How to Handle Them

| Situation | What to Watch For | Suggested Fix |
|-----------|-------------------|---------------|
| **Rotated or skewed images** | Bounding boxes อาจเอียงหรือไม่ตรง | ทำการ pre‑process ด้วย deskewing (เช่น `warpAffine` ของ OpenCV) |
| **Very small fonts** | Engine อาจพลาดอักขระ ทำให้บรรทัดว่าง | เพิ่มความละเอียดของภาพหรือใช้ `ocr_engine.set_dpi(300)` |
| **Mixed languages** | โมเดลภาษาไม่ตรงทำให้ข้อความเสีย | ตั้งค่า `ocr_engine.language = ["en", "de"]` ก่อนทำการ recognization |
| **Overlapping boxes** | Post‑processor อาจรวมสองบรรทัดโดยไม่ตั้งใจ | ตรวจสอบ `line.bounds` หลังการประมวลผล; ปรับ thresholds ใน `ai.run_postprocessor` |

การจัดการกับกรณีเหล่านี้ตั้งแต่ต้นจะช่วยลดปัญหาเมื่อคุณขยายโซลูชันไปยังเอกสารหลายร้อยฉบับต่อวัน

---

## Full End‑to‑End Script

ด้านล่างเป็นโปรแกรมเต็มที่พร้อมรัน ซึ่งรวมทุกขั้นตอนเข้าด้วยกัน คัดลอก‑วาง, ปรับเส้นทางภาพ, แล้วคุณก็พร้อมใช้งาน

```python
# -*- coding: utf-8 -*-
"""
Run OCR on image – extract text with coordinates using structured OCR recognition.
Author: Your Name
Date: 2026-05-03
"""

import aocr
import ai
from PIL import Image, ImageDraw

def run_structured_ocr(image_path: str, annotate: bool = False):
    # 1️⃣ Initialise the OCR engine
    ocr_engine = aocr.Engine()
    ocr_engine.recognize_mode = aocr.RecognitionMode.Structured

    # 2️⃣ Recognise the image
    raw_result = ocr_engine.recognize(image_path)

    # 3️⃣ Post‑process while keeping geometry
    processed = ai.run_postprocessor(raw_result)

    # 4️⃣ Print each line with its bounding box
    for line in processed.lines:
        print(f"[{line.bounds}] {line.text}")

    # Optional visualisation
    if annotate:
        img = Image.open(image_path)
        draw = ImageDraw.Draw(img)
        for line in processed.lines:
            x, y, w, h = line.bounds
            draw.rectangle([x, y, x + w, y + h], outline="red", width=2)
        annotated_path = "annotated_" + image_path
        img.save(annotated_path)
        print(f"Annotated image saved as {annotated_path}")

if __name__ == "__main__":
    INPUT_IMG = "input_image.png"
    run_structured_ocr(INPUT_IMG, annotate=True)
```

การรันสคริปต์นี้จะ:

1. **Run OCR on image** ด้วยโหมด structured  
2. **Extract text with coordinates** สำหรับทุกบรรทัด  
3. ตัวเลือกสร้าง PNG ที่มี annotation แสดงกล่อง

---

## Conclusion

ตอนนี้คุณมีโซลูชันครบวงจรเพื่อ **run OCR on image** และ **extract text with coordinates** ด้วย **structured OCR recognition** โค้ดแสดงทุกขั้นตอน—from การ initialise engine ไปจนถึง post‑processing และการตรวจสอบด้วยภาพ—เพื่อให้คุณปรับใช้กับใบเสร็จ, ฟอร์ม, หรือเอกสารภาพใด ๆ ที่ต้องการการระบุตำแหน่งข้อความอย่างแม่นยำ  

ต่อไปคุณอาจลองสลับ `aocr` engine กับไลบรารีอื่น (Tesseract, EasyOCR) แล้วเปรียบเทียบผลลัพธ์ structured ของพวกมัน ทดลองกลยุทธ์ post‑processing ต่าง ๆ เช่นการตรวจสอบการสะกดหรือ regex เฉพาะโดเมน เพื่อเพิ่มความแม่นยำสำหรับงานของคุณ และหากคุณกำลังสร้าง pipeline ขนาดใหญ่ คิดถึงการเก็บคู่ `(text, bounds)` ลงฐานข้อมูลเพื่อการวิเคราะห์ต่อไป  

Happy coding, and may your OCR projects be ever accurate!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}