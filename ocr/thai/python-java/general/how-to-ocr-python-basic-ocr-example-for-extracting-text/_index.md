---
category: general
date: 2026-04-26
description: 'วิธีใช้ OCR กับ Python: เรียนรู้การดึงข้อความจากภาพและอ่านไฟล์ TIFF
  ด้วย Python โดยใช้ตัวอย่าง OCR พื้นฐาน พร้อมโค้ดที่รวดเร็วและสามารถรันได้รวมไว้ด้วย.'
draft: false
keywords:
- how to ocr python
- extract text from image
- read tiff file python
- basic ocr example
- convert scanned image text
language: th
og_description: 'วิธีทำ OCR ด้วย Python: คู่มือขั้นตอนต่อขั้นตอนที่แสดงวิธีดึงข้อความจากภาพ,
  อ่านไฟล์ TIFF ด้วย Python, และแปลงข้อความจากภาพสแกนด้วยสคริปต์ง่าย ๆ ที่สามารถรันได้'
og_title: วิธีทำ OCR ด้วย Python – ตัวอย่าง OCR พื้นฐานสำหรับการดึงข้อความ
tags:
- OCR
- Python
- Image Processing
title: วิธีทำ OCR ด้วย Python – ตัวอย่าง OCR พื้นฐานสำหรับการดึงข้อความ
url: /th/python-java/general/how-to-ocr-python-basic-ocr-example-for-extracting-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีทำ OCR ด้วย Python – ตัวอย่าง OCR พื้นฐานสำหรับการสกัดข้อความ

เคยสงสัย **how to ocr python** เมื่อคุณมีไฟล์ TIFF สแกนอยู่บนโต๊ะของคุณไหม? คุณไม่ได้เป็นคนเดียวที่มองไฟล์รูปภาพหลายไฟล์แล้วถามว่า “จะดึงคำออกจากไฟล์นี้ได้อย่างไร?” ข่าวดีคือการเปลี่ยนรูปภาพให้เป็นข้อความธรรมดานั้นทำได้ง่ายมากเมื่อมีไลบรารีที่เหมาะสมและขั้นตอนที่ชัดเจนไม่กี่ขั้นตอน

ในบทแนะนำนี้เราจะเดินผ่าน **basic OCR example** ที่อ่านไฟล์ TIFF, สกัดข้อความ, และพิมพ์ผลลัพธ์ลงคอนโซล. เมื่อเสร็จคุณจะรู้วิธี **extract text from image** จากไฟล์ภาพ, วิธีจัดการกับความแปลกของฟอร์แมต TIFF, และสิ่งที่ต้องปรับแต่งหากต้อง **convert scanned image text** ให้เป็นประโยชน์มากขึ้น ไม่มีเวทมนตร์ซ่อนอยู่—แค่ Python ธรรมดาที่คุณสามารถคัดลอก‑วางและรันได้ทันที

## สิ่งที่คุณต้องมี

ก่อนที่เราจะลงลึก, ตรวจสอบให้แน่ใจว่าคุณมี:

- Python 3.9+ ติดตั้งแล้ว (เวอร์ชันล่าสุดที่เสถียรที่สุดเป็นตัวเลือกที่ดีที่สุด)
- ไลบรารี OCR ที่ติดตั้งผ่าน pip. สำหรับคู่มือนี้เราจะใช้แพ็กเกจสมมติ `aocr` ที่เลียนแบบเครื่องมือยอดนิยมอย่าง Tesseract; คุณสามารถเปลี่ยนเป็น `pytesseract` หรือ `easyocr` ได้ในภายหลัง
- ภาพ TIFF ที่ต้องการประมวลผล – ตั้งชื่อไฟล์เป็น `input.tiff` แล้ววางไว้ในโฟลเดอร์ที่คุณจะอ้างอิงในโค้ด
- ความคุ้นเคยพื้นฐานกับบรรทัดคำสั่ง (เพียงเพื่อทำการติดตั้งแพ็กเกจ)

เท่านี้เอง ไม่มีการพึ่งพาไลบรารีหนัก ๆ, ไม่มี Docker container, แค่ไม่กี่บรรทัดของโค้ด

## Step 1 – Install and Import Dependencies (how to ocr python)

แรกเริ่มให้ติดตั้งแพ็กเกจ OCR. เปิดเทอร์มินัลและรัน:

```bash
pip install aocr
```

หากคุณต้องการใช้ไลบรารีจริง ๆ ให้เปลี่ยน `aocr` เป็น `pytesseract` แล้วติดตั้งเอนจิน Tesseract แยกต่างหาก

ต่อไปให้ import สิ่งที่ต้องการ. คลาส `Path` จาก `pathlib` ให้วิธีที่สะอาดในการทำงานกับเส้นทางไฟล์ข้ามระบบปฏิบัติการ

```python
# Step 1: Import the Path class for handling file paths
from pathlib import Path

# Import the OCR engine and image loader from the chosen library
from aocr import OcrEngine, Image
```

*ทำไมต้องใช้ `Path`?* เพราะมันแยกความแตกต่างของสแลช (`/` vs `\`) และให้คุณรวมไดเรกทอรีได้โดยไม่ต้องกังวลเกี่ยวกับ OS ที่อยู่เบื้องหลัง รายละเอียดเล็ก ๆ นี้มักช่วยลดปัญหาเมื่อคุณย้ายสคริปต์ไปยังเซิร์ฟเวอร์ CI

## Step 2 – Create the OCR Engine Instance (basic ocr example)

ต่อไปให้สร้างอินสแตนซ์ของ OCR engine. คิดว่า `OcrEngine` คือสมองที่จะอ่านรูปภาพและส่งออกอักขระ

```python
# Step 2: Create an instance of the OCR engine
ocr_engine = OcrEngine()
```

ไลบรารี OCR ส่วนใหญ่ให้คุณปรับภาษา, DPI, หรือเกณฑ์ความเชื่อมั่นได้ที่นี่ สำหรับ **basic OCR example** นี้เราจะใช้ค่าเริ่มต้น, แต่คุณสามารถสำรวจ `ocr_engine.config` ต่อไปได้หากต้องจัดการเอกสารหลายภาษา

## Step 3 – Load Your TIFF Image (read tiff file python)

นี่คือส่วนที่ **read tiff file python** เข้ามา. ไฟล์ TIFF สามารถมีหลายหน้า, แต่ `Image.load` จะดึงหน้าที่แรกโดยค่าเริ่มต้น—เหมาะกับการสแกนหน้าเดียว

```python
# Step 3: Load the image you want to recognize
# Using a generic placeholder path makes it easy to adapt the example
ocr_engine.image = Image.load(Path("YOUR_DIRECTORY/input.tiff"))
```

แทนที่ `"YOUR_DIRECTORY"` ด้วยโฟลเดอร์จริงที่เก็บ `input.tiff`. หากคุณไม่แน่ใจว่าสคริปต์ทำงานจากที่ไหน, `Path.cwd()` จะพิมพ์ไดเรกทอรีทำงานปัจจุบัน—มีประโยชน์สำหรับดีบักปัญหาเส้นทาง

## Step 4 – Run the OCR Process (extract text from image)

ตอนนี้จุดมุ่งหมายของเราจะเริ่มทำงาน. การเรียก `process()` จะส่งภาพผ่าน pipeline ของ OCR และคืนอ็อบเจ็กต์ผลลัพธ์

```python
# Step 4: Run the OCR process to extract text from the image
ocr_result = ocr_engine.process()
```

เบื้องหลังเครื่องยนต์อาจทำการแปลงภาพเป็นระดับสีเทา, ปรับค่า threshold, แล้วส่งเข้าเครือข่ายประสาทเทียม คุณไม่จำเป็นต้องจัดการขั้นตอนเหล่านี้; ไลบรารีทำหน้าที่แอบซ่อนไว้ให้คุณ

## Step 5 – Print the Recognized Text (convert scanned image text)

สุดท้ายให้พิมพ์ข้อความที่ได้รับ. ในโปรเจกต์จริงคุณอาจเขียนลงไฟล์หรือฐานข้อมูล, แต่การพิมพ์ทำให้ตัวอย่างดูเรียบง่าย

```python
# Step 5: Print the recognized text to the console
print(ocr_result.text)
```

เมื่อรันสคริปต์, คุณควรเห็นผลลัพธ์ประมาณนี้:

```
Hello, world!
This is a sample scanned document.
```

หากผลลัพธ์ดูเป็นอักขระผสม, ตรวจสอบให้แน่ใจว่าภาพต้นฉบับชัดเจนและภาษาของ OCR ตรงกับข้อความ

## Full Working Script

รวมทุกอย่างเข้าด้วยกัน, นี่คือโปรแกรมที่พร้อมรันเต็มรูปแบบ:

```python
# Full script: how to ocr python – basic OCR example

from pathlib import Path
from aocr import OcrEngine, Image  # Replace with your OCR library if needed

def main():
    # Initialize the OCR engine
    ocr_engine = OcrEngine()

    # Load the TIFF image (adjust the path as needed)
    image_path = Path("YOUR_DIRECTORY/input.tiff")
    if not image_path.is_file():
        raise FileNotFoundError(f"Could not find {image_path}. Make sure the file exists.")
    
    ocr_engine.image = Image.load(image_path)

    # Perform OCR
    ocr_result = ocr_engine.process()

    # Output the extracted text
    print("=== OCR Output ===")
    print(ocr_result.text)

if __name__ == "__main__":
    main()
```

### Expected Output

```
=== OCR Output ===
Your scanned document’s text appears here, line by line.
```

หากคุณต้อง **convert scanned image text** ให้เป็น PDF ที่ค้นหาได้, คุณสามารถส่ง `ocr_result.text` ไปยังตัวสร้าง PDF อย่าง `reportlab`—แต่เรื่องนั้นเป็นบทแนะนำแยกอีกเรื่องหนึ่ง

## Common Pitfalls & Pro Tips

- **Low‑resolution scans**: OCR ทำงานได้ยากเมื่อความละเอียดต่ำกว่า 150 DPI. หาก TIFF ของคุณเบลอ, ให้อัป‑ซัมป์ก่อนด้วย Pillow (`Image.open(...).resize(...)`)
- **Multiple pages**: สำหรับ TIFF หลายหน้า, ให้วนลูป `Image.load_multi_page()` (ถ้าไลบรารีของคุณรองรับ) แล้วต่อผลลัพธ์เข้าด้วยกัน
- **Language support**: เครื่องส่วนใหญ่ตั้งค่าเริ่มต้นเป็นอังกฤษ. ตั้งค่า `ocr_engine.language = "spa"` เพื่อใช้ภาษาสเปนเป็นตัวอย่าง
- **Whitespace handling**: OCR มักเพิ่มบรรทัดว่างโดยไม่ตั้งใจ. ใช้ `str.splitlines()` หรือ regex เพื่อทำความสะอาดผลลัพธ์
- **Performance**: หากต้องประมวลผลจำนวนมาก, ให้ใช้อินสแตนซ์ `OcrEngine` ตัวเดียวซ้ำ ๆ แทนการสร้างใหม่ทุกไฟล์

## Extending the Example

ตอนนี้คุณได้เชี่ยวชาญ **how to ocr python** สำหรับภาพเดียวแล้ว, ลองทำขั้นตอนต่อไปนี้:

1. **Batch processing** – วนลูปโฟลเดอร์ของ TIFFs แล้วเขียนผลลัพธ์แต่ละไฟล์ลง `.txt`
2. **Integration with Pandas** – เก็บข้อความที่สกัดไว้พร้อมเมตาดาต้าเพื่อการวิเคราะห์อย่างรวดเร็ว
3. **Hybrid approach** – ผสาน OCR กับไลบรารี NLP อย่าง `spaCy` เพื่อสกัดเอนทิตี (ชื่อ, วันที่, จำนวนเงิน) จากใบแจ้งหนี้ที่สแกน
4. **Alternative file formats** – แทนที่ `Image.load` ด้วย `Image.from_bytes` เพื่อจัดการภาพที่มาจาก API หรือฐานข้อมูล

ทั้งหมดนี้ต่อยอดจากแนวคิดหลักของ **extract text from image** และ **convert scanned image text** ให้เป็นข้อมูลที่เครื่องคอมพิวเตอร์เข้าใจได้

## Conclusion

เราได้เดินผ่าน **basic OCR example** อย่างชัดเจนจากต้นจนจบ ที่แสดง **how to ocr python**, วิธี **read tiff file python**, และวิธี **extract text from image** ด้วยเพียงไม่กี่บรรทัดสคริปต์. สคริปต์นี้เป็นอิสระ, มีการจัดการข้อผิดพลาด, และพิมพ์ผลลัพธ์โดยตรง, ทำให้เป็นพื้นฐานที่มั่นคงสำหรับโครงการใด ๆ ที่ต้องแปลงเอกสารสแกนเป็นข้อความที่แก้ไขได้

ลองทดลองเปลี่ยน backend OCR, ปรับการเตรียมภาพ, หรือเชื่อมต่อผลลัพธ์กับ workflow ถัดไป. ท้องฟ้าเป็นขอบเขตเมื่อคุณสามารถ **convert scanned image text** ให้เป็นข้อมูลที่ค้นหาได้อย่างมั่นใจ

มีคำถามเกี่ยวกับกรณีขอบ, แพ็คภาษาต่าง ๆ, หรือการปรับประสิทธิภาพ? แสดงความคิดเห็นด้านล่าง, แล้วขอให้เขียนโค้ดอย่างสนุกสนาน!

![how to ocr python example](/images/ocr-python-example.png "Screenshot of how to ocr python script output")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}