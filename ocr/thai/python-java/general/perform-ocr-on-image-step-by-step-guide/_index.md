---
category: general
date: 2026-03-18
description: ทำ OCR บนรูปภาพเพื่อดึงข้อความจากรูปภาพอย่างรวดเร็ว เรียนรู้วิธีโหลดรูปภาพสำหรับ
  OCR สร้างเครื่องมือ OCR และปรับปรุงความแม่นยำของ OCR ด้วยตัวเลือกภาษา
draft: false
keywords:
- perform OCR on image
- extract text from image
- improve OCR accuracy
- load image for OCR
- create OCR engine
language: th
og_description: ทำ OCR บนภาพด้วยคู่มือที่ละเอียดนี้ เรียนรู้วิธีโหลดภาพสำหรับ OCR
  สร้างเครื่องมือ OCR และปรับปรุงความแม่นยำของ OCR เพื่อการสกัดข้อความที่เชื่อถือได้.
og_title: ทำ OCR บนภาพ – บทเรียนการเขียนโปรแกรมครบถ้วน
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: ทำ OCR บนรูปภาพ – คู่มือขั้นตอนโดยละเอียด
url: /th/python-java/general/perform-ocr-on-image-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ทำ OCR บนรูปภาพ – การสอนเขียนโปรแกรมแบบครบถ้วน

เคยต้อง **ทำ OCR บนรูปภาพ** แต่ไม่แน่ใจว่าจะเลือกไลบรารีไหนหรือจะได้ผลลัพธ์ที่เชื่อถือได้หรือไม่? คุณไม่ได้อยู่คนเดียว ในคู่มือนี้เราจะพาคุณผ่านทุกขั้นตอนที่จำเป็นเพื่อ **ดึงข้อความจากรูปภาพ** ตั้งแต่การโหลดรูปจนถึงการปรับตัวเลือกภาษาเพื่อที่คุณจะ **ปรับปรุงความแม่นยำของ OCR** ในทุกขั้นตอน

เราจะอธิบายวิธี **โหลดรูปสำหรับ OCR**, วิธี **สร้าง OCR engine**, และเหตุผลที่แต่ละการตั้งค่ามีความสำคัญ สุดท้ายคุณจะได้สคริปต์ที่พร้อมรันและพิมพ์ข้อความที่ถูกจดจำออกมา พร้อมเข้าใจ “ทำไม” ของแต่ละบรรทัด—ไม่มีการอ้างอิง “ดูเอกสาร” แบบสั้น ๆ มาให้ ลุยกันเลย

## สิ่งที่คุณต้องมี

- Python 3.8+ (โค้ดใช้ f‑strings และ type hints)
- แพคเกจสมมติ `ocr_lib` – ติดตั้งด้วย `pip install ocr_lib`
- ไฟล์รูปภาพที่มีข้อความพิมพ์ชัดเจน (เช่น `lab_report.png`)
- โปรแกรมแก้ไขข้อความหรือ IDE เบื้องต้น (VS Code, PyCharm, หรืออะไรก็ได้ที่คุณชอบ)

ถ้าคุณมีทั้งหมดแล้ว เยี่ยม—พร้อมเริ่มได้เลย หากยังไม่มี ให้ดาวน์โหลด Python จาก python.org แล้วรันคำสั่ง pip; ใช้เวลาแค่หนึ่งนาที

![perform OCR on image example](/images/ocr-example.png)

*ข้อความอธิบาย: ทำ OCR บนรูปภาพ – ตัวอย่างผลลัพธ์ที่แสดงข้อความที่ถูกดึงออกมา*

## ขั้นตอนที่ 1: สร้าง OCR Engine – วิธี **create OCR engine** ใน Python

ก่อนที่การจดจำใด ๆ จะเกิดขึ้น ไลบรารีต้องการอ็อบเจกต์ engine ที่เก็บการตั้งค่าและสถานะการทำงาน คิดว่า engine คือสมองของกระบวนการนี้

```python
# step_1_create_engine.py
from ocr_lib import OcrEngine, LanguageOptions, OcrResult

def build_engine() -> OcrEngine:
    """
    Initialize and return a fresh OcrEngine instance.
    Creating the engine once and reusing it is more efficient than
    instantiating it inside a loop.
    """
    engine = OcrEngine()
    return engine
```

**ทำไมจึงสำคัญ:** การสร้าง engine ตั้งแต่ต้นทำให้คุณสามารถแนบตัวเลือกภาษาในภายหลังได้ และยังทำให้โมเดลภายในถูกแคชไว้เพื่อให้การเรียกครั้งต่อไปเร็วขึ้น

## ขั้นตอนที่ 2: โหลดรูปสำหรับ OCR – วิธี **load image for OCR** ที่ถูกต้อง

เมื่อเรามี engine แล้ว เราต้องให้มันมีข้อมูลให้อ่าน เมธอด `setImageFromFile` รับพาธของไฟล์ระบบ; พาธสามารถเป็นแบบเต็มหรือสัมพันธ์กับไดเรกทอรีทำงานของสคริปต์

```python
# step_2_load_image.py
def load_image(engine: OcrEngine, image_path: str) -> None:
    """
    Attach an image file to the engine.
    Raises FileNotFoundError if the file does not exist.
    """
    engine.setImageFromFile(image_path)
```

**เคล็ดลับ:** ใช้พาธเต็มหรือ `os.path.join` เพื่อหลีกเลี่ยงข้อผิดพลาด “file not found” เมื่อสคริปต์รันจากโฟลเดอร์อื่น

```python
import os

image_file = os.path.join("YOUR_DIRECTORY", "lab_report.png")
load_image(my_engine, image_file)
```

## ขั้นตอนที่ 3: ปรับปรุงความแม่นยำของ OCR – ปรับ **language options** เพื่อ **improve OCR accuracy**

OCR ที่พร้อมใช้งานทำงานได้, แต่คำศัพท์เฉพาะด้าน (เช่นศัพท์ห้องปฏิบัติการ) มักทำให้ผลลัพธ์คลาดเคลื่อน โดยการใส่พจนานุกรมกำหนดเองและ blacklist คุณจะลดการจดจำผิด เช่น การสับสนระหว่าง “0” กับ “O”

```python
# step_3_language_options.py
def configure_language(engine: OcrEngine) -> None:
    """
    Set up language options to help the engine recognize domain‑specific terms
    and ignore characters that are frequently misread.
    """
    language_opts = LanguageOptions()
    # Add terms that appear often in laboratory reports
    language_opts.setDictionary(["HPLC", "UV‑VIS", "chromatogram"])
    # Blacklist characters that cause confusion
    language_opts.setBlacklist(["0", "O", "l", "1"])
    engine.setLanguageOptions(language_opts)
```

**ทำไมวิธีนี้ช่วยได้:** พจนานุกรมบอกโมเดล OCR ว่า “HPLC” เป็นโทเคนที่ถูกต้อง, ป้องกันไม่ให้โมเดลแยกคำเป็นสิ่งไร้สาระ ส่วน blacklist บอกโมเดลให้ถือสัญลักษณ์ที่คลุมเครือเป็นสัญญาณรบกวน, ซึ่งโดยตรง **ปรับปรุงความแม่นยำของ OCR** 

## ขั้นตอนที่ 4: ทำ OCR บนรูปภาพ – การเรียก **perform OCR on image** หลัก

เมื่อ engine พร้อมและรูปภาพถูกแนบแล้ว ถึงเวลาจดจำข้อความจริง ๆ ขั้นตอนนี้จะคืนค่าอ็อบเจกต์ `OcrResult` ที่คุณสามารถสอบถามข้อความดิบ, คะแนนความเชื่อมั่น, หรือ bounding box ได้

```python
# step_4_recognize.py
def recognize_text(engine: OcrEngine) -> OcrResult:
    """
    Run the OCR process. This may take a few seconds depending on image size.
    Returns an OcrResult that contains the extracted string and metadata.
    """
    result = engine.recognize()
    return result
```

หากรูปภาพเบลอ คุณจะเห็นคะแนนความเชื่อมั่นที่ต่ำในผลลัพธ์ นั่นเป็นสัญญาณให้คุณทำการพรี‑โปรเซสภาพ (เช่น เพิ่มความคมชัด) ก่อนส่งให้ engine

## ขั้นตอนที่ 5: ดึงข้อความจากรูปภาพ – การ **extract text from image** ขั้นสุดท้าย

สุดท้าย เราเรียก `OcrResult` เพื่อขอข้อความในรูปแบบสตริง เมธอด `getText()` จะคืนสตริงแบบ plain‑text พร้อมใช้ต่อ (บันทึกไฟล์, ส่งเข้า DB, ฯลฯ)

```python
# step_5_output.py
def print_result(result: OcrResult) -> None:
    """
    Output the recognized text to the console.
    You could also write it to a file with open('output.txt', 'w') …
    """
    extracted = result.getText()
    print("=== OCR Output Start ===")
    print(extracted)
    print("=== OCR Output End ===")
```

**ผลลัพธ์ที่คาดหวัง:** สมมติว่า `lab_report.png` มีตารางง่าย ๆ คุณอาจเห็นข้อความประมาณนี้

```
=== OCR Output Start ===
Sample ID: 00123
Method: HPLC
Result: 5.67 mg/L
=== OCR Output End ===
```

เท่านี้ก็เสร็จขั้นตอน **extract text from image** แล้ว

## ตัวอย่างทำงานเต็มรูปแบบ – รวมทุกอย่างไว้ในสคริปต์เดียว

ด้านล่างเป็นสคริปต์เดียวที่รวมส่วนต่าง ๆ จากขั้นตอนก่อนหน้า คุณสามารถคัดลอก‑วางลงใน `run_ocr.py` แล้วรันด้วย `python run_ocr.py`

```python
# run_ocr.py
import os
from ocr_lib import OcrEngine, LanguageOptions, OcrResult

def build_engine() -> OcrEngine:
    engine = OcrEngine()
    return engine

def load_image(engine: OcrEngine, image_path: str) -> None:
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")
    engine.setImageFromFile(image_path)

def configure_language(engine: OcrEngine) -> None:
    language_opts = LanguageOptions()
    language_opts.setDictionary(["HPLC", "UV‑VIS", "chromatogram"])
    language_opts.setBlacklist(["0", "O", "l", "1"])
    engine.setLanguageOptions(language_opts)

def recognize_text(engine: OcrEngine) -> OcrResult:
    return engine.recognize()

def print_result(result: OcrResult) -> None:
    extracted = result.getText()
    print("\n=== OCR Output Start ===")
    print(extracted)
    print("=== OCR Output End ===\n")

def main() -> None:
    # 1️⃣ Create the OCR engine
    ocr_engine = build_engine()

    # 2️⃣ Load the image you want to process
    image_file = os.path.join("YOUR_DIRECTORY", "lab_report.png")
    load_image(ocr_engine, image_file)

    # 3️⃣ Apply language tweaks to **improve OCR accuracy**
    configure_language(ocr_engine)

    # 4️⃣ **Perform OCR on image** – this is the heavy lifting
    ocr_result = recognize_text(ocr_engine)

    # 5️⃣ **Extract text from image** and show it
    print_result(ocr_result)

if __name__ == "__main__":
    main()
```

### รายการตรวจสอบอย่างรวดเร็ว

| ✅ | รายการ |
|---|------|
| ✔️ | สร้าง engine (`create OCR engine`) |
| ✔️ | โหลดรูป (`load image for OCR`) |
| ✔️ | ตั้งค่าตัวเลือกภาษา (`improve OCR accuracy`) |
| ✔️ | ทำ OCR (`perform OCR on image`) |
| ✔️ | ดึงข้อความ (`extract text from image`) |

รันสคริปต์และดูที่คอนโซล หากคุณเห็นบล็อก “OCR Output” พร้อมเนื้อหารายงานของคุณ แสดงว่าคุณ **ทำ OCR บนรูปภาพ** สำเร็จแล้ว

## ปัญหาที่พบบ่อยและวิธีหลีกเลี่ยง

| ปัญหา | สาเหตุ | วิธีแก้ |
|-------|--------|--------|
| **ภาพเบลอ** | โมเดล OCR ไม่สามารถแยกอักขระได้ | พรี‑โปรเซสด้วย OpenCV: `cv2.GaussianBlur` หรือเพิ่ม DPI |
| **ภาษาไม่ตรง** | ภาษาเริ่มต้นอาจตั้งเป็นอื่นที่ไม่ใช่อังกฤษ | เรียก `engine.setLanguage("eng")` ก่อน `recognize()` |
| **พจนานุกรมขาดคำ** | คำเฉพาะด้านกลายเป็นอักขระผิด | เพิ่มคำผ่าน `setDictionary` ตามขั้นตอนที่ 3 |
| **อักขระใน blacklist ทำให้** |  |

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}