---
category: general
date: 2026-06-22
description: วิธีเปลี่ยนภาษาของเครื่อง OCR อย่างรวดเร็ว เรียนรู้การตั้งค่าภาษา OCR
  ภาษาอาหรับ (ar) ด้วยโค้ดง่าย ๆ และหลีกเลี่ยงข้อผิดพลาดทั่วไป
draft: false
keywords:
- how to change language
- ocr language arabic
- how to set OCR
- change OCR language
- set language OCR
language: th
og_description: วิธีการเปลี่ยนภาษาในเครื่องมือ OCR ถูกอธิบายในประโยคแรก ตามบทแนะนำนี้เพื่อกำหนดภาษาของ
  OCR ภาษาอาหรับอย่างรวดเร็ว.
og_title: วิธีเปลี่ยนภาษาใน OCR – คู่มือครบวงจร
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: How to change language in OCR engines quickly. Learn to set Arabic
    (ar) OCR language using simple code and avoid common pitfalls.
  headline: How to Change Language in OCR – Set Arabic Language Step‑by‑Step
  type: TechArticle
- description: How to change language in OCR engines quickly. Learn to set Arabic
    (ar) OCR language using simple code and avoid common pitfalls.
  name: How to Change Language in OCR – Set Arabic Language Step‑by‑Step
  steps:
  - name: '**Grab the OCR engine instance** – this is usually a singleton or a factory‑created
      object.'
    text: '**Grab the OCR engine instance** – this is usually a singleton or a factory‑created
      object.'
  - name: '**Pull the settings object** – most libraries keep language, DPI, and other
      options in a separate config container.'
    text: '**Pull the settings object** – most libraries keep language, DPI, and other
      options in a separate config container.'
  - name: '**Set the language code** – for Arabic the ISO‑639‑2 code is `"ar"`.'
    text: '**Set the language code** – for Arabic the ISO‑639‑2 code is `"ar"`.'
  type: HowTo
tags:
- OCR
- multilingual
- programming
title: วิธีเปลี่ยนภาษาใน OCR – ตั้งค่าภาษาอาหรับแบบทีละขั้นตอน
url: /th/python-java/general/how-to-change-language-in-ocr-set-arabic-language-step-by-st/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีเปลี่ยนภาษาใน OCR – คู่มือการเขียนโปรแกรมฉบับสมบูรณ์

การเปลี่ยนภาษาของเครื่อง OCR เป็นอุปสรรคที่พบบ่อยเมื่อคุณเริ่มทำงานกับเอกสารหลายภาษา ในบทแนะนำนี้เราจะพาคุณผ่านขั้นตอนที่แน่นอนเพื่อกำหนดภาษาของ OCR เป็นภาษาอาหรับ พร้อมตัวอย่างโค้ดที่สามารถรันได้และคำอธิบายสำหรับแต่ละบรรทัด หากคุณเคยสงสัย *“how to set OCR* ไปยังสคริปต์ที่แตกต่างโดยไม่ทำให้ pipeline พัง* คุณมาถูกที่แล้ว*.

เราจะครอบคลุมทุกสิ่งที่คุณต้องการ: ไลบรารีที่จำเป็น, วิธีการรับอินสแตนซ์ของ OCR engine, วิธีการเข้าถึงการตั้งค่า, และสุดท้ายวิธีการเปลี่ยนภาษาของ OCR อย่างปลอดภัย เมื่อจบคุณจะสามารถสลับจากภาษาอังกฤษเป็นภาษาอาหรับ (หรือภาษาอื่นที่รองรับ) ด้วยการเรียกเมธอดเดียว ไม่ต้องใช้เวทมนตร์ เพียงโค้ดที่ชัดเจนและเคล็ดลับปฏิบัติเล็กน้อย.

## ข้อกำหนดเบื้องต้น

- Python 3.8+ (หรือเวอร์ชันล่าสุดใดก็ได้)
- ไลบรารี OCR ที่เปิดเผยวัตถุ settings – ตัวอย่างใช้ **pytesseract** ที่ห่อหุ้มด้วยคลาสช่วยขนาดเล็ก แต่รูปแบบเดียวกันทำงานกับเอนจินอื่น ๆ เช่น EasyOCR หรือ Microsoft’s Computer Vision SDK.
- ข้อมูลภาษาอาหรับที่ติดตั้งสำหรับเครื่อง OCR (`ara.traineddata` สำหรับ Tesseract).  
  *Pro tip:* บน Ubuntu คุณสามารถติดตั้งได้ด้วย `sudo apt-get install tesseract-ocr-ara`.

## วิธีเปลี่ยนภาษาใน OCR – ภาพรวม

การเปลี่ยนภาษานั้นโดยพื้นฐานคือการทำตามขั้นตอนสามขั้นตอน:

1. **Grab the OCR engine instance** – ปกติจะเป็น singleton หรืออ็อบเจกต์ที่สร้างโดย factory
2. **Pull the settings object** – ไลบรารีส่วนใหญ่เก็บภาษา, DPI, และตัวเลือกอื่น ๆ ในคอนเทนเนอร์ config แยก
3. **Set the language code** – สำหรับภาษาอาหรับรหัส ISO‑639‑2 คือ `"ar"`.

ด้านล่างเป็นสคริปต์ขนาดเล็กที่สามารถรันได้เต็มรูปแบบซึ่งแสดงขั้นตอนเหล่านี้.

![How to change language in OCR screenshot](image-placeholder.png "How to change language in OCR example")

## ขั้นตอนที่ 1: สร้างหรือรับอินสแตนซ์ของ OCR Engine

First we need an engine. In real projects the engine might be created elsewhere and passed around; for clarity we’ll instantiate it right here.

```python
# step1_engine.py
import pytesseract
from PIL import Image

class SimpleOCREngine:
    """A thin wrapper around pytesseract to expose a settings object."""
    def __init__(self):
        # pytesseract itself doesn't expose a mutable settings object,
        # so we store options in a dict that we later pass to image_to_string().
        self._options = {"lang": "eng"}  # default to English

    def get_settings(self):
        """Return a Settings object that can modify OCR options."""
        return OcrSettings(self)

    def recognize(self, image_path: str) -> str:
        """Run OCR on the given image using current options."""
        img = Image.open(image_path)
        return pytesseract.image_to_string(img, config=self._build_config())

    def _build_config(self) -> str:
        """Convert the internal options dict to a Tesseract command line."""
        # Example: '-l eng' or '-l ar+eng' for multiple languages
        lang_option = self._options.get("lang", "eng")
        return f"-l {lang_option}"
```

**Why we wrap the engine** – many OCR SDKs (including Tesseract) expect language to be passed as a string each call. By encapsulating the options in a settings object we get a clean, *how to set OCR*‑style API that mirrors the original code snippet you provided.

## ขั้นตอนที่ 2: เข้าถึงวัตถุ Settings ของ Engine

Now that we have an engine, we retrieve its settings. This mirrors the second line of the original example (`settings = engine.get_settings()`).

```python
# step2_settings.py
class OcrSettings:
    """Provides getters and setters for OCR configuration."""
    def __init__(self, engine: SimpleOCREngine):
        self._engine = engine

    def set_language(self, lang_code: str):
        """
        Change OCR language.
        :param lang_code: ISO‑639‑2 language code, e.g., 'ar' for Arabic.
        """
        # Validate the language code – a tiny safety net.
        if not isinstance(lang_code, str) or len(lang_code) < 2:
            raise ValueError("Language code must be a non‑empty string.")
        self._engine._options["lang"] = lang_code

    def get_language(self) -> str:
        """Return the currently configured language code."""
        return self._engine._options.get("lang", "eng")
```

Here we expose **how to set OCR** language via `set_language`. The method also performs a basic sanity check, which is a nice defensive programming habit.

## ขั้นตอนที่ 3: ตั้งค่าภาษา OCR เป็นภาษาอาหรับ (ocr language arabic)

Finally we call the method with the Arabic code `"ar"`. This is the heart of the *change OCR language* operation.

```python
# step3_change_language.py
from step1_engine import SimpleOCREngine

# Obtain the OCR engine instance (could be a singleton in a larger app)
engine = SimpleOCREngine()

# Access the settings object
settings = engine.get_settings()

# Set the OCR language to Arabic – this is the "how to change language" line.
settings.set_language("ar")

# Optional: verify the change
print("Current OCR language:", settings.get_language())

# Run OCR on a sample Arabic image (replace with your own path)
# result = engine.recognize("sample_arabic.png")
# print("OCR Output:", result)
```

**ผลลัพธ์ที่คาดหวัง**

```
Current OCR language: ar
```

If you uncomment the `recognize` call and point it at a real Arabic image, you should see Arabic characters printed to the console (provided the language data is installed).

## วิธีตั้งค่า OCR สำหรับหลายภาษา

Sometimes you need *ocr language arabic* **plus** English, especially for mixed documents. The `set_language` method can accept a `+`‑separated list:

```python
settings.set_language("ar+eng")
print("Now recognizing both Arabic and English:", settings.get_language())
```

*Edge case*: If the requested language pack isn’t installed, Tesseract will throw an error like `Error opening language file`. To avoid a crash, you can catch the exception and fall back to a default language.

```python
try:
    settings.set_language("ar")
except Exception as e:
    print("Failed to set Arabic language:", e)
    settings.set_language("eng")  # fallback
```

## เปลี่ยนภาษา OCR อย่างไดนามิกระหว่างการทำงาน

In many applications the user selects a language from a dropdown. Because the settings live inside the engine object, you can switch languages on‑the‑fly without re‑instantiating the engine.

```python
def switch_language(lang_code: str):
    settings.set_language(lang_code)
    print(f"OCR language switched to {lang_code}")

# Example usage:
switch_language("fr")   # switch to French
switch_language("ar")   # back to Arabic
```

This pattern satisfies the *set language OCR* requirement while keeping the code tidy.

## ข้อผิดพลาดทั่วไปและเคล็ดลับมืออาชีพ

| ปัญหา | สิ่งที่เกิดขึ้น | วิธีแก้ |
|---------|--------------|-----|
| ขาดแพ็คภาษา | Tesseract คืนค่า “Failed loading language ‘ar’” | ติดตั้งข้อมูลภาษา (`sudo apt-get install tesseract-ocr-ara` หรือดาวน์โหลดจากรีโป) |
| ใช้รหัส ISO ผิด | ไม่มีผลลัพธ์หรืออักขระแสดงผิด | ตรวจสอบรหัส (`ar` สำหรับอาหรับ, `eng` สำหรับอังกฤษ, `chi_sim` สำหรับจีนแบบ Simplified) |
| ลืมเรียก rebuild config | Engine ยังคงใช้ภาษาที่เก่า | ควรเรียก `engine._build_config()` เสมอ (จะทำงานโดยอัตโนมัติเมื่อคุณเรียก `recognize`) |
| ส่งรายการแทนสตริง | TypeError | ใช้ `"ar+eng"` เป็นสตริงเดียว ไม่ใช่ `["ar", "eng"]` |

## ตัวอย่างทำงานเต็มรูปแบบ (รวมทุกส่วนเข้าด้วยกัน)

```python
# full_example.py
import pytesseract
from PIL import Image

class SimpleOCREngine:
    def __init__(self):
        self._options = {"lang": "eng"}

    def get_settings(self):
        return OcrSettings(self)

    def recognize(self, image_path: str) -> str:
        img = Image.open(image_path)
        return pytesseract.image_to_string(img, config=self._build_config())

    def _build_config(self) -> str:
        return f"-l {self._options.get('lang', 'eng')}"

class OcrSettings:
    def __init__(self, engine: SimpleOCREngine):
        self._engine = engine

    def set_language(self, lang_code: str):
        if not isinstance(lang_code, str) or len(lang_code) < 2:
            raise ValueError("Language code must be a non‑empty string.")
        self._engine._options["lang"] = lang_code

    def get_language(self) -> str:
        return self._engine._options.get("lang", "eng")

# ---------- Usage ----------
engine = SimpleOCREngine()
settings = engine.get_settings()

# Change to Arabic (how to change language)
settings.set_language("ar")
print("Current OCR language:", settings.get_language())

# Uncomment and point to a real Arabic image to test OCR
# output = engine.recognize("sample_arabic.png")
# print("OCR result:", output)
```

Run the script with `python full_example.py`. If everything is set up, you’ll see:

```
Current OCR language: ar
```

…and the OCR output for your Arabic image if you enable the last two lines.

## สรุป

You now know **how to change language in OCR** engines, specifically how to set the OCR language to Arabic using a clean, reusable pattern. The guide walked through obtaining the engine, accessing its settings, and finally applying the language change—covering both the *ocr language arabic* scenario and the broader *change OCR language* use case.  

Next steps? Try adding support for more languages, experiment with multi‑language strings (`"ar+eng"`), or integrate this logic into a web service that lets users upload documents in any script. If you’re curious about *set language OCR* in other libraries (EasyOCR, Google Vision

## คุณควรเรียนรู้อะไรต่อไป?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [วิธี OCR ข้อความในรูปภาพด้วยภาษาโดยใช้ Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [ดึงข้อความจากรูปภาพ C# ด้วยการเลือกภาษาโดยใช้ Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [วิธีดึง OCR – การกำหนดค่า OCR](/ocr/english/net/ocr-configuration/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}