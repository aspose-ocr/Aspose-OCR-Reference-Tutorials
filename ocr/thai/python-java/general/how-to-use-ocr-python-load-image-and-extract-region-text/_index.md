---
category: general
date: 2026-06-25
description: วิธีใช้ OCR ใน Python – เรียนรู้วิธีโหลดภาพสำหรับ OCR, จดจำข้อความในพื้นที่,
  และดึงข้อความจากพื้นที่อย่างรวดเร็ว.
draft: false
keywords:
- how to use ocr
- load image for ocr
- recognize text in region
- how to extract region text
language: th
og_description: วิธีใช้ OCR ใน Python – คู่มือขั้นตอนการโหลดภาพ, จดจำข้อความในพื้นที่เฉพาะ,
  และดึงหมายเลขใบแจ้งหนี้.
og_title: 'วิธีใช้ OCR ด้วย Python: โหลดภาพและดึงข้อความจากพื้นที่'
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: How to use OCR in Python – learn how to load image for OCR, recognize
    text in region, and extract region text quickly.
  headline: 'How to Use OCR Python: Load Image and Extract Region Text'
  type: TechArticle
- questions:
  - answer: Most modern OCR engines handle a wide range of fonts, but you can boost
      accuracy by training a custom language model or pre‑processing the image (e.g.,
      applying a threshold filter).
    question: What if the invoice number is printed in a fancy font?
  - answer: Absolutely. Define a list of `Rectangle` objects—one per field—and loop
      over them, storing each result in a dictionary.
    question: Can I extract multiple fields at once?
  - answer: 'Convert each page to an image first (using `pdf2image` or similar), then
      apply the same region‑based extraction per page. --- ## Wrapping Up In this
      tutorial we covered **how to use OCR** in Python to load an image, recognize
      text in a specific region, and extract that region’s text—perfect for pull'
    question: Does this work on multi‑page PDFs?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
title: 'วิธีใช้ OCR Python: โหลดภาพและดึงข้อความจากพื้นที่'
url: /th/python-java/general/how-to-use-ocr-python-load-image-and-extract-region-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีใช้ OCR ใน Python: โหลดรูปภาพและดึงข้อความจากพื้นที่

**วิธีใช้ OCR ใน Python** นั้นง่ายกว่าที่คุณคิด เคยมองใบแจ้งหนี้ที่สแกนแล้วสงสัยว่าจะดึงเลขที่ใบแจ้งหนี้ออกมาโดยไม่ต้องอ่านทั้งหน้าไหม? คุณไม่ได้เป็นคนเดียว—นักพัฒนาหลายคนเจอปัญหานี้เมื่อลองใช้การจดจำอักขระด้วยแสง (OCR) ครั้งแรก ในคู่มือนี้เราจะพาคุณผ่านขั้นตอนการโหลดรูปภาพสำหรับ OCR, กำหนดสี่เหลี่ยม, จดจำข้อความในพื้นที่นั้น, และสุดท้ายดึงข้อความจากพื้นที่ออกมา เมื่อเสร็จคุณจะมีสคริปต์พร้อมรันที่สามารถแยกข้อความใด ๆ ที่คุณต้องการได้

> *เคล็ดลับ:* หากคุณทำงานกับ PDF ให้แปลงแต่ละหน้าเป็นรูปภาพก่อน—ส่วนใหญ่ไลบรารี OCR จะทำงานกับ PNG/JPEG ได้ดีที่สุด

## สิ่งที่คุณต้องเตรียม

- Python 3.8+ (แนะนำให้ใช้เวอร์ชันล่าสุดที่เสถียร)  
- ไลบรารี OCR ที่ให้คลาส `OcrEngine` (เช่น **ocr** จาก `pip install ocr-lib`)  
- รูปตัวอย่าง—ในที่นี้เราจะใช้ `invoice.png` ที่วางไว้ในโฟลเดอร์ที่คุณควบคุม  
- ความคุ้นเคยพื้นฐานกับสี่เหลี่ยม (x, y, width, height)  

ไม่มีการพึ่งพาไลบรารีหนัก ๆ ไม่ต้องใช้ GPU—ทำงานบน CPU ธรรมดา ทำให้พกพาง่าย

---

## วิธีใช้ OCR: เริ่มต้น Engine (ขั้นตอน 1)

ก่อนที่ข้อความจะถูกอ่านได้ คุณต้องสร้างอินสแตนซ์ของ OCR engine คิดว่าเป็นสมองที่จะวิเคราะห์รูปแบบพิกเซล

```python
import ocr               # The OCR library
from ocr import Rectangle  # Helper for defining regions

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*ทำไมจึงสำคัญ:* การเริ่มต้น engine จะโหลดโมเดลภาษาและตั้งค่าคอนฟิกเริ่มต้น หากข้ามขั้นตอนนี้จะทำให้เกิดข้อยกเว้นทันทีเมื่อคุณเรียก `recognize_region`

---

## โหลดรูปภาพสำหรับ OCR (ขั้นตอน 2)

เมื่อ engine พร้อมแล้ว เราจะส่งรูปภาพให้มัน ไลบรารีเมธอด `Image.load` จะจัดการรูปแบบทั่วไปและทำให้บิตแมพเป็นมาตรฐาน

```python
# Step 2: Load the image containing the invoice
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)
```

หากไฟล์ไม่พบ Python จะโยน `FileNotFoundError` ตรวจสอบให้แน่ใจว่าเส้นทางเป็นแบบ absolute หรือ relative กับไดเรกทอรีทำงานของสคริปต์  

*กรณีพิเศษ:* บาง OCR engine ต้องการรูปภาพแบบ grayscale หากคุณพบความแม่นยำต่ำ ให้แปลงรูปภาพก่อน:

```python
image = image.convert("L")  # L = 8‑bit pixels, black and white
```

---

## จดจำข้อความในพื้นที่ (ขั้นตอน 3)

การกำหนดพื้นที่คือการบอก engine ว่า *จะมอง* ที่ไหน `Rectangle` รับค่าทศนิยมเพื่อความแม่นยำระดับ sub‑pixel ซึ่งมีประโยชน์เมื่อทำงานกับสแกนความละเอียดสูง

```python
# Step 3: Define the rectangle that encloses the invoice number
invoice_rect = Rectangle(120.5, 45.2, 300.0, 60.0)
```

- **x, y** – พิกัดมุมซ้ายบนของสี่เหลี่ยม (หน่วยพิกเซล)  
- **width, height** – ขนาดของกล่อง  

คุณอาจสงสัยว่าจะหาเลขเหล่านี้ได้อย่างไร วิธีง่าย ๆ คือเปิดรูปในโปรแกรมแก้ไขใดก็ได้ (เช่น GIMP หรือ Paint.NET) แล้วใช้เครื่องมือเลือกเพื่ออ่านพิกัด  

*ทำไมไม่ OCR ทั้งหน้า?* การจำกัดพื้นที่ช่วยลดสัญญาณรบกวน เร็วขึ้น และเพิ่มความแม่นยำอย่างมากสำหรับฟิลด์เล็ก ๆ เช่นเลขที่ใบแจ้งหนี้

---

## วิธีดึงข้อความจากพื้นที่ (ขั้นตอน 4)

เมื่อกำหนดพื้นที่แล้ว ให้ engine จดจำเฉพาะส่วนนั้น ผลลัพธ์จะมีข้อความดิบและคะแนนความเชื่อมั่น

```python
# Step 4: Recognize text only within the specified region
region_result = engine.recognize_region(image, invoice_rect)
```

หาก OCR engine รองรับหลายภาษา คุณสามารถส่งรหัสภาษาเพิ่มเติมได้:

```python
region_result = engine.recognize_region(image, invoice_rect, lang="eng")
```

*ข้อผิดพลาดทั่วไป:* บาง engine คืนค่ารายการคำแทนที่จะเป็นสตริงเดียว ในกรณีนั้นให้ต่อคำเข้าด้วยกัน:

```python
text = " ".join(region_result.words)
```

---

## แสดงผลเลขที่ใบแจ้งหนี้ที่ดึงมา (ขั้นตอน 5)

สุดท้าย พิมพ์หรือบันทึกข้อความที่ดึงมา คุณยังสามารถทำ post‑process เพื่อลบช่องว่างหรืออักขระที่ไม่ใช่ตัวเลขได้

```python
# Step 5: Output the extracted invoice number
raw_text = region_result.text.strip()
# Optional: keep only digits (most invoice numbers are numeric)
invoice_number = "".join(filter(str.isdigit, raw_text))

print("Invoice number:", invoice_number)
```

รันสคริปต์พร้อมสี่เหลี่ยมที่จัดตำแหน่งถูกต้องจะได้ผลลัพธ์ประมาณนี้:

```
Invoice number: 20231578
```

หากได้อักขระแปลก ๆ ให้ตรวจสอบพิกัดสี่เหลี่ยมอีกครั้งหรือพิจารณาเพิ่มความละเอียดของรูปภาพ

---

## ตัวอย่างทำงานเต็มรูปแบบ

รวมทุกขั้นตอนเข้าด้วยกัน นี่คือสคริปต์อิสระที่คุณสามารถคัดลอก‑วางและรันได้:

```python
import ocr
from ocr import Rectangle

def extract_invoice_number(image_path: str,
                          rect: Rectangle,
                          lang: str = "eng") -> str:
    """
    Loads an image, runs OCR on the specified rectangle, and returns
    a cleaned invoice number string.
    """
    engine = ocr.OcrEngine()
    image = ocr.Image.load(image_path)

    # Optional: force grayscale for better accuracy
    image = image.convert("L")

    result = engine.recognize_region(image, rect, lang=lang)
    raw = result.text.strip()
    cleaned = "".join(filter(str.isdigit, raw))
    return cleaned

if __name__ == "__main__":
    # Adjust these values to match your invoice layout
    invoice_rect = Rectangle(120.5, 45.2, 300.0, 60.0)
    invoice_path = "YOUR_DIRECTORY/invoice.png"

    number = extract_invoice_number(invoice_path, invoice_rect)
    print("Invoice number:", number)
```

บันทึกไฟล์เป็น `extract_invoice.py` แทนที่ `YOUR_DIRECTORY` ด้วยโฟลเดอร์จริงของคุณ แล้วรัน:

```bash
python extract_invoice.py
```

คุณควรเห็นเลขที่ใบแจ้งหนี้แสดงบนคอนโซล

---

## คำถามที่พบบ่อย

**ถาม: ถ้าเลขที่ใบแจ้งหนี้พิมพ์ด้วยฟอนต์หรูหรา จะทำอย่างไร?**  
ตอบ: OCR engine สมัยใหม่ส่วนใหญ่รองรับฟอนต์หลากหลาย แต่คุณสามารถเพิ่มความแม่นยำได้โดยฝึกโมเดลภาษาแบบกำหนดเองหรือทำการ pre‑process รูปภาพ (เช่น ใช้ฟิลเตอร์ threshold)

**ถาม: ฉันสามารถดึงหลายฟิลด์พร้อมกันได้หรือไม่?**  
ตอบ: ทำได้แน่นอน กำหนดรายการของอ็อบเจกต์ `Rectangle`—หนึ่งอ็อบเจกต์ต่อฟิลด์—แล้ววนลูปผ่านแต่ละรายการ เก็บผลลัพธ์ไว้ใน dictionary

**ถาม: วิธีนี้ใช้กับ PDF หลายหน้าได้หรือไม่?**  
ตอบ: ให้แปลงแต่ละหน้าเป็นรูปภาพก่อน (ใช้ `pdf2image` หรือเครื่องมือคล้ายกัน) แล้วใช้การดึงข้อความตามพื้นที่เดียวกันสำหรับแต่ละหน้า

---

## สรุป

ในบทเรียนนี้เราได้อธิบาย **วิธีใช้ OCR** ใน Python เพื่อโหลดรูปภาพ, จดจำข้อความในพื้นที่เฉพาะ, และดึงข้อความจากพื้นที่นั้น—เหมาะสำหรับการดึงเลขที่ใบแจ้งหนี้, ID คำสั่งซื้อ, หรือข้อมูลเล็ก ๆ จากเอกสารสแกน การแยกพื้นที่ที่ต้องการช่วยให้เร็วขึ้น แม่นยำขึ้น และลดความยุ่งยากในการประมวลผลต่อมา

พร้อมก้าวต่อไปหรือยัง? ลองขยายสคริปต์เพื่อ **โหลดรูปภาพสำหรับ OCR** จากโฟลเดอร์ใบแจ้งหนี้หลายใบ, หรือทดลอง **จดจำข้อความในพื้นที่** สำหรับฟิลด์อื่น ๆ เช่น วันที่และยอดรวม รูปแบบเดียวกัน—เปลี่ยนแค่พิกัดสี่เหลี่ยม

หากคุณเจออุปสรรคหรือมีไอเดียปรับปรุง แสดงความคิดเห็นด้านล่างได้เลย ขอให้เขียนโค้ดสนุกและ OCR ของคุณแม่นยำเสมอ!

## สิ่งที่คุณควรเรียนต่อไป

บทแนะนำต่อไปนี้เกี่ยวกับหัวข้อที่ใกล้เคียงและต่อยอดเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอน‑ขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโปรเจกต์ของคุณ

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}