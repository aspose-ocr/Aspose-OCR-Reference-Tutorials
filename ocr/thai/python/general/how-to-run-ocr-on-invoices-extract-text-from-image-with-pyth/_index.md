---
category: general
date: 2026-01-07
description: วิธีรัน OCR และดึงข้อความจากภาพสำหรับการประมวลผลใบแจ้งหนี้ เรียนรู้การปรับปรุงความแม่นยำของ
  OCR โหลดภาพสำหรับ OCR และประมวลผล OCR ใบแจ้งหนี้อย่างมีประสิทธิภาพ
draft: false
keywords:
- how to run ocr
- extract text from image
- improve ocr accuracy
- load image for ocr
- process invoice ocr
language: th
og_description: วิธีทำ OCR บนใบแจ้งหนี้แบบขั้นตอนต่อขั้นตอน ดึงข้อความจากภาพ ปรับปรุงความแม่นยำของ
  OCR และโหลดภาพสำหรับ OCR ด้วย Aspose AI.
og_title: วิธีทำ OCR บนใบแจ้งหนี้ – คู่มือ Python ฉบับเต็ม
tags:
- OCR
- Python
- Image Processing
title: วิธีทำ OCR บนใบแจ้งหนี้ – ดึงข้อความจากรูปภาพด้วย Python
url: /th/python/general/how-to-run-ocr-on-invoices-extract-text-from-image-with-pyth/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีรัน OCR บนใบแจ้งหนี้ – ดึงข้อความจากภาพด้วย Python

เคยสงสัย **วิธีรัน OCR** บนใบแจ้งหนี้ที่สแกนและได้ข้อความที่สะอาดและสามารถค้นหาได้หรือไม่? คุณไม่ได้เป็นคนเดียวที่เจอปัญหา นักพัฒนาหลายคนเจออุปสรรคเมื่อผลลัพธ์ OCR ดิบเต็มไปด้วยการสะกดผิด การตัดบรรทัดที่ไม่ถูกต้อง และการขาดเครื่องหมายวรรคตอน ในบทแนะนำนี้เราจะพาไปผ่านโซลูชันแบบเต็มสแตกที่ไม่เพียง **ดึงข้อความจากภาพ** แต่ยัง **ปรับปรุงความแม่นยำของ OCR** ด้วยการประมวลผลต่อด้วยโมเดล AI ของ Aspose

คุณจะได้เห็นวิธี **โหลดภาพสำหรับ OCR**, รันเอนจินในตัว, แล้วนำการตรวจสอบการสะกดแบบเบาไปใช้เพื่อทำให้ผลลัพธ์พร้อมสำหรับการวิเคราะห์ต่อไป เมื่อเสร็จสิ้นคุณจะมีสคริปต์ที่สามารถนำกลับมาใช้ใหม่ได้และสามารถใส่ลงใน pipeline การประมวลผลใบแจ้งหนี้ใดก็ได้

> **What you’ll need**  
> * Python 3.9 หรือใหม่กว่า  
> * `aspose-ocr` and `aspose-ai` packages (ติดตั้งผ่าน `pip`)  
> * ภาพใบแจ้งหนี้ (PNG, JPEG หรือ TIFF) – เราจะใช้ `sample_invoice.png` เป็นตัวอย่าง  
> * ตัวเลือก: GPU ที่มี VRAM อย่างน้อย 4 GB เพื่อเร่งการสรุปโมเดล (สคริปต์ทำงานบน CPU ได้เช่นกัน)

---

## ขั้นตอนที่ 1: ติดตั้งแพ็กเกจที่จำเป็นและเตรียมสภาพแวดล้อม

ก่อนที่เราจะ **โหลดภาพสำหรับ OCR** เราต้องมั่นใจว่ามีไลบรารีที่จำเป็นพร้อมใช้งาน Aspose OCR engine มาพร้อมกับ wrapper ของ Python ที่เรียบง่าย ในขณะที่ AI post‑processor พึ่งพาโมเดล quantized ของ Hugging Face

```bash
# Install Aspose OCR and AI packages
pip install aspose-ocr aspose-ai
```

> **Pro tip:** หากคุณวางแผนใช้การเร่งด้วย GPU ให้ติดตั้ง `torch` พร้อมการสนับสนุน CUDA (`pip install torch --extra-index-url https://download.pytorch.org/whl/cu121`).

---

## ขั้นตอนที่ 2: โหลดภาพใบแจ้งหนี้

การโหลดภาพนั้นตรงไปตรงมา แต่ควรอธิบายว่าทำไมเราตั้งค่าเส้นทางเป็น raw string (`r"..."`) อย่างชัดเจน สิ่งนี้ช่วยป้องกันการเกิด escape‑character โดยบังเอิญบนเส้นทางของ Windows

```python
import aspose.ocr as ocr

# Define the path to your invoice image
image_path = r"YOUR_DIRECTORY/sample_invoice.png"

# Initialize the OCR engine and attach the image
engine = ocr.OcrEngine()
engine.image = ocr.Image.load(image_path)
```

*ทำไมเรื่องนี้สำคัญ:* การใช้ `ocr.Image.load` รับประกันว่าภาพจะถูกประมวลผลล่วงหน้า (การทำไบนารี, การแก้เอียง) ตามค่าเริ่มต้นที่ดีที่สุดของ Aspose ซึ่งแล้วทำให้ **ปรับปรุงความแม่นยำของ OCR** ก่อนที่การทำงานของ AI จะเริ่ม

---

## ขั้นตอนที่ 3: รันเอนจิน OCR ในตัว

ตอนนี้เราจะ **run OCR** จริงและจับข้อความดิบ ขั้นตอนนี้จะแสดงผลลัพธ์ทั่วไปที่คุณจะได้จากการรัน OCR แบบธรรมดา—มักจะเป็นการจัดเรียงบรรทัดที่ยุ่งยากและการสะกดผิดเป็นบางครั้ง

```python
# Perform OCR
engine.recognize()
raw_text = engine.recognized_text

print("Raw OCR output:")
print(raw_text)
```

**ผลลัพธ์ดิบทั่วไป** (ตัดสั้นเพื่อความกระชับ):

```
INVOICE NO: 2023‑00123
Date: 06/15/2023
Bill To:
Acme Corp
123 Main St
...
Total Due: $1,250.00
```

คุณอาจสังเกตว่า “Invoice” ปรากฏเป็น “Invo1ce” หรือเครื่องหมายวรรคตอนหายไป นั่นคือจุดที่ AI post‑processor เข้ามาช่วย

---

## ขั้นตอนที่ 4: ตั้งค่าโมเดล AI ของ Aspose

โมเดล AI ที่เราจะใช้คือ **Qwen2.5‑3B‑Instruct‑GGUF** โมเดล LLM ที่ปรับแต่งด้วย instruction‑tuning เบา ๆ ซึ่งทำงานได้อย่างสบายบน GPU ระดับกลาง การตั้งค่าด้านล่างบอก Aspose ว่าจะดึงโมเดลจากที่ไหน จำนวนเลเยอร์ที่ให้ทำงานบน GPU เท่าใด และขนาด context สำหรับจัดการย่อหน้าที่ยาว

```python
from aspose.ai import AsposeAI, AsposeAIModelConfig

model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="q4_k_m",
    gpu_layers=30,               # 30 layers on GPU, remainder on CPU
    context_size=4096            # larger context for long paragraphs
)

ai = AsposeAI()
ai.initialize(model_config)   # you could also pass `model_config` to the constructor
```

> **Why this config?**  
> * `gpu_layers=30` สมดุลระหว่างความเร็วและหน่วยความจำ—การสรุปส่วนใหญ่ทำบน GPU, ส่วนที่เหลืออยู่บน CPU เพื่อหลีกเลี่ยงข้อผิดพลาด OOM.  
> * `context_size=4096` ทำให้โมเดลมองเห็นใบแจ้งหนี้ทั้งหมดในครั้งเดียว, ป้องกันการตัดข้อมูลสำคัญ.

---

## ขั้นตอนที่ 5: สร้างตัวประมวลผลหลังการตรวจสอบการสะกดแบบง่าย

เราจะห่อการเรียก AI ไว้ในฟังก์ชันเล็ก ๆ ชื่อ `simple_spell_check` คำสั่ง (prompt) ถูกออกแบบให้กระชับ: “Correct spelling and punctuation:” ตามด้วยข้อความ OCR ดิบ โมเดลจะคืนค่าที่ทำความสะอาดแล้ว

```python
def simple_spell_check(text):
    prompt = f"Correct spelling and punctuation:\n{text}"
    return ai.run_prompt(prompt)

# Register the post‑processor with the AI instance
ai.set_post_processor(simple_spell_check, None)
```

**How it works:** `ai.run_prompt` ส่ง prompt ไปยัง LLM ที่โหลดไว้ในเครื่อง จากนั้นโมเดลจะคืนสตริงเดียวที่มีการแก้ไขการสะกด, เครื่องหมายวรรคตอนที่ถูกต้อง, และการจัดเรียงบรรทัดที่เป็นธรรมชาติมากขึ้น

---

## ขั้นตอนที่ 6: ใช้ตัวประมวลผลหลังกับข้อความ OCR ดิบ

ตอนนี้จุดมหัศจรรย์เกิดขึ้น เรานำผลลัพธ์ OCR ดิบเข้าสู่ post‑processor ของเราและพิมพ์ผลลัพธ์ที่ได้รับการปรับปรุง

```python
enhanced_text = ai.run_postprocessor(raw_text)

print("\nAI‑enhanced OCR output:")
print(enhanced_text)
```

**Sample enhanced output**:

```
Invoice No: 2023‑00123
Date: 06/15/2023
Bill To:
Acme Corp
123 Main St
...
Total Due: $1,250.00
```

สังเกตการแก้ไขการสะกด “Invoice”, การใช้เครื่องหมายโคลอนที่ถูกต้อง, และการจัดบรรทัดที่สม่ำเสมอ—สิ่งที่คุณต้องการสำหรับการแยกข้อมูลต่อไปที่เชื่อถือได้

---

## ขั้นตอนที่ 7: ทำความสะอาดทรัพยากร

ทั้ง OCR engine และโมเดล AI จะจัดสรรทรัพยากรระดับ native การปล่อยทรัพยากรเมื่อเสร็จเป็นแนวปฏิบัติที่ดี โดยเฉพาะในบริการที่ทำงานต่อเนื่องเป็นเวลานาน

```python
ai.free_resources()
engine.dispose()
```

---

## สคริปต์เต็ม – พร้อมวาง

ด้านล่างเป็นสคริปต์ที่สมบูรณ์และสามารถรันได้ ซึ่งเชื่อมทุกขั้นตอนเข้าด้วยกัน บันทึกเป็น `invoice_ocr.py`, แทนที่ `YOUR_DIRECTORY` ด้วยโฟลเดอร์ที่มีภาพใบแจ้งหนี้ของคุณ, แล้วรันด้วย `python invoice_ocr.py`

```python
# invoice_ocr.py
import aspose.ocr as ocr
from aspose.ai import AsposeAI, AsposeAIModelConfig

# -------------------------------------------------
# Step 1: Load the image to be processed
# -------------------------------------------------
image_path = r"YOUR_DIRECTORY/sample_invoice.png"
engine = ocr.OcrEngine()
engine.image = ocr.Image.load(image_path)

# -------------------------------------------------
# Step 2: Run the built‑in OCR engine and obtain raw text
# -------------------------------------------------
engine.recognize()
raw_text = engine.recognized_text
print("Raw OCR output:")
print(raw_text)

# -------------------------------------------------
# Step 3: Configure the Aspose AI model for post‑processing
# -------------------------------------------------
model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="q4_k_m",
    gpu_layers=30,
    context_size=4096
)

ai = AsposeAI()
ai.initialize(model_config)   # alternatively, pass config to the constructor

# -------------------------------------------------
# Step 4: Define a simple spell‑check post‑processor
# -------------------------------------------------
def simple_spell_check(text):
    prompt = f"Correct spelling and punctuation:\n{text}"
    return ai.run_prompt(prompt)

ai.set_post_processor(simple_spell_check, None)

# -------------------------------------------------
# Step 5: Apply the post‑processor to the raw OCR text
# -------------------------------------------------
enhanced_text = ai.run_postprocessor(raw_text)
print("\nAI‑enhanced OCR output:")
print(enhanced_text)

# -------------------------------------------------
# Step 6: Release resources
# -------------------------------------------------
ai.free_resources()
engine.dispose()
```

รันสคริปต์แล้วคุณจะเห็นทั้งข้อมูล OCR ดิบที่มีเสียงรบกวนและเวอร์ชันที่ขัดเกลาแล้ว, **improved OCR accuracy** เคียงข้างกัน

---

## คำถามที่พบบ่อย & กรณีขอบ

### 1. ถ้าภาพใบแจ้งหนี้ของฉันเป็น PDF หลายหน้า?

Aspose OCR สามารถโหลดหน้า PDF ได้โดยตรง แทนบรรทัดการโหลดภาพด้วย:

```python
engine.image = ocr.Image.load("invoice.pdf", page_index=0)  # 0‑based page number
```

วนลูป `page_index` เพื่อประมวลผลแต่ละหน้าอย่างต่อเนื่อง

### 2. GPU ของฉันหมดหน่วยความจำ—ฉันสามารถใช้ CPU เท่านั้นได้ไหม?

แน่นอน ตั้งค่า `gpu_layers=0` ใน `AsposeAIModelConfig` โมเดลจะทำงานทั้งหมดบน CPU ซึ่งช้ากว่าแต่ปลอดภัยสำหรับฮาร์ดแวร์ระดับล่าง

### 3. ฉันจะจัดการกับใบแจ้งหนี้ที่ไม่ใช่ภาษาอังกฤษอย่างไร?

สลับ `model repository ID` ไปเป็นโมเดลที่รองรับภาษานั้น ๆ เช่น `"mistralai/Mistral-7B-Instruct-v0.2"` สำหรับการสนับสนุนหลายภาษา ส่วนที่เหลือของ pipeline ไม่ต้องเปลี่ยนแปลง

### 4. ฉันสามารถต่อหลายตัวประมวลผลหลัง (เช่น จัดรูปแบบวันที่, ดึงยอดรวม) ได้หรือไม่?

ได้ `ai.set_post_processor` รับรายการของ callable ตัวอย่างเช่น:

```python
def extract_totals(text):
    # simple regex to pull monetary values
    import re
    totals = re.findall(r"\$\d+(?:,\d{3})*(?:\.\d{2})?", text)
    return "\n".join(totals)

ai.set_post_processor([simple_spell_check, extract_totals], None)
```

ผลลัพธ์จะถูกตรวจสอบการสะกดก่อน แล้วจึงดึงยอดรวมออกมา

---

## เคล็ดลับประสิทธิภาพ & แนวทางปฏิบัติที่ดีที่สุด

| Tip | Why it Helps |
|-----|---------------|
| **Batch multiple invoices** – load them into a list and process in a loop. | ลดภาระของ Python interpreter และทำให้โมเดล AI อยู่ในสถานะ warm ในหน่วยความจำ |
| **Cache the model** – avoid calling `initialize` repeatedly in a web service. | การโหลดโมเดลอาจใช้เวลาประมาณ ~30 วินาที; การแคชทำให้ตอบสนองได้ทันที |
| **Resize large images** to 1500 px width before OCR. | ภาพขนาดเล็กทำให้ OCR และ AI inference เร็วขึ้นโดยไม่เสียความแม่นยำ |
| **Set `allow_auto_download="false"` in production** – ship the model with your deployment. | รับประกันเวลาเริ่มต้นที่คาดเดาได้และหลีกเลี่ยงปัญหาเครือข่าย |

---

## สรุป

เราได้ครอบคลุม **วิธีรัน OCR** บนใบแจ้งหนี้ ตั้งแต่การโหลดภาพจนถึงการขัดเกลาผลลัพธ์ด้วย AI‑driven spell‑check ด้วยขั้นตอนเหล่านี้คุณสามารถ **ดึงข้อความจากภาพ** อย่างเชื่อถือได้, **ปรับปรุงความแม่นยำของ OCR**, และประมวลผล **invoice OCR** อย่างราบรื่นใน workflow ที่ใช้ Python ใดก็ได้

ลองใช้กับรูปแบบใบแจ้งหนี้หลายแบบ—อาจเป็นใบเสร็จมือเขียนหรือสัญญาที่สแกน—pipeline เดียวกันสามารถปรับใช้ได้ด้วยการปรับแต่งเล็กน้อย แสดงให้เห็นว่า OCR + AI combo ที่ออกแบบดีเป็นเครื่องมืออเนกประสงค์สำหรับโครงการอัตโนมัติเอกสารใด ๆ

หากคุณพบว่าคู่มือนี้เป็นประโยชน์ โปรดแชร์ให้ทีมงานหรือกดดาวที่ repository ที่โฮสต์แพ็กเกจ Aspose

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}