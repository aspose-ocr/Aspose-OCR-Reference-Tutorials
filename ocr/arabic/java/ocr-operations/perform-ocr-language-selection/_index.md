---
title: تنفيذ التعرف الضوئي على الحروف (OCR) مع تحديد اللغة في Aspose.OCR
linktitle: تنفيذ التعرف الضوئي على الحروف (OCR) مع تحديد اللغة في Aspose.OCR
second_title: Aspose.OCR جافا API
description: أطلق العنان لاستخراج النص الدقيق من الصور باستخدام Aspose.OCR لـ Java. اتبع دليلنا خطوة بخطوة للتعرف الضوئي على الحروف بدقة مع اختيار اللغة.
type: docs
weight: 11
url: /ar/java/ocr-operations/perform-ocr-language-selection/
---
## مقدمة

في عالم التكنولوجيا دائم التطور، يلعب التعرف الضوئي على الحروف (OCR) دورًا محوريًا في استخراج معلومات ذات معنى من الصور. يبرز Aspose.OCR for Java كأداة قوية تمكن المطورين من دمج إمكانات التعرف الضوئي على الحروف (OCR) بسلاسة في تطبيقات Java الخاصة بهم. في هذا الدليل التفصيلي، سنستكشف كيفية إجراء التعرف الضوئي على الحروف (OCR) مع تحديد اللغة باستخدام Aspose.OCR، مما يفتح إمكانية معالجة المحتوى المتنوع بدقة.

## المتطلبات الأساسية

قبل الغوص في البرنامج التعليمي، تأكد من توفر المتطلبات الأساسية التالية:

- بيئة تطوير Java: تأكد من تثبيت Java على نظامك، وإعداد بيئة التطوير لديك.

-  مكتبة Aspose.OCR: قم بتنزيل وتثبيت مكتبة Aspose.OCR لـ Java. يمكنك العثور على المكتبة والوثائق ذات الصلة[هنا](https://reference.aspose.com/ocr/java/).

- ملف الصورة: قم بإعداد ملف صورة يحتوي على النص الذي تريد استخراجه. على سبيل المثال، لنستخدم ملفًا يسمى "p3.png."

## حزم الاستيراد

في مشروع Java الخاص بك، قم باستيراد الحزم اللازمة للاستفادة من وظيفة Aspose.OCR. أضف الأسطر التالية في بداية ملف Java الخاص بك:

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

## الخطوة 1: قم بإعداد دليل المستندات الخاص بك

```java
// المسار إلى دليل المستندات.
String dataDir = "Your Document Directory";
```

استبدل "دليل المستندات الخاص بك" بالمسار الفعلي للدليل الذي يوجد به ملف الصورة الخاص بك.

## الخطوة 2: تحديد مسار الصورة

```java
// مسار الصورة
String file = dataDir + "p3.png";
```

اضبط متغير الملف للإشارة إلى ملف الصورة المحدد الخاص بك.

## الخطوة 3: إنشاء مثيل Aspose.OCR API

```java
// إنشاء مثيل API
AsposeOCR api = new AsposeOCR();
```

قم بتهيئة كائن AsposeOCR للوصول إلى ميزاته.

## الخطوة 4: ضبط خيارات التعرف

```java
// ضبط خيارات التعرف
RecognitionSettings settings = new RecognitionSettings();
settings.setAutoSkew(false);
ArrayList<Rectangle> rectangles = new ArrayList<Rectangle>();
rectangles.add(new Rectangle(90, 186, 775, 95));
settings.setRecognitionAreas(rectangles);
settings.setSkew(0.5);
settings.setLanguage(Language.Eng);
```

قم بتخصيص إعدادات التعرف بناءً على متطلباتك. اضبط المعلمات مثل مناطق الانحراف واللغة والتعرف.

## الخطوة 5: إجراء التعرف الضوئي على الحروف واسترجاع النتائج

```java
// الحصول على كائن النتيجة
RecognitionResult result = null;
try {
    result = api.RecognizePage(file, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

قم بتنفيذ عملية التعرف الضوئي على الحروف (OCR) باستخدام ملف الصورة والإعدادات المحددة. التقط النتيجة في كائن RecognitionResult.

## الخطوة 6: طباعة النتائج واستخدامها

```java
// طباعة النتيجة
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

اطبع النص المستخرج ومناطق التعرف وتمثيل JSON وزاوية الانحراف وأي تحذيرات. استخدم النتائج حسب الحاجة في طلبك.

## خاتمة

في هذا البرنامج التعليمي، بحثنا في التكامل السلس لـ Aspose.OCR لـ Java لإجراء التعرف الضوئي على الحروف مع اختيار اللغة. تفتح هذه المكتبة القوية عالمًا من الإمكانيات للمطورين الذين يهدفون إلى استخراج النص من الصور بدقة.

## الأسئلة الشائعة

### س١: هل يمكنني استخدام Aspose.OCR للغات متعددة في عملية التعرف الواحدة؟

ج1: نعم، يمكنك تعيين لغات متعددة في إعدادات التعرف لتحسين دقة التعرف على المحتوى متعدد اللغات.

### س2: كيف يمكنني التعامل مع تنسيقات الصور المختلفة باستخدام Aspose.OCR؟

ج2: يدعم Aspose.OCR تنسيقات الصور المختلفة، بما في ذلك PNG وJPEG وTIFF. ما عليك سوى توفير مسار الملف الصحيح في متغير مسار الصورة.

### س3: هل هناك حد لحجم الصورة التي يمكن لـ Aspose.OCR معالجتها؟

ج3: يمكن لـ Aspose.OCR التعامل مع الصور ذات الأحجام المختلفة، ولكن الصور الأكبر حجمًا قد تتطلب المزيد من وقت المعالجة والموارد.

### س4: هل يمكنني ضبط إعدادات التعرف على مناطق معينة داخل الصورة؟

ج4: بالتأكيد. استخدم ميزة RecognitionAreas لتحديد مستطيلات محددة داخل الصورة للتعرف المستهدف.

### س5: هل Aspose.OCR مناسب لكل من المشاريع الشخصية والتجارية؟

ج5: نعم، يوفر Aspose.OCR خيارات ترخيص مرنة، مما يجعله مناسبًا للاستخدام الشخصي والتجاري.