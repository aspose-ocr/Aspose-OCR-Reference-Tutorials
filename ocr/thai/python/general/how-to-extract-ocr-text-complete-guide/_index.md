---
category: general
date: 2026-02-22
description: เรียนรู้วิธีดึงข้อความ OCR และปรับปรุงความแม่นยำของ OCR ด้วยการประมวลผลหลังจาก
  AI ทำความสะอาดข้อความ OCR อย่างง่ายใน Python ด้วยตัวอย่างทีละขั้นตอน.
draft: false
keywords:
- how to extract OCR
- improve OCR accuracy
- clean OCR text
- OCR post‑processing
- AI OCR enhancement
language: th
og_description: ค้นพบวิธีการสกัดข้อความ OCR ปรับปรุงความแม่นยำของ OCR และทำความสะอาดข้อความ
  OCR ด้วยเวิร์กโฟลว์ Python ง่าย ๆ พร้อมการประมวลผลหลังจาก AI
og_title: วิธีสกัดข้อความ OCR – คู่มือแบบขั้นตอนต่อขั้นตอน
tags:
- OCR
- AI
- Python
title: วิธีสกัดข้อความ OCR – คู่มือฉบับสมบูรณ์
url: /th/python/general/how-to-extract-ocr-text-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีดึงข้อความ OCR – การสอนโปรแกรมแบบครบถ้วน

เคยสงสัย **วิธีดึง OCR** จากเอกสารสแกนโดยไม่ต้องเจอข้อความที่เต็มไปด้วยการพิมพ์ผิดและบรรทัดที่ขาดหายหรือไม่? คุณไม่ได้เป็นคนเดียว ในหลายโครงการจริง ๆ ผลลัพธ์ดิบจากเครื่อง OCR มักดูเหมือนย่อหน้าที่สับสน และการทำความสะอาดมันรู้สึกเหมือนงานบ้าน  

ข่าวดีคืออะไร? ด้วยการทำตามคู่มือนี้ คุณจะได้เห็นวิธีที่เป็นประโยชน์ในการดึงข้อมูล OCR ที่มีโครงสร้าง, รัน AI post‑processor, และได้ **ข้อความ OCR ที่สะอาด** พร้อมสำหรับการวิเคราะห์ต่อไป เราจะพูดถึงเทคนิคเพื่อ **ปรับปรุงความแม่นยำของ OCR** เพื่อให้ผลลัพธ์เชื่อถือได้ตั้งแต่ครั้งแรก  

ในไม่กี่นาทีต่อไป เราจะครอบคลุมทุกสิ่งที่คุณต้องการ: ไลบรารีที่จำเป็น, สคริปต์ที่สามารถรันได้เต็มรูปแบบ, และเคล็ดลับเพื่อหลีกเลี่ยงข้อผิดพลาดทั่วไป ไม่ใช่การบอก “ดูเอกสาร” ที่คลุมเครือ—แต่เป็นโซลูชันครบถ้วนที่คุณสามารถคัดลอก‑วางและรันได้

## สิ่งที่คุณต้องเตรียม

- Python 3.9+ (โค้ดใช้ type hints แต่ทำงานได้บนเวอร์ชัน 3.x เก่า ๆ ด้วย)
- เครื่อง OCR ที่สามารถคืนผลลัพธ์ที่มีโครงสร้าง (เช่น Tesseract ผ่าน `pytesseract` พร้อมแฟล็ก `--psm 1` หรือ API เชิงพาณิชย์ที่ให้ข้อมูลบล็อก/บรรทัด)
- โมเดล AI post‑processing – ในตัวอย่างนี้เราจะจำลองด้วยฟังก์ชันง่าย ๆ แต่คุณสามารถเปลี่ยนเป็น `gpt‑4o-mini` ของ OpenAI, Claude, หรือ LLM ใด ๆ ที่รับข้อความและคืนผลลัพธ์ที่ทำความสะอาดแล้ว
- ตัวอย่างภาพหลายบรรทัด (PNG/JPG) สำหรับทดสอบ

หากคุณเตรียมพร้อมแล้ว ไปเริ่มกันเลย.

## วิธีดึง OCR – การดึงข้อมูลเบื้องต้น

ขั้นตอนแรกคือการเรียกใช้เครื่อง OCR และขอให้มันคืน **การแสดงผลที่มีโครงสร้าง** แทนการเป็นสตริงธรรมดา ผลลัพธ์ที่มีโครงสร้างจะรักษาขอบเขตของบล็อก, บรรทัด, และคำ ซึ่งทำให้การทำความสะอาดต่อมาง่ายขึ้นมาก.

```python
import pytesseract
from PIL import Image
from dataclasses import dataclass, field
from typing import List

# Simple data classes mirroring a typical structured OCR response
@dataclass
class Line:
    text: str

@dataclass
class Block:
    lines: List[Line] = field(default_factory=list)

@dataclass
class StructuredResult:
    blocks: List[Block] = field(default_factory=list)

def recognize_structured(image_path: str) -> StructuredResult:
    """
    Run Tesseract with the `--psm 1` layout mode to get block/line info.
    In a real engine you would get JSON directly; here we simulate it.
    """
    img = Image.open(image_path)

    # Tesseract's TSV output includes level, page_num, block_num, par_num, line_num, word_num, text…
    tsv = pytesseract.image_to_data(img, output_type=pytesseract.Output.DICT)

    result = StructuredResult()
    current_block_idx = -1
    current_line_idx = -1

    for i, level in enumerate(tsv["level"]):
        if level == 3:  # block level
            result.blocks.append(Block())
            current_block_idx += 1
            current_line_idx = -1
        elif level == 4:  # line level
            result.blocks[current_block_idx].lines.append(Line(text=""))
            current_line_idx += 1

        # level 5 is word; concatenate words into the current line
        if level == 5:
            word = tsv["text"][i]
            if word.strip():
                line_obj = result.blocks[current_block_idx].lines[current_line_idx]
                line_obj.text += (word + " ")

    # Trim trailing spaces
    for block in result.blocks:
        for line in block.lines:
            line.text = line.text.strip()
    return result
```

> **Why this matters:** ด้วยการรักษาบล็อกและบรรทัด เราจะหลีกเลี่ยงการต้องเดาว่าพารากราฟเริ่มต้นที่ไหน ฟังก์ชัน `recognize_structured` ให้เรามีโครงสร้างที่สะอาดซึ่งเราสามารถส่งต่อให้โมเดล AI ได้ในภายหลัง.

```python
# Demo call – replace with your own image path
structured_result = recognize_structured("sample_scan.png")
print("Before AI:", structured_result.blocks[0].lines[0].text)
```

การรันสคริปต์นี้จะแสดงบรรทัดแรกตามที่เครื่อง OCR เห็น ซึ่งมักมีการจดจำผิด เช่น “0cr” แทน “OCR”.

## ปรับปรุงความแม่นยำของ OCR ด้วย AI Post‑Processing

เมื่อเรามีผลลัพธ์ที่มีโครงสร้างดิบแล้ว ให้ส่งต่อไปยัง AI post‑processor เป้าหมายคือ **ปรับปรุงความแม่นยำของ OCR** ด้วยการแก้ไขข้อผิดพลาดทั่วไป, ทำให้เครื่องหมายวรรคตอนเป็นมาตรฐาน, และแม้กระทั่งทำการแบ่งบรรทัดใหม่เมื่อจำเป็น.

```python
import openai  # Example: using OpenAI's API; replace with your provider

def run_postprocessor(structured: StructuredResult) -> StructuredResult:
    """
    Sends each line to an LLM that returns a cleaned version.
    This simple loop can be parallelized for large documents.
    """
    api_key = "YOUR_OPENAI_API_KEY"
    openai.api_key = api_key

    for block in structured.blocks:
        for line in block.lines:
            prompt = (
                "You are an OCR cleanup assistant. Fix any spelling, spacing, "
                "or punctuation errors in the following line while preserving the original meaning:\n\n"
                f"\"{line.text}\""
            )
            response = openai.ChatCompletion.create(
                model="gpt-4o-mini",
                messages=[{"role": "user", "content": prompt}],
                temperature=0.0,
                max_tokens=200,
            )
            cleaned = response.choices[0].message.content.strip()
            line.text = cleaned
    return structured
```

> **Pro tip:** หากคุณไม่มีการสมัครสมาชิก LLM คุณสามารถเปลี่ยนการเรียกใช้เป็น transformer ภายในเครื่อง (เช่น `sentence‑transformers` + โมเดลแก้ไขที่ฝึกเพิ่มเติม) หรือแม้กระทั่งวิธีการแบบ rule‑based แนวคิดหลักคือ AI จะมองแต่ละบรรทัดแยกจากกัน ซึ่งมักเพียงพอที่จะ **ทำความสะอาดข้อความ OCR**.

```python
# Apply the AI post‑processor
structured_result = run_postprocessor(structured_result)
print("After AI:", structured_result.blocks[0].lines[0].text)
```

ตอนนี้คุณควรเห็นประโยคที่สะอาดกว่ามาก—การพิมพ์ผิดถูกแทนที่, ช่องว่างส่วนเกินถูกลบ, และเครื่องหมายวรรคตอนถูกแก้ไข.

## ทำความสะอาดข้อความ OCR เพื่อผลลัพธ์ที่ดีกว่า

แม้หลังจากการแก้ไขด้วย AI แล้ว คุณอาจต้องการทำขั้นตอนการทำความสะอาดสุดท้าย: ลบอักขระที่ไม่ใช่ ASCII, ทำให้การขึ้นบรรทัดเป็นมาตรฐาน, และลบช่องว่างหลายช่องให้เป็นหนึ่งช่อง การทำขั้นตอนเพิ่มเติมนี้ทำให้ผลลัพธ์พร้อมสำหรับงานต่อไป เช่น NLP หรือการนำเข้าฐานข้อมูล.

```python
import re

def final_cleanup(structured: StructuredResult) -> str:
    """
    Flattens the hierarchy into a single string and performs
    additional regex‑based cleaning.
    """
    lines = []
    for block in structured.blocks:
        for line in block.lines:
            # Remove any lingering non‑printable characters
            cleaned = re.sub(r"[^\x20-\x7E]", "", line.text)
            # Collapse multiple spaces
            cleaned = re.sub(r"\s+", " ", cleaned).strip()
            lines.append(cleaned)
    # Join blocks with double newline to preserve paragraph breaks
    return "\n\n".join(lines)

clean_text = final_cleanup(structured_result)
print("\n=== Cleaned OCR Text ===\n")
print(clean_text)
```

`final_cleanup` ฟังก์ชันจะให้สตริงธรรมดาที่คุณสามารถส่งต่อเข้าไปยังดัชนีการค้นหา, โมเดลภาษา, หรือการส่งออก CSV ได้โดยตรง เนื่องจากเรารักษาขอบเขตของบล็อกไว้ โครงสร้างของพารากราฟจึงยังคงอยู่.

## กรณีขอบและสถานการณ์ที่อาจเกิดขึ้น

- **รูปแบบหลายคอลัมน์:** หากแหล่งข้อมูลของคุณมีคอลัมน์, เครื่อง OCR อาจสลับบรรทัดกัน คุณสามารถตรวจจับพิกัดคอลัมน์จากผลลัพธ์ TSV และจัดเรียงบรรทัดใหม่ก่อนส่งให้ AI.
- **สคริปต์ที่ไม่ใช่ละติน:** สำหรับภาษาต่าง ๆ เช่น จีนหรืออาหรับ ให้เปลี่ยน prompt ของ LLM เพื่อขอการแก้ไขเฉพาะภาษา, หรือใช้โมเดลที่ฝึกเฉพาะสคริปต์นั้น.
- **เอกสารขนาดใหญ่:** การส่งแต่ละบรรทัดแยกกันอาจช้า ให้ทำการจัดกลุ่มบรรทัด (เช่น 10 บรรทัดต่อคำขอ) แล้วให้ LLM คืนรายการบรรทัดที่ทำความสะอาดแล้ว จำไว้ว่าต้องคำนึงถึงขีดจำกัดโทเคน.
- **บล็อกหายไป:** บางเครื่อง OCR คืนรายการคำแบบแบนราบเท่านั้น ในกรณีนั้นคุณสามารถสร้างบรรทัดใหม่โดยจัดกลุ่มคำที่มีค่า `line_num` คล้ายกัน.

## ตัวอย่างการทำงานเต็มรูปแบบ

เมื่อรวมทุกอย่างเข้าด้วยกัน นี่คือไฟล์เดียวที่คุณสามารถรันจากต้นจนจบ แทนที่ตัวแปรตำแหน่งด้วย API key และเส้นทางภาพของคุณเอง.

```python
# ocr_cleanup.py
import re
import pytesseract
from PIL import Image
from dataclasses import dataclass, field
from typing import List
import openai

# ---------- Data structures ----------
@dataclass
class Line:
    text: str

@dataclass
class Block:
    lines: List[Line] = field(default_factory=list)

@dataclass
class StructuredResult:
    blocks: List[Block] = field(default_factory=list)

# ---------- Step 1: Extract OCR ----------
def recognize_structured(image_path: str) -> StructuredResult:
    img = Image.open(image_path)
    tsv = pytesseract.image_to_data(img, output_type=pytesseract.Output.DICT)

    result = StructuredResult()
    cur_block = -1
    cur_line = -1

    for i, lvl in enumerate(tsv["level"]):
        if lvl == 3:                # block
            result.blocks.append(Block())
            cur_block += 1
            cur_line = -1
        elif lvl == 4:              # line
            result.blocks[cur_block].lines.append(Line(text=""))
            cur_line += 1
        elif lvl == 5:              # word
            word = tsv["text"][i]
            if word.strip():
                result.blocks[cur_block].lines[cur_line].text += word + " "

    # Trim spaces
    for blk in result.blocks:
        for ln in blk.lines:
            ln.text = ln.text.strip()
    return result

# ---------- Step 2: AI post‑processor ----------
def run_postprocessor(structured: StructuredResult) -> StructuredResult:
    openai.api_key = "YOUR_OPENAI_API_KEY"
    for block in structured.blocks:
        for line in block.lines:
            prompt = (
                "Correct OCR errors (spelling, spacing, punctuation) in this line:\n"
                f"\"{line.text}\""
            )
            resp = openai.ChatCompletion.create(
                model="gpt-4o-mini",
                messages=[{"role": "user", "content": prompt}],
                temperature=0.0,
                max_tokens=150,
            )
            line.text = resp.choices[0].message.content.strip()
    return structured

# ---------- Step 3: Final cleanup ----------
def final_cleanup(structured: StructuredResult) -> str:
    out = []
    for block in structured.blocks:
        for line in block.lines:
            txt = re.sub(r"[^\x20-\x7E]", "", line.text)   # strip non‑ASCII
            txt = re.sub(r"\s+", " ", txt).strip

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}