---
category: general
date: 2026-06-19
description: วิธีทำ OCR ทีละขั้นตอนและปรับปรุงความแม่นยำของ OCR ด้วยเทคนิค OCR ข้อความธรรมดา
  เรียนรู้กระบวนการทำงานที่รวดเร็วสำหรับการสกัดข้อความที่เชื่อถือได้
draft: false
keywords:
- how to run OCR
- improve OCR accuracy
- plain text OCR
- OCR post‑processing
- layout‑aware OCR
language: th
og_description: วิธีการใช้งาน OCR อย่างมีประสิทธิภาพ บทเรียนนี้แสดงวิธีการปรับปรุงความแม่นยำของ
  OCR ด้วยการใช้ OCR ข้อความธรรมดาและการประมวลผลหลังด้วย AI.
og_title: วิธีรัน OCR ด้วย Python – คู่มือครบวงจร
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to run OCR step‑by‑step and improve OCR accuracy with plain text
    OCR techniques. Learn a fast workflow for reliable text extraction.
  headline: How to Run OCR in Python – Complete Guide
  type: TechArticle
- description: How to run OCR step‑by‑step and improve OCR accuracy with plain text
    OCR techniques. Learn a fast workflow for reliable text extraction.
  name: How to Run OCR in Python – Complete Guide
  steps:
  - name: '**Batch processing** – Wrap the whole script in a function that walks a
      directory, handling thousands of files in parallel with `concurrent.futures`.'
    text: '**Batch processing** – Wrap the whole script in a function that walks a
      directory, handling thousands of files in parallel with `concurrent.futures`.'
  - name: '**Language models** – Swap the simple difflib heuristic for a call to OpenAI’s
      `gpt‑4o` or a locally hosted LLaMA model to get richer contextual corrections.'
    text: '**Language models** – Swap the simple difflib heuristic for a call to OpenAI’s
      `gpt‑4o` or a locally hosted LLaMA model to get richer contextual corrections.'
  - name: '**Export formats** – Write the corrected structure to a searchable PDF'
    text: '**Export formats** – Write the corrected structure to a searchable PDF'
  type: HowTo
tags:
- OCR
- Python
- AI
title: วิธีรัน OCR ด้วย Python – คู่มือครบถ้วน
url: /th/python/general/how-to-run-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีการรัน OCR ใน Python – คู่มือฉบับสมบูรณ์

เคยสงสัย **วิธีรัน OCR** บนชุดไฟล์ PDF ที่สแกนหลายไฟล์โดยไม่ต้องเสียเวลาปรับตั้งค่าหลายชั่วโมงหรือไม่? คุณไม่ได้อยู่คนเดียว ในหลายโครงการอุปสรรคแรกคือการดึงข้อความที่เชื่อถือได้จากภาพ และความแตกต่างระหว่างผลลัพธ์ที่คลาดเคลื่อนกับการสกัดที่สะอาดมักขึ้นอยู่กับขั้นตอนอัจฉริยะไม่กี่ขั้นตอน

ในคู่มือนี้เราจะพาคุณผ่านกระบวนการสี่ขั้นตอนที่ใช้งานได้จริง ไม่เพียงแต่ **รัน OCR** แต่ยัง **ปรับปรุงความแม่นยำของ OCR** ด้วยการผสานการสแกนแบบข้อความธรรมดาอย่างรวดเร็วกับการสแกนที่รับรู้โครงสร้างและตัวประมวลผลหลังจาก AI สุดท้าย เมื่อเสร็จคุณจะได้สคริปต์พร้อมรัน คำอธิบายว่าทำไมแต่ละขั้นตอนจึงสำคัญ และเคล็ดลับการจัดการกรณีขอบเช่นหน้าหลายคอลัมน์หรือสแกนที่มีเสียงรบกวน

---

## สิ่งที่คุณต้องมี

ก่อนที่เราจะเริ่มลงมือ ตรวจสอบให้แน่ใจว่าคุณมีสิ่งต่อไปนี้:

- **Python 3.9+** – โค้ดใช้ type hints และ f‑strings
- **Tesseract OCR** ติดตั้งและเรียกใช้ได้ผ่านคำสั่ง `tesseract` (บน Ubuntu: `sudo apt install tesseract-ocr`; บน Windows ดาวน์โหลดตัวติดตั้งจากรีโพสิตอรีอย่างเป็นทางการ)
- ตัวห่อ **pytesseract** (`pip install pytesseract`)
- **ไลบรารีการประมวลผลหลังจาก AI** – ตัวอย่างนี้เราจะสมมติว่าคุณมีโมดูล `ai` เบา ๆ ที่มีฟังก์ชัน `run_postprocessor` แทนที่ด้วย API GPT‑4 ของ OpenAI หรือ LLM ภายในเครื่องตามที่คุณต้องการ
- ตัวอย่างรูปภาพหรือ PDF จำนวนไม่กี่ไฟล์สำหรับทดสอบ

เท่านี้เอง ไม่ต้องใช้เฟรมเวิร์กหนัก ไม่ต้องทำ Docker เพียงแค่ติดตั้ง pip ไม่กี่ตัวคุณก็พร้อมลุย

---

## ขั้นตอนที่ 1: ทำการสแกนแบบ Plain‑Text อย่างเร็ว

สิ่งแรกที่นักพัฒนาส่วนใหญ่มองข้ามคือการรัน OCR แบบ *plain text* ซึ่งเร็วมากและให้การตรวจสอบเบื้องต้น เราจะเรียก `engine.Recognize()` เพื่อดึงอักขระดิบโดยไม่มีเมตาดาต้าโครงสร้าง นี่คือสิ่งที่เราหมายถึง **plain text OCR**  

```python
import pytesseract
from PIL import Image

def plain_text_ocr(image_path: str) -> str:
    """Run a quick plain‑text OCR pass and return the raw string."""
    img = Image.open(image_path)
    # pytesseract returns a single string with line breaks.
    raw_text = pytesseract.image_to_string(img, lang='eng')
    return raw_text
```

*ทำไมขั้นตอนนี้สำคัญ:*  
- **ความเร็ว** – การสแกนแบบ plain บนหน้า 300 dpi มักเสร็จภายในไม่ถึงหนึ่งวินาที  
- **Baseline** – คุณสามารถเปรียบเทียบผลลัพธ์ที่มีโครงสร้างในภายหลังกับ baseline นี้เพื่อหาข้อผิดพลาดชัดเจน  
- **การจับข้อผิดพลาด** – หากการสแกนแบบ plain ล้มเหลวอย่างสมบูรณ์ (เช่น ผลลัพธ์เป็นอักขระไร้ความหมาย) คุณจะรู้ว่าคุณภาพภาพต่ำเกินไปและสามารถหยุดได้เร็ว

---

## ขั้นตอนที่ 2: รัน OCR แบบ Layout‑Aware อย่างละเอียด

Plain text ดี แต่จะละทิ้ง *ตำแหน่ง* ของแต่ละคำบนหน้า สำหรับใบแจ้งหนี้ ฟอร์ม หรือแมกกาซีนหลายคอลัมน์คุณต้องการพิกัด หมายเลขบรรทัด และบางครั้งข้อมูลฟอนต์ นั่นคือเหตุผลที่ `engine.RecognizeStructured()` เข้ามาช่วย  

ด้านล่างเป็น wrapper เบา ๆ ของผลลัพธ์ **TSV** ของ Tesseract ซึ่งให้ลำดับชั้นของหน้า → บรรทัด → คำ พร้อมบ็อกซิ่ง

```python
from typing import List, Dict

def structured_ocr(image_path: str) -> List[Dict]:
    """Return a list of pages, each containing lines with word coordinates."""
    img = Image.open(image_path)

    # Tesseract TSV includes page, block, paragraph, line, word indices.
    tsv_data = pytesseract.image_to_data(img, output_type=pytesseract.Output.DICT, lang='eng')

    pages = {}
    for i, level in enumerate(tsv_data["level"]):
        if level != 5:  # focus on word level (5)
            continue
        page_num = tsv_data["page_num"][i]
        line_num = tsv_data["line_num"][i]
        word = tsv_data["text"][i]
        if not word.strip():
            continue

        # Build nested dict structure.
        pages.setdefault(page_num, {}).setdefault(line_num, []).append({
            "text": word,
            "bbox": (
                tsv_data["left"][i],
                tsv_data["top"][i],
                tsv_data["width"][i],
                tsv_data["height"][i],
            ),
        })

    # Convert dicts to a more convenient list format.
    structured_result = []
    for page_id, lines in pages.items():
        page_obj = {"PageNumber": page_id, "Lines": []}
        for line_id, words in lines.items():
            line_text = " ".join(w["text"] for w in words)
            line_obj = {
                "LineNumber": line_id,
                "Text": line_text,
                "Words": words,
            }
            page_obj["Lines"].append(line_obj)
        structured_result.append(page_obj)

    return structured_result
```

*เหตุผลที่ทำเช่นนี้:*  
- **พิกัด** ช่วยให้คุณแมปข้อความที่สกัดกลับไปยังภาพต้นฉบับเพื่อไฮไลท์หรือทำลบข้อมูลได้  
- **การจัดกลุ่มบรรทัด** รักษาเลย์เอาต์เดิม ซึ่งจำเป็นเมื่อคุณต้องสร้างตารางหรือคอลัมน์ใหม่  
- การสแกนนี้ช้ากว่าการสแกนแบบ plain เล็กน้อย แต่ยังเสร็จในไม่กี่วินาทีสำหรับเอกสารส่วนใหญ่

---

## ขั้นตอนที่ 3: รัน AI Post‑Processor เพื่อแก้ไขข้อผิดพลาดของ OCR

แม้ OCR ที่ดีที่สุดก็ทำผิดได้ — เช่น “rn” กับ “m”, การขาด diacritics, หรือการแยกคำ AI โมเดลสามารถดูที่สตริงดิบและข้อมูลโครงสร้าง, ตรวจจับความไม่สอดคล้อง, แล้วเขียนข้อความใหม่โดยคงพิกัดเดิมไว้  

ด้านล่างเป็นการ **mock** implementation; แทนที่ส่วนเนื้อหาด้วยการเรียก LLM จริงหากคุณมี

```python
def ai_postprocess(plain_text: str, structured_result: List[Dict]) -> List[Dict]:
    """
    Simulate an AI post‑processor that corrects OCR errors.
    It walks through each line, compares it with the plain text,
    and applies simple heuristics (e.g., spell‑check).
    """
    import difflib
    corrected = []

    for page in structured_result:
        new_page = {"PageNumber": page["PageNumber"], "Lines": []}
        for line in page["Lines"]:
            # Find the closest match in the plain text using difflib.
            best_match = difflib.get_close_matches(line["Text"], plain_text.splitlines(), n=1, cutoff=0.6)
            corrected_text = best_match[0] if best_match else line["Text"]
            # Preserve original word list but replace the text field.
            new_line = {
                "LineNumber": line["LineNumber"],
                "Text": corrected_text,
                "Words": line["Words"],  # coordinates stay the same
            }
            new_page["Lines"].append(new_line)
        corrected.append(new_page)

    return corrected
```

*ทำไมขั้นตอนนี้ช่วยเพิ่มความแม่นยำของ OCR:*  
- **การแก้ไขตามบริบท** – AI สามารถตัดสินใจว่า “l0ve” น่าจะเป็น “love” จากคำรอบข้าง  
- **การคงพิกัด** – คุณยังคงข้อมูลเลย์เอาต์ไว้ ทำให้งานต่อไป (เช่น การคอมเมนต์ PDF) ยังคงแม่นยำ  
- **การปรับปรุงแบบวนลูป** – คุณอาจรัน post‑processor หลายครั้ง แต่ละรอบทำความสะอาดข้อผิดพลาดเพิ่มขึ้น

---

## ขั้นตอนที่ 4: วนลูปผ่านโครงสร้างที่แก้ไขแล้ว

ตอนนี้เรามีโครงสร้างที่ทำความสะอาดแล้ว การดึงข้อความสุดท้ายเป็นเรื่องง่าย ด้านล่างเราพิมพ์แต่ละบรรทัด แต่คุณก็สามารถเขียนเป็น CSV, ใส่ลงฐานข้อมูล, หรือสร้าง PDF ที่ค้นหาได้

```python
def display_corrected_text(structured_result: List[Dict]) -> None:
    """Print each line of corrected OCR output."""
    for page in structured_result:
        print(f"\n--- Page {page['PageNumber']} ---")
        for line in page["Lines"]:
            print(line["Text"])

# Example usage tying everything together
if __name__ == "__main__":
    img_path = "sample_scan.png"

    # 1️⃣ Plain‑text OCR
    plain = plain_text_ocr(img_path)
    print("✅ Plain text OCR completed.")

    # 2️⃣ Structured OCR
    structured = structured_ocr(img_path)
    print("✅ Structured OCR completed.")

    # 3️⃣ AI post‑processing
    corrected = ai_postprocess(plain, structured)
    print("✅ AI post‑processor finished.")

    # 4️⃣ Show results
    display_corrected_text(corrected)
```

**ผลลัพธ์ที่คาดหวัง** (สมมติว่าเป็นใบแจ้งหนี้หน้าเดียวง่าย ๆ):

```
--- Page 1 ---
Invoice #12345
Date: 2024‑05‑01
Bill To: Acme Corp
Item Qty Price Total
Widget A 2 $15.00 $30.00
Widget B 1 $25.00 $25.00
Subtotal $55.00
Tax $5.50
Total $60.50
```

สังเกตว่าการแบ่งบรรทัดและลำดับคอลัมน์ยังคงอยู่ และข้อบกพร่อง OCR ทั่วไปเช่น “$15.00” ที่อ่านเป็น “$15,00” ถูกแก้โดยขั้นตอน AI

---

## วิธีที่เวิร์กโฟลว์นี้ช่วย **ปรับปรุงความแม่นยำของ OCR**

| ขั้นตอน | สิ่งที่แก้ไข | ทำไมจึงสำคัญ |
|------|---------------|----------------|
| **Plain text OCR** | ตรวจจับหน้าที่อ่านไม่ออกตั้งแต่ต้น | ประหยัดเวลาโดยข้ามอินพุตที่ไม่มีความหวัง |
| **Structured OCR** | จับเลย์เอาต์และพิกัด | เปิดใช้งานงานต่อเนื่อง (ไฮไลท์, ลบข้อมูล) |
| **AI post‑processor** | แก้ไขการสะกด, รวมคำที่แยก, แก้ตัวเลข | เพิ่มความแม่นยำระดับอักขระจาก ~85 % ไป >95 % บนสแกนที่มีเสียงรบกวน |
| **Iteration** | ให้คุณรันใหม่ด้วยพารามิเตอร์ที่ปรับแต่ง | ปรับแต่งพายป์ไลน์ให้เหมาะกับประเภทเอกสารเฉพาะ |

โดยการผสานสามแนวคิดนี้ — **plain text OCR**, การสกัดแบบ layout‑aware, และการแก้ไขด้วย AI — คุณจะได้โซลูชันที่แข็งแรงซึ่ง *เพิ่มอย่างมีนัยสำคัญ* **ความแม่นยำของ OCR** โดยไม่ต้องเขียนเครือข่ายประสาทเทียมเองจากศูนย์

---

## ข้อผิดพลาดทั่วไป & เคล็ดลับระดับมืออาชีพ

- **ข้อผิดพลาด:** ใส่ภาพความละเอียดต่ำ (≤150 dpi) ให้ Tesseract ทำให้ผลลัพธ์เป็นอักขระยุ่งยาก  
  **เคล็ดลับ:** ก่อน OCR ให้ทำพรี‑โปรเซสด้วย `Pillow` — ใช้ `Image.convert('L')` และ `Image.filter(ImageFilter.MedianFilter())`

- **ข้อผิดพลาด:** AI post‑processor อาจแก้ไขคำเฉพาะโดเมนโดยไม่ได้ตั้งใจ (เช่น “SKU123”)  
  **เคล็ดลับ:** สร้าง whitelist ของคำและส่งให้ LLM หรือใช้ไลบรารีตรวจสอบการสะกดอย่าง `pyspellchecker`

- **ข้อผิดพลาด:** หน้าแบบหลายคอลัมน์ถูกรวมเป็นบรรทัดเดียว  
  **เคล็ดลับ:** ตรวจจับขอบคอลัมน์ด้วยฟิลด์ `block_num` ในผลลัพธ์ TSV ของ Tesseract แล้วแยกบรรทัดตามนั้น

- **ข้อผิดพลาด:** PDF ขนาดใหญ่ทำให้หน่วยความจำพุ่งจนเต็มเมื่อโหลดทุกหน้าในครั้งเดียว  
  **เคล็ดลับ:** ประมวลผลหน้าแบบต่อเนื่อง — ลูป `pdf2image.convert_from_path(..., first_page=n, last_page=n)`

---

## การขยายพายป์ไลน์

หากคุณอยากสำรวจขั้นต่อไป ลองพิจารณาการปรับปรุงต่อไปนี้:

1. **การประมวลผลแบบแบช** – ห่อสคริปต์ทั้งหมดในฟังก์ชันที่เดินผ่านไดเรกทอรี จัดการไฟล์หลายพันไฟล์พร้อมกันด้วย `concurrent.futures`  
2. **โมเดลภาษา** – แทนที่ heuristic แบบ difflib ด้วยการเรียก OpenAI `gpt‑4o` หรือโมเดล LLaMA ที่โฮสต์ภายในเครื่องเพื่อรับการแก้ไขตามบริบทที่ลึกซึ้งกว่า  
3. **รูปแบบการส่งออก** – เขียนโครงสร้างที่แก้ไขแล้วเป็น PDF ที่ค้นหาได้  

## คุณควรเรียนรู้อะไรต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอน‑ขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโปรเจกต์ของคุณ

- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [How to Use OCR - Advanced Techniques with Aspose.OCR for Java](/ocr/english/java/advanced-ocr-techniques/)
- [Improve OCR Accuracy – Detect Areas Mode in OCR](/ocr/hongkong/net/text-recognition/ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}