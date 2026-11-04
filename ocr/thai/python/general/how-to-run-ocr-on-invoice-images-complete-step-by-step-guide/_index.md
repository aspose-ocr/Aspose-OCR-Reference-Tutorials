---
category: general
date: 2026-01-12
description: วิธีรัน OCR และดึงข้อความจากภาพใบแจ้งหนี้โดยใช้ Aspose OCR และโมเดล Hugging
  Face ที่มีน้ำหนักเบา เรียนรู้การดาวน์โหลดโมเดล การแก้ไขข้อผิดพลาดของ OCR และการทำ
  OCR บนภาพ
draft: false
keywords:
- how to run OCR
- extract text from invoice
- download hugging face model
- correct OCR errors
- perform OCR on image
language: th
og_description: วิธีทำ OCR บนภาพใบแจ้งหนี้ ดึงข้อความและแก้ไขข้อผิดพลาดด้วย Hugging
  Face LLM ปฏิบัติตามคู่มือฉบับเต็มนี้เพื่อผลลัพธ์ที่ไร้ที่ติ
og_title: วิธีทำ OCR บนภาพใบแจ้งหนี้ – บทเรียนเต็ม
tags:
- OCR
- Python
- AI post‑processing
- Hugging Face
title: วิธีทำ OCR บนภาพใบแจ้งหนี้ – คู่มือขั้นตอนเต็ม
url: /th/python/general/how-to-run-ocr-on-invoice-images-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีการรัน OCR บนภาพใบแจ้งหนี้ – คู่มือขั้นตอนเต็ม

เคยสงสัย **วิธีการรัน OCR** บนใบแจ้งหนี้ที่สแกนแล้วและได้ข้อความที่สะอาด สามารถค้นหาได้โดยไม่ต้องใช้เวลานานในการทำความสะอาดหรือไม่? คุณไม่ได้เป็นคนเดียวที่มีคำถามนี้ ในหลายโครงการจริง ๆ ผลลัพธ์ OCR ดิบมักเต็มไปด้วยการรับรู้ผิดพลาด—เช่น “O” แทน “0”, “l” แทน “1”, หรือแม้กระทั่งคำทั้งหมดที่สับสน ข่าวดีคือ ด้วยไม่กี่บรรทัดของ Python คุณสามารถ **perform OCR on image** ได้และยังสามารถ **correct OCR errors** อัตโนมัติด้วยโมเดลขนาดเล็กจาก Hugging Face

ในบทเรียนนี้เราจะพาคุณผ่านทุกขั้นตอนที่ต้องรู้: ตั้งแต่การโหลดภาพใบแจ้งหนี้, ดึงข้อความดิบ, ดาวน์โหลดโมเดลที่ถูกควอนไทซ์, จนถึงการขัดเกลาผลลัพธ์เพื่อให้ได้การถอดข้อความที่สมบูรณ์พร้อมสำหรับการประมวลผลต่อไป เมื่อจบคุณจะสามารถ **extract text from invoice** จากไฟล์ PDF หรือ PNG ได้ด้วยสคริปต์เดียวที่ทำซ้ำได้

## ข้อกำหนดเบื้องต้นและการตั้งค่า

| Requirement | Why it matters |
|-------------|----------------|
| Python 3.9+ | ไวยากรณ์สมัยใหม่และการระบุประเภท |
| `aspose-ocr` package | ให้บริการ `ocr.OcrEngine` ที่ใช้ในตัวอย่าง |
| `aspose-ai` package | จัดหา post‑processor `AsposeAI` |
| Access to a GPU (optional) | เร่งความเร็วของชั้น LLM; หากไม่มี GPU CPU ก็ทำงานได้ดี |
| Internet connection (first run) | จำเป็นต้อง **download Hugging Face model** โดยอัตโนมัติ |

คุณสามารถติดตั้งไลบรารีที่จำเป็นได้ด้วย:

```bash
pip install aspose-ocr aspose-ai
```

> **Pro tip:** หากคุณวางแผนรัน LLM บน GPU ให้ติดตั้ง `torch` พร้อมการสนับสนุน CUDA (`pip install torch --extra-index-url https://download.pytorch.org/whl/cu118`).

ตอนนี้สภาพแวดล้อมพร้อมแล้ว ไปที่โค้ดกันเลย

---

## ขั้นตอนที่ 1 – เริ่มต้น OCR Engine และโหลดภาพใบแจ้งหนี้ของคุณ

สิ่งแรกที่คุณต้องทำคือสร้างอินสแตนซ์ของ OCR engine ของ Aspose แล้วชี้ไปที่ไฟล์ที่ต้องการประมวลผล ขั้นตอนนี้เป็นพื้นฐานของ **how to run OCR** บนภาพใด ๆ

```python
import ocr  # Aspose OCR package

# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Load the invoice you want to read
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")
```

> **Why this matters:** `load_image` รองรับ PNG, JPEG, TIFF, และแม้กระทั่งหน้า PDF ทำให้คุณ **perform OCR on image** ได้โดยไม่คำนึงถึงรูปแบบไฟล์

---

## ขั้นตอนที่ 2 – รัน OCR เบื้องต้นเพื่อดึงข้อความดิบ

เมื่อโหลดภาพแล้ว engine สามารถสร้างการถอดข้อความดิบได้ ผลลัพธ์นี้มักจะมีเสียงรบกวน ซึ่งเป็นเหตุผลที่เราจะทำขั้นตอนการแก้ไขต่อไป

```python
# Perform the OCR scan
raw_result = ocr_engine.recognize()

# Show what the engine saw
print("Raw OCR:", raw_result.text)
```

ข้อความดิบที่มักจะเป็นลักษณะเช่นนี้:

```
Raw OCR: Inv0ice No: 12345
Date: 2023/07/15
Total Am0unt: $1,200.00
```

สังเกตเลขศูนย์ (`0`) ที่ควรเป็นอักษร “O” หรือไม่? นั่นคือประเภทของข้อผิดพลาดที่เราจะแก้ไขต่อไป

---

## ขั้นตอนที่ 3 – ตั้งค่า AI Post‑Processor ด้วย LLM ขนาดเล็ก

ตอนนี้เรานำ **download Hugging Face model** ที่มีขนาดเล็กพอที่จะรันบนฮาร์ดแวร์ระดับกลาง แต่ก็มีพลังพอที่จะเข้าใจภาษาของใบแจ้งหนี้ ตัวอย่างใช้โมเดล Qwen 2.5 3B‑Instruct GGUF ที่ถูกควอนไทซ์เป็น `int8` เพื่อให้ใช้หน่วยความจำน้อยที่สุด

```python
from aspose_ai import AsposeAI, AsposeAIModelConfig

# Define model configuration
model_config = AsposeAIModelConfig(
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",          # reduces size dramatically
    gpu_layers=20,                             # use GPU for the first 20 layers if available
    allow_auto_download="true"                # pulls the model on first run
)

# Initialise the AI processor and attach the post‑processor
ai_processor = AsposeAI()
ai_processor.set_post_processor("llm_correction", model_config)
```

> **Why this model?** การควอนไทซ์เป็น `int8` ลดขนาดไฟล์เหลือประมาณ ~1.2 GB ทำให้สามารถรันบนแล็ปท็อปส่วนใหญ่ได้ ชั้น GPU จะเร่งการ inference, แต่โค้ดจะถอยกลับไปใช้ CPU หากไม่พบ GPU

---

## ขั้นตอนที่ 4 – รันการแก้ไขด้วย LLM บนผล OCR ดิบ

เมื่อโมเดลพร้อม เราจะป้อนข้อความดิบเข้าสู่ post‑processor LLM จะทำการเขียนข้อความใหม่ แก้ไขข้อบกพร่องของ OCR ที่พบบ่อยและทำให้ตัวเลขเป็นรูปแบบมาตรฐาน

```python
# Apply AI correction
corrected_result = ai_processor.run_postprocessor(raw_result)

# Display the cleaned output
print("AI‑corrected:", corrected_result.text)
```

ผลลัพธ์ที่ทำความสะอาดแล้วที่คาดว่าจะได้:

```
AI‑corrected: Invoice No: 12345
Date: 2023/07/15
Total Amount: $1,200.00
```

คุณจะเห็นว่าเลขศูนย์กลับกลายเป็นอักษร “O” อีกครั้ง และ “Am0unt” กลายเป็น “Amount” นี่คือหัวใจของการ **correct OCR errors** อย่างอัตโนมัติ

---

## ขั้นตอนที่ 5 – ปล่อยทรัพยากรและทำความสะอาด

โมเดลภาษาใหญ่สามารถยึดหน่วยความจำของ GPU ไว้ได้ ดังนั้นการปล่อยทรัพยากรเมื่อทำงานเสร็จเป็นแนวปฏิบัติที่ดี

```python
# Free the model and any GPU buffers
ai_processor.free_resources()
```

หากคุณวางแผนประมวลผลใบแจ้งหนี้หลายใบเป็นชุด คุณอาจโหลดโมเดลไว้แล้วปล่อยเมื่อตอนจบสคริปต์เท่านั้น

---

## ตัวอย่างการทำงานเต็มรูปแบบ

รวมทุกอย่างเข้าด้วยกัน นี่คือสคริปต์เดียวที่คุณสามารถบันทึกเป็นไฟล์ `.py` แล้วรันได้:

```python
# ------------------------------------------------------------
# How to Run OCR on Invoice Images – End‑to‑End Example
# ------------------------------------------------------------
import ocr
from aspose_ai import AsposeAI, AsposeAIModelConfig

def main():
    # 1️⃣ Initialise OCR engine
    ocr_engine = ocr.OcrEngine()
    ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")

    # 2️⃣ Capture raw OCR text
    raw_result = ocr_engine.recognize()
    print("Raw OCR:", raw_result.text)

    # 3️⃣ Configure lightweight LLM from Hugging Face
    model_cfg = AsposeAIModelConfig(
        hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
        hugging_face_quantization="int8",
        gpu_layers=20,
        allow_auto_download="true"
    )
    ai = AsposeAI()
    ai.set_post_processor("llm_correction", model_cfg)

    # 4️⃣ Run AI correction
    corrected = ai.run_postprocessor(raw_result)
    print("AI‑corrected:", corrected.text)

    # 5️⃣ Clean up
    ai.free_resources()

if __name__ == "__main__":
    main()
```

การรันสคริปต์จะให้ผลลัพธ์คล้ายกับบล็อก “AI‑corrected” ที่แสดงไว้ก่อนหน้า คุณสามารถเปลี่ยนเส้นทางของภาพเป็นใบแจ้งหนี้หรือใบเสร็จอื่น ๆ เพื่อ **extract text from invoice** เป็นจำนวนมากได้ตามต้องการ

---

## คำถามที่พบบ่อยและกรณีขอบ

### What if I don’t have a GPU?

พารามิเตอร์ `gpu_layers` เป็นตัวเลือก ตั้งค่าเป็น `0` หรือไม่ระบุก็ได้ โมเดลจะทำงานทั้งหมดบน CPU คาดว่าจะช้ากว่า—ประมาณ 2–3 วินาทีต่อหน้าในแล็ปท็อปสมัยใหม่

### My invoices are multi‑page PDFs. How do I handle them?

แปลงแต่ละหน้าเป็นภาพแยก (เช่น ใช้ `pdf2image`) แล้ววนลูปผ่านหน้าเหล่านั้นด้วยสคริปต์เดียวกัน OCR engine สามารถประมวลผลแต่ละภาพได้อย่างอิสระ และ LLM จะทำการแก้ไขข้อความแต่ละบล็อก

```python
from pdf2image import convert_from_path

pages = convert_from_path("invoice.pdf", dpi=300)
for i, page_img in enumerate(pages):
    ocr_engine.load_image(page_img)
    # …run steps 2‑4…
```

### The model download fails behind a firewall?

ดาวน์โหลดโมเดลด้วยตนเองจาก Hugging Face model hub, แตกไฟล์ลงโฟลเดอร์ในเครื่อง แล้วตั้งค่า `hugging_face_repo_id` ให้ชี้ไปยังเส้นทางท้องถิ่น:

```python
model_cfg = AsposeAIModelConfig(
    hugging_face_repo_id="/local/path/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20,
    allow_auto_download="false"
)
```

### How accurate is the correction?

สำหรับใบแจ้งหนี้ภาษาอังกฤษทั่วไป LLM สามารถแก้ไข >95 % ของการรับรู้ OCR ที่ผิดพลาดได้ อย่างไรก็ตามโน้ตที่เขียนด้วยมือซับซ้อนอาจยังต้องตรวจสอบด้วยมือ

---

## เคล็ดลับและเทคนิคสำหรับการใช้งานใน Production

- **Batch processing:** ห่อขั้นตอน 2‑4 ไว้ในฟังก์ชันและส่งรายการเส้นทางไฟล์เข้าไป ใช้ `AsposeAI` อินสแตนซ์เดียวเพื่อหลีกเลี่ยงการโหลดโมเดลซ้ำ
- **Logging:** แทนที่ `print` ด้วยโมดูล `logging` ของ Python เพื่อบันทึกทั้งข้อความดิบและข้อความที่แก้ไขสำหรับการตรวจสอบย้อนหลัง
- **Error handling:** ครอบการเรียก OCR ด้วยบล็อก `try/except` หากภาพใดภาพหนึ่งล้มเหลว ให้บันทึกชื่อไฟล์แล้วดำเนินต่อ
- **Performance tuning:** ทดลองปรับค่า `gpu_layers` ชั้นที่มากขึ้นบน GPU จะเร่ง inference แต่ใช้ VRAM มากขึ้น

---

## สรุป

เราได้ครอบคลุม **how to run OCR** บนภาพใบแจ้งหนี้ตั้งแต่ต้นจนจบ แสดงวิธี **perform OCR on image**, **download Hugging Face model**, และ **correct OCR errors** อย่างอัตโนมัติ สคริปต์เต็มแสดงเวิร์กโฟลว์ที่ใช้งานได้จริงซึ่งคุณสามารถนำไปใส่ใน pipeline การอัตโนมัติด้วย Python ใด ๆ

ขั้นตอนต่อไป? ลองขยาย pipeline เพื่อ **extract key fields** (หมายเลขใบแจ้งหนี้, วันที่, ยอดรวม) ด้วย regular expressions บนข้อความที่แก้ไขแล้ว หรือส่งผลลัพธ์ที่ทำความสะอาดไปยังฐานข้อมูลเพื่อให้ค้นหาได้ง่าย คุณยังสามารถทดลองใช้ LLM ขนาดเล็กอื่น ๆ จาก Hugging Face หากต้องการภาษาอื่นหรือความรู้เฉพาะด้าน

Happy coding, and may your OCR results always be crystal‑clear! 

![วิธีการรัน OCR บนภาพใบแจ้งหนี้](ocr_invoice_example.png "วิธีการรัน OCR บนใบแจ้งหนี้")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}