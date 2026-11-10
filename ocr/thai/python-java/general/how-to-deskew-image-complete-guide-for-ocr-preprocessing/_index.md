---
category: general
date: 2026-07-05
description: วิธีแก้ไขการเอียงของภาพอย่างรวดเร็ว เรียนรู้การเตรียมภาพสำหรับ OCR แก้ไขการหมุนของภาพ
  และแปลงการสแกนเป็นข้อความด้วย Python.
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- extract text from image
- convert scan to text
- correct image rotation
language: th
og_description: วิธีแก้ไขการเอียงของภาพและเตรียมภาพสำหรับ OCR คู่มือนี้แสดงวิธีการแก้ไขการหมุนของภาพและสกัดข้อความจากภาพโดยใช้
  Python.
og_title: วิธีแก้ไขการเอียงของภาพ – การเตรียม OCR ขั้นตอนโดยละเอียด
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: How to deskew image quickly. Learn to preprocess image for OCR, correct
    image rotation, and convert scan to text with Python.
  headline: How to Deskew Image – Complete Guide for OCR Preprocessing
  type: TechArticle
tags:
- OCR
- image-processing
- Python
title: วิธีแก้การเอียงของภาพ – คู่มือครบถ้วนสำหรับการเตรียม OCR
url: /th/python-java/general/how-to-deskew-image-complete-guide-for-ocr-preprocessing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีแก้ไขการเอียงของภาพ – คู่มือเต็มสำหรับการเตรียมภาพ OCR

เคยสงสัยไหมว่า **วิธีแก้ไขการเอียงของภาพ** ที่ดูเหมือนถ่ายจากสแกนเนอร์เอียง?  คุณไม่ได้เป็นคนเดียว ในหลายโครงการจริง ๆ สิ่งแรกที่ต้องทำก่อนที่คุณจะ **ดึงข้อความจากภาพ** คือการทำให้ภาพตรงขึ้น  

ในบทแนะนำนี้เราจะพาคุณผ่านตัวอย่างแบบทำ‑มือ‑จริง‑จน‑จบ ที่ **เตรียมภาพสำหรับ OCR** แก้ไขการหมุน และสุดท้าย **แปลงสแกนเป็นข้อความ** ด้วยไลบรารี OCR ของ Python ไม่มีการอ้างอิงที่คลุมเครือ เพียงสคริปต์ทำงานที่คุณคัดลอก‑วางได้ พร้อมเคล็ดลับการหลีกเลี่ยงข้อผิดพลาดทั่วไป  

## สิ่งที่คุณจะได้เรียนรู้

เมื่อจบคู่มือนี้คุณจะสามารถ:

* โหลดไฟล์ JPEG หรือ PNG ที่สแกนแล้วและมีการเอียงเล็กน้อยได้  
* ใช้ฟิลเตอร์แก้เอียงและขั้นตอนการทำไบนารีเพื่อเพิ่มความแม่นยำของ OCR  
* รันเอนจิน OCR และ **ดึงข้อความจากภาพ** อย่างเชื่อถือได้  
* เข้าใจว่าทำไม **การหมุนภาพให้ถูกต้อง** ถึงสำคัญต่อการสกัดข้อความต่อไป  

### ข้อกำหนดเบื้องต้น

* Python 3.9+ ติดตั้งบนเครื่องของคุณ  
* แพคเกจ OCR ที่ติดตั้งผ่าน pip ซึ่งใช้ namespace `ocr` เช่น wrapper เล็ก ๆ ของ Tesseract  
* ความคุ้นเคยพื้นฐานกับฟังก์ชัน Python และแนวคิดการประมวลผลภาพ  

ถ้าคุณมีทั้งหมดนี้แล้ว ไปต่อกันเลย

![how to deskew image example](deskew_before_after.png){alt="วิธีแก้ไขการเอียงของภาพ – ก่อนและหลังการแก้ไข"}

## ขั้นตอนที่ 1: ตั้งค่าเอนจิน OCR – วิธีแก้ไขการเอียงของภาพด้วย Python

สิ่งแรกที่ต้องทำคือคุณต้องมีเอนจิน OCR ที่เข้าใจภาษาของเอกสารของคุณ โค้ดด้านล่างแสดงโครงสร้างพื้นฐานขั้นต่ำเพื่อสร้างเอนจินและบอกว่าเรากำลังทำงานกับข้อความภาษาอังกฤษ

```python
import ocr  # Assume this is a wrapper around your OCR backend

# Create an OCR engine instance and set the language
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH
```

*ทำไมจึงสำคัญ:* การตั้งค่าภาษาของเอนจินจะกำหนดชุดอักขระและพจนานุกรมที่ใช้ การข้ามขั้นตอนนี้อาจทำให้ OCR แปลความหมายคำทั่วไปผิดพลาด โดยเฉพาะหลังจากที่คุณ **แก้ไขการหมุนภาพให้ถูกต้อง**  

## ขั้นตอนที่ 2: โหลดภาพสแกนที่ต้องการทำให้ตรง

ต่อไปเรานำไฟล์เข้ามาในหน่วยความจำ แทนที่ `"YOUR_DIRECTORY/skewed_scan.jpg"` ด้วยพาธของภาพของคุณเอง

```python
# Load the raw scanned image
raw_image = ocr.Image.load("YOUR_DIRECTORY/skewed_scan.jpg")
```

หากภาพอยู่ในรูปแบบ NumPy array หรือ OpenCV `Mat` คุณสามารถปรับตัวโหลดให้สอดคล้อง – สิ่งสำคัญคืออ็อบเจกต์ต้องมีเมธอด `apply_filter` ที่จะใช้ต่อไป  

## ขั้นตอนที่ 3: เตรียมภาพสำหรับ OCR – แก้เอียงและทำไบนารี

นี่คือจุดที่เวทมนตร์เกิดขึ้น เราจะต่อฟิลเตอร์สองตัวเข้าด้วยกัน:

1. **Deskew** – ตรวจจับ baseline ของข้อความโดยอัตโนมัติและหมุนภาพกลับเป็นแนวนอน  
2. **Binarize (Otsu)** – แปลงภาพเป็นสีขาว‑ดำบริสุทธิ์ ซึ่งช่วยเพิ่มอัตราการจดจำอย่างมาก  

```python
# Preprocess: deskew then binarize
preprocessed_image = (
    raw_image
    .apply_filter(ocr.Filter.deskew())          # <-- how to deskew image
    .apply_filter(ocr.Filter.binarize_otsu())  # improves OCR reliability
)
```

*เคล็ดลับ:* หากคุณสังเกตว่าข้อความยังดูเบลอหลังทำไบนารี ลองปรับคอนทราสต์หรือใช้วิธีการ threshold ที่ต่างออกไป โมดูล `ocr.Filter` มักมี `adaptive_threshold()` สำหรับกรณีที่ท้าทาย  

## ขั้นตอนที่ 4: รัน OCR – ดึงข้อความจากภาพ

เมื่อมีแคนวาสที่สะอาดและตรงแล้ว เราจะส่งภาพให้เอนจิน ผลลัพธ์จะมีสตริงที่จดจำได้, คะแนนความเชื่อมั่น, และแม้แต่ bounding box หากคุณต้องการใช้ต่อในภายหลัง

```python
# Perform recognition on the preprocessed image
recognition_result = engine.recognize(preprocessed_image)

# Print the raw text output
print(recognition_result.text)
```

ผลลัพธ์ที่พบบ่อยจะเป็นเช่นนี้:

```
Invoice #12345
Date: 2026-07-01
Total: $1,250.00
Thank you for your business!
```

สังเกตว่าการขึ้นบรรทัดใหม่ตรงกันอย่างสมบูรณ์หรือไม่? นั่นคือประโยชน์ของ **การหมุนภาพให้ถูกต้อง** – OCR ไม่ต้องเดาทิศทางของบรรทัดอีกต่อไป  

## ขั้นตอนที่ 5: รวมทุกอย่างไว้ในสคริปต์ไฟล์เดียว – แปลงสแกนเป็นข้อความ

ด้านล่างเป็นสคริปต์เต็มที่สามารถรันได้ ซึ่งรวมทุกส่วนที่เราได้พูดถึงไว้บันทึกเป็น `deskew_ocr.py` แล้วรันด้วย `python deskew_ocr.py`

```python
#!/usr/bin/env python3
"""
Complete example: how to deskew image, preprocess it for OCR,
and extract text from a scanned document.
"""

import ocr  # Replace with your actual OCR library import

def main():
    # 1️⃣ Initialize OCR engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # 2️⃣ Load the image (change path as needed)
    raw_image = ocr.Image.load("YOUR_DIRECTORY/skewed_scan.jpg")

    # 3️⃣ Preprocess – deskew then binarize
    preprocessed = (
        raw_image
        .apply_filter(ocr.Filter.deskew())          # how to deskew image
        .apply_filter(ocr.Filter.binarize_otsu())  # preprocess image for OCR
    )

    # 4️⃣ Recognize text
    result = engine.recognize(preprocessed)

    # 5️⃣ Output the extracted text
    print("=== Recognized Text ===")
    print(result.text)

if __name__ == "__main__":
    main()
```

### ทำไมวิธีนี้ถึงได้ผล

* **Deskew ก่อน** – การหมุนภาพก่อนทำไบนารีทำให้ขั้นตอน threshold ทำงานบนแนวระดับ  
* **Binarize หลัง deskew** – วิธี Otsu สมมติว่ามีฮิสโตแกรมแบบสองโหมด; หน้าเอียงจะทำลายสมมติฐานนี้  
* **โมเดลภาษาอังกฤษ** – บอก OCR ว่าควรคาดหวังอักขระอะไร ลดการเกิด false positive  

หากต้องการรองรับภาษาอื่น เพียงเปลี่ยน `ocr.Language.ENGLISH` เป็น enum ที่เหมาะสม  

## คำถามที่พบบ่อย & กรณีขอบ

| คำถาม | คำตอบ |
|----------|--------|
| *ถ้าสแกนกลับหัวล่ะ?* | ฟิลเตอร์ `deskew()` มักตรวจจับการหมุน 180° ด้วย หากไม่สำเร็จ ให้เรียก `apply_filter(ocr.Filter.rotate(180))` ก่อนทำ deskew |
| *เอกสารของฉันมีกราฟิกสี – การทำไบนารีจะลบออกหรือไม่?* | ใช่ สำหรับเนื้อหาผสม ควรใช้ `ocr.Filter.deskew()` เพียงอย่างเดียว แล้วรัน OCR บนภาพสี คุณยังคงดึงข้อความได้พร้อมคงกราฟิกไว้ |
| *ฉันต้องการประมวลผลหลายไฟล์พร้อมกันได้ไหม?* | ห่อโลจิกในลูป อ่านพาธไฟล์จากรายการ แล้วบันทึก `result.text` ของแต่ละไฟล์เป็นไฟล์ `.txt` แยกกัน |
| *จะเพิ่มความแม่นยำบนสแกนความละเอียดต่ำอย่างไร?* | ขยายภาพด้วยฟิลเตอร์ bicubic **ก่อน** deskew แล้วตามด้วยฟิลเตอร์ sharpen พิกเซลเพิ่มจะให้ข้อมูลมากขึ้นกับ OCR |

## โบนัส: ตรวจสอบการแก้เอียงด้วยภาพ

หากต้องการดูภาพก่อน‑และ‑หลังข้างกัน ให้เพิ่มโค้ดสั้น ๆ ของ Matplotlib:

```python
import matplotlib.pyplot as plt

def show_comparison(original, processed):
    fig, axs = plt.subplots(1, 2, figsize=(10, 4))
    axs[0].imshow(original.to_numpy(), cmap='gray')
    axs[0].set_title('Original')
    axs[0].axis('off')

    axs[1].imshow(processed.to_numpy(), cmap='gray')
    axs[1].set_title('Deskewed & Binarized')
    axs[1].axis('off')
    plt.show()

show_comparison(raw_image, preprocessed)
```

การเห็นการจัดแนวที่แก้ไขแล้วช่วยให้มั่นใจ โดยเฉพาะเมื่อคุณกำลังดีบักชุดสแกนที่ซับซ้อน  

## สรุป

เราได้ครอบคลุม **วิธีแก้ไขการเอียงของภาพ** ทำไม **การเตรียมภาพสำหรับ OCR** จึงสำคัญ และวิธี **ดึงข้อความจากภาพ** เพื่อสุดท้าย **แปลงสแกนเป็นข้อความ** กระบวนการโหลด → deskew → binarize → recognize ทำให้ OCR ได้เห็นหน้าเพจที่สะอาดและตรง ซึ่งแปลเป็นความแม่นยำที่สูงขึ้นและต้องแก้ไขด้วยมือน้อยลง  

ต่อไปในเส้นทาง OCR ของคุณ ลองทดลองกับ:

* แพ็คภาษาอื่น (`ocr.Language.FRENCH` เป็นต้น)  
* เพิ่มขั้นตอนการวิเคราะห์เลย์เอาต์เพื่อค้นหาคอลัมน์หรือโต๊ะ  
* ส่งออกผล OCR เป็น PDF ที่ค้นหาได้ด้วยไลบรารี PDF  

หากเจออุปสรรคหรือมีเทคนิคของคุณเองที่ช่วยจัดการสแกนที่ยากต่อการประมวลผล อย่าลังเลที่จะแสดงความคิดเห็น เราขอให้คุณเขียนโค้ดอย่างสนุกและภาพของคุณอยู่ในระดับที่สมบูรณ์แบบเสมอ!  

## สิ่งที่คุณควรเรียนต่อไป

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคในคู่มือนี้ แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโปรเจกต์ของคุณ

- [วิธีใช้ AspOCR: ฟิลเตอร์เตรียมภาพ OCR สำหรับ .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [ดึงข้อความจากภาพด้วย C# พร้อมเลือกภาษาโดยใช้ Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [วิธีทำ OCR ภาพ – ทำ OCR บนภาพใน OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}