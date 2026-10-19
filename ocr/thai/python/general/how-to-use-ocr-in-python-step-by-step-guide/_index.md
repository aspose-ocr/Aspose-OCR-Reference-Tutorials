---
category: general
date: 2026-08-12
description: วิธีใช้ OCR ใน Python เพื่อจดจำข้อความจากภาพ, ดึงข้อความ, แปลงภาพเป็นข้อความ,
  และทำความสะอาดข้อความ OCR ด้วยการประมวลผลหลังจากด้วย AI
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use OCR
- recognize text from image
- extract text from image
- convert image to text
- clean up OCR text
language: th
lastmod: 2026-08-12
og_description: วิธีใช้ OCR ใน Python เพื่อแปลงรูปภาพเป็นข้อความที่แก้ไขได้ เรียนรู้การจดจำข้อความจากภาพ
  ดึงข้อความ แปลงภาพเป็นข้อความ และทำความสะอาดข้อความ OCR ด้วย AI
og_image_alt: Screenshot of Python code converting an image to clean text using OCR
  and AI post‑processing
og_title: วิธีใช้ OCR ใน Python – คู่มือการเขียนโปรแกรมครบถ้วน
schemas:
- author: Aspose
  dateModified: '2026-08-12'
  description: How to use OCR in Python to recognize text from image, extract text,
    convert image to text, and clean up OCR text with AI post‑processing.
  headline: How to use OCR in Python – step‑by‑step guide
  type: TechArticle
- description: How to use OCR in Python to recognize text from image, extract text,
    convert image to text, and clean up OCR text with AI post‑processing.
  name: How to use OCR in Python – step‑by‑step guide
  steps:
  - name: Loads an image file (PNG, JPEG, or TIFF).
    text: Loads an image file (PNG, JPEG, or TIFF).
  - name: Recognizes text from the image using an OCR engine.
    text: Recognizes text from the image using an OCR engine.
  - name: Improves the raw output with an AI‑driven post‑processor.
    text: Improves the raw output with an AI‑driven post‑processor.
  - name: Prints the cleaned‑up text to the console.
    text: Prints the cleaned‑up text to the console.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- AI post‑processing
title: วิธีใช้ OCR ใน Python – คู่มือขั้นตอนโดยละเอียด
url: /th/python/general/how-to-use-ocr-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีใช้ OCR ใน Python – คู่มือขั้นตอนต่อขั้นตอน

หากคุณต้องการ **how to use OCR** เพื่อแปลงเอกสารสแกนหรือภาพหน้าจอให้เป็นข้อความที่แก้ไขได้ บทแนะนำนี้จะแสดงวิธีแก้ไขแบบครบวงจรใน Python คุณจะได้เรียนรู้การจดจำข้อความจากภาพ, การดึงข้อความจากภาพ, การแปลงภาพเป็นข้อความ, และการทำความสะอาดข้อความ OCR ด้วย AI post‑processor ที่มีน้ำหนักเบา

คู่มือนี้ครอบคลุมทุกอย่างตั้งแต่การติดตั้งไลบรารีที่จำเป็นจนถึงการจัดการภาพคุณภาพต่ำ เพื่อให้คุณสามารถรวม OCR เข้าใน pipeline การทำงานอัตโนมัติใด ๆ ได้โดยไม่ต้องเดาว่าขั้นตอนไหนหายไป

## สิ่งที่คุณจะสร้าง

เมื่อจบบทความนี้คุณจะมีสคริปต์ Python เพียงไฟล์เดียวที่:

1. โหลดไฟล์ภาพ (PNG, JPEG หรือ TIFF).  
2. จดจำข้อความจากภาพโดยใช้ OCR engine.  
3. ปรับปรุงผลลัพธ์ดิบด้วย AI‑driven post‑processor.  
4. พิมพ์ข้อความที่ทำความสะอาดแล้วไปยังคอนโซล.

ไม่จำเป็นต้องใช้บริการภายนอก—ทุกอย่างทำงานในเครื่อง ทำให้โซลูชันนี้เหมาะกับสภาพแวดล้อมออฟไลน์หรือโครงการที่ต้องการความเป็นส่วนตัว

## ข้อกำหนดเบื้องต้น

- Python 3.9 หรือใหม่กว่า.  
- ไลบรารี `pytesseract` และ `Pillow` (`pip install pytesseract pillow`).  
- ไบนารี Tesseract‑OCR ติดตั้งและพร้อมใช้งานใน `PATH` ของระบบของคุณ.  
- ความเข้าใจพื้นฐานเกี่ยวกับฟังก์ชันใน Python.  

หากคุณมีรายการเหล่านี้แล้ว คุณสามารถข้ามไปยังโค้ดบล็อกแรกได้ทันที

## วิธีใช้ OCR กับ Python

หัวใจของ **how to use OCR** คือการเริ่มต้น OCR engine และป้อนภาพให้มัน ในบทแนะนำนี้เราจะใช้ `pytesseract` ซึ่งเป็น wrapper เบา ๆ รอบ ๆ engine ของ Tesseract แบบโอเพนซอร์ส

```python
import pytesseract
from PIL import Image

def load_image(path: str) -> Image.Image:
    """
    Open an image file and return a Pillow Image object.
    Pillow handles many formats (PNG, JPEG, TIFF) and ensures
    the image is in a mode that Tesseract can read.
    """
    return Image.open(path)
```

> **ทำไมขั้นตอนนี้ถึงสำคัญ** – Tesseract ต้องการภาพที่สะอาดและจัดแนวอย่างถูกต้อง การใช้ Pillow รับประกันว่าข้อมูลภาพจะถูกทำให้เป็นมาตรฐานก่อนที่ OCR จะทำงาน ซึ่งช่วยเพิ่มความแม่นยำของการดำเนินการ **recognize text from image** ถัดไป.

## จดจำข้อความจากภาพ

ตอนนี้เราจะเรียก `pytesseract.image_to_string` เพื่อดึงสตริงดิบ นี่คือการเรียกแบบคลาสสิก “recognize text from image”

```python
def ocr_recognize(image: Image.Image) -> str:
    """
    Run Tesseract OCR on the supplied image and return the raw text.
    """
    raw_text = pytesseract.image_to_string(image, lang='eng')
    return raw_text
```

> **ทำไมเราถึงแยกฟังก์ชันนี้** – การแยกขั้นตอน OCR ทำให้คุณสามารถสลับ engine ในภายหลัง (เช่น เปลี่ยนเป็น EasyOCR) โดยไม่ต้องแก้ไขส่วนอื่นของ pipeline อีกทั้งยังทำให้การทดสอบหน่วยง่ายขึ้น

## ดึงข้อความจากภาพและปรับปรุงคุณภาพ

ผลลัพธ์ OCR ดิบมักมีการขึ้นบรรทัดใหม่, ตัวอักษรแปลกปลอม, หรือคำที่จดจำผิด AI post‑processor สามารถทำความสะอาดสิ่งเหล่านี้โดยอัตโนมัติ ด้านล่างเป็นตัวอย่างขั้นต่ำที่ใช้ไลบรารี `transformers` เพื่อรันโมเดลภาษาเล็ก ๆ ในเครื่อง คุณสามารถเปลี่ยนเป็นบริการใด ๆ ที่เป็นของคุณได้หากต้องการ

```python
from transformers import pipeline

# Initialize a zero‑shot text‑generation pipeline once (expensive operation)
_ai_postprocessor = pipeline("text2text-generation", model="google/flan-t5-small")

def clean_ocr_text(raw: str) -> str:
    """
    Send the raw OCR string to a lightweight AI model that rewrites
    the text, removing obvious errors and normalizing whitespace.
    """
    # The prompt guides the model to act as a post‑processor
    prompt = f"Clean up the following OCR output, fixing spelling mistakes and removing extra line breaks:\n\n{raw}"
    result = _ai_postprocessor(prompt, max_length=512, do_sample=False)
    # The pipeline returns a list of dicts; we take the generated text
    cleaned = result[0]["generated_text"]
    return cleaned.strip()
```

> **ทำไม AI post‑processor ถึงช่วยได้** – OCR engine แบบดั้งเดิมเก่งในการจดจำอักขระแต่มีปัญหาเรื่องการจัดวางและสัญญาณรบกวน โมเดลภาษาเข้าใจบริบท จึงสามารถเปลี่ยน “Th1s 1s 4 test.” ให้เป็น “This is a test.” ขั้นตอนนี้ตอบสนองโดยตรงต่อความต้องการ **clean up OCR text**

## แปลงภาพเป็นข้อความ – สคริปต์เต็ม

การรวมทุกอย่างเข้าด้วยกันจะได้สคริปต์สั้น ๆ ที่ **convert image to text** ตั้งแต่ต้นจนจบ

```python
import sys
from pathlib import Path

def main(image_path: str):
    """
    Complete pipeline:
    1. Load image.
    2. Recognize text from image.
    3. Clean up OCR text.
    4. Print the final result.
    """
    # 1️⃣ Load the image file
    img = load_image(image_path)

    # 2️⃣ Recognize text from image (raw OCR)
    raw_text = ocr_recognize(img)
    print("=== Raw OCR output ===")
    print(raw_text)
    print("\n---\n")

    # 3️⃣ Clean up OCR text with AI post‑processor
    cleaned_text = clean_ocr_text(raw_text)
    print("=== Cleaned‑up text ===")
    print(cleaned_text)

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python ocr_pipeline.py <path-to-image>")
        sys.exit(1)

    image_file = Path(sys.argv[1])
    if not image_file.is_file():
        print(f"Error: file '{image_file}' does not exist.")
        sys.exit(1)

    main(str(image_file))
```

### ผลลัพธ์ที่คาดหวัง

การรันสคริปต์ด้วยภาพตัวอย่าง (`sample.png`) อาจให้ผลลัพธ์ดังนี้:

```
=== Raw OCR output ===
Th1s 1s 4 sampl3
text from an im4ge.

--- 

=== Cleaned‑up text ===
This is a sample text from an image.
```

สังเกตว่า AI post‑processor ได้แก้ไขอักขระที่อ่านผิดและลบการขึ้นบรรทัดใหม่ที่ไม่ต้องการ นี่แสดงให้เห็น workflow **extract text from image** ทั้งหมดและแสดงประโยชน์ของการทำความสะอาด OCR text

## การจัดการกรณีขอบที่พบบ่อย

| Situation | Recommended tweak |
|----------------------------------------|---------------------------------------------------------------------------------|
| Low‑contrast image | แปลงเป็น grayscale และเพิ่มความคอนทราสต์ด้วย `ImageEnhance` ก่อน OCR. |
| Multi‑language document | ส่งรายการคั่นด้วยคอมม่าให้กับ `lang` (เช่น `lang='eng+fra'`). |
| Very large images ( > 2000 px ) | ลดขนาดด้วย `img.thumbnail((2000, 2000))` เพื่อเร่งความเร็วของ Tesseract. |
| Missing Tesseract binary | ตรวจสอบว่า `pytesseract.pytesseract.tesseract_cmd` ชี้ไปที่ไฟล์ executable. |
| AI post‑processor too slow | ใช้โมเดลที่เล็กกว่า (`t5-small`) หรือรัน post‑processor บน GPU. |

> **เคล็ดลับมืออาชีพ:** แคชอ็อบเจ็กต์โมเดล AI (`_ai_postprocessor`) ตอน import โมดูล ตามที่แสดง เพื่อหลีกเลี่ยงการโหลดซ้ำในทุกการเรียกใช้ ซึ่งจะลดความหน่วงอย่างมากเมื่อประมวลผลภาพจำนวนมาก

## วิธีทางเลือก

- **EasyOCR**: ไลบรารี OCR แบบ pure‑Python ที่รองรับกว่า 80 ภาษาโดยไม่ต้องใช้ไบนารีภายนอก แทนที่ `ocr_recognize` ด้วย `EasyOCR.Reader` หากคุณต้องการโซลูชันที่ใช้ pip เท่านั้น.
- **Cloud OCR APIs**: Google Cloud Vision, Azure Computer Vision หรือ Amazon Textract ให้ความแม่นยำสูงกว่าในเลย์เอาต์ที่ซับซ้อน แต่ต้องการการเข้าถึงเครือข่ายและการเรียกเก็บเงิน.
- **Custom post‑processing**: สำหรับการทำความสะอาดแบบกำหนดผลลัพธ์ สามารถใช้ regular expressions (`re.sub`) เพื่อแก้ไขรูปแบบทั่วไป (เช่น การลบการขึ้นบรรทัดใหม่ที่มี hyphen) โดยไม่ต้องใช้โมเดล AI.

## สรุป

ตอนนี้คุณรู้ **how to use OCR** ใน Python เพื่อจดจำข้อความจากภาพ, ดึงข้อความจากภาพ, แปลงภาพเป็นข้อความ, และทำความสะอาด OCR text ด้วย AI post‑processor สคริปต์เต็มแสดง pipeline ที่พร้อมใช้งานในผลิตภัณฑ์ซึ่งคุณสามารถขยายต่อด้วยการ preprocessing เพิ่มเติม (ลดสัญญาณรบกวน, แก้ไขการเอียง) หรือการกระทำต่อเนื่อง (บันทึกลงฐานข้อมูล, ป้อนเข้าสู่ดัชนีการค้นหา).

### ขั้นตอนต่อไป

- ทดลองใช้โมเดล AI ต่าง ๆ (เช่น `gpt‑2`, `flan‑ul2`) เพื่อดูว่าโมเดลใดให้การทำความสะอาดที่ดีที่สุดสำหรับโดเมนของคุณ.  
- ผสาน pipeline เข้ากับเว็บเซอร์วิสโดยใช้ Flask หรือ FastAPI เพื่อเปลี่ยนสคริปต์เป็น endpoint OCR ตามความต้องการ.  
- สำรวจการประมวลผลแบบแบตช์: วนลูปผ่านไดเรกทอรีของภาพและเขียนผลลัพธ์ที่ทำความสะอาดแต่ละไฟล์ไปยังไฟล์ `.txt` ที่สอดคล้องกัน.

อย่าลังเลที่จะแก้ไขโค้ดให้เข้ากับ workflow ของคุณเอง และให้ข้อความที่สะอาดและค้นหาได้เสริมพลังให้ขั้นตอนต่อไปของแอปพลิเคชันของคุณ. Happy coding!

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอนต่อขั้นตอน เพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานทางเลือกในโครงการของคุณ.

- [แปลงภาพเป็นข้อความ: ดึงข้อความจากภาพโดยใช้ Aspose OCR (Python)](/ocr/english/python/general/convert-image-to-text-extract-text-from-image-using-aspose-o/)
- [ดึงข้อความจากภาพด้วย Aspose OCR – คู่มือขั้นตอนต่อขั้นตอน](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [ดึงข้อความจากภาพ – การปรับแต่ง OCR ด้วย Aspose.OCR สำหรับ .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}