---
date: 2025-12-10
description: تعلم كيفية التعرف على النص من الصورة واستخراج الفقرات من الصورة باستخدام
  Aspose.OCR للغة Java. دليل خطوة بخطوة مع أمثلة على الشيفرة.
linktitle: Recognize Text from Image and Retrieve Text Area Rectangles
second_title: Aspose.OCR Java API
title: التعرف على النص من الصورة واسترجاع مستطيلات مناطق النص
url: /ar/java/ocr-basics/get-rectangles-with-text-areas/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص من الصورة واسترجاع مستطيلات مناطق النص

## المقدمة

إذا كنت بحاجة إلى **recognize text from image** في ملفات صورة داخل تطبيق Java، فإن Aspose.OCR للـ Java يوفر طريقة سريعة ودقيقة للقيام بذلك. في هذا الدرس سنستعرض الخطوات الدقيقة المطلوبة لاستخراج الفقرات من صورة، الحصول على المستطيلات المحيطة بكل منطقة نصية، وطباعة تلك الإحداثيات إلى وحدة التحكم. في النهاية ستفهم لماذا تعمل هذه الطريقة، كيف تدمج المكتبة، وأين يمكنك توسيعها لتناسب حالات الاستخدام الخاصة بك.

## إجابات سريعة
- **ما معنى “recognize text from image”؟** يعني تحويل الأحرف البصرية في صورة إلى بيانات نصية قابلة للتحرير.  
- **أي مكتبة تتعامل مع ذلك في Java؟** Aspose.OCR للـ Java.  
- **هل أحتاج إلى ترخيص للتطوير؟** يتوفر ترخيص مؤقت للاختبار؛ يلزم ترخيص كامل للإنتاج.  
- **هل يمكن استخراج الفقرات بدلاً من الكلمات المفردة؟** نعم – استخدم `AreasType.PARAGRAPHS` للحصول على مستطيلات على مستوى الفقرة.  
- **هل الكود متوافق مع Java 11+؟** بالتأكيد، الـ API يعمل مع Java 11 وما بعدها.

## ما هو “recognize text from image” في Aspose.OCR؟
طريقة `RecognizePage` في Aspose.OCR تحلل البت ماب، تطبق خوارزميات OCR، وتعيد السلسلة النصية المعترف بها. عندما تطلب مناطق النص، تحسب المكتبة أيضًا إحداثيات `Rectangle` الدقيقة لكل كتلة نصية، مما يسهل تمييز أو معالجة الأقسام المحددة لاحقًا.

## لماذا تستخدم Aspose.OCR للـ Java؟
- **دقة عالية** – يدعم لغات متعددة وخطوط معقدة.  
- **تكامل سهل** – ملف JAR واحد يضيف قدرات OCR كاملة.  
- **إخراج مرن** – يمكنك استرجاع النص الخام، HTML منسق، أو مستطيلات دقيقة لمناطق النص.  
- **آمن للخطوط المتعددة** – مناسب لبيئات الخوادم ذات الإنتاجية العالية.

## المتطلبات المسبقة

- **Java Development Kit** (JDK 11 أو أحدث) مثبت على جهازك.  
- مكتبة **Aspose.OCR للـ Java** – حمّلها من الموقع الرسمي [هنا](https://releases.aspose.com/ocr/java/).  
- بيئة تطوير أو أداة بناء (Maven/Gradle) لإدارة تبعية الـ JAR.

## استيراد الحزم

في مشروع Java الخاص بك، استورد الفئات اللازمة:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AreasType;
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## دليل خطوة بخطوة

### الخطوة 1: إعداد مشروعك
أنشئ مشروع Java جديد (أو أضف إلى مشروع موجود) وضع ملف Aspose.OCR JAR على مسار الـ classpath. إذا كنت تستخدم Maven، أضف التبعية كما هو موضح في حزمة التحميل.

### الخطوة 2: تحديد دليل المستند ومسار الصورة
حدد مكان وجود صورة العينة:

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";

// The image path
String imagePath = dataDir + "p3.png";
```

### الخطوة 3: إنشاء مثيل Aspose.OCR
أنشئ محرك OCR:

```java
// Create Aspose.OCR instance
AsposeOCR api = new AsposeOCR();
```

### الخطوة 4: التعرف على النص في الصورة
استدعِ `RecognizePage` لتحويل الصورة إلى نص عادي. هذه الخطوة توضح القدرة الأساسية على **recognize text from image**:

```java
try {
    // Recognize page by full path to file
    String result = api.RecognizePage(imagePath);
    System.out.println("Result: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

### الخطوة 5: الحصول على المستطيلات مع مناطق النص
الآن استرجع المستطيلات المحيطة بكل فقرة (أو أنواع مناطق أخرى). هنا تقوم بـ **extract paragraphs from image** وتحصل على إحداثياتها:

```java
// Get rectangles with text areas in the image.
ArrayList<Rectangle> rectResult = api.getTextAreas(imagePath, AreasType.PARAGRAPHS, true);

// Print each text area rectangle
for (Rectangle r : rectResult) {
    System.out.println("Text area:" + r);
}
```

## المشكلات الشائعة & استكشاف الأخطاء وإصلاحها

| العَرَض | السبب المحتمل | الحل |
|---------|--------------|-----|
| `IOException` on `RecognizePage` | مسار ملف غير صحيح أو عدم وجود صلاحية قراءة | تحقق من أن `imagePath` يشير إلى ملف PNG/JPG موجود وأن التطبيق لديه صلاحية الوصول إلى نظام الملفات. |
| Empty result string | صورة ذات جودة منخفضة أو لغة غير مدعومة | عالج الصورة مسبقًا (زيادة التباين، تحويل إلى ثنائي) أو حدد اللغة الصحيحة باستخدام `api.setLanguage("eng")`. |
| No rectangles returned | استخدام `AreasType` غير صحيح (مثلاً `WORDS` بدلاً من الفقرات) | غيّر إلى `AreasType.PARAGRAPHS` أو `AreasType.LINES` حسب الحاجة. |

## الأسئلة المتكررة

**س: هل Aspose.OCR متوافق مع Java 11؟**  
ج: نعم، Aspose.OCR يعمل مع Java 11 والإصدارات الأحدث.

**س: هل يمكنني استخدام Aspose.OCR في المشاريع الشخصية والتجارية؟**  
ج: نعم، يمكنك استخدامه في أي نوع من المشاريع. لتفاصيل الترخيص، زر [هنا](https://purchase.aspose.com/buy).

**س: كيف أحصل على ترخيص مؤقت للتقييم؟**  
ج: يمكنك الحصول على ترخيص مؤقت [هنا](https://purchase.aspose.com/temporary-license/).

**س: أين يمكنني العثور على دعم المجتمع أو المساعدة الرسمية؟**  
ج: للدعم والنقاشات، زر [منتدى Aspose.OCR](https://forum.aspose.com/c/ocr/16).

**س: هل يدعم Aspose.OCR تعدد الخيوط؟**  
ج: نعم، المكتبة آمنة للخطوط المتعددة ويمكن استخدامها في بيئات متزامنة لتحسين الأداء.

## الخلاصة

في هذا الدرس تعلمت كيفية **recognize text from image** باستخدام Aspose.OCR للـ Java، استخراج الفقرات، واسترجاع المستطيلات الدقيقة التي تحيط بكل كتلة نصية. تتيح لك هذه القدرات بناء ملفات PDF قابلة للبحث، تمييز النص في واجهات المستخدم، أو تمرير بيانات منظمة إلى عمليات لاحقة. استكشف الـ API أكثر لتخصيص إعدادات اللغة، معالجة صيغ صور مختلفة، أو دمجها مع التخزين السحابي.

---

**آخر تحديث:** 2025-12-10  
**تم الاختبار مع:** Aspose.OCR 23.10 للـ Java  
**المؤلف:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}