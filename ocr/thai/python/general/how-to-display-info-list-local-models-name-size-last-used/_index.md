---
category: general
date: 2026-01-12
description: เรียนรู้วิธีแสดงข้อมูลจาก AsposeAI โดยการแสดงรายการโมเดลในเครื่อง พร้อมชื่อโมเดล
  ขนาด และเวลาที่ใช้ครั้งล่าสุดในตัวอย่าง Python ที่ชัดเจน
draft: false
keywords:
- how to display info
- list local models
- display model name
- show model size
- show last used
language: th
og_description: 'วิธีแสดงข้อมูลจาก AsposeAI: แสดงรายการโมเดลในเครื่อง, แสดงชื่อโมเดล,
  ขนาด, และเวลาที่ใช้ครั้งสุดท้าย พร้อมขั้นตอนการทำงานด้วย Python อย่างครบถ้วน'
og_title: วิธีแสดงข้อมูล – รายการโมเดลในเครื่อง, ชื่อ, ขนาด, ครั้งสุดท้ายที่ใช้
tags:
- AsposeAI
- Python
- Model Management
title: วิธีแสดงข้อมูล – รายการโมเดลในเครื่อง, ชื่อ, ขนาด, การใช้งานล่าสุด
url: /th/python/general/how-to-display-info-list-local-models-name-size-last-used/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีแสดงข้อมูล – รายการโมเดลในเครื่อง, ชื่อ, ขนาด, ครั้งสุดท้ายที่ใช้

เคยสงสัย **วิธีแสดงข้อมูล** จากการติดตั้ง AsposeAI ของคุณโดยไม่ต้องค้นหาผ่านบันทึกหรือ UI หรือไม่? คุณไม่ได้เป็นคนเดียว ในหลาย ๆ pipeline ของ data‑science สิ่งแรกที่คุณต้องการคือการมองอย่างรวดเร็วว่าโมเดลใดบ้างที่อยู่บนเครื่องของคุณ ชื่ออะไร มีขนาดเท่าไหร่ และคุณใช้มันครั้งสุดท้ายเมื่อไหร่

นี่แหละคือสิ่งที่เราจะครอบคลุม: ตัวอย่างโค้ด Python สั้น ๆ ที่ **แสดงรายการโมเดลในเครื่อง**, จากนั้น **แสดงชื่อโมเดล**, **แสดงขนาดโมเดล**, และ **แสดงเวลาที่ใช้ครั้งสุดท้าย** ไม่ต้องใช้ไลบรารีภายนอก ไม่ต้องมีเวทมนตร์ลับ—เพียงแค่ AsposeAI client ที่คุณมีอยู่แล้ว

เมื่อจบบทเรียนนี้ คุณจะสามารถคัดลอกโค้ดไปใส่ในสคริปต์ใดก็ได้ รันมัน แล้วได้ตารางที่เรียบร้อยของโมเดลที่เก็บไว้ในเครื่องของคุณทันที เหมาะสำหรับการตรวจสอบสภาพแวดล้อม, สร้างแดชบอร์ดสุขภาพ, หรือเพียงแค่ตอบสนองความอยากรู้ว่ามีอะไรซ่อนอยู่บนดิสก์

## ข้อกำหนดเบื้องต้น

- Python 3.8 หรือใหม่กว่า (ตัวอย่างใช้ f‑strings ดังนั้นต้องเป็น 3.6+)
- ติดตั้งแพคเกจ `asposeai` (`pip install asposeai`)
- มีใบอนุญาต AsposeAI ที่ทำงานได้หรือคีย์ทดลอง (client จะดึงข้อมูลรับรองจากตัวแปรสภาพแวดล้อมหรือไฟล์ config)

ถ้าคุณได้ทำตามข้อเหล่านี้แล้ว เยี่ยม—มาเริ่มกันเลย

## ขั้นตอนที่ 1: วิธีแสดงข้อมูล – เริ่มต้น AsposeAI Client

ก่อนที่เราจะ **แสดงรายการโมเดลในเครื่อง**, เราต้องมีอ็อบเจกต์ client ที่สื่อสารกับ runtime ของ AsposeAI ขั้นตอนนี้เป็นพื้นฐาน; หากไม่มี client โค้ดส่วนอื่นจะทำให้เกิด `NameError`

```python
# Step 1: Create an instance of the AsposeAI client
# The client automatically reads credentials from the environment
aspose_ai = AsposeAI()
```

*ทำไมขั้นตอนนี้สำคัญ*: การเริ่มต้น client จะสร้างเซสชันกับเครื่องยนต์ inference ในเครื่อง, โหลดไลบรารีเนทีฟที่จำเป็น และตรวจสอบว่าใบอนุญาตของคุณยังใช้งานได้อยู่ เพื่อป้องกันข้อผิดพลาดที่ไม่ชัดเจนเมื่อคุณพยายาม query โมเดล

> **เคล็ดลับ**: หากคุณรันบนเซิร์ฟเวอร์ CI ให้ตั้งค่า `ASPOSEAI_LICENSE` ใน environment เพื่อให้ client เริ่มทำงานได้โดยไม่ต้องมี prompt แบบโต้ตอบ

## ขั้นตอนที่ 2: รายการโมเดลในเครื่อง – ดึงโมเดลที่มีอยู่

ตอนนี้ client พร้อมแล้ว เราสามารถ **แสดงรายการโมเดลในเครื่อง** ได้ เมธอด `list_local()` จะคืนคอลเลกชันของอ็อบเจกต์, แต่ละอ็อบเจกต์มีคุณสมบัติเช่น `name`, `size_mb`, และ `last_used`

```python
# Step 2: Retrieve the list of locally available models
local_models = aspose_ai.list_local()
```

*สิ่งที่เกิดขึ้นเบื้องหลัง*: `list_local()` สแกนไดเรกทอรีที่ AsposeAI แคชไฟล์โมเดล (`~/.asposeai/models` เป็นค่าเริ่มต้น) แล้วสร้างอ็อบเจกต์เมตาดาต้าแบบเบา ๆ การทำงานนี้เร็วเพราะไม่ได้โหลดน้ำหนักโมเดล—เพียงอ่านไฟล์ JSON manifest ขนาดเล็ก

หากคุณเคยสงสัยว่าโมเดลใดถูกแคชไว้แล้วหรือไม่ การเรียกนี้เป็นวิธีที่เร็วที่สุดในการยืนยัน

## ขั้นตอนที่ 3: แสดงชื่อโมเดล, แสดงขนาดโมเดล, และแสดงครั้งสุดท้ายที่ใช้

เมื่อได้โมเดลมาในมือ เราจะ **แสดงข้อมูล** โดยวนลูปผ่านคอลเลกชันและพิมพ์แต่ละแอตทริบิวต์ ที่นี่เราจะ **แสดงชื่อโมเดล**, **แสดงขนาดโมเดล**, และ **แสดงครั้งสุดท้ายที่ใช้** ทั้งหมดในบรรทัดเดียวที่เรียบร้อย

```python
# Step 3: Print each model's name, size (in MB), and last‑used timestamp
print("Available local models:")
print("-" * 50)
for model_info in local_models:
    # Using an f‑string to format the output cleanly
    print(f"{model_info.name} – {model_info.size_mb} MB – last used {model_info.last_used}")
```

**ผลลัพธ์ที่คาดหวัง** (เวลาที่แสดงอาจแตกต่าง)

```
Available local models:
--------------------------------------------------
gpt‑tiny‑en – 120 MB – last used 2025-11-02 14:23:11
bert‑base‑fr – 420 MB – last used 2025-10-18 09:07:45
whisper‑large‑audio – 1580 MB – last used 2025-09-30 22:41:02
```

*ทำไมเราจัดรูปแบบแบบนี้*: เครื่องหมายขีด (`–`) แยกฟิลด์เพื่อความอ่านง่าย, และบรรทัดหัวเรื่องทำให้ผลลัพธ์ในคอนโซลสแกนได้ง่าย หากคุณต้องการรูปแบบที่เครื่องอ่านได้ในภายหลัง (CSV, JSON) คุณสามารถเปลี่ยน `print` เป็น `writer.writerow` หรือ `json.dump` ได้อย่างง่ายดาย

### การจัดการกรณีขอบ

- **ไม่มีโมเดลที่แคชไว้** – `list_local()` คืนรายการว่าง ลูปจะข้ามไปโดยไม่มีอะไรพิมพ์ นอกจากหัวเรื่อง คุณอาจต้องเพิ่มการตรวจสอบ:

  ```python
  if not local_models:
      print("No local models found. Use aspose_ai.download(...) to fetch one.")
  ```

- **ขาดคุณสมบัติบางอย่าง** – ในกรณีที่ manifest เสียหาย การเข้าถึง `model_info.last_used` อาจทำให้เกิด `AttributeError` ให้ใส่โค้ด `print` ไว้ใน `try/except` หากคาดว่าจะเจอปัญหาแบบนี้

- **ไดเรกทอรีโมเดลขนาดใหญ่** – หากมีโมเดลหลายร้อยตัว ควรพิจารณาแบ่งหน้าแสดงผลหรือเขียนลงไฟล์แทนการพิมพ์ลงคอนโซล

## สรุปภาพรวม (ตัวเลือก)

หากคุณต้องการสัญญาณภาพเร็ว ๆ แผนภาพด้านล่างแสดงกระบวนการจากการเริ่มต้น client ไปจนถึงการแสดงผลสุดท้าย  

![แผนภาพแสดงวิธีแสดงข้อมูลจาก AsposeAI client](/images/how-to-display-info.png "แผนภาพวิธีแสดงข้อมูล")

*ข้อความแทน*: **วิธีแสดงข้อมูล** – แผนผังของการเริ่มต้น AsposeAI client, การแสดงรายการโมเดล, และการแสดงข้อมูล

## สคริปต์ทำงานเต็มรูปแบบ

รวมทุกอย่างเข้าด้วยกัน นี่คือสคริปต์ที่สมบูรณ์และพร้อมรัน:

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

"""
How to display info from AsposeAI:
List local models and show each model's name, size, and last‑used timestamp.
"""

from asposeai import AsposeAI

def main():
    # Initialize client
    aspose_ai = AsposeAI()

    # Retrieve local models
    local_models = aspose_ai.list_local()

    # Header
    print("Available local models:")
    print("-" * 50)

    if not local_models:
        print("No local models found. Use aspose_ai.download(...) to fetch one.")
        return

    # Display each model's details
    for model_info in local_models:
        try:
            print(f"{model_info.name} – {model_info.size_mb} MB – last used {model_info.last_used}")
        except AttributeError:
            # Fallback if any attribute is missing
            print(f"{model_info.name} – info incomplete")

if __name__ == "__main__":
    main()
```

บันทึกไฟล์นี้เป็น `list_models.py`, ทำให้เป็นไฟล์ที่เรียกใช้ได้ (`chmod +x list_models.py`), แล้วรัน:

```bash
./list_models.py
```

คุณจะเห็นรายการที่เรียบร้อยตามที่แสดงไว้ก่อนหน้า

## สรุป

เราได้อธิบาย **วิธีแสดงข้อมูล** จาก AsposeAI โดย **แสดงรายการโมเดลในเครื่อง**, จากนั้น **แสดงชื่อโมเดล**, **แสดงขนาดโมเดล**, และ **แสดงครั้งสุดท้ายที่ใช้** เวลาต่าง ๆ วิธีนี้เบา, ต้องการเพียงแพคเกจ `asposeai` มาตรฐาน, และสามารถนำไปใช้ใน pipeline automation หรือเซสชันดีบักใดก็ได้

ต่อจากนี้คุณอาจ:

- ส่งออกผลลัพธ์เป็น CSV เพื่อวิเคราะห์ในสเปรดชีต (`csv` module)
- นำเวลาที่ได้ไปใส่ในแดชบอร์ดมอนิเตอร์เพื่อแจ้งเตือนโมเดลที่ไม่ได้ใช้มานาน
- ผสานสคริปต์นี้กับ `aspose_ai.download()` เพื่อรีเฟรชโมเดลที่ไม่ได้ใช้เป็นระยะเวลา

จำไว้ว่า การมองเห็นสต็อกโมเดลอย่างชัดเจนช่วยประหยัดเวลา, ลดปัญหาเก็บข้อมูลเกิน, และทำให้บริการ AI ของคุณทำงานได้อย่างราบรื่น ให้ลองสคริปต์นี้ ปรับรูปแบบตามใจคุณ แล้วให้มันกลายเป็นเครื่องมือสำคัญในกล่องเครื่องมือของคุณ

Happy coding, and may your models always be fresh!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}