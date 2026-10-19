---
category: general
date: 2026-06-25
description: เตรียมภาพสำหรับ OCR และจดจำข้อความจากเอกสารสแกนโดยใช้ Python. สอนแบบขั้นตอนต่อขั้นตอนพร้อมโค้ดเต็ม.
draft: false
keywords:
- preprocess image for OCR
- recognize text from scanned document
- Python OCR tutorial
- image deskewing Python
- OCR preprocessing tips
language: th
og_description: เตรียมภาพสำหรับ OCR และจดจำข้อความจากเอกสารสแกนด้วย Python ตามบทเรียนโดยละเอียดที่สามารถรันได้
og_title: การเตรียมภาพสำหรับ OCR ด้วย Python – คู่มือฉบับสมบูรณ์
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Preprocess image for OCR and recognize text from scanned document using
    Python. Step‑by‑step tutorial with full code.
  headline: Preprocess Image for OCR in Python – Complete Guide
  type: TechArticle
- description: Preprocess image for OCR and recognize text from scanned document using
    Python. Step‑by‑step tutorial with full code.
  name: Preprocess Image for OCR in Python – Complete Guide
  steps:
  - name: Create an OCR Engine Instance
    text: '```python import ocr # <-- make sure the OCR library is installed'
  - name: Enable Automatic Deskewing and Binarization
    text: '```python # Step 2: Enable automatic deskewing and binarization to improve
      recognition engine.image_preprocessing = ocr.ImagePreProcessingOptions( auto_deskew=True,
      auto_binarize=True ) ```'
  - name: Load the Skewed Image You Want to Process
    text: '```python # Step 3: Load the skewed image you want to process image_path
      = "YOUR_DIRECTORY/skewed_document.jpg" image = ocr.Image.load(image_path) ```'
  - name: Perform OCR on the Pre‑processed Image
    text: '```python # Step 4: Perform OCR on the pre‑processed image result = engine.recognize(image)
      ```'
  - name: Output the Recognized Text
    text: '```python # Step 5: Output the recognized text print("Deskewed & binarized
      text:", result.text) ```'
  - name: 1. Handling Multiple Languages
    text: 'If your document contains both English and French, configure the engine
      before step 1:'
  - name: 2. Fine‑Tuning Binarization Thresholds
    text: 'Automatic binarization works for most cases, but some old photocopies need
      a custom threshold:'
  - name: 3. Extracting Layout Information
    text: 'Sometimes you need more than raw text—you want to know where each paragraph
      lives on the page. Many engines expose a `result.blocks` collection:'
  - name: 4. Processing a Batch of Files
    text: 'If you have a folder full of scanned PDFs converted to JPEGs, wrap the
      whole flow in a loop:'
  - name: 5. Dealing with Low‑Resolution Scans
    text: 'Low‑resolution images (< 150 dpi) often produce fuzzy characters. A quick
      remedy is to upscale using a high‑quality algorithm before feeding the image
      to the OCR engine:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: การเตรียมภาพสำหรับ OCR ด้วย Python – คู่มือครบถ้วน
url: /th/python-java/general/preprocess-image-for-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# การเตรียมภาพสำหรับ OCR ด้วย Python – คู่มือฉบับสมบูรณ์

เคยสงสัยไหมว่า **preprocess image for OCR** อย่างไรให้ข้อความออกมาสะอาดและเชื่อถือได้? คุณไม่ได้อยู่คนเดียว—นักพัฒนาส่วนใหญ่ก็เจอปัญหาเดียวกันเมื่อหน้าที่สแกนเอียงหรือคอนทราสต์กระจัดกระจาย ข่าวดีคือเพียงไม่กี่บรรทัดของ Python ก็สามารถจัดเรียงภาพให้ตรง, ทำให้เป็นภาพขาว‑ดำ, และคืนข้อความที่คมชัดและค้นหาได้กลับมา

ในบทแนะนำนี้เราจะเดินผ่านขั้นตอนที่แน่นอนเพื่อ **preprocess image for OCR** *และ* **recognize text from scanned document** ด้วยไลบรารี OCR ยอดนิยม เมื่อเสร็จคุณจะมีสคริปต์พร้อมรัน, เข้าใจว่าการตั้งค่าแต่ละอย่างสำคัญอย่างไร, และรู้วิธีปรับให้เหมาะกับกรณีที่ท้าทาย

## สิ่งที่คุณต้องมี

- Python 3.8 หรือใหม่กว่า (โค้ดทำงานได้บน 3.10+ ด้วย)
- แพคเกจ OCR ที่เปิดให้ใช้คลาส `OcrEngine`, `ImagePreProcessingOptions`, และ `Image` (เช่น โมดูล `ocr` สมมติที่ใช้ในตัวอย่าง)
- เอกสารที่สแกนหรือถ่ายภาพที่มีการเอียงหรือคอนทราสต์ต่ำ
- IDE ที่คุณชอบหรือเทอร์มินัลธรรมดา—ไม่ต้องใช้ GUI หนัก

แค่นั้นเอง ไม่ต้องมีไบนารีเพิ่มเติม ไม่ต้องทำ Docker ขั้นสูง ไปกันเลย

## Preprocess Image for OCR – ขั้นตอนทีละขั้น

ด้านล่างเป็นขั้นตอนหลักที่แบ่งเป็นห้าช่วงชัดเจน แต่ละช่วงรวม **เหตุผล** ที่ทำ, **โค้ด** ที่ต้องใช้, และ **คำอธิบายสั้น** เกี่ยวกับสิ่งที่เกิดขึ้นเบื้องหลัง

### ขั้นตอน 1: สร้างอินสแตนซ์ของ OCR Engine

```python
import ocr  # <-- make sure the OCR library is installed

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*ทำไมถึงสำคัญ:*  
อ็อบเจ็กต์ `OcrEngine` คือสมองของกระบวนการ มันเก็บการตั้งค่าต่าง ๆ เช่น language packs, confidence thresholds, และ—ที่สำคัญสำหรับเรา—image‑preprocessing flags การสร้างอินสแตนซ์ก่อนทำให้เรามีพื้นฐานที่สะอาดเพื่อเปิดใช้เทคนิคต่อ ๆ ไป

### ขั้นตอน 2: เปิดใช้งาน Automatic Deskewing และ Binarization

```python
# Step 2: Enable automatic deskewing and binarization to improve recognition
engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,
    auto_binarize=True
)
```

*ทำไมถึงสำคัญ:*  
- **Deskewing** หมุนภาพให้บรรทัดข้อความอยู่ในแนวนอน OCR จะทำงานได้ยากเมื่อ baseline เอียงเกินไม่กี่องศา  
- **Binarization** แปลงภาพเป็นสีขาว‑ดำล้วน ๆ เพื่อลบสัญญาณรบกวนพื้นหลังที่อาจทำให้ตัวอักษรสับสน  
ทั้งสองตัวเลือกเป็น *automatic* ในไลบรารีสมัยใหม่หลายตัว แต่คุณยังต้องเปิดใช้งานด้วยการกำหนดค่าอย่างชัดเจน

> **เคล็ดลับ:** หากภาพต้นฉบับของคุณเรียงตรงแล้ว คุณสามารถตั้งค่า `auto_deskew=False` เพื่อประหยัดมิลลิวินาทีของเวลาในการประมวลผลได้

### ขั้นตอน 3: โหลดภาพที่เอียงที่คุณต้องการประมวลผล

```python
# Step 3: Load the skewed image you want to process
image_path = "YOUR_DIRECTORY/skewed_document.jpg"
image = ocr.Image.load(image_path)
```

*ทำไมถึงสำคัญ:*  
เมธอด `Image.load` อ่านไฟล์เข้าสู่หน่วยความจำและห่อหุ้มเป็นอ็อบเจ็กต์ที่ OCR engine เข้าใจ นอกจากนี้ยังดึงเมตาดาต้าเช่น DPI ซึ่งอาจมีผลต่อค่า scaling เริ่มต้นสำหรับ deskewing

> **กรณีขอบ:** หากภาพเป็นไฟล์ TIFF แบบหลายหน้า คุณต้องวนลูปแต่ละหน้า หรือใช้ตัวช่วยอย่าง `ocr.MultiPageImage.load` การตั้งค่า preprocessing เดียวกันจะใช้กับทุกหน้า

### ขั้นตอน 4: ทำ OCR บนภาพที่ผ่านการเตรียมล่วงหน้า

```python
# Step 4: Perform OCR on the pre‑processed image
result = engine.recognize(image)
```

*ทำไมถึงสำคัญ:*  
ในขั้นตอนนี้ engine จะทำการ deskew และ binarization ตามที่เราเปิดไว้ก่อนหน้า แล้วรัน neural network (หรือ pipeline แบบคลาสสิกของ Tesseract) บนบิตแมปที่ทำความสะอาดแล้ว ผลลัพธ์ `result` มักจะมีข้อความธรรมดา, คะแนนความมั่นใจ, และบางครั้งข้อมูลตำแหน่งของแต่ละคำ

> **ถ้าข้อความยังอ่านไม่ออก?**  
ตรวจสอบความละเอียดของภาพ: OCR ทำงานดีที่สุดที่ 300 dpi หรือสูงกว่า หากต้นฉบับของคุณต่ำกว่า ให้ลอง upscale ก่อนโหลด, หรือขอสแกนต้นฉบับจากแหล่งเอกสาร

### ขั้นตอน 5: แสดงผลข้อความที่ได้รับการจดจำ

```python
# Step 5: Output the recognized text
print("Deskewed & binarized text:", result.text)
```

*ทำไมถึงสำคัญ:*  
`result.text` คือสตริงธรรมดาที่แสดงทุกอย่างที่ engine สามารถอ่านได้ การพิมพ์ออกมาช่วยดีบักอย่างรวดเร็ว; ในแอปจริงคุณอาจบันทึกเป็นไฟล์ `.txt`, เก็บในฐานข้อมูล, หรือส่งต่อไปยัง pipeline NLP ต่อไป

---

## Recognize Text from Scanned Document – ไปไกลกว่าพื้นฐาน

เมื่อ pipeline พื้นฐานทำงานแล้ว เรามาดูการปรับใช้หลายรูปแบบที่คุณอาจเจอเมื่อต้อง **recognize text from scanned document** ในสภาพจริง

### 1. รองรับหลายภาษา

หากเอกสารของคุณมีทั้งภาษาอังกฤษและฝรั่งเศส ให้ตั้งค่า engine ก่อนขั้นตอน 1:

```python
engine = ocr.OcrEngine(languages=["eng", "fra"])
```

หลาย OCR engine รองรับรหัส ISO‑639‑2; การโหลด language pack เพิ่มเติมอาจเพิ่มภาระเล็กน้อยแต่จะทำให้ความแม่นยำบนหน้า multilingual ดีขึ้นอย่างมาก

### 2. ปรับแต่ง Threshold ของ Binarization อย่างละเอียด

Automatic binarization ทำงานได้กับกรณีส่วนใหญ่ แต่สำเนาโฟโต้คัดลอกเก่าอาจต้อง threshold ที่กำหนดเอง:

```python
engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,
    auto_binarize=False,          # turn off auto
    binarization_threshold=180   # manual threshold (0‑255)
)
```

ลองค่าอยู่ระหว่าง 120 ถึง 220 จนกว่าพื้นหลังจะหายไปโดยไม่ทำให้ตัวอักษรอ่อนแอลบหาย

### 3. ดึงข้อมูล Layout

บางครั้งคุณต้องการมากกว่าข้อความดิบ—ต้องการรู้ว่าพารากราฟแต่ละอันอยู่ที่ไหนบนหน้า หลาย engine มีคอลเลกชัน `result.blocks`:

```python
for block in result.blocks:
    print(f"Block at ({block.x}, {block.y}) size {block.width}x{block.height}")
    print(block.text)
```

สิ่งนี้มีประโยชน์อย่างยิ่งสำหรับการสร้างตารางใหม่หรือรักษาลำดับคอลัมน์

### 4. ประมวลผลไฟล์หลายไฟล์เป็นชุด

หากคุณมีโฟลเดอร์เต็มของ PDF ที่แปลงเป็น JPEG, ให้ห่อกระบวนการทั้งหมดในลูป:

```python
import pathlib

folder = pathlib.Path("YOUR_DIRECTORY")
for img_file in folder.glob("*.jpg"):
    img = ocr.Image.load(str(img_file))
    txt = engine.recognize(img).text
    (folder / f"{img_file.stem}.txt").write_text(txt, encoding="utf-8")
    print(f"Processed {img_file.name}")
```

ลูปนี้ใช้อินสแตนซ์ `engine` เดียวกัน ซึ่งมีประสิทธิภาพมากกว่าการสร้างใหม่สำหรับแต่ละไฟล์

### 5. จัดการกับสแกนความละเอียดต่ำ

ภาพความละเอียดต่ำ (< 150 dpi) มักทำให้ตัวอักษรเบลอ วิธีแก้เร็วคือ upscale ด้วยอัลกอริทึมคุณภาพสูงก่อนส่งให้ OCR engine:

```python
from PIL import Image as PilImage

pil_img = PilImage.open("low_res.jpg")
upscaled = pil_img.resize((pil_img.width * 2, pil_img.height * 2), PilImage.LANCZOS)
upscaled.save("upscaled.jpg")
image = ocr.Image.load("upscaled.jpg")
```

การ upscale ไม่ได้สร้างรายละเอียดใหม่ แต่ขั้นตอน binarization จะทำงานกับขอบที่คมชัดขึ้น ทำให้ได้ผลลัพธ์ที่ดีขึ้นเล็กน้อย

---

## ผลลัพธ์ที่คาดหวัง

การรันสคริปต์ห้าขั้นตอนบนสแกนที่เอียงปานกลาง, 300 dpi ควรพิมพ์ข้อความประมาณนี้:

```
Deskewed & binarized text: 
Dear Customer,

Thank you for your recent purchase. Please find your receipt attached.

Best regards,
Acme Corp.
```

หากเห็นอักขระแปลก ๆ ให้ตรวจสอบ flags ของ preprocessing, ความละเอียดของภาพ, และการตั้งค่าภาษาอีกครั้ง

---

## สรุป

เราได้ครอบคลุมทุกอย่างที่คุณต้องการเพื่อ **preprocess image for OCR** และ **recognize text from scanned document** ด้วย Python เริ่มจากการสร้าง engine ใหม่, เปิด automatic deskewing และ binarization, โหลดภาพเอียง, รันการจดจำ, และพิมพ์ข้อความที่สะอาด ตลอดทางเราได้สำรวจการสนับสนุนหลายภาษา, การปรับ threshold ด้วยตนเอง, การดึง layout, การประมวลผลเป็นชุด, และวิธีรับมือกับสแกนความละเอียดต่ำ

ลองใช้สคริปต์กับสแกนของคุณ—อาจเป็นใบเสร็จหลายใบ, แบบฟอร์มเขียนมือ, หรือคลิปข่าวเก่า เมื่อคุณคุ้นเคยแล้ว ลองต่อยอดด้วยการสร้าง PDF หรือส่งผลลัพธ์ไปยังดัชนีการค้นหา ความเป็นไปได้ไม่มีที่สิ้นสุด

**พร้อมรับความท้าทายต่อไปหรือยัง?** ตรวจสอบบทแนะนำของเราเรื่อง *“Extract Tables from Scanned PDFs with Python”* และ *“Train Custom OCR Models with TensorFlow”* เพื่อขยายเครื่องมืออัตโนมัติเอกสารของคุณต่อไป

ขอให้เขียนโค้ดสนุกและ OCR ของคุณคมชัดเสมอ!

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดเทคนิคที่แสดงในคู่มือนี้ ทุกแหล่งข้อมูลมีโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานแบบอื่นในโปรเจกต์ของคุณ

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}