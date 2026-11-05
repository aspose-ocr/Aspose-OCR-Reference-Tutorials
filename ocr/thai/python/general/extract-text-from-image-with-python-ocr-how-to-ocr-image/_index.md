---
category: general
date: 2026-05-31
description: ดึงข้อความจากภาพด้วยไลบรารี aocr ของ Python เรียนรู้วิธีทำ OCR กับภาพ
  โหลดภาพสำหรับ OCR และจดจำอักขระพิเศษได้ในไม่กี่บรรทัด.
draft: false
keywords:
- extract text from image
- recognize special characters
- convert image to text
- how to ocr image
- load image for ocr
language: th
og_description: ดึงข้อความจากรูปภาพโดยใช้ไลบรารี aocr ของ Python คู่มือนี้แสดงวิธีทำ
  OCR รูปภาพ โหลดรูปภาพสำหรับ OCR และจดจำอักขระพิเศษอย่างรวดเร็ว.
og_title: ดึงข้อความจากภาพด้วย Python OCR – วิธีทำ OCR กับภาพ
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Extract text from image using Python's aocr library. Learn how to OCR
    image, load image for OCR, and recognize special characters in just a few lines.
  headline: Extract Text from Image with Python OCR – How to OCR Image
  type: TechArticle
- description: Extract text from image using Python's aocr library. Learn how to OCR
    image, load image for OCR, and recognize special characters in just a few lines.
  name: Extract Text from Image with Python OCR – How to OCR Image
  steps:
  - name: 5.1 Low‑Resolution Images
    text: 'If the image is under 150 dpi, the OCR accuracy can drop dramatically.
      A quick fix is to upscale before feeding it to aocr:'
  - name: 5.2 Incorrect Language Detection
    text: 'aocr auto‑detects language, but you can force a specific script for better
      results:'
  - name: 5.3 Noise and Background Patterns
    text: 'A noisy background can confuse the model. Pre‑process with OpenCV to binarize:'
  type: HowTo
- questions:
  - answer: Not directly. Convert PDF pages to images first (e.g., using `pdf2image`)
      and then feed each image to aocr.
    question: Does this work on PDFs?
  - answer: For typical 300 dpi scans, aocr processes a page in ~0.3 s on a modern
      laptop—roughly twice as fast as vanilla Tesseract with default settings.
    question: How fast is aocr compared to Tesseract?
  - answer: 'Absolutely. Wrap the `main` function in a loop over `Path(folder).glob("*.png")`
      and collect results in a CSV. --- ## Conclusion You now have a solid, end‑to‑end
      workflow to **extract text from image** using Python’s aocr library. From loading
      the file to printing Unicode output, every step is expla'
    question: Can I batch‑process a folder of images?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
title: ดึงข้อความจากรูปภาพด้วย Python OCR – วิธีทำ OCR รูปภาพ
url: /th/python/general/extract-text-from-image-with-python-ocr-how-to-ocr-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ดึงข้อความจากรูปภาพด้วย Python OCR – วิธี OCR รูปภาพ

เคยต้อง **ดึงข้อความจากรูปภาพ** แต่ไม่แน่ใจว่าคลังใดจะจัดการกับสัญลักษณ์แปลก ๆ อย่าง “Ł”, “Ž”, หรือ “ß” ได้หรือไม่? คุณไม่ได้อยู่คนเดียว ในหลายโครงการจริง—เช่น ใบเสร็จสแกน, ป้ายหลายภาษา, หรือเอกสารประวัติศาสตร์—ความสามารถในการ **จดจำอักขระพิเศษ** สามารถเป็นความแตกต่างระหว่างชุดข้อมูลที่ใช้ได้และความล้มเหลว

ข่าวดีคือ? ด้วยเพียงไม่กี่บรรทัดของ Python และแพ็กเกจ **aocr** ที่เบา คุณสามารถแปลงรูปใดก็ได้ให้เป็นข้อความที่ค้นหาได้ ด้านล่างนี้คุณจะได้เห็นสคริปต์ที่พร้อมรันเต็มรูปแบบ พร้อมกับ *เหตุผล* ของแต่ละขั้นตอน เพื่อให้คุณไม่เพียงคัดลอก‑วาง แต่เข้าใจสิ่งที่เกิดขึ้นจริง

## สิ่งที่บทเรียนนี้ครอบคลุม

- การติดตั้งและนำเข้าไลบรารี **aocr**  
- การโหลดรูปภาพสำหรับ OCR (รวมถึงข้อผิดพลาดที่พบบ่อย)  
- การเรียกใช้เอนจินเพื่อ **แปลงรูปภาพเป็นข้อความ**  
- การพิมพ์ผลลัพธ์และการจัดการกับอักขระพิเศษ  
- การขยายกระบวนการพื้นฐานเพื่อรองรับหลายภาษาและการจัดการข้อผิดพลาด  

เมื่ออ่านจบคุณจะสามารถ **ดึงข้อความจากรูปภาพ** ของไฟล์ใดก็ได้ในทุกภาษา และจะรู้วิธีปรับแต่งกระบวนการเมื่อการตั้งค่าเริ่มต้นไม่เพียงพอ

## ข้อกำหนดเบื้องต้น

| Requirement | Why it matters |
|-------------|----------------|
| Python 3.8+ | aocr พึ่งพาฟีเจอร์ typing สมัยใหม่ |
| `pip` access | เพื่อติดตั้งไลบรารี |
| ตัวอย่างรูปภาพ (เช่น `multilingual.png`) | เราจะใช้ไฟล์นี้เพื่อสาธิตอักขระพิเศษ |
| ความคุ้นเคยพื้นฐานกับ virtual environments (ไม่บังคับ) | ช่วยให้การจัดการ dependencies เป็นระเบียบ |

ไม่ต้องใช้เครื่องมือภายนอกหนัก ๆ อย่าง Tesseract—**aocr** มีเอนจินประสาทเทียมที่เร็วและทำงานได้ทันที

---

## ขั้นตอนที่ 1: ติดตั้งไลบรารี aocr

แรกเริ่ม เปิดเทอร์มินัล (หรือคอนโซลของ IDE) แล้วรัน:

```bash
pip install aocr
```

*เคล็ดลับ:* หากคุณทำงานหลายโปรเจกต์พร้อมกัน ให้สร้าง virtual environment ก่อน:

```bash
python -m venv ocr-env
source ocr-env/bin/activate   # macOS/Linux
.\ocr-env\Scripts\activate    # Windows
pip install aocr
```

การทำเช่นนี้จะทำให้ dependencies ของ OCR แยกจากระบบหลัก—สิ่งที่ผมพบว่าช่วยลดปัญหาได้มากในภายหลัง

---

## ขั้นตอนที่ 2: โหลดรูปภาพสำหรับ OCR

เมื่อแพ็กเกจพร้อม เราต้อง **โหลดรูปภาพสำหรับ OCR** คลาส `OcrEngine` ต้องการพาธไปยังไฟล์ ดังนั้นตรวจสอบให้แน่ใจว่ารูปภาพมีอยู่และอ่านได้

```python
import aocr

# Step 2: Create an OCR engine instance
ocr_engine = aocr.OcrEngine()

# Step 2b: Point to your image file (adjust the path as needed)
image_path = r"YOUR_DIRECTORY/multilingual.png"
ocr_engine.load_image(image_path)
```

> **ทำไมเรื่องนี้สำคัญ:**  
> - `load_image` ทำการตรวจสอบอย่างรวดเร็ว (การมีไฟล์, ฟอร์แมตที่รองรับ)  
> - การใช้ raw string (`r"..."`) ป้องกันบั๊กจากอักขระ escape บน Windows paths  
> - หากรูปภาพใหญ่เกินไป aocr จะทำการ downscale อัตโนมัติเพื่อควบคุมการใช้หน่วยความจำ  

หากคุณได้รับ `FileNotFoundError` ให้ตรวจสอบพาธอีกครั้งและตรวจว่าไฟล์มีนามสกุลเป็น PNG, JPEG หรือ BMP

---

## ขั้นตอนที่ 3: ทำ OCR – แปลงรูปภาพเป็นข้อความ

เมื่อรูปภาพอยู่ในหน่วยความจำแล้ว การเรียกต่อไปจะ **จดจำอักขระพิเศษ** และคืนค่าเป็นสตริง Unicode

```python
# Step 3: Run the OCR engine
recognized_text = ocr_engine.recognize()
```

เบื้องหลัง aocr ทำงานด้วยเครือข่าย convolutional‑recurrent ที่เบาและได้รับการฝึกบนชุดข้อมูลหลายภาษา นั่นคือเหตุผลที่คุณจะเห็นอักขระจาก Cyrillic, Latin‑extended และ glyph ที่หายากบางตัวแสดงอย่างถูกต้อง

---

## ขั้นตอนที่ 4: แสดงข้อความที่ดึงมา

สุดท้าย พิมพ์ผลลัพธ์ออกมา ผลลัพธ์จะรวมทุกอักขระที่เอนจินสามารถถอดรหัสได้ รวมถึง diacritics ที่น่ารำคาญด้วย

```python
# Step 4: Show what we extracted
print("=== OCR RESULT ===")
print(recognized_text)
```

**ตัวอย่างผลลัพธ์** (ผลจริงของคุณจะขึ้นกับเนื้อหารูปภาพ):

```
=== OCR RESULT ===
Łąka žužuҖß – multilingual test string
```

*ตัวอย่างรูปภาพ:*  
![ดึงข้อความจากรูปภาพ ตัวอย่างผลลัพธ์](https://example.com/ocr-output.png "ดึงข้อความจากรูปภาพ ตัวอย่างผลลัพธ์")

> **หมายเหตุ:** คำสั่ง `print` ใช้การเข้ารหัส UTF‑8 เป็นค่าเริ่มต้นใน Python รุ่นใหม่ จึงควรเห็นอักขระพิเศษอย่างถูกต้องในเทอร์มินัลส่วนใหญ่ หากผลลัพธ์เป็นอักขระเสีย ให้ตั้งค่าคอนโซลเป็น UTF‑8 หรือเขียนสตริงลงไฟล์ด้วย `encoding='utf-8'`

---

## ขั้นตอนที่ 5: จัดการกรณีขอบและข้อผิดพลาดทั่วไป

### 5.1 รูปภาพความละเอียดต่ำ

หากรูปภาพต่ำกว่า 150 dpi ความแม่นยำของ OCR จะลดลงอย่างมาก วิธีแก้ง่ายคือ upscale ก่อนส่งให้ aocr:

```python
from PIL import Image

img = Image.open(image_path)
img = img.resize((img.width * 2, img.height * 2), Image.LANCZOS)
img.save("upscaled.png")
ocr_engine.load_image("upscaled.png")
```

### 5.2 การตรวจจับภาษาผิด

aocr ตรวจจับภาษาอัตโนมัติ แต่คุณสามารถบังคับสคริปต์เฉพาะเพื่อผลลัพธ์ที่ดีกว่า:

```python
ocr_engine.set_language("rus")   # forces Cyrillic detection
```

รหัสภาษาที่รองรับรวมถึง `eng`, `deu`, `fra`, `rus`, `spa` เป็นต้น

### 5.3 สัญญาณรบกวนและพื้นหลังที่ซับซ้อน

พื้นหลังที่มีนอยส์อาจทำให้โมเดลสับสน ก่อนประมวลผลด้วย OpenCV เพื่อทำ binarize:

```python
import cv2

raw = cv2.imread(image_path, cv2.IMREAD_GRAYSCALE)
_, thresh = cv2.threshold(raw, 127, 255, cv2.THRESH_BINARY | cv2.THRESH_OTSU)
cv2.imwrite("clean.png", thresh)
ocr_engine.load_image("clean.png")
```

---

## สคริปต์เต็ม – โซลูชันคลิกเดียว

ด้านล่างเป็น **ตัวอย่างที่สมบูรณ์และรันได้** ที่รวมทุกส่วนเข้าด้วยกัน บันทึกเป็น `ocr_demo.py` แล้วรันด้วย `python ocr_demo.py`

```python
# ocr_demo.py
# -------------------------------------------------
# Complete example: extract text from image using aocr
# -------------------------------------------------

import aocr
from pathlib import Path
import sys

def main(image_path: str):
    # Verify the file exists early – gives a nicer error message
    if not Path(image_path).is_file():
        sys.exit(f"❌ File not found: {image_path}")

    # 1️⃣ Create OCR engine
    ocr_engine = aocr.OcrEngine()

    # 2️⃣ Load the image (you can also call preprocess_image() here)
    ocr_engine.load_image(image_path)

    # Optional: force language if you know it (uncomment)
    # ocr_engine.set_language("eng")

    # 3️⃣ Run OCR – this is where we **convert image to text**
    recognized_text = ocr_engine.recognize()

    # 4️⃣ Output – includes special characters like Ł, Ž, Җ, ß
    print("\n=== OCR RESULT ===")
    print(recognized_text)

if __name__ == "__main__":
    # Example usage: python ocr_demo.py multilingual.png
    if len(sys.argv) != 2:
        sys.exit("Usage: python ocr_demo.py <path-to-image>")
    main(sys.argv[1])
```

รันตามนี้:

```bash
python ocr_demo.py YOUR_DIRECTORY/multilingual.png
```

คุณจะเห็นอักขระที่ดึงมาแสดงในคอนโซล ยืนยันว่าคุณได้ **ดึงข้อความจากรูปภาพ** และ **จดจำอักขระพิเศษ** อย่างสำเร็จ

---

## คำถามที่พบบ่อย

**Q: ทำงานกับ PDF ได้หรือไม่?**  
A: ไม่ได้โดยตรง ให้แปลงหน้าของ PDF เป็นรูปภาพก่อน (เช่น ใช้ `pdf2image`) แล้วจึงส่งแต่ละรูปไปยัง aocr

**Q: aocr เร็วกว่า Tesseract แค่ไหน?**  
A: สำหรับสแกน 300 dpi ปกติ aocr ประมวลผลหน้าในประมาณ ~0.3 s บนแล็ปท็อปสมัยใหม่—เร็วประมาณสองเท่าของ Tesseract ปกติที่ใช้ค่าตั้งต้น

**Q: สามารถประมวลผลหลายไฟล์ในโฟลเดอร์ได้หรือไม่?**  
A: ทำได้แน่นอน ใส่ฟังก์ชัน `main` ไว้ในลูปที่วน `Path(folder).glob("*.png")` แล้วเก็บผลลัพธ์ลง CSV

---

## สรุป

ตอนนี้คุณมีเวิร์กโฟลว์ครบวงจรเพื่อ **ดึงข้อความจากรูปภาพ** ด้วยไลบรารี aocr ของ Python ตั้งแต่การโหลดไฟล์จนถึงการพิมพ์ผล Unicode ทุกขั้นตอนอธิบายไว้เพื่อให้คุณปรับใช้กับโปรเจกต์ของตนเองได้ ไม่ว่าจะเป็นบริการสแกนใบเสร็จหรือคลังเอกสารหลายภาษา

ต่อไปลองสำรวจหัวข้อที่เกี่ยวข้องเหล่านี้:

- **แปลงรูปภาพเป็นข้อความ** สำหรับ PDF (ใช้ `pdf2image` + OCR)  
- **จดจำอักขระพิเศษ** ในโน้ตมือเขียน (ทดลอง `ocr_engine.set_dpi(600)`)  
- **โหลดรูปภาพสำหรับ OCR** ใน API เว็บ (Flask + aocr)  

ลองใช้งาน ปรับตั้งค่าภาษา แล้วดูข้อมูลของคุณกลายเป็น searchable ทันที มีคำถามหรือกรณีการใช้งานที่เจ๋ง? แสดงความคิดเห็นด้านล่าง—ขอให้สนุกกับการเขียนโค้ด!

## คุณควรเรียนรู้อะไรต่อไป?

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}