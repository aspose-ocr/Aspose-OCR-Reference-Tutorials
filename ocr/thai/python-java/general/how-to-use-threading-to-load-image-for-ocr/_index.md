---
category: general
date: 2026-04-26
description: วิธีใช้ threading เพื่อโหลดรูปภาพสำหรับ OCR ใน Python. เรียนรู้การประมวลผล
  OCR แบบอะซิงโครนัสด้วย callbacks, background threads, และการโหลดรูปภาพในไม่กี่ขั้นตอน.
draft: false
keywords:
- how to use threading
- load image for OCR
- python threading OCR
- async OCR callback
- background thread image processing
language: th
og_description: วิธีใช้ threading เพื่อโหลดรูปภาพสำหรับ OCR ใน Python คู่มือนี้แสดงตัวอย่างที่สมบูรณ์และสามารถรันได้พร้อมกับการเรียกกลับและการทำงานในพื้นหลัง
og_title: วิธีใช้ Threading เพื่อโหลดภาพสำหรับ OCR
tags:
- Python
- Threading
- OCR
- Image Processing
title: วิธีใช้การทำงานหลายเธรดเพื่อโหลดภาพสำหรับ OCR
url: /th/python-java/general/how-to-use-threading-to-load-image-for-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีใช้ Threading เพื่อโหลด Image สำหรับ OCR

เคยสงสัย **วิธีใช้ threading** เพื่อโหลดภาพสำหรับ OCR โดยไม่ทำให้แอปของคุณค้างหรือไม่? นี่คือสถานการณ์ที่มักเกิดขึ้นไม่ว่าจะคุณกำลังสร้างเครื่องสแกนเดสก์ท็อป, บริการเว็บ, หรือสคริปต์ง่าย ๆ ที่ต้องประมวลผลรูปภาพจำนวนมาก ข่าวดีคือ เพียงไม่กี่บรรทัดของ Python พร้อมแพทเทิร์น threading ที่เหมาะสม จะทำให้ UI ของคุณตอบสนองได้เร็วขณะที่เอนจิน OCR ทำงานอยู่

ในบทเรียนนี้เราจะเดินผ่านตัวอย่างครบวงจรจากต้นจนจบ: โหลด PNG ขนาดใหญ่, เริ่ม OCR บนเธรดพื้นหลัง, และจัดการผลลัพธ์ด้วย callback. เมื่อจบคุณจะไม่เพียงรู้ **วิธีใช้ threading** เท่านั้น แต่ยังรู้ **วิธีโหลด Image สำหรับ OCR** อย่างสะอาดและนำกลับมาใช้ใหม่ได้

## สิ่งที่คุณต้องเตรียม

- Python 3.9+ (ไวยากรณ์ที่ใช้ทำงานได้กับเวอร์ชันล่าสุดทั้งหมด)
- `pillow` สำหรับจัดการภาพ (`pip install pillow`)
- `pytesseract` เป็น wrapper เบา ๆ รอบ Tesseract OCR (`pip install pytesseract`)
- ติดตั้ง Tesseract OCR engine บนเครื่องของคุณ (ดาวน์โหลดจาก [tesseract‑ocr.org](https://github.com/tesseract-ocr/tesseract))
- ไฟล์ภาพขนาดใหญ่ที่คุณต้องการประมวลผล (`large_image.png` ในคู่มือนี้)

ไม่มีเฟรมเวิร์กเพิ่มเติม, ไม่มี async/await—แค่ `threading` คลาสสิกและ callback

## Step 1: Import the Threading Module (Required for Background Execution)

สิ่งแรกที่เราทำคือ import โมดูล `threading`. โมดูลนี้ให้คลาส `Thread` ที่ทำให้เรารันฟังก์ชันใด ๆ ในเธรดของระบบปฏิบัติการแยกออกมา

```python
import threading
```

*ทำไมเรื่องนี้ถึงสำคัญ*: หากคุณรัน OCR บนเธรดหลัก โปรแกรมของคุณ (โดยเฉพาะ GUI) จะค้างจนกว่า OCR จะเสร็จ. การมอบหมายงานให้เธรดพื้นหลังทำให้เธรดหลักยังคงอิสระในการอัปเดต UI, รับอินพุตจากผู้ใช้, หรือเริ่มงานอื่นต่อไป

## Step 2: Define a Callback That Will Be Invoked When OCR Finishes

Callback คือฟังก์ชันที่โค้ดส่วนอื่นเรียกใช้เมื่อทำงานเสร็จ. ที่นี่เราจะพิมพ์ข้อความที่ OCR จดจำได้, แต่คุณก็สามารถเก็บไว้, ส่งผ่านเครือข่าย, หรืออัปเดตวิดเจ็ต UI ได้

```python
def ocr_done(result_text: str) -> None:
    """Called when the OCR thread finishes."""
    print("\n--- Async OCR finished ---")
    print(result_text)   # Display the recognized text
```

*เคล็ดลับ*: ทำให้ callback มีน้ำหนักเบา. การประมวลผลหนักภายใน callback จะทำลายประโยชน์ของ threading เพราะมันยังคงบล็อกเธรดที่เรียก (มักจะเป็นเธรดหลัก)

## Step 3: Load the Image You Want to Process

การโหลดภาพเป็นเรื่องแยกจาก OCR, แต่ก็เป็นส่วนหนึ่งของ workflow ทั้งหมด. การใช้ Pillow ทำให้เรื่องนี้ง่ายมาก

```python
from PIL import Image

def load_image(path: str) -> Image.Image:
    """Loads an image from disk and returns a Pillow Image object."""
    try:
        img = Image.open(path)
        print(f"Image '{path}' loaded – size: {img.size}")
        return img
    except Exception as exc:
        raise RuntimeError(f"Failed to load image: {exc}") from exc
```

*ทำไมเราทำที่นี่*: หากภาพใหญ่ การโหลดบนเธรดหลักอาจทำให้เกิดการกระตุกแล้ว. ในแอปจริง ๆ คุณอาจย้ายการโหลดไปยังเธรดอีกอันหนึ่ง, แต่เพื่อความชัดเจนเราจะทำแบบ synchronous ที่นี่

## Step 4: Create a Small OCR Engine Wrapper

โค้ดต้นฉบับใช้ `engine.process_async`. เราจะจำลองด้วยคลาสเล็ก ๆ ที่สร้างเธรดภายในและเรียก callback ที่ส่งมาเมื่อทำเสร็จ

```python
import pytesseract

class SimpleOcrEngine:
    """A minimal OCR engine that runs pytesseract in a background thread."""

    def __init__(self, image: Image.Image):
        self.image = image

    def _run_ocr(self, callback):
        """Internal method executed in the worker thread."""
        try:
            # pytesseract returns the recognized text as a plain string
            text = pytesseract.image_to_string(self.image)
            callback(text)
        except Exception as exc:
            callback(f"OCR failed: {exc}")

    def process_async(self, callback):
        """Public method to start OCR on a new thread."""
        worker = threading.Thread(target=self._run_ocr, args=(callback,))
        worker.daemon = True          # Daemon so it won’t block program exit
        worker.start()
        print("OCR thread started…")
```

*คำอธิบาย*:  
- `_run_ocr` ทำงานหนักจริง.  
- `process_async` สร้างอ็อบเจ็กต์ `Thread`, ตั้งให้เป็น daemon (เพื่อให้ interpreter สามารถออกได้แม้เธรดยังทำงาน), แล้วเริ่มเธรด.  
- Callback จะได้รับข้อความ OCR หรือข้อความข้อผิดพลาด

## Step 5: Tie Everything Together and Do Other Work While OCR Runs

ตอนนี้เราจะจัดระเบียบ flow ทั้งหมด: โหลดภาพ, สร้างอินสแตนซ์ของ engine, เริ่ม OCR แบบ async, แล้วให้เธรดหลักทำอย่างอื่นต่อ (ที่นี่เราจะพิมพ์ข้อความ)

```python
if __name__ == "__main__":
    # 1️⃣ Load the image you want to OCR
    img_path = "YOUR_DIRECTORY/large_image.png"
    image = load_image(img_path)

    # 2️⃣ Create the OCR engine instance
    engine = SimpleOcrEngine(image)

    # 3️⃣ Start OCR on a background thread, passing our callback
    engine.process_async(callback=ocr_done)

    # 4️⃣ Do other work while OCR runs (simulated with a loop)
    for i in range(5):
        print(f"Main thread doing other work… ({i+1}/5)")
        # In a real app you might update a progress bar, handle UI events, etc.
        threading.Event().wait(0.5)  # Sleep 0.5 s without blocking the OS thread

    # Give the OCR thread a moment to finish before the script exits
    threading.Event().wait(2)
    print("Script finished.")
```

**ผลลัพธ์ที่คาดหวัง (ตัดทอนเพื่อความกระชับ):**

```
Image 'YOUR_DIRECTORY/large_image.png' loaded – size: (3840, 2160)
OCR thread started…
Main thread doing other work… (1/5)
Main thread doing other work… (2/5)
...
--- Async OCR finished ---
The quick brown fox jumps over the lazy dog.
Script finished.
```

หาก OCR ล้มเหลว, callback จะพิมพ์ข้อความข้อผิดพลาดแทนข้อความผลลัพธ์

---

## ทำไมวิธีนี้จึงดีกว่าการวนลูปแบบธรรมดา

- **Responsiveness**: เธรดหลักไม่บล็อกการเรียก OCR, ซึ่งอาจใช้เวลาหลายนาทีสำหรับภาพขนาดใหญ่
- **Scalability**: คุณสามารถสปินหลายอินสแตนซ์ของ `SimpleOcrEngine`, แต่ละอันทำงานบนเธรดของตนเอง เพื่อประมวลผลชุดภาพพร้อมกัน
- **Separation of Concerns**: การโหลด, การประมวลผล, และการจัดการผลลัพธ์ถูกแยกออกอย่างชัดเจน ทำให้โค้ดง่ายต่อการทดสอบและบำรุงรักษา

## ข้อผิดพลาดทั่วไปและวิธีหลีกเลี่ยง

| Pitfall | What Happens | Fix |
|---------|--------------|-----|
| Forgetting to mark the thread as *daemon* | สคริปต์ค้างหลังจากงานหลักเสร็จ เพราะเธรด OCR ยังคงทำงานอยู่ | ตั้ง `worker.daemon = True` **หรือ** `join()` เธรดก่อนออกจากโปรแกรม |
| Using a global variable for the result without locks | สภาพการแข่งขัน (race condition) ทำให้ข้อมูลเสียหายเมื่อหลายเธรดเขียนพร้อมกัน | ส่งผลลัพธ์ผ่าน callback (เช่นทำ) หรือใช้คอนเทนเนอร์ที่ปลอดเธรดเช่น `queue.Queue` |
| Loading a massive image on the main thread | UI ค้างก่อนที่ OCR พื้นหลังจะเริ่มทำงาน | ย้ายการโหลดภาพไปยังเธรดอีกอันหนึ่ง, หรือใช้เทคนิค lazy loading |
| Not handling exceptions inside the worker thread | ข้อผิดพลาดที่ไม่จับจะทำให้เธรดตายโดยเงียบ, ไม่ได้ผลลัพธ์ใด ๆ | ห่อโลจิก OCR ด้วย `try/except` แล้วส่งข้อผิดพลาดไปยัง callback |

## การต่อยอดรูปแบบนี้

- **Progress Reporting**: ใช้ `queue.Queue` ร่วมกันเพื่อส่งเปอร์เซ็นต์ความคืบหน้าแบบกึ่งเรียลไทม์จากเธรด OCR ไปยังเธรดหลัก
- **Thread Pool**: สำหรับการประมวลผลเป็นชุด, แทนที่การสร้าง `Thread` แยก ๆ ด้วย `concurrent.futures.ThreadPoolExecutor`
- **GUI Integration**: ในแอป Tkinter หรือ PyQt, ให้กำหนดเวลาเรียก callback ด้วย `after()` (Tkinter) หรือ `QTimer.singleShot` (Qt) เพื่อให้การอัปเดต UI เกิดบนเธรดหลัก

## Full Working Example (Copy‑Paste Ready)

```python
import threading
from PIL import Image
import pytesseract

def ocr_done(result_text: str) -> None:
    """Callback invoked when OCR finishes."""
    print("\n--- Async OCR finished ---")
    print(result_text)

def load_image(path: str) -> Image.Image:
    """Load an image and report its size."""
    try:
        img = Image.open(path)
        print(f"Image '{path}' loaded – size: {img.size}")
        return img

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}