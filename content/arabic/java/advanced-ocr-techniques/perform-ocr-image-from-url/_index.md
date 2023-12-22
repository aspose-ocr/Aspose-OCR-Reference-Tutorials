---
title: تنفيذ التعرف الضوئي على الحروف (OCR) على الصورة من عنوان URL في Aspose.OCR لـ Java
linktitle: تنفيذ التعرف الضوئي على الحروف (OCR) على الصورة من عنوان URL في Aspose.OCR لـ Java
second_title: Aspose.OCR جافا API
description: أطلق العنان لاستخراج نص الصورة بشكل سلس في Java باستخدام Aspose.OCR. دقة عالية في التعرف الضوئي على الحروف (OCR) مع سهولة التكامل.
type: docs
weight: 11
url: /ar/java/advanced-ocr-techniques/perform-ocr-image-from-url/
---
## مقدمة

مرحبًا بك في دليلنا خطوة بخطوة حول كيفية إجراء التعرف البصري على الأحرف (OCR) على صورة من عنوان URL باستخدام Aspose.OCR لـ Java. تم تصميم هذا البرنامج التعليمي لمساعدتك على دمج Aspose.OCR بسلاسة في تطبيقات Java الخاصة بك، مما يسمح لك باستخراج النص من الصور بسهولة. Aspose.OCR هي مكتبة OCR قوية تدعم تنسيقات الصور المختلفة، مما يجعلها أداة قيمة للتطبيقات التي تتطلب استخراج النص.

## المتطلبات الأساسية

قبل الغوص في البرنامج التعليمي، تأكد من أن لديك المتطلبات الأساسية التالية:

1. بيئة تطوير Java: تأكد من إعداد بيئة تطوير Java عاملة على جهازك.

2.  مكتبة Aspose.OCR: قم بتنزيل وتثبيت Aspose.OCR لمكتبة Java. يمكنك العثور على المكتبة والوثائق ذات الصلة على[موقع Aspose.OCR](https://reference.aspose.com/ocr/java/).

## حزم الاستيراد

في مشروع Java الخاص بك، قم باستيراد الحزم اللازمة لـ Aspose.OCR:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.License;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.RecognitionSettings;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## الخطوة 1: إنشاء مثيل API

تهيئة مثيل لفئة AsposeOCR:

```java
AsposeOCR api = new AsposeOCR();
```

## الخطوة 2: تحديد عنوان URL للصورة

حدد عنوان URL للصورة التي تريد إجراء التعرف الضوئي على الحروف منها:

```java
String uri = "https://www.example.com/your-image.png";
```

## الخطوة 3: ضبط خيارات التعرف

تكوين إعدادات التعرف، مثل تعطيل الانحراف التلقائي وتحديد مناطق التعرف:

```java
RecognitionSettings settings = new RecognitionSettings();
settings.setAutoSkew(false);

// تحديد مناطق التعرف باستخدام المستطيلات
ArrayList<Rectangle> rectangles = new ArrayList<Rectangle>();
rectangles.add(new Rectangle(90, 186, 775, 95));
settings.setRecognitionAreas(rectangles);
```

## الخطوة 4: تنفيذ التعرف الضوئي على الحروف

استدعاء عملية التعرف الضوئي على الحروف:

```java
RecognitionResult result = null;
try {
    result = api.RecognizePageFromUri(uri, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

## الخطوة 5: طباعة النتائج

عرض نتائج التعرف، بما في ذلك النص المستخرج ونص مناطق التعرف ومخرجات JSON وأي تحذيرات:

```java
System.out.println("Result: \n" + result.recognitionText + "\n\n");
System.out.println("RecognitionAreasText: \n");
for (String text : result.recognitionAreasText) {
    System.out.println(text);
}
System.out.println("JSON: \n" + result.GetJson());
System.out.println("Warnings: \n");
for (String warning : result.warnings) {
    System.out.println(warning);
}
```

كرر هذه الخطوات لدمج Aspose.OCR في تطبيق Java الخاص بك واستخراج النص من الصور بدقة.

## خاتمة

وفي الختام، فإن الاستفادة من Aspose.OCR لـ Java توفر حلاً قويًا لمهام التعرف الضوئي على الحروف، مما يمكّن المطورين من استخراج النص من الصور بسلاسة. ويضمن الدليل التفصيلي عملية تكامل سلسة، مما يجعله في متناول المطورين من جميع المستويات.

## الأسئلة الشائعة

### س1: ما مدى دقة Aspose.OCR في التعرف على النص من الصور؟

A1: يوفر Aspose.OCR دقة عالية في التعرف على النص، خاصة عند تكوينه بمناطق التعرف الدقيقة.

### س2: هل يستطيع Aspose.OCR التعامل مع لغات متعددة أثناء التعرف على OCR؟

ج2: نعم، يدعم Aspose.OCR التعرف على النص بلغات متعددة، مما يوفر تنوعًا في التطبيقات المتنوعة.

### س3: هل هناك أي اعتبارات ترخيصية لاستخدام Aspose.OCR في المشاريع التجارية؟

ج3: نعم، تأكد من الامتثال لشروط ترخيص Aspose.OCR للاستخدام التجاري. تشير إلى[buy.aspose.com](https://purchase.aspose.com/buy) للحصول على تفاصيل الترخيص.

### س٤: كيف يمكنني الحصول على الدعم للمشكلات المتعلقة بـ Aspose.OCR؟

 ج4: قم بزيارة[منتدى Aspose.OCR](https://forum.aspose.com/c/ocr/16) لدعم المجتمع والمناقشات. للحصول على دعم متميز، فكر في الحصول على ترخيص مؤقت من[ترخيص مؤقت](https://purchase.aspose.com/temporary-license/).

### س5: هل هناك نسخة تجريبية مجانية متاحة لـ Aspose.OCR لـ Java؟

 ج5: نعم، استكشف ميزات Aspose.OCR من خلال النسخة التجريبية المجانية المتوفرة على[Releases.aspose.com](https://releases.aspose.com/).
