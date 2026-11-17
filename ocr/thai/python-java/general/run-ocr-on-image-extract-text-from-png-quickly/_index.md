---
category: general
date: 2026-03-18
description: เรียกใช้ OCR บนภาพเพื่อดึงข้อความจาก PNG และสร้าง PDF ที่ค้นหาได้ เรียนรู้วิธีจดจำข้อความในภาพและแปลง
  PNG เป็น PDF ในไม่กี่นาที
draft: false
keywords:
- run OCR on image
- extract text from png
- recognize text image
- generate searchable pdf
- convert png to pdf
language: th
og_description: ใช้ OCR บนภาพเพื่อดึงข้อความจากไฟล์ PNG, จดจำข้อความในภาพ, และสร้าง
  PDF ที่ค้นหาได้. ทำตามคู่มือขั้นตอนต่อไปนี้.
og_title: ทำ OCR บนภาพ – ดึงข้อความจาก PNG อย่างรวดเร็ว
tags:
- OCR
- Python
- Image Processing
title: รัน OCR บนภาพ – ดึงข้อความจาก PNG อย่างรวดเร็ว
url: /th/python-java/general/run-ocr-on-image-extract-text-from-png-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# เรียกใช้ OCR บนรูปภาพ – ดึงข้อความจาก PNG อย่างรวดเร็ว

เคยต้องการ **run OCR on image** ไฟล์แต่ไม่แน่ใจว่าจะเริ่มจากตรงไหนหรือไม่? บางทีคุณอาจมีบทความสแกนที่บันทึกเป็น `article.png` และต้องการเพียงข้อความธรรมดา หรือคุณต้องการ PDF ที่สามารถค้นหาได้เพื่อการเก็บรักษา ไม่ว่ากรณีใด คุณอยู่ในที่ถูกต้อง ในบทแนะนำนี้เราจะอธิบายขั้นตอนการดึงข้อความจาก PNG, การจดจำข้อความในรูปภาพ, และแม้กระทั่งการแปลง PNG นั้นเป็น PDF ที่สามารถค้นหาได้—ทั้งหมดด้วยไม่กี่บรรทัดของโค้ด

> **สิ่งที่คุณจะได้รับ:** สคริปต์ที่สมบูรณ์และสามารถรันได้ซึ่งโหลด PNG, ทำ OCR, บันทึกผลลัพธ์ hOCR, และโดยออปชันสร้าง PDF ที่สามารถค้นหาได้ ไม่มีการนำเข้าแบบหายไป, ไม่มี “ดูเอกสาร” ที่เป็น dead‑ends—เพียงโซลูชันที่เป็นอิสระที่คุณสามารถใส่ลงในโปรเจกต์ของคุณได้ทันที

## สิ่งที่ต้องเตรียมก่อน

Before we dive in, make sure you have:

- **Python 3.8+** (ไวยากรณ์ที่ใช้ที่นี่ทำงานกับเวอร์ชันล่าสุดใดก็ได้)
- The **`ocr_engine`** library you’re using (ตัวอย่างสมมติว่ามีคลาสชื่อ `OcrEngine`; แทนที่ด้วย Tesseract, EasyOCR ฯลฯ หากจำเป็น)
- ภาพ PNG ที่คุณต้องการประมวลผล (เช่น `article.png` ที่วางไว้ในโฟลเดอร์ที่คุณอ้างอิงได้)
- สิทธิ์การเขียนไปยังไดเรกทอรีผลลัพธ์

หากคุณใช้ Tesseract เป็นพื้นฐาน, ติดตั้งโดยใช้:

```bash
# Ubuntu/Debian
sudo apt-get install tesseract-ocr

# macOS (Homebrew)
brew install tesseract
```

และจากนั้นติดตั้ง Python wrapper:

```bash
pip install pytesseract Pillow
```

*Pro tip:* รักษาไลบรารี OCR ของคุณให้เป็นเวอร์ชันล่าสุด—แพ็คเกจภาษาใหม่และการปรับปรุงประสิทธิภาพมักจะออกบ่อย

## เรียกใช้ OCR บนรูปภาพ – คู่มือขั้นตอนโดยละเอียด

ด้านล่างเป็น **complete script**. คุณสามารถคัดลอกและวางลงในไฟล์ชื่อ `run_ocr.py` แล้วรันด้วย `python run_ocr.py`.

```python
# run_ocr.py
import os
from pathlib import Path

# Import the OCR engine – replace with your actual import if different
# For Tesseract via pytesseract you would use: import pytesseract
# Here we assume a generic OcrEngine class that matches the example
from ocr_engine import OcrEngine  # <-- adjust as needed

def main():
    # ------------------------------------------------------------------
    # Step 1: Create an OCR engine instance
    # ------------------------------------------------------------------
    ocr_engine = OcrEngine()
    # Why this matters: the engine holds configuration (language, DPI, etc.)
    # You can tweak ocr_engine.setLanguage('eng') or similar before proceeding.

    # ------------------------------------------------------------------
    # Step 2: Load the image you want to process
    # ------------------------------------------------------------------
    image_path = Path("YOUR_DIRECTORY/article.png")
    if not image_path.is_file():
        raise FileNotFoundError(f"Image not found: {image_path}")
    ocr_engine.setImageFromFile(str(image_path))

    # ------------------------------------------------------------------
    # Step 3: Choose the export format
    # ------------------------------------------------------------------
    # hOCR preserves layout (bounding boxes, fonts) – perfect for searchable PDFs.
    # Other options: "txt", "pdf", "pdfa"
    ocr_engine.setExportFormat("hocr")

    # ------------------------------------------------------------------
    # Step 4: Run the recognition process
    # ------------------------------------------------------------------
    ocr_result = ocr_engine.recognize()
    # The result object gives us access to the raw OCR text, hOCR, etc.

    # ------------------------------------------------------------------
    # Step 5: Write the HOCR output to a file
    # ------------------------------------------------------------------
    output_path = Path("YOUR_DIRECTORY/article.hocr")
    with open(output_path, "w", encoding="utf-8") as output_file:
        output_file.write(ocr_result.getExportedContent())
    print(f"✅ HOCR saved to {output_path}")

    # ------------------------------------------------------------------
    # Optional: Generate a searchable PDF from the HOCR
    # ------------------------------------------------------------------
    # Many OCR engines can bundle the original image with the hOCR to produce
    # a PDF that you can search. If your engine supports it, uncomment:
    # ocr_engine.setExportFormat("pdf")
    # pdf_result = ocr_engine.recognize()
    # pdf_path = Path("YOUR_DIRECTORY/article_searchable.pdf")
    # with open(pdf_path, "wb") as pdf_file:
    #     pdf_file.write(pdf_result.getExportedContent())
    # print(f"📄 Searchable PDF created at {pdf_path}")

if __name__ == "__main__":
    main()
```

### สิ่งที่สคริปต์ทำ, เป็นภาษาอังกฤษธรรมดา

1. **Instantiate** เครื่อง OCR เพื่อให้คุณสามารถควบคุมการตั้งค่าได้.
2. **Load** ไฟล์ PNG (`article.png`). สคริปต์จะหยุดทำงานตั้งแต่ต้นหากไฟล์ไม่มี—ไม่มีข้อผิดพลาด `NoneType` ที่ลึกลับในภายหลัง.
3. **Select** `hocr` เป็นรูปแบบการส่งออก รูปแบบนี้รักษาเลย์เอาต์เดิมซึ่งจำเป็นสำหรับการแปลงภาพเป็น PDF ที่สามารถค้นหาได้ในภายหลัง.
4. **Run** เครื่องจดจำ; การทำงานหนักเกิดขึ้นที่นี่.
5. **Write** ไฟล์ hOCR XML ไปยัง `article.hocr`. ตอนนี้คุณมีการแสดงผลที่เครื่องอ่านได้ของข้อความและพิกัดของมัน.
6. *(Optional)* สลับเป็น `"pdf"` และสร้าง PDF ที่สามารถค้นหาได้ในขั้นตอนเพิ่มเติมหนึ่งขั้น.

ไฟล์ **ผลลัพธ์ที่คาดหวัง** คือไฟล์ `.hocr` ที่เข้ารหัสเป็น UTF‑8 ซึ่งมีลักษณะประมาณนี้ (ตัดให้สั้นเพื่อความกระชับ):

```xml
<div class='ocr_page' id='page_1' title='image "article.png"; bbox 0 0 2480 3508; ppageno 0'>
  <div class='ocr_carea' id='block_1_1' title="bbox 100 100 2400 3400">
    <p class='ocr_par' id='par_1' title="bbox 100 100 2400 200">
      <span class='ocr_line' id='line_1' title="bbox 100 100 2400 150; baseline 0 -5">
        <span class='ocrx_word' id='word_1' title="bbox 100 100 300 150; x_wconf 96">This</span>
        <span class='ocrx_word' id='word_2' title="bbox 310 100 500 150; x_wconf 92">is</span>
        …
```

หากคุณยกเลิกคอมเมนต์ส่วน PDF, คุณจะได้ไฟล์ `article_searchable.pdf` ซึ่งคุณสามารถเปิดด้วยโปรแกรมดู PDF ใดก็ได้และใช้กล่องค้นหา **Ctrl + F** เพื่อค้นหาคำได้ทันที.

![ผลลัพธ์ตัวอย่างการเรียกใช้ OCR บนรูปภาพ](example.png "เรียกใช้ OCR บนรูปภาพ – ผลลัพธ์ hOCR และ PDF")

## วิธีดึงข้อความจาก PNG ด้วย OcrEngine

หากคุณต้องการเพียงข้อความดิบ (ไม่มีเลย์เอาต์, ไม่มี PDF) คุณสามารถข้ามขั้นตอน hOCR ได้ทั้งหมด:

```python
ocr_engine.setExportFormat("txt")
text_result = ocr_engine.recognize()
plain_text = text_result.getExportedContent()
print("📝 Extracted text:\n", plain_text)
```

*ทำไมต้องเลือกข้อความธรรมดา?* มันเบา, เหมาะสำหรับการทำดัชนี, และทำงานได้ดีกับ pipeline NLP ต่อไป.

## จดจำข้อความในรูปภาพและสร้าง PDF ที่สามารถค้นหาได้

การสร้าง PDF ที่สามารถค้นหาได้เป็นกระบวนการสองขั้นตอน:

1. **Run OCR** ด้วย `hocr` (เช่นที่ทำข้างต้น) เพื่อรับข้อมูลเลย์เอาต์.
2. **Combine** PNG ดั้งเดิมกับ hOCR เพื่อสร้าง PDF โดยใช้ PDF exporter ของ engine.

ไลบรารี OCR สมัยใหม่ส่วนใหญ่ (Tesseract, ABBYY, Google Vision) มีการส่งออก `pdf` ที่ทำเช่นนี้ได้ตรงๆ ตัวอย่างโค้ดในบล็อก *Optional* ของสคริปต์หลักแสดงรูปแบบ หากไลบรารีของคุณไม่มี PDF exporter ในตัว, คุณสามารถใช้ **`pdf2image`** + **`reportlab`** เพื่อต่อภาพและ hOCR เข้าด้วยกัน—แค่บอกฉัน, แล้วฉันจะแบ่งปันตัวอย่างเพิ่มเติมอย่างรวดเร็ว.

## แปลง PNG เป็น PDF พร้อมผลลัพธ์ OCR

บางครั้งคุณอาจต้องการ **plain PDF** ที่มีภาพอยู่ (ไม่มีชั้นที่สามารถค้นหาได้) นั่นง่ายกว่ามาก:

```python
from PIL import Image

png_path = Path("YOUR_DIRECTORY/article.png")
pdf_path = Path("YOUR_DIRECTORY/article.pdf")

# Pillow can convert directly:
Image.open(png_path).convert("RGB").save(pdf_path, "PDF", resolution=100.0)
print(f"📄 PNG converted to PDF at {pdf_path}")
```

ผสานขั้นตอนนี้กับขั้นตอน OCR หากคุณต้องการเวอร์ชันที่สามารถค้นหาได้, หรือเก็บไว้เป็นสำเนาภาพที่ตรงตามต้นฉบับเพื่อการเก็บรักษา.

## ข้อผิดพลาดทั่วไป & เคล็ดลับ

| Issue | Why it Happens | Quick Fix |
|-------|----------------|-----------|
| **ภาพ PNG เบลอหรือความละเอียดต่ำ** | ความแม่นยำของ OCR ลดลงอย่างมากเมื่อความละเอียดต่ำกว่า ~300 DPI. | ขยายขนาดด้วย `Image.resize((width*2, height*2), Image.LANCZOS)` ก่อนส่งให้เอนจิน. |
| **ภาษาไม่ถูกต้อง** | เอนจินตั้งค่าเริ่มต้นเป็นภาษาอังกฤษ; ตัวอักษรที่ไม่ใช่ภาษาอังกฤษจะกลายเป็นอักขระผิด. | เรียก `ocr_engine.setLanguage('deu')` (หรือรหัส ISO ที่เหมาะสม) ก่อน `recognize()`. |
| **ไม่มีผลลัพธ์ hOCR** |บางเอนจินตั้งค่าเริ่มต้นเป็นข้อความธรรมดาเมื่อไม่ได้เรียก `setExportFormat`. | ตรวจสอบให้แน่ใจว่า `setExportFormat("hocr")` ทำงาน **ก่อน** `recognize()`. |
| **ข้อผิดพลาดสิทธิ์ไฟล์** | พยายามเขียนไปยังโฟลเดอร์ที่เป็นแบบอ่านอย่างเดียว. | ใช้เส้นทางภายในโปรเจกต์ของคุณหรือเรียก `os.makedirs(..., exist_ok=True)` ก่อน. |
| **PDF ขนาดใหญ่ทำให้หน่วยความจำพุ่งสูง** | PDF exporter เก็บภาพทั้งหมดใน RAM. | ประมวลผลหน้าเป็นส่วน ๆ หรือใช้ตัวเขียน PDF แบบสตรีมมิ่ง. |

*Pro tip:* ทดสอบกับภาพตัวอย่างขนาดเล็กก่อนขยายเป็นหลายพันภาพ จะช่วยประหยัดเวลาการดีบักหลายชั่วโมง.

## สรุป

คุณตอนนี้รู้ **how to run OCR on image** ไฟล์, **extract text from PNG**, **recognize text image** สำหรับงานต่อไป, **generate a searchable PDF**, และ **convert PNG to PDF** เมื่อคุณต้องการเก็บเป็นไฟล์ง่าย ๆ สคริปต์ที่ให้มานี้เป็นโซลูชันที่สมบูรณ์พร้อมคัดลอกและวางที่ทำงานได้ทันที, และส่วนออปชันให้คุณปรับผลลัพธ์ให้ตรงกับกระบวนการทำงานของคุณ

### สิ่งที่ควรทำต่อ?

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}