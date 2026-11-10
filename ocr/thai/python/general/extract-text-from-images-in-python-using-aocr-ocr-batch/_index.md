---
category: general
date: 2026-06-25
description: สกัดข้อความจากภาพด้วยไลบรารี Python aocr – เรียนรู้การทำ OCR แบบแบตช์,
  ตั้งค่าโหมดการจดจำเป็นแบบพิมพ์, และเพิ่มตัวประมวลผลหลังด้วย AI.
draft: false
keywords:
- extract text from images
- Python OCR batch
- aocr library
- recognition mode printed
- AI postprocessor
language: th
og_description: ดึงข้อความจากรูปภาพโดยใช้ไลบรารี Python aocr. บทเรียนนี้แสดงการทำ
  OCR แบบเป็นชุด, โหมดการจดจำข้อความพิมพ์, และตัวประมวลผลหลัง AI ที่เป็นตัวเลือก.
og_title: ดึงข้อความจากรูปภาพด้วย Python – คู่มือการทำ Batch aocr อย่างครบถ้วน
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Extract text from images with Python aocr library – learn batch OCR,
    set recognition mode printed, and add an AI postprocessor.
  headline: Extract Text from Images in Python Using aocr OCR Batch
  type: TechArticle
- description: Extract text from images with Python aocr library – learn batch OCR,
    set recognition mode printed, and add an AI postprocessor.
  name: Extract Text from Images in Python Using aocr OCR Batch
  steps:
  - name: Prerequisites
    text: '- Python 3.8 or newer installed on your machine. - Basic familiarity with
      Python scripting (loops, imports, etc.). - Access to a folder of scanned images
      (PNG, JPG, TIFF, etc.).'
  - name: 1. Unsupported File Types
    text: '`aocr` silently skips files it can’t decode. If you suspect you have PDFs
      or BMPs mixed in, filter them beforehand:'
  - name: 2. Large Batches and Memory Consumption
    text: 'Running thousands of high‑resolution scans can balloon memory usage. Mitigate
      this by processing in chunks:'
  - name: 3. Empty or Low‑Contrast Pages
    text: 'If a page yields fewer than 10 characters, you might want to flag it for
      manual review:'
  type: HowTo
- questions:
  - answer: Not out‑of‑the‑box. `aocr` only handles raster images. Convert PDFs to
      PNG/TIFF first (e.g., using `pdf2image`).
    question: Does this work on PDFs?
  - answer: Absolutely—just replace `aocr.RecognitionMode.PRINTED` with `aocr.RecognitionMode.HANDWRITTEN`.
      Expect a slower run time but better results on cursive notes.
    question: Can I change the recognition mode to handwritten?
  - answer: 'The library ships with language packs. Install the desired language module
      (`pip install aocr-lang-fr` for French, etc.) and set `ocr_batch.language =
      "fr"` before running. ## Next Steps and Related Topics - **Parallel processing:**
      Wrap the batch execution in a `concurrent.futures.ThreadPoolExecuto'
    question: What if I need multilingual support?
  type: FAQPage
tags:
- OCR
- Python
- image processing
title: ดึงข้อความจากภาพใน Python ด้วย aocr OCR Batch
url: /th/python/general/extract-text-from-images-in-python-using-aocr-ocr-batch/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สกัดข้อความจากภาพใน Python ด้วย aocr OCR Batch

เคยต้องการ **สกัดข้อความจากภาพ** แต่รู้สึกท่วมท้นกับขั้นตอนเล็ก ๆ หลายสิบขั้นตอนหรือไม่? คุณไม่ได้เป็นคนเดียว ไม่ว่าคุณจะกำลังดิจิไทซ์แบบฟอร์มที่สแกน, ดึงข้อมูลจากใบเสร็จ, หรือสร้างคลังข้อมูลที่ค้นหาได้ การได้ผลลัพธ์ OCR ที่เชื่อถือได้ในปริมาณมากอาจรู้สึกเหมือนการปีนเขาที่ชัน

ข่าวดีคืออะไร? ด้วย **aocr library** คุณสามารถสร้าง **Python OCR batch** ครบวงจรได้ในเพียงไม่กี่บรรทัด ในคู่มือนี้เราจะพาคุณผ่านการสร้าง OCR batch, โหลดรูปภาพที่รองรับทั้งหมดจากโฟลเดอร์, เลือก **recognition mode printed** ที่เหมาะสม, และแม้กระทั่งผนวก **AI postprocessor** เพื่อเพิ่มความแม่นยำให้ดียิ่งขึ้น เมื่อเสร็จสิ้นคุณจะมีสคริปต์พร้อมรันที่สกัดข้อความจากภาพและบอกคุณว่ามีข้อความกี่ตัวอักษรที่จับได้ต่อไฟล์

## สิ่งที่คุณจะได้เรียนรู้

- วิธีติดตั้งและนำเข้าแพคเกจ `aocr`
- การตั้งค่า `OcrBatch` เพื่อจัดการไฟล์หลายพันไฟล์โดยอัตโนมัติ
- การเลือกโหมดการจดจำที่เหมาะสมสำหรับเอกสารพิมพ์
- (ทางเลือก) การเชื่อมต่อ AI post‑processor เพื่อทำความสะอาดผลลัพธ์ที่มีเสียงรบกวน
- การแสดงเส้นทางไฟล์พร้อมความยาวของข้อความที่สกัดได้
- เคล็ดลับการจัดการกรณีขอบเช่นรูปแบบที่ไม่รองรับหรือหน้าว่าง

### ข้อกำหนดเบื้องต้น

- Python 3.8 หรือใหม่กว่า ติดตั้งบนเครื่องของคุณ  
- ความคุ้นเคยพื้นฐานกับการเขียนสคริปต์ Python (ลูป, import, ฯลฯ)  
- มีโฟลเดอร์ที่บรรจุภาพสแกน (PNG, JPG, TIFF, ฯลฯ)  

ถ้าคุณมีทั้งหมดนี้แล้ว มาเริ่มกันเลย—ไม่ต้องพึ่งบริการภายนอก

## ขั้นตอนที่ 1: ติดตั้ง aocr Library

สิ่งแรกที่ต้องทำ `aocr` ไม่ได้เป็นส่วนหนึ่งของไลบรารีมาตรฐาน ดังนั้นคุณต้องดึงมาจาก PyPI

```bash
pip install aocr
```

> **เคล็ดลับ:** ใช้ virtual environment (`python -m venv .venv`) เพื่อแยกการพึ่งพาออกจากระบบ  

เมื่อติดตั้งเสร็จแล้ว คุณสามารถ import คลาสหลักได้

```python
# core imports
import aocr
```

## ขั้นตอนที่ 2: สร้างอินสแตนซ์ OCR Batch

`OcrBatch` คือเครื่องจักรหลักที่จะสำรวจไดเรกทอรีของคุณและติดตามไฟล์ภาพทุกไฟล์ คิดว่าเป็นสายพานลำเลียงที่ส่งรูปภาพเข้าสู่เอนจิน OCR

```python
# Step 2: Initialize the batch
ocr_batch = aocr.OcrBatch()
```

ในตอนนี้ batch ยังว่างเปล่า เราจะเติมข้อมูลในขั้นตอนต่อไป

## ขั้นตอนที่ 3: เพิ่มรูปภาพที่รองรับทั้งหมดจากโฟลเดอร์ (แบบ Recursively)

คุณอาจมีโครงสร้างโฟลเดอร์หลายระดับ—อาจเป็นโฟลเดอร์ย่อยต่อคลายเอนต์หรือต่อเดือน `add_folder` จะเดินสำรวจต้นไม้ให้คุณและดึงรูปภาพทุกไฟล์ที่สามารถอ่านได้

```python
# Step 3: Load images from a directory
ocr_batch.add_folder("YOUR_DIRECTORY/scanned_forms/", recursive=True)
```

เปลี่ยน `"YOUR_DIRECTORY/scanned_forms/"` ให้เป็นพาธจริงบนระบบของคุณ หลังจากเรียกนี้ `ocr_batch.file_paths` จะเป็นรายการของชื่อไฟล์แบบ absolute และ batch จะรู้จำนวนรายการที่ต้องประมวลผลทั้งหมด

## ขั้นตอนที่ 4: เลือกโหมดการจดจำสำหรับข้อความพิมพ์

เอนจิน `aocr` รองรับหลายโหมด (handwritten, printed, mixed) เนื่องจากเรากำลังจัดการแบบฟอร์มพิมพ์ที่สะอาด จึงตั้งค่าโหมดให้สอดคล้อง โฟลกนี้สามารถเพิ่มความแม่นยำอย่างมาก เพราะเอนจินจะข้าม heuristic ที่ซับซ้อนสำหรับสคริปต์ลายมือ

```python
# Step 4: Tell the engine we have printed text
ocr_batch.recognition_mode = aocr.RecognitionMode.PRINTED
```

> **ทำไมถึงสำคัญ:** ข้อความพิมพ์มี baseline และรูปแบบอักษรคงที่ ทำให้โมเดล OCR ใช้พจนานุกรมอักขระที่แคบลง หากคุณปล่อยโหมดเป็น “auto” อาจเจอเสียงรบกวนจากสแกนความละเอียดต่ำ

## ขั้นตอนที่ 5: (ทางเลือก) ผนวก AI Post‑Processor

หากสแกนของคุณมีเบลอ, คอนทราสต์ต่ำ, หรือฟอนต์แปลก AI post‑processor สามารถทำความสะอาดผลลัพธ์ OCR ดิบก่อนส่งต่อไปยังระบบต่อไป `set_ai_postprocessor` ต้องการอ็อบเจ็กต์ที่มีเมธอด `process(text: str) -> str`

ด้านล่างเป็นตัวอย่างขั้นต่ำโดยใช้คลาสสมมติ `SimpleCleaner` ในการใช้งานจริงคุณอาจเชื่อมต่อ HuggingFace transformer, โมเดลภาษาแบบกำหนดเอง, หรือแม้กระทั่ง spell‑checker แบบ rule‑based

```python
# Optional Step 5: Define a tiny post‑processor
class SimpleCleaner:
    def process(self, text: str) -> str:
        # Strip extra whitespace and fix common OCR quirks
        cleaned = " ".join(text.split())
        return cleaned.replace("—", "-")  # replace em‑dash with hyphen

# Instantiate and attach
ai = SimpleCleaner()
ocr_batch.set_ai_postprocessor(ai)
```

ถ้าข้ามขั้นตอนนี้ batch จะคืนค่า OCR ดิบโดยตรง

## ขั้นตอนที่ 6: รัน OCR บน Batch ทั้งหมดและเก็บผลลัพธ์

ตอนนี้งานหนักเริ่มขึ้นแล้ว เมธอด `run` จะวนลูปทุกไฟล์, รันเอนจิน OCR, ส่งผลลัพธ์ผ่าน AI post‑processor (ถ้ามี) และคืนรายการสตริง—หนึ่งรายการต่อหนึ่งภาพ

```python
# Step 6: Execute the batch
ocr_results = ocr_batch.run()   # list of extracted texts
```

เพราะเมธอดคืนค่าเป็น Python list ธรรมดา คุณจึงสามารถจัดการเหมือนคอลเลกชันอื่น ๆ—เก็บไว้, เขียนเป็น CSV, หรือใส่ลงฐานข้อมูล

## ขั้นตอนที่ 7: แสดงเส้นทางไฟล์พร้อมความยาวของข้อความที่สกัดได้

การตรวจสอบอย่างเร็วคือพิมพ์จำนวนอักขระที่สกัดจากแต่ละไฟล์ หากหน้าว่างหรือ OCR ล้มเหลว คุณจะเห็นความยาวเป็น `0`

```python
# Step 7: Show results summary
for file_path, text in zip(ocr_batch.file_paths, ocr_results):
    print(f"{file_path} -> {len(text)} chars")
```

ผลลัพธ์ทั่วไปอาจเป็นเช่นนี้:

```
/data/forms/invoice_001.png -> 1245 chars
/data/forms/invoice_002.jpg -> 0 chars
/data/forms/receipt_2023-04-15.tif -> 876 chars
```

การเห็นค่า `0` จะบ่งบอกไฟล์ใดต้องตรวจสอบอีกครั้ง (อาจเสียหายหรือไม่ใช่ภาพเลย)

## การจัดการกรณีขอบทั่วไป

### 1. ไฟล์ประเภทที่ไม่รองรับ

`aocr` จะข้ามไฟล์ที่ไม่สามารถถอดรหัสได้อย่างเงียบ หากคุณสงสัยว่ามี PDF หรือ BMP ปะปนอยู่ ให้กรองก่อน:

```python
supported_ext = {".png", ".jpg", ".jpeg", ".tif", ".tiff"}
ocr_batch.file_paths = [
    p for p in ocr_batch.file_paths if p.lower().endswith(tuple(supported_ext))
]
```

### 2. Batch ขนาดใหญ่และการใช้หน่วยความจำ

การประมวลผลสแกนความละเอียดสูงหลายพันไฟล์อาจทำให้หน่วยความจำพุ่งสูง ลดผลกระทบโดยประมวลผลเป็นชิ้นย่อย:

```python
batch_size = 200
for i in range(0, len(ocr_batch.file_paths), batch_size):
    sub_batch = aocr.OcrBatch()
    sub_batch.file_paths = ocr_batch.file_paths[i:i+batch_size]
    sub_batch.recognition_mode = aocr.RecognitionMode.PRINTED
    if 'ai' in locals():
        sub_batch.set_ai_postprocessor(ai)
    results = sub_batch.run()
    # handle results (e.g., write to file) before next chunk
```

### 3. หน้าเปล่าหรือคอนทราสต์ต่ำ

หากหน้าหนึ่งให้ตัวอักษรน้อยกว่า 10 ตัว คุณอาจต้องทำเครื่องหมายให้ตรวจสอบด้วยมือ:

```python
for fp, txt in zip(ocr_batch.file_paths, ocr_results):
    if len(txt.strip()) < 10:
        print(f"⚠️  Low‑confidence result for {fp}")
```

## ตัวอย่างทำงานเต็มรูปแบบ

รวมทุกขั้นตอนเข้าด้วยกัน นี่คือสคริปต์ที่คุณสามารถคัดลอก‑วางและรันได้ทันที บันทึกเป็น `batch_ocr.py`

```python
#!/usr/bin/env python3
"""
Batch OCR script using aocr to extract text from images.
"""

import aocr

# ----------------------------------------------------------------------
# Optional: a tiny AI post‑processor to clean up OCR output
# ----------------------------------------------------------------------
class SimpleCleaner:
    def process(self, text: str) -> str:
        cleaned = " ".join(text.split())
        return cleaned.replace("—", "-")

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
IMAGE_ROOT = "YOUR_DIRECTORY/scanned_forms/"   # ← change this!
RECOGNITION_MODE = aocr.RecognitionMode.PRINTED

# ----------------------------------------------------------------------
# Build and run the OCR batch
# ----------------------------------------------------------------------
def main():
    # 1️⃣ Create batch
    batch = aocr.OcrBatch()

    # 2️⃣ Load images recursively
    batch.add_folder(IMAGE_ROOT, recursive=True)

    # 3️⃣ Set mode for printed text
    batch.recognition_mode = RECOGNITION_MODE

    # 4️⃣ Attach AI post‑processor (comment out if not needed)
    ai = SimpleCleaner()
    batch.set_ai_postprocessor(ai)

    # 5️⃣ Run OCR
    results = batch.run()

    # 6️⃣ Summarize
    for path, text in zip(batch.file_paths, results):
        print(f"{path} -> {len(text)} chars")

if __name__ == "__main__":
    main()
```

**ผลลัพธ์ที่คาดหวัง** (ตัดบางส่วนเพื่อความกระชับ):

```
/home/me/scanned_forms/formA.png -> 1342 chars
/home/me/scanned_forms/subfolder/formB.tif -> 0 chars
/home/me/scanned_forms/invoice_2024-01.jpg -> 987 chars
```

รันด้วยคำสั่ง:

```bash
python batch_ocr.py
```

หากทุกอย่างตั้งค่าอย่างถูกต้อง คุณจะเห็นบรรทัดสำหรับทุกภาพ พร้อมรายงานจำนวนอักขระของข้อความที่สกัดได้

## คำถามที่พบบ่อย

**Q: ทำงานกับ PDF ได้หรือไม่?**  
A: ไม่ได้โดยตรง `aocr` รองรับเฉพาะภาพ raster เท่านั้น ให้แปลง PDF เป็น PNG/TIFF ก่อน (เช่นใช้ `pdf2image`)

**Q: สามารถเปลี่ยนโหมดการจดจำเป็น handwritten ได้หรือไม่?**  
A: แน่นอน—เปลี่ยน `aocr.RecognitionMode.PRINTED` เป็น `aocr.RecognitionMode.HANDWRITTEN` จะใช้เวลานานกว่าแต่ให้ผลลัพธ์ดีกับโน้ตลายมือ

**Q: หากต้องการรองรับหลายภาษา ทำอย่างไร?**  
A: ไลบรารีมาพร้อม language pack ติดตั้งโมดูลภาษาที่ต้องการ (`pip install aocr-lang-fr` สำหรับฝรั่งเศส ฯลฯ) แล้วตั้ง `ocr_batch.language = "fr"` ก่อนรัน

## ขั้นตอนต่อไปและหัวข้อที่เกี่ยวข้อง

- **การประมวลผลแบบขนาน:** ห่อการทำงานของ batch ด้วย `concurrent.futures.ThreadPoolExecutor` เพื่อใช้หลายคอร์ CPU  
- **การเก็บผลลัพธ์:** เขียน `ocr_results` ลง CSV หรือ SQLite สำหรับการวิเคราะห์ต่อเนื่อง  
- **การผสานกับ Cloud AI:** แทนที่ `SimpleCleaner` ด้วยโมเดล transformer จาก HuggingFace เพื่อการแก้ไขการสะกดที่ล้ำสมัย  
- **Fine‑tuning aocr:** หากคุณมีชุดฟอนต์เฉพาะของตนเอง ให้สำรวจ `aocr.Trainer` เพื่อปรับปรุงความแม่นยำในโหมด printed  

---

นั่นแหละ—คุณมีพื้นฐานที่มั่นคงแล้ว


## สิ่งที่คุณควรเรียนต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอน‑โดย‑ขั้นตอน เพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการนำไปใช้แบบต่าง ๆ ในโปรเจกต์ของคุณ

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}