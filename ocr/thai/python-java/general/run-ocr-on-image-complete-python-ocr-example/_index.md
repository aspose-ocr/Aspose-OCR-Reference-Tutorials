---
category: general
date: 2026-03-18
description: ทำ OCR บนภาพอย่างรวดเร็วด้วย Python. เรียนรู้วิธีจดจำข้อความจาก PNG,
  โหลดภาพสำหรับ OCR, และดึงคำจากภาพในคู่มือขั้นตอนต่อขั้นตอน.
draft: false
keywords:
- run OCR on image
- recognize text from png
- python OCR example
- extract words from image
- load image for OCR
language: th
og_description: ทำ OCR บนภาพด้วย Python บทเรียนนี้แสดงวิธีจดจำข้อความจากไฟล์ PNG โหลดภาพสำหรับ
  OCR และดึงคำจากภาพพร้อมตัวอย่างโค้ดเต็ม.
og_title: ทำ OCR บนรูปภาพ – คู่มือ Python
tags:
- OCR
- Python
- Image Processing
title: เรียกใช้ OCR บนรูปภาพ – ตัวอย่าง OCR ด้วย Python อย่างครบถ้วน
url: /th/python-java/general/run-ocr-on-image-complete-python-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# รัน OCR บนรูปภาพ – ตัวอย่าง Python OCR แบบครบถ้วน

เคยต้องการ **run OCR on image** ไฟล์แต่ไม่แน่ใจว่าจะเริ่มจากตรงไหนหรือไม่? คุณไม่ได้อยู่คนเดียว; นักพัฒนาหลายคนเจออุปสรรคนี้เมื่อพยายามดึงข้อความจากเอกสารสแกนเป็นครั้งแรก ในบทเรียนนี้เราจะพาไปผ่าน **Python OCR example** ที่ให้คุณ **recognize text from PNG** ไฟล์, **load image for OCR**, และ **extract words from image** พร้อมคะแนนความมั่นใจ—ทั้งหมดในไม่กี่บรรทัดของโค้ด

เราจะครอบคลุมทุกอย่างที่คุณต้องการ: ไลบรารีที่จำเป็น, วิธีตั้งค่าเอนจิน, ทำไมแต่ละขั้นตอนถึงสำคัญ, และผลลัพธ์ที่ได้เป็นอย่างไร สุดท้ายคุณจะสามารถคัดลอกสคริปต์นี้ไปใส่ในโปรเจกต์ของคุณและเริ่มดึงข้อความจากรูปใดก็ได้ทันที ไม่มีเนื้อหาเกินความจำเป็น เพียงโซลูชันที่ทำงานได้จริง

## สิ่งที่คุณต้องการ

ก่อนที่เราจะลงลึก, ตรวจสอบให้แน่ใจว่าคุณมี:

- Python 3.8 หรือใหม่กว่า ติดตั้งแล้ว  
- แพคเกจ `ocrengine` (หรือไลบรารีใด ๆ ที่มีคลาส `OcrEngine`) คุณสามารถติดตั้งได้ด้วย `pip install ocrengine` – ปรับชื่อหากคุณใช้ไลบรารี OCR อื่นเช่น `pytesseract`.  
- ไฟล์รูปภาพ (PNG, JPG, ฯลฯ) ที่ต้องการประมวลผล – ในคู่มือนี้เราจะใช้ `invoice.png`.  

เท่านี้แหละ ไม่มี dependency ที่หนักหน่วง, ไม่มีบริการภายนอก, เพียงแค่ Python ธรรมดา

![run OCR on image example showing a scanned invoice](/images/run-ocr-on-image.png)

*Alt text: ตัวอย่างการรัน OCR บนรูปภาพ – ใบแจ้งหนี้ที่สแกนกำลังประมวลผล*

## ขั้นตอนที่ 1 – ติดตั้งและนำเข้า OCR Library

เริ่มแรกเราต้องนำ OCR engine เข้ามาในสภาพแวดล้อมและทำการ import หากคุณใช้แพคเกจ `ocrengine` สมมติ การ import จะเป็นดังนี้:

```python
# Install the package (run once in your terminal)
# pip install ocrengine

# Import the OCR engine class
from ocrengine import OcrEngine
```

**ทำไมขั้นตอนนี้สำคัญ:** การ import คลาสที่ถูกต้องทำให้คุณเข้าถึงเมธอดที่เราจะเรียกใช้ต่อไป เช่น `setImageFromFile` และ `recognize` หากข้ามขั้นตอนนี้ Python จะโยน `ModuleNotFoundError` และคุณจะติดอยู่ก่อนแม้จะโหลดรูปภาพได้เลย

## ขั้นตอนที่ 2 – สร้างอินสแตนซ์ของ OCR Engine

เมื่อไลบรารีพร้อมแล้ว เราต้องการอ็อบเจกต์เอนจินที่เก็บการตั้งค่าและสถานะของกระบวนการจดจำ

```python
# Step 2: Create an OCR engine instance
ocr_engine = OcrEngine()
```

*เคล็ดลับ:* บาง OCR engine ให้คุณปรับโมเดลภาษา หรือการตั้งค่า DPI ได้ในขั้นตอนนี้ สำหรับ **python OCR example** พื้นฐานค่าเริ่มต้นทำงานได้ดี, แต่หากคุณทำงานกับสแกนความละเอียดต่ำ ควรพิจารณาปรับค่าเหล่านี้ที่นี่

## ขั้นตอนที่ 3 – โหลดรูปภาพที่ต้องการประมวลผล

ขั้นตอนต่อไปคือ **load image for OCR** คุณเพียงแค่ชี้เอนจินไปที่พาธของไฟล์ PNG (หรือฟอร์แมตที่รองรับ) ที่ต้องการวิเคราะห์

```python
# Step 3: Load the image you want to process
ocr_engine.setImageFromFile("YOUR_DIRECTORY/invoice.png")
```

**อะไรที่เกิดขึ้นเบื้องหลัง?** เอนจินจะอ่านข้อมูลพิกเซล, แปลงเป็นรูปแบบที่อัลกอริทึมจดจำเข้าใจ, และเก็บไว้ภายใน หากพาธไฟล์ผิดคุณจะได้รับ `FileNotFoundError` ดังนั้นตรวจสอบให้แน่ใจว่ารูปภาพมีอยู่จริง

## ขั้นตอนที่ 4 – รันอัลกอริทึมจดจำ

เมื่อโหลดรูปภาพแล้ว เราจึง **run OCR on image** เพื่อสกัดเนื้อหาข้อความออกมา

```python
# Step 4: Run the recognition algorithm to obtain results
ocr_result = ocr_engine.recognize()
```

ในขั้นตอนนี้เอนจินจะสแกนบิตแมพ, ใช้การจับคู่รูปแบบ, และคืนอ็อบเจกต์ที่บรรจุคำ, บรรทัด, และเมตริกความมั่นใจทั้งหมด

## ขั้นตอนที่ 5 – วนลูปคำที่จดจำได้และแสดงความมั่นใจ

ส่วนที่เป็นประโยชน์ที่สุดของกระบวนการ OCR คือการดู **the confidence** ของแต่ละโทเคนที่สกัดออกมา มันบอกว่าเอนจินมั่นใจแค่ไหนกับแต่ละคำ ทำให้คุณกรองผลลัพธ์ที่ความมั่นใจต่ำได้หากต้องการ

```python
# Step 5: Iterate over each recognized word and display its text with confidence
for recognized_word in ocr_result.getWords():
    word_text = recognized_word.getText()
    confidence = recognized_word.getConfidence()   # 0‑100%
    print(f"Word: '{word_text}' – confidence: {confidence}%")
```

**ผลลัพธ์ที่คาดหวัง** (ตัวอย่าง):

```
Word: 'Invoice' – confidence: 98%
Word: 'Number' – confidence: 95%
Word: ':' – confidence: 92%
Word: '2023-07-15' – confidence: 97%
Word: 'Total' – confidence: 96%
Word: ':' – confidence: 93%
Word: '$' – confidence: 88%
Word: '1,250.00' – confidence: 94%
```

ตอนนี้คุณสามารถเห็นได้อย่างชัดเจนว่า **what words were extracted from the image** และความน่าเชื่อถือของการตรวจจับแต่ละรายการ นี่คือหัวใจของ **extract words from image** pipeline

## จัดการกับกรณีขอบทั่วไป

### ถ้ารูปภาพเป็น Grayscale จะทำอย่างไร?

บาง OCR engine ทำงานได้ดีกว่ากับรูปสี หากคุณสังเกตเห็นความมั่นใจต่ำทั่วทั้งภาพ ลองแปลง PNG เป็นเวอร์ชันขาว‑ดำคอนทราสต์สูงก่อนส่งให้เอนจิน Pillow สามารถช่วยได้:

```python
from PIL import Image, ImageOps

img = Image.open("YOUR_DIRECTORY/invoice.png")
bw = ImageOps.grayscale(img).point(lambda x: 0 if x < 128 else 255, '1')
bw.save("YOUR_DIRECTORY/invoice_bw.png")
ocr_engine.setImageFromFile("YOUR_DIRECTORY/invoice_bw.png")
```

### จัดการหลายภาษา

หากเอกสารของคุณมีทั้งภาษาอังกฤษและสเปน คุณอาจต้อง **recognize text from PNG** ด้วยโมเดลหลายภาษา ส่วนใหญ่เอนจินให้คุณตั้งค่ารายการภาษาในระหว่างการเริ่มต้น:

```python
ocr_engine = OcrEngine(languages=["eng", "spa"])
```

### กรองคำที่ความมั่นใจต่ำ

บางครั้งคุณต้องการเฉพาะคำที่ความมั่นใจสูงกว่า 90 % ตัวกรองอย่างรวดเร็วเป็นดังนี้:

```python
high_confidence_words = [
    w.getText()
    for w in ocr_result.getWords()
    if w.getConfidence() >= 90
]
print(high_confidence_words)
```

## สคริปต์เต็มพร้อมรัน

รวมทุกอย่างเข้าด้วยกัน นี่คือสคริปต์เดียวที่คุณสามารถคัดลอก‑วางและรันได้ทันที (เพียงเปลี่ยนพาธไปยัง PNG ของคุณ)

```python
# run_ocr_on_image.py
# -------------------------------------------------
# Complete Python OCR example: load image for OCR,
# run OCR on image, and extract words from image.
# -------------------------------------------------

# Install the library first:
# pip install ocrengine pillow   # pillow only needed for optional preprocessing

from ocrengine import OcrEngine

def main():
    # 1️⃣ Create the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load the target PNG (replace with your own file)
    image_path = "YOUR_DIRECTORY/invoice.png"
    ocr_engine.setImageFromFile(image_path)

    # 3️⃣ Run recognition
    ocr_result = ocr_engine.recognize()

    # 4️⃣ Print each word with its confidence
    print("\n--- OCR Results ---")
    for word in ocr_result.getWords():
        text = word.getText()
        conf = word.getConfidence()
        print(f"Word: '{text}' – confidence: {conf}%")

if __name__ == "__main__":
    main()
```

รันด้วยคำสั่ง:

```bash
python run_ocr_on_image.py
```

คุณควรเห็นรายการคำและเปอร์เซ็นต์ความมั่นใจพิมพ์ออกมาที่คอนโซล ตามที่แสดงไว้ก่อนหน้านี้

## คำถามที่พบบ่อย

**ทำงานกับไฟล์ JPG หรือ TIFF ได้หรือไม่?**  
ทำได้แน่นอน เมธอด `setImageFromFile` รองรับฟอร์แมตใดก็ได้ที่ไลบรารีพื้นฐานสามารถถอดรหัสได้ ดังนั้นคุณสามารถ **run OCR on image** ไฟล์ประเภท JPG, TIFF, BMP ฯลฯ

**สามารถประมวลผลหลายรูปในลูปได้หรือไม่?**  
ทำได้เลย เพียงใส่ขั้นตอนการโหลดและจดจำไว้ใน `for` ลูปที่วนผ่านรายการพาธไฟล์ อย่าลืมรี‑initialize เอนจินหากไลบรารีต้องการอินสแตนซ์ใหม่ต่อแต่ละรูป

**ถ้าต้องการข้อความเป็นสตริงเดียวแทนการแยกตามคำจะทำอย่างไร?**  
ผลลัพธ์ OCR ส่วนใหญ่มีเมธอด `getText()` ที่คืนเอกสารทั้งหมดเป็นสตริง ตัวอย่าง:

```python
full_text = ocr_result.getText()
print(full_text)
```

## ขั้นตอนต่อไปและหัวข้อที่เกี่ยวข้อง

ตอนนี้คุณรู้วิธี **run OCR on image** แล้ว ลองสำรวจต่อ:

- **Post‑processing**: ใช้ regular expressions ทำความสะอาดวันที่, จำนวนเงิน, หรือรหัสที่สกัดจากใบแจ้งหนี้  
- **Batch processing**: ผสานสคริปต์กับ `os.listdir()` เพื่อจัดการโฟลเดอร์เต็มของเอกสารสแกน  
- **Alternative libraries**: `pytesseract` เป็นตัวเลือกโอเพนซอร์สที่นิยม; กระบวนการทำงานคล้ายกัน—แค่เปลี่ยนการเรียกใช้เอนจิน  
- **Exporting results**: เขียนคำที่สกัดและคะแนนความมั่นใจลง CSV เพื่อการวิเคราะห์ต่อไป  

แต่ละส่วนขยายเหล่านี้ต่อเนื่องจากพื้นฐานที่เราตั้งไว้ ทำให้คุณแปลงข้อมูล OCR ดิบให้เป็นข้อมูลที่นำไปใช้ได้จริง

---

### TL;DR

เราได้แสดง **python OCR example** สั้น ๆ ที่สาธิตวิธี **load image for OCR**, **run OCR on image**, และ **extract words from image** พร้อมรายงานความมั่นใจ สคริปต์เต็มพร้อมรันแล้ว และคุณมีความรู้เพียงพอที่จะปรับใช้กับโปรเจกต์ใด ๆ ที่ต้อง **recognize text from PNG** (หรือฟอร์แมตอื่น) ลองใช้งาน ปรับค่า threshold ของความมั่นใจ แล้วดูแอปของคุณกลายเป็น “text‑aware” ในไม่กี่นาที ขอให้สนุกกับการเขียนโค้ด!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}