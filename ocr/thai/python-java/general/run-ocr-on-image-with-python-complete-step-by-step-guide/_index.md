---
category: general
date: 2026-06-06
description: ใช้ Python ทำ OCR บนรูปภาพและดูคะแนนความเชื่อมั่น เรียนรู้วิธีกรองคำที่มีความเชื่อมั่นต่ำ
  ตั้งค่าขีดจำกัด และจัดการกับกรณีขอบ.
draft: false
keywords:
- run OCR on image
- Python OCR tutorial
- OCR confidence threshold
- low‑confidence word detection
- image text extraction
language: th
og_description: ทำ OCR บนรูปภาพด้วย Python, ตรวจสอบระดับความมั่นใจ, และกรองคำที่ความมั่นใจต่ำ
  บทเรียนนี้จะพาคุณผ่านตัวอย่างที่สมบูรณ์และสามารถรันได้.
og_title: เรียกใช้ OCR บนภาพด้วย Python – คู่มือเต็ม
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Run OCR on image using Python and see confidence scores. Learn how
    to filter low‑confidence words, set thresholds, and handle edge cases.
  headline: Run OCR on Image with Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Run OCR on image using Python and see confidence scores. Learn how
    to filter low‑confidence words, set thresholds, and handle edge cases.
  name: Run OCR on Image with Python – Complete Step‑by‑Step Guide
  steps:
  - name: Install and Import the OCR Engine
    text: First, make sure the OCR library is available. **EasyOCR** works out‑of‑the‑box
      for many languages and gives you a confidence score per word.
  - name: Run OCR on the Image
    text: Now we actually **run OCR on image**. The `recognize_image` method from
      the original example is replaced with EasyOCR’s `readtext` call, which returns
      a list of `(bbox, text, confidence)` tuples.
  - name: Summarize Overall Confidence
    text: 'Unlike the earlier snippet that printed a single `confidence` attribute,
      EasyOCR gives a confidence per word. To get an overall sense, we’ll average
      them:'
  - name: List Low‑Confidence Words
    text: Now comes the part that directly answers the “list words whose confidence
      is below the desired threshold” requirement. We’ll set a **OCR confidence threshold**
      of 0.80 (80 %) by default, but you can adjust it.
  - name: Edge Cases & Variations
    text: 1. **Batch Processing** – If you need to **run OCR on image** files in bulk,
      wrap the above logic in a loop that iterates over a directory. 2. **Multiple
      Languages** – Pass a list like `['en', 'fr']` to `easyocr.Reader` and the engine
      will detect both. 3. **Alternative Engines** – Want to try **pyte
  type: HowTo
- questions:
  - answer: Not directly. Convert each PDF page to an image first (e.g., with `pdf2image`)
      and then feed the PNG/JPEG into the script.
    question: Does this work with PDFs?
  - answer: 'Try image preprocessing: increase contrast, remove background noise,
      or rotate the image to a horizontal baseline. EasyOCR also accepts a `contrast_ths`
      parameter you can tweak.'
    question: My confidence numbers are all low—what can I do?
  - answer: Absolutely. After the low‑confidence loop, write `ocr_results` to a `csv.DictWriter`
      where each row contains `text`, `confidence`, and bounding‑box coordinates.
    question: Can I export the results to CSV?
  - answer: 'EasyOCR automatically uses CUDA if a compatible GPU and PyTorch are installed.
      Verify with `torch.cuda.is_available()` before running the script. --- ## Conclusion
      We’ve just **run OCR on image** using Python, inspected the overall confidence,
      and isolated any low‑confidence words that need a {{< /b'
    question: Is there a GPU‑accelerated version?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
title: ทำ OCR บนภาพด้วย Python – คู่มือขั้นตอนเต็มแบบละเอียด
url: /th/python-java/general/run-ocr-on-image-with-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# รัน OCR บนภาพด้วย Python – คู่มือขั้นตอนเต็ม

เคยต้องการ **run OCR on image** ไฟล์แต่ไม่แน่ใจว่าจะดึงข้อความที่เชื่อถือได้ออกมาอย่างไร? คุณไม่ได้เป็นคนเดียว—นักพัฒนาหลายคนเจอปัญหาเดียวกันเมื่อคำที่ดึงออกมาดูสั่นและคะแนนความเชื่อมั่นเป็นเรื่องลึกลับ  

ในคู่มือนี้เราจะลงลึกสู่โซลูชันที่ทำงานได้: คุณจะเห็นวิธี **run OCR on image**, อ่านคะแนนความเชื่อมั่นรวม, และดึงคำที่มีความเชื่อมั่นต่ำที่อาจต้องตรวจสอบด้วยมือออกมา เมื่อเสร็จคุณจะมีสคริปต์ที่ใช้ซ้ำได้, เข้าใจว่าทำไมแต่ละบรรทัดสำคัญ, และรู้วิธีปรับค่าเกณฑ์ความเชื่อมั่นสำหรับโปรเจคของคุณเอง

## สิ่งที่บทแนะนำนี้ครอบคลุม

* เลือกเครื่องมือ OCR ที่มั่นคง (เราจะใช้ **EasyOCR**, ไลบรารี OCR ของ Python ที่เป็นที่นิยม)  
* การตีความแอตทริบิวต์ `confidence` ที่ผลลัพธ์ OCR ทุกอย่างส่งคืน  
* กรองคำด้วย **OCR confidence threshold** ที่กำหนดเอง  
* ขยายสคริปต์สำหรับการประมวลผลแบบแบตช์หรือเครื่องมือทางเลือกเช่น **pytesseract**  

ไม่จำเป็นต้องมีประสบการณ์ OCR มาก่อน, เพียงแค่คุ้นเคยพื้นฐานกับ Python และสภาพแวดล้อมการทำงาน (แนะนำ Python 3.9+).  

พร้อมที่จะเปลี่ยนภาพหน้าจอที่เบลอให้เป็นข้อความที่สะอาดและค้นหาได้หรือยัง? ไปกันเลย.

---

## ## วิธีรัน OCR บนภาพด้วย Python

หัวใจของบทแนะนำคือโค้ดสแนปสามขั้นตอนที่สะท้อนโค้ดที่คุณเคยเห็นแล้ว ด้านล่างเราจะแยกแต่ละบรรทัด, อธิบายเหตุผล, และให้สคริปต์เต็มพร้อมคัดลอกและวาง.

### ขั้นตอน 1: ติดตั้งและนำเข้า OCR Engine

แรกสุด, ตรวจสอบให้แน่ใจว่ามีไลบรารี OCR พร้อมใช้งาน **EasyOCR** ทำงานได้ทันทีสำหรับหลายภาษาและให้คะแนนความเชื่อมั่นต่อคำ.

```bash
pip install easyocr
```

```python
import easyocr  # The engine that will run OCR on image files
import os
```

*ทำไมต้อง EasyOCR?* มันรวมโมเดล deep‑learning ที่ฝึกด้วยชุดข้อมูลหลากหลาย, ดังนั้นคุณมักจะได้ค่าความเชื่อมั่นที่สูงกว่ากลไก Tesseract เก่า, โดยเฉพาะกับภาพคุณภาพผสม.

> **เคล็ดลับ:** หากคุณอยู่ในสภาพแวดล้อมที่จำกัด (เช่น Docker container ขนาดเล็ก), `pytesseract` อาจเบากว่า, แต่คุณจะสูญเสียความแม่นยำสมัยใหม่ที่ EasyOCR มีให้.

### ขั้นตอน 2: รัน OCR บนภาพ

ตอนนี้เราจริง ๆ **run OCR on image**. เมธอด `recognize_image` จากตัวอย่างเดิมถูกแทนที่ด้วยการเรียก `readtext` ของ EasyOCR, ซึ่งคืนค่ารายการของ tuple `(bbox, text, confidence)`.

```python
# Initialize the OCR reader for English (you can add more languages as needed)
reader = easyocr.Reader(['en'])

# Path to the image you want to process
image_path = os.path.join("YOUR_DIRECTORY", "mixed_quality.png")

# Perform OCR – this is the step where we run OCR on image
ocr_results = reader.readtext(image_path, detail=1, paragraph=False)
```

แต่ละรายการใน `ocr_results` มีลักษณะดังนี้:

```python
[
    ((x1, y1, x2, y2, x3, y3, x4, y4), "Detected text", 0.92),
    ...
]
```

องค์ประกอบที่สาม (`0.92` ในตัวอย่าง) คือคะแนนความเชื่อมั่นที่อยู่ในช่วง 0 ถึง 1.

### ขั้นตอน 3: สรุปคะแนนความเชื่อมั่นรวม

ไม่เหมือนสแนปก่อนหน้าที่พิมพ์แอตทริบิวต์ `confidence` เดียว, EasyOCR ให้คะแนนความเชื่อมั่นต่อคำ. เพื่อให้ได้ความรู้โดยรวม, เราจะหาค่าเฉลี่ยของมัน:

```python
# Extract just the confidence numbers
confidences = [item[2] for item in ocr_results]

# Compute the mean confidence (overall confidence)
overall_confidence = sum(confidences) / len(confidences) if confidences else 0

print(f"Overall confidence: {overall_confidence:.2%}")
```

*ทำไมต้องเฉลี่ย?* มันให้การตรวจสอบสุขภาพอย่างรวดเร็ว—หากความเชื่อมั่นรวมต่ำกว่า, เช่น 70 %, คุณอาจต้องปรับปรุงภาพ (แสงดีกว่า, การเตรียมข้อมูลล่วงหน้า, ฯลฯ).

### ขั้นตอน 4: รายการคำที่ความเชื่อมั่นต่ำ

ตอนนี้มาถึงส่วนที่ตอบโดยตรงต่อความต้องการ “รายการคำที่ความเชื่อมั่นต่ำกว่าขีดจำกัดที่ต้องการ”. เราจะตั้ง **OCR confidence threshold** ที่ 0.80 (80 %) เป็นค่าเริ่มต้น, แต่คุณสามารถปรับได้.

```python
# Define the confidence threshold – tweak as needed
THRESHOLD = 0.80

print("\nLow‑confidence words:")
low_confidence_found = False
for bbox, text, conf in ocr_results:
    if conf < THRESHOLD:
        low_confidence_found = True
        print(f"  • '{text}' ({conf:.2%})")
if not low_confidence_found:
    print("  All words meet the confidence threshold.")
```

ลูปนี้พิมพ์แต่ละคำที่ไม่ผ่านเกณฑ์, พร้อมกับเปอร์เซ็นต์ความเชื่อมั่นของมัน. นี่คือการทำงานที่เหมือนกับลูป `for recognized_word in recognition_result.words` ดั้งเดิม, แต่ตอนนี้ทำงานกับรูปแบบผลลัพธ์ของ EasyOCR.

---

## ## ทำความเข้าใจคะแนนความเชื่อมั่นของ OCR

ความเชื่อมั่นไม่ใช่ตัวเลขวิเศษ; มันเป็นการประมาณของโมเดลว่ามั่นใจแค่ไหนกับการถอดข้อความหนึ่ง. นี่คือบางสิ่งที่ควรจำ:

| สถานการณ์ | ความเชื่อมั่นโดยทั่วไป | ควรทำ |
|-----------|-------------------|------------|
| สแกนที่ชัดเจนและความละเอียดสูง | 0.95 – 1.00 | ไม่ต้องทำงานเพิ่มเติม |
| เบลอเล็กน้อยหรือแสงไม่สม่ำเสมอ | 0.80 – 0.94 | พิจารณาการเตรียมข้อมูลล่วงหน้าเล็กน้อย (เพิ่มคอนทราสต์) |
| สัญญาณรบกวนมาก, ข้อความหมุน | < 0.70 | ใช้การเตรียมภาพล่วงหน้า (แก้ไขการเอียง, กำจัดสัญญาณรบกวน) หรือเปลี่ยนไปใช้เครื่องมือ OCR อื่น |

> **ระวัง:** บางภาษา (เช่น การเขียนลายมือแบบต่อเนื่อง) จะให้คะแนนต่ำตามธรรมชาติ. ปรับเกณฑ์ตามนั้น.

### กรณีขอบและความแปรผัน

1. **Batch Processing** – หากคุณต้องการ **run OCR on image** ไฟล์เป็นจำนวนมาก, ให้ใส่ตรรกะข้างต้นในลูปที่วนผ่านไดเรกทอรี.  
2. **Multiple Languages** – ส่งรายการเช่น `['en', 'fr']` ไปยัง `easyocr.Reader` แล้วเครื่องมือจะตรวจจับทั้งสองภาษา.  
3. **Alternative Engines** – อยากลอง **pytesseract**? แทนที่บล็อกรีดเดอร์ด้วย:

   ```python
   import pytesseract
   from PIL import Image

   img = Image.open(image_path)
   raw_text = pytesseract.image_to_string(img, output_type=pytesseract.Output.DICT)
   # raw_text['text'] contains the full string,
   # raw_text['conf'] holds per‑character confidence.
   ```

   จากนั้นคุณต้องรวมคะแนนความเชื่อมั่นต่ออักขระเป็นคะแนนต่อคำ—อาจต้องทำงานเพิ่มเล็กน้อยแต่ทำได้.  
4. **Pre‑processing Tricks** – การใช้ฟิลเตอร์ของ OpenCV (`cv2.threshold`, `cv2.GaussianBlur`) สามารถเพิ่มความเชื่อมั่นสำหรับสแกนที่มีสัญญาณรบกวน.

---

## ## สคริปต์เต็มพร้อมรัน

ด้านล่างเป็นไฟล์ Python ฉบับเต็มที่คุณสามารถใส่ในโปรเจคของคุณได้ บันทึกเป็น `ocr_report.py` แล้วรัน `python ocr_report.py`. ตรวจสอบให้แน่ใจว่าเส้นทางภาพชี้ไปยังไฟล์จริง.

```python
#!/usr/bin/env python3
"""
run_ocr_on_image.py

A self‑contained script that:
  1. Runs OCR on an image using EasyOCR.
  2. Prints the overall confidence.
  3. Lists any words whose confidence falls below a configurable threshold.

Author: Your Name
Date: 2026‑06‑06
"""

import os
import easyocr

# --------------------------- Configuration --------------------------- #
IMAGE_DIR = "YOUR_DIRECTORY"          # <-- Change to your folder
IMAGE_NAME = "mixed_quality.png"      # <-- Change to your file name
THRESHOLD = 0.80                       # Confidence threshold (0‑1)

# --------------------------- Helper Functions ----------------------- #
def load_image_path():
    """Construct the absolute path to the target image."""
    return os.path.join(IMAGE_DIR, IMAGE_NAME)

def run_ocr(image_path):
    """Run OCR on the image and return detailed results."""
    reader = easyocr.Reader(['en'])
    return reader.readtext(image_path, detail=1, paragraph=False)

def compute_overall_confidence(results):
    """Return the mean confidence across all detected words."""
    if not results:
        return 0.0
    confidences = [item[2] for item in results]
    return sum(confidences) / len(confidences)

def report_low_confidence_words(results, threshold):
    """Print words whose confidence is below the given threshold."""
    low_conf = [(text, conf) for _, text, conf in results if conf < threshold]
    if not low_conf:
        print("All words meet the confidence threshold.")
    else:
        for text, conf in low_conf:
            print(f"Low‑confidence word: '{text}' ({conf:.2%})")

# --------------------------- Main Execution ------------------------ #
def main():
    image_path = load_image_path()
    if not os.path.isfile(image_path):
        print(f"❌ Image not found: {image_path}")
        return

    # Step 1: Run OCR on image
    ocr_results = run_ocr(image_path)

    # Step 2: Show overall confidence
    overall = compute_overall_confidence(ocr_results)
    print(f"Overall confidence: {overall:.2%}")

    # Step 3: List low‑confidence words
    print("\n--- Low‑confidence words (threshold: {0:.0%}) ---".format(THRESHOLD))
    report_low_confidence_words(ocr_results, THRESHOLD)

if __name__ == "__main__":
    main()
```

**ผลลัพธ์ที่คาดหวัง** (ตัวเลขของคุณอาจแตกต่าง):

```
Overall confidence: 78.45%

--- Low‑confidence words (threshold: 80%) ---
Low‑confidence word: 'recgnition' (62.13%)
Low‑confidence word: 'imgae' (57.90%)
```

หากทุกคำผ่านเกณฑ์ 80 % คุณจะเห็นข้อความเป็นมิตร “All words meet the confidence threshold.” แทน.

---

## ## คำถามที่พบบ่อย (FAQ)

**Q: Does this work with PDFs?**  
A: ไม่ได้โดยตรง. แปลงแต่ละหน้า PDF เป็นภาพก่อน (เช่น ด้วย `pdf2image`) แล้วจึงส่งไฟล์ PNG/JPEG เข้าไปในสคริปต์.

**Q: My confidence numbers are all low—what can I do?**  
A: ลองทำการเตรียมภาพล่วงหน้า: เพิ่มคอนทราสต์, กำจัดสัญญาณรบกวนพื้นหลัง, หรือหมุนภาพให้เป็นแนวนอน. EasyOCR ยังรับพารามิเตอร์ `contrast_ths` ที่คุณสามารถปรับได้.

**Q: Can I export the results to CSV?**  
A: แน่นอน. หลังจากลูปความเชื่อมั่นต่ำ, เขียน `ocr_results` ไปยัง `csv.DictWriter` โดยแต่ละแถวมี `text`, `confidence`, และพิกัด bounding‑box.

**Q: Is there a GPU‑accelerated version?**  
A: EasyOCR จะใช้ CUDA อัตโนมัติหากมี GPU ที่เข้ากันได้และติดตั้ง PyTorch. ตรวจสอบด้วย `torch.cuda.is_available()` ก่อนรันสคริปต์.

---

## สรุป

เราเพิ่ง **run OCR on image** ด้วย Python, ตรวจสอบคะแนนความเชื่อมั่นรวม, และแยกคำที่ความเชื่อมั่นต่ำที่ต้องการ

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดซึ่งต่อยอดจากเทคนิคในคู่มือนี้. แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานครบถ้วนพร้อมคำอธิบายขั้นตอนเพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานทางเลือกในโปรเจคของคุณ.

- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)
- [How to Use Aspose OCR for JSON Result in Image Recognition](/ocr/english/net/text-recognition/get-result-as-json/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}