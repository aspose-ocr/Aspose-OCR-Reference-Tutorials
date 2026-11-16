---
category: general
date: 2026-02-22
description: เรียนรู้วิธีแสดงรายการโมเดลที่เก็บไว้ในแคชและแสดงไดเรกทอรีแคชบนเครื่องของคุณอย่างรวดเร็ว
  รวมขั้นตอนการดูโฟลเดอร์แคชและจัดการการจัดเก็บโมเดล AI ในเครื่อง.
draft: false
keywords:
- list cached models
- show cache directory
- how to view cache folder
- AI model cache
- local model storage
language: th
og_description: ค้นหาวิธีการแสดงรายการโมเดลที่แคชไว้, แสดงไดเรกทอรีแคช, และดูโฟลเดอร์แคชในไม่กี่ขั้นตอนง่าย
  ๆ พร้อมตัวอย่าง Python ครบถ้วน.
og_title: รายการโมเดลที่แคชไว้ – คู่มือสั้นเพื่อดูไดเรกทอรีแคช
tags:
- AI
- caching
- Python
- development
title: รายการโมเดลที่แคช – วิธีดูโฟลเดอร์แคชและแสดงไดเรกทอรีแคช
url: /th/python/general/list-cached-models-how-to-view-cache-folder-and-show-cache-d/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# รายการโมเดลที่แคช – คู่มือเร็วสำหรับดูไดเรกทอรีแคช

เคยสงสัยไหมว่า **รายการโมเดลที่แคช** อยู่ที่ไหนบนเครื่องของคุณโดยไม่ต้องค้นหาโฟลเดอร์ที่ซับซ้อน? คุณไม่ได้เป็นคนเดียวที่เจอปัญหานี้ นักพัฒนาหลายคนมักเจออุปสรรคเมื่อต้องตรวจสอบว่าโมเดล AI ใดบ้างที่ถูกเก็บไว้ในเครื่องแล้ว โดยเฉพาะเมื่อพื้นที่ดิสก์มีจำกัด ข่าวดีคือ? เพียงไม่กี่บรรทัดคุณก็สามารถ **รายการโมเดลที่แคช** และ **แสดงไดเรกทอรีแคช** ได้พร้อมกัน ทำให้คุณมองเห็นโฟลเดอร์แคชของคุณได้อย่างเต็มที่

ในบทเรียนนี้เราจะเดินผ่านสคริปต์ Python ที่ทำงานอิสระซึ่งทำสิ่งนั้นได้อย่างแม่นยำ เมื่อจบคุณจะรู้วิธีดูโฟลเดอร์แคช เข้าใจว่าแคชอยู่ที่ไหนบนระบบปฏิบัติการต่าง ๆ และแม้กระทั่งเห็นรายการโมเดลที่ดาวน์โหลดแล้วที่พิมพ์ออกมาชัดเจน ไม่ต้องอ้างอิงเอกสารภายนอก ไม่ต้องเดา—แค่โค้ดและคำอธิบายที่คุณสามารถคัดลอก‑วางได้ทันที

## สิ่งที่คุณจะได้เรียน

- วิธีเริ่มต้น AI client (หรือ stub) ที่ให้ฟังก์ชันการแคช  
- คำสั่งที่แน่นอนสำหรับ **รายการโมเดลที่แคช** และ **แสดงไดเรกทอรีแคช**  
- ที่ตั้งของแคชบน Windows, macOS, และ Linux เพื่อให้คุณสามารถนำทางไปยังตำแหน่งนั้นด้วยตนเองได้หากต้องการ  
- เคล็ดลับการจัดการกรณีขอบเช่นแคชว่างหรือเส้นทางแคชที่กำหนดเอง  

**ข้อกำหนดเบื้องต้น** – คุณต้องมี Python 3.8+ และ AI client ที่ติดตั้งผ่าน pip ซึ่งมีเมธอด `list_local()`, `get_local_path()`, และอาจมี `clear_local()` หากคุณยังไม่มี ตัวอย่างใช้คลาส mock `YourAIClient` ที่คุณสามารถเปลี่ยนเป็น SDK จริง (เช่น `openai`, `huggingface_hub` ฯลฯ)  

พร้อมหรือยัง? ไปดูกันเลย

## ขั้นตอนที่ 1: ตั้งค่า AI Client (หรือ Mock)

หากคุณมีอ็อบเจกต์ client อยู่แล้ว ให้ข้ามบล็อกนี้ไปเลย มิฉะนั้น ให้สร้างตัวแทนขนาดเล็กที่จำลองอินเทอร์เฟซการแคช นี้ทำให้สคริปต์ทำงานได้แม้ไม่มี SDK จริง

```python
# step_1_client_setup.py
import os
from pathlib import Path

class YourAIClient:
    """
    Minimal mock of an AI client that stores downloaded models in a
    directory called `.ai_cache` inside the user's home folder.
    """
    def __init__(self, cache_dir: Path | None = None):
        # Use a custom path if supplied, otherwise default to ~/.ai_cache
        self.cache_dir = Path(cache_dir) if cache_dir else Path.home() / ".ai_cache"
        self.cache_dir.mkdir(parents=True, exist_ok=True)

    def list_local(self):
        """Return a list of model folder names that exist in the cache."""
        return [p.name for p in self.cache_dir.iterdir() if p.is_dir()]

    def get_local_path(self):
        """Absolute path to the cache directory."""
        return str(self.cache_dir.resolve())

    # Optional helper for demonstration purposes
    def _populate_dummy_models(self, count=3):
        for i in range(1, count + 1):
            (self.cache_dir / f"model_{i}").mkdir(exist_ok=True)

# Initialize the client (replace with real client if you have one)
ai = YourAIClient()
# Populate with dummy data the first time you run the script
if not ai.list_local():
    ai._populate_dummy_models()
```

> **Pro tip:** หากคุณมี client จริงอยู่แล้ว (เช่น `from huggingface_hub import HfApi`) เพียงเปลี่ยนการเรียก `YourAIClient()` เป็น `HfApi()` และตรวจสอบให้เมธอด `list_local` และ `get_local_path` มีอยู่หรือถูกห่อหุ้มอย่างเหมาะสม

## ขั้นตอนที่ 2: **รายการโมเดลที่แคช** – ดึงและแสดงผล

ตอนนี้ client พร้อมแล้ว เราสามารถขอให้มันแสดงรายการทั้งหมดที่มีในเครื่อง นี่คือหัวใจของการ **รายการโมเดลที่แคช** ของเรา

```python
# step_2_list_models.py
print("Cached models:")
for model_name in ai.list_local():
    print(" -", model_name)
```

**ผลลัพธ์ที่คาดหวัง** (จากข้อมูลจำลองในขั้นตอน 1):

```
Cached models:
 - model_1
 - model_2
 - model_3
```

หากแคชว่างคุณจะเห็นเพียง:

```
Cached models:
```

บรรทัดว่างเล็ก ๆ นี้บ่งบอกว่าไม่มีอะไรถูกเก็บไว้—เป็นประโยชน์เมื่อคุณเขียนสคริปต์ทำความสะอาด

## ขั้นตอนที่ 3: **แสดงไดเรกทอรีแคช** – แคชอยู่ที่ไหน?

การรู้เส้นทางเป็นครึ่งหนึ่งของการแก้ปัญหา ระบบปฏิบัติการต่าง ๆ จะวางแคชไว้ในตำแหน่งเริ่มต้นที่แตกต่างกัน และบาง SDK อนุญาตให้คุณกำหนดทับผ่านตัวแปรสภาพแวดล้อม โค้ดต่อไปนี้จะพิมพ์เส้นทางเต็มเพื่อให้คุณ `cd` เข้าไปหรือเปิดในไฟล์เอ็กซ์พลอเรอร์

```python
# step_3_show_path.py
print("\nCache directory:", ai.get_local_path())
```

**ผลลัพธ์ทั่วไป** บนระบบ Unix‑like:

```
Cache directory: /home/youruser/.ai_cache
```

บน Windows คุณอาจเห็นประมาณนี้:

```
Cache directory: C:\Users\YourUser\.ai_cache
```

ตอนนี้คุณรู้วิธี **ดูโฟลเดอร์แคช** บนแพลตฟอร์มใดก็ได้แล้ว

## ขั้นตอนที่ 4: รวมทั้งหมดไว้ในสคริปต์เดียวที่รันได้

ด้านล่างเป็นโปรแกรมเต็มที่พร้อมรันซึ่งรวมสามขั้นตอนเข้าด้วยกัน บันทึกเป็น `view_ai_cache.py` แล้วรันด้วย `python view_ai_cache.py`

```python
# view_ai_cache.py
import os
from pathlib import Path

class YourAIClient:
    """Simple mock client exposing cache‑related utilities."""
    def __init__(self, cache_dir: Path | None = None):
        self.cache_dir = Path(cache_dir) if cache_dir else Path.home() / ".ai_cache"
        self.cache_dir.mkdir(parents=True, exist_ok=True)

    def list_local(self):
        return [p.name for p in self.cache_dir.iterdir() if p.is_dir()]

    def get_local_path(self):
        return str(self.cache_dir.resolve())

    def _populate_dummy_models(self, count=3):
        for i in range(1, count + 1):
            (self.cache_dir / f"model_{i}").mkdir(exist_ok=True)

# ----------------------------------------------------------------------
# Main execution block
# ----------------------------------------------------------------------
if __name__ == "__main__":
    # Initialize (replace with real client if available)
    ai = YourAIClient()

    # Populate dummy data only on first run – remove this in production
    if not ai.list_local():
        ai._populate_dummy_models()

    # Step 1: list cached models
    print("Cached models:")
    for model_name in ai.list_local():
        print(" -", model_name)

    # Step 2: show cache directory
    print("\nCache directory:", ai.get_local_path())
```

รันสคริปต์แล้วคุณจะเห็นทั้งรายการโมเดลที่แคช **และ** ตำแหน่งของไดเรกทอรีแคชในทันที

## กรณีขอบและรูปแบบต่าง ๆ

| สถานการณ์ | วิธีทำ |
|-----------|------------|
| **แคชว่าง** | สคริปต์จะพิมพ์ “Cached models:” โดยไม่มีรายการ คุณสามารถเพิ่มการแจ้งเตือนเงื่อนไข: `if not models: print("⚠️ No models cached yet.")` |
| **เส้นทางแคชที่กำหนดเอง** | ส่งพาธเมื่อสร้าง client: `YourAIClient(cache_dir=Path("/tmp/my_ai_cache"))`. การเรียก `get_local_path()` จะสะท้อนตำแหน่งที่กำหนดเองนั้น |
| **ข้อผิดพลาดเรื่องสิทธิ์** | บนเครื่องที่จำกัดสิทธิ์ client อาจโยน `PermissionError`. ให้ห่อการเริ่มต้นด้วย `try/except` แล้วเปลี่ยนไปใช้ไดเรกทอรีที่ผู้ใช้เขียนได้ |
| **การใช้ SDK จริง** | แทนที่ `YourAIClient` ด้วยคลาส client ที่แท้จริงและตรวจสอบให้ชื่อเมธอดตรงกัน หลาย SDK มีแอตทริบิวต์ `cache_dir` ที่คุณสามารถอ่านได้โดยตรง |

## เคล็ดลับระดับ Pro สำหรับการจัดการแคชของคุณ

- **ทำความสะอาดเป็นระยะ:** หากคุณดาวน์โหลดโมเดลขนาดใหญ่บ่อย ๆ ตั้งงาน cron ที่เรียก `shutil.rmtree(ai.get_local_path())` หลังจากยืนยันว่าไม่ต้องการโมเดลเหล่านั้นอีกแล้ว  
- **ตรวจสอบการใช้ดิสก์:** ใช้ `du -sh $(ai.get_local_path())` บน Linux/macOS หรือ `Get-ChildItem -Recurse | Measure-Object -Property Length -Sum` ใน PowerShell เพื่อดูขนาดโดยรวม  
- **โฟลเดอร์เวอร์ชัน:** บาง client สร้างโฟลเดอร์ย่อยตามเวอร์ชันของโมเดล เมื่อคุณ **รายการโมเดลที่แคช** คุณจะเห็นแต่ละเวอร์ชันเป็นรายการแยก—ใช้ข้อมูลนี้เพื่อลบเวอร์ชันเก่าออก  

## ภาพรวมแบบภาพ

![list cached models screenshot](https://example.com/images/list-cached-models.png "list cached models – console output showing models and cache path")

*ข้อความแทนภาพ:* *list cached models – แสดงผลคอนโซลของชื่อโมเดลที่แคชและเส้นทางไดเรกทอรีแคช*

## สรุป

เราได้ครอบคลุมทุกอย่างที่คุณต้องการเพื่อ **รายการโมเดลที่แคช**, **แสดงไดเรกทอรีแคช**, และโดยทั่วไป **วิธีดูโฟลเดอร์แคช** บนระบบใดก็ได้ สคริปต์สั้น ๆ นี้แสดงวิธีแก้ที่สมบูรณ์และรันได้จริง พร้อมอธิบาย **เหตุผล** ที่แต่ละขั้นตอนสำคัญและให้คำแนะนำเชิงปฏิบัติสำหรับการใช้งานจริง  

ต่อไปคุณอาจสำรวจ **วิธีล้างแคช** ผ่านโปรแกรม หรือผสานคำสั่งเหล่านี้เข้าไปใน pipeline การปรับใช้ที่ตรวจสอบความพร้อมของโมเดลก่อนเริ่มงาน inference ไม่ว่าคุณจะทำอย่างไร คุณก็มีพื้นฐานที่มั่นคงในการจัดการการเก็บโมเดล AI ในเครื่องของคุณแล้ว  

มีคำถามเกี่ยวกับ SDK AI ใดเป็นพิเศษ? แสดงความคิดเห็นด้านล่าง แล้วขอให้สนุกกับการแคช!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}