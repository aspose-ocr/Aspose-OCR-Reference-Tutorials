---
date: 2025-12-12
description: تعلم كيفية تنفيذ التعرف الضوئي على الأحرف (OCR) باستخدام وضع اكتشاف المناطق
  مع Aspose.OCR للغة Java، استخراج النص من الصورة، والحصول على نتائج مدققة إملائيًا.
  هذا دليل Aspose OCR للغة Java خطوة بخطوة.
linktitle: How to Perform OCR with Detect Areas Mode in Aspose.OCR
second_title: Aspose.OCR Java API
title: كيفية إجراء OCR باستخدام وضع كشف المناطق باستخدام Aspise.OCR للـ Java
url: /ar/java/ocr-operations/perform-ocr-detect-areas-mode/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إجراء OCR باستخدام وضع كشف المناطق في Aspose.OCR

## المقدمة

التعرف الضوئي على الأحرف (OCR) ضروري عندما تحتاج إلى **استخراج النص من صورة** وتحويلها إلى بيانات قابلة للبحث والتحرير. في هذا **دروس Aspose OCR Java** سنستعرض مثالًا عمليًا يوضح لك **كيفية إجراء OCR** باستخدام ميزة *Detect Areas Mode* القوية، وسنظهر أيضًا قدرة التدقيق الإملائي المدمجة. بنهاية هذا الدليل ستحصل على مقتطف شفرة جاهز للتنفيذ يتعرف على النص من مستند على شكل صورة ويعيد مخرجات نظيفة ومصححة.

## إجابات سريعة
- **ما هو وضع كشف المناطق؟** إعداد يُحسّن OCR للصور الفوتوغرافية عن طريق تحديد كتل النص تلقائيًا.  
- **ما هي لغة المثال المستخدمة؟** Java، مع مكتبة Aspose.OCR.  
- **هل أحتاج إلى ترخيص للاختبار؟** النسخة التجريبية المجانية تعمل للتطوير؛ يتطلب الترخيص التجاري للإنتاج.  
- **هل يمكن تدقيق النتيجة إملائيًا؟** نعم – تُعيد الـ API قسم “ocr with spell check”.  
- **ما نوع الملف المستخدم في العرض؟** صورة JPEG باسم *Receipt.jpg*.

## المتطلبات المسبقة

قبل الغوص في الدرس، تأكد من توفر المتطلبات التالية:

- بيئة تطوير Java: تأكد من تثبيت Java على جهازك.  
- Aspose.OCR for Java: قم بتحميل وتثبيت مكتبة Aspose.OCR. يمكنك العثور على رابط التحميل [هنا](https://releases.aspose.com/ocr/java/).  
- مستند للـ OCR: حضّر صورة مستند (مثلاً **Receipt.jpg**) تحتوي على النص الذي تريد استخراجَه.

## استيراد الحزم

في مشروع Java الخاص بك، استورد الحزم اللازمة لاستخدام Aspose.OCR. إليك مثالًا:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.DetectAreasMode;
import com.aspose.ocr.Language;
import com.aspose.ocr.License;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.RecognitionResult.LinesResult;
import com.aspose.ocr.RecognitionSettings;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## الخطوة 1: إعداد عملية OCR

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";

// The image path
String file = dataDir + "Receipt.jpg";

// Create AsposeOCR instance
AsposeOCR api = new AsposeOCR();

// Set recognition options
RecognitionSettings settings = new RecognitionSettings();
settings.setDetectAreasMode(DetectAreasMode.PHOTO);
```

في هذه الخطوة نقوم بتهيئة محرك OCR، وتوجيهه إلى ملف الصورة، وتمكين **Detect Areas Mode** بحيث يتعامل المحرك مع الصورة كصورة عادية تحتوي على كتل نصية متفرقة.

## الخطوة 2: تنفيذ OCR واسترجاع النتائج

```java
// Get result object
RecognitionResult result = null;
try {
    result = api.RecognizePage(file, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

هنا نقوم فعليًا **بتنفيذ OCR**. استدعاء `RecognizePage` يُعيد كائن `RecognitionResult` يحتوي على النص الخام، معلومات التخطيط، ومخرجات التدقيق الإملائي.

## الخطوة 3: طباعة نتائج OCR

```java
// Print result
printResult(result);
```

طريقة المساعدة `printResult` (المقدمة في حزمة المصدر الكاملة) تعرض كمية كبيرة من المعلومات: النص المستخرج، درجات الثقة، الفقرات المكتشفة، البيانات سطرًا بسطر، بدائل الأحرف، التحذيرات، حمولة JSON، والنص المصحح **OCR with spell check**.

## لماذا نستخدم Detect Areas Mode؟

- **محسّن للصور** – يعزل تلقائيًا مناطق النص، مما يقلل الضوضاء.  
- **دقة محسّنة** – خاصةً في الإيصالات، الفواتير، والنماذج الممسوحة.  
- **تدقيق إملائي مدمج** – ينظف الأخطاء الشائعة في OCR دون معالجة إضافية.

## حالات الاستخدام الشائعة

| السيناريو | الفائدة |
|----------|---------|
| معالجة الإيصالات | استخراج سريع لأسماء التجار، الإجماليات، والتواريخ. |
| رقمنة الفواتير | استخراج بنود الفاتورة ومعلومات الضرائب للأنظمة المحاسبية. |
| مسح وثائق الهوية | التقاط الأسماء والأرقام من رخص القيادة أو جوازات السفر. |

## نصائح استكشاف الأخطاء وإصلاحها ومواطن الأخطاء الشائعة

- **مسار ملف غير صحيح** – تحقق مرة أخرى من `dataDir` وتأكد من وجود الصورة.  
- **صور منخفضة الدقة** – تنخفض دقة OCR بشكل كبير تحت 300 dpi؛ فكر في معالجة مسبقة للصورة.  
- **ترخيص مفقود** – بدون ترخيص صالح، تعمل الـ API في وضع التجربة وقد تضع علامة مائية على النتائج.  

## الخلاصة

تهانينا! لقد تعلمت بنجاح **كيفية إجراء OCR** باستخدام Detect Areas Mode عبر Aspose.OCR للـ Java. هذه الطريقة لا تستخرج النص من ملفات الصور فحسب، بل توفر أيضًا مخرجات مصححة إملائيًا ونظيفة—مثالية لتدفقات البيانات اللاحقة أو عرض واجهة المستخدم.

## الأسئلة المتكررة

**س: هل يمكن لـ Aspose.OCR التعامل مع لغات متعددة؟**  
ج: نعم، يدعم Aspose.OCR مجموعة واسعة من اللغات، مما يجعله مرنًا للتطبيقات العالمية.

**س: هل Aspose.OCR مناسب لعمليات OCR على نطاق واسع؟**  
ج: بالتأكيد. تم تصميم المكتبة لتعامل مع سيناريوهات عالية الإنتاجية ويمكن دمجها في خطوط معالجة الدُفعات.

**س: هل يمكنني دمج Aspose.OCR في تطبيقات الويب؟**  
ج: نعم، يمكنك تضمين واجهة برمجة تطبيقات Java في خدمات الويب القائمة على Servlets أو Spring Boot لتوفير OCR كنقطة نهاية REST.

**س: هل يوفر Aspose.OCR قدرات التدقيق الإملائي؟**  
ج: نعم، كما هو موضح، تتضمن النتيجة قسم “ocr with spell check” الذي يصحح الأخطاء الشائعة في التعرف.

**س: هل هناك منتدى مجتمع لدعم Aspose.OCR؟**  
ج: نعم، يمكنك العثور على الدعم والتفاعل مع المجتمع في [منتدى Aspose.OCR](https://forum.aspose.com/c/ocr/16).

---

**Last Updated:** 2025-12-12  
**Tested With:** Aspose.OCR for Java 23.12 (latest at time of writing)  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}