---
category: general
date: 2026-06-22
description: كيفية تغيير اللغة في محركات OCR بسرعة. تعلم ضبط لغة OCR العربية (ar)
  باستخدام كود بسيط وتجنب الأخطاء الشائعة.
draft: false
keywords:
- how to change language
- ocr language arabic
- how to set OCR
- change OCR language
- set language OCR
language: ar
og_description: تم شرح كيفية تغيير اللغة في محركات OCR في الجملة الأولى. اتبع هذا
  الدليل لتعيين لغة OCR العربية بسرعة.
og_title: كيفية تغيير اللغة في OCR – دليل كامل
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
title: كيفية تغيير اللغة في OCR – ضبط اللغة العربية خطوة بخطوة
url: /ar/python-java/general/how-to-change-language-in-ocr-set-arabic-language-step-by-st/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تغيير اللغة في OCR – دليل برمجي كامل

تغيير اللغة في محركات OCR هو عائق شائع عندما تبدأ بالتعامل مع مستندات متعددة اللغات. في هذا الدرس سنرشدك إلى الخطوات الدقيقة لتعيين لغة OCR إلى العربية، مع مثال شفرة قابل للتنفيذ وتفسيرات لكل سطر. إذا تساءلت يومًا *"كيف تضبط OCR* إلى نص مختلف دون كسر سير العمل*، فأنت في المكان الصحيح*.

سنغطي كل ما تحتاجه: المكتبات المطلوبة، كيفية الحصول على نسخة محرك OCR، كيفية الوصول إلى إعداداته، وأخيرًا كيفية تغيير لغة OCR بأمان. في النهاية ستتمكن من التحويل من الإنجليزية إلى العربية (أو أي لغة مدعومة أخرى) باستدعاء طريقة واحدة. لا سحر، فقط شفرة واضحة وبعض النصائح العملية.

## المتطلبات المسبقة

- Python 3.8+ (أو أي إصدار حديث)
- مكتبة OCR تُظهر كائن إعدادات – المثال يستخدم **pytesseract** ملفوفًا في فئة مساعدة صغيرة، لكن النمط نفسه يعمل مع محركات أخرى مثل EasyOCR أو Microsoft Computer Vision SDK.
- بيانات اللغة العربية مثبتة لمحرك OCR (`ara.traineddata` لـ Tesseract).  
  *نصيحة احترافية:* على Ubuntu يمكنك تثبيتها باستخدام `sudo apt-get install tesseract-ocr-ara`.

## نظرة عامة على كيفية تغيير اللغة في OCR

تغيير اللغة هو في الأساس رقصة من ثلاث خطوات:

1. **الحصول على نسخة محرك OCR** – عادةً ما تكون كائنًا أحاديًا أو مُنشأً عبر مصنع.
2. **استخراج كائن الإعدادات** – معظم المكتبات تحتفظ باللغة، DPI، وغيرها من الخيارات في حاوية إعدادات منفصلة.
3. **تعيين رمز اللغة** – للغة العربية رمز ISO‑639‑2 هو `"ar"`.

فيما يلي سكريبت بسيط، قابل للتنفيذ بالكامل، يوضح هذه الخطوات.

![How to change language in OCR screenshot](image-placeholder.png "How to change language in OCR example")

## الخطوة 1: إنشاء أو الحصول على نسخة محرك OCR

أولاً نحتاج إلى محرك. في المشاريع الحقيقية قد يتم إنشاء المحرك في مكان آخر وتمريره؛ من أجل الوضوح سنقوم بإنشائه هنا مباشرة.

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

**لماذا نغلف المحرك** – العديد من SDKs الخاصة بـ OCR (بما في ذلك Tesseract) تتوقع تمرير اللغة كسلسلة نصية في كل استدعاء. من خلال تجميع الخيارات في كائن إعدادات نحصل على واجهة API نظيفة، *how to set OCR*‑style، تعكس المقتطف الأصلي الذي قدمته.

## الخطوة 2: الوصول إلى كائن إعدادات المحرك

الآن بعد أن حصلنا على محرك، نسترجع إعداداته. هذا يعكس السطر الثاني من المثال الأصلي (`settings = engine.get_settings()`).

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

هنا نعرض طريقة **how to set OCR** لتعيين اللغة عبر `set_language`. الطريقة أيضًا تقوم بفحص أساسي للمنطق، وهو عادةً ما يكون عادةً برمجة دفاعية جيدة.

## الخطوة 3: تعيين لغة OCR إلى العربية (ocr language arabic)

أخيرًا نستدعي الطريقة مع رمز اللغة العربية `"ar"`. هذا هو جوهر عملية *change OCR language*.

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

**الناتج المتوقع**

```
Current OCR language: ar
```

إذا أزلت التعليق عن استدعاء `recognize` ووجهته إلى صورة عربية حقيقية، يجب أن ترى الأحرف العربية مطبوعة في وحدة التحكم (بشرط أن تكون بيانات اللغة مثبتة).

## كيفية ضبط OCR لعدة لغات

أحيانًا تحتاج إلى *ocr language arabic* **بالإضافة إلى** الإنجليزية، خاصةً في المستندات المختلطة. يمكن لطريقة `set_language` قبول قائمة مفصولة بـ `+`:

```python
settings.set_language("ar+eng")
print("Now recognizing both Arabic and English:", settings.get_language())
```

*حالة حافة*: إذا لم يكن حزمة اللغة المطلوبة مثبتة، سيُظهر Tesseract خطأً مثل `Error opening language file`. لتجنب الانهيار، يمكنك التقاط الاستثناء والعودة إلى لغة افتراضية.

```python
try:
    settings.set_language("ar")
except Exception as e:
    print("Failed to set Arabic language:", e)
    settings.set_language("eng")  # fallback
```

## تغيير لغة OCR ديناميكيًا أثناء التشغيل

في العديد من التطبيقات يختار المستخدم لغةً من قائمة منسدلة. لأن الإعدادات تعيش داخل كائن المحرك، يمكنك تبديل اللغات أثناء التشغيل دون إعادة إنشاء المحرك.

```python
def switch_language(lang_code: str):
    settings.set_language(lang_code)
    print(f"OCR language switched to {lang_code}")

# Example usage:
switch_language("fr")   # switch to French
switch_language("ar")   # back to Arabic
```

هذا النمط يحقق متطلبات *set language OCR* مع الحفاظ على نظافة الشفرة.

## المشكلات الشائعة والنصائح الاحترافية

| المشكلة | ما يحدث | الحل |
|---------|----------|------|
| حزمة اللغة مفقودة | Tesseract يُعيد “Failed loading language ‘ar’” | ثبّت بيانات اللغة (`sudo apt-get install tesseract-ocr-ara` أو حمّلها من المستودع). |
| استخدام رمز ISO غير صحيح | لا مخرجات أو أحرف مشوشة | تحقق من الرمز (`ar` للعربية، `eng` للإنجليزية، `chi_sim` للصينية المبسطة). |
| نسيان إعادة بناء الإعدادات | المحرك لا يزال يستخدم اللغة القديمة | دائمًا استدعِ `engine._build_config()` (يُنفّذ داخليًا عند استدعاء `recognize`). |
| تمرير قائمة بدلاً من سلسلة | TypeError | استخدم `"ar+eng"` كسلسلة واحدة، وليس `["ar", "eng"]`. |

## مثال كامل يعمل (جميع الأجزاء معًا)

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

شغّل السكريبت باستخدام `python full_example.py`. إذا كان كل شيء مُعدًا، سترى:

```
Current OCR language: ar
```

…وإخراج OCR لصورتك العربية إذا فعلت السطرين الأخيرين.

## الخاتمة

أنت الآن تعرف **كيفية تغيير اللغة في محركات OCR**، وبشكل خاص كيفية تعيين لغة OCR إلى العربية باستخدام نمط نظيف وقابل لإعادة الاستخدام. استعرض الدليل الحصول على المحرك، الوصول إلى إعداداته، وأخيرًا تطبيق تغيير اللغة — مع تغطية كل من سيناريو *ocr language arabic* وحالة *change OCR language* الأوسع.  

ما الخطوة التالية؟ جرّب إضافة دعم لمزيد من اللغات، جرب سلاسل متعددة اللغات (`"ar+eng"`)، أو دمج هذه المنطق في خدمة ويب تسمح للمستخدمين بتحميل مستندات بأي نص. إذا كنت فضوليًا حول *set language OCR* في مكتبات أخرى (EasyOCR، Google Vision

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك الخاصة.

- [كيفية استخراج نص الصورة باستخدام OCR مع اللغة باستخدام Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [استخراج نص الصورة بلغة C# مع اختيار اللغة باستخدام Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [كيفية استخراج OCR – إعدادات OCR](/ocr/english/net/ocr-configuration/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}