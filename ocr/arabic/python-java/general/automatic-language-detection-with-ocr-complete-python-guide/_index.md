---
category: general
date: 2026-05-31
description: اكتشاف اللغة التلقائي في OCR أصبح سهلًا. تعلّم كيفية تحميل صورة OCR،
  وتفعيل اكتشاف اللغة التلقائي، والتعرف على نص الصورة في بضع خطوات فقط.
draft: false
keywords:
- automatic language detection
- recognize text image
- load image ocr
- enable auto language detection
- detect language ocr
language: ar
og_description: اكتشاف اللغة تلقائيًا في OCR أصبح سهلًا. اتبع هذا الدليل خطوة بخطوة
  لتمكين اكتشاف اللغة التلقائي، وتحميل OCR للصورة، والتعرف على نص الصورة.
og_title: اكتشاف اللغة تلقائيًا باستخدام OCR – دليل بايثون الكامل
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Automatic language detection in OCR made easy. Learn how to load image
    OCR, enable auto language detection, and recognize text image in just a few steps.
  headline: Automatic Language Detection with OCR – Complete Python Guide
  type: TechArticle
- description: Automatic language detection in OCR made easy. Learn how to load image
    OCR, enable auto language detection, and recognize text image in just a few steps.
  name: Automatic Language Detection with OCR – Complete Python Guide
  steps:
  - name: Python 3.8+ installed (any recent version works).
    text: Python 3.8+ installed (any recent version works).
  - name: 'The OCR library that provides `OcrEngine`, `LanguageAutoDetectMode`, etc.
      – for this guide we’ll assume a hypothetical package called `myocr`. Install
      it with:'
    text: 'The OCR library that provides `OcrEngine`, `LanguageAutoDetectMode`, etc.
      – for this guide we’ll assume a hypothetical package called `myocr`. Install
      it with:'
  - name: An image file (`multilingual_sample.png`) that contains text in at least
      two different languages.
    text: An image file (`multilingual_sample.png`) that contains text in at least
      two different languages.
  - name: A little curiosity—if you’ve never touched OCR before, don’t worry; the
      code is deliberately straightforward.
    text: A little curiosity—if you’ve never touched OCR before, don’t worry; the
      code is deliberately straightforward.
  type: HowTo
tags:
- OCR
- Python
- Multilingual
- Computer Vision
title: الكشف التلقائي عن اللغة باستخدام OCR – دليل بايثون الكامل
url: /ar/python-java/general/automatic-language-detection-with-ocr-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# الكشف التلقائي عن اللغة باستخدام OCR – دليل بايثون كامل

هل تساءلت يوماً كيف تجعل محرك OCR *يخمن* لغة المستند الممسوح ضوئياً دون أن تخبره بما يبحث عنه؟ هذا بالضبط ما يفعله **الكشف التلقائي عن اللغة**، وهو تغيير جذري عندما تتعامل مع ملفات PDF متعددة اللغات، أو صور لعلامات الشوارع، أو أي صورة تمزج بين خطوط مختلفة.  

في هذا الدرس سنستعرض مثالاً عملياً يوضح لك كيفية **تمكين الكشف التلقائي عن اللغة**، **تحميل OCR للصورة**، و**التعرف على نص الصورة** باستخدام واجهة برمجة تطبيقات على نمط بايثون. في النهاية ستحصل على سكريبت مستقل يطبع كل من رمز اللغة المكتشفة والنص المستخرج—دون الحاجة لتحديد اللغة يدوياً.

## ما ستتعلمه

- كيفية إنشاء كائن محرك OCR وتفعيل **الكشف التلقائي عن اللغة**.  
- الخطوات الدقيقة **لتحميل OCR للصورة** من القرص.  
- كيفية استدعاء طريقة `recognize()` للمحرك والحصول على نتيجة تتضمن رمز اللغة.  
- نصائح للتعامل مع الحالات الخاصة مثل الصور منخفضة الدقة أو الخطوط غير المدعومة.  

لا تحتاج إلى خبرة سابقة في OCR متعدد اللغات؛ فقط إعداد بسيط لبايثون وملف صورة.

---

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

1. تثبيت Python 3.8+ (أي نسخة حديثة تعمل).  
2. مكتبة OCR التي توفر `OcrEngine`، `LanguageAutoDetectMode`، إلخ – في هذا الدليل سنفترض حزمة افتراضية تسمى `myocr`. ثبّتها باستخدام:

   ```bash
   pip install myocr
   ```

3. ملف صورة (`multilingual_sample.png`) يحتوي على نص على الأقل بلغتين مختلفتين.  
4. قليل من الفضول—إذا لم تتعامل مع OCR من قبل، لا تقلق؛ الكود بسيط ومباشر.

---

## الخطوة 1: تمكين الكشف التلقائي عن اللغة

أول شيء عليك فعله هو إخبار المحرك بأنه يجب أن *يكتشف* اللغة بنفسه. هنا يأتي دور علم **الكشف التلقائي عن اللغة**.

```python
from myocr import OcrEngine, LanguageAutoDetectMode

# Step 1: Create an OCR engine instance
engine = OcrEngine()

# Step 2: Enable automatic language detection
engine.language_auto_detect_mode = LanguageAutoDetectMode.AUTO_DETECT
```

> **لماذا هذا مهم:**  
> عندما يتم ضبط `AUTO_DETECT`، يقوم المحرك بتشغيل مصنف لغة خفيف الوزن على الصورة قبل أن يبدأ التعرف الثقيل على الأحرف. هذا يعني أنك لا تحتاج إلى تخمين ما إذا كان النص إنجليزياً، روسياً، فرنسياً، أو أي تركيبة أخرى. سيختار المحرك تلقائياً نموذج اللغة الأنسب لكل منطقة من الصورة.

---

## الخطوة 2: تحميل OCR للصورة

الآن بعد أن علم المحرك أنه يجب أن يكتشف اللغات تلقائياً، نحتاج إلى تزويده بشيء يعمل عليه. خطوة **تحميل OCR للصورة** تقرأ البت ماب وتجهز المخازن الداخلية.

```python
# Step 3: Load the image containing multilingual text
image_path = "YOUR_DIRECTORY/multilingual_sample.png"
engine.load_image(image_path)
```

> **نصيحة احترافية:**  
> إذا كانت صورتك أكبر من 300 dpi، فكر في تقليل حجمها إلى حوالي 150‑200 dpi. التفاصيل الزائدة قد تُبطئ مرحلة الكشف عن اللغة دون تحسين الدقة.

---

## الخطوة 3: التعرف على نص الصورة

مع الصورة في الذاكرة وتفعيل الكشف عن اللغة، الخطوة الأخيرة هي طلب من المحرك **التعرف على نص الصورة**. هذه الدعوة الواحدة تقوم بكل العمل الشاق.

```python
# Step 4: Perform OCR recognition
result = engine.recognize()
```

`result` هو كائن يحتوي عادةً على خاصيتين على الأقل:

| الخاصية | الوصف |
|-----------|-------------|
| `language` | رمز ISO‑639‑1 للغة المكتشفة (مثال: `"en"` للإنجليزية). |
| `text`     | النص المستخرج من الصورة كـ plain‑text. |

---

## الخطوة 4: استرجاع اللغة المكتشفة والنص المستخرج

الآن نطبع ما اكتشفه المحرك. هذا يوضح قدرة **detect language OCR** عملياً.

```python
# Step 5: Display the detected language and extracted text
print("Detected language:", result.language)   # e.g. "en", "ru", "fr"
print("Text:", result.text)
```

**نموذج المخرجات**

```
Detected language: fr
Text: Bonjour le monde! This is a multilingual sample.
```

> **ماذا لو أعاد المحرك `None`؟**  
> عادةً ما يعني ذلك أن الصورة غير واضحة أو أن النص صغير جداً (< 8 pt). حاول زيادة التباين أو استخدام مصدر بدقة أعلى.

---

## مثال كامل يعمل (تمكين الكشف التلقائي عن اللغة من البداية إلى النهاية)

بجمع كل ما سبق، إليك سكريبت جاهز للتنفيذ يغطي **تمكين الكشف التلقائي عن اللغة**، **تحميل OCR للصورة**، **التعرف على نص الصورة**، و**الكشف عن اللغة** في خطوة واحدة.

```python
# automatic_language_detection_ocr.py
from myocr import OcrEngine, LanguageAutoDetectMode

def main():
    # Create engine and turn on auto language detection
    engine = OcrEngine()
    engine.language_auto_detect_mode = LanguageAutoDetectMode.AUTO_DETECT

    # Load the image (adjust the path to your own file)
    image_path = "YOUR_DIRECTORY/multilingual_sample.png"
    engine.load_image(image_path)

    # Run OCR
    result = engine.recognize()

    # Output results
    print("Detected language:", result.language)
    print("Text:", result.text)

if __name__ == "__main__":
    main()
```

احفظه باسم `automatic_language_detection_ocr.py`، استبدل `YOUR_DIRECTORY` بالمجلد الذي يحتوي على ملف PNG، ثم شغّله:

```bash
python automatic_language_detection_ocr.py
```

ستظهر لك رمز اللغة متبوعاً بالنص المستخرج، تماماً كما في مثال المخرجات أعلاه.

---

## التعامل مع الحالات الشائعة

| الحالة | الحل المقترح |
|-----------|----------------|
| **صورة ذات دقة منخفضة جداً** (أقل من 100 dpi) | قم بزيادة الدقة باستخدام مرشح بيكوبك قبل التحميل، أو اطلب مصدرًا بدقة أعلى. |
| **خطوط مختلطة في صورة واحدة** (مثال: إنجليزي + سيريلي) | عادةً ما يقسم المحرك الصفحة إلى مناطق؛ إذا لاحظت أخطاء في الكشف، اضبط `engine.enable_region_split = True`. |
| **لغة غير مدعومة** | تأكد أن مكتبة OCR تتضمن حزمة لغة للخط الذي تحتاجه؛ قد تحتاج إلى تحميل نماذج إضافية. |
| **معالجة دفعات كبيرة** | أنشئ المحرك مرة واحدة، ثم أعد استخدامه عبر عدة دورات `load_image` / `recognize` لتجنب تحميل النماذج مراراً. |

---

## نظرة بصرية عامة

![مثال على الكشف التلقائي للغة](https://example.com/auto-lang-detect.png "الكشف التلقائي عن اللغة")

*النص البديل:* مثال على الكشف التلقائي للغة يُظهر رمز اللغة المكتشف والنص المتعدد اللغات المستخرج.

---

## الخلاصة

لقد غطينا الآن **الكشف التلقائي عن اللغة** من البداية إلى النهاية—إنشاء المحرك، تفعيل الكشف التلقائي، تحميل صورة للـ OCR، التعرف على النص، وأخيراً استرجاع اللغة المكتشفة. يتيح لك هذا التدفق المتكامل معالجة المستندات متعددة اللغات دون الحاجة لتكوين نماذج اللغة يدوياً في كل مرة.

إذا كنت مستعداً للانتقال إلى مستوى أعلى، فكر في:

- **معالجة دفعات** مئات الصور باستخدام حلقة تعيد استخدام نفس كائن `OcrEngine`.  
- **معالجة ما بعد الاستخراج** للنص باستخدام مدقق إملائي أو محلل لغوي مخصص.  
- **دمج** السكريبت في خدمة ويب تستقبل تحميلات المستخدم وتعيد JSON يحتوي على حقلي `language` و `text`.

لا تتردد في تجربة صيغ صور مختلفة (`.jpg`, `.tif`) وملاحظة كيف تتغير دقة الكشف. هل لديك أسئلة أو صورة صعبة لا تُقرأ؟ اترك تعليقاً أدناه—برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [recognize text image with Aspose OCR for multiple languages](/ocr/english/net/ocr-settings/working-with-different-languages/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}