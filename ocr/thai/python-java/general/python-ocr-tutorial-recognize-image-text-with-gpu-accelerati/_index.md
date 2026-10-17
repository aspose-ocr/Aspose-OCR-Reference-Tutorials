---
category: general
date: 2026-06-06
description: บทเรียน OCR ด้วย Python แสดงวิธีการจดจำข้อความในภาพ, ทำ OCR ความละเอียดสูงและสกัดข้อความภาษาสเปนโดยใช้
  OCR ที่เร่งด้วย GPU.
draft: false
keywords:
- python ocr tutorial
- recognize image text
- high resolution ocr
- gpu accelerated ocr
- extract spanish text
language: th
og_description: บทเรียน OCR ด้วย Python ที่สอนคุณขั้นตอนการจดจำข้อความในรูปภาพ, OCR
  ความละเอียดสูง, และการดึงข้อความภาษาสเปนด้วยการเร่งความเร็วด้วย GPU.
og_title: บทเรียน OCR ด้วย Python – การจดจำข้อความด้วย GPU เร่งความเร็ว
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Python OCR tutorial showing how to recognize image text, perform high
    resolution OCR and extract Spanish text using GPU accelerated OCR.
  headline: Python OCR Tutorial – Recognize Image Text with GPU Acceleration
  type: TechArticle
- description: Python OCR tutorial showing how to recognize image text, perform high
    resolution OCR and extract Spanish text using GPU accelerated OCR.
  name: Python OCR Tutorial – Recognize Image Text with GPU Acceleration
  steps:
  - name: Prerequisites
    text: '- Python 3.9+ (the code works on 3.10 and newer as well). - A CUDA‑compatible
      GPU (optional but highly recommended). - Basic familiarity with pip and virtual
      environments.'
  - name: 6.1 Fallback When No GPU Is Present
    text: "```python if not torch.cuda.is_available(): # Re‑initialize the reader
      without GPU to avoid hidden errors reader = Reader(lang_list=[\"es\"], gpu=False)
      print(\"\U0001F504 Re‑initialized reader for CPU execution.\") ```"
  - name: 6.2 Down‑sampling Very Large Images
    text: 'If your image is larger than 4000 × 4000 px, you might run out of GPU memory.
      Down‑sample proportionally while preserving DPI:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- GPU
- Spanish
title: บทเรียน OCR ด้วย Python – การจดจำข้อความในภาพด้วยการเร่งความเร็วด้วย GPU
url: /th/python-java/general/python-ocr-tutorial-recognize-image-text-with-gpu-accelerati/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python OCR Tutorial – การจดจำข้อความในรูปภาพด้วยการเร่งความเร็วด้วย GPU

เคยสงสัยไหมว่า **recognize image text** ในสคริปต์ Python จะทำอย่างไรโดยไม่ต้องใช้เวลาหลายชั่วโมงปรับแต่งการตั้งค่า? คุณไม่ได้เป็นคนเดียว ใน **python ocr tutorial** นี้เราจะสาธิตวิธีที่สะอาดและครบวงจรในการสกัดข้อความสเปนจากภาพความละเอียดสูง พร้อมใส่การเร่งความเร็วด้วย GPU เพื่อให้กระบวนการทำงานเร็วเหมือนสายฟ้า

คิดว่าเป็นการสาธิตสั้น ๆ ระหว่างพักกาแฟที่คุณสามารถขยายเป็นไพป์ไลน์ระดับการผลิตในภายหลังได้ เมื่ออ่านจบคุณจะได้โปรแกรมที่ทำงาน **high resolution OCR**, ใช้ GPU ที่เปิดใช้งาน CUDA, และแสดงอักขระสเปนที่ต้องการอย่างแม่นยำ

## สิ่งที่คุณจะได้เรียนรู้

- วิธีติดตั้งและนำเข้าไลบรารี OCR สมัยใหม่ที่รองรับการเร่งความเร็วด้วย GPU  
- วิธีสร้างอินสแตนซ์ของ OCR engine และตั้งค่าให้ **recognize image text** เป็นภาษาสเปน  
- วิธีเปิดใช้งาน **gpu accelerated OCR** เพื่อเพิ่มความเร็วอย่างมหาศาลกับไฟล์ความละเอียดสูง  
- วิธีจัดการกับกรณีขอบเช่นขาดไดรเวอร์ CUDA หรือการ fallback ไปยัง CPU  
- เคล็ดลับเพื่อปรับปรุงความแม่นยำเมื่อคุณต้อง **extract spanish text** จากสแกนที่มีเสียงรบกวน

### ข้อกำหนดเบื้องต้น

- Python 3.9+ (โค้ดทำงานได้บน 3.10 และใหม่กว่า)  
- GPU ที่รองรับ CUDA (ไม่บังคับแต่แนะนำอย่างยิ่ง)  
- ความคุ้นเคยพื้นฐานกับ pip และ virtual environments  

หากคุณขาดอย่างใดอย่างหนึ่งก็ไม่เป็นไร—บทเรียนยังทำงานได้—แค่ข้ามขั้นตอน GPU แล้วไลบรารีจะ fallback ไปยัง CPU โดยอัตโนมัติ

---

## Python OCR Tutorial: Install the Required Packages

ก่อนอื่นเราต้องมี OCR engine ที่แข็งแรง สำหรับบทเรียนนี้เราจะใช้แพคเกจโอเพ่นซอร์ส **`easyocr`** ซึ่งมีการสนับสนุน GPU ในตัวเมื่อพบอุปกรณ์ที่เข้ากันได้

```bash
# Create a fresh virtual environment (optional but tidy)
python -m venv ocr-env
source ocr-env/bin/activate   # On Windows use `ocr-env\Scripts\activate`

# Install EasyOCR and its optional torch dependencies
pip install easyocr[torch]   # Installs both CPU and GPU builds of PyTorch
```

> **Pro tip:** หากคุณมี PyTorch ติดตั้งอยู่แล้ว ให้ตรวจสอบให้ตรงกับเวอร์ชัน CUDA ของคุณ (`pip install torch==2.2.0+cu121 -f https://download.pytorch.org/whl/torch_stable.html`). เวอร์ชันที่ไม่ตรงกันเป็นสาเหตุทั่วไปของข้อผิดพลาด “GPU not found”

---

## Step 1: Create an OCR Engine Instance

ตอนนี้เราจะเปิดใช้งาน engine. EasyOCR มีคลาสหลักชื่อ `Reader`. ตัวสร้างรับรายการรหัสภาษา; เราจะส่ง `"es"` สำหรับสเปน

```python
# Step 1: Initialize the OCR reader for Spanish
from easyocr import Reader

# The `gpu` flag tells EasyOCR to try using CUDA if it’s available.
reader = Reader(lang_list=["es"], gpu=True)
```

*ทำไมเรื่องนี้สำคัญ:* การกำหนดภาษาล่วงหน้าช่วยให้ engine โหลดน้ำหนักของเครือข่ายประสาทเทียมที่จำเป็นเท่านั้น ซึ่งประหยัดหน่วยความจำและเร่งการ inference—โดยเฉพาะอย่างยิ่งเมื่อคุณทำ **high resolution OCR** ต่อไป

---

## Step 2: Prepare a High‑Resolution Image

ภาพความละเอียดสูงให้พิกเซลมากขึ้นสำหรับโมเดล ซึ่งมักทำให้การจดจำอักขระดีขึ้น สมมติว่าคุณมีไฟล์ชื่อ `high_res_spanish.png` อยู่ในโฟลเดอร์ `samples`

```python
import os

# Construct an absolute path – keeps the script portable
image_path = os.path.join("samples", "high_res_spanish.png")

# Quick sanity check – raise a clear error if the file is missing
if not os.path.isfile(image_path):
    raise FileNotFoundError(f"Image not found at {image_path}")
```

หากไม่มีตัวอย่างความละเอียดสูง คุณสามารถดาวน์โหลดฟรีจาก Unsplash หรือสร้างภาพสังเคราะห์ด้วย Pillow. สิ่งสำคัญคือรักษา DPI ไว้เหนือ 300 เพื่อผลลัพธ์ที่ดีที่สุด

---

## Step 3: Enable GPU Acceleration (Optional but Recommended)

EasyOCR จะพยายามใช้ GPU เมื่อคุณตั้งค่า `gpu=True`. อย่างไรก็ตาม ควรตรวจสอบว่าอุปกรณ์จริง ๆ ถูกใช้หรือไม่ โดยเฉพาะบนเครื่องที่มีหลาย GPU

```python
import torch

# Verify CUDA availability – helpful for debugging
if torch.cuda.is_available():
    print(f"✅ CUDA device detected: {torch.cuda.get_device_name(0)}")
else:
    print("⚠️ No CUDA device found – falling back to CPU. Performance will be slower.")
```

*ทำไมต้องตรวจสอบ?* หากสคริปต์ลับ ๆ fallback ไปยัง CPU คุณอาจสงสัยว่าทำไมงาน 5 วินาทีถึงใช้ 30 วินาที การตรวจสอบเล็ก ๆ นี้ทำให้พฤติกรรมโปร่งใสและทำให้ **gpu accelerated OCR** ของคุณคาดเดาได้

---

## Step 4: Perform High‑Resolution OCR and Recognize Image Text

ตอนนี้มาถึงส่วนที่สนุก—การอ่านข้อความจริง ๆ วิธี `readtext` ของ EasyOCR จะคืนรายการของทูเพิลที่ประกอบด้วย bounding box, สตริงที่จดจำได้, และคะแนนความเชื่อมั่น

```python
# Step 4: Run OCR on the high‑resolution image
results = reader.readtext(image_path, detail=1, paragraph=False)

# `results` looks like:
# [
#   ([(x1, y1), (x2, y2), (x3, y3), (x4, y4)], 'Texto reconocido', 0.98),
#   ...
# ]
```

หากต้องการสตริงดิบโดยไม่มีพิกัด ให้ตั้งค่า `detail=0`. สำหรับกรณีการใช้ **recognize image text** ส่วนใหญ่ ค่าเริ่มต้น (`detail=1`) จะให้บริบทเพียงพอสำหรับการประมวลผลต่อไป

---

## Step 5: Extract Spanish Text and Clean the Output

เพราะเราเรียก EasyOCR ให้ใช้ภาษาสเปนแล้ว สตริงที่ได้จึงเป็นสเปนอยู่แล้ว อย่างไรก็ตาม คุณอาจต้องการต่อข้อความเข้าด้วยกัน, ลบช่องว่าง, หรือกรองการตรวจจับที่ความเชื่อมั่นต่ำ

```python
# Step 5: Consolidate high‑confidence Spanish strings
extracted_text = []
for bbox, text, conf in results:
    if conf > 0.85:                # Drop anything below 85 % confidence
        extracted_text.append(text)

# Join everything into a single block – perfect for further NLP tasks
final_text = "\n".join(extracted_text)

print("📝 Extracted Spanish text:")
print(final_text)
```

**ถ้าความเชื่อมั่นต่ำล่ะ?** คุณสามารถลดเกณฑ์ (เสี่ยงต่อเสียงรบกวน) หรือทำพรี‑โปรเซสภาพ (เพิ่มคอนทราสต์, ทำไบนารี, หรือแก้ไขการเอียง). เทคนิคเหล่านี้เป็นที่นิยมเมื่อทำ **high resolution OCR** กับเอกสารสแกน

---

## Step 6: Handling Edge Cases and Performance Tweaks

แม้โมเดลที่ฝึกอย่างดีที่สุดก็อาจเจอสถานการณ์บางอย่าง ด้านล่างเป็นวิธีแก้ไขด่วนที่คุณสามารถคัดลอกไปใส่ในสคริปต์ได้

### 6.1 Fallback When No GPU Is Present

```python
if not torch.cuda.is_available():
    # Re‑initialize the reader without GPU to avoid hidden errors
    reader = Reader(lang_list=["es"], gpu=False)
    print("🔄 Re‑initialized reader for CPU execution.")
```

### 6.2 Down‑sampling Very Large Images

หากภาพของคุณใหญ่กว่า 4000 × 4000 px คุณอาจหมดหน่วยความจำ GPU. ให้ลดขนาดโดยคงอัตราส่วนและรักษา DPI ไว้:

```python
from PIL import Image

def resize_if_needed(path, max_dim=3000):
    img = Image.open(path)
    if max(img.size) > max_dim:
        scale = max_dim / max(img.size)
        new_size = (int(img.width * scale), int(img.height * scale))
        img = img.resize(new_size, Image.LANCZOS)
        resized_path = path.replace(".png", "_resized.png")
        img.save(resized_path)
        return resized_path
    return path

image_path = resize_if_needed(image_path)
```

โค้ดสั้น ๆ เหล่านี้ทำให้สคริปต์ของคุณแข็งแรง ไม่ว่าจะรันบนเวิร์กสเตชันหรือแล็ปท็อปที่มีทรัพยากรจำกัด

---

## Full Working Example

รวมทุกอย่างเข้าด้วยกัน นี่คือสคริปต์เต็มที่คุณสามารถคัดลอก‑วางและรันได้ทันที:

```python
# python_ocr_tutorial.py
import os
import torch
from PIL import Image
from easyocr import Reader

# ----------------------------------------------------------------------
# Helper: Resize very large images to avoid GPU OOM errors
def resize_if_needed(path, max_dim=3000):
    img = Image.open(path)
    if max(img.size) > max_dim:
        scale = max_dim / max(img.size)
        new_size = (int(img.width * scale), int(img.height * scale))
        img = img.resize(new_size, Image.LANCZOS)
        resized_path = path.replace(".png", "_resized.png")
        img.save(resized_path)
        return resized_path
    return path
# ----------------------------------------------------------------------

# 1️⃣ Verify CUDA availability (optional)
if torch.cuda.is_available():
    print(f"✅ CUDA device detected: {torch.cuda.get_device_name(0)}")
else:
    print("⚠️ No CUDA device – using CPU (expect slower performance).")

# 2️⃣ Initialize the OCR engine for Spanish (GPU if possible)
reader = Reader(lang_list=["es"], gpu=torch.cuda.is_available())

# 3️⃣ Path to the high‑resolution image
image_path = os.path.join("samples", "high_res_spanish.png")
if not os.path.isfile(image_path):
    raise FileNotFoundError(f"Image not found at {image_path}")

# 4️⃣ Resize if the image is gigantic
image_path = resize_if_needed(image_path)

# 5️⃣ Run OCR – this is the core **recognize image text** step
results = reader.readtext(image_path, detail=1, paragraph=False)

# 6️⃣ Filter and concatenate high‑confidence Spanish strings
extracted = []
for bbox, txt, conf in results:
    if conf > 0.85:
        extracted.append(txt)

final_text = "\n".join(extracted)

# 7️⃣ Output the result – **extract spanish text** ready for downstream processing
print("\n📝 Extracted Spanish text:")
print(final_text)
```

**ผลลัพธ์ที่คาดหวัง (ตัวอย่าง):**



## What Should You Learn Next?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคในคู่มือนี้ แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอน‑ต่อ‑ขั้นตอน เพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโปรเจกต์ของคุณ

- [สกัดข้อความจากรูปภาพด้วย Aspose OCR – คู่มือขั้นตอน](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [วิธี OCR ข้อความในรูปภาพพร้อมภาษาโดยใช้ Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [วิธีจดจำสี่เหลี่ยมหน้ากระดาษสำหรับ OCR Text Recognition ใน Aspose.OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}