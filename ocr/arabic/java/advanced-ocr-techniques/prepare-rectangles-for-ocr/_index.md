---
date: 2026-02-20
description: تعلم كيفية التعرف على مستطيلات الصفحات باستخدام Aspose.OCR للغة Java،
  واستخراج نصوص الصور في مشاريع Java، وتابع هذا الدرس التعليمي لـ Aspose OCR للغة
  Java للحصول على OCR دقيق.
linktitle: How to Recognize Page Rectangles for OCR Text Recognition in Aspose.OCR
second_title: Aspose.OCR Java API
title: كيفية التعرف على مستطيلات الصفحة لتقنية التعرف الضوئي على النص في Aspose.OCR
url: /ar/java/advanced-ocr-techniques/prepare-rectangles-for-ocr/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية التعرف على مستطيلات الصفحات للتعرف على النص باستخدام OCR في Aspose.OCR

## إجابات سريعة
- **ما المكتبة التي تتعامل مع التعرف على نص OCR في Java؟** Aspose.OCR for Java.  
- **هل أحتاج إلى ترخيص للاستخدام في الإنتاج؟** نعم – ترخيص Aspose.OCR صالح يفتح جميع الوظائف.  
- **هل يمكنني تحديد OCR لأجزاء معينة من الصورة؟** بالتأكيد؛ يمكنك تعريف المستطيلات التي تحدد المناطق المستهدفة.  
- **ما هي المتطلبات الأساسية الرئيسية؟** JDK 17+، Aspose.OCR for Java، وبيئة تطوير Java IDE.  
- **هل هذه الطريقة مناسبة لاستخراج النص من الصور؟** نعم، إنها طريقة فعّالة لـ **extract text image java** projects.

## ما هو “recognize page rectangles”؟
تشير العبارة إلى ممارسة تزويد محرك OCR بقائمة من كائنات `java.awt.Rectangle` حتى يعالج فقط تلك المناطق المحددة في الصفحة. هذا النهج المركّز يقلل من وقت المعالجة ويحسن الدقة، خاصةً في المستندات المعقدة مثل الفواتير أو النماذج.

## لماذا إعداد المستطيلات للتعرف على نص OCR؟
تحديد المستطيلات يركز المحرك على المناطق التي تحتوي فعليًا على نص، مما:
* يقلل من وقت المعالجة.  
* يحسن الدقة بتجاهل الخلفيات المزعجة.  
* يتيح لك استخراج البيانات التي تحتاجها فقط—مثالي للنماذج والفواتير والإيصالات.  

## المتطلبات الأساسية

قبل أن تبدأ، تأكد من أن لديك:

- **Java Development Kit (JDK)** – Aspose.OCR for Java يعمل مع JDK 17 أو أحدث. قم بتنزيله من موقع Oracle.  
- **Aspose.OCR for Java library** – احصل على أحدث ملف JAR من صفحة التحميل الرسمية [here](https://releases.aspose.com/ocr/java/). اتبع دليل التثبيت [here](https://reference.aspose.com/ocr/java/).  
- **بيئة التطوير** – أي IDE للـ Java (IntelliJ IDEA، Eclipse، VS Code، إلخ) سيكون مناسبًا.

## استيراد الحزم

في ملف Java الخاص بك، استورد الفئات المطلوبة من Aspose.OCR والأدوات القياسية لـ Java:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

> *نستورد `java.awt.Rectangle` لأن واجهة برمجة تطبيقات OCR تتوقع المستطيلات التي تحدد المناطق التي يجب مسحها.*

## الخطوة 1: إعداد الترخيص

```java
SetLicense.main(null);
```

استدعاء `SetLicense` يفعّل ترخيص Aspose.OCR الخاص بك، يزيل حدود التقييم ويفعل التعرف الكامل على نص OCR.

## الخطوة 2: تعريف دليل المستند ومسار الصورة

```java
String dataDir = "Your Document Directory";
String imagePath = dataDir + "p.png";
```

استبدل `"Your Document Directory"` بالمسار المطلق حيث توجد صورتك (`p.png`). هذه هي الصورة التي سيتم معالجتها.

## الخطوة 3: إنشاء كائن Aspose.OCR

```java
AsposeOCR api = new AsposeOCR();
```

إنشاء كائن `AsposeOCR` يمنحك الوصول إلى طريقة `RecognizePage`، التي تقوم بتنفيذ OCR الفعلي.

## الخطوة 4: إعداد المستطيلات مع النصوص

```java
ArrayList<Rectangle> rectArray = new ArrayList<Rectangle>();
rectArray.add(new Rectangle(138, 352, 2033, 537));
rectArray.add(new Rectangle(147, 890, 2033, 1157));
rectArray.add(new Rectangle(923, 2045, 465, 102));
rectArray.add(new Rectangle(104, 2147, 2076, 819));
```

كل `Rectangle(x, y, width, height)` يخبر Aspose.OCR بالضبط أين يبحث عن النص. عدّل الإحداثيات لتتناسب مع تخطيط الصورة المصدر.

## الخطوة 5: تنفيذ التعرف على OCR

```java
try {
    String result = api.RecognizePage(imagePath, rectArray);
    System.out.println("Result with rect: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

استدعاء `RecognizePage` يعالج فقط المستطيلات المحددة ويعيد السلسلة المستخرجة. يتيح لك إخراج وحدة التحكم التحقق من نتيجة **ocr text recognition** فورًا.

## المشكلات الشائعة والنصائح

| المشكلة | السبب | الحل |
|-------|-------|----------|
| **لا يوجد إخراج** | إحداثيات المستطيلات غير صحيحة أو مسار الصورة غير صحيح | تحقق مرة أخرى من قيمة `dataDir` وتأكد من أن المستطيلات تغطي مناطق النص فعليًا. |
| **حروف غير صالحة** | صورة منخفضة الدقة أو خط غير مدعوم | استخدم مصدرًا بدقة أعلى أو طبّق معالجة مسبقة للصورة (مثل التحويل إلى ثنائي). |
| **لم يتم تطبيق الترخيص** | `SetLicense` لم يُستدعَ قبل OCR | تأكد من تشغيل `SetLicense.main(null);` قبل أي استدعاءات API. |
| **بطء الأداء** | عدد كبير من المستطيلات الكبيرة | قلل عدد المستطيلات واجعلها ضيقة قدر الإمكان حول النص. |

## الأسئلة المتكررة

**س:** *هل Aspose.OCR متوافق مع لغات برمجة أخرى؟*  
**ج:** نعم، Aspose.OCR يدعم أيضًا .NET، C++، وPython. راجع الوثائق الرسمية للحصول على أمثلة خاصة بكل لغة.

**س:** *هل يمكنني استخدام Aspose.OCR في مشروع تجاري؟*  
**ج:** بالتأكيد. اشترِ ترخيصًا تجاريًا عبر [Aspose store](https://purchase.aspose.com/buy).

**س:** *هل هناك نسخة تجريبية مجانية متاحة؟*  
**ج:** نعم، يمكنك تنزيل نسخة تجريبية [here](https://releases.aspose.com/).

**س:** *كيف أحصل على ترخيص مؤقت للتقييم؟*  
**ج:** يتم توفير التراخيص المؤقتة عبر [Aspose temporary‑license portal](https://purchase.aspose.com/temporary-license/).

**س:** *أين يمكنني الحصول على دعم المجتمع؟*  
**ج:** زر منتدى Aspose.OCR [forum](https://forum.aspose.com/c/ocr/16) للحصول على أسئلة، نصائح، وعينات كود.

## الخلاصة

لقد تعلمت الآن كيفية **recognize page rectangles** باستخدام Aspose.OCR للـ Java، إعداد الترخيص، تعريف مسارات الصور، والأهم من ذلك إعداد مستطيلات دقيقة لتوجيه OCR إلى الأجزاء المحددة من الصورة التي تحتاجها. هذه التقنية مثالية لأي **aspose ocr java tutorial** يتطلب استخراج نص دقيق وعالي الأداء.

---

**آخر تحديث:** 2026-02-20  
**تم الاختبار مع:** Aspose.OCR for Java 24.12  
**المؤلف:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}