---
category: general
date: 2026-06-22
description: จดจำข้อความจากไฟล์ PNG ด้วย Aspose OCR ใน Python เรียนรู้การทำ OCR รูปภาพเป็นชุดและตั้งค่าชั้น
  GPU เพื่อการประมวลผลที่เร็วขึ้น.
draft: false
keywords:
- recognize text from png
- batch ocr images
- set gpu layers
- Aspose OCR Python
- GPU acceleration OCR
language: th
og_description: จดจำข้อความจากไฟล์ PNG ด้วย Aspose OCR ใน Python คู่มือนี้แสดงวิธีทำ
  OCR รูปภาพเป็นชุดและตั้งค่าชั้น GPU เพื่อเพิ่มความเร็ว.
og_title: จดจำข้อความจาก PNG – คู่มือ Aspose OCR ขั้นตอนต่อขั้นตอน
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: recognize text from png files using Aspose OCR in Python. Learn batch
    OCR images and set GPU layers for fast processing.
  headline: recognize text from png – Complete Guide with Aspose OCR & AI
  type: TechArticle
- description: recognize text from png files using Aspose OCR in Python. Learn batch
    OCR images and set GPU layers for fast processing.
  name: recognize text from png – Complete Guide with Aspose OCR & AI
  steps:
  - name: '**Model download fails** – Ensure your environment can reach `https://huggingface.co`.
      A corporate proxy may need configuration (`https_proxy` env var).'
    text: '**Model download fails** – Ensure your environment can reach `https://huggingface.co`.
      A corporate proxy may need configuration (`https_proxy` env var).'
  - name: '**GPU not detected** – Verify that the `torch` library (installed as a
      dependency) sees the GPU: `import torch; print(torch.cuda.is_available())`.
      If it returns `False`, install the CUDA‑compatible PyTorch wheel.'
    text: '**GPU not detected** – Verify that the `torch` library (installed as a
      dependency) sees the GPU: `import torch; print(torch.cuda.is_available())`.
      If it returns `False`, install the CUDA‑compatible PyTorch wheel.'
  - name: '**Incorrect image path** – `Path.glob("*.png")` is case‑sensitive on Linux.
      Use `*.PNG` or `*.png` accordingly, or add `pathlib.Path(...).rglob("*.[pP][nN][gG]")`
      for safety.'
    text: '**Incorrect image path** – `Path.glob("*.png")` is case‑sensitive on Linux.
      Use `*.PNG` or `*.png` accordingly, or add `pathlib.Path(...).rglob("*.[pP][nN][gG]")`
      for safety.'
  - name: '**Post‑processor over‑corrects** – The simple replace may turn legitimate
      “0” characters into “o”. Test on a representative sample and adjust the logic
      as needed.'
    text: '**Post‑processor over‑corrects** – The simple replace may turn legitimate
      “0” characters into “o”. Test on a representative sample and adjust the logic
      as needed.'
  type: HowTo
tags:
- OCR
- Python
- AsposeAI
title: แปลงข้อความจาก PNG – คู่มือฉบับสมบูรณ์ด้วย Aspose OCR & AI
url: /th/python/general/recognize-text-from-png-complete-guide-with-aspose-ocr-ai/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# จดจำข้อความจาก png – บทแนะนำ Aspose OCR & AI ที่ครบถ้วน

เคยต้องการ **จดจำข้อความจากไฟล์ png** แต่รู้สึกสับสนกับรายละเอียดการตั้งค่าหรือไม่? คุณไม่ได้เป็นคนเดียว ไม่ว่าคุณจะกำลังแปลงใบเสร็จเป็นดิจิทัล, สแกนแบบฟอร์ม, หรือเปลี่ยนภาพหน้าจอให้เป็นข้อความที่สามารถค้นหาได้ การเชี่ยวชาญการทำ **batch OCR images** ด้วย Python สามารถช่วยคุณประหยัดเวลามาก

ในคู่มือนี้ เราจะพาคุณผ่านตัวอย่างที่พร้อมใช้งานซึ่งไม่เพียงแต่ **จดจำข้อความจาก png** แต่ยังแสดงวิธี **ตั้งค่า GPU layers** เพื่อเพิ่มความเร็วอย่างเห็นได้ชัด ในตอนท้ายคุณจะได้สคริปต์ที่ทำงานได้เอง คำอธิบายที่ชัดเจนของแต่ละขั้นตอน และเคล็ดลับปฏิบัติที่คุณสามารถคัดลอกและวางไปใช้ในโปรเจกต์ของคุณได้

## สิ่งที่บทเรียนนี้ครอบคลุม

- การติดตั้งแพ็กเกจ Aspose OCR และ Aspose AI สำหรับ Python  
- การกำหนดค่าโมเดล AI พร้อมการดาวน์โหลดอัตโนมัติจาก Hugging Face  
- การสร้าง post‑processor เล็ก ๆ ที่แก้ไขข้อผิดพลาด OCR ที่พบบ่อยที่สุด  
- การรันลูป **batch OCR images** สำหรับโฟลเดอร์ PNG ทั้งหมด  
- การใช้ตัวเลือก **set GPU layers** เพื่อใช้ประโยชน์จากการ์ดกราฟิกของคุณ  
- การทำความสะอาดทรัพยากรอย่างปลอดภัยหลังการประมวลผล  

ไม่มีบริการภายนอก ไม่มีเวทมนตร์ที่ซ่อนอยู่—เพียงโค้ด Python ธรรมดาที่คุณสามารถวางลงในไฟล์ `.py` แล้วรันได้

![Diagram of recognize text from png workflow](workflow.png){alt="แผนภาพการทำงานของการจดจำข้อความจาก png"}

## ข้อกำหนดเบื้องต้น

| ข้อกำหนด | เหตุผลสำคัญ |
|-----------|--------------|
| Python 3.8+ | wheel ของ Aspose AI รองรับ interpreter รุ่นใหม่ |
| GPU ที่รองรับ CUDA (ไม่บังคับ) | จำเป็นหากคุณต้องการ **ตั้งค่า GPU layers** เพื่อเร่งความเร็ว |
| การเชื่อมต่ออินเทอร์เน็ตในการรันครั้งแรก | โมเดลจะถูกดาวน์โหลดอัตโนมัติจาก Hugging Face |
| `pip` ติดตั้งแล้ว | เพื่อดึงแพ็กเกจ Aspose |

หากคุณมีทั้งหมดแล้ว เยี่ยม—คุณพร้อมเริ่มใช้งานแล้ว หากยังไม่มี ขั้นตอนการติดตั้งด้านล่างจะช่วยคุณเติมเต็มส่วนที่ขาด

---

## ขั้นตอนที่ 1: ติดตั้งแพ็กเกจ Aspose OCR และ Aspose AI

ขั้นแรก ให้ดาวน์โหลดไลบรารีจาก PyPI คำสั่งด้านล่างจะดึงทั้ง OCR engine และ AI helper พร้อมกัน

```bash
pip install aspose-ocr aspose-ai
```

*เคล็ดลับ:* ใช้ virtual environment (`python -m venv .venv`) เพื่อให้แพ็กเกจแยกจากการติดตั้ง Python ระดับระบบของคุณ

---

## ขั้นตอนที่ 2: สร้างและกำหนดค่า Aspose AI Instance

ส่วนประกอบ AI ทำให้ OCR engine มีโหมด “intelligent”. เราจะชี้ไปที่โมเดล `Qwen/Qwen2.5-3B-Instruct-GGUF` ให้ดาวน์โหลดอัตโนมัติหากไม่มี และ **ตั้งค่า GPU layers** เป็น 30 (คุณสามารถปรับได้ในภายหลัง)

```python
from aspose_ai import AsposeAI, AsposeAIModelConfig

# Initialize the AI wrapper
ai = AsposeAI()

# Build a model configuration
model_cfg = AsposeAIModelConfig(
    allow_auto_download="true",                     # Grab the model automatically
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",               # Smaller footprint, still accurate
    directory_model_path="YOUR_DIRECTORY/ai_models", # Where the model will live
    gpu_layers=30                                   # <-- set gpu layers for GPU acceleration
)

# Apply the configuration and spin up the model
ai.initialize(model_cfg)
```

**เหตุผลที่สำคัญ:**  
- `allow_auto_download` ขจัดขั้นตอนการดาวน์โหลดโมเดลขนาด ~2 GB ด้วยตนเอง  
- `gpu_layers=30` บอกให้ transformer ที่อยู่ภายใต้ทำงาน 30 ชั้นแรกบน GPU ลดเวลา inference อย่างมากเมื่อมี GPU ที่รองรับ  
- การใช้ quantization แบบ `int8` ทำให้การใช้หน่วยความจำน้อยลงโดยไม่สูญเสียความแม่นยำมาก

---

## ขั้นตอนที่ 3: กำหนด Simple Post‑Processor เพื่อทำความสะอาดข้อผิดพลาด OCR

OCR ไม่สมบูรณ์—โดยเฉพาะบน PNG ความละเอียดต่ำ วิธีแก้เร็วคือการแทนที่อักขระที่มักอ่านผิด ฟังก์ชันต่อไปนี้จะแทนที่ “0” ด้วย “o” และ “1” ด้วย “l” ซึ่งเป็นรูปแบบที่เรามักพบในใบแจ้งหนี้ที่สแกน

```python
def fix_common_errors(text, **_):
    """
    Post‑processor that corrects typical OCR mis‑recognitions.
    Feel free to extend this with regexes or custom dictionaries.
    """
    return text.replace("0", "o").replace("1", "l")
```

เราจะเชื่อมฟังก์ชันนี้กับ AI instance ในขั้นตอนต่อไป เพื่อให้ผลลัพธ์การจดจำทุกครั้งผ่านการประมวลผลนี้โดยอัตโนมัติ

---

## ขั้นตอนที่ 4: เชื่อม Post‑Processor กับ OCR Engine

ตอนนี้เราจะเชื่อมทุกอย่าง: OCR engine, โมเดล AI, และ post‑processor

```python
import ocr  # Aspose OCR module

# Attach the post‑processor
ai.set_post_processor(fix_common_errors, {})

# Spin up the OCR engine and bind the AI
engine = ocr.OcrEngine()
engine.set_ai(ai)
```

**อะไรกำลังเกิดขึ้นเบื้องหลัง?**  
`OcrEngine` มอบงานหนักให้กับโมเดล AI ที่คุณกำหนด หลังจากโมเดลคืนข้อความดิบ Aspose จะเรียก `fix_common_errors` เพื่อทำความสะอาดผลลัพธ์ก่อนที่คุณจะเห็น

---

## ขั้นตอนที่ 5: Batch OCR Images – ประมวลผลทุก PNG ในโฟลเดอร์

นี่คือหัวใจของบทเรียน: ลูปที่เดินผ่านไดเรกทอรี โหลดไฟล์ `.png` แต่ละไฟล์ รัน OCR และพิมพ์ผลลัพธ์ที่ทำความสะอาดแล้ว รูปแบบนี้เป็นวิธีมาตรฐานในการ **batch OCR images** อย่างมีประสิทธิภาพ

```python
from pathlib import Path

# Replace with the folder that holds your PNG files
image_folder = Path("YOUR_DIRECTORY")

# Iterate over every PNG file in the folder
for img_path in image_folder.glob("*.png"):
    # Load the image into the engine
    engine.load_image(str(img_path))

    # Perform recognition
    result = engine.recognize()

    # Output the filename and the extracted text
    print(f"[{img_path.name}] → {result.text}")
```

**ผลลัพธ์ที่คาดหวัง** (ตัวอย่างสำหรับใบเสร็จ):

```
[receipt_001.png] → Total amount: $23.45
[receipt_002.png] → Item: Coffee, Price: $3.50
```

หากคุณมีไฟล์หลายสิบหรือหลายร้อยไฟล์ ลูปนี้จะจัดการแบบต่อเนื่อง ใช้ AI instance เดียวกันซ้ำเพื่อหลีกเลี่ยงค่าใช้จ่ายจากการโหลดโมเดลหลายครั้ง

---

## ขั้นตอนที่ 6: ทำความสะอาด – ปล่อยทรัพยากรและทำลาย Engine

เมื่อเสร็จแล้ว การปล่อยหน่วยความจำ GPU และทรัพยากร native อื่น ๆ เป็นแนวปฏิบัติที่ดี Aspose มีเมธอดเฉพาะสำหรับทำเช่นนั้น

```python
# Release the AI model and any GPU buffers
ai.free_resources()

# Dispose of the OCR engine to close native handles
engine.dispose()
```

การข้ามขั้นตอนนี้อาจทำให้หน่วยความจำ GPU ค้างอยู่ ซึ่งอาจทำให้เกิดข้อผิดพลาด out‑of‑memory ครั้งต่อไปที่รันสคริปต์

---

## โบนัส: ปรับค่า GPU Layers สำหรับฮาร์ดแวร์ที่แตกต่าง

ค่าของ `gpu_layers` ที่คุณตั้งไว้ก่อนหน้านี้เป็นจุดที่เหมาะสมสำหรับ GPU สมัยใหม่หลายรุ่น แต่คุณอาจต้องปรับค่า:

| หน่วยความจำ GPU (GB) | แนะนำ `gpu_layers` |
|-----------------------|--------------------|
| 4 GB หรือ น้อยกว่า    | 10‑15              |
| 6‑8 GB                | 20‑30              |
| 12 GB ขึ้นไป          | 35‑45 (หรือสูงกว่า) |

หากคุณใช้หน่วยความจำ GPU เกินขีดจำกัด Engine จะย้อนกลับไปใช้ CPU สำหรับชั้นที่เหลือโดยอัตโนมัติ ดังนั้นคุณจะไม่เกิดการหยุดทำงาน—แต่จะช้าลงเท่านั้น อย่าลังเลที่จะทดลองและตรวจสอบการใช้ด้วย `nvidia‑smi`

---

## ข้อผิดพลาดทั่วไป & วิธีหลีกเลี่ยง

1. **การดาวน์โหลดโมเดลล้มเหลว** – ตรวจสอบว่าสภาพแวดล้อมของคุณสามารถเข้าถึง `https://huggingface.co` ได้ อาจต้องตั้งค่า proxy ขององค์กร (`https_proxy` env var)  
2. **GPU ไม่ถูกตรวจพบ** – ยืนยันว่าไลบรารี `torch` (ติดตั้งเป็น dependency) มองเห็น GPU: `import torch; print(torch.cuda.is_available())`. หากคืนค่า `False` ให้ติดตั้ง PyTorch wheel ที่รองรับ CUDA  
3. **เส้นทางรูปภาพไม่ถูกต้อง** – `Path.glob("*.png")` แยกแยะตัวพิมพ์ใหญ่/เล็กบน Linux ใช้ `*.PNG` หรือ `*.png` ตามความเหมาะสม หรือเพิ่ม `pathlib.Path(...).rglob("*.[pP][nN][gG]")` เพื่อความปลอดภัย  
4. **Post‑processor แก้ไขเกิน** – การแทนที่อย่างง่ายอาจทำให้ “0” ที่เป็นตัวอักษรจริงกลายเป็น “o”. ทดสอบกับตัวอย่างที่เป็นตัวแทนและปรับตรรกะตามต้องการ  

---

## ตัวอย่างทำงานเต็ม (พร้อมคัดลอก‑วาง)

```python
# recognize_text_from_png_batch.py
# -------------------------------------------------
# Author: Your Name
# Date:   2026‑06‑22
# -------------------------------------------------
from pathlib import Path
import ocr                      # Aspose OCR module
from aspose_ai import AsposeAI, AsposeAIModelConfig

# ----- Step 1: AI configuration -----
ai = AsposeAI()
model_cfg = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    directory_model_path="YOUR_DIRECTORY/ai_models",
    gpu_layers=30               # <-- set gpu layers
)
ai.initialize(model_cfg)

# ----- Step 2: Post‑processor -----
def fix_common_errors(text, **_):
    """Replace typical OCR mis‑reads."""
    return text.replace("0", "o").replace("1", "l")

ai.set_post_processor(fix_common_errors, {})

# ----- Step 3: OCR engine -----
engine = ocr.OcrEngine()
engine.set_ai(ai)

# ----- Step 4: Batch processing -----
image_folder = Path("YOUR_DIRECTORY")
for img_path in image_folder.glob("*.png"):
    engine.load_image(str(img_path))
    result = engine.recognize()
    print(f"[{img_path.name}] → {result.text}")

# ----- Step 5: Cleanup -----
ai.free_resources()
engine.dispose()
```

รันด้วย:

```bash
python recognize_text_from_png_batch.py
```

คุณควรเห็นชื่อไฟล์ PNG แต่ละไฟล์ตามด้วยข้อความที่สกัดออกมา เหมือนที่แสดงไว้ก่อนหน้านี้

---

## สรุป

เราได้อธิบายขั้นตอนการทำงานแบบครบวงจรพร้อมใช้งานในผลิตภัณฑ์เพื่อ **จดจำข้อความจาก png** ด้วย Aspose OCR และ Aspose AI ใน Python โดยการรวมขั้นตอนเหล่านี้ไว้ในสคริปต์ที่เรียบง่าย คุณสามารถ **batch OCR images** ได้อย่างง่ายดาย และขอบคุณ `set gpu layers`

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดซึ่งต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดที่ทำงานครบถ้วนพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานแบบอื่นในโปรเจกต์ของคุณ

- [วิธี Batch OCR Images ด้วย List ใน Aspose.OCR สำหรับ .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [ดึงข้อความจากรูปภาพโดยใช้ OCR Operation บนโฟลเดอร์](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [วิธี OCR ข้อความรูปภาพด้วยภาษาโดยใช้ Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}