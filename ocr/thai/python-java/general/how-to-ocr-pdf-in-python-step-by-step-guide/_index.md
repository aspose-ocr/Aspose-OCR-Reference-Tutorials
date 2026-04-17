---
category: general
date: 2026-03-28
description: เรียนรู้วิธีทำ OCR PDF ด้วย Python อย่างรวดเร็ว คู่มือนี้จะแสดงวิธีดึงข้อความจาก
  PDF, จดจำข้อความจาก PDF, และแปลง PDF สแกนเป็นข้อความโดยใช้ Aspose OCR.
draft: false
keywords:
- how to ocr pdf
- ocr pdf with python
- extract text from pdf
- recognize text from pdf
- convert scanned pdf to text
language: th
og_description: เชี่ยวชาญการทำ OCR PDF ด้วย Python ดึงข้อความจาก PDF จดจำข้อความจาก
  PDF และแปลง PDF สแกนเป็นข้อความในเวลาไม่กี่นาที.
og_title: วิธีทำ OCR PDF ด้วย Python – คู่มือเต็ม
tags:
- PDF
- OCR
- Python
- Aspose
title: วิธีทำ OCR PDF ด้วย Python – คู่มือขั้นตอนโดยละเอียด
url: /th/python-java/general/how-to-ocr-pdf-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีทำ OCR PDF ด้วย Python – คู่มือขั้นตอนเต็ม

เคยสงสัย **วิธีทำ OCR PDF** เมื่อไฟล์เป็นแค่รูปของหน้าเอกสารหรือไม่? คุณไม่ได้เป็นคนเดียว ในบทเรียนนี้เราจะพาคุณผ่านขั้นตอนทั้งหมดเพื่อทำ OCR PDF, ดึงข้อความจาก PDF, และแปลง PDF ที่สแกนเป็นข้อความที่ค้นหาได้ – ทั้งหมดด้วยโค้ด Python ธรรมดา

เราจะครอบคลุมตั้งแต่การติดตั้งไลบรารี Aspose OCR ไปจนถึงการดึงข้อความที่ได้รับการจดจำจากแต่ละหน้า เมื่อเสร็จคุณจะสามารถ **OCR PDF ด้วย Python**, **ดึงข้อความจาก PDF**, และ **แปลง PDF ที่สแกนเป็นข้อความ** ได้โดยไม่ต้องค้นหาเอกสารกระจัดกระจาย ไม่มีส่วนเกิน เพียงตัวอย่างที่ทำงานได้จริงที่คุณสามารถคัดลอก‑วางได้

## สิ่งที่คุณต้องมี

ก่อนที่เราจะเริ่มลงมือทำ โปรดตรวจสอบว่าคุณมี:

* Python 3.8+ (เวอร์ชันล่าสุดที่เสถียรที่สุดทำงานได้ดีที่สุด)  
* ใบอนุญาต Aspose OCR for Python หรือคีย์ทดลองฟรี – สามารถรับได้จากเว็บไซต์ของ Aspose  
* PDF ที่สแกนที่ต้องการประมวลผล (เราจะเรียกมันว่า `input.pdf`)  

ถ้าคุณมีทั้งหมดแล้ว เยี่ยม—มาเริ่มกันเลย ถ้ายังไม่มี การติดตั้งแพ็กเกจก็ง่ายมากและเราจะสอนคุณ

## วิธีทำ OCR PDF – การตั้งค่าสภาพแวดล้อม

สิ่งแรกที่ต้องทำคือดึงโมดูล Aspose OCR มาติดตั้งบนเครื่องของคุณ แพ็กเกจชื่อ `aspose-ocr` และคุณสามารถติดตั้งได้ผ่าน pip:

```bash
pip install aspose-ocr
```

> **เคล็ดลับ:** ใช้ virtual environment (`python -m venv venv`) เพื่อให้การจัดการ dependencies เป็นระเบียบ

เมื่อแพ็กเกจติดตั้งเสร็จ คุณพร้อมที่จะ import และเริ่มต้น OCR engine นี่คือพื้นฐานของทุก workflow **ocr pdf with python** ที่คุณจะสร้างต่อไป

## OCR PDF ด้วย Python – การ import Aspose OCR

ตอนนี้ไลบรารีพร้อมใช้งานแล้ว มา import เข้ามาในสคริปต์ของเรา เราจะตั้งค่า engine ให้ทำงานใน *direct PDF mode* ซึ่งบอก Aspose ให้อ่านไบต์ของ PDF ตรงจากไฟล์โดยไม่ต้องแปลงแต่ละหน้าเป็นรูปก่อน

```python
# Step 1: Import the Aspose OCR module
import aspose.ocr as aocr

# Step 2: Create an OCR engine instance and enable direct PDF processing
ocr_engine = aocr.OcrEngine()
ocr_engine.pdf_mode = aocr.PdfMode.DIRECT
```

ทำไมต้องใช้ `PdfMode.DIRECT`? เพราะมันข้ามขั้นตอน rasterization เพิ่มเติม ทำให้กระบวนการเร็วขึ้นและคงรูปแบบต้นฉบับไว้—เป็นประโยชน์อย่างยิ่งเมื่อคุณต้อง **recognize text from PDF** อย่างแม่นยำ

## จดจำข้อความจาก PDF – การรัน Engine

เมื่อ engine พร้อมแล้ว ให้ชี้ไปที่ไฟล์ที่สแกนของคุณ เมธอด `recognize_from_pdf` จะทำงานหนักทั้งหมด: แยกแต่ละหน้า, รันอัลกอริทึม OCR, และคืนค่าเป็นอ็อบเจ็กต์ `OcrResult` ที่มีคอลเลกชันของอ็อบเจ็กต์ `Page`

```python
# Step 3: Define the path to the PDF you want to process
input_pdf_path = "YOUR_DIRECTORY/input.pdf"

# Step 4: Perform OCR on the PDF and obtain the result object
ocr_result = ocr_engine.recognize_from_pdf(input_pdf_path)
```

หากคุณสงสัยว่าใช้งานกับ PDF ที่เข้ารหัสได้หรือไม่—ใช่, เพียงใส่รหัสผ่านผ่าน `ocr_engine.password = "secret"` ก่อนเรียก `recognize_from_pdf` นั่นคือกรณีขอบที่หลายบทเรียนมักมองข้าม แต่จริง ๆ แล้วมีประโยชน์ในสายงานจริง

## ดึงข้อความจาก PDF – การเข้าถึงผลลัพธ์ของหน้า

รายการ `ocr_result.pages` จะเก็บรายการหนึ่งรายการต่อหน้า แต่ละอ็อบเจ็กต์ `Page` มีแอตทริบิวต์ `.text` ที่บรรจุข้อความแบบ plain‑text ของหน้าที่สแกน มา loop ผ่านและพิมพ์ผลลัพธ์เพื่อให้คุณเห็นว่ามีอะไรถูกดึงออกมาบ้าง

```python
# Step 5: Iterate through each page and display the recognized text
print("PDF OCR complete. Text per page:")
for page_index, page in enumerate(ocr_result.pages):
    print(f"--- Page {page_index + 1} ---")
    print(page.text)
```

การรันสคริปต์จะให้ผลลัพธ์ประมาณนี้:

```
PDF OCR complete. Text per page:
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

ผลลัพธ์นี้พิสูจน์ว่าคุณได้ **extract text from PDF** และ **recognize text from PDF** ด้วย Aspose OCR สำเร็จแล้ว คุณสามารถส่งสตริงเหล่านี้ต่อไปยังฐานข้อมูล, ดัชนีการค้นหา, หรือ pipeline NLP ใด ๆ ก็ได้

![ตัวอย่างการทำ ocr pdf](placeholder-image.png "ตัวอย่างการทำ ocr pdf")

*ข้อความแทนรูป:* **ตัวอย่างการทำ ocr pdf** – แสดงผลลัพธ์บนคอนโซลของข้อความที่จดจำได้ต่อหน้า

## แปลง PDF ที่สแกนเป็นข้อความ – การบันทึกผลลัพธ์

นักพัฒนาส่วนใหญ่ไม่ต้องการเพียงแค่ดูข้อความบนคอนโซล; พวกเขาต้องการไฟล์ที่คงอยู่ ด้านล่างเป็นฟังก์ชันช่วยเหลือขนาดเล็กที่เขียนข้อความของแต่ละหน้าไปยังไฟล์ `.txt` แยกกัน ทำให้ **convert scanned PDF to text** ลงในโฟลเดอร์ชื่อ `output`

```python
import os

output_dir = "output_text"
os.makedirs(output_dir, exist_ok=True)

for i, page in enumerate(ocr_result.pages, start=1):
    txt_path = os.path.join(output_dir, f"page_{i}.txt")
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(page.text)
    print(f"Saved page {i} text to {txt_path}")
```

เมื่อสคริปต์ทำงานเสร็จคุณจะได้โครงสร้างโฟลเดอร์ที่เป็นระเบียบ:

```
output_text/
│─ page_1.txt
│─ page_2.txt
└─ …
```

ตอนนี้คุณได้ **convert scanned PDF to text** อย่างครบถ้วนและสามารถนำไฟล์เหล่านี้ไปใช้ในกระบวนการต่อไปได้—การค้นหา, การวิเคราะห์, หรือแม้กระทั่ง `grep` ธรรมดา

## คำถามทั่วไป & กรณีขอบ

**ถ้า PDF ของฉันมีรูปภาพผสมกับข้อความจริงล่ะ?**  
Aspose OCR จะพยายามจดจำทุกอย่าง แต่คุณสามารถเร่งความเร็วได้โดยปิดการทำ OCR สำหรับหน้าที่มีข้อความที่เลือกได้อยู่แล้ว ตั้งค่า `ocr_engine.auto_detect_page_orientation = True` แล้วเรียก `ocr_engine.recognize_from_pdf(..., detect_text=False)` สำหรับหน้าที่รู้ว่ามีข้อความเลือกได้

**ฉันสามารถควบคุมโมเดลภาษาได้หรือไม่?**  
ทำได้เลย ตั้งค่า `ocr_engine.language = aocr.Language.English` (หรือภาษาอื่นที่รองรับ) ก่อนเรียก `recognize_from_pdf` จะช่วยเพิ่มความแม่นยำสำหรับเอกสารที่ไม่ใช่ภาษาอังกฤษ

**จะจัดการกับ PDF ขนาดใหญ่มาก (100+ หน้า) อย่างไร?**  
แบ่งเป็นส่วน ๆ เมธอด `recognize_from_pdf` รองรับอาร์กิวเมนต์ `page_range` เช่น `ocr_engine.recognize_from_pdf(path, page_range=(1, 20))` ทำ loop ตามช่วงเพื่อให้การใช้หน่วยความจำน้อยลง

## ตัวอย่างทำงานเต็มรูปแบบ

รวมทุกอย่างเข้าด้วยกัน นี่คือสคริปต์เดียวที่คุณสามารถบันทึกเป็นไฟล์ `ocr_pdf.py` แล้วรันได้:

```python
import os
import aspose.ocr as aocr

# -------------------------------------------------
# 1️⃣  Initialize the OCR engine (direct PDF mode)
# -------------------------------------------------
ocr_engine = aocr.OcrEngine()
ocr_engine.pdf_mode = aocr.PdfMode.DIRECT
# Optional: set language for better accuracy
ocr_engine.language = aocr.Language.English

# -------------------------------------------------
# 2️⃣  Path to the scanned PDF you want to process
# -------------------------------------------------
input_pdf_path = "YOUR_DIRECTORY/input.pdf"

# -------------------------------------------------
# 3️⃣  Run OCR – this is where we actually recognize text from PDF
# -------------------------------------------------
ocr_result = ocr_engine.recognize_from_pdf(input_pdf_path)

# -------------------------------------------------
# 4️⃣  Print the extracted text (shows how to extract text from PDF)
# -------------------------------------------------
print("PDF OCR complete. Text per page:")
for page_index, page in enumerate(ocr_result.pages):
    print(f"--- Page {page_index + 1} ---")
    print(page.text)

# -------------------------------------------------
# 5️⃣  Save each page as a .txt file (convert scanned PDF to text)
# -------------------------------------------------
output_dir = "output_text"
os.makedirs(output_dir, exist_ok=True)

for i, page in enumerate(ocr_result.pages, start=1):
    txt_path = os.path.join(output_dir, f"page_{i}.txt")
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(page.text)
    print(f"Saved page {i} text to {txt_path}")
```

รันด้วยคำสั่ง:

```bash
python ocr_pdf.py
```

คุณจะเห็นผลลัพธ์บนคอนโซลที่ยืนยันข้อความของแต่ละหน้าและตำแหน่งของไฟล์ `.txt` ที่บันทึกไว้

## สรุป

เราได้ครอบคลุม **วิธีทำ OCR PDF** ด้วย Python, แสดงวิธี **ocr pdf with python** อย่างสะอาด, สอน **extract text from PDF**, อธิบายกลไกของ **recognize text from PDF**, และสุดท้ายให้โค้ดพร้อมใช้ที่ **convert scanned PDF to text** ทั้งหมดนี้ถูกห่อหุ้มไว้ในขั้นตอนเดียว

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}