---
category: general
date: 2026-06-19
description: ดึงข้อความจากรูปภาพด้วย Python OCR. เรียนรู้การตรวจจับภาษาที่อัตโนมัติ
  การประมวลผลแบบขนาน และการรับรู้แบบชุดในบทเรียนสั้น ๆ.
draft: false
keywords:
- extract text from images
- Python OCR library
- automatic language detection
- parallel processing OCR
- batch image recognition
- ocr.OcrEngine usage
language: th
og_description: ดึงข้อความจากรูปภาพด้วย Python OCR. คู่มือนี้แสดงการตรวจจับภาษาอัตโนมัติ,
  การประมวลผลแบบขนาน, และการรับรู้แบบชุดในบทเรียนเดียว.
og_title: ดึงข้อความจากรูปภาพใน Python – คู่มือ OCR เต็ม
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: extract text from images using Python OCR. Learn automatic language
    detection, parallel processing, and batch recognition in a concise tutorial.
  headline: extract text from images in Python – Full OCR Guide
  type: TechArticle
- description: extract text from images using Python OCR. Learn automatic language
    detection, parallel processing, and batch recognition in a concise tutorial.
  name: extract text from images in Python – Full OCR Guide
  steps:
  - name: Python 3.8 or newer installed.
    text: Python 3.8 or newer installed.
  - name: The `ocr` package (`pip install ocr`).
    text: The `ocr` package (`pip install ocr`).
  - name: A folder of PNG (or JPG) images you want to process.
    text: A folder of PNG (or JPG) images you want to process.
  - name: Basic familiarity with Python functions and loops.
    text: Basic familiarity with Python functions and loops.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: สกัดข้อความจากรูปภาพใน Python – คู่มือ OCR ฉบับเต็ม
url: /th/python-java/general/extract-text-from-images-in-python-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ดึงข้อความจากรูปภาพใน Python – คู่มือ OCR ฉบับเต็ม

เคยสงสัยไหมว่าจะแยก **extract text from images** อย่างไรโดยไม่ต้องพิมพ์ทุกคำด้วยตนเอง? คุณไม่ได้เป็นคนเดียว ไม่ว่าคุณจะกำลังดิจิไทซ์ใบเสร็จเก่า, สร้างคลังเอกสารที่ค้นหาได้, หรือแค่เล่นกับเทคนิค AI ที่เจ๋ง ความสามารถในการดึงข้อความจากรูปภาพเป็นทักษะที่จำเป็นสำหรับนักพัฒนา Python ทุกคนในวันนี้.

ในบทแนะนำนี้ เราจะพาคุณผ่านตัวอย่างที่สมบูรณ์และพร้อมรันที่ **extracts text from images** ด้วยเครื่องมือ OCR ยอดนิยม เราจะครอบคลุมการตรวจจับภาษาอัตโนมัติ, การประมวลผลแบบขนานเพื่อความเร็ว, และการจดจำภาพแบบแบตช์ เพื่อให้คุณจัดการกับหลายสิบไฟล์ในไม่กี่วินาที ฟังดูตรงกับความต้องการของคุณหรือไม่? มาเริ่มกันเลย.

## สิ่งที่คุณจะได้เรียนรู้

- วิธีสร้างอินสแตนซ์ของ OCR engine ด้วย `ocr.OcrEngine`.
- เปิดใช้งาน **automatic language detection** เพื่อให้ engine เลือกภาษาที่ถูกต้องโดยอัตโนมัติ.
- กำหนดค่า **parallel processing OCR** ด้วย thread pool ที่กำหนดเอง.
- รัน **batch image recognition** บนรายการไฟล์.
- พิมพ์ข้อความที่จดจำได้สำหรับแต่ละภาพ, พร้อมสำหรับการบันทึกหรือทำดัชนี.

ไม่ต้องอ้างอิงเอกสารภายนอก—ทุกอย่างที่คุณต้องการอยู่ที่นี่แล้ว, และโค้ดทำงานได้ทันทีด้วยแพคเกจ `ocr` (ติดตั้งโดยใช้ `pip install ocr`).

## ข้อกำหนดเบื้องต้น

ก่อนเริ่ม, ตรวจสอบว่าคุณมี:

1. Python 3.8 หรือใหม่กว่า
2. `ocr` package (`pip install ocr`)
3. โฟลเดอร์ที่มีรูปภาพ PNG (หรือ JPG) ที่ต้องการประมวลผล
4. ความคุ้นเคยพื้นฐานกับฟังก์ชันและลูปของ Python

เท่านี้—ไม่มีการพึ่งพาที่ซับซ้อน, ไม่มีการใช้ GPU, เพียงแค่ Python ธรรมดา.

![ตัวอย่างการดึงข้อความจากรูปภาพ](https://example.com/ocr-demo.png "ภาพหน้าจอแสดงผลลัพธ์การดึงข้อความจากรูปภาพ")

*ข้อความแทน: ภาพสาธิตการดึงข้อความจากรูปภาพ*

## ขั้นตอนที่ 1 – ตั้งค่า OCR Engine (คีย์เวิร์ดหลักในแอคชัน)

อันดับแรก: สร้างอินสแตนซ์ของ OCR engine. คิดว่า `ocr.OcrEngine()` เป็นสมองของการทำงาน; มันรู้วิธีอ่านอักขระ, บรรทัด, และย่อหน้า.

```python
import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

ทำไมเราต้องการ engine ที่กำหนดเอง? เพราะการใช้ **ocr.OcrEngine usage** ให้คุณควบคุมการตั้งค่าภาษา, การทำงานหลายเธรด, และอื่น ๆ อย่างละเอียด มันเป็นวิธีที่ยืดหยุ่นที่สุดในการ **extract text from images** เมื่อเทียบกับฟังก์ชันหนึ่งบรรทัด.

## ขั้นตอนที่ 2 – ให้ Engine ตรวจจับภาษาด้วยตนเอง

ไลบรารี OCR ส่วนใหญ่ต้องการให้คุณระบุภาษาที่ต้องการค้นหา ซึ่งเหมาะกับโครงการที่ใช้ภาษาเดียว แต่ทำให้ยุ่งยากสำหรับแบตช์ที่มีหลายภาษา โชคดีที่แพคเกจ `ocr` รองรับ **automatic language detection**.

```python
# Step 2: Enable automatic language detection
engine.language = ocr.Language.Auto
```

การตั้งค่า `engine.language` เป็น `ocr.Language.Auto` จะบอก engine ให้ตรวจสอบแต่ละภาพและเลือกโมเดลภาษาที่เหมาะสม บรรทัดเล็ก ๆ นี้ช่วยคุณประหยัดเวลาการตั้งค่าด้วยตนเองหลายชั่วโมงเมื่อทำงานกับเอกสารระหว่างประเทศ.

## ขั้นตอนที่ 3 – เร่งความเร็วด้วย Parallel Processing OCR

หากคุณมีคอร์ CPU สี่คอร์หรือมากกว่า ทำไมไม่ใช้มัน? Engine สามารถสร้าง thread pool เพื่อให้หลายภาพถูกประมวลผลพร้อมกัน นี่คือจุดเด่นของ **parallel processing OCR**.

```python
# Step 3: Enable parallel processing with four worker threads
engine.set_thread_pool_size(4)
```

คุณสามารถปรับจำนวน `4` ตามเครื่องของคุณได้ จำนวนเธรดที่มากขึ้น → การรันแบตช์ที่เร็วขึ้น, แต่จำไว้ว่าทุกเธรดใช้หน่วยความจำ, ดังนั้นหาจุดที่เหมาะสมสำหรับสภาพแวดล้อมของคุณ.

## ขั้นตอนที่ 4 – รวบรวมรูปภาพที่ต้องการประมวลผล

ตอนนี้เราต้องการรายการเส้นทางไฟล์ คุณสามารถสร้างรายการนี้ด้วยตนเอง, อ่านจาก CSV, หรือใช้ `glob`. เพื่อความชัดเจน เราจะกำหนดรายการสั้น ๆ ด้วยการเขียนโค้ดตรง:

```python
# Step 4: Prepare a list of image files to be recognized
files = [
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.png",
    "YOUR_DIRECTORY/doc4.png"
]
```

แทนที่ `YOUR_DIRECTORY` ด้วยเส้นทางจริงบนระบบของคุณ หากคุณมีหลายสิบไฟล์, การใช้ `glob.glob("*.png")` อย่างรวดเร็วจะทำงานหนักให้คุณ.

## ขั้นตอนที่ 5 – รัน Batch Image Recognition

นี่คือหัวใจของบทแนะนำ: การเรียกเดียวที่ประมวลผลทุกภาพใน `files` และคืนรายการอ็อบเจ็กต์ผลลัพธ์ นี่คือฟีเจอร์ **batch image recognition** ที่ทำให้ OCR ขนาดใหญ่เป็นไปได้จริง.

```python
# Step 5: Perform batch recognition on all images
results = engine.recognize_batch(files)
```

เบื้องหลัง, engine จะกระจายไฟล์แต่ละไฟล์ไปยังสี่เธรดทำงานที่เราตั้งค่าไว้ก่อนหน้า, พร้อมกับตรวจจับภาษาของแต่ละภาพโดยอัตโนมัติ วิธีนี้คืนรายการที่แต่ละองค์ประกอบเก็บข้อความที่จดจำได้และเมตาดาต้า.

## ขั้นตอนที่ 6 – พิมพ์ (หรือบันทึก) ข้อความที่ดึงออกมา

สุดท้าย, เราจะวนลูปผลลัพธ์และพิมพ์ข้อความ ในโครงการจริงคุณอาจบันทึกลงฐานข้อมูลหรือไฟล์ CSV, แต่การพิมพ์ทำให้ตัวอย่างง่ายขึ้น.

```python
# Step 6: Output the recognized text for each image
for result in results:
    print("---")
    print(f"File: {result.file_path}")
    print("Extracted Text:")
    print(result.text.strip())
    print("---\n")
```

**ผลลัพธ์ที่คาดหวัง** (ตัดทอนเพื่อความกระชับ):

```
---
File: YOUR_DIRECTORY/doc1.png
Extracted Text:
Invoice #12345
Date: 2024‑03‑15
Total: $250.00
---
```

แต่ละบล็อกจะแสดงชื่อไฟล์ตามด้วยสตริงที่ได้จาก OCR หากภาพมีหลายภาษา, คุณจะเห็นอักขระที่เหมาะสมปรากฏขึ้นเนื่องจากขั้นตอน **automatic language detection** ก่อนหน้า.

## เคล็ดลับระดับมืออาชีพ & จุดบกพร่องทั่วไป

- **Image quality matters** – รูปภาพที่เบลอหรือคอนทราสต์ต่ำจะให้ผลลัพธ์เป็นขยะ. เตรียมการล่วงหน้าด้วย OpenCV (`cv2.threshold`, `cv2.resize`) หากจำเป็น.
- **Thread count vs. I/O** – หากรูปภาพของคุณอยู่บนไดรฟ์เครือข่ายที่ช้า, การเพิ่มจำนวนเธรดอาจไม่ช่วย. คอยตรวจสอบการใช้ CPU ด้วย `top` หรือ `Task Manager`.
- **Unicode handling** – `result.text` เป็นสตริง Unicode. เมื่อเขียนไฟล์, เปิดด้วย `encoding="utf‑8"` เพื่อหลีกเลี่ยง `UnicodeEncodeError`s.
- **Memory usage** – PDF ขนาดใหญ่สามารถใช้ RAM มาก. หากเจอ `MemoryError`, ลดขนาด thread pool หรือประมวลผลภาพเป็นชิ้นเล็ก ๆ.

## สคริปต์ทำงานเต็มรูปแบบ

ด้านล่างเป็นสคริปต์ที่พร้อมคัดลอกและวางครบถ้วนซึ่งรวมทุกขั้นตอนที่เราอธิบายไว้. บันทึกเป็น `batch_ocr.py` และรัน `python batch_ocr.py`.

```python
#!/usr/bin/env python3
"""
Batch OCR script to extract text from images using the ocr package.
Features:
- Automatic language detection
- Parallel processing with configurable thread pool
- Simple batch API for multiple files
"""

import ocr
import os
import sys

def main(image_dir: str, workers: int = 4):
    # Verify directory exists
    if not os.path.isdir(image_dir):
        print(f"Error: Directory '{image_dir}' does not exist.", file=sys.stderr)
        sys.exit(1)

    # Build list of PNG/JPG files
    supported_ext = (".png", ".jpg", ".jpeg", ".tif", ".tiff")
    files = [
        os.path.join(image_dir, f)
        for f in os.listdir(image_dir)
        if f.lower().endswith(supported_ext)
    ]

    if not files:
        print("No supported image files found in the directory.", file=sys.stderr)
        sys.exit(1)

    # Initialize OCR engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.Auto          # automatic language detection
    engine.set_thread_pool_size(workers)         # parallel processing OCR

    # Perform batch recognition
    print(f"Processing {len(files)} files with {workers} workers...")
    results = engine.recognize_batch(files)

    # Output results
    for result in results:
        print("---")
        print(f"File: {result.file_path}")
        print("Extracted Text:")
        print(result.text.strip())
        print("---\n")

if __name__ == "__main__":
    # Example usage: python batch_ocr.py ./my_images 4
    if len(sys.argv) < 2:
        print("Usage: python batch_ocr.py <image_directory> [worker_count]")
        sys.exit(1)

    directory = sys.argv[1]
    worker_count = int(sys.argv[2]) if len(sys.argv) > 2 else 4
    main(directory, worker_count)
```

รันโดยใช้คำสั่งดังนี้:

```bash
python batch_ocr.py ./my_images 4
```

คุณจะเห็นบล็อกข้อความที่จัดรูปแบบอย่างสวยงามสำหรับแต่ละภาพ, แสดงให้เห็นว่าคุณสามารถ **extract text from images** ในระดับใหญ่ได้.

## ขั้นตอนต่อไปคืออะไร?

เมื่อคุณเชี่ยวชาญพื้นฐานของ **extract text from images** ด้วย Python แล้ว, ลองสำรวจต่อไปนี้:

- **Post‑processing**: ทำความสะอาดผลลัพธ์ OCR ด้วย regex หรือไลบรารีประมวลผลภาษาธรรมชาติ.
- **PDF conversion**: ส่งสตริงที่ดึงออกไปยังตัวสร้าง PDF เพื่อสร้าง PDF ที่ค้นหาได้.
- **Cloud OCR services**: เปรียบเทียบผลลัพธ์ `ocr` ภายในเครื่องกับ Google Vision หรือ Azure OCR เพื่อความแม่นยำในกรณีพิเศษ.
- **GUI front‑end**: สร้างแอป Flask หรือ FastAPI ขนาดเล็กที่ให้ผู้ใช้อัปโหลดรูปภาพและดูข้อความที่ดึงออกได้ทันที.

แต่ละหัวข้อเหล่านี้ต่อยอดจากพื้นฐาน **Python OCR library** ที่คุณตั้งค่าไว้, และทั้งหมดจะได้ประโยชน์จากเทคนิค **parallel processing OCR** เดียวกันที่เราใช้ในที่นี้.

---

*ขอให้สนุกกับการเขียนโค้ด! หากเจอปัญหาใด ๆ, แสดงความคิดเห็นด้านล่าง—ฉันพร้อมช่วยแก้ไขข้อผิดพลาดของ OCR เสมอ.*

## สิ่งที่คุณควรเรียนต่อไปคืออะไร?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดซึ่งต่อยอดจากเทคนิคที่แสดงในคู่มือนี้. แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานครบถ้วนพร้อมคำอธิบายทีละขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานแบบอื่นในโครงการของคุณ.

- [ดึงข้อความจากรูปภาพด้วย Aspose OCR – คู่มือขั้นตอนโดยละเอียด](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [ดึงข้อความจากรูปภาพโดยใช้การทำงาน OCR บนโฟลเดอร์](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [ดึงข้อความจากรูปภาพ – การปรับแต่ง OCR ด้วย Aspose.OCR สำหรับ .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}