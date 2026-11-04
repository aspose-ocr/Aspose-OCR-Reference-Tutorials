---
category: general
date: 2026-06-22
description: เรียนรู้วิธีตรวจจับภาษาจากภาพและดึงข้อความด้วย OCR ใน Python บทเรียนทีละขั้นตอนที่ครอบคลุมการตรวจจับภาษาอัตโนมัติและการสกัดข้อความ
draft: false
keywords:
- how to detect language
- detect language from image
- extract text from image
- how to use ocr
- how to extract text
language: th
og_description: วิธีตรวจจับภาษาจากภาพโดยใช้ OCR? คู่มือนี้จะแสดงขั้นตอนโดยละเอียดว่าการใช้
  OCR ใน Python เพื่อตรวจจับภาษาและดึงข้อความอย่างไร
og_title: วิธีตรวจจับภาษาในภาพด้วย OCR – คู่มือเต็ม Python
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Learn how to detect language from image and extract text using OCR
    in Python. Step‑by‑step tutorial covering automatic language detection and text
    extraction.
  headline: How to Detect Language from Images with OCR – Complete Python Guide
  type: TechArticle
- description: Learn how to detect language from image and extract text using OCR
    in Python. Step‑by‑step tutorial covering automatic language detection and text
    extraction.
  name: How to Detect Language from Images with OCR – Complete Python Guide
  steps:
  - name: Expected Output
    text: 'If `sample-multilang.png` contains French text, you might see something
      like:'
  - name: 1. Unsupported Image Formats
    text: 'If you try to load a TIFF file that the OCR library doesn’t recognise,
      `ocr.ImageStream.from_file()` will raise an `OcrUnsupportedFormatError`. Wrap
      the load call in a try/except block:'
  - name: 2. Low‑Resolution Images
    text: 'OCR accuracy drops sharply below ~300 dpi. If you notice poor detection,
      consider pre‑processing the image with Pillow:'
  - name: 3. Multiple Languages in One Image
    text: 'When an image contains text in more than one language, the auto‑detect
      feature will pick the dominant one. To capture all languages, you can disable
      auto‑detect and manually pass a list of languages to the engine:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: วิธีตรวจจับภาษาจากภาพด้วย OCR – คู่มือ Python ฉบับสมบูรณ์
url: /th/python-java/general/how-to-detect-language-from-images-with-ocr-complete-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีตรวจจับภาษาจากรูปภาพด้วย OCR – คู่มือ Python ฉบับสมบูรณ์

เคยสงสัย **วิธีตรวจจับภาษา** ในรูปภาพโดยไม่ต้องเปิดดูด้วยตนเองหรือไม่? คุณไม่ได้เป็นคนเดียว ในหลายโครงการ—เช่น ตัวสแกนใบเสร็จ, คลังเอกสารหลายภาษา, หรือแอปแปลงรูปเป็นข้อความ—คุณต้องรู้ว่า *ข้อความนั้นเป็นภาษาอะไร* ก่อนจึงจะดำเนินการต่อได้  

ในบทเรียนนี้เราจะเดินผ่านตัวอย่างเชิงปฏิบัติแบบครบวงจรที่แสดง **วิธีตรวจจับภาษา** จากรูปภาพและดึงอักขระจริงออกมา หลังจากอ่านจบคุณจะสามารถรันเพียงไม่กี่บรรทัดของ Python, ชี้สคริปต์ไปที่รูปภาพที่รองรับใดก็ได้, และได้รับทั้งรหัสภาษาที่ตรวจจับได้ *และ* ข้อความที่สกัดออกมา ไม่ฟุ่มเฟือย เพียงวิธีแก้ปัญหาที่ชัดเจนและคัดลอก‑วางได้ทันที

## สิ่งที่คุณจะได้เรียนรู้

- ติดตั้งและตั้งค่าไลบรารี OCR ขนาดเบาใน Python  
- เริ่มต้นเครื่อง OCR และเปิดใช้งานการตรวจจับภาษาอัตโนมัติ  
- โหลดรูปภาพ (ทุกรูปแบบที่รองรับ) แล้วรัน OCR  
- ดึงภาษาที่ตรวจจับได้และข้อความที่สกัดออกมา  
- จัดการกับปัญหาที่พบบ่อย เช่น รูปแบบที่ไม่รองรับหรือผลลัพธ์ภาษาที่คล ambiguous  

หากคุณเคยถามตัวเอง **วิธีใช้ OCR** สำหรับเอกสารหลายภาษา คู่มือนี้มีคำตอบให้คุณแล้ว

---

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะลงลึก โปรดตรวจสอบว่าคุณมีสิ่งต่อไปนี้ในเครื่องของคุณ:

| ความต้องการ | เหตุผลที่สำคัญ |
|-------------|----------------|
| Python 3.9 หรือใหม่กว่า | แพ็กเกจ OCR ที่เราจะใช้ต้องการตัวแปลที่ทันสมัย |
| `pip` (ตัวจัดการแพ็กเกจของ Python) | จำเป็นสำหรับการติดตั้งไลบรารี OCR |
| ตัวอย่างรูปภาพที่มีข้อความอย่างน้อยหนึ่งภาษา (เช่น `sample-multilang.png`) | ให้คุณมีสิ่งที่ทดสอบได้จริง |
| ตัวเลือก: สภาพแวดล้อมเสมือน (`venv` หรือ `conda`) | ทำให้การจัดการ dependencies เป็นระเบียบและหลีกเลี่ยงการชนกันของเวอร์ชัน |

> **เคล็ดลับ:** หากคุณทำงานในสภาพแวดล้อมเสมือน ให้เปิดใช้งานมันก่อนติดตั้งแพ็กเกจ OCR เพื่อให้ Python หลักของคุณสะอาด

---

## ขั้นตอนที่ 1: ติดตั้งไลบรารี OCR

สำหรับการสาธิตนี้เราจะใช้แพ็กเกจสมมติ `ocr` ที่มี API เหมือนกับโค้ดตัวอย่าง ในสถานการณ์จริงคุณสามารถเปลี่ยนเป็น `pytesseract`, `easyocr` หรือไลบรารีอื่นที่รองรับการตรวจจับภาษาอัตโนมัติได้

```bash
pip install ocr
```

> **หมายเหตุ:** แพ็กเกจนี้มีขนาดเบา (< 5 MB) และทำงานได้บน Windows, macOS, และ Linux หากเจอข้อผิดพลาดเรื่องสิทธิ์ ให้เพิ่ม `--user` เข้าไปในคำสั่ง

---

## ขั้นตอนที่ 2: เริ่มต้นเครื่อง OCR – วิธีตรวจจับภาษา

เมื่อไลบรารีพร้อม เราสามารถสร้างอินสแตนซ์ของเครื่อง OCR ได้ ซึ่งเป็นอ็อบเจกต์ที่ทำหน้าที่สแกนรูปภาพและหาภาษา

```python
import ocr

# Initialise the OCR engine – this is where we start the language detection pipeline
engine = ocr.OcrEngine()
```

ทำไมต้องเริ่มด้วยเครื่อง? คิดว่าเครื่องเป็น “สมอง” ของระบบ OCR; มันเก็บการตั้งค่า, โหลดโมเดลภาษา, และจัดการงานหนักเบื้องหลัง การเริ่มต้นก่อนทำให้การเรียกต่อไป (เช่น การโหลดรูปภาพ) มีบริบทที่พร้อมใช้งาน

---

## ขั้นตอนที่ 3: โหลดรูปภาพและเปิดใช้งานการตรวจจับภาษาอัตโนมัติ

ขั้นตอนต่อไปคือใส่รูปภาพเข้าไปในเครื่อง เราจะเปิดฟลัก *auto‑detect language* เพื่อให้เครื่อง OCR พยายามคาดเดาภาษาโดยอัตโนมัติ

```python
# Load the image (any supported format – PNG, JPEG, BMP, etc.)
image_path = "YOUR_DIRECTORY/sample-multilang.png"
image = ocr.ImageStream.from_file(image_path)

# Attach the image to the engine
engine.set_image(image)

# Enable automatic language detection – this is the key for detecting language from image
engine.get_settings().set_auto_detect_language(True)
```

> **ทำไมต้องเปิด auto‑detect?**  
> ไลบรารี OCR ส่วนใหญ่จะตั้งค่าภาษาเริ่มต้นเป็นอังกฤษ หากเอกสารของคุณมีภาษาฝรั่งเศส, ญี่ปุ่น หรือสคริปต์อื่น ๆ เครื่องจะพลาดหากไม่ได้เปิดการตั้งค่านี้ โดยการตั้งค่า `set_auto_detect_language(True)` เราให้เครื่องสแกนบิตแมป, เปรียบเทียบสถิติรูปทรงอักขระ, แล้วเลือกโมเดลภาษาที่น่าจะเป็นไปได้ที่สุด

---

## ขั้นตอนที่ 4: ทำ OCR – สกัดข้อความจากรูปภาพ

เมื่อรูปภาพโหลดแล้วและเปิดการตรวจจับภาษา การทำ OCR จริงเป็นแค่การเรียกเมธอดเดียว

```python
# Run the OCR process – this both detects the language and extracts the text
result = engine.recognize()
```

เมธอด `recognize()` ทำสองอย่างภายใต้ผิวหนัง:

1. **การตรวจจับภาษา:** รันคลาสสิฟายเออร์ขนาดเล็กบนรูปเพื่อเลือกรหัสภาษา (เช่น `en`, `fr`, `es`)  
2. **การสกัดข้อความ:** จากนั้นใช้โมเดลที่ตรงกับภาษานั้นเพื่อแปลงอักขระเป็นสตริง Unicode  

เพราะสองขั้นตอนทำพร้อมกัน คุณจะได้อ็อบเจกต์ `result` ที่บรรจุทุกอย่างที่ต้องการ

---

## ขั้นตอนที่ 5: ดึงและแสดงภาษาที่ตรวจจับได้และข้อความที่สกัดออกมา

สุดท้าย เราจะดึงรหัสภาษาและข้อความดิบจากอ็อบเจกต์ `result` แล้วพิมพ์ออกคอนโซล

```python
# Print the detected language and the extracted text
print("Detected language:", result.get_language())
print("Text:", result.get_text())
```

### ผลลัพธ์ที่คาดหวัง

หาก `sample-multilang.png` มีข้อความเป็นภาษาฝรั่งเศส คุณอาจเห็นดังนี้:

```
Detected language: fr
Text: Bonjour, ceci est un texte d'exemple.
```

หากรูปภาพคล ambiguous หรือมีหลายภาษา เครื่องจะคืนค่าภาษาเดียวที่มันมั่นใจที่สุด และคุณสามารถตรวจสอบคะแนนความมั่นใจได้ในภายหลัง (ไลบรารีส่วนใหญ่มีเมธอด `get_confidence()` สำหรับกรณีใช้งานขั้นสูง)

---

## การจัดการกับกรณีขอบทั่วไป

### 1. รูปแบบภาพที่ไม่รองรับ

หากคุณพยายามโหลดไฟล์ TIFF ที่ไลบรารี OCR ไม่รู้จัก `ocr.ImageStream.from_file()` จะโยน `OcrUnsupportedFormatError` ให้ห่อการโหลดด้วย `try/except`:

```python
try:
    image = ocr.ImageStream.from_file(image_path)
except ocr.OcrUnsupportedFormatError as e:
    print(f"Unsupported format: {e}")
    raise
```

### 2. ภาพความละเอียดต่ำ

ความแม่นยำของ OCR ลดลงอย่างชัดเจนเมื่อต่ำกว่า ~300 dpi หากพบการตรวจจับแย่ลง ให้ทำการพรี‑โปรเซสด้วย Pillow:

```python
from PIL import Image, ImageEnhance

pil_img = Image.open(image_path)
pil_img = pil_img.resize((pil_img.width * 2, pil_img.height * 2), Image.LANCZOS)
pil_img.save("resized.png")
image = ocr.ImageStream.from_file("resized.png")
```

### 3. หลายภาษาในหนึ่งภาพ

เมื่อภาพมีข้อความหลายภาษา ฟีเจอร์ auto‑detect จะเลือกภาษาที่โดดเด่นที่สุด หากต้องการจับทุกภาษา คุณสามารถปิด auto‑detect แล้วส่งรายการภาษาที่ต้องการให้เครื่อง:

```python
engine.get_settings().set_auto_detect_language(False)
engine.get_settings().set_languages(["en", "fr", "de"])
```

ตอนนี้ OCR จะพยายามรู้จำอักขระโดยใช้แต่ละโมเดลภาษาและคืนค่าการจับคู่ที่ดีที่สุดสำหรับแต่ละบล็อกข้อความ

---

## สคริปต์เต็ม – รวมทุกขั้นตอนไว้ในไฟล์เดียว

ด้านล่างเป็นสคริปต์ Python ที่พร้อมรันครบทุกขั้นตอนที่เราอธิบายไว้ บันทึกเป็น `detect_language_ocr.py` แล้วรันด้วย `python detect_language_ocr.py`

```python
# detect_language_ocr.py
# -------------------------------------------------
# How to detect language from image and extract text using OCR
# -------------------------------------------------

import ocr

def main():
    # 1️⃣ Initialise the OCR engine
    engine = ocr.OcrEngine()

    # 2️⃣ Load the image (any supported format)
    image_path = "YOUR_DIRECTORY/sample-multilang.png"
    try:
        image = ocr.ImageStream.from_file(image_path)
    except ocr.OcrUnsupportedFormatError as err:
        print(f"Error loading image: {err}")
        return

    engine.set_image(image)

    # 3️⃣ Enable automatic language detection
    engine.get_settings().set_auto_detect_language(True)

    # 4️⃣ Perform OCR – this both detects language and extracts text
    try:
        result = engine.recognize()
    except ocr.OcrRecognitionError as err:
        print(f"OCR failed: {err}")
        return

    # 5️⃣ Retrieve and display the detected language and extracted text
    print("Detected language:", result.get_language())
    print("Text:", result.get_text())

if __name__ == "__main__":
    main()
```

**รันสคริปต์** แล้วคุณจะเห็นรหัสภาษาและข้อความที่สกัดออกมาทันที นั่นคือคำตอบทั้งหมดสำหรับ **วิธีตรวจจับภาษา** และ **วิธีสกัดข้อความ** จากรูปภาพด้วย OCR

---

## ก้าวต่อไป – ขั้นตอนต่อไป & หัวข้อที่เกี่ยวข้อง

- **เพิ่มความแม่นยำ:** ทดลองพรี‑โปรเซสภาพ (thresholding, denoising) ด้วย `opencv-python`  
- **ประมวลผลเป็นชุด:** ห่อสคริปต์ในลูปเพื่อจัดการโฟลเดอร์รูปหลายไฟล์  
- **เชื่อมต่อกับ NLP:** ส่งข้อความที่สกัดไปยังไลบรารีระบุภาษาอย่าง `langdetect` เพื่อยืนยันผลอีกครั้ง  
- **สำรวจเครื่อง OCR อื่น:** `pytesseract` ให้การควบคุมละเอียด, `easyocr` รองรับกว่า 80 ภาษาแบบพร้อมใช้  

หัวข้อทั้งหมดนี้เชื่อมโยงกับคีย์เวิร์ดรองของเรา—*detect language from image*, *extract text from image*, *how to use OCR*, และ *how to extract text*—เพื่อให้คุณขยายเครื่องมือโดยไม่ต้องเริ่มจากศูนย์

---

## สรุป

เราได้ครอบคลุม **วิธีตรวจจับภาษา** จากรูปภาพแล้ว ผ่านการอธิบายโค้ดที่จำเป็นและเหตุผลของแต่ละขั้นตอน โดยการเริ่มต้นเครื่อง OCR, โหลดรูป, เปิดการตรวจจับภาษาอัตโนมัติ, แล้วเรียก `recognize()` คุณจะได้ทั้งตัวระบุภาษาและข้อความที่สกัดออกมาในขั้นตอนเดียว  

ตอนนี้คุณสามารถฝังตรรกะนี้ลงในแอปพลิเคชันขนาดใหญ่—ไม่ว่าจะเป็นบริการสแกนใบเสร็จ, แชทบอทหลายภาษา, หรือยูทิลิตี้เดสก์ท็อปง่าย ๆ แนวคิดหลักยังคงเหมือนเดิม: ให้เครื่อง OCR ทำงานหนัก แล้วใช้ผลลัพธ์ตามที่คุณต้องการ  

มีคำถามเกี่ยวกับกรณีขอบหรืออยากแชร์การใช้งานที่เจ๋ง? แสดงความคิดเห็นด้านล่างได้เลย ขอให้สนุกกับการเขียนโค้ดและแปลงภาพเป็นข้อความที่ค้นหาได้!  

![วิธีตรวจจับภาษาจากรูปภาพ](ocr-demo.png "ภาพหน้าจอแสดงวิธีตรวจจับภาษาจากรูปภาพด้วย Python OCR")

## สิ่งที่คุณควรเรียนต่อ

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโปรเจกต์ของคุณ

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}