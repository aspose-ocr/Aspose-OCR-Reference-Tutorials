---
date: 2025-12-13
description: تعلم كيفية استخراج النص من الصورة باستخدام Aspose.OCR للـ Java مع اختيار
  اللغة. يوضح هذا الدليل خطوة بخطوة لـ Aspose OCR للـ Java تكوين OCR الدقيق.
linktitle: How to Extract Text from Image with Language Selection Using Aspose.OCR
second_title: Aspose.OCR Java API
title: كيفية استخراج النص من الصورة مع اختيار اللغة باستخدام Aspose.OCR
url: /ar/java/ocr-operations/perform-ocr-language-selection/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخراج النص من صورة مع اختيار اللغة باستخدام Aspose.OCR

## مقدمة

استخراج النص من ملفات الصور هو مطلب شائع سواء كنت تقوم برقمنة المستندات الممسوحة ضوئياً، أو معالجة الإيصالات، أو بناء أرشيفات قابلة للبحث. تجعل Aspose.OCR for Java هذه المهمة بسيطة وتمنحك تحكمًا دقيقًا في اختيار اللغة، وتصحيح الميل، ومناطق التعرف. في هذا الدرس سنستعرض مثالًا عمليًا كاملًا يوضح **كيفية استخراج النص من صورة** باستخدام إعداد لغة محدد، حتى تتمكن من دمج OCR موثوق به في تطبيقات Java الخاصة بك اليوم.

## إجابات سريعة
- **ما المكتبة التي تتعامل مع OCR في Java؟** Aspose.OCR for Java  
- **أي إعداد يحدد اللغة؟** `settings.setLanguage(Language.Eng)` (أو أي لغة مدعومة)  
- **هل أحتاج إلى ترخيص للتطوير؟** ترخيص تقييم مجاني يعمل للاختبار؛ الترخيص التجاري مطلوب للإنتاج.  
- **هل يمكنني تحديد OCR إلى منطقة معينة من الصورة؟** نعم، استخدم `RecognitionSettings.setRecognitionAreas()` مع المستطيلات.  
- **ما هو زمن التشغيل النموذجي؟** بضع ثوانٍ لكل صفحة على حاسوب محمول عادي، حسب حجم الصورة وتعقيد اللغة.  

## ما هو “استخراج النص من صورة”؟
استخراج النص من صورة (OCR) يحول التمثيل البصري للأحرف إلى سلاسل قابلة للقراءة آليًا. يتيح ذلك البحث والتحليلات وتدفقات استخراج البيانات التي كانت ستتطلب في غير ذلك كتابة يدوية.

## لماذا استخدام Aspose.OCR مع اختيار اللغة؟
- **دعم متعدد اللغات** – اختر اللغة (اللغات) الدقيقة الموجودة في صورتك لزيادة الدقة.  
- **تحكم دقيق** – ضبط الميل، تعريف مناطق التعرف، وتعيين سلوك auto‑skew.  
- **واجهة برمجة تطبيقات Java صافية** – لا تبعيات أصلية، سهل الدمج في أي مشروع Java.  
- **بيانات نتيجة غنية** – احصل على النص العادي، JSON، المستطيلات المحيطة، والتحذيرات في استدعاء واحد.  

## المتطلبات المسبقة

قبل البدء، تأكد من أن لديك:

- **مجموعة تطوير جافا (JDK)** مثبتة (JDK 8 أو أحدث).  
- **مكتبة Aspose.OCR for Java** – حمّلها من الموقع الرسمي [here](https://reference.aspose.com/ocr/java/).  
- ملف صورة يحتوي على النص الذي تريد استخراجه، مثل `p3.png`.

## استيراد الحزم

في ملف Java المصدر الخاص بك، قم بتضمين فئات Aspose.OCR المطلوبة وأدوات Java القياسية:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.Language;
import com.aspose.ocr.License;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.RecognitionSettings;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## دليل خطوة بخطوة

### الخطوة 1: إعداد دليل المستند الخاص بك

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";
```

استبدل `"Your Document Directory"` بالمسار المطلق حيث يقع `p3.png`.

### الخطوة 2: تعريف مسار الصورة

```java
// The image path
String file = dataDir + "p3.png";
```

تأكد من أن المتغير `file` يشير إلى الصورة الدقيقة التي تريد معالجتها.

### الخطوة 3: إنشاء مثيل Aspose.OCR API

```java
// Create API instance
AsposeOCR api = new AsposeOCR();
```

كائن `AsposeOCR` يمنحك الوصول إلى جميع عمليات OCR.

### الخطوة 4: ضبط خيارات التعرف (اختيار اللغة)

```java
// Set recognition options
RecognitionSettings settings = new RecognitionSettings();
settings.setAutoSkew(false);
ArrayList<Rectangle> rectangles = new ArrayList<Rectangle>();
rectangles.add(new Rectangle(90, 186, 775, 95));
settings.setRecognitionAreas(rectangles);
settings.setSkew(0.5);
settings.setLanguage(Language.Eng);
```

هنا نقوم بـ:

1. تعطيل auto‑skew لأننا نوفر قيمة ميل يدوية.  
2. تعريف منطقة مستطيلة (`RecognitionAreas`) لتحديد OCR إلى الجزء من الصورة الذي يحتوي فعليًا على النص.  
3. ضبط **اللغة** إلى الإنجليزية (`Language.Eng`). غيّرها إلى `Language.Fra`، `Language.Spa`، إلخ، حسب صورة المصدر.

### الخطوة 5: تنفيذ OCR واسترجاع النتائج

```java
// Get result object
RecognitionResult result = null;
try {
    result = api.RecognizePage(file, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

استدعاء `RecognizePage` يشغّل محرك OCR باستخدام الصورة والإعدادات التي حددتها. النتيجة تُخزن في كائن `RecognitionResult`.

### الخطوة 6: طباعة واستخدام النتائج

```java
// Print result
System.out.println("Result: \n" + result.recognitionText + "\n\n");
for (String n : result.recognitionAreasText) {
    System.out.println(n);
}
for (Rectangle n : result.recognitionAreasRectangles) {
    System.out.println(n.height + ":" + n.width + ":" + n.x + ":" + n.y);
}
System.out.println("\nJSON:" + result.GetJson());
System.out.println("Angle:" + result.skew);
for (String n : result.warnings) {
    System.out.println(n);
}

System.out.println("OCROperationWithLanguageSelection: execution complete");
```

يعرض إخراج وحدة التحكم:

- النص المستخرج بالكامل (`recognitionText`).  
- النص لكل مستطيل معرف (`recognitionAreasText`).  
- إحداثيات المستطيل المحيط.  
- تمثيل JSON لتسهيل المعالجة اللاحقة.  
- زاوية الميل المكتشفة وأي تحذيرات.

يمكنك الآن تمرير `result.recognitionText` إلى منطق عملك—تخزينه، فهرسته، أو إرساله إلى خدمة أخرى.

## المشكلات الشائعة والحلول

| المشكلة | السبب | الحل |
|-------|-------|-----|
| **حروف غير مفهومة** | اختيار لغة خاطئة | اضبط تعداد `Language` الصحيح (مثال: `Language.Fra` للفرنسية). |
| **عدم إرجاع نص** | منطقة التعرف لا تغطي النص | عدّل إحداثيات `Rectangle` أو أزل `RecognitionAreas` لمعالجة الصورة بالكامل. |
| **أداء بطيء** | صورة كبيرة جدًا أو دقة عالية | قلل حجم الصورة قبل OCR أو زد تخصيص الذاكرة لـ JVM. |
| **تحذيرات حول تنسيق غير مدعوم** | تنسيق الصورة غير معروف | حوّل الصورة إلى PNG أو JPEG أو TIFF قبل المعالجة. |

## الأسئلة المتكررة

**س: هل يمكنني التعرف على عدة لغات في استدعاء OCR واحد؟**  
ج: نعم. استخدم `settings.setLanguage(Language.Eng | Language.Fra)` لتمكين التعرف متعدد اللغات.

**س: ما هي صيغ الصور التي يدعمها Aspose.OCR؟**  
ج: PNG، JPEG، BMP، TIFF، GIF، والعديد غيرها. فقط قدم مسار الملف الصحيح.

**س: هل هناك حد لحجم الصورة؟**  
ج: لا يوجد حد صريح، لكن الصور الكبيرة جدًا تزيد من استهلاك الذاكرة ووقت المعالجة. يُفضَّل تصغير حجم الملفات الكبيرة.

**س: كيف أحصل على ترخيص للإنتاج؟**  
ج: اشترِ ترخيصًا من موقع Aspose وطبقه عبر فئة `License` كما هو موضح في وثائق Aspose.

**س: هل يمكن استخراج النص من صفحة PDF مباشرة؟**  
ج: ليس مباشرة باستخدام Aspose.OCR. حوّل صفحة PDF إلى صورة أولاً (مثلاً باستخدام Aspose.PDF) ثم نفّذ OCR.

## الخاتمة

لقد رأيت الآن كيفية **استخراج النص من صورة** باستخدام Aspose.OCR for Java مع اختيار اللغة المناسبة وتحديد التعرف إلى مناطق محددة. يقدّم هذا النهج OCR دقيقًا وعالي الأداء يمكن دمجه في أي سير عمل مبني على Java—من أنظمة إدارة المستندات إلى خطوط أنابيب جمع البيانات.

---

**Last Updated:** 2025-12-13  
**Tested With:** Aspose.OCR 24.11 for Java  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}