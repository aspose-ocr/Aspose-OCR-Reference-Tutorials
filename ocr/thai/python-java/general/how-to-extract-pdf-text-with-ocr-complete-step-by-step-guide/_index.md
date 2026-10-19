---
category: general
date: 2026-03-26
description: วิธีดึงข้อความจาก PDF ด้วย OCR เรียนรู้การโหลด PDF เป็นภาพ, การจดจำข้อความใน
  PDF และการดึงข้อความจาก PDF ด้วยตัวอย่าง Python อย่างง่าย.
draft: false
keywords:
- how to extract pdf
- extract text from pdf
- recognize pdf text
- load pdf as image
- how to use OCR
language: th
og_description: วิธีดึงข้อความจาก PDF ด้วย OCR คู่มือนี้จะแสดงวิธีโหลด PDF เป็นภาพ
  จดจำข้อความใน PDF และดึงข้อความจาก PDF ด้วย Python
og_title: วิธีดึงข้อความจาก PDF ด้วย OCR – คู่มือเต็ม
tags:
- OCR
- Python
- PDF processing
title: วิธีสกัดข้อความจาก PDF ด้วย OCR – คู่มือขั้นตอนโดยละเอียด
url: /th/python-java/general/how-to-extract-pdf-text-with-ocr-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีดึงข้อความจาก PDF ด้วย OCR – คู่มือขั้นตอนเต็ม

เคยสงสัย **วิธีดึงข้อความจาก PDF** ที่เป็นแค่ภาพสแกนหรือไม่? คุณไม่ได้เป็นคนเดียว—นักพัฒนาหลายคนเจออุปสรรคนี้เมื่อต้องการเนื้อหาที่ค้นหาได้แต่มีแค่ PDF ที่เป็นภาพเท่านั้น ข่าวดีคือ? เพียงไม่กี่บรรทัดของโค้ดและไลบรารี OCR ที่ดี สามารถเปลี่ยน PDF ที่เป็นรูปภาพให้เป็นข้อความธรรมดาได้อย่างรวดเร็ว  

ในบทเรียนนี้เราจะเดินผ่าน **วิธีใช้ OCR** เพื่อโหลด PDF เป็นภาพ, จดจำข้อความใน PDF, และสุดท้าย **ดึงข้อความจาก PDF** ไม่ว่าจะยาวแค่ไหน ก็ตาม เมื่อเสร็จคุณจะได้สคริปต์ที่ทำงานได้, คำอธิบายแต่ละขั้นตอนที่ชัดเจน, และเคล็ดลับหลายอย่างเพื่อหลีกเลี่ยงปัญหาที่มักเจอ

## สิ่งที่คุณต้องเตรียม

- Python 3.9 หรือใหม่กว่า (โค้ดทำงานบน 3.10+ ด้วย)  
- แพ็กเกจ Python `ocr` (หรือไลบรารี OCR ใด ๆ ที่มี `OcrEngine`, `OcrEngineMode`, และ `Imaging.Image`)  
- PDF หลายหน้า ที่คุณต้องการประมวลผล (สำหรับสาธิตเราจะใช้ชื่อ `multi_page.pdf`)  
- ความคุ้นเคยพื้นฐานกับ virtual environment (ไม่บังคับแต่แนะนำ)

> **Pro tip:** หากคุณใช้ Windows ควรใช้ Anaconda Prompt; บน macOS/Linux เพียง `python -m venv venv && source venv/bin/activate` ก็พอ

## ขั้นตอน 1: ติดตั้งไลบรารี OCR

ก่อนอื่นให้ดาวน์โหลดแพ็กเกจ OCR จาก PyPI ตัวอย่างด้านล่างใช้แพ็กเกจสมมติ `ocr` ที่มี API เหมือนโค้ดที่แสดง, แต่ไลบรารีจริงส่วนใหญ่ (เช่น `pytesseract` + `pdf2image`) มีรูปแบบคล้ายกัน

```bash
pip install ocr
```

หากคุณใช้เอนจินอื่น ให้เปลี่ยน `ocr` เป็นชื่อที่เหมาะสม (เช่น `pip install pytesseract pdf2image`)

## ขั้นตอน 2: เริ่มต้น OCR Engine

การสร้างอินสแตนซ์ของเอนจินเป็นพื้นฐานของ **วิธีดึงข้อความจาก PDF** คิดว่าเอนจินคือสมองที่จะแปลพิกเซลในแต่ละหน้า PDF

```python
import ocr

# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()

# Set the engine to the default mode (fast enough for most PDFs)
ocr_engine.set_engine_mode(ocr.OcrEngineMode.DEFAULT)
```

> **ทำไมจึงสำคัญ:** `set_engine_mode` ให้คุณแลกเปลี่ยนความเร็วกับความแม่นยำ `DEFAULT` เป็นตัวเลือกที่สมดุล; หากต้องการความแม่นยำสูงขึ้นให้สลับเป็น `HIGH_ACCURACY` (ถ้าไลบรารีรองรับ)

## ขั้นตอน 3: โหลด PDF เป็นอ็อบเจกต์ Image

OCR ทำงานกับภาพ ไม่ใช่ไฟล์ PDF ดังนั้นต้องแปลง PDF เป็นรูปภาพก่อน วิธี `Imaging.Image.load` จะจัดการ PDF หลายหน้าให้โดยอัตโนมัติ

```python
# Step 3: Load the multi‑page PDF as an image object
pdf_path = "YOUR_DIRECTORY/multi_page.pdf"
pdf_image = ocr.Imaging.Image.load(pdf_path)
```

> **กรณีขอบ:** ไลบรารีบางตัวรับเฉพาะภาพหน้าเดียว ในกรณีนั้นคุณต้องวนลูปแต่ละหน้าโดยใช้ `pdf2image.convert_from_path` การเรียก `load` ของเราจัดการให้แล้ว ทำให้ **load pdf as image** เป็นบรรทัดเดียว

## ขั้นตอน 4: จดจำข้อความในทุกหน้า

ต่อไปคือหัวใจของ **recognize PDF text** เอนจินจะสแกนทุกหน้าและคืนรายการอ็อบเจกต์ผลลัพธ์—หนึ่งอ็อบเจกต์ต่อหน้า

```python
# Step 4: Recognize text on all pages of the PDF
page_results = ocr_engine.recognize_multi_page(pdf_image)
```

แต่ละ `page_result` มีเมธอดเช่น `get_text()` (ข้อความธรรมดา) และ `get_confidence()` (เมตริกคุณภาพเสริม)  

> **เคล็ดลับ:** หากต้องการเฉพาะหน้าแรก ให้เรียก `recognize(pdf_image[0])` แทนการใช้ตัวช่วยหลายหน้า

## ขั้นตอน 5: วนลูปผลลัพธ์และแสดงข้อความที่ดึงออกมา

สุดท้ายเราวนลูปผลลัพธ์และพิมพ์ข้อความของแต่ละหน้า นี่คือขั้นตอน **extract text from PDF** ทั้งหมด

```python
# Step 5: Print extracted text page by page
for index, page_result in enumerate(page_results):
    print(f"--- Page {index + 1} ---")
    print(page_result.get_text())
    # Optional: show confidence score
    # print(f"Confidence: {page_result.get_confidence():.2f}%")
```

### ผลลัพธ์ที่คาดหวัง

หาก `multi_page.pdf` มีสามหน้าโดยมีคำว่า “Hello”, “World”, และ “Python”, คุณจะเห็น:

```
--- Page 1 ---
Hello
--- Page 2 ---
World
--- Page 3 ---
Python
```

เท่านี้—PDF ของคุณก็สามารถค้นหาได้แล้วและข้อความพร้อมสำหรับการประมวลผลต่อ (เช่น การทำดัชนี, การวิเคราะห์อารมณ์, ฯลฯ)

## ขั้นตอน 6: จัดการกับปัญหาที่พบบ่อย

| Issue | Why it Happens | Quick Fix |
|-------|----------------|-----------|
| **Blank output** | PDF สแกนที่ DPI ต่ำ ทำให้ตัวอักษรไม่ชัด | เพิ่มความละเอียดของภาพก่อน OCR: `pdf_image = pdf_image.resize(300)` (300 DPI เป็นค่าที่เหมาะ) |
| **Garbage characters** | ตัวอักษรที่ไม่ใช่ละตินต้องการแพ็คเกจภาษา | โหลดโมเดลภาษาที่เหมาะ: `ocr_engine.load_language('spa')` สำหรับภาษาสเปน ฯลฯ |
| **Memory blow‑up on huge PDFs** | โหลดทุกหน้าในครั้งเดียวกิน RAM มาก | ประมวลผลเป็นชุด: `for img in pdf_image.split(batch=10): …` (pseudo‑code) |
| **Slow performance** | ใช้ `DEFAULT` กับเอกสารขนาดใหญ่ทำให้ช้า | สลับเป็นโหมด `FAST` หรือรัน OCR แบบขนานด้วย `concurrent.futures` |

## โบนัส: บันทึกข้อความที่ดึงออกไปเป็นไฟล์

หลาย pipeline จริงต้องเก็บข้อความไว้ นี่คือตัวช่วยขนาดเล็กที่เขียนทุกอย่างลง `output.txt`

```python
output_path = "YOUR_DIRECTORY/output.txt"

with open(output_path, "w", encoding="utf-8") as f:
    for idx, result in enumerate(page_results):
        f.write(f"--- Page {idx + 1} ---\n")
        f.write(result.get_text() + "\n\n")
print(f"All text saved to {output_path}")
```

ตอนนี้คุณสามารถส่ง `output.txt` ไปยังเครื่องมือค้นหา, ฐานข้อมูล, หรือโมเดล NLP ใด ๆ ก็ได้

## รวมทุกอย่างไว้ในสคริปต์เต็ม

ด้านล่างเป็นโปรแกรมที่พร้อมรัน คัดลอก‑วาง, ปรับเส้นทางไฟล์ตามต้องการ, แล้วคุณก็พร้อมใช้งาน

```python
# -*- coding: utf-8 -*-
"""
How to extract PDF text with OCR – end‑to‑end example.

Prerequisites:
    pip install ocr
"""

import ocr

def extract_text_from_pdf(pdf_path: str):
    """
    Load a PDF, run OCR on every page, and return a list of strings.
    """
    # Initialize engine
    engine = ocr.OcrEngine()
    engine.set_engine_mode(ocr.OcrEngineMode.DEFAULT)

    # Load PDF as image (multi‑page support)
    pdf_image = ocr.Imaging.Image.load(pdf_path)

    # Recognize text on all pages
    results = engine.recognize_multi_page(pdf_image)

    # Collect plain text
    texts = [res.get_text() for res in results]
    return texts

def main():
    pdf_file = "YOUR_DIRECTORY/multi_page.pdf"
    texts = extract_text_from_pdf(pdf_file)

    # Print and optionally save
    for i, txt in enumerate(texts, start=1):
        print(f"--- Page {i} ---")
        print(txt)
        print()

    # Save to file
    out_path = "YOUR_DIRECTORY/extracted_text.txt"
    with open(out_path, "w", encoding="utf-8") as out_f:
        for i, txt in enumerate(texts, start=1):
            out_f.write(f"--- Page {i} ---\n{txt}\n\n")
    print(f"Extracted text stored in {out_path}")

if __name__ == "__main__":
    main()
```

รันสคริปต์:

```bash
python extract_pdf_ocr.py
```

คุณจะเห็นเนื้อหาของแต่ละหน้าถูกพิมพ์บนคอนโซล ตามด้วยข้อความยืนยันว่าไฟล์ `extracted_text.txt` ถูกสร้างแล้ว

## สรุป

เราได้ครอบคลุม **วิธีดึงข้อความจาก PDF** ที่เป็นไฟล์ภาพ‑เท่านั้นโดยใช้ OCR ตั้งแต่การติดตั้งไลบรารีจนถึงการจัดการผลลัพธ์หลายหน้าและการบันทึกผลลัพธ์ คุณตอนนี้รู้ **วิธีใช้ OCR**, **วิธีโหลด PDF เป็นภาพ**, และ **วิธีจดจำข้อความใน PDF** อย่างมั่นใจ  

ขั้นตอนต่อไป? ลองสลับโหมดเอนจินเป็น high‑accuracy, ทดลองใช้แพ็คเกจภาษาเพื่อรองรับ PDF หลายภาษา, หรือส่งข้อความที่ดึงออกไปยังดัชนีการค้นหาเต็มข้อความอย่าง Elasticsearch ความเป็นไปได้ไม่มีที่สิ้นสุดเมื่อคุณเชี่ยวชาญพื้นฐานการดึงข้อความจากไฟล์ PDF

---

![ตัวอย่างการแยกข้อความจาก PDF](images/ocr_flowchart.png){alt="แผนผังการทำงานของการแยกข้อความจาก PDF"}

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}