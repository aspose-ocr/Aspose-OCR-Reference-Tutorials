---
category: general
date: 2026-05-31
description: สร้าง PDF ที่สามารถค้นหาได้จากภาพสแกนโดยใช้ Python OCR. เรียนรู้วิธีแปลง
  PDF จากภาพสแกน, แปลง TIFF เป็น PDF, และเพิ่มชั้นข้อความ OCR ในไม่กี่นาที.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- convert tiff to pdf
- how to run OCR
- add OCR text layer
language: th
og_description: สร้าง PDF ที่ค้นหาได้ทันที คู่มือนี้แสดงวิธีการทำ OCR, แปลง PDF ที่เป็นภาพสแกน,
  และเพิ่มชั้นข้อความ OCR ด้วยสคริปต์ Python เพียงไฟล์เดียว.
og_title: สร้าง PDF ที่ค้นหาได้ด้วย Python – บทเรียนเต็มรูปแบบ
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Create searchable PDF from scanned images using Python OCR. Learn how
    to convert scanned image PDF, convert TIFF to PDF, and add OCR text layer in minutes.
  headline: Create Searchable PDF with Python – Step‑by‑Step Guide
  type: TechArticle
- description: Create searchable PDF from scanned images using Python OCR. Learn how
    to convert scanned image PDF, convert TIFF to PDF, and add OCR text layer in minutes.
  name: Create Searchable PDF with Python – Step‑by‑Step Guide
  steps:
  - name: Expected Output
    text: 'Running the script prints:'
  - name: 1️⃣ Can I process multi‑page PDFs?
    text: Yes. Use `ocr_engine.load_image("file.pdf")` and then loop over each page
      with `ocr_engine.recognize(pdf_save_options, page_number)`. The library will
      automatically generate a multi‑page searchable PDF.
  - name: 2️⃣ What if my source file is a high‑resolution TIFF (300 dpi+)?
    text: 'Higher DPI yields better OCR accuracy but also larger memory usage. If
      you hit a `MemoryError`, downscale the image first:'
  - name: 3️⃣ How do I change the language of the OCR?
    text: 'Set the `language` property on the engine before loading the image:'
  - name: 4️⃣ What if I need to keep the original image quality?
    text: The `PdfSaveOptions` class has a `compression` property. Set it to `PdfCompression.None`
      to preserve the raster data exactly as it was.
  type: HowTo
tags:
- OCR
- Python
- PDF
- Document Automation
title: สร้าง PDF ที่ค้นหาได้ด้วย Python – คู่มือขั้นตอนโดยละเอียด
url: /th/python-java/general/create-searchable-pdf-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง PDF ที่สามารถค้นหาได้ด้วย Python – คู่มือขั้นตอนโดยละเอียด

เคยสงสัยไหมว่าจะ **สร้าง PDF ที่สามารถค้นหาได้** จากหน้าที่สแกนโดยไม่ต้องใช้เครื่องมือหลายสิบอย่าง? คุณไม่ได้เป็นคนเดียว ในหลายกระบวนการทำงานของสำนักงาน ไฟล์ TIFF หรือ JPEG ที่สแกนแล้วจะถูกวางไว้บนไดรฟ์ร่วมกัน และคนถัดไปต้องคัดลอก‑วางข้อความด้วยตนเอง – ทำให้เจ็บปวด มีโอกาสผิดพลาด และเสียเวลา  

ในบทเรียนนี้เราจะพาไปผ่านวิธีแก้ปัญหาแบบโปรแกรมที่สะอาดตา ซึ่งทำให้คุณ **แปลง PDF ที่เป็นภาพสแกน**, **แปลง TIFF เป็น PDF**, และ **เพิ่มชั้นข้อความ OCR** ได้ในขั้นตอนเดียว เมื่อเสร็จแล้วคุณจะได้สคริปต์พร้อมใช้ที่ทำ OCR ฝังข้อความที่ซ่อนอยู่ และสร้าง PDF ที่สามารถค้นหาได้ซึ่งคุณสามารถทำดัชนี ค้นหา หรือแชร์ได้อย่างมั่นใจ

## สิ่งที่คุณต้องมี

- Python 3.9+ (เวอร์ชันล่าสุดใดก็ได้)
- แพคเกจ `aspose-ocr` และ `aspose-pdf` (ติดตั้งด้วย `pip install aspose-ocr aspose-pdf`)
- ไฟล์ภาพสแกน (`.tif`, `.png`, `.jpg` หรือแม้แต่ PDF หน้าเดียวที่เป็นภาพ)
- RAM ปริมาณปานกลาง (เอนจิน OCR มีน้ำหนักเบา; แม้แล็ปท็อปก็จัดการได้)

> **เคล็ดลับมืออาชีพ:** หากคุณใช้ Windows วิธีที่ง่ายที่สุดในการรับแพคเกจคือรันคำสั่งใน PowerShell ที่เปิดด้วยสิทธิ์ผู้ดูแลระบบ

```bash
pip install aspose-ocr aspose-pdf
```

เมื่อเงื่อนไขเบื้องต้นเรียบร้อยแล้ว ไปดูกันที่โค้ดกันเลย

## ขั้นตอนที่ 1: สร้างอินสแตนซ์ของ OCR Engine – *create searchable pdf*

สิ่งแรกที่เราทำคือเปิดใช้งาน OCR engine คิดว่าเป็นสมองที่อ่านพิกเซลทุกจุดและแปลงเป็นอักขระ

```python
from aspose.ocr import OcrEngine

# Initialize the OCR engine – this is the core of the create searchable pdf process
ocr_engine = OcrEngine()
```

> **ทำไมจึงสำคัญ:** การเริ่มต้นเอนจินเพียงครั้งเดียวช่วยลดการใช้หน่วยความจำ หากคุณเรียก `OcrEngine()` ภายในลูปสำหรับแต่ละหน้า คุณจะใช้ทรัพยากรหมดเร็วเกินไป

## ขั้นตอนที่ 2: โหลดภาพสแกน – *convert tiff to pdf* & *convert scanned image pdf*

ต่อไปให้ชี้เอนจินไปที่ไฟล์ที่ต้องการประมวลผล API รองรับภาพแรสเตอร์ใดก็ได้ ดังนั้น TIFF จึงทำงานได้เท่า JPEG

```python
# Load the image you want to OCR. Replace the path with your own file location.
ocr_engine.load_image("YOUR_DIRECTORY/scanned_page.tif")
```

หากคุณมี PDF ที่มีเพียงภาพสแกนอยู่ คุณยังสามารถใช้ `load_image` ได้ เพราะ Aspose จะดึงหน้าที่แรกออกมาโดยอัตโนมัติ

## ขั้นตอนที่ 3: เตรียมตัวเลือกการบันทึก PDF – *add OCR text layer*

ที่นี่เราตั้งค่าการแสดงผลของ PDF ขั้นสุดท้าย ธงสำคัญคือ `create_searchable_pdf`; ตั้งค่าเป็น `True` จะบอกไลบรารีให้ฝังชั้นข้อความที่มองไม่เห็นซึ่งสอดคล้องกับเนื้อหาภาพ

```python
from aspose.pdf import PdfSaveOptions

pdf_save_options = PdfSaveOptions()
pdf_save_options.create_searchable_pdf = True   # embed OCR text layer
pdf_save_options.output_path = "YOUR_DIRECTORY/scanned_page_searchable.pdf"
```

> **ชั้นข้อความทำอะไร:** เมื่อคุณเปิดไฟล์ที่ได้ใน Adobe Reader แล้วพยายามเลือกข้อความ คุณจะเห็นอักขระที่ซ่อนอยู่ เครื่องมือค้นหาก็สามารถทำดัชนีได้เช่นกัน – เหมาะสำหรับการปฏิบัติตามกฎระเบียบหรือการเก็บถาวร

## ขั้นตอนที่ 4: รัน OCR และบันทึก – *how to run OCR* ในคำสั่งเดียว

ตอนนี้จุดมหัศจรรย์เกิดขึ้น การเรียกเมธอดเดียวจะรันเอนจินการจดจำและเขียน PDF ที่สามารถค้นหาได้ลงดิสก์

```python
# Run OCR and generate the searchable PDF in one go
ocr_engine.recognize(pdf_save_options)

print("PDF saved as searchable PDF.")
```

เมธอด `recognize` จะคืนค่าออบเจ็กต์สถานะที่คุณสามารถตรวจสอบข้อผิดพลาดได้ แต่สำหรับสถานการณ์ที่ตรงไปตรงมาส่วนใหญ่ การเรียกแบบง่ายข้างต้นก็เพียงพอ

### ผลลัพธ์ที่คาดหวัง

การรันสคริปต์จะแสดงผล:

```
PDF saved as searchable PDF.
```

หากคุณเปิด `scanned_page_searchable.pdf` คุณจะสังเกตว่าเลือกข้อความได้ คัดลอก‑วางได้ และแม้กระทั่งใช้ `Ctrl+F` ค้นหาได้ นี่คือสัญลักษณ์ของกระบวนการ **create searchable pdf**

## สคริปต์ทำงานเต็มรูปแบบ

ด้านล่างเป็นสคริปต์ที่พร้อมรัน เพียงแทนที่พาธตัวอย่างด้วยตำแหน่งไฟล์ของคุณเอง

```python
# ------------------------------------------------------------
# create_searchable_pdf.py – Convert scanned image to searchable PDF
# ------------------------------------------------------------

from aspose.ocr import OcrEngine
from aspose.pdf import PdfSaveOptions

def main():
    # 1️⃣ Initialize OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load image (TIFF, JPEG, PNG, or scanned PDF page)
    image_path = "YOUR_DIRECTORY/scanned_page.tif"
    ocr_engine.load_image(image_path)

    # 3️⃣ Configure PDF output – embed OCR text layer
    pdf_save_options = PdfSaveOptions()
    pdf_save_options.create_searchable_pdf = True
    pdf_save_options.output_path = "YOUR_DIRECTORY/scanned_page_searchable.pdf"

    # 4️⃣ Run OCR and write searchable PDF
    ocr_engine.recognize(pdf_save_options)

    print("PDF saved as searchable PDF.")

if __name__ == "__main__":
    main()
```

บันทึกไฟล์นี้เป็น `create_searchable_pdf.py` แล้วรัน:

```bash
python create_searchable_pdf.py
```

## คำถามที่พบบ่อย & กรณีขอบ

### 1️⃣ ฉันสามารถประมวลผล PDF หลายหน้าได้หรือไม่?

ได้ ใช้ `ocr_engine.load_image("file.pdf")` แล้ววนลูปแต่ละหน้าโดยใช้ `ocr_engine.recognize(pdf_save_options, page_number)` ไลบรารีจะสร้าง PDF ที่สามารถค้นหาได้หลายหน้าโดยอัตโนมัติ

### 2️⃣ ถ้าไฟล์ต้นฉบับของฉันเป็น TIFF ความละเอียดสูง (300 dpi+) จะทำอย่างไร?

DPI ที่สูงขึ้นให้ความแม่นยำ OCR ดียิ่งขึ้นแต่ใช้หน่วยความจำมากขึ้น หากเจอ `MemoryError` ให้ลดขนาดภาพก่อน:

```python
from PIL import Image
img = Image.open(image_path)
img = img.resize((int(img.width * 0.5), int(img.height * 0.5)), Image.ANTIALIAS)
img.save("temp.tif")
ocr_engine.load_image("temp.tif")
```

### 3️⃣ ฉันจะเปลี่ยนภาษาของ OCR ได้อย่างไร?

ตั้งค่าคุณสมบัติ `language` ของเอนจินก่อนโหลดภาพ:

```python
ocr_engine.language = "fra"   # French
```

รายการรหัสภาษาที่รองรับทั้งหมดอยู่ในเอกสารของ Aspose

### 4️⃣ ถ้าฉันต้องการรักษาคุณภาพภาพต้นฉบับไว้?

คลาส `PdfSaveOptions` มีคุณสมบัติ `compression` ตั้งค่าเป็น `PdfCompression.None` เพื่อเก็บข้อมูลแรสเตอร์ไว้ตามเดิม

```python
pdf_save_options.compression = "None"
```

## เคล็ดลับสำหรับการปรับใช้ในระดับ Production

- **การประมวลผลเป็นชุด:** ห่อโลจิกหลักในฟังก์ชันที่รับรายการพาธไฟล์ บันทึกผลสำเร็จ/ความล้มเหลวแต่ละรายการลง CSV เพื่อใช้เป็นบันทึกตรวจสอบ
- **การทำงานแบบขนาน:** ใช้ `concurrent.futures.ThreadPoolExecutor` เพื่อรัน OCR บนหลายคอร์ จำไว้ว่าทุกเธรดต้องมีอินสแตนซ์ `OcrEngine` ของตนเอง
- **ความปลอดภัย:** หากจัดการกับเอกสารที่เป็นความลับ ให้รันสคริปต์ในสภาพแวดล้อมแซนด์บ็อกซ์และลบไฟล์ชั่วคราวทันทีหลังการประมวลผล

## สรุป

คุณได้เรียนรู้วิธี **สร้าง PDF ที่สามารถค้นหาได้** จากภาพสแกนด้วยสคริปต์ Python สั้น ๆ ด้วยการเริ่มต้น OCR engine, โหลด TIFF (หรือแรสเตอร์ใดก็ได้), ตั้งค่า `PdfSaveOptions` เพื่อ **add OCR text layer**, แล้วเรียก `recognize` ทั้งหมดทำให้กระบวนการ **convert scanned image pdf** และ **convert TIFF to PDF** กลายเป็นคำสั่งเดียวที่ทำซ้ำได้

ขั้นตอนต่อไป? ลองเชื่อมสคริปต์นี้กับตัวตรวจจับไฟล์เพื่อให้ทุกการสแกนใหม่ที่วางลงในโฟลเดอร์กลายเป็นไฟล์ที่สามารถค้นหาได้โดยอัตโนมัติ หรือทดลองใช้ภาษาต่าง ๆ ของ OCR เพื่อรองรับคลังข้อมูลหลายภาษา ความเป็นไปได้ไม่มีที่สิ้นสุดเมื่อคุณผสาน OCR กับการสร้าง PDF

มีคำถามเพิ่มเติมเกี่ยวกับ **how to run OCR** ในภาษา หรือเฟรมเวิร์กอื่น ๆ หรือไม่? แสดงความคิดเห็นด้านล่าง แล้วขอให้เขียนโค้ดอย่างสนุกสนาน!

![Diagram showing the flow from scanned image → OCR engine → searchable PDF (create searchable pdf)](searchable-pdf-flow.png "ไดอะแกรมการไหลของการสร้าง PDF ที่สามารถค้นหาได้")

## คุณควรเรียนรู้อะไรต่อไป?

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}