---
category: general
date: 2026-04-26
description: كيفية استخدام الخيوط لتحميل الصورة للتعرف الضوئي على الأحرف (OCR) في
  بايثون. تعلّم معالجة OCR غير المتزامنة باستخدام ردود النداء، الخيوط الخلفية، وتحميل
  الصور في بضع خطوات فقط.
draft: false
keywords:
- how to use threading
- load image for OCR
- python threading OCR
- async OCR callback
- background thread image processing
language: ar
og_description: كيفية استخدام الخيوط لتحميل الصورة للتعرف الضوئي على الأحرف في بايثون.
  يوضح هذا الدليل مثالًا كاملاً قابلاً للتنفيذ مع ردود النداء والتنفيذ في الخلفية.
og_title: كيفية استخدام الـ Threading لتحميل الصورة للتعرف الضوئي على الأحرف
tags:
- Python
- Threading
- OCR
- Image Processing
title: كيفية استخدام الـ Threading لتحميل الصورة للتعرف الضوئي على الأحرف
url: /ar/python-java/general/how-to-use-threading-to-load-image-for-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيف تستخدم الـ Threading لتحميل صورة للتعرف الضوئي على الأحرف (OCR)

هل تساءلت يومًا **كيف تستخدم الـ threading** لتحميل صورة للتعرف الضوئي على الأحرف (OCR) دون تجميد تطبيقك؟ هذا سيناريو يظهر سواء كنت تبني ماسحًا مكتبيًا، أو خدمة ويب، أو سكربت بسيط يعالج صورًا ضخمة. الخبر السار؟ بضع أسطر من بايثون والنمط الصحيح للـ threading سيجعل واجهة المستخدم سريعة بينما يعمل محرك الـ OCR بسحره.

في هذا الدرس سنستعرض مثالًا كاملًا من البداية إلى النهاية: تحميل ملف PNG كبير، تشغيل الـ OCR على خيط خلفي، ومعالجة النتيجة عبر رد نداء (callback). في النهاية لن تعرف فقط **كيف تستخدم الـ threading** بل أيضًا **كيفية تحميل صورة للتعرف الضوئي على الأحرف (OCR)** بطريقة نظيفة وقابلة لإعادة الاستخدام.

## ما ستحتاجه

- Python 3.9+ (الصياغة التي نستخدمها تعمل على أي نسخة حديثة)
- `pillow` لمعالجة الصور (`pip install pillow`)
- `pytesseract` كغلاف خفيف حول Tesseract OCR (`pip install pytesseract`)
- محرك Tesseract OCR مثبت على جهازك (حمّله من [tesseract‑ocr.org](https://github.com/tesseract-ocr/tesseract))
- ملف صورة كبير تريد معالجته (`large_image.png` في هذا الدليل)

لا أطر إضافية، لا async/await — فقط `threading` الكلاسيكي ورد نداء (callback).

## الخطوة 1: استيراد وحدة الـ Threading (مطلوبة للتنفيذ في الخلفية)

أول شيء نفعله هو استيراد وحدة `threading`. تُعطينا فئة `Thread` التي تسمح لنا بتشغيل أي دالة في خيط نظام تشغيل منفصل.

```python
import threading
```

*لماذا هذا مهم*: إذا شغّلت الـ OCR على الخيط الرئيسي، سيتجمد برنامجك (خاصةً واجهة المستخدم) حتى ينتهي الـ OCR. بتفويض العمل إلى خيط خلفي، يبقى الخيط الرئيسي حرًا لتحديث الواجهة، ومعالجة إدخال المستخدم، أو بدء مهام أخرى.

## الخطوة 2: تعريف رد نداء (Callback) سيتم استدعاؤه عند انتهاء الـ OCR

رد النداء هو ببساطة دالة يستدعيها جزء آخر من الشيفرة عندما ينتهي. هنا سنطبع النص المُعترف به، لكن يمكنك تخزينه، إرساله عبر الشبكة، أو تحديث عنصر واجهة المستخدم.

```python
def ocr_done(result_text: str) -> None:
    """Called when the OCR thread finishes."""
    print("\n--- Async OCR finished ---")
    print(result_text)   # Display the recognized text
```

*نصيحة احترافية*: اجعل رد النداء خفيفًا. المعالجة الثقيلة داخل رد النداء تُفقد الفائدة من الـ threading لأنه سيظل يحجز الخيط الذي استدعاه (غالبًا الخيط الرئيسي).

## الخطوة 3: تحميل الصورة التي تريد معالجتها

تحميل الصورة أمر منفصل عن الـ OCR، لكنه لا يزال جزءًا من سير العمل العام. استخدام Pillow يجعل ذلك سهلًا.

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

*لماذا نفعل ذلك هنا*: إذا كانت الصورة ضخمة، قد يسبب تحميلها على الخيط الرئيسي تباطؤًا. في العديد من التطبيقات الواقعية قد تفرغ التحميل إلى خيط، لكن للوضوح نحتفظ به متزامنًا.

## الخطوة 4: إنشاء غلاف بسيط لمحرك الـ OCR

المقتطف الأصلي استخدم `engine.process_async`. سنحاكي ذلك بفئة صغيرة تبدأ خيطًا داخليًا وتستدعي رد النداء المزوَّد عند الانتهاء.

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

*شرح*:  
- `_run_ocr` يقوم بالعمل الشاق.  
- `process_async` ينشئ كائن `Thread`، يضعه كـ daemon (حتى يتمكن المفسر من الخروج حتى لو كان الخيط لا يزال يعمل)، ويبدأه.  
- رد النداء يتلقى إما نص الـ OCR أو رسالة خطأ.

## الخطوة 5: ربط كل شيء معًا والقيام بأعمال أخرى أثناء تشغيل الـ OCR

الآن نقوم بتنظيم التدفق بالكامل: تحميل الصورة، إنشاء المحرك، إطلاق الـ OCR غير المتزامن، وإبقاء الخيط الرئيسي مشغولًا بشيء آخر (هنا نطبع رسالة فقط).

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

**الناتج المتوقع (مقتطع للاختصار):**

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

إذا فشل الـ OCR، سيطبع رد النداء رسالة خطأ بدلًا من النص.

---

## لماذا يعمل هذا النهج أفضل من حلقة بسيطة

- **الاستجابة**: الخيط الرئيسي لا يُحجز أبدًا عند استدعاء الـ OCR، والذي قد يستغرق ثوانٍ للصور الكبيرة.
- **القابلية للتوسع**: يمكنك تشغيل عدة نسخ من `SimpleOcrEngine`، كل واحدة في خيطها الخاص، لمعالجة دفعة من الصور بشكل متزامن.
- **فصل المسؤوليات**: التحميل، المعالجة، ومعالجة النتيجة مفصولة بوضوح، مما يجعل الشيفرة أسهل للاختبار والصيانة.

## الأخطاء الشائعة وكيفية تجنّبها

| المشكلة | ما يحدث | الحل |
|---------|----------|------|
| نسيان وضع الخيط كـ *daemon* | يبقى السكربت معلقًا بعد انتهاء العمل الرئيسي لأن خيط الـ OCR لا يزال حيًا. | عيّن `worker.daemon = True` **أو** استدعِ `join()` للخيط قبل الخروج. |
| استخدام متغيّر عام للنتيجة بدون أقفال | قد تتسبب حالات السباق في فساد البيانات عندما يكتب عدة خيوط في آن واحد. | مرّر النتيجة عبر رد نداء (كما نفعل) أو استخدم حاويات آمنة للـ threading مثل `queue.Queue`. |
| تحميل صورة ضخمة على الخيط الرئيسي | تتجمد واجهة المستخدم قبل أن يبدأ الـ OCR في الخلفية. | فرّغ تحميل الصورة إلى خيط أيضًا، أو استخدم تقنيات التحميل الكسول. |
| عدم معالجة الاستثناءات داخل خيط العامل | الاستثناءات غير الملتقطة تقتل الخيط صامتًا، وتتركك بدون نتيجة. | غلف منطق الـ OCR بـ `try/except` ومرّر الخطأ إلى رد النداء. |

## توسيع هذا النمط

- **تقارير التقدم**: استخدم `queue.Queue` مشترك لدفع نسب التقدم المتوسطة من خيط الـ OCR إلى الخيط الرئيسي.
- **مجموعة الخيوط (Thread Pool)**: للمعالجة الدفعية، استبدل كائنات `Thread` الفردية بـ `concurrent.futures.ThreadPoolExecutor`.
- **دمج مع واجهة المستخدم**: في تطبيق Tkinter أو PyQt، جدولة رد النداء باستخدام `after()` (Tkinter) أو `QTimer.singleShot` (Qt) لضمان حدوث تحديثات الواجهة على الخيط الرئيسي.

## مثال كامل يعمل (جاهز للنسخ واللصق)

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