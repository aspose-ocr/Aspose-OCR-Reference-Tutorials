---
category: general
date: 2026-01-12
description: วิธีทำ OCR รูปภาพเป็นชุดอย่างรวดเร็วและดึงข้อความจากไฟล์ JPEG ด้วย Python.
  เรียนรู้การประมวลผลเป็นชุดแบบขั้นตอนต่อขั้นตอนพร้อมตัวอย่างที่สามารถรันได้ครบถ้วน.
draft: false
keywords:
- how to batch OCR images
- extract text from JPEG files
language: th
og_description: วิธีทำ OCR รูปภาพเป็นชุดและดึงข้อความจากไฟล์ JPEG คู่มือนี้จะพาคุณผ่านโซลูชัน
  Python ที่สมบูรณ์พร้อมใช้งาน.
og_title: วิธีทำ OCR รูปภาพเป็นชุด – การสอน Python อย่างรวดเร็ว
tags:
- OCR
- Python
- image processing
title: วิธีทำ OCR รูปภาพเป็นชุด – คู่มือเร็วสำหรับการดึงข้อความจากไฟล์ JPEG
url: /th/python-java/general/how-to-batch-ocr-images-fast-guide-for-extracting-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีทำ OCR รูปภาพเป็นชุด – คู่มือเร็วสำหรับการสกัดข้อความจากไฟล์ JPEG

เคยสงสัย **วิธีทำ OCR รูปภาพเป็นชุด** โดยไม่ต้องเขียนสคริปต์แยกสำหรับแต่ละไฟล์หรือไม่? คุณไม่ได้เป็นคนเดียว ในหลายโครงการ—การสแกนใบแจ้งหนี้, การดิจิไทซ์เอกสารเก่า, หรือการตรวจสอบเนื้อหา—เราต้องดึงข้อความจากรูป JPEG หลายสิบหรือหลายร้อยไฟล์ในครั้งเดียว ข่าวดีคือคุณสามารถทำได้ด้วยเพียงไม่กี่บรรทัดของ Python และคุณจะได้เอ็นจิ้นที่นำกลับมาใช้ใหม่ได้ซึ่งสามารถใส่ลงในไพพ์ไลน์ใดก็ได้

ในบทแนะนำนี้เราจะสาธิต **วิธีทำ OCR รูปภาพเป็นชุด** อย่างละเอียด จากนั้นจะอธิบายขั้นตอนการสกัดข้อความจากไฟล์ JPEG, การจัดการกรณีขอบ, และการตรวจสอบผลลัพธ์ เมื่อจบคุณจะมีสคริปต์ที่ทำงานอิสระซึ่งสามารถรันกับโฟลเดอร์รูปภาพใดก็ได้ และคุณจะเข้าใจว่าการประมวลผลเป็นชุดสำคัญอย่างไรต่อประสิทธิภาพและการบำรุงรักษา

## สิ่งที่คุณจะได้เรียนรู้

- ตั้งค่า OCR engine อย่างง่ายและกำหนดให้ใช้ภาษาอังกฤษ
- รวบรวมไฟล์ JPEG ทั้งหมดจากไดเรกทอรีด้วย `pathlib`
- เรียกใช้ OCR engine ครั้งเดียวเพื่อประมวลผลชุดทั้งหมด
- แสดงตัวอย่างข้อความที่ถูกจดจำสำหรับแต่ละรูปภาพ
- เคล็ดลับการจัดการชุดใหญ่, ภาษาอื่น ๆ, และข้อผิดพลาดทั่วไป

**Prerequisites**: Python 3.8+, ไลบรารี `ocr` (หรือ wrapper ที่เข้ากันได้), และโฟลเดอร์ที่มีรูป JPEG ที่คุณต้องการวิเคราะห์ ไม่ต้องใช้บริการภายนอก—ทุกอย่างทำงานบนเครื่องของคุณ

---

## Step 1: Initialise the OCR Engine – The Core of How to Batch OCR Images

ก่อนที่เราจะ **ทำ OCR รูปภาพเป็นชุด** เราต้องมีเอ็นจิ้นที่รู้วิธีอ่านข้อความ ในไลบรารีส่วนใหญ่คุณจะสร้างอ็อบเจกต์ engine, ตั้งค่าภาษา (ถ้าต้องการ) แล้วใช้ซ้ำสำหรับทุกไฟล์

```python
import ocr
import pathlib

# Create the OCR engine and set it to English (the most common case)
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

*Why this matters*: การเริ่มต้นเอ็นจิ้นเพียงครั้งเดียวช่วยหลีกเลี่ยงค่าใช้จ่ายจากการโหลดโมเดลภาษาแบบซ้ำ ๆ อีกทั้งยังให้จุดเดียวที่คุณสามารถปรับตั้งค่า (เช่น DPI, รายการอักขระที่อนุญาต) ที่จะส่งผลต่อทั้งชุด

> **Pro tip**: หากคุณวางแผนจะประมวลผลเอกสารหลายภาษา ให้เปลี่ยน `ocr.Language.ENGLISH` เป็น `ocr.Language.MULTI` หรือโหลดแพ็คภาษาเพิ่มเติมก่อนเริ่มชุด

---

## Step 2: Gather All JPEG Files – The “Extract Text from JPEG Files” Part

เมื่อเอ็นจิ้นพร้อมแล้ว เราต้องบอกให้มันรู้ว่าต้องทำงานกับรูปภาพใด ใช้ `pathlib` ทำให้โค้ดเป็นแบบข้ามแพลตฟอร์มและกระชับ

```python
# Replace YOUR_DIRECTORY with the path that holds your JPEG files
image_dir = pathlib.Path("YOUR_DIRECTORY/")
image_paths = list(image_dir.glob("*.jpg"))  # only JPEG files, case‑sensitive
```

*Why this matters*: การรวบรวมรายการไฟล์ก่อนทำให้เราสามารถส่งคอลเลกชันทั้งหมดให้ OCR engine ในหนึ่งคำสั่ง—นี่คือสิ่งที่ “วิธีทำ OCR รูปภาพเป็นชุด” หมายถึง หากคุณมีโฟลเดอร์ย่อย สามารถเปลี่ยน `glob("**/*.jpg")` ให้ค้นหาแบบเรียกซ้ำได้

> **Edge case**: หากรูปของคุณมีส่วนขยายผสม (`.jpeg`, `.JPG`) ให้ขยายแพทเทิร์น glob เป็น: `image_dir.rglob("*.[jJ][pP][eE]?g")`

---

## Step 3: Process the Whole Batch in One Call – The Real Power of Batch OCR

ไลบรารี OCR สมัยใหม่ส่วนใหญ่มีเมธอด `process_batch` (หรือชื่อคล้ายกัน) ที่รับ iterable ของเส้นทางไฟล์ นี่คือหัวใจของ **วิธีทำ OCR รูปภาพเป็นชุด** อย่างมีประสิทธิภาพ

```python
# Process every JPEG file in a single batch operation
ocr_results = ocr_engine.process_batch(image_paths)
```

*Why this matters*: การเรียก batch เพียงครั้งเดียวลดจำนวนการเปลี่ยนจาก Python ไป C, ทำให้โมเดลภาษาอยู่ในหน่วยความจำตลอดเวลา และมักจะเปิดใช้การทำงานขนานภายใน ผลลัพธ์คือรายการอ็อบเจกต์—แต่ละอ็อบเจกต์มีข้อความที่จดจำและคะแนนความเชื่อมั่น

> **Performance note**: สำหรับชุดขนาดใหญ่มาก (หลายพันรูป) ควรแบ่งรายการเป็นชิ้นย่อย (เช่น 200 ไฟล์) เพื่อหลีกเลี่ยงการใช้หน่วยความจำมากเกินไป

---

## Step 4: Show a Preview of the Extracted Text – Quick Validation

หลังจาก batch เสร็จสิ้น การดูตัวอย่างอักขระแรก ๆ ของแต่ละผลลัพธ์เป็นประโยชน์ ช่วยยืนยันว่า OCR กำลังสกัดข้อความจากไฟล์ JPEG ของคุณจริง ๆ

```python
for image_path, ocr_result in zip(image_paths, ocr_results):
    # Show the image name and the first 100 characters of its recognised text
    preview = ocr_result.text[:100].replace("\n", " ").strip()
    print(f"{image_path.name}: {preview}...")
```

*Why this matters*: ตัวอย่างสั้น ๆ ทำให้คุณมองเห็นความล้มเหลวที่ชัดเจน (เช่น ผลลัพธ์ว่าง, ตัวอักษรเสีย) โดยไม่ต้องเปิดไฟล์ทุกไฟล์ หากพบปัญหาระบบ คุณสามารถปรับตั้งค่าเอ็นจิ้นและรัน batch ใหม่ได้

> **Common pitfall**: ลืมลบอักขระขึ้นบรรทัดใหม่ (`\n`) จะทำให้ตัวอย่างดูรกบรรทัด `replace("\n", " ")` จะแก้ให้เรียบร้อย

---

## Full Working Example – All Steps Combined

ด้านล่างเป็นสคริปต์เต็มที่คุณสามารถคัดลอก‑วาง, ปรับเส้นทางไดเรกทอรี, แล้วรันได้ มันแสดงขั้นตอน **วิธีทำ OCR รูปภาพเป็นชุด** ตั้งแต่ต้นจนจบ

```python
import ocr
import pathlib

def batch_ocr_jpeg(folder: str):
    """
    Process all JPEG files in `folder` and print a 100‑character preview
    of the recognised text for each image.
    """
    # Step 1 – Initialise OCR engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # Step 2 – Gather JPEG paths
    img_dir = pathlib.Path(folder)
    jpeg_paths = list(img_dir.glob("*.jpg"))  # add more patterns if needed

    if not jpeg_paths:
        print("No JPEG files found in the specified directory.")
        return

    # Step 3 – Batch process
    results = engine.process_batch(jpeg_paths)

    # Step 4 – Display previews
    for path, res in zip(jpeg_paths, results):
        preview = res.text[:100].replace("\n", " ").strip()
        print(f"{path.name}: {preview}...")

if __name__ == "__main__":
    # Replace with the path containing your JPEG images
    batch_ocr_jpeg("YOUR_DIRECTORY/")
```

**Expected output** (sample):

```
invoice_001.jpg: Invoice #001  Date: 2024-03-15  Total: $1,245.00  Bill To: Acme Corp...
receipt_202.jpg: Receipt 202  Store: QuickMart  Total: $45.67  Date: 03/12/2024...
...
```

หากตัวอย่างแสดงข้อความที่มีความหมาย คุณได้ **สกัดข้อความจากไฟล์ JPEG** ด้วยวิธี batch อย่างสำเร็จ

---

## Handling Large Batches and Advanced Scenarios

### Chunking Large Workloads
เมื่อจัดการกับหลายพันรูป หน่วยความจำอาจเป็นคอขวด แบ่งรายการเป็นชิ้นย่อย:

```python
from itertools import islice

def chunked(iterable, size):
    it = iter(iterable)
    while True:
        chunk = list(islice(it, size))
        if not chunk:
            break
        yield chunk

for chunk in chunked(jpeg_paths, 200):  # 200 files per batch
    results = engine.process_batch(chunk)
    # process results as shown earlier
```

### Switching Languages
หากเอกสารของคุณมีภาษาเฟรนช์หรือสเปน ให้เปลี่ยนภาษาก่อนเริ่ม batch:

```python
engine.language = ocr.Language.FRENCH  # or ocr.Language.SPANISH
```

### Saving Results to Disk
แทนที่จะพิมพ์ผล คุณอาจต้องการบันทึกผล OCR แต่ละรายการเป็นไฟล์ `.txt`:

```python
output_dir = pathlib.Path("ocr_output")
output_dir.mkdir(exist_ok=True)

for path, res in zip(jpeg_paths, results):
    txt_path = output_dir / f"{path.stem}.txt"
    txt_path.write_text(res.text, encoding="utf-8")
```

---

## Conclusion

คุณตอนนี้รู้ **วิธีทำ OCR รูปภาพเป็นชุด** และสามารถ **สกัดข้อความจากไฟล์ JPEG** อย่างมั่นคงด้วยสคริปต์ Python ขนาดกะทัดรัด โดยการเริ่มต้นเอ็นจิ้นครั้งเดียว, รวบรวมเส้นทาง JPEG ทั้งหมด, ประมวลผลใน batch เดียว, และแสดงตัวอย่างผลลัพธ์ คุณจะได้ความเร็วและความเรียบง่ายจากการทำงานนี้ จากนี้คุณสามารถขยาย workflow—เพิ่มการสนับสนุนหลายภาษา, เก็บผลลัพธ์ในฐานข้อมูล, หรือรวมสคริปต์เข้ากับไพพ์ไลน์การประมวลผลเอกสารขนาดใหญ่ได้

พร้อมก้าวต่อไปหรือยัง? ลองสลับไลบรารี `ocr` ไปใช้ Tesseract, ทดลองพรี‑โปรเซสภาพ (thresholding, resizing) ต่าง ๆ, หรือส่งข้อความที่สกัดไปยังโมเดลการประมวลผลภาษาธรรมชาติสำหรับการจัดประเภทอัตโนมัติ ไม่จำกัดแค่ฟังก์ชันที่คุณทำได้—คุณมีพื้นฐานที่แข็งแรงเพื่อสร้างต่อไป

Happy coding, and may your OCR batches always be error‑free!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}