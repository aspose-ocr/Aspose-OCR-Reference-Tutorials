---
category: general
date: 2026-07-05
description: สร้าง PDF ที่ค้นหาได้ด้วย Python เรียนรู้วิธีทำ OCR กับ PNG ที่สแกน แปลง
  PDF รูปภาพที่สแกน และได้ PDF ที่ค้นหาได้ในไม่กี่นาที.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- how to ocr pdf
- ocr recognition example
- convert png searchable pdf
language: th
og_description: สร้าง PDF ที่สามารถค้นหาได้อย่างรวดเร็ว คู่มือนี้แสดงวิธีทำ OCR กับ
  PNG, แปลง PDF ที่สแกนเป็นภาพ, และสร้าง PDF ที่สามารถค้นหาได้โดยใช้ Python.
og_title: สร้าง PDF ที่ค้นหาได้จากภาพสแกน – บทเรียน OCR ด้วย Python
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Create searchable PDF with Python. Learn how to OCR a scanned PNG,
    convert scanned image PDF, and get a searchable PDF in minutes.
  headline: Create Searchable PDF from Scanned Image – Full Python OCR Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF
- Automation
title: สร้าง PDF ที่ค้นหาได้จากภาพสแกน – คู่มือ OCR ด้วย Python อย่างเต็มรูปแบบ
url: /th/python-java/general/create-searchable-pdf-from-scanned-image-full-python-ocr-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง PDF ที่ค้นหาได้จากภาพสแกน – คู่มือ OCR ด้วย Python อย่างเต็มรูปแบบ

เคยสงสัยไหมว่า **สร้าง PDF ที่ค้นหาได้** จากรูปสแกนโดยไม่ต้องจ่ายซอฟต์แวร์ราคาแพง? คุณไม่ได้เป็นคนเดียว ในหลายสำนักงาน PDF มักมาถึงในรูปแบบภาพแบน—ค้นหาได้ยาก, คัดลอก‑วางไม่ได้, และเป็นปัญหาสำหรับการตรวจสอบความสอดคล้อง ข่าวดีคือ ด้วยบรรทัดโค้ด Python เพียงไม่กี่บรรทัด คุณสามารถเปลี่ยน PNG คงที่ให้เป็น PDF ที่ค้นหาได้เต็มรูปแบบ และขั้นตอนนั้นง่ายกว่าที่คิด

ในบทเรียนนี้เราจะเดินผ่าน **ตัวอย่างการรับรู้ OCR** อย่างครบถ้วน ตั้งแต่การติดตั้งไลบรารีที่ถูกต้องจนถึงการเขียนไฟล์ PDF สุดท้าย เมื่อจบคุณจะรู้วิธี **แปลงไฟล์ PDF จากภาพสแกน** อย่างแม่นยำ, วิธี **ocr pdf** อย่างโปรแกรมเมติก, และจะได้สคริปต์ที่นำกลับไปใช้ในโปรเจกต์ใดก็ได้

## สิ่งที่คุณจะได้เรียน

- ติดตั้งและกำหนดค่าไลบรารี OCR ของ Python (เราจะใช้ `pytesseract` และ `pdf2image`)
- เริ่มต้นเครื่องมือ OCR และตั้งค่าภาษา
- โหลด PNG ที่สแกน (หรือรูปใดก็ได้) แล้วรัน OCR
- แปลงผล OCR เป็น **PDF ที่ค้นหาได้** (byte array) แล้วบันทึก
- เคล็ดลับการจัดการเอกสารหลายหน้า, ภาษาต่าง ๆ, และข้อผิดพลาดทั่วไป

ไม่จำเป็นต้องมีประสบการณ์กับ OCR มาก่อน—แค่มีสภาพแวดล้อม Python 3 ที่ทำงานได้และความอยากรู้เล็กน้อย

---

## สร้าง PDF ที่ค้นหาได้ – ภาพรวม

ด้านล่างเป็นแผนผังระดับสูงของขั้นตอนที่เราจะทำ  

![Create searchable PDF workflow diagram](https://example.com/flowchart.png "Create searchable PDF workflow diagram")

*Alt text: Create searchable PDF workflow diagram showing engine init, image load, OCR recognition, PDF conversion, and file write.*

---

## ขั้นตอนที่ 1: เริ่มต้นเครื่องมือ OCR (how to ocr pdf)

ทำไมเราต้องเริ่มต้นอะไรสักอย่าง? เครื่องมือ OCR คือสมองที่แปลรูปแบบพิกเซลเป็นอักขระ โดยการสร้างอินสแตนซ์ของเครื่องมือและกำหนดภาษาชัดเจน เราบอกไลบรารีว่าคาดหวังอักษรชุดใด ซึ่งจะเพิ่มความแม่นยำอย่างมาก

```python
import pytesseract
from pdf2image import convert_from_path
from PIL import Image
import io

# Ensure Tesseract is on your PATH or provide the executable location
pytesseract.pytesseract.tesseract_cmd = r"/usr/local/bin/tesseract"  # adjust as needed

# Define the language – ENGLISH is the default, but you can add more (e.g., 'fra' for French)
ocr_language = "eng"
```

**เคล็ดลับ:** หากต้อง OCR เอกสารหลายภาษา ให้ติดตั้งแพ็คภาษาให้ตรงกับ Tesseract แล้วส่งรายการเช่น `"eng+spa"` ไปยัง `ocr_language`

---

## ขั้นตอนที่ 2: โหลดภาพสแกน (convert scanned image pdf)

ส่วนต่อไปของปริศนาคือการนำข้อมูลภาพเข้าสู่ Python ไม่ว่าจะเป็น PNG เดียวหรือ TIFF หลายหน้า, คลาส `PIL.Image` สามารถเปิดได้ หากเริ่มจาก PDF ที่มีภาพสแกนอยู่แล้ว `pdf2image` จะเปลี่ยนแต่ละหน้าเป็นภาพให้เรา

```python
# Path to the scanned image (PNG, JPG, TIFF, etc.)
image_path = "YOUR_DIRECTORY/scanned_agreement.png"

# Open the image using Pillow
image = Image.open(image_path)

# If you were starting from a scanned PDF, you could do:
# pages = convert_from_path("scanned.pdf", dpi=300)
# image = pages[0]  # just take the first page for this example
```

**ทำไมต้องทำเช่นนี้:** การโหลดภาพเป็นอ็อบเจ็กต์ Pillow ทำให้เราสามารถเข้าถึงข้อมูลพิกเซลดิบที่เครื่องมือ OCR ต้องการ การข้ามขั้นตอนนี้และส่งไบต์ดิบโดยตรงจะทำให้เกิดข้อผิดพลาด

---

## ขั้นตอนที่ 3: ทำการรับรู้ OCR บนภาพ (ocr recognition example)

ตอนนี้มาถึงส่วนสนุก—ให้เครื่องมืออ่านข้อความ `pytesseract.image_to_pdf_or_hocr` จะคืนสตรีม PDF ที่มีชั้นข้อความแบบโปร่งใสอยู่แล้ว ซึ่งเป็นสิ่งที่เราต้องการสำหรับ **PDF ที่ค้นหาได้**

```python
# Run OCR and ask for a PDF output (includes the hidden text layer)
pdf_bytes = pytesseract.image_to_pdf_or_hocr(
    image,
    lang=ocr_language,
    extension='pdf'  # returns PDF bytes
)

# pdf_bytes is a binary blob that can be saved directly to disk
```

**กรณีพิเศษ:** หากภาพของคุณคอนทราสต์ต่ำ ให้พิจารณาใช้การทำ threshold อย่างง่ายก่อน OCR:

```python
# Convert to grayscale and increase contrast
gray = image.convert('L')
threshold = gray.point(lambda x: 0 if x < 128 else 255, '1')
pdf_bytes = pytesseract.image_to_pdf_or_hocr(threshold, lang=ocr_language, extension='pdf')
```

ขั้นตอนการเตรียมภาพเล็ก ๆ นี้สามารถเพิ่มความแม่นยำได้อย่างมาก

---

## ขั้นตอนที่ 4: เขียนไบต์ PDF ลงไฟล์ (convert png searchable pdf)

ไลบรารี OCR จะให้เราเป็นอาร์เรย์ไบต์—คิดว่าเป็นเนื้อหาดิบของไฟล์ PDF เราต้องทำแค่เขียนไบต์เหล่านั้นลงดิสก์

```python
output_path = "YOUR_DIRECTORY/agreement_searchable.pdf"

with open(output_path, "wb") as f:
    f.write(pdf_bytes)

print(f"✅ Searchable PDF created at: {output_path}")
```

**สิ่งที่คุณจะเห็น:** เปิดไฟล์ที่ได้ในโปรแกรมอ่าน PDF ใดก็ได้และลองค้นหาคำที่คุณรู้ว่ามีอยู่ในภาพต้นฉบับ คำที่ไฮไลท์จะพุ่งตรงไปยังตำแหน่งนั้น แสดงว่าชั้นข้อความแบบโปร่งใสทำงาน

---

## ขั้นตอนที่ 5: ขยายไปยังเอกสารหลายหน้า (convert scanned image pdf)

สัญญาในชีวิตจริงมักมีหลายหน้า เพื่อ **แปลงไฟล์ PDF จากภาพสแกน** ที่มีหลายหน้า ให้วนลูปแต่ละหน้า, OCR แล้วต่อ PDF ที่ได้เข้าด้วยกัน

```python
def ocr_image_to_pdf(image_obj, lang="eng"):
    """Helper that returns PDF bytes for a single image."""
    return pytesseract.image_to_pdf_or_hocr(image_obj, lang=lang, extension='pdf')

def merge_pdfs(pdf_bytes_list):
    """Combine multiple PDF byte streams into one."""
    from PyPDF2 import PdfMerger
    merger = PdfMerger()
    for i, pdf_bytes in enumerate(pdf_bytes_list):
        merger.append(io.BytesIO(pdf_bytes))
    output = io.BytesIO()
    merger.write(output)
    merger.close()
    return output.getvalue()

# Example: convert a multi‑page scanned PDF to searchable PDF
pages = convert_from_path("YOUR_DIRECTORY/scanned_contract.pdf", dpi=300)
pdf_parts = [ocr_image_to_pdf(p, lang=ocr_language) for p in pages]
final_pdf = merge_pdfs(pdf_parts)

with open("YOUR_DIRECTORY/contract_searchable.pdf", "wb") as f:
    f.write(final_pdf)

print("✅ Multi‑page searchable PDF created.")
```

**ทำไมต้องรวม?** แต่ละครั้งที่เรียก `image_to_pdf_or_hocr` จะสร้าง PDF แยกส่วน การรวมเข้าด้วยกันทำให้เอกสารสุดท้ายรักษาลำดับหน้าตามต้นฉบับ

---

## ข้อผิดพลาดทั่วไป & วิธีแก้

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| ไม่สามารถค้นหาข้อความหลังเปิด PDF | Tesseract ไม่พบอักขระใด ๆ (ผลลัพธ์ว่าง) | ตรวจสอบคุณภาพภาพ, เพิ่ม DPI, หรือทำการเตรียมภาพ (คอนทราสต์, binarization) |
| ตัวอักษรแปลก (เช่น �) | ใช้แพ็คภาษาไม่ตรงหรือฟอนต์หาย | ติดตั้งข้อมูลภาษาให้ถูก (`tesseract‑lang‑eng`) และตรวจสอบให้ `ocr_language` ตรงกัน |
| ขนาดไฟล์ PDF ใหญ่เกิน (>10 MB สำหรับภาพหน้าเดียว) | ใช้ PNG lossless เป็นแหล่ง; OCR เพิ่มภาพความละเอียดเต็ม | ลดขนาดภาพก่อน OCR (`image.thumbnail((1240, 1754))` สำหรับ A4) |
| สคริปต์พังบน Windows พร้อมข้อความ “tesseract.exe not found” | ไฟล์ไบนารีของ Tesseract ไม่อยู่ใน PATH | เพิ่ม `pytesseract.pytesseract.tesseract_cmd = r"C:\\Program Files\\Tesseract-OCR\\tesseract.exe"` (ปรับเส้นทางให้ตรง) |

---

## สคริปต์เต็มพร้อมใช้งาน

รวมทุกอย่างเข้าด้วยกัน นี่คือไฟล์เดียวที่คุณสามารถคัดลอก‑วางและรันได้:

```python
#!/usr/bin/env python3
"""
create_searchable_pdf.py
A complete example that converts a scanned PNG (or PDF) into a searchable PDF using Tesseract OCR.
"""

import io
import sys
from pathlib import Path

import pytesseract
from pdf2image import convert_from_path
from PIL import Image
from PyPDF2 import PdfMerger

# -------------------- Configuration --------------------
# Adjust these paths for your environment
TESSERACT_CMD = r"/usr/local/bin/tesseract"   # macOS/Linux
# TESSERACT_CMD = r"C:\\Program Files\\Tesseract-OCR\\tesseract.exe"  # Windows
OCR_LANGUAGE = "eng"                         # Add '+spa' for Spanish, etc.
INPUT_PATH = Path("YOUR_DIRECTORY/scanned_agreement.png")
OUTPUT_PATH = Path("YOUR_DIRECTORY/agreement_searchable.pdf")
# -------------------------------------------------------

# Point pytesseract at the executable
pytesseract.pytesseract.tesseract_cmd = TESSERACT_CMD

def load_image(path: Path) -> Image.Image:
    """Load an image from disk; supports PNG, JPG, TIFF."""
    if not path.is_file():
        sys.exit(f"❌ File not found: {path}")
    return Image.open(path)

def ocr_to_pdf_bytes(img: Image.Image, lang: str = OCR_LANGUAGE) -> bytes:
    """Run OCR on a Pillow image and return PDF bytes with hidden text."""
    return pytesseract.image_to_pdf_or_hocr(img, lang=lang, extension='pdf')

def write_pdf(data: bytes, dest: Path):
    """Write PDF byte stream to a file."""
    dest.parent.mkdir(parents=True, exist_ok=True)
    with open(dest, "wb") as f:
        f.write(data)
    print(f"✅ Searchable PDF saved to {dest}")

def main():
    # Load the scanned image
    image = load_image(INPUT_PATH)

    # Optional: improve contrast for low‑quality scans
    # image = image.convert('L').point(lambda x: 0 if x < 128 else 255, '1')

    # OCR → PDF bytes
    pdf_bytes = ocr_to_pdf_bytes(image)

    # Save the result
    write_pdf(pdf_bytes, OUTPUT_PATH)

if __name__ == "__main__":
    main()
```

บันทึกเป็น `create_searchable_pdf.py`, แทนที่ตัวแปร placeholder ด้วยเส้นทางจริงของคุณ, แล้วรัน:

```bash
python create_searchable_pdf.py
```

คุณควรจะเห็น

## คุณควรเรียนรู้อะไรต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคในคู่มือนี้ แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโปรเจกต์ของคุณ

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [OCR Recognizing PDF Documents in Aspose.OCR for Java](/ocr/hongkong/java/ocr-operations/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}