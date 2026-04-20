---
category: general
date: 2026-02-09
description: วิธีรัน OCR ด้วย Aspose AI และโมเดล Hugging Face – เรียนรู้การดาวน์โหลดโมเดล
  Hugging Face, แก้ไขข้อผิดพลาดของ OCR และปล่อยหน่วยความจำ GPU.
draft: false
keywords:
- how to run OCR
- download hugging face model
- free gpu memory
- how to free gpu
- correct OCR errors
language: th
og_description: วิธีการรัน OCR ด้วย Aspose AI ได้อธิบายไว้ในย่อหน้าแรก – ค้นหาวิธีดาวน์โหลดโมเดล
  Hugging Face, แก้ไขข้อผิดพลาดของ OCR และปล่อยหน่วยความจำ GPU
og_title: วิธีใช้งาน OCR กับ Aspose AI – คู่มือฉบับสมบูรณ์
tags:
- OCR
- Aspose
- AI
- HuggingFace
title: วิธีใช้ OCR กับ Aspose AI – คู่มือขั้นตอนโดยละเอียด
url: /th/python/general/how-to-run-ocr-with-aspose-ai-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีรัน OCR ด้วย Aspose AI – คู่มือฉบับสมบูรณ์

เคยสงสัย **วิธีรัน OCR** บนใบแจ้งหนี้ที่สแกนและได้ตัวเลขที่สะอาดสมบูรณ์โดยไม่ต้องเสียเวลาตรวจแก้ไขข้อผิดพลาดหรือไม่? คุณไม่ได้อยู่คนเดียว ในหลายโครงการจริง ๆ ข้อความดิบที่ได้จากเครื่อง OCR แบบคลาสสิกยังคงมีอักขระแปลก ๆ สัญลักษณ์สกุลเงินที่เสียหาย หรือเลขที่บิดเบือน—โดยเฉพาะเมื่อภาพต้นแบบมีสัญญาณรบกวน

ข่าวดีคือ คุณสามารถเชื่อม LLM เข้ากับ Aspose OCR, ดาวน์โหลดโมเดล Hugging Face แบบอัตโนมัติ, แล้วให้ AI ปรับผลลัพธ์ให้คุณได้ ในบทแนะนำนี้เราจะพาคุณผ่านขั้นตอนทั้งหมด ตั้งแต่การดึงโมเดล (ใช่ เราจะแสดงวิธี **download hugging face model** อย่างอัตโนมัติ) จนถึงการปล่อยทรัพยากร GPU เมื่อเสร็จสิ้น สุดท้ายคุณจะได้สคริปต์ที่ทำซ้ำได้ซึ่ง **corrects OCR errors**, ทำงานเร็วบน GPU ขนาดกลาง, และทำความสะอาดหลังการใช้งานเพื่อไม่ให้เสียหน่วยความจำ

## สิ่งที่คุณจะได้เรียนรู้

- ตั้งค่า Aspose AI ให้ดึงโมเดล **Qwen2.5‑3B‑Instruct‑GGUF** จาก Hugging Face
- รันเครื่องมือ Aspose OCR มาตรฐานบนไฟล์รูปภาพ
- ใช้พรอมต์ LLM แบบกำหนดเองที่รักษาตัวเลขและสัญลักษณ์สกุลเงินไว้ไม่เปลี่ยน
- ปล่อยหน่วยความจำ GPU ด้วยฟังก์ชัน **free gpu memory** ที่มาพร้อม
- ปรับแต่ง workflow สำหรับกรณีขอบเช่น PDF หลายหน้า หรือ GPU รุ่นต่ำ

> **Prerequisites** – Python 3.9+, แพคเกจ `aspose-ocr`, การเชื่อมต่ออินเทอร์เน็ตสำหรับการดาวน์โหลดโมเดลครั้งแรก, และ GPU ที่มี VRAM อย่างน้อย 4 GB (ไม่บังคับแต่แนะนำ) หากคุณไม่มี GPU สคริปต์จะสลับไปใช้ CPU สำหรับเลเยอร์ที่เหลือโดยอัตโนมัติ

---

## วิธีรัน OCR และปรับปรุงผลลัพธ์

ด้านล่างเป็นสคริปต์ Python เต็มรูปแบบพร้อมรันได้เลย บันทึกเป็น `ocr_with_ai.py` แล้วแทนที่เส้นทางไฟล์ตัวอย่างด้วยของคุณเอง

```python
# ocr_with_ai.py
import aspose.ocr as aocr
from aspose.ocr.ai import AsposeAI, AsposeAIModelConfig

# -------------------------------------------------
# Step 1 – Configure the AI engine (download hugging face model)
# -------------------------------------------------
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",                     # auto‑download if missing
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",               # tiny memory footprint
    gpu_layers=20,                                  # 20 layers on GPU, rest on CPU
    directory_model_path=r"YOUR_DIRECTORY/Models"  # optional custom folder
)
ai = AsposeAI(ai_config)

# -------------------------------------------------
# Step 2 – Load an image and run the classic OCR engine
# -------------------------------------------------
ocr_engine = aocr.OcrEngine()
ocr_engine.load_image(r"YOUR_DIRECTORY/invoice.png")
raw_text = ocr_engine.recognize()   # returns plain‑text string

# -------------------------------------------------
# Step 3 – Register a custom LLM prompt (correct OCR errors)
# -------------------------------------------------
def financial_prompt():
    # Bias the model toward financial terminology
    return {"prompt": "Correct OCR errors, keep numbers and currency symbols intact"}

ai.set_post_processor("llm_correction", financial_prompt)

# -------------------------------------------------
# Step 4 – Let the LLM polish the output
# -------------------------------------------------
corrected_text = ai.run_postprocessor(raw_text)

print("Original :", raw_text)
print("Enhanced :", corrected_text)

# -------------------------------------------------
# Step 5 – Release resources (free gpu memory)
# -------------------------------------------------
ai.free_resources()
```

> **Pro tip:** พารามิเตอร์ `gpu_layers` ให้คุณกำหนดจำนวนเลเยอร์ของ transformer ที่จะทำงานบน GPU หากเจอข้อผิดพลาด “out‑of‑memory” ให้ลดจำนวนนี้ลง ส่วนที่เหลือจะทำงานบน CPU – คุณยังคงสามารถ **free gpu memory** ได้ในภายหลังด้วย `ai.free_resources()`

### ผลลัพธ์ที่คาดหวัง

การรันสคริปต์บนใบแจ้งหนี้ตัวอย่างจะให้ผลลัพธ์ประมาณนี้:

```
Original : Invoic # 12345 \n Total: $1O0.00\n Date: 2023-07-15
Enhanced : Invoice # 12345
Total: $100.00
Date: 2023-07-15
```

สังเกตว่า AI แก้ไข “O” ใน `$1O0.00` ให้เป็นศูนย์ที่ถูกต้องพร้อมคงสัญลักษณ์ดอลลาร์ไว้ นี่คือหัวใจของ **correct OCR errors** สำหรับเอกสารทางการเงิน

---

## ดาวน์โหลดโมเดล Hugging Face – สิ่งที่เกิดขึ้นเบื้องหลัง?

เมื่อคุณตั้งค่า `allow_auto_download="true"` ตัว wrapper ของ Aspose AI จะตรวจสอบ `directory_model_path` หากไม่พบไฟล์โมเดล มันจะเชื่อมต่อกับ Hugging Face Hub ดึงเวอร์ชัน **int8‑quantized** ของ `Qwen2.5‑3B‑Instruct‑GGUF` แล้วเก็บไว้ในเครื่อง การดาวน์โหลดครั้งเดียวนี้มักมีขนาดไม่เกิน 2 GB ทำให้สามารถใช้ได้แม้บน SSD ขนาดเล็ก

> **ทำไมต้องเป็น int8?** การคิวไทซ์เป็น 8‑bit ลดการใช้หน่วยความจำอย่างมาก—สำคัญเมื่อคุณต้องการ **free gpu memory** หลังการประมวลผล การเสียแม่นยำเพียงเล็กน้อยเป็นการแลกเปลี่ยนที่ยอมรับได้สำหรับการทำ post‑processing ข้อความ OCR

หากคุณต้องการโฮสต์โมเดลเอง เพียงวางไฟล์ `.gguf` ลงใน `YOUR_DIRECTORY/Models` แล้ว Aspose จะโหลดโดยอัตโนมัติโดยไม่ต้องเชื่อมต่ออินเทอร์เน็ตอีกครั้ง

---

## วิธีปล่อย GPU – แนวทางปฏิบัติที่ดีที่สุด

ทรัพยากร GPU เป็นสินค้าร่วมใช้บนหลายเครื่องทำงาน การปล่อยเทนเซอร์ให้ค้างหลังสคริปต์เสร็จอาจทำให้เกิดข้อผิดพลาด “CUDA out of memory” สำหรับงานต่อไป คำสั่ง `ai.free_resources()` ทำสามอย่าง:

1. **Disposes the underlying transformer** – ปล่อยน้ำหนักที่อยู่บน GPU ทั้งหมด
2. **Clears the PyTorch cache** – เรียก `torch.cuda.empty_cache()` ภายใน
3. **Deletes temporary files** – ลบไฟล์แคชบนดิสก์ที่สร้างระหว่างการดาวน์โหลด

คุณยังสามารถเรียก `torch.cuda.empty_cache()` ด้วยตนเองได้หากใช้ Aspose AI ร่วมกับงาน PyTorch อื่น ๆ แต่วิธีในตัวมักเพียงพอ

---

## ขั้นตอนการทำงานแบบละเอียด (H2s with Secondary Keywords)

### ดาวน์โหลดโมเดล Hugging Face อัตโนมัติ

คอนสตรัคเตอร์ `AsposeAIModelConfig` ซ่อนความซับซ้อนของการติดต่อ Hugging Face API เพียงตรวจสอบว่ามีการเชื่อมต่ออินเทอร์เน็ตครั้งแรกที่รันสคริปต์ หลังจากนั้นโมเดลจะอยู่ใน `YOUR_DIRECTORY/Models` และการรันต่อไปจะเริ่มทันที

### ปล่อยหน่วยความจำ GPU หลังการทำ Inference

หากคุณรันสคริปต์นี้ภายในบริการที่ทำงานต่อเนื่อง (เช่น Flask API) ให้เรียก `ai.free_resources()` หลังทุกคำขอ วิธีนี้ป้องกันการรั่วไหลของหน่วยความจำและทำให้คำขอถัดไปสามารถใช้ GPU เดียวกันได้โดยไม่มีสะดุด

### แก้ไขข้อผิดพลาด OCR ด้วยพรอมต์กำหนดเอง

ฟังก์ชัน `financial_prompt` ของเราจะคืนค่า dictionary ที่มีคีย์เดียวคือ `prompt` คุณสามารถปรับให้เข้ากับโดเมนใดก็ได้:

```python
def medical_prompt():
    return {"prompt": "Fix OCR mistakes, keep dosage numbers and units unchanged"}
```

เปลี่ยนชื่อฟังก์ชันใน `ai.set_post_processor(...)` แล้วคุณจะได้ pipeline **correct OCR errors** สำหรับบันทึกทางการแพทย์

### วิธีรัน OCR บน PDF หลายหน้า

Aspose OCR รองรับ PDF โดยตรง:

```python
ocr_engine.load_document(r"YOUR_DIRECTORY/multi_page.pdf")
raw_text = ocr_engine.recognize()  # concatenates pages automatically
```

เมื่อได้สตริงดิบแล้ว post‑processor ของ LLM จะทำความสะอาดข้อความของแต่ละหน้าโดยอัตโนมัติ ไม่ต้องเขียนโค้ดเพิ่ม

### เมื่อไม่มี GPU – วิธีปล่อย GPU (แม้ไม่มี GPU)

แม้บนเครื่องที่มีเฉพาะ CPU การเรียก `ai.free_resources()` ก็ไม่ทำอันตราย มันจะล้างแคชภายในซึ่งช่วยลดการใช้ RAM ได้ ดังนั้นคำแนะนำ **how to free gpu** จึงใช้ได้กับทุกกรณี: ทำความสะอาดหลังการใช้งานเสมอ

---

## ข้อผิดพลาดทั่วไป & วิธีแก้

| Issue | Why It Happens | Fix |
|-------|----------------|-----|
| **Out‑of‑Memory on GPU** | `gpu_layers` ตั้งค่าสูงเกินกว่าการ์ดของคุณ | ลด `gpu_layers` เหลือ 10 หรือ 5 ให้ส่วนที่เหลือทำงานบน CPU |
| **Model never downloads** | ไฟร์วอลล์องค์กรบล็อก HTTPS ไปยัง huggingface.co | ดาวน์โหลดโมเดลด้วยตนเองจากเครือข่ายอื่น แล้วตั้งค่า `directory_model_path` ให้ชี้ไปที่โฟลเดอร์โลคัล |
| **Numbers get corrupted** | พรอมต์ไม่ชัดเจนพอเกี่ยวกับการรักษาตัวเลข | เพิ่มข้อความ “preserve all numeric values and currency symbols exactly as they appear” เข้าไปในพรอมต์ |
| **`free_resources` raises an exception** | ใช้เวอร์ชัน Aspose OCR เก่า | อัปเกรดเป็นแพคเกจ `aspose-ocr` ล่าสุด (pip install --upgrade aspose-ocr) |

---

## สรุปตัวอย่างเต็ม

นี่คือสคริปต์อีกครั้งพร้อมคอมเมนต์ในบรรทัดที่อธิบายแต่ละบรรทัดเพื่ออ้างอิงในอนาคต:

```python
import aspose.ocr as aocr
from aspose.ocr.ai import AsposeAI, AsposeAIModelConfig

# 1️⃣ Configure AI – will auto‑download the model if needed
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20,                     # adjust based on your GPU size
    directory_model_path=r"YOUR_DIRECTORY/Models"
)
ai = AsposeAI(ai_config)               # initialise the engine

# 2️⃣ Run classic OCR on an image (or PDF)
ocr_engine = aocr.OcrEngine()
ocr_engine.load_image(r"YOUR_DIRECTORY/invoice.png")
raw_text = ocr_engine.recognize()      # plain‑text result

# 3️⃣ Define a prompt that tells the LLM to keep numbers intact
def financial_prompt():
    return {"prompt": "Correct OCR errors, keep numbers and currency symbols intact"}

ai.set_post_processor("llm_correction", financial_prompt)

# 4️⃣ Let the LLM clean the text
corrected_text = ai.run_postprocessor(raw_text)

# 5️⃣ Show before/after
print("Original :", raw_text)
print("Enhanced :", corrected_text)

# 6️⃣ Clean up – this frees GPU memory for the next run
ai.free_resources()
```

---

## สรุป

เราได้ครอบคลุม **how to run OCR** ด้วย Aspose, ดาวน์โหลดโมเดล Hugging Face ตามต้องการ, สร้างพรอมต์ที่ **corrects OCR errors**, และสุดท้าย **free gpu memory** เพื่อให้เวิร์กสเตชันของคุณตอบสนองได้ดี workflow ทั้งหมดอยู่ในไฟล์ Python เพียงไฟล์เดียว—ไม่มีสคริปต์ภายนอก, ไม่มีการจัดการโมเดลด้วยมือ, และไม่มีการค้างของ GPU

ขั้นตอนต่อไป? ลองสลับ `financial_prompt` เป็น

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}