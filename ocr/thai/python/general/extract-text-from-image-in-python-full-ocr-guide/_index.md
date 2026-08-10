---
category: general
date: 2026-06-25
description: ดึงข้อความจากภาพด้วย Python OCR. เรียนรู้วิธีโหลดภาพสำหรับ OCR, ทำ OCR
  ด้วย Python, และแปลงใบเสร็จเป็น JSON ในไม่กี่ขั้นตอนง่าย ๆ.
draft: false
keywords:
- extract text from image
- load image for OCR
- perform OCR in Python
- convert receipt to JSON
language: th
og_description: ดึงข้อความจากภาพด้วย OCR ของ Python. บทเรียนนี้จะแนะนำขั้นตอนการโหลดภาพเพื่อทำ
  OCR, การทำ OCR ด้วย Python, และการแปลงใบเสร็จเป็น JSON.
og_title: ดึงข้อความจากรูปภาพด้วย Python – คู่มือ OCR ฉบับเต็ม
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Extract text from image using Python OCR. Learn how to load image for
    OCR, perform OCR in Python, and convert receipt to JSON in a few simple steps.
  headline: Extract Text from Image in Python – Full OCR Guide
  type: TechArticle
- description: Extract text from image using Python OCR. Learn how to load image for
    OCR, perform OCR in Python, and convert receipt to JSON in a few simple steps.
  name: Extract Text from Image in Python – Full OCR Guide
  steps:
  - name: '**Create an OCR engine instance** – the entry point for all recognition
      work.'
    text: '**Create an OCR engine instance** – the entry point for all recognition
      work.'
  - name: '**Load an image for OCR** – tell the engine which file to read.'
    text: '**Load an image for OCR** – tell the engine which file to read.'
  - name: '**Choose the export format** – JSON or XML, we’ll pick JSON because it’s
      easier to consume.'
    text: '**Choose the export format** – JSON or XML, we’ll pick JSON because it’s
      easier to consume.'
  - name: '**Run the recognition** – actually perform OCR in Python.'
    text: '**Run the recognition** – actually perform OCR in Python.'
  - name: '**Print or store the result** – convert receipt to JSON and see the output.'
    text: '**Print or store the result** – convert receipt to JSON and see the output.'
  - name: Sends the image through a pre‑trained convolutional network.
    text: Sends the image through a pre‑trained convolutional network.
  - name: Decodes the network output into readable characters.
    text: Decodes the network output into readable characters.
  - name: Packages everything into the selected format (JSON in our case).
    text: Packages everything into the selected format (JSON in our case).
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- JSON
title: ดึงข้อความจากรูปภาพด้วย Python – คู่มือ OCR ฉบับเต็ม
url: /th/python/general/extract-text-from-image-in-python-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ดึงข้อความจากรูปภาพด้วย Python – คู่มือ OCR ฉบับเต็ม

เคยต้อง **ดึงข้อความจากรูปภาพ** แต่ไม่รู้ว่าจะเริ่มต้นอย่างไรไหม? ในบทแนะนำนี้เราจะพาคุณผ่านขั้นตอน **โหลดรูปภาพสำหรับ OCR**, **ทำ OCR ด้วย Python**, และ **แปลงใบเสร็จเป็น JSON**—ทั้งหมดด้วยไม่กี่บรรทัดของโค้ด

หากคุณเคยสร้างแอปสแกนใบเสร็จ, แอปติดตามค่าใช้จ่าย, หรือแค่ต้องการอัตโนมัติการป้อนข้อมูล, คุณจะเห็นว่าการเชี่ยวชาญกระบวนการนี้เป็นการเปลี่ยนเกมอย่างไร เมื่อเสร็จสิ้นคุณจะมีสคริปต์ที่อ่านรูปภาพของใบเสร็จและส่งออก JSON ที่สะอาดพร้อมใช้ในบริการต่อไป

## สิ่งที่คุณจะได้เรียน

เราจะครอบคลุมทุกขั้นตอนตั้งแต่การติดตั้งไลบรารี `aocr` ไปจนถึงการจัดการผลลัพธ์ดิบ โดยเฉพาะคุณจะได้เรียนรู้วิธี:

1. **สร้างอินสแตนซ์ของ OCR engine** – จุดเริ่มต้นสำหรับการจดจำทั้งหมด  
2. **โหลดรูปภาพสำหรับ OCR** – บอก engine ว่าจะอ่านไฟล์ใด  
3. **เลือกรูปแบบการส่งออก** – JSON หรือ XML เราจะเลือก JSON เพราะใช้งานง่ายกว่า  
4. **รันการจดจำ** – ทำ OCR จริงใน Python  
5. **พิมพ์หรือบันทึกผลลัพธ์** – แปลงใบเสร็จเป็น JSON และดูผลลัพธ์

ไม่จำเป็นต้องมีประสบการณ์กับ OCR มาก่อน; เพียงแค่ตั้งค่า Python เบื้องต้นและไฟล์รูปภาพ (ใบเสร็จ, ใบปลิว, หรืออะไรก็ได้ที่คุณต้องการ)  

---

![Diagram showing the flow of extracting text from image using Python OCR](extract-text-from-image-python-ocr.png){alt="แผนผังการดึงข้อความจากรูปภาพด้วย Python OCR"}

## ดึงข้อความจากรูปภาพ – ขั้นตอน‑โดย‑ขั้นตอนด้วย Python OCR

ด้านล่างเป็นสคริปต์ที่พร้อมรันครบถ้วน คุณสามารถคัดลอก‑วางลงในไฟล์ชื่อ `receipt_ocr.py` แล้วรันด้วย `python receipt_ocr.py`

```python
# receipt_ocr.py

# 1️⃣ Import the aocr package (make sure it's installed via `pip install aocr`)
import aocr

# 2️⃣ Create an OCR engine instance – this object orchestrates the whole process
engine = aocr.OcrEngine()

# 3️⃣ Load the image you want to process.
#    Replace the path with the location of your receipt or any image.
engine.load_image("YOUR_DIRECTORY/receipt.png")

# 4️⃣ Choose the output format. JSON is handy for APIs and downstream services.
engine.export_format = aocr.ExportFormat.JSON

# 5️⃣ Run the recognition and obtain the raw result.
json_result = engine.recognize()

# 6️⃣ Output the raw JSON string – you can also write it to a file if you prefer.
print(json_result)
```

### ทำไมวิธีนี้ถึงได้ผล

- **อินสแตนซ์ของ engine** – `aocr.OcrEngine()` จัดการงานหนักทั้งหมด (การโหลดโมเดล, การเตรียมข้อมูล ฯลฯ)  
- **การโหลดรูปภาพ** – `engine.load_image()` บอกไลบรารีว่าต้องวิเคราะห์บิตแมปใด; คุณสามารถใส่ JPEG, PNG หรือแม้แต่ PDF หลายหน้าได้  
- **รูปแบบการส่งออก** – ตั้งค่า `engine.export_format` เป็น `aocr.ExportFormat.JSON` ทำให้ผลลัพธ์เป็นสตริงที่มีโครงสร้าง เหมาะกับ API ที่คาดหวัง JSON  
- **การเรียกจดจำ** – `engine.recognize()` ทำการ inference ของเครือข่ายประสาทเทียมเบื้องหลัง; มันคืนสตริง JSON ที่มีบล็อกข้อความที่ตรวจพบ, คะแนนความมั่นใจ, และข้อมูลเลย์เอาต์  

---

## โหลดรูปภาพสำหรับ OCR ด้วย aocr

หากคุณสงสัยว่ารูปภาพต้องผ่านการเตรียมพิเศษหรือไม่ คำตอบสั้นคือ **ไม่**—`aocr` จัดการกรณีส่วนใหญ่อัตโนมัติ (การปรับคอนทราสต์, การแก้ไขการเอียง) อย่างไรก็ตาม คุณสามารถเพิ่มความแม่นยำได้โดย:

- ตรวจสอบให้แน่ใจว่ารูปภาพมีความละเอียดอย่างน้อย 300 dpi  
- ครอบตัดขอบที่ไม่เกี่ยวข้องออก  
- แปลงเป็นระดับสีเทาก่อนส่งเข้า (ไม่บังคับ, `engine.load_image()` จะทำให้เอง)

```python
# Optional preprocessing example using Pillow
from PIL import Image, ImageOps

original = Image.open("YOUR_DIRECTORY/receipt.png")
# Convert to grayscale and increase contrast
processed = ImageOps.autocontrast(original.convert("L"))
processed.save("processed_receipt.png")
engine.load_image("processed_receipt.png")
```

*เคล็ดลับ:* หากใบเสร็จมีเสียงรบกวนมาก การทำขั้นตอนเพิ่มเติมข้างต้นสามารถเพิ่ม **perform OCR in Python** ให้แม่นยำขึ้นอย่างเห็นได้ชัด

---

## เลือกรูปแบบการส่งออกและแปลงใบเสร็จเป็น JSON

คุณอาจถามว่า “ทำไมไม่เอาเป็นข้อความธรรมดา?” เพราะ JSON คงโครงสร้างแบบลำดับชั้น (บรรทัด, คำ, กล่องขอบเขต) ทำให้ง่ายต่อการแมปฟิลด์เช่น *ยอดรวม* หรือ *วันที่* ในภายหลัง

```python
engine.export_format = aocr.ExportFormat.JSON   # Switch to XML with aocr.ExportFormat.XML if needed
```

เมื่อคุณรันสคริปต์, `json_result` จะมีลักษณะประมาณนี้ (ตัดให้สั้นเพื่อความกระชับ):

```json
{
  "pages": [
    {
      "blocks": [
        {
          "text": "Store Name",
          "confidence": 0.98,
          "bbox": [12, 34, 210, 45]
        },
        {
          "text": "Total: $23.45",
          "confidence": 0.96,
          "bbox": [15, 400, 190, 420]
        }
      ]
    }
  ]
}
```

ตอนนี้คุณมี **convert receipt to JSON** payload ที่สามารถส่งตรงไปยังฐานข้อมูล, REST endpoint, หรือโมเดลแมชชีน‑เลิร์นนิงได้

---

## รันการจดจำและดึงผลลัพธ์

ขั้นตอนสุดท้าย—การทำ OCR จริง—ง่ายเพียงเรียก `recognize()` ด้านหลังไลบรารีทำงาน:

1. ส่งรูปภาพผ่านเครือข่ายคอนโวลูชันที่ฝึกมาแล้ว  
2. ถอดรหัสผลลัพธ์ของเครือข่ายเป็นอักขระที่อ่านได้  
3. จัดแพ็คทุกอย่างเป็นรูปแบบที่เลือก (JSON ในกรณีของเรา)

```python
json_result = engine.recognize()
print(json_result)   # <-- This prints the JSON string to stdout
```

หากคุณต้องการบันทึกผลลัพธ์แทนการพิมพ์ เพียงเขียนลงไฟล์:

```python
with open("receipt_output.json", "w", encoding="utf-8") as f:
    f.write(json_result)
```

*กรณีพิเศษ:* ใบเสร็จบางใบมีอักขระที่ไม่ใช่ ASCII (เช่น “€”). ให้เปิดไฟล์ด้วยการเข้ารหัส UTF‑8 ตามที่แสดงข้างต้น เพื่อหลีกเลี่ยงข้อความเสียหาย

---

## ตัวอย่างทำงานเต็มรูปแบบ (รวมทุกขั้นตอนในสคริปต์เดียว)

รวมทุกอย่างเข้าด้วยกัน นี่คือสคริปต์สุดท้ายที่คุณสามารถรันจากต้นจนจบ:

```python
import aocr
from PIL import Image, ImageOps

# Create engine
engine = aocr.OcrEngine()

# Optional: preprocess image for better accuracy
raw = Image.open("YOUR_DIRECTORY/receipt.png")
processed = ImageOps.autocontrast(raw.convert("L"))
processed.save("processed_receipt.png")

# Load the (processed) image
engine.load_image("processed_receipt.png")

# Choose JSON output
engine.export_format = aocr.ExportFormat.JSON

# Run OCR
json_result = engine.recognize()

# Save result
with open("receipt_output.json", "w", encoding="utf-8") as out_file:
    out_file.write(json_result)

print("OCR complete! JSON saved to receipt_output.json")
```

รันด้วยคำสั่ง:

```bash
python receipt_ocr.py
```

คุณควรเห็นบรรทัดยืนยันและในโฟลเดอร์เดียวกันจะมีไฟล์ `receipt_output.json` ที่บรรจุข้อมูลโครงสร้าง

---

## สรุป

คุณได้เรียนรู้ **วิธีดึงข้อความจากรูปภาพ** ด้วย Python, **วิธีโหลดรูปภาพสำหรับ OCR**, **วิธีทำ OCR ใน Python**, และ **วิธีแปลงใบเสร็จเป็น JSON** เพื่อการใช้งานต่อไป กระบวนการแบบต้นถึงปลายนี้เบา, ต้องการเพียงแพคเกจ `aocr` เท่านั้น, และสามารถนำไปใส่ในพายป์ไลน์อัตโนมัติใดก็ได้

ต่อไปคุณจะทำอะไร? ลองสลับรูปแบบการส่งออกเป็น XML, ทดลองเทคนิคการเตรียมรูปภาพต่าง ๆ, หรือสร้าง Flask API เล็ก ๆ ที่รับใบเสร็จอัปโหลดและคืน JSON payload ทันที ความเป็นไปได้ไม่มีขีดจำกัดเมื่อคุณมีพื้นฐานแล้ว

มีคำถามหรือเจออุปสรรค? แสดงความคิดเห็นด้านล่าง แล้วขอให้สนุกกับการเขียนโค้ด!

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคในคู่มือนี้ แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอน‑โดย‑ขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโปรเจกต์ของคุณ

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to extract table from image using Aspose.OCR for .NET](/ocr/english/net/text-recognition/recognize-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}