---
category: general
date: 2026-06-22
description: เรียนรู้วิธีทำ OCR ไฟล์ PDF ด้วย Python, ดึงข้อความจาก PDF, และแปลง PDF
  เป็นข้อความโดยใช้วิธีการแบบสตรีม ขั้นตอนง่าย ๆ สำหรับการประมวลผล PDF ที่สแกน.
draft: false
keywords:
- how to ocr pdf
- extract text from pdf
- convert pdf to text
- load pdf from stream
- process scanned pdf
language: th
og_description: วิธีทำ OCR ไฟล์ PDF ด้วย Python? ทำตามคำแนะนำนี้เพื่อดึงข้อความจาก
  PDF, แปลง PDF เป็นข้อความ, และประมวลผล PDF สแกนโดยใช้สตรีม.
og_title: วิธีทำ OCR PDF ด้วย Python – คู่มือขั้นตอนโดยละเอียด
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Learn how to OCR PDF files in Python, extract text from PDF, and convert
    PDF to text using a stream‑based approach. Simple steps for processing scanned
    PDF.
  headline: How to OCR PDF in Python – Complete Guide to Extract Text from PDFs
  type: TechArticle
- description: Learn how to OCR PDF files in Python, extract text from PDF, and convert
    PDF to text using a stream‑based approach. Simple steps for processing scanned
    PDF.
  name: How to OCR PDF in Python – Complete Guide to Extract Text from PDFs
  steps:
  - name: Expected Output
    text: 'If `multipage.pdf` contains three scanned pages, you’ll see something like:'
  - name: 1. PDFs with Mixed Image and Text Layers
    text: 'Some PDFs already contain a hidden text layer (e.g., exported from Word).
      If you want the OCR engine to **ignore existing text** and re‑process the image,
      set:'
  - name: 2. Large Files Exceeding Memory Limits
    text: 'When working with gigabyte‑size PDFs, consider processing in chunks:'
  - name: 3. Language and Font Support
    text: 'If your scanned documents are in French or contain special characters,
      tell the engine which language model to use:'
  type: HowTo
tags:
- OCR
- Python
- PDF processing
title: วิธีทำ OCR PDF ด้วย Python – คู่มือครบวงจรสำหรับการดึงข้อความจาก PDF
url: /th/python-java/general/how-to-ocr-pdf-in-python-complete-guide-to-extract-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีทำ OCR PDF ด้วย Python – คู่มือครบวงจรสำหรับการสกัดข้อความจาก PDF

เคยสงสัย **วิธีทำ OCR PDF** ไฟล์โดยไม่ต้องต่อสู้กับเครื่องมือเดสก์ท็อปที่หนักหน่วงหรือไม่? คุณไม่ได้เป็นคนเดียว ในหลายโครงการจริง—เช่นการทำอัตโนมัติใบแจ้งหนี้หรือการแปลงสแกนเอกสารเก่าเป็นดิจิทัล—คุณต้องการวิธีที่เชื่อถือได้ในการแปลง PDF ที่สแกนเป็นข้อความที่สามารถค้นหาและแก้ไขได้

ในบทเรียนนี้เราจะพาคุณผ่านตัวอย่างที่สะอาดและครบวงจรซึ่ง **สกัดข้อความจาก PDF** หน้าโดยใช้เครื่องมือ OCR ของ Python ที่มีน้ำหนักเบา เมื่อจบคุณจะรู้วิธี **แปลง PDF เป็นข้อความ** อย่างแม่นยำ วิธี **โหลด PDF จากสตรีม** และวิธี **ประมวลผล PDF ที่สแกน** อย่างมีประสิทธิภาพ ไม่ต้องใช้เวทมนตร์ เพียงโค้ด Python ธรรมดาที่คุณสามารถนำไปใช้ในโปรเจคของคุณได้ทันที

## สิ่งที่คุณจะได้เรียนรู้

- ติดตั้งและกำหนดค่าไลบรารี OCR ของ Python ที่รองรับการรับ PDF เป็นอินพุต  
- เปิดใช้งานโหมดจดจำ PDF และตั้งค่ารูปแบบผลลัพธ์เป็นข้อความธรรมดา  
- โหลด PDF หลายหน้าจากสตรีมไฟล์ (รูปแบบ “โหลด PDF จากสตรีม” แบบคลาสสิก)  
- รัน OCR บนทุกหน้าและดึงเนื้อหาข้อความออกมา  
- พิมพ์หรือบันทึกผลลัพธ์เพื่อการประมวลผลต่อไป

**ข้อกำหนดเบื้องต้น**  
- มี Python 3.8+ ติดตั้งบนเครื่องของคุณ  
- คุ้นเคยพื้นฐานกับ pip และ virtual environment  
- มีไฟล์ PDF ที่สแกน (ชื่อ `multipage.pdf` ในตัวอย่าง) อยู่ในไดเรกทอรีที่รู้จัก

หากสิ่งใดในข้างต้นฟังดูแปลกใหม่ ไม่ต้องกังวล—แต่ละขั้นตอนจะอธิบายด้วยภาษาง่าย ๆ และเราจะให้คำสั่งที่คุณต้องใช้อย่างแม่นยำ

---

## ขั้นตอนที่ 1: ติดตั้ง OCR Engine (วิธีทำ OCR PDF)

ก่อนอื่นคุณต้องมี OCR engine ที่สามารถจัดการกับ PDF ได้ สำหรับคู่มือนี้เราจะใช้แพคเกจสมมติ `ocr` (API มีลักษณะคล้ายกับ SDK เชิงพาณิชย์ยอดนิยม แต่รูปแบบเดียวกันก็ใช้ได้กับ Tesseract‑OCR, ABBYY หรือ Google Vision เมื่อห่อหุ้มอย่างเหมาะสม)

```bash
# Create a virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate

# Install the OCR package
pip install ocr
```

> **เคล็ดลับ:** หากคุณใช้ Windows แล้วเจอข้อผิดพลาดเรื่องสิทธิ์ ให้ลองใช้ `pip install --user ocr` แทน

เมื่อติดตั้งแพคเกจแล้ว คุณสามารถนำเข้าในสคริปต์และสร้างอินสแตนซ์ของ engine—นี่คือหัวใจของ **วิธีทำ OCR PDF**

```python
import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

อ็อบเจ็กต์ `OcrEngine` จะเก็บการตั้งค่าต่าง ๆ ที่เราจะปรับในภายหลัง เช่น ภาษา, DPI, และ—ที่สำคัญ—โหมด PDF

---

## ขั้นตอนที่ 2: เปิดใช้งานการจดจำ PDF และเลือกรูปแบบผลลัพธ์ (สกัดข้อความจาก PDF)

โดยค่าเริ่มต้นหลาย SDK ของ OCR จะสมมติว่าคุณส่งภาพให้กับมัน เพื่อให้ engine ปฏิบัติต่อสตรีมที่เข้ามาเป็น PDF เราต้องเปิดแฟล็กการจดจำ PDF และขอผลลัพธ์เป็นข้อความธรรมดา

```python
# Step 2: Turn on PDF mode and request plain text results
settings = engine.get_settings()
settings.set_recognize_pdf(True)                     # tells the engine to parse PDF containers
settings.set_output_format(ocr.OutputFormat.TEXT)   # we want raw text, not XML or PDF
```

ทำไมต้องระบุรูปแบบผลลัพธ์? เพราะบาง engine สามารถคืนค่า PDF ที่มีเลเยอร์ข้อความซ่อนอยู่, PDF ที่ค้นหาได้, หรือ JSON ที่มีกรอบพิกัด หากคุณทำงานในสายการสกัดข้อมูล การ **สกัดข้อความจาก PDF** เป็นสตริงธรรมดาจะเป็นรูปแบบที่สะอาดที่สุดสำหรับขั้นตอนต่อไป

---

## ขั้นตอนที่ 3: โหลด PDF จากสตรีมไฟล์ (โหลด PDF จากสตรีม)

การโหลด PDF จากสตรีมเป็นรูปแบบที่ประหยัดหน่วยความจำ—you จะหลีกเลี่ยงการโหลดไฟล์ทั้งหมดเข้าสู่ RAM พร้อมกัน ซึ่งเป็นประโยชน์อย่างยิ่งเมื่อจัดการกับเอกสารหลายหน้าขนาดใหญ่

```python
# Step 3: Load the multi‑page PDF from a file stream
pdf_path = "YOUR_DIRECTORY/multipage.pdf"
pdf_stream = ocr.ImageStream.from_file(pdf_path)   # wraps the file handle in an OCR‑friendly object
engine.set_image(pdf_stream)
```

> **ไฟล์อยู่บน S3 หรือคลาวด์บัคเก็ตอื่น?**  
> เพียงเปลี่ยน `from_file` เป็นเมธอดที่รับบัฟเฟอร์ไบต์ (เช่น `ImageStream.from_bytes(s3_object.read())`) ส่วนที่เหลือของ pipeline จะยังคงเหมือนเดิม

---

## ขั้นตอนที่ 4: รัน OCR บนทุกหน้า (ประมวลผล PDF ที่สแกน)

ตอนนี้งานหนักเริ่มขึ้นแล้ว engine จะวนลูปผ่านทุกหน้า, รันการจดจำ, และคืนรายการอ็อบเจ็กต์หน้า—แต่ละอ็อบเจ็กต์จะเปิดเผยเนื้อหาข้อความของมัน

```python
# Step 4: Perform OCR on all pages of the PDF
pages = engine.recognize_pdf()
```

เบื้องหลัง OCR library จะทำการแตกข้อมูล PDF หน้าแต่ละหน้า, แปลงเป็น raster ที่ DPI ที่กำหนด, แล้วส่งบิตแมปผ่านโมเดล neural‑network ผลลัพธ์คือคอลเลกชันของอ็อบเจ็กต์ `Page` ที่พร้อมสำหรับการสกัด

---

## ขั้นตอนที่ 5: ดึงและแสดงข้อความที่จดจำได้ (แปลง PDF เป็นข้อความ)

สุดท้าย เราจะวนลูปผ่านหน้าแต่ละหน้าและพิมพ์ข้อความที่จดจำได้ นี่คือช่วงที่ **แปลง PDF เป็นข้อความ** เกิดขึ้นจริง ๆ

```python
# Step 5: Iterate through the recognized pages and display their text
for index, page in enumerate(pages):
    print(f"--- Page {index + 1} ---")
    print(page.get_text())
```

### ผลลัพธ์ที่คาดหวัง

หาก `multipage.pdf` มีสามหน้าที่สแกน คุณจะเห็นผลลัพธ์ประมาณนี้:

```
--- Page 1 ---
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
...

--- Page 2 ---
Item Description   Qty   Price
Widget A           10    $50.00
Widget B            5    $30.00
...

--- Page 3 ---
Thank you for your business!
```

สังเกตการแยกหน้าที่ชัดเจน—มีประโยชน์หากคุณต้องการเก็บข้อความของแต่ละหน้าในฐานข้อมูลหรือส่งต่อให้โมเดล NLP ขั้นต่อไป

---

## การจัดการกับกรณีขอบทั่วไป

### 1. PDF ที่มีเลเยอร์ภาพและข้อความผสม

บาง PDF มีเลเยอร์ข้อความซ่อนอยู่แล้ว (เช่นที่ส่งออกจาก Word) หากคุณต้องการให้ OCR engine **ละเว้นข้อความที่มีอยู่** และประมวลผลภาพใหม่ ให้ตั้งค่า:

```python
settings.set_force_ocr(True)   # forces rasterization and OCR even if text exists
```

### 2. ไฟล์ขนาดใหญ่เกินขีดจำกัดหน่วยความจำ

เมื่อทำงานกับ PDF ขนาดกิกะไบต์ ควรพิจารณาประมวลผลเป็นชิ้น ๆ:

```python
for page_number in range(1, engine.get_page_count() + 1):
    single_page_stream = engine.get_page_stream(page_number)
    engine.set_image(single_page_stream)
    page = engine.recognize_pdf()[0]   # only one page at a time
    print(f"--- Page {page_number} ---")
    print(page.get_text())
```

### 3. การสนับสนุนภาษาและฟอนต์

หากเอกสารที่สแกนเป็นภาษาฝรั่งเศสหรือมีอักขระพิเศษ ให้บอก engine ว่าจะใช้โมเดลภาษาใด:

```python
settings.set_language("fr")   # or "en", "de", etc.
```

---

## สคริปต์เต็ม – พร้อมรัน

ด้านล่างเป็นตัวอย่างที่สมบูรณ์และสามารถรันได้ ซึ่งรวมทุกส่วนเข้าด้วยกัน บันทึกเป็น `ocr_pdf.py` แล้วรันด้วยคำสั่ง `python ocr_pdf.py`

```python
import ocr

def main():
    # Initialize engine
    engine = ocr.OcrEngine()

    # Configure for PDF recognition and plain‑text output
    settings = engine.get_settings()
    settings.set_recognize_pdf(True)
    settings.set_output_format(ocr.OutputFormat.TEXT)

    # Optional: force OCR even if PDF already has text
    # settings.set_force_ocr(True)

    # Load PDF from a stream
    pdf_path = "YOUR_DIRECTORY/multipage.pdf"
    pdf_stream = ocr.ImageStream.from_file(pdf_path)
    engine.set_image(pdf_stream)

    # Perform OCR on every page
    pages = engine.recognize_pdf()

    # Output the results
    for idx, page in enumerate(pages):
        print(f"--- Page {idx + 1} ---")
        print(page.get_text())

if __name__ == "__main__":
    main()
```

**การรันสคริปต์** จะพิมพ์ข้อความของแต่ละหน้าออกที่คอนโซล เหมือนที่แสดงในส่วน “ผลลัพธ์ที่คาดหวัง” จากนั้นคุณสามารถเปลี่ยนการแสดงผลไปยังไฟล์ได้:

```bash
python ocr_pdf.py > extracted_text.txt
```

---

## สรุป

เราได้อธิบาย **วิธีทำ OCR PDF** ด้วย Python ตั้งแต่ต้นจนจบ โดยการกำหนดค่า engine, โหลดเอกสารผ่านสตรีม, และวนลูปผ่านแต่ละหน้าที่จดจำได้ คุณสามารถ **สกัดข้อความจาก PDF**, **แปลง PDF เป็นข้อความ**, และ **ประมวลผล PDF ที่สแกน** เพียงไม่กี่บรรทัด วิธีนี้สามารถขยายได้ตั้งแต่ใบแจ้งหนี้สองหน้าขนาดเล็กจนถึงคลังเอกสารหลายร้อยหน้าขนาดใหญ่

ต่อไปคุณอาจลองนำข้อความที่สกัดไปใส่ในดัชนีการค้นหา, สรุปด้วยโมเดลภาษา, หรือ pipeline ตรวจสอบข้อมูล คุณอาจทดลองใช้รูปแบบผลลัพธ์เช่น JSON เพื่อเก็บข้อมูลตำแหน่งสำหรับการวิเคราะห์เอกสารขั้นสูง

มีคำถามเกี่ยวกับการจัดการ PDF ที่เข้ารหัสหรือการเชื่อมต่อกับคลาวด์สตอเรจหรือไม่? แสดงความคิดเห็นด้านล่าง—ขอให้โค้ดสนุก!

![แผนภาพแสดงขั้นตอนการทำ OCR PDF – วิธีทำ OCR PDF, โหลด PDF จากสตรีม, จดจำหน้า, และสกัดข้อความ](ocr-pdf-workflow.png "แผนภาพขั้นตอนการทำ OCR PDF")

## สิ่งที่คุณควรเรียนต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานทางเลือกในโปรเจคของคุณเอง

- [วิธีทำ OCR PDF ด้วย .NET กับ Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [วิธีสกัดข้อความจากภาพด้วย Aspose.OCR สำหรับ .NET](/ocr/english/net/text-recognition/get-recognition-result/)
- [วิธีสกัดข้อความจากไฟล์ ZIP ด้วย Aspose.OCR สำหรับ .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}