---
category: general
date: 2026-06-06
description: OCR รูป PNG ด้วย Python – เรียนรู้วิธีดึงข้อความจากภาพ, รันตัวอย่าง OCR
  ด้วย Python และแม้กระทั่งอ่านข้อความภาษากรีกโบราณได้อย่างง่ายดาย.
draft: false
keywords:
- ocr png image
- extract text from image
- python ocr example
- read ancient greek
- recognize image text
language: th
og_description: อธิบายการทำ OCR ภาพ PNG ด้วย Python คู่มือนี้แสดงวิธีดึงข้อความจากภาพ,
  รันตัวอย่าง OCR ด้วย Python และอ่านภาษากรีกโบราณได้อย่างง่ายดาย
og_title: OCR รูปภาพ PNG ด้วย Python – คู่มือฉบับสมบูรณ์
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: OCR PNG image with Python – learn how to extract text from image, run
    a python OCR example and even read ancient greek text easily.
  headline: OCR PNG Image in Python – Full Step‑by‑Step Guide
  type: TechArticle
- description: OCR PNG image with Python – learn how to extract text from image, run
    a python OCR example and even read ancient greek text easily.
  name: OCR PNG Image in Python – Full Step‑by‑Step Guide
  steps:
  - name: Prerequisites
    text: '| Requirement | Why it matters | |-------------|----------------| | Python
      3.8+ | Modern syntax and type hints | | `pytesseract` package | Thin wrapper
      around the Tesseract engine | | Tesseract OCR binaries (≥ 5.0) | The actual
      engine that does the heavy lifting | | Greek language data (`grc.trained'
  - name: How do I improve accuracy on a noisy PNG?
    text: '- Convert the image to grayscale: `img = img.convert(''L'')` - Apply a
      binary threshold: `img = img.point(lambda x: 0 if x < 128 else 255, ''1'')`
      - Upscale with `img = img.resize((img.width*2, img.height*2), Image.LANCZOS)`'
  - name: Can I process a whole folder of PNGs?
    text: Absolutely. Wrap the `recognize_image` call in a `for` loop over `Path.glob("*.png")`.
      Store each result in a dictionary or write to a CSV for later analysis.
  - name: What if I need to extract numbers only?
    text: 'Pass a custom **config** string to `image_to_string`:'
  - name: Is there a way to get confidence scores?
    text: Yes—use `pytesseract.image_to_data` which returns a TSV with confidence
      per word. You can filter out low‑confidence tokens before assembling the final
      string.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: OCR ภาพ PNG ด้วย Python – คู่มือเต็มขั้นตอนโดยละเอียด
url: /th/python-java/general/ocr-png-image-in-python-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR PNG Image ใน Python – คู่มือเต็มขั้นตอน

เคยสงสัยไหมว่าจะแปลงข้อความจากไฟล์ **OCR PNG image** โดยตรงจากสคริปต์ Python ได้อย่างไร? บางทีคุณอาจมีโฟลเดอร์ที่เต็มไปด้วยต้นฉบับสแกนโบราณและต้องการ **extract text from image** โดยไม่ต้องพิมพ์ทุกอย่างด้วยตนเอง ข่าวดีคือคุณไม่จำเป็นต้องมีปริญญาเอกด้านคอมพิวเตอร์วิชัน—แค่ไม่กี่บรรทัดของโค้ดและไลบรารีที่เหมาะสม แล้วคุณก็จะอ่านภาษากรีกโบราณได้ในไม่กี่วินาที

ในบทเรียนนี้เราจะเดินผ่าน **python OCR example** ที่จดจำข้อความจาก PNG ตั้งค่าภาษาเป็น Greek polytonic และพิมพ์ผลลัพธ์ออกมา เมื่อจบคุณจะรู้วิธี **recognize image text** อย่างแม่นยำ จัดการกับปัญหาที่พบบ่อย และปรับสคริปต์ให้ทำงานกับภาษาอื่นหรือรูปแบบภาพอื่นได้

## สิ่งที่คุณจะได้เรียนรู้

- ติดตั้งและกำหนดค่าไลบรารี OCR ของ Python (pytesseract + Tesseract OCR)
- สร้างอินสแตนซ์ของ OCR engine และโหลดไฟล์ PNG
- ตั้งค่าภาษาเป็น Greek polytonic เพื่อ **read ancient greek**
- แสดงข้อความที่จดจำได้และแก้ไขปัญหาที่พบบ่อย
- ขยายสคริปต์เพื่อประมวลผลหลาย PNG หรือสลับไปใช้ภาษาอื่น

### ข้อกำหนดเบื้องต้น

| ข้อกำหนด | เหตุผลที่สำคัญ |
|-------------|----------------|
| Python 3.8+ | ไวยากรณ์สมัยใหม่และ type hints |
| `pytesseract` package | ห่อหุ้มเบา ๆ รอบ engine ของ Tesseract |
| Tesseract OCR binaries (≥ 5.0) | Engine จริงที่ทำงานหนัก |
| Greek language data (`grc.traineddata`) | จำเป็นสำหรับ **read ancient greek** อย่างถูกต้อง |
| A PNG image you want to analyse (e.g., `ancient_greek.png`) | เป้าหมายของการสาธิต **ocr png image** |

คุณสามารถติดตั้งส่วนของ Python ด้วย:

```bash
pip install pytesseract Pillow
```

และบน Ubuntu/macOS คุณจะต้องเพิ่ม engine เอง:

```bash
# Ubuntu
sudo apt-get install tesseract-ocr libtesseract-dev

# macOS (Homebrew)
brew install tesseract
```

อย่าลืมดาวน์โหลดข้อมูลฝึก Greek polytonic:

```bash
wget https://github.com/tesseract-ocr/tessdata/blob/main/greek.traineddata -P /usr/share/tesseract-ocr/4.00/tessdata/
```

*(Path อาจแตกต่าง; ปรับ `TESSDATA_PREFIX` หากจำเป็น)*

---

## OCR PNG Image: สร้างอินสแตนซ์ของ Engine

สิ่งแรกที่เราต้องการคืออ็อบเจ็กต์ที่สื่อสารกับ Tesseract ใน `pytesseract` engine ถูกเข้าถึงผ่านฟังก์ชันระดับโมดูล แต่เพื่อความชัดเจนเราจะห่อหุ้มไว้ในคลาสเล็ก ๆ ซึ่งสะท้อนแนวคิด “engine” ที่คุณเห็นในโค้ดต้นฉบับ

```python
from pathlib import Path
from PIL import Image
import pytesseract

class OcrEngine:
    """
    Simple wrapper around pytesseract to keep the API similar to the original example.
    """
    def __init__(self, tess_cmd: str = "tesseract"):
        # You can point pytesseract to a custom binary if you installed it somewhere unusual.
        pytesseract.pytesseract.tesseract_cmd = tess_cmd

    def set_recognition_language(self, language: str):
        """
        Store the language code for later calls.
        Example: 'grc' for Greek polytonic.
        """
        self.lang = language

    def recognize_image(self, image_path: str):
        """
        Open the PNG, run OCR, and return the raw result object.
        """
        img = Image.open(image_path)
        # pytesseract returns a string; we wrap it for consistency with the original code.
        text = pytesseract.image_to_string(img, lang=self.lang)
        return OcrResult(text=text)

class OcrResult:
    """Container for OCR output – mimics the .text attribute used in the example."""
    def __init__(self, text: str):
        self.text = text
```

**ทำไมต้องห่อหุ้ม?**  
- ทำให้ API สาธารณะเหมือนกับสแนปเพล็ตเดิม ทำให้การย้ายโค้ดเป็นเรื่องง่าย  
- สามารถเพิ่ม logging หรือการจัดการข้อผิดพลาดในภายหลังโดยไม่ต้องแก้ไขโฟลว์หลัก  
- แสดงแนวปฏิบัติ OOP ที่ดี — สิ่งที่นักพัฒนาระดับสูงชื่นชม

---

## Extract Text from Image: ตั้งค่าภาษาเป็น Greek Polytonic

ตอนนี้เรามี engine แล้ว เราต้องบอกให้มันรู้ว่าคาดหวังภาษาอะไร Greek polytonic ใช้เครื่องหมายวรรณยุกต์ที่ไม่ได้รวมอยู่ในข้อมูล “greek” ปกติ ดังนั้นเราจึงชี้ Tesseract ไปที่ไฟล์ฝึก `grc`

```python
# Step 2: Set the recognition language to Greek polytonic
engine = OcrEngine()
engine.set_recognition_language("grc")   # 'grc' is the ISO‑639‑2 code for ancient Greek
```

หากคุณต้องการ **extract text from image** ในภาษาอื่น เพียงเปลี่ยน `"grc"` เป็น `"eng"` สำหรับอังกฤษ, `"fra"` สำหรับฝรั่งเศส ฯลฯ บรรทัดเดียวนี้ทำงานกับทุกภาษาที่คุณติดตั้งไว้

---

## Recognize Image Text: รัน OCR บน PNG

เมื่อกำหนดภาษาแล้ว เราจะส่ง PNG เข้า engine ตัวอย่างเดิมใช้พาธคงที่; เราจะทำให้ยืดหยุ่นขึ้นโดยใช้วัตถุ `Path`

```python
# Step 3: Recognize text from the image file
image_path = Path("YOUR_DIRECTORY/ancient_greek.png")
ocr_result = engine.recognize_image(str(image_path))
```

**เคล็ดลับและกรณีขอบ**

- **ไฟล์ไม่พบ** – ห่อการเรียกใน `try/except FileNotFoundError` เพื่อแสดงข้อความที่เป็นมิตร  
- **PNG ความละเอียดต่ำ** – พิจารณา pre‑processing (เช่น การปรับขนาด, การทำไบนารี) ด้วย Pillow ก่อน OCR  
- **ข้อความไม่ใช่ภาษากรีก** – Tesseract จะพยายามถอดรหัสต่อไป แต่ความแม่นยำจะลดลงอย่างมาก ควรเลือกภาษาให้ตรงกันเสมอ

---

## Output the Recognized Text

สุดท้ายเราพิมพ์ผลลัพธ์ออกมา ในโครงการจริงคุณอาจบันทึกลงฐานข้อมูล, CSV, หรือส่งต่อไปยัง pipeline การแปล

```python
# Step 4: Output the recognized text
print("=== OCR Result ===")
print(ocr_result.text)
```

เมื่อรันสคริปต์กับสแกนที่ชัดเจนของจารึกกรีกโบราณ คุณควรเห็นข้อความประมาณนี้:

```
=== OCR Result ===
Ἀνδρὸς ἐστὶν ὁ ἥλιος...
```

หากผลลัพธ์ดูเป็นอักขระแปลก ๆ ให้ตรวจสอบว่าไฟล์ **greek.traineddata** อยู่ในโฟลเดอร์ที่ถูกต้องและ PNG ไม่มีสัญญาณรบกวนมากเกินไป

---

## Full Working Example (All Steps in One Script)

ด้านล่างเป็นโปรแกรมเต็มที่พร้อมรัน บันทึกเป็น `ocr_greek.py` แล้วเรียก `python ocr_greek.py`

```python
# ocr_greek.py
from pathlib import Path
from PIL import Image
import pytesseract

class OcrEngine:
    def __init__(self, tess_cmd: str = "tesseract"):
        pytesseract.pytesseract.tesseract_cmd = tess_cmd
        self.lang = "eng"  # default fallback

    def set_recognition_language(self, language: str):
        self.lang = language

    def recognize_image(self, image_path: str):
        img = Image.open(image_path)
        text = pytesseract.image_to_string(img, lang=self.lang)
        return OcrResult(text)

class OcrResult:
    def __init__(self, text: str):
        self.text = text

def main():
    # 1️⃣ Create an OCR engine instance
    engine = OcrEngine()

    # 2️⃣ Set the language to Greek polytonic (read ancient greek)
    engine.set_recognition_language("grc")

    # 3️⃣ Path to the PNG you want to analyse
    png_path = Path("YOUR_DIRECTORY/ancient_greek.png")
    if not png_path.is_file():
        raise FileNotFoundError(f"Cannot find image at {png_path}")

    # 4️⃣ Recognize and retrieve the text
    result = engine.recognize_image(str(png_path))

    # 5️⃣ Print the extracted text
    print("=== OCR PNG Image Result ===")
    print(result.text)

if __name__ == "__main__":
    main()
```

**ผลลัพธ์ที่คาดหวัง** (ตัดทอนเพื่อความกระชับ):

```
=== OCR PNG Image Result ===
Ἀνδρὸς ἐστὶν ὁ ἥλιος·
Καὶ ὁ ἥλιος ἀνατέλλει·
```

หากคุณเห็นอักขระกรีกที่ถูกต้อง ยินดีด้วย — คุณได้ทำการ **ocr png image** ด้วย Python สำเร็จแล้ว!

---

## Common Questions & Pro Tips

### ฉันจะปรับปรุงความแม่นยำบน PNG ที่มีสัญญาณรบกวนได้อย่างไร?

- แปลงภาพเป็นระดับสีเทา: `img = img.convert('L')`  
- ใช้ threshold แบบไบนารี: `img = img.point(lambda x: 0 if x < 128 else 255, '1')`  
- ขยายขนาดด้วย `img = img.resize((img.width*2, img.height*2), Image.LANCZOS)`

ขั้นตอนเหล่านี้มักทำให้ **recognize image text** จากความยุ่งยากกลายเป็นผลลัพธ์ที่สะอาด

### ฉันสามารถประมวลผลโฟลเดอร์เต็มของ PNG ได้หรือไม่?

ได้เลย. ห่อการเรียก `recognize_image` ไว้ในลูป `for` ที่วนผ่าน `Path.glob("*.png")` แล้วเก็บผลลัพธ์ในดิกชันนารีหรือเขียนลง CSV เพื่อการวิเคราะห์ต่อไป

```python
for png in Path("my_folder").glob("*.png"):
    res = engine.recognize_image(str(png))
    print(f"{png.name}: {res.text[:50]}...")
```

### ถ้าฉันต้องการสกัดเฉพาะตัวเลขเท่านั้นจะทำอย่างไร?

ส่งสตริง **config** ที่กำหนดเองไปยัง `image_to_string`:

```python
digits = pytesseract.image_to_string(img, lang=self.lang, config='outputbase digits')
```

วิธีนี้คุณสามารถ **extract text from image** ที่มีตาราง, หมายเลขซีเรียล, หรือ timestamps ได้อย่างแม่นยำ

### มีวิธีรับคะแนนความเชื่อมั่นหรือไม่?

มี — ใช้ `pytesseract.image_to_data` ซึ่งคืนค่า TSV พร้อมคะแนนความเชื่อมั่นต่อคำ คุณสามารถกรองโทเคนที่ความเชื่อมั่นต่ำก่อนประกอบสตริงสุดท้ายได้

---

## Extending the Tutorial

เมื่อคุณเชี่ยวชาญพื้นฐานแล้ว ลองสำรวจหัวข้อที่เกี่ยวข้องต่อไปนี้:

- **Batch OCR with multiprocessing** – เร่งความเร็วการประมวลผลคอร์ปัส PNG ขนาดใหญ่  
- **Hybrid OCR + NLP pipelines** – แปลกรีกโบราณที่สกัดออกมาเป็นอังกฤษสมัยใหม่โดยอัตโนมัติ  
- **Alternative engines** – ทดลอง `easyocr` หรือวิธีการที่อิง `opencv` สำหรับกรณีใช้เฉพาะ  
- **Cloud OCR services** – Google Vision, Azure Computer Vision, หรือ AWS Textract สำหรับการขยายแบบ serverless  

แต่ละหัวข้อนี้ต่อยอดจาก **python ocr example** ที่เราได้ครอบคลุมแล้ว ทำให้คุณพร้อมลุยต่อไปอย่างมั่นใจ

---

## Conclusion

เราได้เริ่มจากสแนปเพล็ตเล็ก ๆ แล้วพัฒนาเป็น workflow **ocr png image** ที่แข็งแรงใน Python โดยสร้าง `OcrEngine` ตั้งค่าภาษาเป็น Greek polytonic ส่ง PNG เข้า engine และพิมพ์ผลลัพธ์ ตอนนี้คุณรู้วิธี **extract text from image**, **recognize image text**, และแม้กระทั่ง **read ancient greek**

## คุณควรเรียนรู้อะไรต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอน‑ขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานทางเลือกในโปรเจกต์ของคุณเอง

- [สกัดข้อความจากรูปภาพด้วย Aspose OCR – คู่มือขั้นตอนต่อขั้นตอน](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [วิธีตั้งค่าค่าธรณีใน OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)
- [จดจำข้อความจากภาพด้วย Aspose OCR สำหรับหลายภาษา](/ocr/english/net/ocr-settings/working-with-different-languages/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}