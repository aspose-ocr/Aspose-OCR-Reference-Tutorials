---
category: general
date: 2026-03-26
description: เรียนรู้วิธีใช้ OCR กับภาพ PNG ภาษาอาหรับและดึงข้อความภาษาอาหรับออกอย่างรวดเร็ว
  คู่มือนี้แสดงการแปลงภาพเป็นข้อความด้วยโค้ด Python ทีละขั้นตอน
draft: false
keywords:
- how to run ocr
- extract arabic text
- recognize arabic text
- convert image to text
- extract text from png
language: th
og_description: วิธีรัน OCR บนภาพ PNG ภาษาอารบิก? ทำตามคู่มือฉบับเต็มนี้เพื่อดึงข้อความภาษาอารบิก,
  จำแนกข้อความภาษาอารบิก, และแปลงภาพเป็นข้อความโดยใช้ Python.
og_title: วิธีใช้ OCR กับไฟล์ PNG ภาษาอาหรับ – ดึงข้อความจากภาพ
tags:
- OCR
- Python
- Arabic
title: วิธีทำ OCR บนไฟล์ PNG ภาษาอารบิก – แยกข้อความจากรูปภาพ
url: /th/python-java/general/how-to-run-ocr-on-arabic-png-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีการรัน OCR บน PNG ภาษาอารบิก – แยกข้อความจากภาพ

เคยสงสัย **วิธีการรัน OCR** บนภาพที่มีอักษรอารบิกหรือไม่? บางทีคุณอาจมีใบเสร็จสแกน, ต้นฉบับประวัติศาสตร์, หรือเพียงแค่ภาพหน้าจอของโพสต์ในโซเชียลมีเดียและคุณต้องการข้อความในรูปแบบที่สามารถค้นหาได้ คุณไม่ได้เป็นคนเดียว—นักพัฒนาทั่วโลกต่างเจอปัญหานี้เมื่อต้องจัดการกับภาษาที่เขียนจากขวาไปซ้าย

ในบทแนะนำนี้เราจะพาคุณผ่านตัวอย่างที่สมบูรณ์และสามารถรันได้ ซึ่งแสดง **วิธีการรัน OCR** บนไฟล์ PNG, แยกข้อความอารบิก, และพิมพ์ผลลัพธ์ไปยังคอนโซล ไม่มีลิงก์ “ดูเอกสาร” ที่คลุมเครือ; มีเพียงโค้ดที่คุณสามารถคัดลอก‑วางได้ พร้อมคำอธิบายว่าทำไมแต่ละบรรทัดจึงสำคัญ เมื่อจบคุณจะสามารถ **แปลงภาพเป็นข้อความ** ได้อย่างเชื่อถือได้ แม้แหล่งที่มาจะเป็น PNG ภาษาอารบิกที่ท้าทาย

> **สิ่งที่คุณจะได้เรียนรู้**
> - ตั้งค่า Python OCR engine สำหรับภาษาอารบิก  
> - โหลดภาพ PNG และจัดการกับปัญหาทั่วไป  
> - จดจำข้อความอารบิกและตรวจสอบผลลัพธ์  
> - เคล็ดลับสำหรับ **การแยกข้อความอารบิก** จากคุณภาพภาพที่ต่างกัน  

ก่อนที่เราจะเริ่มลงลึก, ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง Python 3.8+ แล้วและมีเวอร์ชันล่าสุดของไลบรารี `ocr` (ที่ใช้ในตัวอย่าง) หากคุณใช้ virtual environment, ให้เปิดใช้งานตอนนี้—เพื่อให้การจัดการ dependencies เป็นระเบียบ

## ข้อกำหนดเบื้องต้น

- Python 3.8 หรือใหม่กว่า  
- `ocr` package (`pip install ocr‑engine` – แทนที่ด้วยชื่อแพคเกจจริง)  
- ภาพ PNG ภาษาอารบิก (`arabic_doc.png`) ที่วางไว้ในตำแหน่งที่คุณสามารถอ้างอิงได้  
- ความคุ้นเคยพื้นฐานกับฟังก์ชันและคลาสของ Python  

เท่านี้เอง ไม่ต้องใช้เฟรมเวิร์กหนัก, ไม่ต้อง Docker containers—แค่ Python ธรรมดา

## ขั้นตอนที่ 1: ติดตั้งและนำเข้าไลบรารี OCR

สิ่งแรกที่ต้องทำคือ เราต้องการ OCR engine เอง ไลบรารีที่เราใช้เปิดเผยคลาส `OcrEngine` พร้อม API ที่เข้าใจง่าย

```python
# Install the library (run once in your terminal)
# pip install ocr-engine   # <-- replace with the correct package name

# Import the necessary classes
import ocr
from ocr import Imaging
```

*ทำไมต้องนำเข้า `Imaging` แยกต่างหาก?* โมดูลย่อย `Imaging` ให้เมธอด `Image.load` ที่สะดวกซึ่งรองรับ PNG, JPEG, และ TIFF โดยอัตโนมัติ การข้ามขั้นตอนนี้จะทำให้คุณต้องจัดการกับไบต์ดิบด้วยตนเอง ซึ่งไม่จำเป็นสำหรับกรณีใช้งานส่วนใหญ่

## ขั้นตอนที่ 2: สร้างอินสแตนซ์ของ OCR Engine

ตอนนี้เราจะสร้างอินสแตนซ์ของ engine คิดว่าอ็อบเจ็กต์นี้เป็น “สมอง” ที่จะประมวลผลภาพ

```python
# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()
```

> **เคล็ดลับมืออาชีพ:** หากคุณวางแผนจะประมวลผลหลายภาพต่อเนื่อง, ให้ใช้อินสแตนซ์ `ocr_engine` เดียวกันซ้ำ มันจะเก็บแคชโมเดลภาษา ซึ่งทำให้การจดจำต่อไปเร็วขึ้น

## ขั้นตอนที่ 3: ตั้งค่าภาษาเป็นอารบิก

อารบิกไม่ใช่ภาษาละติน; มันมีชุดอักขระของตนเอง, ทิศทางจากขวาไปซ้าย, และการจัดรูปแบบตามบริบท นั่นคือเหตุผลที่เราต้องบอก engine อย่างชัดเจนว่าโมเดลภาษาใดจะโหลด

```python
# Step 3: Set the language to Arabic (language code "ar")
ocr_engine.set_language("ar")
```

หากคุณลืมบรรทัดนี้, engine จะใช้ค่าเริ่มต้นเป็นภาษาอังกฤษและคุณจะได้ผลลัพธ์ที่เป็นอักขระผสม—สิ่งที่ฉันเคยเห็นบ่อยเกินไป

## ขั้นตอนที่ 4: โหลดภาพ PNG ของคุณ

นี่คือจุดที่ส่วน **แปลงภาพเป็นข้อความ** เริ่มต้นจริงๆ เราจะโหลดไฟล์ PNG ที่มีสคริปต์อารบิก

```python
# Step 4: Load the image that contains the Arabic text
image_path = "YOUR_DIRECTORY/arabic_doc.png"   # replace with your actual path
ocr_engine.set_image(Imaging.Image.load(image_path))
```

### กรณีขอบที่พบบ่อย

| ปัญหา | อาการ | วิธีแก้ |
|-------|---------|-----|
| ภาพมืดเกินไป | ผลลัพธ์มีช่องว่างจำนวนมาก | ทำการพรี‑โปรเซสด้วย Pillow (`ImageEnhance.Brightness`) |
| PNG มีช่องอัลฟา | บาง OCR engine อ่านพิกเซลโปร่งแสงผิด | แปลงเป็น RGB (`image.convert("RGB")`) ก่อนโหลด |
| ข้อความถูกหมุน | ข้อความที่จดจำได้กลับหัว | หมุนภาพ (`image.rotate(90, expand=True)`) ก่อนส่งให้ engine |

## ขั้นตอนที่ 5: รันกระบวนการจดจำ

เมื่อทุกอย่างพร้อม, เราจะขอให้ engine ทำหน้าที่ของมันในที่สุด

```python
# Step 5: Run the recognition process
ocr_result = ocr_engine.recognize()
```

เมธอด `recognize` จะคืนค่าอ็อบเจ็กต์ที่เก็บสตริง Unicode ดิบ, คะแนนความเชื่อมั่น, และ bounding box สำหรับนักพัฒนาส่วนใหญ่, ข้อความธรรมดาก็เพียงพอ

## ขั้นตอนที่ 6: แสดงข้อความอารบิกที่จดจำได้

ตอนนี้เราจะพิมพ์ผลลัพธ์ ในแอปพลิเคชันจริงคุณอาจเขียนลงไฟล์, ฐานข้อมูล, หรือส่งต่อไปยัง API แปลภาษา

```python
# Step 6: Output the recognized text
print(ocr_result.get_text())
```

เมื่อคุณรันสคริปต์, คุณควรเห็นอักขระอารบิกแสดงในคอนโซลของคุณ (ตรวจสอบให้แน่ใจว่าเทอร์มินัลของคุณรองรับ Unicode) หากคุณเห็นเครื่องหมายคำถามหรือสตริงว่าง, ตรวจสอบการตั้งค่าภาษาและคุณภาพของภาพอีกครั้ง

### ผลลัพธ์ที่คาดหวัง

```
هذا نص عربي من صورة PNG تم استخراجها باستخدام OCR.
```

หากผลลัพธ์คล้ายกับบรรทัดข้างบน, ยินดีด้วย—คุณได้ **แยกข้อความอารบิก** จาก PNG อย่างสำเร็จ!

## ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นสคริปต์ทั้งหมด พร้อมคัดลอก‑วาง แทนที่ `YOUR_DIRECTORY/arabic_doc.png` ด้วยพาธไปยังไฟล์ของคุณ

```python
import ocr
from ocr import Imaging

def main():
    # Create OCR engine
    ocr_engine = ocr.OcrEngine()
    
    # Set Arabic language
    ocr_engine.set_language("ar")
    
    # Load the PNG image
    image_path = "YOUR_DIRECTORY/arabic_doc.png"
    ocr_engine.set_image(Imaging.Image.load(image_path))
    
    # Recognize text
    ocr_result = ocr_engine.recognize()
    
    # Print the extracted Arabic text
    print(ocr_result.get_text())

if __name__ == "__main__":
    main()
```

รันด้วย `python run_ocr.py` (หรือชื่อไฟล์ที่คุณตั้ง) หากทุกอย่างติดตั้งอย่างถูกต้อง, คุณจะเห็นประโยคอารบิกแสดงในคอนโซล

## วิธีการรัน OCR บนรูปแบบภาพต่างๆ

โค้ดเดียวกันทำงานได้กับ JPEG, TIFF, หรือ BMP—เพียงเปลี่ยนส่วนขยายไฟล์ เมธอด `Image.load` จะตรวจจับรูปแบบโดยอัตโนมัติ, ดังนั้นคุณสามารถ **แปลงภาพเป็นข้อความ** ได้โดยไม่ต้องเขียนโค้ดเพิ่มเติม

```python
# Example for a JPEG file
ocr_engine.set_image(Imaging.Image.load("sample.jpg"))
```

จำไว้ว่า, คุณภาพของภาพต้นทางมีผลอย่างมากต่อความแม่นยำของขั้นตอน **recognize Arabic text** ภาพความละเอียดสูง, การบีบอัดต่ำให้ผลลัพธ์ที่ดีที่สุด

## การแยกข้อความจาก PNG: เคล็ดลับเพื่อความแม่นยำที่ดียิ่งขึ้น

1. **DPI Matters** – ตั้งเป้าอย่างน้อย 300 dpi. DPI ต่ำมักทำให้พลาดอักขระ  
2. **Contrast is King** – ใช้เครื่องมือประมวลผลภาพ (เช่น OpenCV) เพื่อเพิ่มคอนทราสต์ก่อนส่งภาพให้ OCR engine  
3. **Noise Removal** – จุดสัญญาณรบกวนขนาดเล็กอาจทำให้โมเดลสับสน; การกรองมัธยฐานช่วยได้  

นี่คือตัวอย่างสคริปต์สั้นๆ ที่ใช้ Pillow เพื่อปรับปรุง PNG ก่อน OCR:

```python
from PIL import Image, ImageEnhance, ImageFilter

def preprocess_png(path):
    img = Image.open(path).convert("L")          # grayscale
    img = ImageEnhance.Contrast(img).enhance(2)  # boost contrast
    img = img.filter(ImageFilter.MedianFilter()) # denoise
    return img

# Use the preprocessed image
prepped = preprocess_png("arabic_doc.png")
ocr_engine.set_image(Imaging.Image.from_pil(prepped))
```

## คำถามที่พบบ่อย

**Q: วิธีนี้ทำงานกับภาษาที่เขียนจากขวาไปซ้ายอื่น ๆ นอกจากอารบิกหรือไม่?**  
A: แน่นอน เพียงเปลี่ยนรหัสภาษา (`"ar"` → `"he"` สำหรับ Hebrew, `"fa"` สำหรับ Persian) แล้ว engine จะโหลดโมเดลที่เหมาะสม  

**Q: ถ้าฉันต้องการแยกข้อความจากหลายไฟล์ PNG ในโฟลเดอร์จะทำอย่างไร?**  
A: วนลูปไฟล์, ใช้ `ocr_engine` อินสแตนซ์เดียวกันซ้ำ, แล้วเก็บผลลัพธ์ในรายการหรือเขียนแต่ละไฟล์เป็น `.txt` แยกกัน  

**Q: ฉันสามารถรับคะแนนความเชื่อมั่นสำหรับแต่ละคำได้หรือไม่?**  
A: ได้ `ocr_result` มักมีเมธอด `get_confidences()` ให้ใช้ จับคู่คะแนนความเชื่อมั่นกับคำที่สอดคล้องเพื่อควบคุมคุณภาพ  

## ขั้นตอนต่อไป

ตอนนี้คุณรู้ **วิธีการรัน OCR** บน PNG ภาษาอารบิกแล้ว, พิจารณาแนวคิดต่อไปนี้:

- **Batch processing:** ผสานสคริปต์กับ `os.listdir` เพื่อ **แยกข้อความอารบิก** จากไดเรกทอรีทั้งหมด  
- **Post‑processing:** ใช้ไลบรารี `arabic_reshaper` และ `python-bidi` เพื่อแสดงผลลัพธ์จากขวาไปซ้ายอย่างถูกต้องใน PDF  
- **Integration:** ส่งข้อความที่แยกได้เข้าไปในดัชนีการค้นหา (เช่น Elasticsearch) เพื่อทำให้เอกสารสแกนสามารถค้นหาได้  

แต่ละหัวข้อเหล่านี้ต่อยอดจากพื้นฐานที่อธิบายไว้ที่นี่, และจะช่วยให้คุณเปลี่ยนสคริปต์ **แปลงภาพเป็นข้อความ** ง่ายๆ ให้เป็น pipeline ที่พร้อมใช้งานในผลิตภัณฑ์

---

![how to run OCR on Arabic PNG](

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}