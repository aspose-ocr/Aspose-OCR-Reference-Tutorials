---
category: general
date: 2026-06-19
description: ทำ OCR บนภาพโดยใช้ไลบรารี ocr ของ Python เรียนรู้วิธีตรวจจับข้อความจากภาพ,
  จดจำข้อความจากไฟล์ JPEG, และสกัดข้อความจากภาพสแกนอย่างมีประสิทธิภาพ.
draft: false
keywords:
- perform OCR on image
- recognize text from jpeg
- detect text from image
- extract text from scanned image
- load image for OCR
language: th
og_description: ทำ OCR บนภาพด้วย Python และดึงข้อความจากไฟล์สแกน คู่มือนี้จะพาคุณผ่านขั้นตอนการโหลดภาพ
  การแก้ไขการเอียง และการจดจำข้อความอย่างเป็นขั้นตอน
og_title: ทำ OCR บนรูปภาพด้วย Python – คู่มือการสกัดข้อความเต็มรูปแบบ
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Perform OCR on image using Python's ocr library. Learn how to detect
    text from image, recognize text from jpeg, and extract text from scanned image
    efficiently.
  headline: Perform OCR on Image in Python – Full Text Extraction Guide
  type: TechArticle
- description: Perform OCR on image using Python's ocr library. Learn how to detect
    text from image, recognize text from jpeg, and extract text from scanned image
    efficiently.
  name: Perform OCR on Image in Python – Full Text Extraction Guide
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed (the example uses the `ocr` package available via
      `pip install ocr-lib` – replace with your actual library name). - Basic familiarity
      with Python functions and virtual environments. - An image file (JPEG, PNG,
      TIFF) you want to process; we’ll use `skewed_page.jpg` as a placeh'
  - name: Recognize Text from JPEG vs PNG
    text: 'Both formats are supported, but JPEG compression can introduce artifacts
      that confuse the engine. If you notice frequent mis‑recognitions, try converting
      the JPEG to PNG first:'
  - name: Detect Text from Image with Multiple Languages
    text: 'If your document mixes English and Spanish, set a multilingual mode:'
  - name: Extract Text from Scanned PDFs
    text: 'For PDFs, you need to rasterize each page into an image first. Libraries
      like `pdf2image` make this painless:'
  type: HowTo
- questions:
  - answer: Absolutely. The library works without a GUI; just ensure the necessary
      native binaries (e.g., Tesseract) are installed on the server.
    question: Can I run this on a headless server?
  - answer: Consider adding a sharpening filter before `engine.recognize`. Many OCR
      libraries expose `image_preprocessing.sharpen = True` or you can use OpenCV’s
      `cv2.GaussianBlur` in reverse.
    question: What if the image is blurry?
  - answer: 'Yes. Wrap `perform_ocr` in a loop over a list of file paths, ## What
      Should You Learn Next?


      The following tutorials cover closely related topics that build on the techniques
      demonstrated in this guide. Each resource includes complete working code examples
      with step-by-step explanations to help you master additional API features and
      explore alternative implementation approaches in your own projects.

      - [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
      - [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
      - [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

      {{< /blocks/products/pf/tutorial-page-section >}} {{< /blocks/products/pf/main-container
      >}} {{< /blocks/products/pf/main-wrap-class >}} {{< blocks/products/products-backtop-button
      >}}'
    question: Does the script support batch processing?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: ทำ OCR บนรูปภาพด้วย Python – คู่มือการสกัดข้อความเต็มรูปแบบ
url: /th/python-java/general/perform-ocr-on-image-in-python-full-text-extraction-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ทำ OCR บนรูปภาพด้วย Python – คู่มือการสกัดข้อความเต็มรูปแบบ

เคยต้องการ **perform OCR on image** ไฟล์แต่เจออุปสรรคเพราะโค้ดดูซับซ้อน? คุณไม่ใช่คนเดียว ไม่ว่าจะเปลี่ยนใบเสร็จสแกนเป็น PDF ที่ค้นหาได้หรือดึงคำบรรยายจาก JPEG สำหรับโครงการ data‑science ความสามารถในการจดจำข้อความจาก JPEG และรูปแบบอื่นเป็นทักษะที่จำเป็นสำหรับนักพัฒนาทุกคนในวันนี้.

ในบทแนะนำนี้เราจะพาคุณผ่านตัวอย่างที่สมบูรณ์และสามารถรันได้ ซึ่งจะแสดงวิธี **detect text from image** ไฟล์, **extract text from scanned image** เอกสาร, และแม้กระทั่ง **load image for OCR** ด้วยเพียงไม่กี่บรรทัด เมื่อจบคุณจะได้โค้ดสแนปช็อตที่พร้อมใช้งานในระดับ production ที่สามารถนำไปใส่ในโปรเจกต์ของคุณได้—ไม่มีการนำเข้าแบบหายไป ไม่มีทางลัด “ดูเอกสาร” ที่คลุมเครือ.

## สิ่งที่คุณจะสร้าง

- สคริปต์ Python เล็ก ๆ ที่สร้าง OCR engine, เปิดใช้งาน auto‑deskew, โหลด JPEG (หรือรูปแบบที่รองรับใด ๆ) และพิมพ์ข้อความที่จดจำได้.
- คำอธิบายของ **why** แต่ละการตั้งค่า ทำไมจึงสำคัญ, ไม่ใช่แค่ **how** ที่พิมพ์.
- เคล็ดลับการจัดการ PDF หลายหน้า, ภาษาไม่ใช่ภาษาอังกฤษ, และข้อผิดพลาดทั่วไปเช่นสแกนเบลอ.

### ข้อกำหนดเบื้องต้น

- ติดตั้ง Python 3.8+ (ตัวอย่างใช้แพคเกจ `ocr` ที่สามารถติดตั้งได้ด้วย `pip install ocr-lib` – แทนที่ด้วยชื่อไลบรารีของคุณ).
- ความคุ้นเคยพื้นฐานกับฟังก์ชัน Python และ virtual environments.
- ไฟล์รูปภาพ (JPEG, PNG, TIFF) ที่คุณต้องการประมวลผล; เราจะใช้ `skewed_page.jpg` เป็นตัวอย่าง.

> **Pro tip:** หากคุณใช้ Windows ให้รันเทอร์มินัลในฐานะ Administrator ขณะติดตั้งไลบรารี OCR เพื่อหลีกเลี่ยงปัญหาการอนุญาต.

## ทำ OCR บนรูปภาพ – การตั้งค่าและการกำหนดค่า

สิ่งแรกที่คุณต้องการคืออินสแตนซ์ของ OCR engine ที่สะอาด คิดว่าเป็นสมองของการทำงาน; หากไม่มีการกำหนดค่าที่เหมาะสม แม้ภาพที่คมชัดที่สุดก็จะให้ผลลัพธ์เป็นข้อความไร้สาระ.

```python
# Step 1: Import the OCR library and create an engine
import ocr

engine = ocr.OcrEngine()
# Set the recognition language – English works for most cases
engine.language = ocr.Language.English
```

**Why this matters:**  
การตั้งค่า `engine.language` จะจำกัดชุดอักขระที่ OCR engine คาดหวัง, เพิ่มความแม่นยำอย่างมาก. หากข้ามขั้นตอนนี้, engine จะพยายามเดา ซึ่งมักทำให้คำง่าย ๆ ผิดพลาด.

## เปิดใช้งาน Automatic Deskew – แก้ไขการสแกนเอียง

หน้าที่สแกนมักไม่เรียบสมบูรณ์ การเอียงเล็กน้อยอาจทำให้การแยกอักขระผิดพลาด, ทำให้ “Hello” กลายเป็น “H3llo”. ธง `auto_deskew` จะทำงานหนักให้คุณ.

```python
# Step 2: Turn on automatic deskew to straighten tilted images
engine.image_preprocessing.auto_deskew = True
```

**Edge case:** หากคุณทราบว่ารูปภาพของคุณเรียงตรงอยู่แล้ว การปิด deskew สามารถลดเวลาประมวลผลลงหลายมิลลิวินาที—มีประโยชน์เมื่อจัดการกับหลายพันหน้าในงานแบช.

## โหลดรูปภาพสำหรับ OCR – รองรับ JPEG, PNG, TIFF

ตอนนี้เราจริง ๆ **load image for OCR**. เมธอด `ocr.Image.load` มีความยืดหยุ่น; มันรับพาธไปยังรูปแบบ raster ที่รองรับใด ๆ.

```python
# Step 3: Load the image you want to analyze
image_path = "YOUR_DIRECTORY/skewed_page.jpg"
image = ocr.Image.load(image_path)
```

> **Why this step is crucial:** ไลบรารีอ่านไฟล์เข้าสู่บิตแมพภายใน, ทำการแปลงสีที่จำเป็น. การข้ามขั้นตอนนี้และส่งสตรีมไบต์ดิบจะทำให้เกิด `FileNotFoundError` หรือแย่กว่า, ผลลัพธ์ว่างเปล่าโดยไม่มีการแจ้ง.

หากคุณต้องการ **recognize text from JPEG** โดยเฉพาะ, เพียงตรวจสอบให้ส่วนขยายไฟล์เป็น `.jpeg` หรือ `.jpg`. การเรียกเดียวกันทำงานกับ PNG (`.png`) หรือ TIFF (`.tif`) โดยไม่ต้องแก้ไข.

## ทำ OCR บนรูปภาพ – การรัน Engine

เมื่อ engine พร้อมและรูปภาพอยู่ในหน่วยความจำ, ถึงเวลาที่จะ **perform OCR on image** ข้อมูล. บรรทัดเดียวนี้ทำงานหนัก: การเตรียมข้อมูล, การแยกส่วน, การจำแนก, และการประกอบข้อความ.

```python
# Step 4: Run OCR and capture the result object
result = engine.recognize(image)
```

**What happens under the hood?**  
- Engine ใช้การแปลง deskew (หากเปิดใช้งาน).  
- มันรัน neural network หรือ backend ของ Tesseract เพื่อระบุอักขระ.  
- สุดท้าย, มันเชื่อมอักขระเป็นคำและบรรทัด, ส่งคืนอ็อบเจกต์ `result` ที่เต็มรูปแบบ.

## สกัดข้อความจากสแกนภาพ – แสดงผลลัพธ์

ขั้นตอนสุดท้ายคือ **extract text from scanned image** และแสดงผล. แอตทริบิวต์ `result.text` มีการแสดงผลเป็นข้อความธรรมดา.

```python
# Step 5: Print the detected text to the console
print("Detected text:")
print(result.text)
```

ผลลัพธ์ทั่วไปจะมีลักษณะดังนี้:

```
Detected text:
Invoice #12345
Date: 2023‑09‑01
Total: $1,234.56
Thank you for your business!
```

หาก OCR engine ไม่พบอักขระใด ๆ, `result.text` จะเป็นสตริงว่าง. ในกรณีนั้น, ตรวจสอบคุณภาพของรูปภาพอีกครั้งหรือพิจารณาปรับค่า `engine.confidence_threshold` (หากไลบรารีของคุณรองรับ).

## การจัดการกับความแตกต่างทั่วไป

### การจดจำข้อความจาก JPEG vs PNG

ทั้งสองรูปแบบได้รับการสนับสนุน, แต่การบีบอัด JPEG อาจทำให้เกิดอาร์ติแฟคต์ที่ทำให้ engine สับสน. หากคุณพบการจดจำผิดบ่อย, ลองแปลง JPEG เป็น PNG ก่อน:

```python
from PIL import Image
Image.open(image_path).save("temp.png", format="PNG")
image = ocr.Image.load("temp.png")
```

### การตรวจจับข้อความจากรูปภาพหลายภาษา

หากเอกสารของคุณผสมภาษาอังกฤษและสเปน, ตั้งค่าโหมดหลายภาษา:

```python
engine.language = ocr.Language.English | ocr.Language.Spanish
```

### สกัดข้อความจาก PDF ที่สแกน

สำหรับ PDF, คุณต้อง rasterize แต่ละหน้ามาเป็นรูปภาพก่อน. ไลบรารีอย่าง `pdf2image` ทำให้ขั้นตอนนี้ง่ายดาย:

```python
from pdf2image import convert_from_path

pages = convert_from_path("document.pdf", dpi=300)
for i, page_image in enumerate(pages):
    image = ocr.Image.from_pil(page_image)   # assuming the library accepts a PIL image
    result = engine.recognize(image)
    print(f"Page {i+1} text:")
    print(result.text)
```

## ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นสคริปต์เต็มที่คุณสามารถคัดลอก‑วางลงในไฟล์ `ocr_demo.py`. มันรวมการจัดการข้อผิดพลาดและตัวช่วยเล็ก ๆ เพื่อวัดเวลาในการทำงาน.

```python
import ocr
import time
import sys
from pathlib import Path

def perform_ocr(image_path: str) -> str:
    """
    Perform OCR on a given image file and return the extracted text.
    Handles auto‑deskew and basic error reporting.
    """
    if not Path(image_path).exists():
        sys.exit(f"❌ Error: File not found – {image_path}")

    engine = ocr.OcrEngine()
    engine.language = ocr.Language.English
    engine.image_preprocessing.auto_deskew = True

    try:
        image = ocr.Image.load(image_path)
    except Exception as e:
        sys.exit(f"❌ Failed to load image: {e}")

    start = time.time()
    result = engine.recognize(image)
    elapsed = time.time() - start

    if not result.text.strip():
        print("⚠️ No text detected. Try a higher‑resolution image or adjust preprocessing.")
    else:
        print(f"✅ OCR completed in {elapsed:.2f}s")
        print("Detected text:")
        print(result.text)

    return result.text

if __name__ == "__main__":
    # Replace with the path to your JPEG/PNG/TIFF file
    perform_ocr("YOUR_DIRECTORY/skewed_page.jpg")
```

**Expected output** (สมมติว่าการสแกนชัดเจน):

```
✅ OCR completed in 0.87s
Detected text:
Lorem ipsum dolor sit amet,
consectetur adipiscing elit.
```

## คำถามที่พบบ่อย

**Q: Can I run this on a headless server?**  
A: แน่นอน. ไลบรารีทำงานได้โดยไม่มี GUI; เพียงตรวจสอบให้แน่ใจว่าไบนารีเนทีฟที่จำเป็น (เช่น Tesseract) ถูกติดตั้งบนเซิร์ฟเวอร์.

**Q: What if the image is blurry?**  
A: พิจารณาเพิ่มฟิลเตอร์ทำให้คมก่อน `engine.recognize`. ไลบรารี OCR หลายตัวเปิดให้ใช้ `image_preprocessing.sharpen = True` หรือคุณสามารถใช้ `cv2.GaussianBlur` ของ OpenCV ในทางกลับกัน.

**Q: Does the script support batch processing?**  
A: ใช่. ห่อ `perform_ocr` ไว้ในลูปที่วนผ่านรายการของพาธไฟล์,

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}