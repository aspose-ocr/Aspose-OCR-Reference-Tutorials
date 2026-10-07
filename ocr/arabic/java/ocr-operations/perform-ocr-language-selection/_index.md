---
date: 2026-02-12
description: تعلم كيفية تحويل نص الصورة إلى نص باستخدام OCR مع اختيار اللغة باستخدام
  Aspose.OCR للغة Java. يغطي هذا الدليل خطوة بخطوة استخراج النص في Java، وتصحيح انحراف
  OCR، وأكثر من ذلك.
linktitle: How to OCR Image Text with Language Using Aspose.OCR
second_title: Aspose.OCR Java API
title: كيفية التعرف الضوئي على نص الصورة باستخدام اللغة مع Aspose.OCR
url: /ar/java/ocr-operations/perform-ocr-language-selection/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخراج نص الصورة باستخدام لغة مع Aspose.OCR

## المقدمة

استخراج النص من ملفات الصور هو طلب شائع سواءً كنت تقوم برقمنة المستندات الممسوحة ضوئياً، أو معالجة الإيصالات، أو بناء أرشيفات قابلة للبحث. في هذا الدرس سنستعرض مثالًا كاملاً وتطبيقيًا يوضح **كيفية استخراج نص الصورة** باستخدام إعداد لغة محدد، حتى تتمكن من دمج OCR موثوق به في تطبيقات Java الخاصة بك اليوم. ستتعرف أيضًا على كيفية معالجة تصحيح الميل في OCR والتعرف القائم على المناطق للحصول على أقصى دقة.

## إجابات سريعة
- **ما المكتبة التي تتعامل مع OCR في Java؟** Aspose.OCR for Java  
- **أي إعداد يختار اللغة؟** `settings.setLanguage(Language.Eng)` (أو أي لغة مدعومة)  
- **هل أحتاج إلى ترخيص للتطوير؟** ترخيص تجريبي مجاني يعمل للاختبار؛ الترخيص التجاري مطلوب للإنتاج.  
- **هل يمكنني تحديد OCR لمنطقة معينة من الصورة؟** نعم، استخدم `RecognitionSettings.setRecognitionAreas()` مع المستطيلات.  
- **ما هو زمن التنفيذ النموذجي؟** بضع ثوانٍ لكل صفحة على حاسوب محمول عادي، حسب حجم الصورة وتعقيد اللغة.

## كيفية استخراج نص الصورة مع اختيار اللغة
في هذا القسم نجيب على السؤال الأساسي **كيف يتم OCR** لصورة عندما تعرف لغة النص. اختيار اللغة الصحيحة يحسن دقة التعرف بشكل كبير لأن محرك OCR يمكنه تطبيق القواميس ونماذج الحروف الخاصة بتلك اللغة.

### لماذا هذا مهم
- **دقة أعلى** – نماذج اللغة المحددة تقلل الأخطاء في التعرف.  
- **تحسين الأداء** – يتخطى المحرك فحوصات اللغات غير الضرورية.  
- **معالجة أفضل للعلامات** – يتم التعرف على الفرنسية، الإسبانية، الألمانية، إلخ، بشكل صحيح عند استخدام تعداد `Language` المناسب.

## ما هو “استخراج النص من الصورة”؟
استخراج النص من الصورة (OCR) يحول التمثيل البصري للأحرف إلى سلاسل قابلة للقراءة آليًا. هذا يتيح البحث، التحليل، وسير عمل استخراج البيانات التي كانت تتطلب في السابق نسخًا يدويًا.

## لماذا تستخدم Aspose.OCR مع اختيار اللغة؟
- **دعم متعدد اللغات** – اختر اللغة (اللغات) الموجودة في صورتك لزيادة الدقة.  
- **تحكم دقيق** – اضبط الميل، حدد مناطق التعرف، واضبط سلوك الميل التلقائي.  
- **واجهة برمجة تطبيقات Java صافية** – لا توجد تبعيات أصلية، سهل الدمج في أي مشروع Java.  
- **بيانات نتيجة غنية** – احصل على النص العادي، JSON، المستطيلات المحيطة، والتحذيرات في استدعاء واحد.

## المتطلبات المسبقة

قبل البدء، تأكد من وجود ما يلي:

- **مجموعة تطوير جافا (JDK)** مثبتة (JDK 8 أو أحدث).  
- **مكتبة Aspose.OCR for Java** – حمّلها من الموقع الرسمي [هنا](https://reference.aspose.com/ocr/java/).  
- ملف صورة يحتوي على النص الذي تريد استخراجه، مثال: `p3.png`.

## استيراد الحزم

في ملف مصدر Java الخاص بك، أدرج الفئات المطلوبة من Aspose.OCR وأدوات Java القياسية:

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

استبدل `"Your Document Directory"` بالمسار المطلق حيث يوجد ملف `p3.png`.

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

1. تعطيل الميل التلقائي لأننا نوفر قيمة ميل يدوية.  
2. تعريف منطقة مستطيلة (`RecognitionAreas`) لتحديد OCR على الجزء من الصورة الذي يحتوي فعليًا على النص.  
3. ضبط **اللغة** إلى الإنجليزية (`Language.Eng`). غيّرها إلى `Language.Fra` أو `Language.Spa` إلخ، حسب صورة المصدر.

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

استدعاء `RecognizePage` يشغل محرك OCR باستخدام الصورة والإعدادات التي حددتها. النتيجة تُخزن في كائن `RecognitionResult`.

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

مخرجات وحدة التحكم تُظهر:

- النص المستخرج بالكامل (`recognitionText`).  
- النص لكل مستطيل معرف (`recognitionAreasText`).  
- إحداثيات المستطيل المحيط.  
- تمثيل JSON لتسهيل المعالجة اللاحقة.  
- زاوية الميل المكتشفة وأي تحذيرات.

يمكنك الآن تمرير `result.recognitionText` إلى منطق عملك—احفظه، فهرسه، أو أرسله إلى خدمة أخرى.

## المشكلات الشائعة والحلول

| المشكلة | السبب | الحل |
|-------|-------|-----|
| **حروف غير مفهومة** | اختيار لغة خاطئة | اضبط تعداد `Language` الصحيح (مثال: `Language.Fra` للفرنسية). |
| **عدم إرجاع نص** | منطقة التعرف لا تغطي النص | عدّل إحداثيات `Rectangle` أو أزل `RecognitionAreas` لمعالجة الصورة بالكامل. |
| **أداء بطيء** | صورة كبيرة جدًا أو بدقة عالية | قلل حجم الصورة قبل OCR أو زد تخصيص الذاكرة لـ JVM. |
| **تحذيرات حول تنسيق غير مدعوم** | تنسيق الصورة غير معترف به | حوّل الصورة إلى PNG أو JPEG أو TIFF قبل المعالجة. |

## الأسئلة الشائعة

**س: هل يمكنني التعرف على عدة لغات في استدعاء OCR واحد؟**  
ج: نعم. استخدم `settings.setLanguage(Language.Eng | Language.Fra)` لتمكين التعرف متعدد اللغات.

**س: ما هي صيغ الصور التي يدعمها Aspose.OCR؟**  
ج: PNG، JPEG، BMP، TIFF، GIF، والعديد غيرها. فقط قدّم مسار الملف الصحيح.

**س: هل هناك حد لحجم الصورة؟**  
ج: لا يوجد حد ثابت، لكن الصور الكبيرة جدًا تستهلك ذاكرة أكبر وتزيد من زمن المعالجة. يُفضَّل تصغير الملفات الكبيرة.

**س: كيف أحصل على ترخيص للإنتاج؟**  
ج: اشترِ ترخيصًا من موقع Aspose وطبقه عبر فئة `License` كما هو موضح في وثائق Aspose.

**س: هل يمكن استخراج النص من صفحة PDF مباشرة؟**  
ج: ليس مباشرة باستخدام Aspose.OCR. حوّل صفحة PDF إلى صورة أولاً (مثلاً باستخدام Aspose.PDF) ثم نفّذ OCR.

## الخاتمة

لقد رأيت الآن **كيفية استخراج نص من الصورة** باستخدام Aspose.OCR for Java مع اختيار اللغة المناسبة وتحديد مناطق التعرف. يوفّر هذا النهج OCR دقيقًا وعالي الأداء يمكن دمجه في أي سير عمل مبني على Java—من أنظمة إدارة المستندات إلى خطوط التقاط البيانات. هل أنت مستعد للخطوة التالية؟ جرّب تغيير تعداد اللغة، واختبر مناطق التعرف المختلفة، ودمج النتائج في منطق تطبيقك الخاص.

---

**آخر تحديث:** 2026-02-12  
**تم الاختبار مع:** Aspose.OCR 24.11 for Java  
**المؤلف:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}