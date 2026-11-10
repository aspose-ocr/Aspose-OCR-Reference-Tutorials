---
category: general
date: 2026-06-22
description: บทเรียน OCR แบบแบตช์ด้วย Python แสดงวิธีรัน OCR แบบหลายเธรดบนโฟลเดอร์ของภาพ
  PNG ด้วย Tesseract และ pathlib เรียนรู้การทำ OCR ภาพแบบแบตช์อย่างรวดเร็วใน Python.
draft: false
keywords:
- python batch ocr tutorial
- multithreaded OCR in Python
- tesseract OCR batch processing
- pathlib image handling
- OCR thread count optimization
language: th
og_description: บทเรียน python batch ocr พาคุณผ่านสคริปต์ที่สมบูรณ์และสามารถรันได้ซึ่งประมวลผล
  PNG จำนวนมากด้วย Tesseract โดยใช้หลายเธรด
og_title: บทเรียน OCR แบบแบตช์ด้วย Python – OCR แบบมัลติเทรดเร็วสำหรับภาพ PNG
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: python batch ocr tutorial showing how to run multithreaded OCR on a
    folder of PNG images using Tesseract and pathlib. Learn fast batch image OCR in
    Python.
  headline: 'python batch ocr tutorial: Process Multiple PNGs Efficiently'
  type: TechArticle
- description: python batch ocr tutorial showing how to run multithreaded OCR on a
    folder of PNG images using Tesseract and pathlib. Learn fast batch image OCR in
    Python.
  name: 'python batch ocr tutorial: Process Multiple PNGs Efficiently'
  steps:
  - name: '**Collects** every PNG with **pathlib image handling**.'
    text: '**Collects** every PNG with **pathlib image handling**.'
  - name: '**Spins up** a **multithreaded OCR in Python** worker pool.'
    text: '**Spins up** a **multithreaded OCR in Python** worker pool.'
  - name: '**Optimizes** the number of threads for your hardware (**OCR thread count
      optimization**).'
    text: '**Optimizes** the number of threads for your hardware (**OCR thread count
      optimization**).'
  - name: '**Writes** each result to a dedicated folder (**tesseract OCR batch processing**).'
    text: '**Writes** each result to a dedicated folder (**tesseract OCR batch processing**).'
  type: HowTo
tags:
- OCR
- Python
- Batch Processing
title: 'บทเรียน OCR แบบแบตช์ด้วย Python: ประมวลผล PNG หลายไฟล์อย่างมีประสิทธิภาพ'
url: /th/python-java/general/python-batch-ocr-tutorial-process-multiple-pngs-efficiently/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# python batch ocr tutorial – การ OCR แบบหลายเธรดเร็วสำหรับไฟล์ PNG

เคยสงสัยไหมว่า **python batch ocr tutorial** จะทำอย่างไรให้ผ่านรูป PNG จำนวนหลายร้อยรูปโดยไม่ทำให้ CPU ร้อนจนละลาย? คุณไม่ได้เป็นคนเดียว ไม่ว่าคุณจะกำลังแปลงฟอร์มสแกนเป็นดิจิทัล, ดึงข้อความจากใบเสร็จ, หรือสร้างคลังข้อมูลที่ค้นหาได้, การทำ pipeline OCR แบบ batch ที่มั่นคงจะช่วยคุณประหยัดเวลาหลายชั่วโมง

ในคู่มือนี้เราจะสร้างสคริปต์ขนาดเล็กแต่ทรงพลังที่รวบรวมไฟล์ `*.png` ทุกไฟล์ในโฟลเดอร์, ส่งต่อให้ Tesseract ผ่านตัวประมวลผลแบบหลายเธรด, แล้วบันทึกผลลัพธ์เป็นข้อความธรรมดาไปยังโฟลเดอร์ผลลัพธ์ที่เรียบร้อย ไม่ต้องพึ่งไลบรารีลับ—ใช้แค่ `pathlib`, `concurrent.futures`, และ `pytesseract` ที่เชื่อถือได้เสมอ เมื่อเสร็จแล้วคุณจะได้ **python batch ocr tutorial** ที่สามารถคัดลอก‑วางไปใช้ในโปรเจกต์ใดก็ได้

## สิ่งที่คุณจะได้เรียน

- วิธีรวบรวมไฟล์รูปภาพด้วย **pathlib image handling**  
- การตั้งค่า **multithreaded OCR in Python** worker pool  
- การปรับ **OCR thread count optimization** ให้เหมาะกับคอร์ CPU ของคุณ  
- การบันทึกผลลัพธ์แต่ละไฟล์ด้วยรูปแบบการตั้งชื่อที่ชัดเจนสำหรับการค้นหาในภายหลัง  
- การรันทั้งหมดเป็นสคริปต์เดียวที่ทำงานอิสระ  

## สิ่งที่ต้องเตรียมล่วงหน้า (Prerequisites)

| Requirement | Why It Matters |
|-------------|----------------|
| Python 3.9+ | ไวยากรณ์สมัยใหม่ (`pathlib`, f‑strings) |
| Tesseract 5.x installed and accessible in `PATH` | เครื่องมือ OCR ที่อยู่เบื้องหลัง `pytesseract` |
| `pytesseract` (`pip install pytesseract`) | ตัวห่อ Python สำหรับ Tesseract |
| `Pillow` (`pip install pillow`) | การโหลดภาพสำหรับ Tesseract |
| โฟลเดอร์ที่มีไฟล์ PNG ที่ต้องการประมวลผล | เป้าหมาย **tesseract OCR batch processing** ของเรา |

> **Pro tip:** หากคุณใช้ Windows, ให้เพิ่ม `C:\Program Files\Tesseract-OCR` ไปยัง `PATH` ของระบบ เพื่อให้ `pytesseract` หาไฟล์ปฏิบัติการได้โดยอัตโนมัติ

---

## ขั้นตอนที่ 1 – รวบรวมรูป PNG ทั้งหมด (Using pathlib)

สิ่งแรกที่ต้องทำคือสร้างรายการของรูปภาพทุกไฟล์ที่เราจะทำ OCR. `pathlib` ทำให้ขั้นตอนนี้เป็นบรรทัดเดียวและทำให้โค้ดเป็น OS‑agnostic

```python
import pathlib

# Adjust the path to point at your source folder
source_dir = pathlib.Path("YOUR_DIRECTORY/batch_images")
image_files = list(source_dir.glob("*.png"))

print(f"Found {len(image_files)} PNG files to process.")
```

*ทำไมต้องใช้ `pathlib`?* มันแยกความแตกต่างระหว่าง backslash ของ Windows กับ slash ของ Unix ออกไป ทำให้สคริปต์เดียวสามารถทำงานได้ทุกที่ นี่คือหัวใจของ **pathlib image handling** ในบทเรียนของเรา

---

## ขั้นตอนที่ 2 – สร้างคลาส Batch OCR Processor แบบง่าย

ด้านล่างเป็น wrapper ที่เบาและซ่อน boilerplate ของ threading. มันสอดคล้องกับ pseudo‑code ที่คุณเห็นก่อนหน้าแต่ทำงานได้เต็มรูปแบบ

```python
import concurrent.futures
import pytesseract
from PIL import Image
import os

class BatchOcrProcessor:
    """Encapsulates multithreaded OCR logic."""

    def __init__(self):
        self.thread_count = os.cpu_count() or 4  # sensible default
        self.output_folder = pathlib.Path("ocr_results")
        self.output_folder.mkdir(parents=True, exist_ok=True)

    def set_thread_count(self, count: int):
        """Adjust the number of worker threads (OCR thread count optimization)."""
        if count < 1:
            raise ValueError("Thread count must be at least 1")
        self.thread_count = count
        print(f"Thread pool size set to {self.thread_count}")

    def set_output_folder(self, folder: str):
        """Where each OCR result will be saved (tesseract OCR batch processing)."""
        self.output_folder = pathlib.Path(folder)
        self.output_folder.mkdir(parents=True, exist_ok=True)
        print(f"Output folder set to {self.output_folder}")

    def _process_single(self, image_path: pathlib.Path):
        """Run OCR on a single image and write the text file."""
        try:
            img = Image.open(image_path)
            text = pytesseract.image_to_string(img)
            out_file = self.output_folder / f"{image_path.stem}.txt"
            out_file.write_text(text, encoding="utf-8")
            return f"✅ {image_path.name} → {out_file.name}"
        except Exception as exc:
            return f"❌ {image_path.name} failed: {exc}"

    def process(self, image_paths):
        """Run OCR on the entire batch using a thread pool."""
        print("🚀 Starting batch OCR...")
        with concurrent.futures.ThreadPoolExecutor(max_workers=self.thread_count) as executor:
            results = list(executor.map(self._process_single, image_paths))
        for line in results:
            print(line)
        print("🏁 Batch OCR completed.")
```

**คำอธิบายตัวเลือกสำคัญ**

- **ThreadPoolExecutor** ให้เราได้การทำงานหลายเธรดจริงสำหรับงานที่ I/O‑bound เช่น การอ่านไฟล์และเรียกไบนารี Tesseract ภายนอก  
- เมธอด `set_thread_count` คือที่ที่คุณสามารถทดลอง **OCR thread count optimization**; เพิ่มเธรดมักทำให้ความเร็วเพิ่มขึ้นจนถึงจุดที่คอร์ CPU ถูกใช้เต็มที่  
- แต่ละรูปจะสร้างไฟล์ `.txt` ที่มีชื่อเดียวกับ PNG ต้นฉบับ—เหมาะสำหรับการทำดัชนีหรือการค้นหาในภายหลัง  

---

## ขั้นตอนที่ 3 – เชื่อมต่อทุกอย่างเข้าด้วยกัน

ตอนนี้เราจะสร้างอินสแตนซ์ของ processor, ปรับจำนวนเธรด, ระบุโฟลเดอร์ผลลัพธ์, แล้วส่งรายการรูปภาพให้มันทำงาน

```python
if __name__ == "__main__":
    # 1️⃣ Gather PNGs (already done above)
    # 2️⃣ Create processor instance
    ocr_processor = BatchOcrProcessor()

    # 3️⃣ Configure thread pool – feel free to change 8 → your core count
    ocr_processor.set_thread_count(8)   # multithreaded OCR in Python

    # 4️⃣ Choose where results land
    ocr_processor.set_output_folder("YOUR_DIRECTORY/ocr_results")

    # 5️⃣ Run the batch – this call blocks until everything is done
    ocr_processor.process(image_files)

    # 6️⃣ All done – a friendly console message
    print("✅ All images processed. Check the ocr_results folder.")
```

เมื่อรันสคริปต์จะได้ผลลัพธ์คล้ายกับ:

```
Found 42 PNG files to process.
Thread pool size set to 8
Output folder set to YOUR_DIRECTORY/ocr_results
🚀 Starting batch OCR...
✅ invoice_001.png → invoice_001.txt
✅ receipt_2023-04-15.png → receipt_2023-04-15.txt
...
🏁 Batch OCR completed.
✅ All images processed. Check the ocr_results folder.
```

แต่ละไฟล์ `.txt` จะมีผลลัพธ์ OCR ดิบ เปิดไฟล์ใดก็จะเห็นข้อความที่สกัดออกมา พร้อมสำหรับการทำดัชนี, วิเคราะห์อารมณ์, หรือขั้นตอนต่อไปที่คุณต้องการ

---

## ขั้นตอนที่ 4 – ปัญหาที่พบบ่อยและวิธีหลีกเลี่ยง

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| ไฟล์ `.txt` ว่างเปล่า | Tesseract ไม่พบข้อมูลภาษา หรือรูปภาพมืดเกินไป | ติดตั้ง language pack (`tesseract-ocr-eng`) และทำการ preprocess ภาพ (เพิ่มความคอนทราสต์) |
| `UnicodeDecodeError` ขณะอ่านผลลัพธ์ | ผลลัพธ์มีอักขระที่ไม่ใช่ UTF‑8 | เขียนไฟล์ด้วย `encoding="utf-8"` (โค้ดมีแล้ว) หรือใช้ `errors="ignore"` เป็นวิธีแก้ชั่วคราว |
| CPU พุ่งสูง แต่ไม่มีความเร็วเพิ่ม | จำนวนเธรดเกินคอร์จริง | ลด `set_thread_count` ให้เท่ากับ `os.cpu_count()` หรือใต้มัน |
| `FileNotFoundError` ขณะเปิดภาพ | พาธมีอักขระ non‑ASCII บน Windows | ใส่ prefix `r` ก่อนสตริง หรือใช้วัตถุ `pathlib` ตรง (เช่นที่ทำ) |

---

## ขั้นตอนที่ 5 – ขยายบทเรียน (Next Steps)

- **เพิ่มการ preprocess ภาพ** ด้วย OpenCV (`cv2`) เพื่อเพิ่มความแม่นยำของ OCR (เช่น deskew, threshold)  
- **ทำ parallelization ข้ามเครื่อง** ด้วย `multiprocessing` หรือคิวงานอย่าง RabbitMQ สำหรับงานขนาดใหญ่  
- **เชื่อมต่อกับเครื่องมือค้นหา** (Elasticsearch) เพื่อทำให้ข้อความที่สกัดได้ searchable แบบเรียลไทม์  
- **สลับ Tesseract ไปใช้ Cloud OCR API** (Google Vision, Azure Computer Vision) หากต้องการความแม่นยำสูงขึ้นสำหรับข้อความมือเขียน  

ทั้งหมดนี้ต่อยอดจากพื้นฐานที่คุณมีแล้ว: **python batch ocr tutorial** ที่ทำงานได้ทันที

---

## สรุป

คุณเพิ่งสร้าง **python batch ocr tutorial** ครบวงจรที่:

1. **รวบรวม** ทุก PNG ด้วย **pathlib image handling**  
2. **สร้าง** **multithreaded OCR in Python** worker pool  
3. **ปรับ** จำนวนเธรดให้เหมาะกับฮาร์ดแวร์ของคุณ (**OCR thread count optimization**)  
4. **บันทึก** ผลลัพธ์แต่ละไฟล์ลงในโฟลเดอร์เฉพาะ (**tesseract OCR batch processing**)  

สคริปต์พร้อมใส่ลงใน pipeline ใดก็ได้ ไม่ว่าจะเป็นการประมวลผลใบเสร็จ, เอกสารกฎหมาย, หรือกองภาพหน้าจอจำนวนมหาศาล ปรับจำนวนเธรด, เพิ่มการ preprocess ภาพ, หรือเชื่อมต่อผลลัพธ์กับฐานข้อมูล—ทั้งหมดขึ้นกับคุณ

มีคำถาม? แสดงความคิดเห็นด้านล่างได้เลย, ขอให้สนุกกับการเขียนโค้ด!

![Workflow diagram of python batch ocr tutorial processing multiple PNG files in parallel](/images/python-batch-ocr-workflow.png){.center width=600 alt="แผนภาพการทำงานของ python batch ocr tutorial ที่ประมวลผลไฟล์ PNG หลายไฟล์พร้อมกัน"}

---


## สิ่งที่คุณควรเรียนต่อไป


บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโปรเจกต์ของคุณ

- [Aspose OCR Tutorial – Optical Character Recognition](/ocr/english/)
- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}