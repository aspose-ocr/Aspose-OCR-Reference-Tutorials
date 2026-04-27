---
category: general
date: 2026-04-26
description: วิธีใช้ OCR กับ PDF ที่สแกน, ดึงข้อความจาก PDF, ทำ OCR บน PDF, และแปลง
  PDF ที่สแกนให้เป็นไฟล์ที่สามารถค้นหาได้ในไม่กี่ขั้นตอน.
draft: false
keywords:
- how to use OCR
- extract text from pdf
- run OCR on pdf
- convert scanned pdf
- load pdf as image
language: th
og_description: 'วิธีใช้ OCR ใน Python: เรียนรู้วิธีดึงข้อความจาก PDF, ทำ OCR บน PDF,
  และแปลง PDF สแกนให้เป็นเอกสารที่สามารถค้นหาได้.'
og_title: วิธีใช้ OCR – คู่มือด่วนสำหรับการดึงข้อความจาก PDF
tags:
- OCR
- Python
- PDF
- Text Extraction
title: วิธีใช้ OCR – ดึงข้อความจาก PDF ด้วย Python
url: /th/python-java/general/how-to-use-ocr-extract-text-from-pdf-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีใช้ OCR – ดึงข้อความจาก PDF ด้วย Python

เคยสงสัย **how to use OCR** ว่าจะดึงข้อความจากสัญญาที่สแกน, ใบเสร็จ, หรือ ebook อย่างไรไหม? คุณไม่ได้เป็นคนเดียว ในหลายโครงการจริง ๆ PDF ที่คุณได้รับเป็นเพียงภาพเท่านั้น, และหากไม่มี OCR คุณจะไม่สามารถค้นหา, ทำดัชนี, หรือวิเคราะห์เนื้อหาได้  

ในบทแนะนำนี้เราจะเดินผ่านตัวอย่างที่สมบูรณ์และสามารถรันได้ซึ่งแสดง **how to use OCR**, วิธี **extract text from PDF**, และเหตุผลที่คุณอาจต้องการ **convert scanned PDF** ไฟล์ให้เป็นเอกสารที่สามารถค้นหาได้ เราจะครอบคลุมศิลปะที่ละเอียดอ่อนของ **loading PDF as image** เพื่อให้เครื่อง OCR มองเห็นทุกหน้าอย่างชัดเจน

> **Quick preview:** เมื่อจบคุณจะมีสคริปต์ที่โหลด PDF หลายหน้า, รัน OCR บนแต่ละหน้า, และพิมพ์ข้อความที่ถูกจดจำ – ไม่ต้องใช้บริการภายนอก

## สิ่งที่คุณต้องการ

- Python 3.9+ (เวอร์ชันล่าสุดใดก็ได้ที่ทำงานได้)
- `aocr` package (หรือไลบรารี OCR ที่เข้ากันได้ซึ่งให้ `OcrEngine` และ `Image.load`)
- ไฟล์ PDF ที่สแกนที่คุณต้องการประมวลผล (เช่น `contract.pdf`)
- RAM ปริมาณพอสมควร (≈ 200 MB ต่อ PDF 100 หน้าโดยทั่วไปก็พอใช้)

หากคุณยังไม่ได้ติดตั้งไลบรารี OCR, ให้รัน:

```bash
pip install aocr
```

> **Pro tip:** ใช้ virtual environment เพื่อจัดการ dependencies ให้เป็นระเบียบ

## ขั้นตอนที่ 1: Load PDF as Image – ส่วนแรกของปริศนา

ก่อนที่ OCR จะทำงาน, PDF ต้องถูกแปลงเป็นภาพ นี่คือจุดที่คีย์เวิร์ดรอง **load pdf as image** เข้ามามีบทบาท

```python
# Step 1: Create an OCR engine instance
ocr_engine = OcrEngine()

# Step 2: Load the PDF file as a multi‑page image
ocr_engine.image = aocr.Image.load("YOUR_DIRECTORY/contract.pdf")
```

*ทำไมเรื่องนี้สำคัญ:* `aocr.Image.load` จะทำการแรสเตอร์แต่ละหน้าของ PDF เป็นบิตแมปที่เครื่อง OCR เข้าใจ หากคุณข้ามขั้นตอนนี้และส่ง PDF ดิบเข้าไป, เครื่องจะเกิดข้อผิดพลาดเพราะคาดหวังข้อมูลพิกเซล ไม่ใช่ข้อมูลเวกเตอร์

> **Note:** เส้นทางสามารถเป็นแบบ absolute หรือ relative ได้ ตรวจสอบให้ไฟล์สามารถอ่านได้; หากไม่เช่นนั้นคุณจะเจอ `FileNotFoundError`.

## ขั้นตอนที่ 2: Run OCR on PDF – แปลงพิกเซลเป็นอักขระ

เมื่อ PDF อยู่ในรูปภาพแล้ว, เราสามารถ **run OCR on PDF** ได้ในที่สุด โค้ดต่อไปนี้จะประมวลผลทุกหน้าในครั้งเดียว:

```python
# Step 3: Run OCR on every page of the document
page_results = ocr_engine.process_all_pages()
```

*อะไรที่เกิดขึ้นภายใน?* `process_all_pages` จะวนลูปผ่านหน้าที่แรสเตอร์, ใช้โมเดล OCR, และคืนค่าเป็นรายการของอ็อบเจกต์ผลลัพธ์—หนึ่งต่อหนึ่งหน้า แต่ละผลลัพธ์มีข้อความที่จดจำได้, คะแนนความมั่นใจ, และกล่องขอบเขต (หากคุณต้องการใช้ต่อไป)

## ขั้นตอนที่ 3: Extract Text from PDF – ดึงข้อความออกมา

เมื่อมีผลลัพธ์ OCR อยู่ในมือ, การดึงข้อความธรรมดากลายเป็นเรื่องง่าย เราจะวนลูปผ่านหน้าและพิมพ์ผลลัพธ์, แสดงคีย์เวิร์ดรอง **extract text from pdf**

```python
# Step 4: Iterate through the results and output the recognized text
for page_number, page_result in enumerate(page_results, start=1):
    print(f"--- Page {page_number} ---")
    print(page_result.text)
```

**ผลลัพธ์ที่คาดหวัง** (ตัดทอนเพื่อความกระชับ):

```
--- Page 1 ---
This Agreement is made on the 1st day of January...
--- Page 2 ---
Section 2.1: Definitions...
```

หากคุณต้องการข้อความเป็นสตริงเดียว, เพียงแค่ต่อกัน:

```python
full_text = "\n".join(r.text for r in page_results)
```

ตอนนี้คุณได้ **extracted text from PDF** ด้วย OCR อย่างสำเร็จแล้ว

## ขั้นตอนที่ 4: Convert Scanned PDF – ทำให้สามารถค้นหาได้

เครื่องมือ downstream หลายตัว (เช่น Elasticsearch หรือ SharePoint) คาดหวัง PDF ที่สามารถค้นหาได้ ไม่ใช่แค่ dump ของข้อความธรรมดา คุณสามารถฝังผลลัพธ์ OCR กลับเข้าไปใน PDF ดั้งเดิม, ทำให้ **convert scanned PDF** เป็นเวอร์ชันที่สามารถค้นหาได้

```python
# Optional: Create a searchable PDF
searchable_pdf_path = "YOUR_DIRECTORY/contract_searchable.pdf"
ocr_engine.save_searchable_pdf(searchable_pdf_path)
print(f"Searchable PDF saved to {searchable_pdf_path}")
```

*ทำไมต้องทำ?* PDF ที่สามารถค้นหาได้จะรักษาเลย์เอาต์และภาพเดิมไว้พร้อมกับให้สามารถเลือกข้อความและทำดัชนีได้ — เป็นประโยชน์ทั้งสำหรับมนุษย์และเครื่อง

## ปัญหาที่พบบ่อย & กรณีขอบ

### PDF หลายหน้าใหญ่เกินหน่วยความจำ

หาก PDF ของคุณมีหลายร้อยหน้า, การโหลดทั้งหมดพร้อมกันอาจทำให้ RAM หมด `aocr` library รองรับการโหลดแบบ lazy:

```python
ocr_engine.image = aocr.Image.load("bigfile.pdf", lazy=True)
```

แล้วประมวลผลหน้าแบบทีละหน้า:

```python
for page in ocr_engine.image.iter_pages():
    result = ocr_engine.process_page(page)
    print(result.text)
```

### สแกนคุณภาพต่ำ

ความแม่นยำของ OCR ลดลงอย่างมากเมื่อสแกนเบลอหรือคอนทราสต์ต่ำ ก่อนส่งภาพให้เครื่อง, ควรพิจารณาการประมวลผลล่วงหน้า:

```python
from aocr import preprocess

# Improve contrast and denoise
clean_image = preprocess.enhance(ocr_engine.image, contrast=1.5, denoise=True)
ocr_engine.image = clean_image
```

### การสนับสนุนภาษา

โดยค่าเริ่มต้นเครื่องจะสมมติเป็นภาษาอังกฤษ เพื่อ **run OCR on PDF** ในภาษาอื่น, ตั้งค่าโค้ดภาษา:

```python
ocr_engine.language = "spa"  # Spanish
```

ตรวจสอบให้แน่ใจว่าโมเดลภาษาที่สอดคล้องได้ถูกติดตั้ง

## ตัวอย่างทำงานเต็มรูปแบบ

รวมทุกอย่างเข้าด้วยกัน, นี่คือสคริปต์ที่เป็นอิสระที่คุณสามารถวางลงในไฟล์ชื่อ `ocr_pdf.py` และรันได้ทันที:

```python
# ocr_pdf.py
from aocr import OcrEngine, Image, preprocess

def main(pdf_path: str, output_path: str = None):
    # Initialize OCR engine
    ocr_engine = OcrEngine()

    # Load PDF as image (lazy loading for large files)
    ocr_engine.image = Image.load(pdf_path, lazy=False)

    # Optional preprocessing – improves accuracy on noisy scans
    ocr_engine.image = preprocess.enhance(ocr_engine.image, contrast=1.4, denoise=True)

    # Run OCR on all pages
    page_results = ocr_engine.process_all_pages()

    # Print extracted text
    for i, result in enumerate(page_results, start=1):
        print(f"--- Page {i} ---")
        print(result.text)

    # If a searchable PDF is desired
    if output_path:
        ocr_engine.save_searchable_pdf(output_path)
        print(f"Searchable PDF saved to {output_path}")

if __name__ == "__main__":
    import argparse
    parser = argparse.ArgumentParser(description="Extract text from a scanned PDF using OCR.")
    parser.add_argument("pdf", help="Path to the input scanned PDF")
    parser.add_argument("-o", "--output", help="Path to save searchable PDF (optional)")
    args = parser.parse_args()
    main(args.pdf, args.output)
```

Run it like so:

```bash
python ocr_pdf.py YOUR_DIRECTORY/contract.pdf -o YOUR_DIRECTORY/contract_searchable.pdf
```

คุณจะเห็นข้อความพิมพ์บนคอนโซล, และหากคุณระบุ `-o`, PDF ที่สามารถค้นหาได้จะปรากฏข้างไฟล์ต้นฉบับ

## เคล็ดลับมืออาชีพ & แนวปฏิบัติที่ดีที่สุด

- **Batch processing:** เมื่อจัดการกับหลายสิบไฟล์ PDF, ให้ใส่ตรรกะข้างต้นในลูปและบันทึกผลสำเร็จ/ความล้มเหลวของแต่ละไฟล์
- **Confidence filtering:** แต่ละ `page_result` มีเมตริกความมั่นใจ. ลบหรือทำเครื่องหมายหน้าที่มีความมั่นใจต่ำเพื่อการตรวจสอบด้วยมือ
- **Parallelism:** หาก CPU ของคุณมีหลายคอร์, พิจารณาใช้ `concurrent.futures` เพื่อประมวลผลหน้าพร้อมกัน—แต่ต้องระวังการใช้หน่วยความจำ
- **Version lock:** API ของ `aocr` อาจเปลี่ยนแปลง. ระบุเวอร์ชันใน `requirements.txt` (เช่น `aocr==2.3.1`) เพื่อหลีกเลี่ยงการเปลี่ยนแปลงที่ทำให้พัง

## สรุป

เราได้อธิบาย **how to use OCR** เพื่อ **extract text from PDF**, **run OCR on PDF**, **load PDF as image**, และแม้กระทั่ง **convert scanned PDF** ให้เป็นรูปแบบที่สามารถค้นหาได้ โค้ดสมบูรณ์, คำอธิบายครอบคลุมทั้ง *what* และ *why*, และตอนนี้คุณมีรูปแบบที่นำกลับไปใช้ใหม่ได้สำหรับโครงการใด ๆ ที่จัดการกับ PDF ที่เป็นภาพ

ต่อไปคุณจะทำอะไร? ลองส่งข้อความที่ดึงมาไปยัง pipeline ประมวลผลภาษาธรรมชาติ, ทำดัชนี PDF ที่สามารถค้นหาได้ด้วย Elasticsearch, หรือทดลองใช้ OCR back‑ends ต่าง ๆ เช่น Tesseract หรือ Azure Computer Vision. ไม่มีขีดจำกัด, และเครื่องมืออยู่ในมือของคุณ

ขอให้เขียนโค้ดอย่างสนุกสนาน, และขอให้ PDF ของคุณสามารถค้นหาได้เสมอ! 

![ตัวอย่างการใช้ OCR](/images/ocr_workflow.png "วิธีใช้ OCR")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}