---
category: general
date: 2026-06-28
description: تعلم كيفية التعرف على النص من الصورة وإجراء OCR على الصورة باستخدام Aspose
  OCR للبايثون. يتضمن خطوات لتعيين لغة OCR واستخراج درجات الثقة.
draft: false
keywords:
- recognize text from image
- perform ocr on image
- how to set OCR language
language: ar
og_description: التعرف على النص من الصورة باستخدام Aspose OCR في بايثون. يوضح هذا
  الدليل كيفية تعيين لغة OCR، وإجراء OCR على الصورة، وقراءة مستويات الثقة.
og_title: التعرف على النص من الصورة – دورة شاملة لتقنية OCR بلغة بايثون
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Learn how to recognize text from image and perform OCR on image using
    Aspose OCR for Python. Includes steps to set OCR language and extract confidence
    scores.
  headline: recognize text from image with Aspose OCR – Complete Python Guide
  type: TechArticle
- description: Learn how to recognize text from image and perform OCR on image using
    Aspose OCR for Python. Includes steps to set OCR language and extract confidence
    scores.
  name: recognize text from image with Aspose OCR – Complete Python Guide
  steps:
  - name: What if my image contains multiple languages?
    text: 'Aspose OCR supports multi‑language detection, but you need to pass a **combined
      language flag**. For example, to handle both Latin and Cyrillic:'
  - name: How do I improve accuracy on low‑resolution images?
    text: '- **Pre‑process** the image: increase contrast, apply binarization, or
      upscale using a library like Pillow. - **Set the correct DPI** if you know it;
      Aspose respects the image metadata. - **Choose the right language**—the more
      specific you are, the better the model performs.'
  - name: Can I extract only certain regions of the image?
    text: Yes. Use the `recognizeRegion` method (not shown in the basic example) and
      pass a rectangle object defining the area of interest. This is handy when you
      only need a table or a specific block of text.
  type: HowTo
tags:
- OCR
- Python
- Aspose
title: التعرف على النص من الصورة باستخدام Aspose OCR – دليل بايثون الكامل
url: /ar/python-java/general/recognize-text-from-image-with-aspose-ocr-complete-python-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص من الصورة باستخدام Aspose OCR – دليل Python الكامل

هل احتجت يومًا إلى **التعرف على النص من الصورة** لكنك لم تكن متأكدًا أي مكتبة ستوفر لك السرعة والدقة معًا؟ لست وحدك. في عالم أتمتة المستندات، القدرة على **إجراء OCR على الصورة** هي مطلب يومي — سواء كنت تقوم برقمنة الإيصالات، أو مسح جوازات السفر، أو استخراج البيانات من العلامات متعددة اللغات.

في هذا الدرس سنستعرض مثالًا عمليًا يوضح بالضبط كيفية **التعرف على النص من الصورة** باستخدام Aspose OCR للغة Python، وسنغطي أيضًا **كيفية ضبط لغة OCR** حتى يعرف المحرك ما إذا كان يتعامل مع اللاتينية أو السيريالية أو أي نص آخر. في النهاية ستحصل على سكريبت جاهز للتنفيذ يطبع النص الكامل، وثقة كل سطر، وحتى الصناديق المحيطة بكل كلمة.

## ما ستحتاجه

- **Python 3.8+** (الكود يعمل على أي نسخة حديثة)
- حزمة **Aspose.OCR for Python via Java** – ثبّتها باستخدام `pip install aspose-ocr`
- ملف صورة (مثال: `mixed_script.png`) يحتوي على النص الذي تريد استخراجه
- بيئة تطوير أساسية أو محرر—VS Code، PyCharm، أو حتى محرر نص بسيط يكفي

لا توجد تبعيات ثقيلة، ولا ملفات تنفيذية أصلية تحتاج إلى تجميع. فقط تثبيت عبر pip وستكون جاهزًا.

## الخطوة 1: تثبيت واستيراد محرك OCR

أولًا، لنقم بتنزيل المكتبة إلى جهازك واستيراد الفئات التي ستحتاجها.

```python
# Install the package (run this once in your terminal)
# pip install aspose-ocr

# Import the OCR engine and the language enumeration
from asposeocrjava import OcrEngine, Language
```

> **نصيحة احترافية:** إذا كنت تعمل خلف بروكسي مؤسسي، أضف العلامة `--proxy` إلى أمر pip. سيوفر عليك الكثير من المتاعب لاحقًا.

## الخطوة 2: إنشاء المحرك و **كيفية ضبط لغة OCR**

إنشاء كائن `OcrEngine` بسيط مثل استدعاء المُنشئ الخاص به، لكن القوة الحقيقية تظهر عندما تخبر المحرك أي لغة يتوقعها. هذا هو الجزء الذي يجيب على سؤال **كيفية ضبط لغة OCR**.

```python
# Instantiate the OCR engine
ocr_engine = OcrEngine()

# Tell the engine we’re dealing with Latin script (you can pick others like Language.Cyrillic)
ocr_engine.setLanguage(Language.Latin)
```

لماذا هذا مهم؟ خوارزميات OCR تستخدم نماذج حروف خاصة بكل لغة؛ ضبط اللغة الصحيحة يعزز الدقة بشكل كبير، خاصةً للخطوط التي تشبه بعضها (مثل “0” مقابل “O” في اللاتينية مقابل “О” في السيريالية).

## الخطوة 3: **إجراء OCR على الصورة** – التعرف على النص

الآن نمرّر مسار الصورة إلى المحرك ونتركه يقوم بسحره. تُعيد الطريقة كائن `RecognitionResult` يحتوي على كل ما قد تحتاجه.

```python
# Path to the image you want to process
image_path = "YOUR_DIRECTORY/mixed_script.png"

# Run the OCR operation
recognition_result = ocr_engine.recognizeImage(image_path)
```

إذا لم يُعثر على الملف، سيُطلق Aspose استثناء `FileNotFoundError`. احرص على وضع الاستدعاء داخل كتلة `try/except` في الكود الإنتاجي—لا شيء أسوأ من استثناء غير مُعالَج يوقف خدمتك.

## الخطوة 4: إخراج النص الكامل المعترف به

أكثر الطلبات شيوعًا هو ببساطة “أعطني النص”. طريقة `getText()` تجمع جميع السطور المكتشفة في سلسلة واحدة.

```python
# Print the complete text extracted from the image
print("Full text:", recognition_result.getText())
```

ستظهر لك نتيجة مشابهة لـ:

```
Full text: Hello World!
This is a sample mixed‑script image.
```

هذا هو جوهر **التعرف على النص من الصورة**—سطر واحد يُعيد كل ما استطاع المحرك فك شفرته.

## الخطوة 5: (اختياري) إظهار مستوى الثقة لكل سطر تم اكتشافه

تُتيح لك درجات الثقة تقييم موثوقية النتائج. قد تحتاج إلى مراجعة السطور التي تكون درجتها أقل من 0.70 مثلاً.

```python
print("\n--- Line‑by‑Line Confidence ---")
for line in recognition_result.getLines():
    # Each line object provides its text and a confidence value between 0 and 1
    print(f"Line: '{line.getText()}'  Confidence: {line.getConfidence():.2f}")
```

نموذج للمخرجات:

```
Line: 'Hello World!'  Confidence: 0.98
Line: 'This is a sample mixed‑script image.'  Confidence: 0.85
```

## الخطوة 6: (اختياري) استرجاع الصناديق المحيطة لكل كلمة – مفيد لتسليط الضوء في واجهة المستخدم

إذا كنت تبني عارضًا يسمح للمستخدم بالنقر على كلمة لرؤية بيانات OCR الخاصة بها، فإن إحداثيات الصندوق المحيط هي ذهب.

```python
print("\n--- Word Bounding Boxes ---")
for word in recognition_result.getWords():
    bbox = word.getBoundingBox()   # Returns (x, y, width, height)
    print(f"Word '{word.getText()}' at {bbox}")
```

نموذج للمخرجات:

```
Word 'Hello' at (12, 34, 58, 20)
Word 'World' at (78, 34, 60, 20)
```

هذه الإحداثيات بوحدة البكسل نسبةً إلى الصورة الأصلية، لذا يمكنك رسمها مباشرةً على لوحة الرسم.

## البرنامج الكامل العامل

نجمع كل ما سبق في سكريبت جاهز للتنفيذ يمكنك وضعه في أي مشروع. فقط استبدل `YOUR_DIRECTORY/mixed_script.png` بالمسار الفعلي لصورتك.

```python
# ocr_demo.py
from asposeocrjava import OcrEngine, Language

def main(image_path: str, language: Language = Language.Latin):
    """
    Recognize text from an image using Aspose OCR.
    Parameters:
        image_path (str): Full path to the image file.
        language (Language): OCR language to use (default: Latin).
    """
    # Create the OCR engine and set the desired language
    ocr_engine = OcrEngine()
    ocr_engine.setLanguage(language)

    try:
        # Perform OCR
        result = ocr_engine.recognizeImage(image_path)

        # Full text output
        print("Full text:", result.getText())

        # Optional: line confidence
        print("\n--- Line‑by‑Line Confidence ---")
        for line in result.getLines():
            print(f"Line: '{line.getText()}'  Confidence: {line.getConfidence():.2f}")

        # Optional: word bounding boxes
        print("\n--- Word Bounding Boxes ---")
        for word in result.getWords():
            bbox = word.getBoundingBox()
            print(f"Word '{word.getText()}' at {bbox}")

    except FileNotFoundError:
        print(f"Error: Image file not found at {image_path}")
    except Exception as e:
        print(f"An unexpected error occurred: {e}")

if __name__ == "__main__":
    # Change the path below to point at your own test image
    IMAGE_PATH = "YOUR_DIRECTORY/mixed_script.png"
    main(IMAGE_PATH, Language.Latin)
```

شغّله باستخدام:

```bash
python ocr_demo.py
```

سترى النص المستخرج بالكامل، ودرجات الثقة، والصناديق المحيطة تُطبع في وحدة التحكم.

## أسئلة شائعة وحالات خاصة

### ماذا لو كانت صورتي تحتوي على لغات متعددة؟

يدعم Aspose OCR اكتشاف متعدد اللغات، لكن عليك تمرير **علامة لغة مركبة**. مثال لتعامل مع اللاتينية والسيريالية معًا:

```python
ocr_engine.setLanguage(Language.Latin | Language.Cyrillic)
```

عامل الـ `|` (الأنابيب) يدمج القيم enum. هذا يجيب على متطلبات **إجراء OCR على الصورة** في السيناريوهات متعددة اللغات.

### كيف أحسن الدقة في الصور منخفضة الدقة؟

- **معالجة مسبقة** للصورة: زيادة التباين، تطبيق التحويل إلى ثنائي، أو تكبير الحجم باستخدام مكتبة مثل Pillow.  
- **ضبط DPI الصحيح** إذا كنت تعرفه؛ Aspose يحترم بيانات التعريف الخاصة بالصورة.  
- **اختيار اللغة المناسبة**—كلما كنت أكثر تحديدًا، كلما كان النموذج أدق.

### هل يمكنني استخراج مناطق معينة فقط من الصورة؟

نعم. استخدم طريقة `recognizeRegion` (غير معروضة في المثال الأساسي) ومرّر كائن مستطيل يحدد منطقة الاهتمام. هذا مفيد عندما تحتاج فقط إلى جدول أو كتلة نصية محددة.

## الخلاصة

لقد استعرضنا مثالًا كاملاً من البداية إلى النهاية حول كيفية **التعرف على النص من الصورة** باستخدام Aspose OCR للغة Python. الآن تعرف كيف **تجري OCR على الصورة**، وتضبط **لغة OCR** بشكل صحيح، وتستخرج كل من درجات الثقة وصناديق الكلمات لاستخدامها في واجهات المستخدم.

من هنا يمكنك:

- تجربة لغات أخرى (`Language.Arabic`, `Language.Japanese`, إلخ)  
- دمج السكريبت في خدمة ويب (Flask/Django) لتقديم OCR كواجهة برمجة تطبيقات (API)  
- الجمع بين بيانات الصناديق والمحرك الأمامي لتسمح للمستخدمين بتمييز النص

الإمكانات واسعة بقدر المستندات التي تحتاج إلى رقمنتها. هل لديك صورة صعبة لا تستجيب؟ اترك تعليقًا وسنساعدك على حل المشكلة. برمجة سعيدة! 

![مثال على التعرف على النص من الصورة](/images/ocr_example.png "التعرف على النص من الصورة – مخرجات Aspose OCR")


## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [استخراج النص من الصورة باستخدام Aspose OCR – دليل خطوة بخطوة](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [التعرف على نص الصورة باستخدام Aspose OCR لعدة لغات](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [كيفية ضبط قيمة العتبة في التعرف على الصورة باستخدام OCR](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}