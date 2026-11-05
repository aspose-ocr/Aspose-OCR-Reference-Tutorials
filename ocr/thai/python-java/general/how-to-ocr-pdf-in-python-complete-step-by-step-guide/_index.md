---
category: general
date: 2026-06-06
description: วิธีทำ OCR PDF ด้วย Python, ดึงข้อความจาก PDF, แปลงข้อความจาก PDF ที่สแกน,
  และเปลี่ยนภาษาของ OCR เพียงไม่กี่บรรทัดของโค้ด.
draft: false
keywords:
- how to ocr pdf
- extract text from pdf
- convert scanned pdf text
- perform ocr on pdf
- change ocr language
language: th
og_description: 'วิธีทำ OCR PDF ด้วย Python: คู่มือปฏิบัติที่แสดงวิธีดึงข้อความจาก
  PDF, แปลงข้อความจาก PDF สแกน, และเปลี่ยนภาษาของ OCR อย่างง่ายดาย.'
og_title: วิธีทำ OCR PDF ด้วย Python – บทเรียนการเขียนโปรแกรมเต็มรูปแบบ
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to OCR PDF using Python, extract text from PDF, convert scanned
    PDF text, and change OCR language in just a few lines of code.
  headline: How to OCR PDF in Python – Complete Step‑by‑Step Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF processing
title: วิธีทำ OCR PDF ด้วย Python – คู่มือขั้นตอนเต็มครบถ้วน
url: /th/python-java/general/how-to-ocr-pdf-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีทำ OCR PDF ด้วย Python – คู่มือขั้นตอนเต็ม

เคยสงสัย **วิธีทำ OCR PDF** โดยไม่ต้องจ่ายค่าใช้จ่ายสูงของเครื่องมือ SaaS หรือไม่? คุณไม่ได้เป็นคนเดียว ไม่ว่าคุณจะกำลังดิจิไทซ์หนังสือเก่า ดึงข้อมูลจากใบแจ้งหนี้ หรือแค่ต้องการข้อความที่ค้นหาได้จากรายงานสแกน การเชี่ยวชาญ OCR PDF ด้วย Python สามารถช่วยคุณประหยัดเวลาการคัดลอกด้วยมือหลายชั่วโมงได้

ในบทเรียนนี้เราจะพาคุณผ่านตัวอย่างสั้น ๆ ที่ทำงานได้จริง ซึ่ง **ดึงข้อความจาก PDF** แสดงวิธี **แปลงข้อความ PDF ที่สแกน** ให้เป็นสตริงที่แก้ไขได้ และแม้แต่สาธิตวิธี **เปลี่ยนภาษาของ OCR** หากเอกสารของคุณไม่ได้เป็นภาษาอังกฤษ เมื่อจบคุณจะได้โค้ดสแนปที่สามารถนำไปใช้ในโปรเจกต์ใดก็ได้

## ข้อกำหนดเบื้องต้น & การตั้งค่า

ก่อนที่เราจะเริ่มลงมือทำ โปรดตรวจสอบว่าคุณมี:

- Python 3.8+ ติดตั้งแล้ว (โค้ดทำงานบน 3.9, 3.10 และใหม่กว่า)
- แพคเกจ `ocr` ที่ให้คลาส `OcrEngine` (คุณสามารถติดตั้งได้ด้วย `pip install ocr-lib` – แทนที่ด้วยชื่อแพคเกจจริงที่คุณใช้)
- ไฟล์ PDF ที่ต้องการประมวลผล; สำหรับการสาธิตเราจะใช้ `high_res_book.pdf` ที่อยู่ในโฟลเดอร์ชื่อ `YOUR_DIRECTORY`

หากคุณใช้ virtual environment (แนะนำอย่างยิ่ง) ให้เปิดใช้งานก่อน:

```bash
python -m venv .venv
source .venv/bin/activate   # on Windows: .venv\Scripts\activate
pip install ocr-lib
```

> **เคล็ดลับ:** เก็บไฟล์ PDF ของคุณไว้ในไดเรกทอรี `data/` เฉพาะเพื่อหลีกเลี่ยงปัญหาเกี่ยวกับเส้นทางในภายหลัง

## ขั้นตอนที่ 1: สร้างอินสแตนซ์ของ OCR Engine (How to OCR PDF – Initialization)

สิ่งแรกที่คุณต้องทำเมื่อ **ต้องการทำ OCR บนไฟล์ PDF** คือสร้างอินสแตนซ์ของเอนจิน คิดว่าเอนจินเป็นสมองที่จะอ่านแต่ละหน้า แปลอักขระ และส่งข้อความธรรมดากลับมาให้คุณ

```python
# Step 1: Create an OCR engine instance
engine = OcrEngine()
```

ทำไมจึงสำคัญ: หากไม่มีเอนจิน คุณจะไม่มีบริบทสำหรับการตั้งค่าภาษา ตัวเลือกการเรนเดอร์ หรือการจัดการ PDF `OcrEngine` จะเก็บค่าเริ่มต้นทั้งหมดเหล่านี้และให้คุณปรับแต่งได้ในภายหลัง

## ขั้นตอนที่ 2: ตั้งค่าภาษาในการรับรู้ (Change OCR Language)

ไลบรารี OCR ส่วนใหญ่ตั้งค่าเริ่มต้นเป็นภาษาอังกฤษ แต่ถ้าเอกสารของคุณเป็นภาษาฝรั่งเศส เยอรมัน หรือแม้แต่ญี่ปุ่น การเปลี่ยนภาษาก็ทำได้ง่ายโดยเรียก `set_recognition_language` ซึ่งตอบสนองต่อความต้องการ **เปลี่ยนภาษาของ OCR** และช่วยให้ความแม่นยำสูงขึ้น

```python
# Step 2: Set the recognition language to English (or any supported language)
engine.set_recognition_language(ocr.Language.ENGLISH)   # swap ENGLISH for FRANCAIS, etc.
```

> **เหตุผลที่คุณอาจต้องทำเช่นนี้:** คลังเอกสารหลายภาษามักมีหน้าที่ผสมภาษาต่าง ๆ การสลับภาษาแบบไดนามิกช่วยป้องกันการรับรู้อักขระผิดพลาด เช่น “ß” หรือ “ñ”

## ขั้นตอนที่ 3: กำหนดตัวเลือกการเรนเดอร์ PDF (Convert Scanned PDF Text Effectively)

เมื่อทำงานกับ PDF ที่สแกน ความละเอียดและโหมดสีมีผลอย่างมากต่อคุณภาพ OCR การเรนเดอร์ที่ 300 DPI ในโหมด grayscale เป็นจุดที่เหมาะสมสำหรับเอกสารส่วนใหญ่—ละเอียดพอที่จะจับรายละเอียด แต่ไม่สูงเกินไปจนใช้หน่วยความจำมาก

```python
# Step 3: Configure PDF rendering options (300 DPI, grayscale)
engine.pdf_render_options() \
      .set_dpi(300) \
      .set_color_mode("grayscale")
```

การเรียกต่อกันอาจดูหรูหรา แต่จริง ๆ แล้วเป็น Fluent API ที่คืนค่าอ็อบเจกต์ options เดียวกันทุกครั้ง หากคุณต้องการสี (เช่น สำหรับแผนภาพสี) ให้เปลี่ยน `"grayscale"` เป็น `"color"`

## ขั้นตอนที่ 4: ทำการรับรู้ PDF และดึงข้อความหน้าที่ 1 (Extract Text from PDF)

ตอนนี้มาถึงหัวใจของ **วิธีทำ OCR PDF**: ส่งเส้นทางไฟล์ให้เอนจินและดึงข้อความที่รับรู้ได้ วิธีนี้จะคืนรายการผลลัพธ์ของแต่ละหน้า; แต่ละผลลัพธ์มีแอตทริบิวต์ `text`

```python
# Step 4: Recognize the PDF and print the text of the first page
results = engine.recognize_pdf("YOUR_DIRECTORY/high_res_book.pdf")
print(results[0].text)   # Text from the first page
```

หากต้องการข้อความของทั้งเอกสาร ให้วนลูปผ่าน `results`:

```python
for i, page in enumerate(results, start=1):
    print(f"--- Page {i} ---")
    print(page.text)
```

### ถ้า PDF ถูกเข้ารหัส?

บาง PDF มีการป้องกันด้วยรหัสผ่าน ในกรณีนั้นคุณสามารถส่งรหัสผ่านไปยัง `recognize_pdf` ได้:

```python
results = engine.recognize_pdf(
    "YOUR_DIRECTORY/secure_doc.pdf",
    password="mySecret123"
)
```

เอนจินจะถอดรหัสแบบเรียลไทม์ก่อนทำ OCR—ไม่ต้องทำขั้นตอนเพิ่มเติม

## ขั้นตอนที่ 5: การทำ Post‑Processing ข้อความที่ดึงมา (Fine‑Tuning Extract Text from PDF)

ผลลัพธ์ OCR ดิบมักมีการขึ้นบรรทัดใหม่ ช่องว่างเกิน หรืออักขระที่รับรู้ผิดพลาดบ้าง การทำความสะอาดอย่างรวดเร็วจะทำให้สตริงที่ดึงมาพร้อมสำหรับการประมวลผลต่อ (เช่น การทำดัชนีการค้นหา การเก็บลงฐานข้อมูล ฯลฯ)

```python
import re

def clean_ocr_text(raw: str) -> str:
    # Remove multiple spaces and line breaks
    text = re.sub(r'\s+', ' ', raw)
    # Strip leading/trailing whitespace
    return text.strip()

clean_text = clean_ocr_text(results[0].text)
print(clean_text)
```

ตอนนี้คุณสามารถ **ดึงข้อความจาก PDF** อย่างปลอดภัยและส่งต่อไปยัง pipeline NLP, เครื่องมือค้นหา, หรือแม้กระทั่งการเขียนไฟล์ด้วย `open(...).write()`

## โบนัส: การประมวลผลหลาย PDF พร้อมกัน (Scaling Perform OCR on PDF)

หากคุณมีโฟลเดอร์เต็มไปด้วย PDF ที่สแกน ให้ห่อโค้ดไว้ในลูป:

```python
import pathlib

pdf_folder = pathlib.Path("YOUR_DIRECTORY")
for pdf_path in pdf_folder.glob("*.pdf"):
    print(f"Processing {pdf_path.name} …")
    pages = engine.recognize_pdf(str(pdf_path))
    full_text = "\n".join(page.text for page in pages)
    cleaned = clean_ocr_text(full_text)

    # Save the extracted text alongside the PDF
    txt_path = pdf_path.with_suffix(".txt")
    txt_path.write_text(cleaned, encoding="utf-8")
    print(f"Saved extracted text to {txt_path.name}")
```

สแนปนี้แสดงวิธี **ทำ OCR บนไฟล์ PDF** เป็นชุดจำนวนมาก ซึ่งเป็นความต้องการทั่วไปสำหรับโครงการดิจิไทซ์

## ผลลัพธ์ที่คาดหวัง

การรันตัวอย่างหน้าเดียว (ขั้นตอน 4) ควรพิมพ์ข้อความประมาณนี้:

```
In the beginning God created the heavens and the earth. Now the earth was formless …
```

หากคุณประมวลผลหนังสือหลายหน้า คอนโซลจะแสดงข้อความที่ทำความสะอาดแล้วของแต่ละหน้า และสคริปต์แบชจะสร้างไฟล์ `.txt` ข้าง ๆ ทุกไฟล์ PDF

## ข้อผิดพลาดทั่วไป & วิธีหลีกเลี่ยง

| ปัญหา | อาการ | วิธีแก้ |
|-------|----------|-----|
| PDF ต้นฉบับความละเอียดต่ำ | ตัวอักษรแสดงเป็นอักขระผิด, คำหาย | เพิ่ม DPI (`set_dpi(400)` หรือสูงกว่า) |
| ตั้งค่าภาษาไม่ถูกต้อง | มีสัญลักษณ์ไม่รู้จักจำนวนมาก, โดยเฉพาะอักขระมีสำเนียง | ใช้ `engine.set_recognition_language(ocr.Language.FRENCH)` หรือ enum ที่เหมาะสม |
| PDF ขนาดใหญ่ทำให้เกิด MemoryError | `MemoryError` หรือแอปพังหลังจากหลายหน้า | ประมวลผลหน้าเป็นชิ้น (`engine.recognize_pdf(..., max_pages=10)`) |
| ฟอนต์หายใน PDF | ผลลัพธ์เป็นค่าว่างสำหรับบางหน้า | ตรวจสอบว่า PDF มีภาพ raster จริง; PDF บางไฟล์เป็น vector‑only และต้องการการจัดการแบบอื่น |

## ภาพประกอบ

ด้านล่างเป็นภาพแสดงขั้นตอนการทำงานอย่างรวดเร็ว ข้อความ alt ถูกออกแบบให้เป็น SEO‑friendly

![วิธีทำ OCR PDF workflow diagram แสดงการเริ่มต้นเอนจิน, การตั้งค่าภาษา, ตัวเลือกการเรนเดอร์, การรับรู้, และการดึงข้อความ](/images/ocr-workflow.png)

*แผนภาพนี้ไม่จำเป็นต่อการรันโค้ด แต่ช่วยให้ผู้เรียนที่ชอบภาพเห็นภาพรวมของแต่ละขั้นตอนได้ชัดเจนขึ้น*

## สรุป

เราได้ครอบคลุม **วิธีทำ OCR PDF** ด้วย Python ตั้งแต่การสร้าง OCR engine, **การเปลี่ยนภาษาของ OCR**, การตั้งค่าการเรนเดอร์เพื่อ **แปลงข้อความ PDF ที่สแกน**, และสุดท้าย **การดึงข้อความจาก PDF** เพื่อใช้งานต่อ ตัวอย่างเต็มที่พร้อมรันพร้อมใช้งานในโปรเจกต์ใดก็ได้ และสคริปต์แบชเสริมแสดงวิธีขยายโซลูชันให้รองรับหลายไฟล์

ต่อไปคุณอาจอยากสำรวจ:

- เพิ่ม **ทำ OCR บน PDF** สำหรับคลังเอกสารหลายภาษาโดยวนลูปผ่านรายการภาษา
- ผสานข้อความที่ดึงมาเข้ากับ Elasticsearch เพื่อการค้นหาแบบเต็มข้อความ
- ใช้ OCR สร้าง PDF ที่ค้นหาได้โดยฝังชั้นข้อความกลับเข้าไฟล์ต้นฉบับ (หลายไลบรารีมีเมธอด `save_as_searchable_pdf`)

ลองทดลอง ปรับค่า DPI หรือสลับไปใช้ backend OCR ตัวอื่นก็ได้ พื้นฐานยังคงเหมือนเดิมและคุณมีฐานที่มั่นคงสำหรับการต่อยอดต่อไป

ขอให้เขียนโค้ดสนุกและเอกสารสแกนของคุณกลายเป็นข้อมูลที่ค้นหาได้!

## คุณควรเรียนรู้อะไรต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอนเพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโปรเจกต์ของคุณ

- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}