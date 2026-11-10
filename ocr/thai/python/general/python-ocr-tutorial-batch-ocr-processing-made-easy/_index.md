---
category: general
date: 2026-05-03
description: บทเรียน OCR ด้วย Python ที่แสดงวิธีโหลดไฟล์ภาพ PNG, แยกข้อความจากภาพ
  และแหล่งทรัพยากร AI ฟรีสำหรับการประมวลผล OCR แบบกลุ่ม
draft: false
keywords:
- python ocr tutorial
- batch ocr processing
- free ai resources
- load png image
- recognize text from image
language: th
og_description: บทเรียน OCR ด้วย Python จะพาคุณผ่านขั้นตอนการโหลดภาพ PNG, การจดจำข้อความจากภาพ
  และการจัดการทรัพยากร AI ฟรีสำหรับการประมวลผล OCR แบบกลุ่ม
og_title: บทเรียน OCR ด้วย Python – การทำ OCR แบบแบตช์อย่างรวดเร็วด้วยแหล่งทรัพยากร
  AI ฟรี
tags:
- OCR
- Python
- AI
title: บทเรียน OCR ด้วย Python – การประมวลผล OCR แบบชุดทำได้ง่าย
url: /th/python/general/python-ocr-tutorial-batch-ocr-processing-made-easy/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# การสอน Python OCR – การประมวลผล OCR แบบกลุ่มอย่างง่าย

เคยต้องการ **python ocr tutorial** ที่จริงจังและทำให้คุณรัน OCR บนไฟล์ PNG หลายสิบไฟล์โดยไม่ต้องบิดหัวไหม? คุณไม่ได้เป็นคนเดียว ในหลายโครงการจริง ๆ คุณต้อง **load png image** ไฟล์เหล่านั้น, ป้อนให้กับเอนจิน, แล้วทำความสะอาดทรัพยากร AI เมื่อเสร็จสิ้น  

ในคู่มือนี้เราจะเดินผ่านตัวอย่างที่พร้อมรันครบถ้วน ซึ่งแสดงให้เห็นอย่างชัดเจนว่า **recognize text from image** อย่างไร, ประมวลผลเป็นกลุ่ม, และปล่อยหน่วยความจำ AI ที่ใช้ไว้ หลังจากเสร็จสิ้น คุณจะได้สคริปต์ที่สามารถนำไปใช้ในโปรเจกต์ใดก็ได้—ไม่มีส่วนเกิน, มีแค่สิ่งที่จำเป็น

## สิ่งที่คุณต้องมี

- Python 3.10 หรือใหม่กว่า (ไวยากรณ์ที่ใช้ในที่นี้พึ่งพา f‑strings และ type hints)  
- ไลบรารี OCR ที่มีเมธอด `engine.recognize` – สำหรับการสาธิตเราจะสมมติว่าใช้แพคเกจ `aocr` แต่ว่าคุณสามารถเปลี่ยนเป็น Tesseract, EasyOCR ฯลฯ ได้  
- โมดูลช่วยเหลือ `ai` ที่แสดงในโค้ดสแนป (มันจัดการการเริ่มต้นโมเดลและการทำความสะอาดทรัพยากร)  
- โฟลเดอร์ที่เต็มไปด้วยไฟล์ PNG ที่คุณต้องการประมวลผล  

หากคุณยังไม่มี `aocr` หรือ `ai` ติดตั้ง, คุณสามารถจำลองด้วยสตับได้ – ดูส่วน “Optional Stubs” ใกล้ท้ายบทความ

## ขั้นตอนที่ 1: เริ่มต้น AI Engine (Free AI Resources)

ก่อนที่คุณจะป้อนรูปภาพใด ๆ เข้าไปใน pipeline ของ OCR, โมเดลพื้นฐานต้องพร้อม การเริ่มต้นเพียงครั้งเดียวช่วยประหยัดหน่วยความจำและเร่งความเร็วของงานแบบกลุ่ม

```python
# step_1_initialize.py
import ai                # hypothetical helper that wraps the AI model
import aocr               # OCR library

def init_engine(config_path: str = "config.yaml"):
    """
    Initialize the AI engine if it hasn't been set up yet.
    This uses free AI resources – the engine will be released later.
    """
    if not ai.is_initialized():
        ai.initialize(config_path)   # auto‑initialize with the provided configuration
    else:
        print("Engine already initialized.")
```

**ทำไมจึงสำคัญ:**  
การเรียก `ai.initialize` ซ้ำ ๆ สำหรับแต่ละรูปภาพจะทำให้หน่วยความจำ GPU ถูกจัดสรรซ้ำ ๆ จนทำให้สคริปต์ล่มได้ การตรวจสอบ `ai.is_initialized()` ทำให้มั่นใจว่ามีการจัดสรรเพียงครั้งเดียว – นี่คือหลักการ “free AI resources”

## ขั้นตอนที่ 2: โหลดไฟล์ PNG สำหรับการประมวลผล OCR แบบกลุ่ม

ต่อไปเราจะรวบรวมไฟล์ PNG ทั้งหมดที่ต้องการรัน OCR การใช้ `pathlib` ทำให้โค้ดทำงานได้บนทุกระบบปฏิบัติการ

```python
# step_2_load_images.py
from pathlib import Path
from typing import List

def collect_png_paths(directory: str) -> List[Path]:
    """
    Scan `directory` and return a list of Path objects pointing to PNG files.
    """
    base_path = Path(directory)
    if not base_path.is_dir():
        raise NotADirectoryError(f"'{directory}' is not a valid folder.")
    
    png_files = sorted(base_path.glob("*.png"))
    if not png_files:
        raise FileNotFoundError("No PNG images found in the specified directory.")
    
    print(f"Found {len(png_files)} PNG image(s) to process.")
    return png_files
```

**กรณีขอบ:**  
หากโฟลเดอร์มีไฟล์ที่ไม่ใช่ PNG (เช่น JPEG) จะถูกละเว้น, ป้องกันไม่ให้ `engine.recognize` เกิดข้อผิดพลาดจากรูปแบบที่ไม่รองรับ

## ขั้นตอนที่ 3: รัน OCR บนแต่ละภาพและทำ Post‑Processing

เมื่อเอนจินพร้อมและรายการไฟล์ถูกเตรียมแล้ว, เราสามารถวนลูปผ่านรูปภาพ, ดึงข้อความดิบ, แล้วส่งให้ post‑processor ที่ทำความสะอาด artefacts ของ OCR (เช่น การขึ้นบรรทัดใหม่ที่ไม่ต้องการ)

```python
# step_3_ocr_batch.py
import aocr
import ai
from pathlib import Path
from typing import List

def ocr_batch(image_paths: List[Path]) -> List[str]:
    """
    Perform OCR on each PNG image and return a list of cleaned strings.
    """
    results = []
    for image_path in image_paths:
        # Load the image – aocr.Image.load abstracts away Pillow/OpenCV details
        img = aocr.Image.load(str(image_path))
        
        # Recognize raw text
        raw_text = engine.recognize(img)
        
        # Refine the raw OCR output using the AI post‑processor
        cleaned_text = ai.run_postprocessor(raw_text)
        results.append(cleaned_text)
        
        print(f"Processed {image_path.name}: {len(cleaned_text)} characters extracted.")
    
    return results
```

**ทำไมต้องแยกการโหลดออกจากการจดจำ:**  
`aocr.Image.load` อาจทำการถอดรหัสแบบ lazy, ซึ่งเร็วกว่าเมื่อจัดการกับชุดข้อมูลขนาดใหญ่ การแยกขั้นตอนการโหลดทำให้ง่ายต่อการสลับไลบรารีรูปภาพอื่น ๆ หากคุณต้องการรองรับ JPEG หรือ TIFF ในอนาคต

## ขั้นตอนที่ 4: ทำความสะอาด – ปล่อยทรัพยากร AI หลังจากทำงานเป็นกลุ่ม

เมื่อการประมวลผลกลุ่มเสร็จสิ้น, เราต้องปล่อยโมเดลเพื่อหลีกเลี่ยงการรั่วของหน่วยความจำ, โดยเฉพาะบนเครื่องที่เปิดใช้ GPU

```python
# step_4_cleanup.py
import ai

def release_resources():
    """
    Free any allocated AI resources. Safe to call multiple times.
    """
    if ai.is_initialized():
        ai.free_resources()
        print("AI resources have been released.")
    else:
        print("No AI resources were allocated.")
```

## รวมทุกอย่างเข้าด้วยกัน – สคริปต์เต็มรูปแบบ

ด้านล่างเป็นไฟล์เดียวที่เชื่อมขั้นตอนสี่ขั้นตอนเข้าด้วยกันเป็น workflow ที่ต่อเนื่อง บันทึกเป็น `batch_ocr.py` แล้วรันจาก command line

```python
# batch_ocr.py
"""
Python OCR tutorial – end‑to‑end batch OCR processing.
Loads PNG images, runs OCR, post‑processes results, and frees AI resources.
"""

import sys
from pathlib import Path
import ai
import aocr

# ----------------------------------------------------------------------
# Helper functions (copied from the steps above)
# ----------------------------------------------------------------------
def init_engine(cfg: str = "config.yaml"):
    if not ai.is_initialized():
        ai.initialize(cfg)
    else:
        print("Engine already initialized.")

def collect_png_paths(directory: str):
    base_path = Path(directory)
    if not base_path.is_dir():
        raise NotADirectoryError(f"'{directory}' is not a valid folder.")
    png_files = sorted(base_path.glob("*.png"))
    if not png_files:
        raise FileNotFoundError("No PNG images found in the specified directory.")
    print(f"Found {len(png_files)} PNG image(s) to process.")
    return png_files

def ocr_batch(image_paths):
    results = []
    for image_path in image_paths:
        img = aocr.Image.load(str(image_path))
        raw_text = engine.recognize(img)
        cleaned_text = ai.run_postprocessor(raw_text)
        results.append(cleaned_text)
        print(f"Processed {image_path.name}: {len(cleaned_text)} characters.")
    return results

def release_resources():
    if ai.is_initialized():
        ai.free_resources()
        print("AI resources released.")
    else:
        print("No resources to release.")

# ----------------------------------------------------------------------
# Main execution block
# ----------------------------------------------------------------------
if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python batch_ocr.py <directory-with-png>")
        sys.exit(1)

    image_dir = sys.argv[1]

    try:
        init_engine()
        png_paths = collect_png_paths(image_dir)
        texts = ocr_batch(png_paths)

        # Optional: write results to a single text file
        output_file = Path("ocr_results.txt")
        with output_file.open("w", encoding="utf-8") as f:
            for path, txt in zip(png_paths, texts):
                f.write(f"--- {path.name} ---\n")
                f.write(txt + "\n\n")
        print(f"All results saved to {output_file.resolve()}")
    finally:
        release_resources()
```

### ผลลัพธ์ที่คาดหวัง

การรันสคริปต์กับโฟลเดอร์ที่มี PNG สามไฟล์อาจพิมพ์:

```
Engine already initialized.
Found 3 PNG image(s) to process.
Processed invoice1.png: 452 characters.
Processed receipt2.png: 317 characters.
Processed flyer3.png: 689 characters.
All results saved to /home/user/ocr_results.txt
AI resources released.
```

ไฟล์ `ocr_results.txt` จะมีตัวแบ่งที่ชัดเจนสำหรับแต่ละภาพตามด้วยข้อความ OCR ที่ทำความสะอาดแล้ว

## สตับแบบเลือกใช้สำหรับ aocr & ai (หากคุณไม่มีแพคเกจจริง)

หากคุณต้องการทดสอบ flow โดยไม่ต้องดึงไลบรารี OCR ขนาดใหญ่, คุณสามารถสร้างโมดูล mock ขั้นพื้นฐานได้:

```python
# aocr/__init__.py
class Image:
    @staticmethod
    def load(path):
        return f"ImageObject({path})"

def dummy_recognize(image):
    return "Raw OCR output for " + str(image)

engine = type("Engine", (), {"recognize": dummy_recognize})()
```

```python
# ai/__init__.py
_state = {"initialized": False}

def is_initialized():
    return _state["initialized"]

def initialize(cfg):
    print(f"Initializing AI engine with {cfg}")
    _state["initialized"] = True

def run_postprocessor(text):
    # Very naive cleanup: strip extra spaces
    return " ".join(text.split())

def free_resources():
    print("Freeing AI resources")
    _state["initialized"] = False
```

วางโฟลเดอร์เหล่านี้ไว้ข้าง `batch_ocr.py` แล้วสคริปต์จะทำงาน, พิมพ์ผลลัพธ์ mock

## เคล็ดลับระดับมืออาชีพ & จุดบกพร่องที่พบบ่อย

- **การกระเด็นของหน่วยความจำ:** หากคุณประมวลผล PNG ความละเอียดสูงหลายพันไฟล์, ควรปรับขนาดภาพก่อน OCR. `aocr.Image.load` มักรับอาร์กิวเมนต์ `max_size`  
- **การจัดการ Unicode:** เปิดไฟล์ผลลัพธ์ด้วย `encoding="utf-8"` เสมอ; เอนจิน OCR สามารถส่งอักขระที่ไม่ใช่ ASCII ได้  
- **การทำงานแบบขนาน:** สำหรับ OCR ที่ใช้ CPU คุณสามารถห่อ `ocr_batch` ด้วย `concurrent.futures.ThreadPoolExecutor`. จำไว้ว่าให้ใช้อินสแตนซ์ `ai` เพียงหนึ่งเดียว – การสร้างหลายเธรดที่แต่ละอันเรียก `ai.initialize` จะทำลายเป้าหมาย “free AI resources”  
- **ความทนทานต่อข้อผิดพลาด:** ห่อการวนลูปต่อภาพด้วย `try/except` เพื่อให้ PNG ที่เสียหายหนึ่งไฟล์ไม่ทำให้การประมวลผลทั้งหมดหยุด

## สรุป

ตอนนี้คุณมี **python ocr tutorial** ที่แสดงวิธี **load png image** ไฟล์, ทำ **batch OCR processing**, และจัดการ **free AI resources** อย่างรับผิดชอบ ตัวอย่างที่ครบถ้วนและรันได้แสดงให้เห็นอย่างชัดเจนว่า **recognize text from image** อย่างไรและทำความสะอาดหลังจากนั้น, เพื่อให้คุณคัดลอก‑วางเข้าโปรเจกต์ของคุณได้โดยไม่ต้องค้นหาโค้ดที่ขาดหาย

พร้อมก้าวต่อไปหรือยัง? ลองสลับโมดูล `aocr` และ `ai` stub ด้วยไลบรารีจริงเช่น `pytesseract` และ `torchvision`. คุณยังสามารถขยายสคริปต์ให้ส่งออกเป็น JSON, ผลักดันผลลัพธ์ไปยังฐานข้อมูล, หรือผสานกับ bucket ของคลาวด์ได้ ไม่จำกัดอะไร—ขอให้สนุกกับการเขียนโค้ด!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}