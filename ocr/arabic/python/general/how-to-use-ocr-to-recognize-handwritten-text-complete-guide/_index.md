---
category: general
date: 2026-03-28
description: كيفية استخدام تقنية التعرف الضوئي على الأحرف (OCR) للتعرف على النص المكتوب
  يدويًا في الصور. تعلم استخراج النص المكتوب يدويًا، تحويل الصورة المكتوبة يدويًا،
  والحصول على نتائج نظيفة بسرعة.
draft: false
keywords:
- how to use OCR
- recognize handwritten text
- extract handwritten text
- handwritten note to text
- convert handwritten image
language: ar
og_description: كيفية استخدام تقنية OCR للتعرف على النص المكتوب يدوياً. يوضح لك هذا
  الدرس خطوة بخطوة كيفية استخراج النص المكتوب يدوياً من الصور والحصول على نتائج مصقولة.
og_title: كيفية استخدام تقنية OCR للتعرف على النص المكتوب بخط اليد – دليل شامل
tags:
- OCR
- Handwriting Recognition
- Python
title: كيفية استخدام OCR للتعرف على النص المكتوب بخط اليد – دليل شامل
url: /ar/python/general/how-to-use-ocr-to-recognize-handwritten-text-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام OCR للتعرف على النص المكتوب بخط اليد – دليل كامل

كيفية استخدام OCR للملاحظات المكتوبة بخط اليد هو سؤال يطرحه العديد من المطورين عندما يحتاجون إلى رقمنة الرسومات، محاضر الاجتماعات، أو الأفكار السريعة المكتوبة. في هذا الدليل سنستعرض الخطوات الدقيقة للتعرف على النص المكتوب بخط اليد، استخراج النص المكتوب بخط اليد، وتحويل صورة مكتوبة بخط اليد إلى سلاسل نظيفة قابلة للبحث.  

إذا سبق لك أن حدقت في صورة لقائمة بقالة وتساءلت، “هل يمكنني تحويل هذه الصورة المكتوبة بخط اليد إلى نص دون كتابة كل شيء مرة أخرى؟” – فأنت في المكان الصحيح. بحلول النهاية ستحصل على سكريبت جاهز للتنفيذ يحول **ملاحظة مكتوبة بخط اليد إلى نص** في ثوانٍ.

## ما ستحتاجه

- Python 3.8+ (الكود يعمل مع أي نسخة حديثة)  
- مكتبة `ocr` – ثبّتها باستخدام `pip install ocr-sdk` (استبدل باسم حزمة موفر الخدمة الخاص بك)  
- صورة واضحة لملاحظة مكتوبة بخط اليد (`hand_note.png` في المثال)  
- قليل من الفضول وفنجان قهوة ☕️ (اختياري لكن يُنصح به)

لا أطر عمل ثقيلة، ولا مفاتيح سحابية مدفوعة – مجرد محرك محلي يدعم **التعرف على الخط المكتوب بخط اليد** مباشرةً.

## الخطوة 1 – تثبيت حزمة OCR واستيرادها

أولاً، لنحصل على الحزمة الصحيحة على جهازك. افتح الطرفية وشغّل:

```bash
pip install ocr-sdk
```

بعد انتهاء التثبيت، استورد الوحدة في سكريبتك:

```python
# Step 1: Import the OCR SDK
import ocr
```

> **نصيحة احترافية:** إذا كنت تستخدم بيئة افتراضية، فعّلها قبل التثبيت. هذا يحافظ على نظافة مشروعك ويتجنب تعارض الإصدارات.

## الخطوة 2 – إنشاء محرك OCR وتفعيل وضع الخط المكتوب بخط اليد

الآن نحتاج إلى **كيفية استخدام OCR** – نحتاج إلى كائن محرك يعرف أننا نتعامل مع خطوط منحنية بدلاً من خطوط مطبوعة. المقتطف التالي ينشئ المحرك ويحول وضعه إلى وضع الخط المكتوب بخط اليد:

```python
# Step 2: Initialize the OCR engine for handwritten text
ocr_engine = ocr.OcrEngine()
ocr_engine.recognition_mode = ocr.RecognitionMode.HANDWRITTEN
```

لماذا نضبط `recognition_mode`؟ لأن معظم محركات OCR تفضّل الكشف عن النص المطبوع افتراضيًا، مما يتخطى غالبًا الحلقات والمنحنيات في الملاحظة الشخصية. تفعيل وضع الخط المكتوب بخط اليد يزيد الدقة بشكل كبير.

## الخطوة 3 – تحميل الصورة التي تريد تحويلها (تحويل صورة مكتوبة بخط اليد)

الصور هي المادة الخام لأي مهمة OCR. تأكد من حفظ صورتك بصيغة غير مضغوطة (PNG يعمل جيدًا) وأن النص قابل للقراءة إلى حد معقول. ثم حمّلها هكذا:

```python
# Step 3: Load the handwritten image you want to convert
handwritten_image = ocr.Image.load(r"YOUR_DIRECTORY/hand_note.png")
```

إذا كانت الصورة موجودة بجوار سكريبتك، يمكنك ببساطة استخدام `"hand_note.png"` بدلاً من المسار الكامل.  

> **ماذا لو كانت الصورة غير واضحة؟** جرّب المعالجة المسبقة باستخدام OpenCV (مثلاً `cv2.cvtColor` إلى تدرج رمادي، `cv2.threshold` لزيادة التباين) قبل تمريرها إلى محرك OCR.

## الخطوة 4 – تشغيل محرك التعرف لاستخراج النص المكتوب بخط اليد

مع جاهزية المحرك وتحميل الصورة في الذاكرة، يمكننا أخيرًا **استخراج النص المكتوب بخط اليد**. طريقة `recognize` تُعيد كائن نتيجة خام يحتوي على النص بالإضافة إلى درجات الثقة.

```python
# Step 4: Perform OCR and get the raw result
raw_result = ocr_engine.recognize(handwritten_image)
print("Raw OCR output:")
print(raw_result.text)
```

قد يتضمن الناتج الخام عادةً فواصل أسطر عشوائية أو أحرف غير صحيحة، خاصةً إذا كان الخط غير مرتب. لهذا السبب توجد الخطوة التالية.

## الخطوة 5 – (اختياري) تحسين النتيجة باستخدام معالج AI ما بعد المعالجة

معظم SDKs الحديثة لـ OCR تأتي مع معالج AI خفيف الوزن ما بعد المعالجة ينظّف التباعد، يصلح الأخطاء الشائعة، ويُوحّد نهايات الأسطر. تشغيله سهل كالتالي:

```python
# Step 5: Refine the raw OCR output (handwritten note to text)
polished_result = ocr_engine.run_postprocessor(raw_result)

# Display the cleaned, readable text
print("\nPolished OCR output:")
print(polished_result.text)
```

إذا تخطيت هذه الخطوة ستحصل على نص قابل للاستخدام، لكن تحويل **الملاحظة المكتوبة بخط اليد إلى نص** سيظهر بصورة أقل صقلًا. المعالج ما بعد المعالجة مفيد خصوصًا للملاحظات التي تحتوي على نقاط تعداد أو كلمات مختلطة الأحرف.

## الخطوة 6 – التحقق من النتيجة ومعالجة الحالات الخاصة

بعد طباعة النتيجة المُنقّحة، تحقق من أن كل شيء يبدو صحيحًا. إليك فحص سريع يمكنك إضافته:

```python
# Step 6: Simple verification
if not polished_result.text.strip():
    raise ValueError("OCR returned an empty string – check image quality.")
else:
    print("\n✅ OCR succeeded! You can now save or further process the text.")
```

**قائمة التحقق من الحالات الخاصة**  

| الحالة | ما الذي يجب فعله |
|-----------|------------|
| **تباين منخفض جدًا** | زيادة التباين باستخدام `cv2.convertScaleAbs` قبل التحميل. |
| **عدة لغات** | ضبط `ocr_engine.language = ["en", "es"]` (أو اللغات المستهدفة). |
| **مستندات كبيرة** | معالجة الصفحات على دفعات لتجنب ارتفاع استهلاك الذاكرة. |
| **رموز خاصة** | إضافة قاموس مخصص عبر `ocr_engine.add_custom_words([...])`. |

## نظرة عامة بصرية

فيما يلي صورة بديلة توضح سير العمل — من ملاحظة مُصوَّرة إلى نص نظيف. يحتوي النص البديل على الكلمة الرئيسية، مما يجعل الصورة صديقة لتحسين محركات البحث.

![كيفية استخدام OCR على صورة ملاحظة مكتوبة بخط اليد](/images/handwritten_ocr_flow.png "كيفية استخدام OCR على صورة ملاحظة مكتوبة بخط اليد")

## سكريبت كامل قابل للتنفيذ

بدمج جميع الأجزاء معًا، إليك البرنامج الكامل جاهز للنسخ واللصق:

```python
# Complete script: Convert a handwritten image to clean text using OCR

import ocr

def main():
    # 1️⃣ Initialize OCR engine for handwritten recognition
    ocr_engine = ocr.OcrEngine()
    ocr_engine.recognition_mode = ocr.RecognitionMode.HANDWRITTEN

    # 2️⃣ Load the image containing the handwritten note
    handwritten_image = ocr.Image.load(r"YOUR_DIRECTORY/hand_note.png")

    # 3️⃣ Perform OCR to extract raw text
    raw_result = ocr_engine.recognize(handwritten_image)
    print("Raw OCR output:")
    print(raw_result.text)

    # 4️⃣ (Optional) Run AI post‑processor for cleaner output
    polished_result = ocr_engine.run_postprocessor(raw_result)

    # 5️⃣ Show the polished, readable text
    print("\nPolished OCR output:")
    print(polished_result.text)

    # 6️⃣ Simple sanity check
    if not polished_result.text.strip():
        raise ValueError("OCR returned an empty string – check image quality.")
    else:
        print("\n✅ OCR succeeded! You can now save or further process the text.")

if __name__ == "__main__":
    main()
```

**الناتج المتوقع (مثال)**  

```
Raw OCR output:
T0d@y I w3nt to the market
and bought 5 aplpes, 2 bananas,
and a loaf of bread.

Polished OCR output:
Today I went to the market and bought 5 apples, 2 bananas, and a loaf of bread.
```

لاحظ كيف قام المعالج ما بعد المعالجة بتصحيح الخطأ “T0d@y” وتوحيد التباعد.

## الأخطاء الشائعة ونصائح احترافية

- **حجم الصورة مهم** – عادةً ما تحدّ محركات OCR حجم الإدخال إلى 4 K × 4 K. قم بتغيير حجم الصور الكبيرة مسبقًا.  
- **نمط الخط** – الخط المتصل مقابل الحروف المنفصلة قد يؤثر على الدقة. إذا كان بإمكانك التحكم في المصدر (مثلاً قلم رقمي)، شجع على كتابة الحروف المنفصلة للحصول على أفضل النتائج.  
- **المعالجة الدفعية** – عند التعامل مع عشرات الملاحظات، غلف السكريبت في حلقة واحفظ كل نتيجة في ملف CSV أو قاعدة بيانات SQLite.  
- **تسرب الذاكرة** – بعض SDKs تحتفظ بذاكر داخلية؛ استدعِ `ocr_engine.dispose()` بعد الانتهاء إذا لاحظت بطءً.

## الخطوات التالية – ما بعد OCR البسيط

الآن بعد أن أتقنت **كيفية استخدام OCR** لصورة واحدة، فكر في هذه التوسعات:

1. **التكامل مع التخزين السحابي** – سحب الصور من AWS S3 أو Azure Blob، تشغيل نفس الخطوات، وإعادة النتائج.  
2. **إضافة كشف اللغة** – استخدم `ocr_engine.detect_language()` لتبديل القواميس تلقائيًا.  
3. **الدمج مع NLP** – مرّر النص المنقّح إلى spaCy أو NLTK لاستخراج الكيانات، التواريخ، أو عناصر العمل.  
4. **إنشاء نقطة نهاية REST** – غلف السكريبت بـ Flask أو FastAPI حتى تتمكن الخدمات الأخرى من إرسال صور عبر POST واستلام نص مشفر بصيغة JSON.

كل هذه الأفكار لا تزال تدور حول المفاهيم الأساسية لـ **التعرف على النص المكتوب بخط اليد**، **استخراج النص المكتوب بخط اليد**، و**تحويل صورة مكتوبة بخط اليد** — العبارات التي من المحتمل أن تبحث عنها لاحقًا.

---

### ملخص

أظهرنا لك **كيفية استخدام OCR** للتعرف على النص المكتوب بخط اليد، استخراجّه، وتنقيته إلى سلسلة قابلة للاستخدام. السكريبت الكامل جاهز للتنفيذ، تم شرح سير العمل خطوة بخطوة، ولديك الآن قائمة تحقق للحالات الخاصة. احصل على صورة لملاحظة اجتماعك القادمة، ضعها في السكريبت، ودع الآلة تقوم بالكتابة بدلاً منك.  

برمجة سعيدة، ولتظل ملاحظاتك دائمًا قابلة للقراءة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}