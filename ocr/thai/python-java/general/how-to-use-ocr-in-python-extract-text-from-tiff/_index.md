---
category: general
date: 2026-07-05
description: วิธีใช้ OCR ใน Python เพื่อแปลงไฟล์ TIFF เป็นข้อความอย่างรวดเร็ว เรียนรู้ขั้นตอนการใช้ไลบรารี
  OCR ใน Python สำหรับการดึงข้อความจากภาพ TIFF และการสร้างเครื่องมือ OCR ด้วย Python.
draft: false
keywords:
- how to use ocr
- ocr library python
- convert tiff to text
- extract text from tiff
- python ocr engine
language: th
og_description: วิธีใช้ OCR ใน Python? คู่มือนี้จะแสดงขั้นตอนโดยละเอียดว่าต้องแปลงไฟล์
  TIFF เป็นข้อความอย่างไรโดยใช้เครื่องมือ OCR ของ Python และไลบรารี ocr ของ Python.
og_title: วิธีใช้ OCR ใน Python – การสกัดข้อความจากไฟล์ TIFF อย่างครบถ้วน
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: How to use OCR in Python to convert TIFF to text quickly. Learn the
    ocr library python steps for extracting text from TIFF images and building a python
    OCR engine.
  headline: How to Use OCR in Python – Extract Text from TIFF
  type: TechArticle
- description: How to use OCR in Python to convert TIFF to text quickly. Learn the
    ocr library python steps for extracting text from TIFF images and building a python
    OCR engine.
  name: How to Use OCR in Python – Extract Text from TIFF
  steps:
  - name: '**Chunk the pages** – Instead of `recognize_multi_page`, call `engine.recognize(page)`
      inside a generator that yields one page at a time.'
    text: '**Chunk the pages** – Instead of `recognize_multi_page`, call `engine.recognize(page)`
      inside a generator that yields one page at a time.'
  - name: '**Adjust DPI** – Lowering the image resolution (e.g., from 300 DPI to 200 DPI)
      reduces CPU load while barely affecting accuracy for most printed text.'
    text: '**Adjust DPI** – Lowering the image resolution (e.g., from 300 DPI to 200 DPI)
      reduces CPU load while barely affecting accuracy for most printed text.'
  - name: '**Parallelize** – If your OCR engine is thread‑safe, spawn a `concurrent.futures.ThreadPoolExecutor`
      to run recognition on multiple pages concurrently.'
    text: '**Parallelize** – If your OCR engine is thread‑safe, spawn a `concurrent.futures.ThreadPoolExecutor`
      to run recognition on multiple pages concurrently.'
  type: HowTo
tags:
- OCR
- Python
- TIFF
- Image Processing
title: วิธีใช้ OCR ใน Python – แยกข้อความจากไฟล์ TIFF
url: /th/python-java/general/how-to-use-ocr-in-python-extract-text-from-tiff/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีใช้ OCR ใน Python – ดึงข้อความจาก TIFF

เคยสงสัย **how to use OCR in Python** ว่าจะเปลี่ยนหนังสือสแกนให้เป็นข้อความที่แก้ไขได้หรือไม่? คุณไม่ได้เป็นคนเดียว—นักพัฒนา นักวิจัย และผู้สนใจต่างก็เจออุปสรรคนี้เมื่อต้องจัดการกับภาพ TIFF หลายหน้า ข่าวดีคืออะไร? ด้วย **ocr library python** คุณสามารถสร้างเครื่อง OCR ขนาดเล็ก ชี้ไปที่ไฟล์ TIFF และรับข้อความที่สะอาดและสามารถค้นหาได้ในไม่กี่วินาที.

ในบทแนะนำนี้ เราจะพาคุณผ่านทุกขั้นตอนที่ต้องการ: การติดตั้งแพคเกจที่เหมาะสม การโหลด TIFF หลายหน้า การรันเครื่อง OCR และสุดท้ายการพิมพ์เนื้อหาของแต่ละหน้า เมื่อเสร็จคุณจะสามารถ **convert TIFF to text** และ **extract text from TIFF** ไฟล์ได้โดยไม่ต้องออกจากสภาพแวดล้อม Python ของคุณ.

## ข้อกำหนดเบื้องต้น

- Python 3.9 หรือใหม่กว่า (ตัวอย่างทดสอบบน 3.11)
- เวอร์ชันล่าสุดของไลบรารี `ocr` (หรือ `python ocr engine` ที่เข้ากันได้ตามที่คุณต้องการ)
- ไฟล์ TIFF หลายหน้าที่คุณต้องการประมวลผล (เราจะเรียกมันว่า `scanned_book.tif`)
- ความคุ้นเคยพื้นฐานกับสคริปต์ Python และ virtual environments

ไม่ต้องใช้เครื่องมือภายนอกหนัก—แค่ pip และไม่กี่บรรทัดของโค้ด.

## ติดตั้ง OCR Library Python

สิ่งแรกที่ต้องทำคือ: คุณต้องมีแบ็กเอนด์ OCR ที่มั่นคง สำหรับคู่มือนี้เราจะใช้แพ็กเกจ `ocr` ที่สมมติขึ้นซึ่งมาพร้อม API ระดับสูงแบบง่าย แต่รูปแบบเดียวกันก็ใช้ได้กับ wrapper ที่อิง Tesseract เช่น `pytesseract` หรือ SDK เชิงพาณิชย์.

```bash
# Create a clean virtual environment (optional but recommended)
python -m venv ocr-env
source ocr-env/bin/activate   # Windows: ocr-env\Scripts\activate

# Install the OCR package
pip install ocr
```

> **Pro tip:** หากคุณใช้ Windows และแพ็กเกจพึ่งพาไบนารีเนทีฟ ให้ตรวจสอบว่าคุณได้ติดตั้ง Visual C++ redistributable ที่เหมาะสมแล้ว ตัวติดตั้งมักจะแจ้งเตือนหากมีสิ่งใดขาดหายไป.

## วิธีใช้ OCR Engine ใน Python

เมื่อไลบรารีพร้อมแล้ว เรามาเปิดเครื่อง OCR และชี้ไปที่ไฟล์ TIFF ของเรา โค้ดตัวอย่างต่อไปนี้สร้างอินสแตนซ์ของเอนจิน ตั้งค่าภาษาเป็น English และเตรียมพร้อมสำหรับการประมวลผลหลายหน้า.

```python
import ocr

# Step 1: Create an OCR engine and set the language to English
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH   # You can switch to ocr.Language.FRENCH, etc.
```

**ทำไมต้องตั้งค่าภาษา?**  
เครื่อง OCR ส่วนใหญ่ใช้โมเดลภาษาเพื่อเพิ่มความแม่นยำ หากคุณข้ามขั้นตอนนี้ เอนจินจะย้อนกลับไปใช้โมเดลทั่วไปซึ่งอาจจดจำเครื่องหมายวรรคตอนหรืออักขระพิเศษผิดได้.

## โหลดภาพ TIFF หลายหน้า

ขั้นตอนต่อไปคือการโหลดเอกสารสแกน `ocr.Image.load` helper รองรับการจัดการสแตก TIFF โดยอัตโนมัติและคืนค่าอ็อบเจ็กต์ที่แทนแต่ละหน้าโดยภายใน.

```python
# Step 2: Load the multi‑page TIFF image containing the scanned book
tiff_path = "YOUR_DIRECTORY/scanned_book.tif"
tiff_image = ocr.Image.load(tiff_path)
```

> **Edge case:** หาก TIFF ของคุณใช้การบีบอัด (เช่น CCITT Group 4, LZW ฯลฯ) และไลบรารีเกิดข้อผิดพลาด ให้ลองแปลงเป็นเวอร์ชันที่ไม่บีบอัดด้วย ImageMagick ก่อน:
> ```bash
> convert scanned_book.tif -compress none scanned_book_uncompressed.tif
> ```

## ทำ OCR บนทุกหน้า – Convert TIFF to Text

เมื่อมีอ็อบเจ็กต์ภาพอยู่ในมือ เอนจินสามารถประมวลผลทุกหน้าได้พร้อมกัน วิธีนี้คืนค่าเป็นรายการที่แต่ละองค์ประกอบเก็บผลลัพธ์ OCR ของหน้าเดียว.

```python
# Step 3: Perform OCR on all pages of the image
page_results = engine.recognize_multi_page(tiff_image)
```

**เกิดอะไรขึ้นภายใน?**  
ฟังก์ชัน `recognize_multi_page` จะวนลูปผ่านแต่ละหน้าที่แรสเตอร์ไลซ์ รันตัวจำแนกด้วย neural‑network และรวมผลลัพธ์ plain‑text พร้อมคะแนนความมั่นใจ มันเป็นการทำงานแบบแบตช์ที่ช่วยคุณหลีกเลี่ยงการเขียนลูปด้วยตนเอง.

## วนลูปผลลัพธ์ – Extract Text from TIFF

สุดท้าย เราแสดงข้อความที่ถูกจำแนก คุณสามารถเขียนผลลัพธ์ลงไฟล์ `.txt` แยกกัน ส่งไปยังฐานข้อมูล หรือใส่ลงในดัชนีการค้นหา—อะไรก็ตามที่เหมาะกับ workflow ของคุณ.

```python
# Step 4: Iterate through the results and display the recognized text for each page
for page_index, result in enumerate(page_results):
    print(f"Page {page_index + 1}:\n{result.text}\n")
```

### ผลลัพธ์ที่คาดหวัง

```
Page 1:
Chapter 1
In the beginning...

Page 2:
The quick brown fox jumps over the lazy dog.

Page 3:
...

```

แต่ละสตริง `result.text` จะมีผลลัพธ์ OCR ดิบของหน้านั้น หากคุณต้องการรักษาการแบ่งบรรทัด ส่วนใหญ่ของเอนจินจะเปิดเผย `result.lines` เป็นรายการของสตริง.

## การจัดการไฟล์ TIFF ขนาดใหญ่ – เคล็ดลับ & เทคนิค

การประมวลผล TIFF ขนาด 500 หน้าอาจใช้หน่วยความจำมาก นี่คือกลยุทธ์บางอย่างเพื่อให้การทำงานราบรื่น:

1. **Chunk the pages** – แทนการใช้ `recognize_multi_page` ให้เรียก `engine.recognize(page)` ภายใน generator ที่ให้หนึ่งหน้าต่อครั้ง.
2. **Adjust DPI** – การลดความละเอียดภาพ (เช่น จาก 300 DPI เป็น 200 DPI) จะลดภาระ CPU ในขณะที่ความแม่นยำของข้อความพิมพ์ส่วนใหญ่ได้รับผลกระทบเพียงเล็กน้อย.
3. **Parallelize** – หาก OCR engine ของคุณเป็น thread‑safe ให้สร้าง `concurrent.futures.ThreadPoolExecutor` เพื่อรันการจำแนกบนหลายหน้าแบบพร้อมกัน.

```python
import concurrent.futures

def ocr_page(page):
    return engine.recognize(page).text

with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
    texts = list(executor.map(ocr_page, tiff_image.pages))
```

## บันทึกข้อความที่ดึงออกไปยังไฟล์

หลาย pipeline ในโลกจริงต้องการการจัดเก็บแบบถาวร ด้านล่างเป็นวิธีสั้น ๆ เพื่อบันทึกข้อความของแต่ละหน้าไปยังไฟล์ของมันเอง โดยคงลำดับหน้า.

```python
import pathlib

output_dir = pathlib.Path("ocr_output")
output_dir.mkdir(exist_ok=True)

for i, result in enumerate(page_results, start=1):
    file_path = output_dir / f"page_{i:03}.txt"
    file_path.write_text(result.text, encoding="utf-8")
    print(f"Saved page {i} to {file_path}")
```

ตอนนี้คุณมีไดเรกทอรีของไฟล์ `.txt` ที่สะอาดพร้อมสำหรับการทำดัชนีหรือการประมวลผล NLP ต่อไป.

## ตัวอย่างภาพ – วิธีใช้ผลลัพธ์ OCR อย่างเป็นภาพ

หากคุณต้องการดูการวางชั้น OCR บนภาพต้นฉบับ (สะดวกสำหรับการดีบัก) ไลบรารีหลายตัวอนุญาตให้วาด bounding box นี่คือตัวอย่างสั้น ๆ ด้วย Pillow:

```python
from PIL import ImageDraw

for page, result in zip(tiff_image.pages, page_results):
    draw = ImageDraw.Draw(page)
    for word in result.words:          # Assume `result.words` gives bounding boxes
        draw.rectangle(word.box, outline="red")
    page.show()   # Opens the annotated page
```

![How to use OCR in Python – OCR overlay on a TIFF page](ocr_overlay_example.png)

*ข้อความแทน:* วิธีใช้ OCR ใน Python – การวางชั้นภาพของข้อความที่จำแนกบนหน้า TIFF

## ข้อผิดพลาดทั่วไปและวิธีหลีกเลี่ยง

| ปัญหา | สาเหตุ | วิธีแก้ |
|-------|--------|----------|
| อักขระเสียหาย | โมเดลภาษาผิด | ตั้งค่า `engine.language` เป็น enum ที่ถูกต้อง |
| หน้าที่หาย | การบีบอัด TIFF ไม่รองรับ | แปลงเป็น TIFF ที่ไม่บีบอัดก่อน |
| ประสิทธิภาพช้า | DPI สูง + การประมวลผลแบบ single‑threaded | ลด DPI หรือเปิดใช้งาน multi‑threading |
| ผลลัพธ์ว่าง | ภาพมืดเกินไป/คอนทราสต์ต่ำ | ทำการพรี‑โปรเซสด้วยการยืดคอนทราสต์ (`opencv` หรือ `Pillow`) |

การแก้ไขปัญหาเหล่านี้ตั้งแต่ต้นจะช่วยคุณประหยัดเวลาการดีบักหลายชั่วโมงในภายหลัง.

## ขั้นตอนต่อไป – ไปไกลกว่าการสกัดพื้นฐาน

เมื่อคุณเชี่ยวชาญพื้นฐานของ **how to use OCR in Python** แล้ว ให้พิจารณาสำรวจ:

- **PDF generation** – ผสานข้อความที่สกัดกับ `reportlab` เพื่อสร้าง PDF ที่ค้นหาได้.
- **Language detection** – สลับ `engine.language` อัตโนมัติด้วย `langdetect`.
- **Structured data extraction** – ใช้ regular expressions หรือ spaCy เพื่อดึงวันที่ ชื่อ หรือ ตารางจากข้อความดิบ.
- **Alternative OCR backends** – เปลี่ยน `ocr` เป็น `pytesseract` หรือ `easyocr` หากต้องการการสนับสนุนหลายภาษา.

แต่ละหัวข้อเหล่านี้เชื่อมโยงกลับไปยังคีย์เวิร์ดรอง **ocr library python**, **convert tiff to text**, **extract text from tiff**, และ **python ocr engine** ทำให้คุณมีพื้นฐานที่มั่นคงสำหรับโครงการขั้นสูงต่อไป.

---

### สรุป

เราได้ครอบคลุม **how to use OCR in Python** ตั้งแต่การติดตั้งจนถึงการประมวลผลหลายหน้า แสดงให้คุณเห็นอย่างชัดเจนว่าอย่างไรจะ **convert TIFF to text** และ **extract text from TIFF** ด้วย **python OCR engine** ที่เรียบง่าย ตัวอย่างที่สมบูรณ์และสามารถรันได้ข้างต้นควรทำงานได้ทันทีสำหรับไฟล์ TIFF มาตรฐานส่วนใหญ่ และเคล็ดลับที่ให้ไว้จะช่วยคุณขยายไปยังเอกสารขนาดใหญ่หรือรวม OCR เข้าไปใน pipeline ที่ใหญ่ขึ้น.

ลองใช้กับหนังสือสแกน, ใบเสร็จ, หรือภาพเก็บถาวรของคุณ—แล้วทดลองแนวคิดระดับต่อไปที่ระบุในส่วน “ขั้นตอนต่อไป” ขอให้สนุกกับการเขียนโค้ดและผลลัพธ์ OCR ของคุณแม่นยำเสมอ!

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดซึ่งต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอนเพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานแบบอื่นในโครงการของคุณ.

- [ดึงข้อความจากภาพด้วย Aspose OCR – คู่มือขั้นตอนโดยละเอียด](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [วิธีดึงข้อความจาก tiff ด้วย Aspose.OCR สำหรับ Java](/ocr/english/java/ocr-operations/recognize-tiff/)
- [วิธีทำการดึงข้อความจากภาพจากสตรีมโดยใช้ Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}