---
category: general
date: 2026-05-31
description: تحميل الصورة للتعرف الضوئي على الأحرف باستخدام مكتبة Aspose OCR للغة
  Java – دليل خطوة بخطوة مع تصحيح الأخطاء الإملائية، إعدادات اللغة، وأفضل 3 اقتراحات.
draft: false
keywords:
- load image for OCR
- Aspose OCR Java
- spell correction OCR
- OCR engine Java
- set OCR language
- max suggestions OCR
language: ar
og_description: تحميل صورة للتعرف الضوئي على الأحرف في جافا باستخدام Aspose OCR. تعلّم
  كيفية تمكين تصحيح الإملاء، وتعيين اللغة، وتقييد الاقتراحات إلى الثلاثة الأوائل.
og_title: تحميل الصورة للتعرف الضوئي على الأحرف باستخدام Aspose OCR Java – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Load image for OCR using Aspose OCR Java library – step‑by‑step guide
    with spell correction, language settings, and top‑3 suggestions.
  headline: Load Image for OCR with Aspose OCR Java – Complete Guide
  type: TechArticle
tags:
- OCR
- Java
- Aspose
- Image Processing
title: تحميل الصورة للتعرف الضوئي على الأحرف باستخدام Aspose OCR Java – دليل كامل
url: /ar/java/ocr-operations/load-image-for-ocr-with-aspose-ocr-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحميل صورة للتعرف الضوئي على الحروف (OCR) باستخدام Aspose OCR Java – دليل كامل

هل تحتاج إلى **تحميل صورة للتعرف الضوئي على الحروف** في تطبيق Java؟ لست وحدك في هذه المشكلة. لحسن الحظ، تجعل مكتبة Aspose OCR for Java العملية شبه خالية من المتاعب، خاصةً عندما تضيف تصحيح الأخطاء الإملائية إلى العملية.

في هذا الدرس سنستعرض كل سطر تحتاجه لوضع صورة نص مكتوب بخطأ إملائي أمام محرك OCR، تشغيل **تصحيح الأخطاء الإملائية**، تحديد عدد الاقتراحات إلى الثلاثة الأوائل، وأخيرًا طباعة النتيجة المصححة. في النهاية ستحصل على برنامج قابل للتنفيذ يمكنك إدراجه في أي مشروع.

## ما ستتعلمه

- كيفية تطبيق رخصة **Aspose OCR Java** حتى يعمل المكتبة بدون علامة مائية.  
- الطريقة الدقيقة **لتحميل صورة للتعرف الضوئي على الحروف** باستخدام `OcrImage`.  
- ضبط لغة OCR (نعم، يمكنك التبديل من الإنجليزية إلى الفرنسية في لحظة.).  
- تفعيل **تصحيح الأخطاء الإملائية في OCR** وتحديد حد `max suggestions`.  
- تشغيل المحرك واسترجاع النص النظيف المصحح.  

لا تحتاج إلى أي خبرة سابقة مع Aspose، فقط بيئة تطوير متوافقة مع Java وصورة صغيرة. لنبدأ.

![Diagram showing the flow of loading an image for OCR, applying spell correction, and retrieving text](load-image-ocr.png "load image for OCR diagram")

## الخطوة 1 – تحميل صورة للتعرف الضوئي على الحروف

أول شيء عليك فعله هو توجيه المحرك إلى الصورة التي تحتوي على النص الذي تريد قراءته. في Aspose هذا سطر واحد:

```java
// Step 1: Load the image that contains misspelled text
engine.setImage(new OcrImage("YOUR_DIRECTORY/misspelled.png"));
```

`OcrImage` تقبل مسار ملف، أو تدفق، أو حتى `BufferedImage`. إذا كانت الصورة موجودة في classpath يمكنك استخدام `getResourceAsStream` بدلاً من ذلك—مفيد لاختبارات الوحدة.  

> **نصيحة احترافية:** احرص على أن لا يتجاوز حجم ملفات الصور 2 ميغابايت؛ الملفات الأكبر تستهلك الذاكرة بشكل كبير وقد تبطئ محرك OCR.

## الخطوة 2 – تهيئة رخصة Aspose OCR

قبل أن يقوم المحرك بأي شيء مفيد تحتاج إلى رخصة صالحة؛ وإلا ستحصل على مخرجات بعلامة مائية وتحذير في وحدة التحكم.

```java
// Step 2: Apply your Aspose OCR license
License license = new License();
license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");
```

إذا لم تحصل على رخصة بعد، يمكنك طلب رخصة مؤقتة مجانية من بوابة Aspose. فقط ضع ملف `.lic` في مكان يمكن لتطبيقك قراءته، وستكون جاهزًا.

## الخطوة 3 – ضبط محرك OCR واللغة

محرك OCR بدون تحديد لغة يشبه GPS بدون خريطة—ضائع. للإنجليزية نستخدم:

```java
// Step 3: Create an OCR engine and set the language to English
OcrEngine engine = new OcrEngine();
engine.setLanguage(OcrLanguage.ENGLISH);
```

تبديل اللغات سهل مثل استبدال `OcrLanguage.ENGLISH` بـ `OcrLanguage.FRENCH` أو `OcrLanguage.SPANISH` وغيرها. المكتبة تتضمن عشرات حزم اللغة المدمجة.

## الخطوة 4 – تفعيل تصحيح الأخطاء الإملائية وتحديد الحد الأقصى للاقتراحات

الآن يأتي السحر الذي يميز مثالنا عن تشغيل OCR عادي: **تصحيح الأخطاء الإملائية في OCR**. بشكل افتراضي يكون مغلقًا، لكن تشغيله وتحديد الحد إلى ثلاثة اقتراحات يمنحك مخرجات مرتبة وقابلة للقراءة.

```java
// Step 4: Enable spell correction and limit suggestions to the top 3
engine.getSpellCorrector().setEnabled(true);
engine.getSpellCorrector().setMaxSuggestions(3);
```

معامل `max suggestions` يتحكم في عدد الكلمات البديلة التي سيقترحها المحرك لكل كلمة مكتوبة بخطأ. إبقاؤه منخفضًا يقلل الضوضاء، خاصةً عندما تكون الصورة المصدر غير واضحة.

## الخطوة 5 – تشغيل OCR واسترجاع النص المصحح

مع إعداد كل شيء، عملية التعرف الفعلية هي مجرد استدعاء طريقة واحدة. المحرك يعيد `String` يحتوي بالفعل على النص المصحح.

```java
// Step 5: Perform OCR and obtain the corrected text
String correctedText = engine.recognize();
```

خلف الكواليس، Aspose يستخدم مصنفًا يعتمد على الشبكات العصبية، ثم يمرّر النتائج الأولية عبر مصحح الأخطاء الإملائية. كامل الخط الأنابيب يكتمل في بضع مليثانية لصورة بحجم 300 × 200 بكسل تقريبًا.

## الخطوة 6 – طباعة النتيجة المصححة

أخيرًا، فقط اطبع السلسلة—أو أرسلها إلى مكان آخر مثل قاعدة بيانات أو استجابة REST.

```java
// Step 6: Output the corrected result
System.out.println(correctedText);
```

### النتيجة المتوقعة

إذا كانت `misspelled.png` تحتوي على العبارة “Ths is a smple test”، سيظهر في وحدة التحكم:

```
This is a simple test
```

لاحظ كيف تم تصحيح الكلمات المكتوبة بخطأ “Ths” و “smple” تلقائيًا، وتم أخذ أفضل ثلاثة اقتراحات فقط في الاعتبار.

## المشكلات الشائعة والنصائح

| المشكلة | السبب | طريقة الحل |
|------|----------------|------------|
| **إخراج فارغ** | الرخصة غير محمَّلة أو مسار الصورة غير صحيح. | تحقق من مسار ملف `.lic` وتأكد من وجود `misspelled.png`. |
| **حروف غير مفهومة** | DPI الصورة منخفض جدًا (أقل من 70). | استخدم مصدر بدقة أعلى أو قم بزيادة الدقة باستخدام `ImageMagick`. |
| **عدد اقتراحات كبير** | `setMaxSuggestions` ترك على القيمة الافتراضية (0 = غير محدود). | استدعِ `setMaxSuggestions(3)` صراحةً كما هو موضح. |
| **لغة خاطئة** | `setLanguage` لم يُستدعَ أو تم تمرير قيمة enum غير صحيحة. | تأكد من أن قيمة enum `OcrLanguage` تتطابق مع لغتك. |

### نصيحة احترافية: المعالجة الدفعية

إذا كنت بحاجة إلى OCR لعدة ملفات، ضع الخطوات من 1 إلى 5 داخل حلقة وأعد استخدام نفس كائن `OcrEngine`. إعادة استخدام المحرك توفر الذاكرة لأن الشبكة العصبية الداخلية تُحمَّل مرة واحدة فقط.

```java
OcrEngine engine = new OcrEngine();
engine.setLanguage(OcrLanguage.ENGLISH);
engine.getSpellCorrector().setEnabled(true);
engine.getSpellCorrector().setMaxSuggestions(3);

for (String path : imagePaths) {
    engine.setImage(new OcrImage(path));
    System.out.println(engine.recognize());
}
```

## ملخص

غطينا كل ما تحتاجه **لتحميل صورة للتعرف الضوئي على الحروف** باستخدام Aspose OCR Java، من الرخصة واختيار اللغة إلى تشغيل **تصحيح الأخطاء الإملائية** وتحديد الحد إلى أفضل ثلاث اقتراحات. البرنامج الكامل القابل للتنفيذ لا يتجاوز بضع أسطر، لكنه يحمل قدرًا كبيرًا من القوة.

ما الخطوة التالية؟ جرّب استبدال `OcrLanguage.ENGLISH` بلغة أخرى، جرب صيغ صور مختلفة (`.tif`, `.bmp`)، أو اربط النتيجة بمولد PDF. الإمكانيات لا حصر لها، والنمط نفسه—رخصة → محرك → صورة → إعدادات → التعرف—ينطبق على كل سيناريو.

برمجة سعيدة، ولتكن نتائج OCR دائمًا واضحة كالكريستال!

## ما الذي يجب أن تتعلمه بعد ذلك؟

- [كيفية استخراج نص من صورة باستخدام Aspose.OCR مع اختيار اللغة](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [استخراج النص من صورة Java باستخدام وضع اكتشاف المناطق في Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [تحويل الصورة إلى نص في Java باستخدام Aspose.OCR و BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}