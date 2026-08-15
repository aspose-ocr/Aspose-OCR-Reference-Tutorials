---
category: general
date: 2026-03-28
description: ดึงข้อความจากไฟล์ TIFF ด้วย Aspose OCR ใน Python เรียนรู้วิธีแปลง TIFF
  เป็นข้อความอย่างรวดเร็วและเชื่อถือได้
draft: false
keywords:
- extract text from tiff
- convert tiff to text
language: th
og_description: ดึงข้อความจากไฟล์ TIFF ด้วย Aspose OCR ใน Python คู่มือนี้แสดงวิธีแปลง
  TIFF เป็นข้อความแบบขั้นตอนต่อขั้นตอน.
og_title: สกัดข้อความจากไฟล์ TIFF – คู่มือ Python ฉบับสมบูรณ์
tags:
- OCR
- Python
- Aspose
title: ดึงข้อความจากไฟล์ TIFF – คู่มือ Python ฉบับสมบูรณ์
url: /th/python-java/general/extract-text-from-tiff-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ดึงข้อความจาก TIFF – คู่มือ Python ฉบับสมบูรณ์

ต้องการ **ดึงข้อความจากภาพ TIFF** ในโปรเจกต์ Python ของคุณหรือไม่? คู่มือนี้จะแสดงวิธี **แปลง TIFF เป็นข้อความ** ด้วยไลบรารี Aspose OCR และทำให้เข้าใจง่ายแม้สำหรับผู้เริ่มต้น  

หากคุณเคยมองภาพ TIFF แบบหลายหน้าและสงสัยว่าจะเอาคำออกมาได้อย่างไรโดยไม่ต้องพิมพ์ด้วยตนเอง คุณมาถูกที่แล้ว เราจะพาคุณผ่านกระบวนการทั้งหมด—ตั้งแต่การติดตั้งแพ็กเกจจนถึงการจัดการกรณีขอบเช่นไฟล์ที่เข้ารหัส—เพื่อให้คุณสามารถมุ่งเน้นการสร้างฟีเจอร์ที่สำคัญได้

## สิ่งที่คุณจะได้เรียนรู้

ในบทเรียนนี้คุณจะพบว่า:

* วิธีตั้งค่า Aspose OCR สำหรับ Python
* โค้ดที่จำเป็นในการอ่านทุกหน้าของ TIFF แบบหลายหน้า
* วิธีจัดการกับปัญหาทั่วไป เช่น ฟอนต์หายหรือหน้าที่เสียหาย
* เคล็ดลับเพื่อปรับปรุงความแม่นยำและประสิทธิภาพเมื่อคุณ **ดึงข้อความจากไฟล์ TIFF** ในปริมาณมาก

เมื่อเสร็จสิ้น คุณจะมีสคริปต์พร้อมรันที่แปลง TIFF ใด ๆ ให้เป็นข้อความธรรมดา พร้อมสำหรับการทำดัชนี การค้นหา หรือการส่งต่อไปยัง pipeline NLP ต่อไป

### ข้อกำหนดเบื้องต้น

* Python 3.8 หรือใหม่กว่า (ไลบรารีรองรับ 3.7+)
* ใบอนุญาต Aspose OCR ที่ใช้งานได้ — หรือคุณสามารถเริ่มต้นด้วยรุ่นทดลอง (โค้ดทำงานในโหมดประเมินผล แต่จะมีลายน้ำบนผลลัพธ์)
* ความคุ้นเคยพื้นฐานกับ virtual environment ของ Python (ไม่บังคับแต่แนะนำ)

---

## ขั้นตอนที่ 1 – ติดตั้งแพ็กเกจ Aspose OCR

สิ่งแรกที่ต้องทำคือให้ได้แพ็กเกจ `aspose-ocr` ซึ่งโฮสต์บน PyPI ดังนั้นการติดตั้งด้วย `pip` ธรรมดาก็เพียงพอ

```bash
pip install aspose-ocr
```

> **เคล็ดลับ:** ใช้ virtual environment (`python -m venv venv`) เพื่อแยกการพึ่งพาออกจากกัน มันช่วยป้องกันการชนกันของเวอร์ชันกับโปรเจกต์อื่นที่คุณอาจกำลังทำอยู่

> **ทำไมเรื่องนี้ถึงสำคัญ:** การติดตั้งแพ็กเกจจะดึงไบนารีของเครื่องมือ OCR ที่ทำงานหนักจริง ๆ หากไม่มีไบนารีเหล่านี้ เมธอด `recognize_from_tiff` จะไม่มีอยู่และคุณจะเจอ `ImportError`

---

## ขั้นตอนที่ 2 – นำเข้าไลบรารีและสร้าง OCR Engine

เมื่อไลบรารีอยู่บนเครื่องแล้ว ให้นำเข้าและสร้างอ็อบเจ็กต์ `OcrEngine` ซึ่งเป็นหัวใจหลักที่ทำการประมวลผลข้อมูลภาพ

```python
# Step 2: Import the Aspose OCR library and create an engine instance
import aspose.ocr as aocr

# Initialize the OCR engine – you can optionally pass a license file here
ocr_engine = aocr.OcrEngine()
```

*คลาส `OcrEngine` จะบรรจุการตั้งค่า OCR ทั้งหมด เช่น ภาษา ความละเอียด และตัวเลือกการเตรียมข้อมูล เราจะปรับบางอย่างในภายหลังเพื่อเพิ่มความแม่นยำ*

---

## ขั้นตอนที่ 3 – ระบุไฟล์ TIFF แบบหลายหน้าของคุณ

คุณต้องมีพาธไปยังไฟล์ TIFF ที่ต้องการอ่าน ไลบรารีรองรับพาธแบบ absolute หรือ relative แต่การใช้พาธ absolute จะช่วยหลีกเลี่ยงความประหลาดใจเมื่อสคริปต์รันจากโฟลเดอร์ทำงานอื่น

```python
# Step 3: Define the path to the TIFF file
tiff_file_path = "YOUR_DIRECTORY/input.tif"
```

> **ข้อผิดพลาดทั่วไป:** ลืม escape backslashes บน Windows (`C:\\Images\\file.tif`) ใช้ raw string (`r"C:\Images\file.tif"`) หรือใช้ slash ไปข้างหน้า (`/`) เพื่อหลีกเลี่ยงปัญหา

---

## ขั้นตอนที่ 4 – จดจำข้อความจากทุกหน้า

นี่คือหัวใจของบทเรียน: เรียก `recognize_from_tiff` เมธอดจะคืนค่าเป็นรายการของอ็อบเจ็กต์ `OcrResult` — หนึ่งอ็อบเจ็กต์ต่อหนึ่งหน้า — เพื่อให้คุณสามารถวนลูปประมวลผลแต่ละหน้าได้

```python
# Step 4: Extract text from every page of the TIFF
ocr_pages = ocr_engine.recognize_from_tiff(tiff_file_path)

# Verify we got results
if not ocr_pages:
    raise RuntimeError("No pages were recognized. Check the file path and format.")
```

**ทำไมวิธีนี้ถึงได้ผล:** Aspose OCR จะทำการแยก TIFF เป็นเฟรมย่อยแต่ละเฟรม รันเครื่องมือ OCR บนแต่ละเฟรม แล้วรวมผลลัพธ์เข้าด้วยกัน วิธีนี้เชื่อถือได้มากกว่าการพยายามแยกหน้าเองด้วย Pillow หรือ ImageMagick

---

## ขั้นตอนที่ 5 – วนลูปผลลัพธ์และแสดงข้อความ

สุดท้าย ให้วนลูปผ่านรายการ `OcrResult` แล้วพิมพ์ (หรือบันทึก) ข้อความที่ดึงได้ คุณยังสามารถเขียนแต่ละหน้าลงไฟล์ `.txt` แยกกันได้หากต้องการ

```python
# Step 5: Print or save the extracted text
for page_index, page_result in enumerate(ocr_pages):
    print(f"--- TIFF Page {page_index + 1} ---")
    print(page_result.text)
    # Optional: write each page to a separate file
    with open(f"page_{page_index + 1}.txt", "w", encoding="utf-8") as f:
        f.write(page_result.text)
```

**ผลลัพธ์ที่คาดหวัง** (ตัดบางส่วนเพื่อความกระชับ):

```
--- TIFF Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
--- TIFF Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore...
```

> **การจัดการกรณีขอบ:** หากหน้าหนึ่งไม่มีข้อความที่สามารถจดจำได้ `page_result.text` จะเป็นสตริงว่าง คุณอาจต้องบันทึกหน้าเหล่านั้นเพื่อทำการตรวจสอบด้วยตนเองในภายหลัง

---

## โบนัส – ปรับแต่งการตั้งค่า OCR เพื่อความแม่นยำที่ดีกว่า

บางครั้งการตั้งค่าเริ่มต้นอาจไม่เพียงพอ โดยเฉพาะกับสแกนความละเอียดต่ำหรือฟอนต์แปลก ๆ ด้านล่างเป็นตัวเลือกบางอย่างที่คุณสามารถปรับได้

```python
# Set language (default is English)
ocr_engine.language = aocr.Language.English

# Increase image resolution before OCR (helps with blurry scans)
ocr_engine.image_preprocessing = aocr.ImagePreprocessingOptions(
    sharpen=True,
    contrast=1.2
)

# Enable deskew to straighten rotated pages
ocr_engine.deskew = True
```

*ตัวเลือกเหล่านี้เป็นทางเลือกเสริม แต่บ่อยครั้งที่ทำให้ผลลัพธ์เปลี่ยนจากข้อความสับสนเป็นข้อความที่อ่านได้และค้นหาได้ง่าย*

---

## ปัญหาที่พบบ่อย & วิธีหลีกเลี่ยง

| อาการ | สาเหตุที่เป็นไปได้ | วิธีแก้ |
|---------|--------------|-----|
| ผลลัพธ์ว่างสำหรับทุกหน้า | พาธไฟล์ผิดหรือ TIFF ใช้การบีบอัดที่ไม่รองรับ | ตรวจสอบพาธและให้แน่ใจว่า TIFF ใช้การบีบอัดที่รองรับ (เช่น LZW, PackBits) |
| ตัวอักษรแปลก (เช่น �) | การตั้งค่าภาษาไม่ถูกต้องหรือไม่มีฟอนต์ที่จำเป็น | ตั้งค่า `ocr_engine.language` ให้ตรงกับภาษาที่ต้องการ; ติดตั้งฟอนต์ที่จำเป็นบนระบบ |
| การประมวลผลช้าเมื่อไฟล์ TIFF ขนาดใหญ่ | โหมดทำงานแบบ single‑threaded เริ่มต้น | ใช้ `ocr_engine.recognize_from_tiff(..., parallel=True)` หากเวอร์ชันไลบรารีรองรับ |
| คำเตือนเรื่องใบอนุญาต | ใช้รุ่นทดลองโดยไม่มีไฟล์ใบอนุญาต | ให้ใบอนุญาตผ่าน `aocr.License().set_license("Aspose.OCR.lic")` |

---

## สคริปต์เต็ม – พร้อมรัน

ด้านล่างเป็นสคริปต์สมบูรณ์ที่รวมทุกขั้นตอนและการปรับแต่งเสริมที่กล่าวถึง คัดลอกและวางลงในไฟล์ชื่อ `extract_tiff_text.py` แล้วรันด้วย `python extract_tiff_text.py`

```python
#!/usr/bin/env python3
"""
extract_tiff_text.py

A complete example that extracts text from a multi‑page TIFF using Aspose OCR.
It demonstrates how to:
- Install and import the library
- Initialize the OCR engine
- Configure optional preprocessing
- Iterate over each page and save the results

Author: Your Name
Date: 2026‑03‑28
"""

import aspose.ocr as aocr
import os
import sys

def main(tiff_path: str, output_dir: str = "output"):
    # Ensure output directory exists
    os.makedirs(output_dir, exist_ok=True)

    # Initialize the OCR engine
    ocr_engine = aocr.OcrEngine()

    # Optional: fine‑tune OCR settings for better accuracy
    ocr_engine.language = aocr.Language.English
    ocr_engine.image_preprocessing = aocr.ImagePreprocessingOptions(
        sharpen=True,
        contrast=1.2
    )
    ocr_engine.deskew = True

    # Perform OCR on the TIFF
    try:
        ocr_pages = ocr_engine.recognize_from_tiff(tiff_path)
    except Exception as e:
        sys.exit(f"Failed to process {tiff_path}: {e}")

    if not ocr_pages:
        sys.exit("No pages were recognized. Check the file path and format.")

    # Iterate over results
    for idx, result in enumerate(ocr_pages, start=1):
        page_text = result.text or "[No recognizable text]"
        print(f"--- TIFF Page {idx} ---")
        print(page_text[:200] + ("..." if len(page_text) > 200 else ""))  # preview

        # Save each page's text
        out_file = os.path.join(output_dir, f"page_{idx}.txt")
        with open(out_file, "w", encoding="utf-8") as f:
            f.write(page_text)

    print(f"\nAll pages processed. Text files saved in '{output_dir}'.")

if __name__ == "__main__":
    if len(sys.argv) < 2:
        sys.exit("Usage: python extract_tiff_text.py <path_to_tiff>")
    tiff_file = sys.argv[1]
    main(tiff_file)
```

**การรันสคริปต์**

```bash
python extract_tiff_text.py /path/to/your/input.tif
```

คุณจะเห็นตัวอย่างข้อความในคอนโซลสำหรับแต่ละหน้า และโฟลเดอร์ `output` ที่มีไฟล์ `page_1.txt`, `page_2.txt` เป็นต้น

---

## สรุป

เราครอบคลุมทุกอย่างที่คุณต้องการเพื่อ **ดึงข้อความจากไฟล์ TIFF** ด้วย Python และ Aspose OCR ตั้งแต่การติดตั้งแพ็กเกจจนถึงการจัดการเอกสารหลายหน้า ปรับตั้งค่าเพื่อความแม่นยำ และบันทึกผลลัพธ์ ตอนนี้เวิร์กโฟลว์ทั้งหมดอยู่ในมือคุณแล้ว  

หากคุณต้องการ **แปลง TIFF เป็นข้อความ** ในสายการผลิตจริง ควรพิจารณาการทำ batch ไฟล์ การทำ parallel OCR และการเก็บผลลัพธ์ในดัชนีที่ค้นหาได้ เช่น Elasticsearch สำหรับผู้ที่อยากท้าทายเพิ่มเติม ลองใช้ภาษาอื่น (`aocr.Language.Spanish`) หรือส่งผลลัพธ์ OCR ดิบเข้าไลบรารีตรวจสอบการสะกดเพื่อทำความสะอาดเสียงรบกวนจาก OCR  

มีคำถามเกี่ยวกับการสเกล การให้ใบอนุญาต หรือการเชื่อมต่อกับคลาวด์สตอเรจ? แสดงความคิดเห็นด้านล่าง แล้วขอให้สนุกกับการเขียนโค้ด!

---

![Diagram showing the OCR flow from TIFF file to extracted text](https://example.com/placeholder-image.png "ดึงข้อความจาก TIFF ด้วย Python")

*ข้อความแทนภาพ: ดึงข้อความจาก TIFF ด้วย Python*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}