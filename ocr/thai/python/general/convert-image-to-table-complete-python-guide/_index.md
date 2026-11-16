---
category: general
date: 2026-03-26
description: แปลงภาพเป็นตารางด้วย Python โดยใช้ OCR และ AI. เรียนรู้วิธีดึงตารางจากภาพ
  ปรับปรุงความแม่นยำของ OCR และรับผลลัพธ์ที่เป็นโครงสร้างอย่างรวดเร็ว.
draft: false
keywords:
- convert image to table
- extract table from image
- extract tabular data image
- enhance OCR accuracy
language: th
og_description: แปลงภาพเป็นตารางใน Python คู่มือนี้แสดงวิธีการดึงตารางจากภาพ เพิ่มความแม่นยำของ
  OCR และทำงานกับข้อมูลที่มีโครงสร้าง
og_title: แปลงรูปภาพเป็นตาราง – บทเรียน Python ทีละขั้นตอน
tags:
- OCR
- Python
- AI post‑processing
title: แปลงรูปภาพเป็นตาราง – คู่มือ Python ฉบับสมบูรณ์
url: /th/python/general/convert-image-to-table-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# แปลงรูปภาพเป็นตาราง – คู่มือ Python ฉบับสมบูรณ์

เคยต้อง **แปลงรูปภาพเป็นตาราง** แต่รู้สึกติดขัดอยู่หน้าภาพหน้าจอที่เบลอหรือไม่? คุณไม่ได้เป็นคนเดียว ในหลายโครงการที่ขับเคลื่อนด้วยข้อมูล วิธีที่เร็วที่สุดในการนำตัวเลขเข้าสู่ DataFrame คือการถ่ายรูปตารางที่พิมพ์ออกมาแล้วให้สคริปต์ทำงานหนักให้ ข่าวดีคือ? ด้วยเครื่องมือ OCR สมัยใหม่ที่ผสานกับ AI post‑processor ขนาดเล็ก คุณสามารถดึงตารางที่สะอาดและมีโครงสร้างออกจากเกือบทุกภาพได้

ในบทแนะนำนี้เราจะเดินผ่าน **ตัวอย่างจากโลกจริงที่สกัดข้อมูลตารางจากรูปภาพ** ทำความสะอาด และพิมพ์แต่ละแถวเป็นข้อความธรรมดา เมื่อจบคุณจะเข้าใจวิธี **enhance OCR accuracy** จัดการกับข้อผิดพลาดทั่วไป และปรับโค้ดให้เข้ากับไพป์ไลน์ของคุณเอง ไม่ต้องใช้เวทมนตร์ เพียง Python ไลบรารีบางตัวและการให้เหตุผลเล็กน้อย

> **สิ่งที่คุณต้องการ**  
> * Python 3.9+  
> * ไลบรารี OCR ที่รองรับ `OutputFormat.Structured` (เช่น `myocr`)  
> * AI post‑processor ทางเลือก (อาจเป็น transformer ขนาดเบา หรือฟังก์ชันแบบ rule‑based)  
> * ตัวอย่างไฟล์รูปภาพ (`table.png`) ที่มีตารางง่าย ๆ

---

## ขั้นตอนที่ 1: แปลงรูปภาพเป็นตาราง – จดจำภาพด้วยผลลัพธ์แบบโครงสร้าง

สิ่งแรกที่เราทำคือส่งภาพไปยังเครื่องมือ OCR แล้วขอผลลัพธ์แบบ **structured** ผลลัพธ์แบบโครงสร้างหมายความว่าเครื่องมือพยายามสรุปแถว คอลัมน์ และขอบเซลล์แทนการคืนสตริงแบน

```python
import myocr as ocr          # Hypothetical OCR package
import myengine as engine    # Wrapper around the OCR engine
import myai as ai            # Simple AI post‑processor

def recognize_image(path: str):
    """
    Sends the image to the OCR engine and asks for a tabular
    (structured) representation.
    """
    # Step 1: Recognize the image and request a structured (tabular) result
    structured_result = engine.recognize_image(
        path,
        output_format=ocr.OutputFormat.Structured
    )
    return structured_result
```

**ทำไมเรื่องนี้ถึงสำคัญ:**  
ถ้าคุณขอ OCR ให้คืนข้อความธรรมดา คุณจะได้อักขระกระจัดกระจายโดยไม่มีแนวคิดของแถวหรือคอลัมน์ การขอรูปแบบโครงสร้างทำให้เครื่องมือทำงานหนักด้านการตรวจจับบรรทัด การจัดแนวคอลัมน์ และแม้กระทั่งการรวมเซลล์พื้นฐาน ซึ่งลดจำนวนการแยกวิเคราะห์ด้วยมือที่คุณต้องทำในภายหลังอย่างมาก

> **เคล็ดลับ:** ตรวจสอบให้แน่ใจว่าภาพมีคอนทราสต์ดีและเอียงน้อย การสแกนที่ 300 dpi มักให้ผลลัพธ์ที่ดีที่สุด

---

## ขั้นตอนที่ 2: ปรับปรุงความแม่นยำของ OCR – ประมวลผลหลังโครงสร้างดิบ

OCR ไม่สมบูรณ์—โดยเฉพาะเมื่อภาพต้นทางมีเส้นที่บอบบางหรือฟอนต์แปลก ๆ นั่นคือจุดที่ AI ขนาดเบา (หรือแม้แต่สคริปต์แบบ rule‑based) สามารถทำความสะอาดผลลัพธ์ แก้ไขการรับรู้ผิดพลาดทั่วไป และเติมบริบทที่ขาดหายไป

```python
def enhance_structure(structured_result):
    """
    Runs a post‑processor that fixes typical OCR errors
    (e.g., 'O' vs '0', merged cells) and adds semantic context.
    """
    # Step 2: Enhance the raw OCR structure with AI (adds context, corrects errors)
    enhanced_structure = ai.run_postprocessor(structured_result)
    return enhanced_structure
```

**ทำไมเรื่องนี้ถึงสำคัญ:**  
ตาราง OCR ดิบอาจระบุหัวตารางเป็น “Q1 2022” แต่อ่านเลข “1” เป็น “l” AI ชั้นนี้สามารถเรียนรู้รูปแบบเหล่านี้จากชุดฝึกขนาดเล็กและส่งออกตารางที่สะอาดขึ้น แม้แต่การใช้กฎง่าย ๆ (แทนที่ “l” ที่โดดเดี่ยวด้วย “1” เมื่ออยู่ระหว่างตัวเลข) ก็สามารถเพิ่ม **enhance OCR accuracy** อย่างมาก

> **กรณีขอบที่พบบ่อย:** หากตารางมีเซลล์ที่รวมกัน OCR อาจทำสำเนาเนื้อหาไปยังคอลัมน์หลาย ๆ คอลัมน์ post‑processor ควรตรวจจับเซลล์ที่เหมือนกันติดกันและรวมเข้าด้วยกัน

---

## ขั้นตอนที่ 3: สกัดข้อมูลตารางจากรูปภาพ – วนลูปผ่านแถวและแสดงข้อความเซลล์

เมื่อเรามีโครงสร้างที่เรียบร้อย การสกัดข้อมูลก็ง่ายดาย เราจะวนลูปผ่านตารางที่ตรวจจับได้แรกและพิมพ์แต่ละแถวเป็นรายการค่าของเซลล์

```python
def print_table(enhanced_structure):
    """
    Prints each row of the first detected table.
    """
    # Step 3: Iterate over the rows of the first detected table and display cell text
    for row in enhanced_structure.tables[0].rows:
        print([cell.text for cell in row.cells])

if __name__ == "__main__":
    # Path to your image file
    image_path = "YOUR_DIRECTORY/table.png"

    # Run the pipeline
    raw = recognize_image(image_path)
    cleaned = enhance_structure(raw)
    print_table(cleaned)
```

**สิ่งที่คุณจะเห็น:**  
สมมติว่า `table.png` มีตารางง่าย 3 × 2 ผลลัพธ์อาจเป็นดังนี้:

```
['Product', 'Price']
['Apple', '$1.20']
['Banana', '$0.80']
```

หาก OCR พลาดหัวตาราง AI post‑processor จะใส่หัวตารางเข้ามาตามบริบทโดยรอบ ดังนั้นตารางสุดท้ายพร้อมใช้กับ pandas หรือการวิเคราะห์ต่อไป

> **ระวัง:** แถวว่างที่ส่วนท้ายของตารางบาง OCR จะเพิ่มแถวเปล่าตอนเจอช่องว่าง การใช้เงื่อนไข `if any(cell.text for cell in row.cells):` จะกรองแถวเหล่านี้ออกได้อย่างรวดเร็ว

---

## โบนัส: ไปไกลกว่านั้น – บันทึกตารางเป็น CSV หรือ DataFrame

หลายเวิร์กโฟลว์จริงต้องการข้อมูลในไฟล์ CSV หรือ DataFrame ของ pandas นี่คือตัวอย่างสั้น ๆ ที่แปลงแถวที่พิมพ์ออกเป็น CSV โดยไม่ต้องออกจากกระบวนการ Python

```python
import csv
import pandas as pd

def save_to_csv(enhanced_structure, output_path="output.csv"):
    rows = [
        [cell.text for cell in row.cells]
        for row in enhanced_structure.tables[0].rows
        if any(cell.text for cell in row.cells)  # Skip empty rows
    ]
    # Write CSV
    with open(output_path, "w", newline="", encoding="utf-8") as f:
        writer = csv.writer(f)
        writer.writerows(rows)

    # Also return a DataFrame for immediate use
    return pd.DataFrame(rows[1:], columns=rows[0])  # Assume first row is header

# Example usage:
df = save_to_csv(cleaned, "my_table.csv")
print(df.head())
```

ตอนนี้คุณมี DataFrame พร้อมใช้ เหมาะสำหรับการวิเคราะห์ การสร้างภาพ หรือการป้อนเข้าสู่โมเดล Machine‑Learning

---

## คำถามที่พบบ่อย (FAQ)

**Q: วิธีนี้ทำงานกับ PDF ที่มีตารางสแกนได้หรือไม่?**  
A: ทำได้แน่นอน—แค่แปลงแต่ละหน้า PDF เป็นภาพ (เช่น ใช้ `pdf2image`) แล้วส่ง PNG ที่ได้เข้าสู่ไพป์ไลน์เดียวกัน

**Q: ตารางของฉันมีเซลล์หัวที่รวมกัน AI จะจัดการได้หรือไม่?**  
A: post‑processor ที่ฝึกอย่างดีสามารถตรวจจับเซลล์ที่รวมกันโดยตรวจสอบ span ของเซลล์ หากใช้วิธี rule‑based ให้มองหาเนื้อหาเดียวกันในเซลล์ติดกันแล้วรวมเข้าด้วยกัน

**Q: ถ้า OCR คืนหลายตารางจะทำอย่างไร?**  
A: `enhanced_structure.tables` เป็นรายการ คุณสามารถวนลูปผ่านหรือเลือกตารางที่มีแถว/คอลัมน์มากที่สุด—ตามที่คุณคาดหวัง

**Q: ฉันสามารถแทนที่ AI post‑processor ด้วยการทำความสะอาดด้วย regex ธรรมดาได้หรือไม่?**  
A: ได้ สำหรับหลายโครงการการแทนที่ด้วย regex เพียงไม่กี่ตัว (เช่น แก้ “O” → “0”) ก็มากพอแล้ว สิ่งสำคัญคือให้มีขั้นตอน *หลัง OCR* เพื่อปรับปรุง **enhance OCR accuracy**

---

## สรุป

เราได้แสดงวิธี **แปลงรูปภาพเป็นตาราง** ด้วย Python ตั้งแต่การรับรู้ OCR ดิบจนถึงการปรับปรุงด้วย AI และโครงสร้างข้อมูลที่พร้อมใช้ กระบวนการสามขั้นตอน—จดจำ, ปรับปรุง, สกัด—ครอบคลุมความท้าทายหลักของ **extract table from image** และแสดงวิธีปฏิบัติที่ทำให้ **enhance OCR accuracy** ได้จริง

จับภาพหน้าจอสเปรดชีตใด ๆ ชี้สคริปต์ไปที่มัน แล้วคุณจะได้ CSV หรือ DataFrame ในไม่กี่วินาที จากนี้คุณสามารถสำรวจเทคนิคขั้นสูงเพิ่มเติม: PDF หลายหน้า, ตารางเขียนมือ, หรือแม้กระทั่งฟีดกล้องแบบเรียลไทม์

พร้อมรับความท้าทายต่อไปหรือยัง? ลองให้ไพป์ไลน์ทำงานกับเฟรมวิดีโอสด หรือทดลอง post‑processor ที่ใช้โมเดลภาษาเพื่อสรุปชื่อคอลัมน์ที่หายไป ท้องฟ้าคือขอบเขต และตอนนี้คุณมีพื้นฐานที่มั่นคงเพื่อสร้างต่อ

ขอให้สนุกกับการเขียนโค้ด! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}