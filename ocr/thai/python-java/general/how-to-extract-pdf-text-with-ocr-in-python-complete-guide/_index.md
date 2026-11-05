---
category: general
date: 2026-06-19
description: วิธีดึงข้อมูลจาก PDF ด้วย OCR ใน Python – บทเรียนทีละขั้นตอนที่ครอบคลุมการดึงข้อความจาก
  PDF, การจดจำข้อความจากภาพ, และตัวอย่าง OCR ด้วย Python
draft: false
keywords:
- how to extract pdf
- extract text from pdf
- recognize text from image
- ocr python example
- read pdf with ocr
language: th
og_description: วิธีดึงข้อมูลจาก PDF ด้วย OCR ใน Python. เรียนรู้การดึงข้อความจาก
  PDF, การจดจำข้อความจากภาพ, และดูตัวอย่าง OCR ด้วย Python อย่างครบถ้วน.
og_title: วิธีดึงข้อความจาก PDF ด้วย OCR ใน Python – คำแนะนำเต็ม
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to extract PDF using OCR in Python – step‑by‑step tutorial covering
    extract text from PDF, recognize text from image, and an OCR Python example.
  headline: How to Extract PDF Text with OCR in Python – Complete Guide
  type: TechArticle
- description: How to extract PDF using OCR in Python – step‑by‑step tutorial covering
    extract text from PDF, recognize text from image, and an OCR Python example.
  name: How to Extract PDF Text with OCR in Python – Complete Guide
  steps:
  - name: – Install the Required Packages
    text: First, we need an OCR engine. The example below uses the popular **ocr**
      package (a thin wrapper around Tesseract). If you prefer a different backend,
      the concepts stay the same.
  - name: – Initialize the OCR Engine and Set Language
    text: Now we spin up the engine and tell it to look for English characters. You
      can swap `ocr.Language.English` for any supported language code.
  - name: – Load a PDF Page as an Image
    text: OCR works on raster images, not PDF objects. The `ocr.Image.from_pdf` helper
      renders the chosen page to a bitmap. Adjust `page_number` for other pages (0‑based
      indexing).
  - name: – Recognize Text from the Rendered Image
    text: Here’s the heart of the **ocr python example**. The engine processes the
      bitmap and returns an object containing the extracted string.
  - name: – Print or Store the Extracted Text
    text: Finally, we output the result. In a real application you’d probably write
      to a file or a database.
  type: HowTo
tags:
- OCR
- Python
- PDF
- Text Extraction
title: วิธีดึงข้อความจาก PDF ด้วย OCR ใน Python – คู่มือฉบับสมบูรณ์
url: /th/python-java/general/how-to-extract-pdf-text-with-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีดึงข้อความจาก PDF ด้วย OCR ใน Python – คู่มือฉบับสมบูรณ์

เคยสงสัย **วิธีดึงข้อความจาก PDF** เมื่อไฟล์เป็นเพียงภาพสแกนหรือไม่? คุณไม่ได้เป็นคนเดียว ในหลายโครงการจริง—เช่น สัญญา ใบแจ้งหนี้ หรือเอกสารประวัติศาสตร์—PDF ที่คุณได้รับไม่มีข้อความที่เลือกได้ ข่าวดีคือ? เพียงไม่กี่บรรทัดของ Python ก็สามารถเปลี่ยนหน้าที่เป็นภาพอย่างเดียวให้กลายเป็นข้อความที่ค้นหาและแก้ไขได้

ในบทเรียนนี้เราจะเดินผ่าน **ตัวอย่าง OCR Python** ที่อ่าน PDF, แปลงหน้าหนึ่งเป็นภาพ, แล้ว **ดึงข้อความจาก PDF** ด้วยเครื่องมือ OCR. เมื่อจบคุณจะรู้วิธี **อ่าน PDF ด้วย OCR** อย่างแม่นยำ ทำไมขั้นตอนแต่ละขั้นตอนสำคัญ และจะปรับโค้ดให้รองรับเอกสารหลายหน้า หรือหลายภาษาอย่างไร

## สิ่งที่คุณจะได้เรียน

- ติดตั้งและตั้งค่าไลบรารี OCR ที่เชื่อถือได้สำหรับ Python  
- แปลงหน้าของ PDF เป็นภาพที่เหมาะกับ OCR  
- **จดจำข้อความจากภาพ** และรับสตริง Unicode ที่สะอาด  
- ปัญหาที่พบบ่อย (PDF ความละเอียดต่ำ, หน้าเอียง) และวิธีหลีกเลี่ยง  
- ขยายสคริปต์เพื่อจัดการหลายหน้า หรือประมวลผลเป็นชุด

**ข้อกำหนดเบื้องต้น**: Python 3.8+, pip, และความเข้าใจพื้นฐานเกี่ยวกับ virtual environment ไม่จำเป็นต้องมีประสบการณ์ OCR มาก่อน—เพียงทำตามขั้นตอน

---

## ## วิธีดึงข้อความจาก PDF ด้วย OCR ใน Python

หัวข้อ H2 นี้มีคีย์เวิร์ดหลักของเราตรงที่เครื่องมือค้นหาชอบเห็น ไปดิ่งสู่โค้ดกันเลย

### ขั้นตอนที่ 1 – ติดตั้งแพ็กเกจที่จำเป็น

ก่อนอื่นเราต้องมีเครื่องมือ OCR ตัวอย่างด้านล่างใช้แพ็กเกจ **ocr** ที่เป็น wrapper บาง ๆ ของ Tesseract หากคุณชอบ backend อื่น แนวคิดยังคงเหมือนเดิม

```bash
# Create a fresh virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate

# Install the OCR wrapper and Pillow for image handling
pip install ocr pillow
```

> **เคล็ดลับ:** บน Linux คุณยังต้องติดตั้งไบนารีของ Tesseract ด้วย: `sudo apt-get install tesseract-ocr` ผู้ใช้ macOS สามารถติดตั้งผ่าน Homebrew: `brew install tesseract`

### ขั้นตอนที่ 2 – เริ่มต้นเครื่องมือ OCR และกำหนดภาษา

ตอนนี้เราจะสตาร์ท engine และบอกให้มองหาตัวอักษรภาษาอังกฤษ คุณสามารถสลับ `ocr.Language.English` ไปเป็นโค้ดภาษาที่รองรับอื่นได้

```python
import ocr

# Step 1: Create an OCR engine and set the language to English
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.English
```

**ทำไมขั้นตอนนี้สำคัญ:** การระบุภาษาอย่างชัดเจนช่วยเพิ่มความแม่นยำอย่างมาก เพราะ engine สามารถใช้พจนานุกรมและโมเดลอักขระเฉพาะภาษา

### ขั้นตอนที่ 3 – โหลดหน้า PDF เป็นภาพ

OCR ทำงานกับภาพ raster ไม่ใช่วัตถุ PDF `ocr.Image.from_pdf` helper จะเรนเดอร์หน้าที่เลือกเป็นบิตแมพ ปรับ `page_number` เพื่อเลือกหน้าอื่น (เริ่มจาก 0)

```python
# Step 2: Load the first page of the PDF as an image
pdf_file_path = "YOUR_DIRECTORY/contract.pdf"
page_image = ocr.Image.from_pdf(pdf_file_path, page_number=1)
```

> **กรณีขอบ:** หาก PDF มีกราฟิกเวกเตอร์แทนภาพสแกน คุณอาจได้การเรนเดอร์ที่คมชัด สำหรับสแกนความละเอียดต่ำ ให้เพิ่ม DPI: `ocr.Image.from_pdf(..., dpi=300)`

### ขั้นตอนที่ 4 – จดจำข้อความจากภาพที่เรนเดอร์แล้ว

นี่คือหัวใจของ **ocr python example** engine จะประมวลผลบิตแมพและคืนอ็อบเจกต์ที่มีสตริงที่ดึงออกมา

```python
# Step 3: Recognize text from the rendered page image
ocr_result = ocr_engine.recognize(page_image)
```

แอตทริบิวต์ `ocr_result.text` จะเก็บผลลัพธ์เป็น plain‑text พร้อมรักษาการขึ้นบรรทัดเมื่อเป็นไปได้

### ขั้นตอนที่ 5 – พิมพ์หรือบันทึกข้อความที่ดึงได้

สุดท้ายเราจะแสดงผลลัพธ์ ในแอปพลิเคชันจริงคุณอาจเขียนลงไฟล์หรือฐานข้อมูล

```python
# Step 4: Print the extracted text
print(ocr_result.text)
```

การรันสคริปต์ควรแสดงผลประมาณนี้:

```
THIS AGREEMENT is made on the 1st day of January 2024...
```

นี่คือเวิร์กโฟลว์ **extract text from pdf** แบบครบวงจรด้วย OCR

---

## ## จดจำข้อความจากภาพ – ปรับความแม่นยำ

หากคุณสนใจเพียง **จดจำข้อความจากภาพ** (เช่น JPEG ของใบเสร็จ) คุณสามารถข้ามขั้นตอนแปลง PDF ได้:

```python
image_path = "receipt.jpg"
page_image = ocr.Image.from_file(image_path)   # Directly load an image
ocr_result = ocr_engine.recognize(page_image)
print(ocr_result.text)
```

**เคล็ดลับเพื่อผลลัพธ์ที่ดีกว่า:**

- **Pre‑process** ภาพ: แปลงเป็น grayscale, ใช้ thresholding, หรือ deskew. Pillow ทำได้ง่าย
- **Increase DPI** ระหว่างการเรนเดอร์ PDF: ความละเอียดสูงให้รายละเอียดมากขึ้นกับ OCR engine
- **Enable OCR engine’s config** สำหรับการแบ่งหน้า (`ocr_engine.config = "--psm 6"` สำหรับบล็อกที่สม่ำเสมอ)

---

## ## อ่าน PDF ด้วย OCR – จัดการหลายหน้า

สัญญาส่วนใหญ่มีหลายหน้า การวนลูปแต่ละหน้าเป็นเรื่องง่าย:

```python
def extract_all_pages(pdf_path):
    all_text = []
    for i in range(ocr.Image.pdf_page_count(pdf_path)):
        img = ocr.Image.from_pdf(pdf_path, page_number=i)
        result = ocr_engine.recognize(img)
        all_text.append(result.text)
    return "\n--- PAGE BREAK ---\n".join(all_text)

full_text = extract_all_pages("YOUR_DIRECTORY/contract.pdf")
print(full_text)
```

ฟังก์ชันนี้ **reads PDF with OCR**, รวมผลลัพธ์เข้าด้วยกันและแทรกเครื่องหมายแบ่งหน้าอย่างชัดเจน จากนั้นคุณสามารถส่ง `full_text` ไปยังดัชนีการค้นหา หรือบันทึกเป็นไฟล์ `.txt`

---

## ## ปัญหาที่พบบ่อยและวิธีแก้

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| ตัวอักษรแปลก ๆ, มี `?` มาก | ภาษาไม่ถูกต้องหรือไม่มีไฟล์ข้อมูลภาษา | ติดตั้งแพ็ก Tesseract ภาษาที่ตรง (`tesseract-ocr-<lang>`) และตั้ง `ocr_engine.language` |
| ขาดบรรทัดหรือคำตัด | DPI ต่ำ (ต่ำกว่า 150) | เรนเดอร์ PDF ที่ 300 DPI หรือสูงกว่า (`dpi=300`) |
| ข้อความเอียงหรือหัวกลับ | หน้าสแกนไม่อยู่ในแนวตั้ง | ใช้ `ocr.Image.deskew(page_image)` ก่อนจดจำ |
| ประมวลผลช้าใน PDF ขนาดใหญ่ | ประมวลผลหน้าแบบต่อเนื่องในเธรดเดียว | ทำ parallel ด้วย `concurrent.futures.ThreadPoolExecutor` |

---

## ## ขยายตัวอย่าง OCR Python

- **Export to PDF/A**: หลังจากดึงข้อความแล้ว คุณสามารถฝังข้อความกลับเข้า PDF ที่ค้นหาได้ด้วย `reportlab` หรือ `pypdf2`
- **ตรวจจับภาษา**: ใช้ `langdetect` กับผลลัพธ์ OCR เพื่อสลับ `ocr_engine.language` แบบไดนามิก
- **ประมวลผลเป็นชุด**: เดินสำรวจโฟลเดอร์ด้วย `os.listdir` แล้วเรียก `extract_all_pages` กับทุกไฟล์

---

## ## ผลลัพธ์ที่คาดหวังและการตรวจสอบ

เมื่อคุณรันสคริปต์กับสแกนภาษาอังกฤษที่ชัดเจน ควรเห็นบล็อกข้อความที่สะอาดและมีเครื่องหมายวรรคตอนที่ถูกต้อง ตรวจสอบโดย:

1. เปรียบเทียบบรรทัดบางบรรทัดกับภาพสแกนต้นฉบับ  
2. รันการนับคำง่าย ๆ (`len(ocr_result.text.split())`) เพื่อให้แน่ใจว่าผลลัพธ์ไม่ว่างเปล่า  
3. ทางเลือก, ส่งผลลัพธ์ไปยัง spell‑checker อย่าง `pyspellchecker` เพื่อตรวจจับข้อผิดพลาดของ OCR

---

## สรุป

เราได้อธิบาย **วิธีดึงข้อความจาก PDF** เมื่อการแยกข้อมูลแบบดั้งเดิมล้มเหลว, แสดง **ocr python example** แบบเต็ม, และอธิบายวิธี **จดจำข้อความจากภาพ** และ **อ่าน PDF ด้วย OCR** ทั้งในกรณีหน้าเดียวและหลายหน้า ด้วยโค้ดตัวอย่างข้างต้น คุณสามารถแปลง PDF สแกนใด ๆ ให้เป็นข้อความที่ค้นหาและแก้ไขได้—ไม่ต้องพิมพ์ใหม่อีกต่อไป

ขั้นตอนต่อไป? ลองสลับภาษาเป็นสเปน (`ocr.Language.Spanish`) หรือทดลองเทคนิคการพรี‑โปรเซสภาพเพื่อเพิ่มความแม่นยำ หากคุณกำลังสร้างระบบจัดการเอกสาร, พิจารณาดัชนีข้อความที่ดึงได้ด้วย Elasticsearch เพื่อการค้นหาเร็วแสง

มีคำถามหรือเจอ PDF ที่แปลกประหลาด? แสดงความคิดเห็นได้เลย, Happy coding!  

![วิธีดึงข้อความจาก PDF ด้วย OCR ใน Python](image.png "วิธีดึงข้อความจาก PDF ด้วย OCR ใน Python")


## สิ่งที่คุณควรเรียนต่อไป

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคในคู่มือนี้ แต่ละแหล่งรวมโค้ดทำงานครบถ้วนพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโครงการของคุณ

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}