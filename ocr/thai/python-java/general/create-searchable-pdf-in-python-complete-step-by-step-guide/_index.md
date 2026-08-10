---
category: general
date: 2026-06-19
description: สร้าง PDF ที่ค้นหาได้จากภาพโดยใช้ Python OCR. เรียนรู้วิธีแปลง OCR เป็น
  PDF, ดึงข้อความจากภาพ, และทำ OCR บนภาพอย่างรวดเร็ว.
draft: false
keywords:
- create searchable pdf
- convert ocr to pdf
- extract text from image
- convert image to pdf
- perform ocr on image
language: th
og_description: สร้างไฟล์ PDF ที่ค้นหาได้จากภาพด้วย Python OCR คู่มือนี้แสดงวิธีแปลง
  OCR เป็น PDF, ดึงข้อความจากภาพ, และทำ OCR บนภาพ.
og_title: สร้างไฟล์ PDF ที่ค้นหาได้ใน Python – คู่มือการเขียนโปรแกรมเต็มรูปแบบ
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Create searchable PDF from an image using Python OCR. Learn to convert
    OCR to PDF, extract text from image, and perform OCR on image quickly.
  headline: Create Searchable PDF in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Create searchable PDF from an image using Python OCR. Learn to convert
    OCR to PDF, extract text from image, and perform OCR on image quickly.
  name: Create Searchable PDF in Python – Complete Step‑by‑Step Guide
  steps:
  - name: The OCR confidence scores (`conf` values). Low confidence may mean the image
      is blurry.
    text: The OCR confidence scores (`conf` values). Low confidence may mean the image
      is blurry.
  - name: Bounding box coordinates—sometimes EasyOCR reports them in a different orientation.
    text: Bounding box coordinates—sometimes EasyOCR reports them in a different orientation.
  - name: That the PDF viewer isn’t set to “image‑only” mode (rare, but some viewers
      have that option).
    text: That the PDF viewer isn’t set to “image‑only” mode (rare, but some viewers
      have that option).
  type: HowTo
tags:
- OCR
- Python
- PDF
- ImageProcessing
title: สร้าง PDF ที่ค้นหาได้ใน Python – คู่มือขั้นตอนเต็มแบบครบถ้วน
url: /th/python-java/general/create-searchable-pdf-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง PDF ที่ค้นหาได้ใน Python – คู่มือขั้นตอนเต็ม

เคยต้องการ **สร้าง PDF ที่ค้นหาได้** จากใบเสร็จที่สแกน แต่ไม่แน่ใจว่าจะเริ่มต้นอย่างไรหรือไม่? คุณไม่ได้อยู่คนเดียว—นักพัฒนาหลายคนเจออุปสรรคเดียวกันเมื่อลองแปลงรูปภาพของข้อความเป็น PDF ที่คุณสามารถค้นหาได้จริง  

ในบทแนะนำนี้เราจะพาคุณผ่านโซลูชันเชิงปฏิบัติที่ทำให้คุณ **ทำ OCR บนภาพ**, แปลงผล OCR เป็น **PDF ที่ค้นหาได้**, และแม้กระทั่งดึงข้อความดิบออกมา หากคุณต้องการใช้ต่อในกระบวนการอื่น ๆ ไม่ต้องมีส่วนเกิน เพียงตัวอย่างทำงานที่คุณสามารถคัดลอก‑วางเข้าโปรเจกต์ของคุณได้ทันที

## สิ่งที่คุณจะได้เรียนรู้

- วิธีตั้งค่าเครื่อง OCR ที่มีน้ำหนักเบาใน Python  
- ขั้นตอนที่แน่นอนเพื่อ **แปลง OCR เป็น PDF** และบันทึกเป็นเอกสารที่ค้นหาได้  
- วิธี **ดึงข้อความจากภาพ** เพื่อการวิเคราะห์ต่อไป  
- เคล็ดลับการจัดการกับปัญหาทั่วไป เช่น การหมุนภาพและไฟล์ขนาดใหญ่  
- สคริปต์สมบูรณ์ที่สามารถรันได้และปรับใช้กับกรณีของคุณเอง

### ข้อกำหนดเบื้องต้น

- Python 3.8+ ติดตั้งบนเครื่องของคุณ  
- ความคุ้นเคยพื้นฐานกับ pip และ virtual environment (ไม่บังคับแต่แนะนำ)  
- ไฟล์ภาพ (PNG, JPEG, ฯลฯ) ที่มีข้อความที่อ่านได้ชัดเจน  

ถ้าคุณมีทั้งหมดนี้แล้ว ไปต่อกันเลย

## ขั้นตอนที่ 1: ติดตั้งไลบรารีที่จำเป็น

โค้ดสแนปที่คุณเห็นก่อนหน้านี้ใช้แพคเกจ `ocr` ที่เป็นตัวอย่างเท่านั้น แต่แนวคิดเดียวกันสามารถใช้กับไลบรารีจริงเช่น **EasyOCR**, **pytesseract**, หรือ **pdfminer.six** สำหรับคู่มือนี้เราจะใช้ **EasyOCR** เพราะเป็นไลบรารี pure Python รองรับหลายภาษา และมีเมธอดแปลงเป็น PDF ผ่านตัวช่วยเสริม

```bash
pip install easyocr pillow
```

> **เคล็ดลับ:** ติดตั้งภายใน virtual environment (`python -m venv venv && source venv/bin/activate`) เพื่อให้การจัดการ dependencies เป็นระเบียบ

## ขั้นตอนที่ 2: เริ่มต้นเครื่อง OCR – ทำ OCR บนภาพ

เมื่อไลบรารีพร้อมแล้ว เราจะสร้าง engine OCR และบอกให้ทำงานกับข้อความภาษาอังกฤษ นี่คือจุดแรกที่เราจะ **ทำ OCR บนภาพ**

```python
import easyocr
from PIL import Image
import io

# Create an EasyOCR reader for English
reader = easyocr.Reader(['en'])  # ← performs OCR on image
```

ทำไมต้องใช้วัตถุ reader แยก? EasyOCR โหลดโมเดลภาษาไว้ล่วงหน้า การใช้ `reader` เดียวกันสำหรับหลายภาพจึงมีประสิทธิภาพมากกว่าการสร้างใหม่ทุกครั้ง

## ขั้นตอนที่ 3: โหลดภาพ – ดึงข้อความจากภาพ

เราจะนำรูปภาพเข้ามาในหน่วยความจำ ขั้นตอนนี้คือจุดที่เราจะ **ดึงข้อความจากภาพ** ในภายหลัง แต่ตอนนี้เราจะเพียงแค่โหลดภาพเท่านั้น

```python
# Replace with the path to your receipt or scanned document
image_path = "YOUR_DIRECTORY/receipt.png"

# Open the image with Pillow (helps with format handling)
pil_image = Image.open(image_path).convert("RGB")
```

หากภาพของคุณกลับหัวหรือเอียง ให้พิจารณาใช้เมธอด `rotate` หรือ `transpose` ของ Pillow ก่อนส่งให้ engine OCR การตรวจสอบภาพอย่างรวดเร็วจะช่วยประหยัดเวลาการดีบักหลายชั่วโมง

## ขั้นตอนที่ 4: รันเครื่อง OCR และบันทึกผลลัพธ์

นี่คือหัวใจของกระบวนการ—ส่งภาพให้ engine OCR แล้วรับข้อมูลที่จัดโครงสร้างกลับมา

```python
# EasyOCR returns a list of (bbox, text, confidence) tuples
ocr_result = reader.readtext(image_path, detail=1, paragraph=True)
```

แฟล็ก `detail=1` จะให้ข้อมูล bounding box ซึ่งจำเป็นเมื่อเราต้อง **แปลง OCR เป็น PDF** หากคุณต้องการแค่สตริงดิบเท่านั้น ให้ตั้งค่า `detail=0`

## ขั้นตอนที่ 5: แปลงผล OCR เป็น PDF ที่ค้นหาได้ – แปลง OCR เป็น PDF

EasyOCR ไม่ได้มีเมธอดเขียน PDF โดยตรง แต่เราสามารถต่อ PDF เองโดยใช้ Pillow และไลบรารี `reportlab` เพื่อให้บทแนะนำนี้เบา เราจะใช้ `fpdf2` ซึ่งช่วยให้เราฝังภาพต้นฉบับและวางข้อความที่มองไม่เห็นลงบนภาพได้

```bash
pip install fpdf2
```

```python
from fpdf import FPDF

class SearchablePDF(FPDF):
    def __init__(self, image_path):
        super().__init__()
        self.add_page()
        self.image(image_path, x=0, y=0, w=self.w, h=self.h)

    def add_ocr_text(self, ocr_data):
        # Set invisible text style
        self.set_text_color(255, 255, 255)   # white on white background
        self.set_font("Helvetica", size=12)

        for bbox, text, conf in ocr_data:
            # bbox = [(x1,y1), (x2,y2), (x3,y3), (x4,y4)]
            x_min = min(point[0] for point in bbox)
            y_min = min(point[1] for point in bbox)
            self.set_xy(x_min, y_min)
            self.cell(0, 0, txt=text, border=0)

# Create PDF instance with the original image as background
pdf = SearchablePDF(image_path)

# Add invisible OCR text on top of the image
pdf.add_ocr_text(ocr_result)

# Save the searchable PDF
output_path = "YOUR_DIRECTORY/receipt_searchable.pdf"
pdf.output(output_path)
```

เกิดอะไรขึ้น? เราใส่ภาพสแกนเป็นเลเยอร์ที่มองเห็นได้ แล้วเขียนคำที่ OCR ตรวจจับได้บนด้านบนด้วยข้อความสีขาวที่ซ่อนอยู่ในพื้นหลังสีขาว เครื่องมือค้นหายังคงอ่านเลเยอร์ที่ซ่อนอยู่ ทำให้ PDF กลายเป็น **searchable** โดยไม่เปลี่ยนรูปลักษณ์ของภาพ

## ขั้นตอนที่ 6: บันทึกไบต์ของ PDF – แปลงภาพเป็น PDF

หากคุณต้องการจัดการ PDF ในหน่วยความจำ (เช่น ส่งผ่าน API) คุณสามารถดึงไบต์แทนการเขียนลงดิสก์ได้

```python
pdf_bytes = pdf.output(dest='S').encode('latin1')  # returns a byte string

# Example: write bytes to a file (same as Step 5 but shows the conversion)
with open(output_path, "wb") as f:
    f.write(pdf_bytes)
```

บรรทัดนี้แสดงการทำงานแบบคลาสสิกของ **convert image to PDF**: เริ่มจากภาพ, รัน OCR, วางข้อความ, แล้วส่งออกสตรีม PDF

## ขั้นตอนที่ 7: ตรวจสอบผลลัพธ์ – ตรวจสอบอย่างรวดเร็ว

หลังจากรันสคริปต์แล้ว เปิด `receipt_searchable.pdf` ด้วยโปรแกรมดู PDF ใดก็ได้และลองใช้ช่องค้นหา (Ctrl + F) พิมพ์คำที่คุณรู้ว่ามีในใบเสร็จ—ถ้าตำแหน่งกระโดดไปที่ตรงนั้น คุณได้ **สร้าง PDF ที่ค้นหาได้** สำเร็จ!  

หากการค้นหาไม่ทำงาน ให้ตรวจสอบสองอย่างต่อไปนี้:

1. คะแนนความเชื่อมั่นของ OCR (`conf` values) คะแนนต่ำอาจหมายถึงภาพเบลอ  
2. พิกัด bounding box—บางครั้ง EasyOCR รายงานในแนวทิศทางที่ต่างกัน  
3. ตรวจสอบว่าโปรแกรมดู PDF ไม่ได้ตั้งเป็นโหมด “image‑only” (หายาก แต่บางโปรแกรมมีตัวเลือกนี้)

## สคริปต์ทำงานเต็มรูปแบบ

รวมทุกอย่างเข้าด้วยกัน นี่คือไฟล์ Python ที่พร้อมรันเต็มรูปแบบ:

```python
# searchable_pdf.py
import easyocr
from PIL import Image
from fpdf import FPDF

# ---------- Configuration ----------
IMAGE_PATH = "YOUR_DIRECTORY/receipt.png"
OUTPUT_PDF = "YOUR_DIRECTORY/receipt_searchable.pdf"
# ----------------------------------

class SearchablePDF(FPDF):
    def __init__(self, image_path):
        super().__init__()
        self.add_page()
        # Fit the image to the page size
        self.image(image_path, x=0, y=0, w=self.w, h=self.h)

    def add_ocr_text(self, ocr_data):
        self.set_text_color(255, 255, 255)   # invisible white text
        self.set_font("Helvetica", size=12)
        for bbox, text, conf in ocr_data:
            x_min = min(p[0] for p in bbox)
            y_min = min(p[1] for p in bbox)
            self.set_xy(x_min, y_min)
            self.cell(0, 0, txt=text, border=0)

def main():
    # 1️⃣ Initialize OCR engine – perform OCR on image
    reader = easyocr.Reader(['en'])

    # 2️⃣ Load the image – extract text from image later
    pil_image = Image.open(IMAGE_PATH).convert("RGB")

    # 3️⃣ Run OCR and capture results
    ocr_result = reader.readtext(IMAGE_PATH, detail=1, paragraph=True)

    # 4️⃣ Convert OCR result to searchable PDF – convert OCR to PDF
    pdf = SearchablePDF(IMAGE_PATH)
    pdf.add_ocr_text(ocr_result)

    # 5️⃣ Save the PDF – convert image to PDF (or keep bytes in memory)
    pdf.output(OUTPUT_PDF)
    print(f"✅ Searchable PDF saved to {OUTPUT_PDF}")

if __name__ == "__main__":
    main()
```

บันทึกไฟล์นี้เป็น `searchable_pdf.py` แทนที่ค่า `YOUR_DIRECTORY` ด้วยพาธจริงของคุณ แล้วรัน:

```bash
python searchable_pdf.py
```

คุณจะเห็นข้อความยืนยันและ PDF ที่ค้นหาได้ใหม่ปรากฏในโฟลเดอร์ของคุณ

## คำถามทั่วไปและกรณีขอบ

**ถ้าภาพเป็นสีจะทำอย่างไร?**  
EasyOCR รองรับทั้งภาพระดับสีเทาและสีเต็ม แต่การแปลงเป็นระดับสีเทา (`pil_image.convert("L")`) บางครั้งช่วยเพิ่มความแม่นยำบนสแกนที่มีเสียงรบกวน

**ฉันสามารถจัดการกับ PDF หลายหน้าได้หรือไม่?**  
ได้—วนลูปแต่ละหน้าภาพ, รันขั้นตอน OCR, แล้วเพิ่มแต่ละหน้าเข้าไปในอ็อบเจ็กต์ `FPDF` เดียวกัน เพียงจำไว้ว่าให้รีเซ็ตเคอร์เซอร์ (`self.add_page()`) สำหรับแต่ละภาพใหม่

**มีวิธีใส่เลเยอร์ข้อความต้นฉบับแทนการใช้ข้อความสีขาวที่มองไม่เห็นหรือไม่?**  
หากต้องการ PDF “text‑under‑image” ที่แท้จริง (เช่น เพื่อการเข้าถึง) ให้พิจารณาใช้ `pdfminer` หรือ `pikepdf` เพื่อฝังเลเยอร์ข้อความที่ซ่อนอยู่พร้อมแท็ก PDF ที่เหมาะสม นี่เป็นขั้นตอนที่ซับซ้อนกว่า แต่หลักการยังคงเหมือนเดิม: ภาพพื้นหลัง + วางข้อความทับ

**ถ้าความเชื่อมั่นของ OCR ต่ำควรทำอย่างไร?**  
คุณสามารถกรองคำที่ความเชื่อมั่นต่ำออกได้:

```python
filtered = [item for item in ocr_result if item[2] > 0.8]  # keep >80% confidence
pdf.add_ocr_text(filtered)
```

## สรุป – สิ่งที่เราบรรลุ

เราเริ่มจากภาพใบเสร็จง่าย ๆ, **ทำ OCR บนภาพ**, ดึงสตริงที่ตรวจจับได้, และสุดท้าย **สร้าง PDF ที่ค้นหาได้** ที่ทำงานเหมือนเอกสารสแกนระดับมืออาชีพ กระบวนการนี้ครอบคลุมคีย์เวิร์ดรองทุกคำ—**แปลง OCR เป็น PDF**, **ดึงข้อความจากภาพ**, **แปลงภาพเป็น PDF**, และ **ทำ OCR บนภาพ**—ดังนั้นคุณจึงมีเครื่องมือที่ใช้ซ้ำได้สำหรับโปรเจกต์ใด ๆ ที่คล้ายกัน

### ขั้นตอนต่อไป

- ทดลองใช้ภาษาอื่นโดยส่งรหัส ISO ไปยัง `easyocr.Reader(['en', 'es'])`  
- เปลี่ยน EasyOCR เป็น Tesseract หากต้องการโซลูชันที่ทำงานแบบออฟไลน์ทั้งหมด; ส่วนของ pipeline จะยังคงเหมือนเดิม  
- เพิ่มการแสดงผลความเชื่อมั่นของ OCR (วาด bounding box บนภาพ) เพื่อดีบักสแกนที่มีปัญหา  

มีไอเดียหรือวิธีที่คุณอยากแชร์ไหม? แสดงความคิดเห็นหรือ fork โปรเจกต์

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอน‑ขั้นตอน เพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโปรเจกต์ของคุณ

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [How to OCR Image – Perform OCR on Image in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}