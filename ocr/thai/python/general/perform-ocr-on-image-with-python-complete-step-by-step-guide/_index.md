---
category: general
date: 2026-07-05
description: ทำ OCR บนรูปภาพด้วย Python เรียนรู้วิธีแปลงรูปภาพเป็นข้อความด้วย Python
  โหลดรูปภาพสำหรับ OCR และสกัดข้อความซีริลลิกจากรูปภาพในไม่กี่นาที
draft: false
keywords:
- perform OCR on image
- convert image to text python
- load image for OCR
- extract Cyrillic text from image
- recognize Cyrillic text
language: th
og_description: ทำ OCR บนภาพด้วย Python. คู่มือนี้จะแสดงวิธีแปลงภาพเป็นข้อความด้วย
  Python, โหลดภาพสำหรับ OCR และดึงข้อความซีริลลิกจากภาพอย่างรวดเร็ว.
og_title: ทำ OCR บนภาพด้วย Python – คู่มือเต็ม
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Perform OCR on image using Python. Learn how to convert image to text
    python, load image for OCR and extract Cyrillic text from image in minutes.
  headline: Perform OCR on Image with Python – Complete Step‑by‑Step Guide
  type: TechArticle
tags:
- OCR
- Python
- Cyrillic
title: ทำ OCR บนภาพด้วย Python – คู่มือขั้นตอนเต็มแบบครบถ้วน
url: /th/python/general/perform-ocr-on-image-with-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ทำ OCR บนรูปภาพด้วย Python – คู่มือขั้นตอนเต็ม

เคยสงสัยไหมว่าจะแปลง **perform OCR on image** ไฟล์อย่างไรโดยไม่ต้องส่งให้บริการของบุคคลที่สาม? คุณไม่ได้เป็นคนเดียว ในหลายโครงการ—สแกนพาสปอร์ต, ดิจิไทซ์ใบเสร็จ, หรือเครื่องมือจัดเก็บข้อมูล—การดึงข้อความดิบจากภาพเป็นอุปสรรคแรก  

ในบทเรียนนี้เราจะเดินผ่านตัวอย่างเชิงปฏิบัติที่ **converts image to text python** style, แสดงวิธี **load image for OCR**, และสุดท้าย **extract Cyrillic text from image** ด้วยไลบรารีโอเพ่นซอร์ส `aocr` เมื่อจบคุณจะสามารถ **recognize Cyrillic text** ในภาพใด ๆ ที่คุณใส่เข้าไปได้

> **What you’ll walk away with:** สคริปต์พร้อมใช้งาน, คำอธิบายที่ชัดเจนของแต่ละขั้นตอน, และเคล็ดลับในการจัดการกับปัญหาทั่วไป (เช่น การสแกนที่เบลอหรือฟอนต์ที่ไม่คาดคิด). ไม่มี API ภายนอก, เพียงแค่ Python แท้

---

## ข้อกำหนดเบื้องต้น

- ติดตั้ง Python 3.8 หรือใหม่กว่า
- มีเทอร์มินัลหรือพรอมต์คำสั่งที่คุณคุ้นเคย
- ติดตั้งแพ็กเกจ `aocr` (ติดตั้งได้ด้วย `pip install aocr`)
- มีไฟล์รูปภาพที่มีอักขระ Cyrillic (เช่น พาสปอร์ตรัสเซียที่สแกน)

หากสิ่งใดเหล่านี้ฟังดูแปลกใหม่ อย่าตื่นตระหนก—แต่ละหัวข้อจะอธิบายสั้น ๆ ขณะดำเนินการ

---

## ขั้นตอนที่ 1: Perform OCR on Image – ตั้งค่าสภาพแวดล้อม

สิ่งแรกที่เราต้องการคือสภาพแวดล้อม Python ที่สะอาดซึ่งไลบรารี OCR จะอาศัยอยู่ การใช้ virtual environment ช่วยแยกการพึ่งพาและป้องกันความขัดแย้งของเวอร์ชัน

```bash
# Create a virtual environment (optional but recommended)
python -m venv ocr-env
# Activate it (Windows)
ocr-env\Scripts\activate
# Activate it (macOS/Linux)
source ocr-env/bin/activate

# Install the aocr library
pip install aocr
```

**ทำไม?**  
สภาพแวดล้อมเฉพาะช่วยให้แน่ใจว่าแพ็กเกจ `aocr` และไบนารีเนทีฟของมันไม่รบกวนโครงการอื่น ๆ อีกทั้งทำให้การทำซ้ำง่าย—ใครก็สามารถโคลนรีโปของคุณและรันคำสั่ง `pip install -r requirements.txt` เดียวกันได้

> **Pro tip:** Freeze your dependencies with `pip freeze > requirements.txt` so you always know exactly which versions were used.

---

## ขั้นตอนที่ 2: Load Image for OCR – นำเข้าและเตรียมไฟล์

ตอนนี้ไลบรารีพร้อมแล้ว เราต้อง **load image for OCR** วิธี `aocr.Image.from_file` รองรับรูปแบบที่พบบ่อย (PNG, JPEG, TIFF) นี่คือตัวอย่างการใช้งาน:

```python
import aocr

# Path to the Cyrillic image – replace with your actual file location
image_path = "YOUR_DIRECTORY/rus_passport.png"

# Load the image into an aocr.Image object
cyrillic_image = aocr.Image.from_file(image_path)
```

**เกิดอะไรขึ้นที่นี่?**  
`aocr.Image.from_file` อ่านข้อมูลไบนารี, ถอดรหัส, และเก็บไว้ในอ็อบเจ็กต์ที่เครื่อง OCR เข้าใจได้ หากไม่พบไฟล์ Python จะโยน `FileNotFoundError` ซึ่งคุณสามารถจับไว้เพื่อจัดการข้อผิดพลาดอย่างสุภาพได้

> **Edge case:** บางสแกนเนอร์ส่งออก TIFF แบบหลายหน้า ในกรณีนั้นคุณต้องแยกหน้าออกก่อน—`aocr` มี `Image.from_tiff_pages()` ให้ใช้

---

## ขั้นตอนที่ 3: Configure the OCR Engine – บังคับการรับรู้ Cyrillic

โดยค่าเริ่มต้น OCR หลายตัวพยายามคาดเดาภาษา ซึ่งอาจทำให้ผลลัพธ์เป็นอักขระผสมสำหรับสคริปต์ที่ไม่ใช่ Latin เพื่อ **recognize Cyrillic text** อย่างแม่นยำ เราตั้งค่าภาษาเป็น “cyrillic” อย่างชัดเจน

```python
# Create an OCR engine instance
ocr_engine = aocr.OcrEngine()

# Force the engine to use the Cyrillic recognizer
ocr_engine.language = "cyrillic"
```

**ทำไมต้องบังคับภาษา?**  
อักขระ Cyrillic มีลักษณะคล้ายกับอักษร Latin (เช่น “A” กับ “А”) การบอกเครื่องให้คาดหวัง Cyrillic ลดการจดจำผิดอย่างมาก โดยเฉพาะกับสแกนความละเอียดต่ำ

---

## ขั้นตอนที่ 4: Perform OCR on Image – เรียกใช้การจดจำ

เมื่อโหลดภาพและตั้งค่าเครื่องแล้ว เราจึง **perform OCR on image** วิธี `recognize` จะคืนค่าอ็อบเจ็กต์ `OcrResult` ที่มีข้อความที่สกัดและคะแนนความเชื่อมั่น

```python
# Run the OCR process
ocr_result = ocr_engine.recognize(cyrillic_image)

# Print the raw text
print("Cyrillic text:")
print(ocr_result.text)
```

**`ocr_result` ให้ข้อมูลอะไรบ้าง?**  
- `text`: สตริงธรรมดาของอักขระที่จดจำได้  
- `confidence`: ค่า float (0‑1) แสดงระดับความมั่นใจโดยรวม  
- `lines`: รายการของอ็อบเจ็กต์บรรทัด หากต้องการควบคุมระดับละเอียด

> **Common question:** *What if the text is upside‑down?*  
> `aocr` สามารถหมุนภาพอัตโนมัติ; เพียงตั้งค่า `ocr_engine.auto_rotate = True` ก่อนเรียก `recognize`

---

## ขั้นตอนที่ 5: Convert Image to Text Python – การประมวลผลผลลัพธ์

สตริงดิบอาจมีช่องว่างหรืออักขระขึ้นบรรทัดที่ไม่ต้องการ เพื่อ **convert image to text python** style เราจะทำความสะอาดด้วยขั้นตอนง่าย ๆ ดังนี้:

```python
import re

# Remove extra whitespace and normalize line breaks
clean_text = re.sub(r'\s+', ' ', ocr_result.text).strip()

print("\nCleaned Cyrillic text:")
print(clean_text)
```

**ทำไมต้องทำ?**  
ผลลัพธ์ที่ทำความสะอาดง่ายต่อการส่งต่อไปยัง pipeline ถัดไป—ไม่ว่าจะเก็บในฐานข้อมูล, ส่งให้ API แปลภาษา, หรือทำการค้นหา regex สำหรับหมายเลขพาสปอร์ต

---

## ขั้นตอนที่ 6: Extract Cyrillic Text from Image – รวมทุกอย่างเข้าด้วยกัน

เราจะรวมทุกอย่างเป็นฟังก์ชันเดียวที่ใช้ซ้ำได้ ทำให้ **extract Cyrillic text from image** กลายเป็นบรรทัดเดียวในโปรเจกต์ของคุณ

```python
def extract_cyrillic_text(image_path: str) -> str:
    """
    Loads an image, forces Cyrillic OCR, and returns cleaned text.
    """
    # Load image
    img = aocr.Image.from_file(image_path)

    # Configure OCR engine for Cyrillic
    engine = aocr.OcrEngine()
    engine.language = "cyrillic"

    # Recognize text
    result = engine.recognize(img)

    # Clean up the output
    cleaned = re.sub(r'\s+', ' ', result.text).strip()
    return cleaned

# Example usage
if __name__ == "__main__":
    path = "YOUR_DIRECTORY/rus_passport.png"
    print("Extracted text:", extract_cyrillic_text(path))
```

**ผลลัพธ์ที่คุณควรเห็น (ตัวอย่าง):**

```
Extracted text: ПАСПОРТ РФ № 1234567890 ИМЯ ФАМИЛИЯ ДАТА РОЖДЕНИЯ 01.01.1990
```

หากภาพคมชัดและฟอนต์ตรงกับโมเดล OCR คุณจะได้การถอดข้อความที่เกือบสมบูรณ์แบบ

---

## แก้ไขปัญหา & เคล็ดลับ

| Issue | Likely Cause | Fix |
|-------|--------------|-----|
| Garbled characters | Wrong language setting | Ensure `ocr_engine.language = "cyrillic"` |
| Empty output | Image too dark or low‑resolution | Preprocess with `opencv` to increase contrast |
| Wrong orientation | Image rotated 90° | Set `ocr_engine.auto_rotate = True` |
| Slow performance | Large image ( >5 MP ) | Resize with `aocr.Image.resize(width=1024)` before recognition |

![ตัวอย่างการทำ OCR บนรูปภาพ](ocr_example.png "ตัวอย่างการทำ OCR บนรูปภาพ")

*ข้อความแทน: “ตัวอย่างการทำ OCR บนรูปภาพแสดงโค้ด Python ที่ดึงข้อความ Cyrillic จากการสแกนพาสปอร์ต.”*

---

## สรุป

เราเพิ่ง **performed OCR on image** ไฟล์ด้วย Python แท้, เรียนรู้วิธี **load image for OCR**, บังคับเครื่องให้ **recognize Cyrillic text**, และสุดท้าย **extracted Cyrillic text from image** ด้วยฟังก์ชันช่วยเหลือที่เรียบง่าย ทั้งกระบวนการ—from การติดตั้ง `aocr` ถึงการทำความสะอาดผลลัพธ์—ใช้เพียงไม่กี่สิบบรรทัดโค้ดและสามารถนำไปใส่ในโปรเจกต์ใดก็ได้ที่ต้องการ **convert image to text python** style

---

## สิ่งต่อไปที่ควรทำ

- **Batch processing:** วนลูปผ่านโฟลเดอร์สแกนและเก็บผลลัพธ์ใน SQLite  
- **Language detection:** ผสาน `langdetect` กับ `aocr` เพื่อสลับอัตโนมัติระหว่าง Cyrillic และ Latin  
- **Advanced preprocessing:** ใช้ `opencv` เพื่อแก้ไขการเอียง, ลดสัญญาณรบกวน, หรือทำไบนาริซภาพเพื่อความแม่นยำสูงขึ้น  
- **Integrate with FastAPI:** เปิดเผยฟังก์ชัน `extract_cyrillic_text` เป็น REST endpoint สำหรับเว็บแอป

ลองเปลี่ยนภาษาเป็น “latin” สำหรับพาสปอร์ตภาษาอังกฤษ หรือทดลองใช้ backend OCR อื่น ๆ ทั้งหมด แนวคิดยังคงเหมือนเดิมและโค้ดยืดหยุ่นพอที่จะปรับใช้

Happy coding, and may your images always be legible!

## คุณควรเรียนรู้อะไรต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอนเพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานแบบอื่นในโปรเจกต์ของคุณ

- [สกัดข้อความจากภาพด้วย Aspose OCR – คู่มือขั้นตอนเต็ม](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [แปลงภาพเป็นข้อความ – ทำ OCR บนภาพจาก URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [สกัดข้อความจากภาพด้วย C# พร้อมการเลือกภาษาโดยใช้ Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}