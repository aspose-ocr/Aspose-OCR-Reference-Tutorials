---
category: general
date: 2026-06-22
description: รับพิกัดกล่องขอบเขตจากภาพโดยใช้ Python. เรียนรู้วิธีดึงข้อความจากภาพด้วย
  Python, Aspose OCR และการแยกวิเคราะห์ JSON ในเวลาไม่กี่นาที.
draft: false
keywords:
- get bounding box coordinates
- extract text from image python
- Aspose OCR Python
- OCR layout data JSON
- Python image processing OCR
language: th
og_description: รับพิกัดกล่องขอบเขตจากภาพด้วย Python คู่มือนี้แสดงวิธีดึงข้อความจากภาพด้วย
  Python และ Aspose OCR พร้อมการแยกข้อมูลโครงสร้าง.
og_title: รับพิกัดกล่องขอบเขตจาก OCR ด้วย Python – บทเรียนเต็ม
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Get bounding box coordinates from images using Python. Learn how to
    extract text from image python with Aspose OCR and JSON parsing in minutes.
  headline: Get Bounding Box Coordinates from OCR in Python – Complete Guide
  type: TechArticle
- description: Get bounding box coordinates from images using Python. Learn how to
    extract text from image python with Aspose OCR and JSON parsing in minutes.
  name: Get Bounding Box Coordinates from OCR in Python – Complete Guide
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed on your machine. - An active Aspose.OCR for Python
      license or a free trial (the library works without a license but adds a watermark).
      - `pip install aspose-ocr` (the package name on PyPI). - A sample image called
      `invoice.png` placed in a folder you can reference.'
  - name: 1. Convert Bounding Boxes to Simple Rectangles
    text: 'If your downstream tool expects `(x, y, width, height)` instead of eight
      points, add a helper:'
  - name: 2. Handle Multi‑Page PDFs
    text: 'Aspose OCR can accept PDF streams. Replace the image loading line with:'
  - name: 3. Visualize Bounding Boxes
    text: 'If you want to see the boxes drawn on the original image, use Pillow:'
  type: HowTo
- questions:
  - answer: For large documents, consider streaming the JSON or processing page‑by‑page
      to keep memory usage low.
    question: What if the JSON is huge?
  - answer: Low contrast or handwritten text often trips OCR engines. Pre‑process
      the image (increase contrast, binarize) before feeding it to Aspose.
    question: Why are some words missing?
  - answer: Yes—set `engine.get_settings().set_output_format(ocr.OutputFormat.JSON_CHAR)`
      to receive a `"characters"` array with its own `boundingBox`.
    question: Can I get character‑level coordinates?
  - answer: Absolutely. (0, 0) is the top‑left corner of the image.
    question: Is the coordinate system zero‑based?
  type: FAQPage
tags:
- OCR
- Python
- JSON
- Image Processing
title: รับพิกัดกล่องขอบเขตจาก OCR ใน Python – คู่มือฉบับสมบูรณ์
url: /th/python-java/general/get-bounding-box-coordinates-from-ocr-in-python-complete-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ดึงพิกัด Bounding Box จาก OCR ด้วย Python – คู่มือฉบับสมบูรณ์

เคยต้องการ **ดึงพิกัด bounding box** ของทุกคำในใบแจ้งหนี้ที่สแกนไว้ แต่ไม่แน่ใจว่าจะเริ่มอย่างไรหรือไม่? คุณไม่ได้เป็นคนเดียว ในหลายโครงการอัตโนมัติ คุณต้องระบุตำแหน่งข้อความบนภาพเพื่อไฮไลท์, ปกปิด, หรือส่งต่อไปยังการวิเคราะห์ต่อไป ข่าวดีคือ ด้วยไม่กี่บรรทัดของ Python และ Aspose.OCR คุณสามารถดึงข้อความ **และ** ตำแหน่งที่แม่นยำได้ในหนึ่งขั้นตอน

ในบทแนะนำนี้ เราจะพาคุณผ่านตัวอย่างเชิงปฏิบัติที่แสดงวิธี **extract text from image python**‑style, จากนั้นเจาะลึกข้อมูล JSON layout เพื่อดึง bounding boxes เหล่านั้น ไม่มีเนื้อหาเกินจำเป็น มีสคริปต์ทำงานได้จริง คำอธิบายว่าทำไมแต่ละขั้นตอนสำคัญ และเคล็ดลับเพื่อหลีกเลี่ยงข้อผิดพลาดทั่วไป

---

## สิ่งที่คุณจะสร้าง

เมื่อจบคู่มือนี้ คุณจะมีสคริปต์ Python ที่พร้อมรันที่:

1. โหลดภาพ (เช่น PNG ใบแจ้งหนี้) เข้า Aspose OCR.  
2. ตั้งค่า engine ให้ส่งออกข้อมูล JSON layout  
3. แปลง JSON เป็น dictionary ของ Python  
4. วนลูปผ่านทุกคำที่ถูกจดจำ พิมพ์ข้อความ **และ** พิกัด bounding box ของมัน  

คุณยังจะได้เห็นวิธีปรับโค้ดสำหรับ PDF หลายหน้า, รูปแบบภาพต่าง ๆ, และระบบพิกัดที่กำหนดเอง

### ข้อกำหนดเบื้องต้น

- ติดตั้ง Python 3.8+ บนเครื่องของคุณ  
- ลิขสิทธิ์ Aspose.OCR for Python ที่ใช้งานได้หรือทดลองฟรี (ไลบรารีทำงานได้โดยไม่มีลิขสิทธิ์แต่จะมีลายน้ำ)  
- `pip install aspose-ocr` (ชื่อแพคเกจบน PyPI)  
- ภาพตัวอย่างชื่อ `invoice.png` ที่วางไว้ในโฟลเดอร์ที่คุณสามารถอ้างอิงได้  

เท่านี้—ไม่มีเฟรมเวิร์กหนัก ๆ ไม่มีบริการภายนอก มาเริ่มกันเลย

## ขั้นตอนที่ 1: ติดตั้งและนำเข้าไลบรารีที่จำเป็น

แรกสุด ตรวจสอบให้แน่ใจว่าแพคเกจ Aspose OCR และโมดูล `json` ที่มาพร้อม Python พร้อมใช้งาน โมดูล `json` มาพร้อมกับ Python ดังนั้นเราต้องติดตั้งแค่ Aspose เท่านั้น

```bash
pip install aspose-ocr
```

จากนั้นนำเข้าพวกมันในสคริปต์ของคุณ:

```python
# Step 1: Import the OCR library and the JSON module
import aspose.ocr as ocr
import json
```

> **ทำไมสิ่งนี้สำคัญ:** การนำเข้า `aspose.ocr` ให้คุณเข้าถึง OCR engine ที่มีประสิทธิภาพสูง ส่วน `json` ช่วยแปลงสตริง layout ดิบเป็น dictionary ของ Python เพื่อการเดินทางที่ง่าย

## ขั้นตอนที่ 2: สร้าง OCR Engine และโหลดภาพของคุณ

engine คือหัวใจของกระบวนการ คุณสร้างอินสแตนซ์แล้วชี้ไปที่ภาพที่ต้องการสแกน

```python
# Step 2: Create an OCR engine instance and load the image to be processed
engine = ocr.OcrEngine()
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/invoice.png"))
```

> **เคล็ดลับ:** แทนที่ `"YOUR_DIRECTORY/invoice.png"` ด้วยพาธแบบ absolute หรือ relative ที่ชี้ไปยังไฟล์จริงของคุณ หากไม่พบไฟล์ Aspose จะโยน `FileNotFoundError` ดังนั้นตรวจสอบการสะกดอีกครั้ง

## ขั้นตอนที่ 3: ตั้งค่า Engine ให้ส่งออกข้อมูล JSON Layout

Aspose OCR สามารถคืนค่าเป็นข้อความธรรมดา, JSON เฉพาะ OCR, หรือ JSON layout เต็มที่รวมพิกัดของคำ, บรรทัด, และแม้แต่ตัวอักษรแต่ละตัว สำหรับ **get bounding box coordinates** เราต้องการ layout JSON

```python
# Step 3: Configure the engine to output results in JSON format (includes layout data)
engine.get_settings().set_output_format(ocr.OutputFormat.JSON)
```

> **ทำไมต้องเป็น JSON?** JSON ไม่ขึ้นกับภาษา, อ่านง่ายสำหรับมนุษย์, และแปลงเป็น dictionary ของ Python อย่างสะอาด layout JSON มีอาร์เรย์ `"words"` ที่แต่ละรายการเก็บข้อความและอาร์เรย์ `boundingBox` ของแปดตัวเลข (สี่จุดมุม)

## ขั้นตอนที่ 4: รันการจดจำและดึงสตริง JSON ดิบ

ตอนนี้เราจะรัน OCR จริง ๆ เมธอด `recognize()` จะคืนค่าเป็นอ็อบเจกต์ `OcrResult` ที่เราสามารถดึงสตริง JSON ออกมาได้

```python
# Step 4: Perform recognition and obtain the raw JSON string with words, lines, and bounding boxes
result = engine.recognize()
layout_json = result.get_json()
```

หากคุณพิมพ์ `layout_json` คุณจะเห็นประมาณนี้:

```json
{
  "words": [
    {
      "text": "Invoice",
      "boundingBox": [12, 34, 112, 34, 112, 58, 12, 58]
    },
    {
      "text": "#12345",
      "boundingBox": [130, 34, 210, 34, 210, 58, 130, 58]
    }
    // ... more words ...
  ]
}
```

> **กรณีขอบ:** บางภาพอาจให้ `"words"` เป็นอาร์เรย์ว่าง หาก OCR engine ไม่สามารถตรวจจับข้อความใด ๆ ในกรณีนั้น ตรวจสอบคุณภาพของภาพ (คอนทราสต์, ความละเอียด) ก่อนดำเนินการต่อ

## ขั้นตอนที่ 5: แปลง JSON เป็น Dictionary ของ Python

การทำงานกับโครงสร้าง Python ดั้งเดิมง่ายกว่าการจัดการสตริงมาก ใช้ฟังก์ชัน `json.loads()` เพื่อแปลงสตริง

```python
# Step 5: Parse the JSON string into a Python dictionary for easy access
layout_data = json.loads(layout_json)
```

ตอนนี้ `layout_data["words"]` เป็นรายการของ dictionary, แต่ละรายการแทนคำและ bounding box ของมัน

## ขั้นตอนที่ 6: วนลูปผ่านคำและ **ดึงพิกัด Bounding Box**

นี่คือหัวใจของบทแนะนำของเรา: วนลูปผ่านแต่ละคำ, ดึงข้อความ, และพิมพ์พิกัด นี่คือจุดที่เราจะ **ดึงพิกัด bounding box**

```python
# Step 6: Iterate through each recognized word and display its text and bounding box coordinates
for word in layout_data["words"]:
    text = word["text"]
    box = word["boundingBox"]  # Format: [x1, y1, x2, y2, x3, y3, x4, y4]
    print(f"'{text}' at {box}")
```

**ตัวอย่างผลลัพธ์** (ตัวเลขของคุณอาจแตกต่างตามภาพ):

```
'Invoice' at [12, 34, 112, 34, 112, 58, 12, 58]
'#12345' at [130, 34, 210, 34, 210, 58, 130, 58]
'Date' at [12, 70, 60, 70, 60, 94, 12, 94]
'01/01/2024' at [70, 70, 150, 70, 150, 94, 70, 94]
```

> **ทำไมต้องเป็นรูปแบบแปดจุด?** สี่มุม (บน‑ซ้าย, บน‑ขวา, ล่าง‑ขวา, ล่าง‑ซ้าย) ทำให้คุณวาดรูปหลายเหลี่ยมรอบคำได้ แม้ว่าข้อความจะเอียง หากคุณต้องการสี่เหลี่ยมธรรมดาเท่านั้น คุณสามารถคำนวณ `x_min = min(x1, x2, x3, x4)`, `y_min = min(y1, y2, y3, y4)`, `width = max(x…) - x_min`, และ `height = max(y…) - y_min`

## การปรับปรุงเพิ่มเติม

### 1. แปลง Bounding Boxes เป็นสี่เหลี่ยมธรรมดา

หากเครื่องมือต่อไปของคุณคาดหวังรูปแบบ `(x, y, width, height)` แทนแปดจุด ให้เพิ่มฟังก์ชันช่วยเหลือ:

```python
def box_to_rect(box):
    xs = box[0::2]  # extract x coordinates
    ys = box[1::2]  # extract y coordinates
    x_min, x_max = min(xs), max(xs)
    y_min, y_max = min(ys), max(ys)
    return (x_min, y_min, x_max - x_min, y_max - y_min)

for word in layout_data["words"]:
    rect = box_to_rect(word["boundingBox"])
    print(f"'{word['text']}' rectangle {rect}")
```

### 2. จัดการ PDF หลายหน้า

Aspose OCR สามารถรับสตรีม PDF แทนภาพได้ แทนบรรทัดการโหลดภาพด้วย:

```python
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/document.pdf"))
engine.get_settings().set_page_number(1)  # change for each page in a loop
```

วนลูป `set_page_number` สำหรับแต่ละหน้า เพื่อเก็บพิกัดต่อหน้า

### 3. แสดงผล Bounding Boxes

หากต้องการเห็นกล่องที่วาดบนภาพต้นฉบับ ใช้ Pillow:

```python
from PIL import Image, ImageDraw

img = Image.open("YOUR_DIRECTORY/invoice.png")
draw = ImageDraw.Draw(img)

for word in layout_data["words"]:
    box = word["boundingBox"]
    # Pillow expects a list of tuples [(x1,y1), (x2,y2), ...]
    polygon = [(box[i], box[i+1]) for i in range(0, len(box), 2)]
    draw.line(polygon + [polygon[0]], fill="red", width=2)

img.show()
```

ตอนนี้คุณจะเห็นเส้นขอบสีแดงรอบทุกคำที่จดจำได้—เหมาะสำหรับการดีบักหรือการแสดงผล UI

## คำถามทั่วไป & ข้อควรระวัง

- **ถ้า JSON มีขนาดใหญ่ล่ะ?** สำหรับเอกสารขนาดใหญ่ ควรพิจารณา stream JSON หรือประมวลผลทีละหน้าเพื่อรักษาการใช้หน่วยความจำให้ต่ำ  
- **ทำไมบางคำถึงหายไป?** คอนทราสต์ต่ำหรือข้อความเขียนมือมักทำให้ OCR engine ทำงานไม่ถูกต้อง ก่อนส่งภาพให้ Aspose ควรทำการประมวลผลล่วงหน้า (เพิ่มคอนทราสต์, ทำ binary)  
- **ฉันสามารถรับพิกัดระดับอักขระได้ไหม?** ได้—ตั้งค่า `engine.get_settings().set_output_format(ocr.OutputFormat.JSON_CHAR)` เพื่อรับอาร์เรย์ `"characters"` ที่มี `boundingBox` ของมันเอง  
- **ระบบพิกัดเริ่มจากศูนย์หรือไม่?** แน่นอน (0, 0) คือมุมบน‑ซ้ายของภาพ  

## สคริปต์เต็ม – พร้อมคัดลอกและรัน

ด้านล่างเป็นตัวอย่างที่สมบูรณ์และสามารถรันได้ ซึ่งรวมทุกขั้นตอน บันทึกเป็น `extract_bboxes.py` แล้วรันด้วยคำสั่ง `python extract_bboxes.py`.

```python
import aspose.ocr as ocr
import json

# -------------------------
# 1️⃣ Initialize OCR engine
# -------------------------
engine = ocr.OcrEngine()
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/invoice.png"))

# -------------------------------------------------
# 2️⃣ Ask for JSON layout output (contains bounding boxes)
# -------------------------------------------------
engine.get_settings().set_output_format(ocr.OutputFormat.JSON)

# -------------------------
# 3️⃣ Run recognition
# -------------------------
result = engine.recognize()
layout_json = result.get_json()

# -------------------------
# 4️⃣ Parse JSON
# -------------------------
layout_data = json.loads(layout_json)

# -------------------------
# 5️⃣ Helper to turn 8‑point box into rectangle (optional)
# -------------------------
def box_to_rect(box):
    xs = box[0::2]
    ys = box[1::2]
    x_min, x_max = min(xs), max(xs)
    y_min, y_max = min(ys), max(ys)
    return (x_min, y_min


## คุณควรเรียนรู้อะไรต่อไป?


บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานแบบอื่นในโครงการของคุณ

- [ดึงข้อความจากภาพด้วย Aspose OCR – คู่มือขั้นตอนต่อขั้นตอน](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [วิธีใช้ Aspose OCR เพื่อรับผลลัพธ์เป็น JSON ในการจดจำภาพ](/ocr/english/net/text-recognition/get-result-as-json/)
- [วิธีดึงข้อความจากภาพโดยเตรียมสี่เหลี่ยมใน OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}