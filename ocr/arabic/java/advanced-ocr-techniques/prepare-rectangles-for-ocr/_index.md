---
date: 2025-12-06
description: تعرّف على كيفية استخدام Aspose.OCR للغة Java لإجراء التعرف الضوئي على
  النص، واستخراج النص من الصور، وإعداد المستطيلات للتعرف المستهدف.
linktitle: Preparing Rectangles for OCR Text Recognition in Aspose.OCR
second_title: Aspose.OCR Java API
title: إعداد المستطيلات للتعرف على النص باستخدام OCR في Aspose.OCR
url: /ar/java/advanced-ocr-techniques/prepare-rectangles-for-ocr/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إعداد المستطيلات لتعرف النصوص عبر OCR في Aspose.OCR

## مقدمة

في عالم اليوم الموجود على البيانات، **تعرف على النص عبر OCR** ​​يصور المستندات الممسوحة ضوئيًا، ولقطات، وصور لمراقبة قابلة للبحث والتحرير. اجعل مكتبة Aspose.OCR لـ Java هذه طريقة موثوقة وموثوقة، خاصة عندما تحتاج إلى التركيز على مناطق محددة من الصورة. في هذا البرنامج التعليمي سنستعرض كل خطوة مطلوبة لإعداد الاسترات التي تدرس التعرف الضوئي على الحروف إلى المناطق التي أون بها، مما يؤدي إلى تحكم دقيق وأداءً أفضل.

## إجابات سريعة
- **ما المكتبة التي تعرفها عبر OCR في Java؟** Aspose.OCR for Java.
- **هل أحتاج إلى ترخيص للاستخدام في الإنتاج؟** نعم –ترخيص Aspose.OCR صالح يفتح جميع الوظائف.
- **هل يمكنني حجز التعرف الضوئي على الحروف على أجزاء معينة من الصورة؟** بالتأكيد؛ يمكنك تعريف تسجيلات مناطق التفاصيل.
- **ما هي المتطلبات الأساسية؟** JDK17+، Aspose.OCR for Java، وبيئة تطوير Java.
- **هل هذه طريقة لاستخراج النص من الصور؟** نعم، طريقة فعّالة لـ **extract text image java** في المشاريع.

## ما هو التعرف الضوئي على الحروف (OCR)؟
تحويل النص عبر OCR (التعرف البصري على الأحرف) يحوّل الصور القائمة على البكسل إلى أحرف قابلة للقراءة آليًا. يتيح لك ذلك البحث، التحرير، وتحليل المحتوى الذي كان في مجرد صور أصلية.

## لماذا نقوم بإعداد المستطيلات للتعرف على النص بتقنية التعرف الضوئي على الحروف؟
تحديد المستطيلات يركّز المحرك على المناطق التي تحتوي فعليًا على نص، مما:
* تحديد زمن المعالجة.
* تحسين الدقة بتجاهل الخلفيات المزعجة.
* يسمح لك باستخراج البيانات التي تحتاجها فقط—مثالي للنماذج، الفاتورة، والإيصالات.

## المتطلبات الأساسية

قبل البدء، تأكد من وجود:

- **Java Development Kit (JDK)** – اضغط على Aspose.OCR لـ Java باستخدام JDK17 أو أحدث. نتانياهو من موقع أوراكل.
- **Aspose.OCR for Java Library** – احصل على أحدث ملف JAR من صفحة التحميل الرسمية [هنا](https://releases.aspose.com/ocr/java/). اتبع دليل التثبيت [هنا](https://reference.aspose.com/ocr/Java/).
- **بيئة التطوير** – أي بيئة تطوير Java (IntelliJ IDEA، Eclipse، VS Code، إلخ) ستفي الكبار.

## استيراد الحزم

في ملف Java الخاص بك، استورد فئات Aspose.OCR المطلوبة وأدوات Java القياسية:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

> *نستورد `java.awt.Rectangle` لأن واجهة برمجة تطبيقات OCR تتوقع مستطيلات تحدد المناطق التي سيتم مسحها.*

## الخطوة 1: إعداد الترخيص

```java
SetLicense.main(null);
```

استدعاء `SetLicense` يُفعّل ترخيص Aspose.OCR الخاص بك، ويزيل حدود التقييم ويتيح التعرف الكامل على النص عبر OCR.

## الخطوة 2: تحديد دليل المستندات ومسار الصورة

```java
String dataDir = "Your Document Directory";
String imagePath = dataDir + "p.png";
```

استبدل `"Your Document Directory"` بالمسار المطلق حيث توجد الصورة (`p.png`). هذه هي الصورة التي سيتم معالجتها.

## الخطوة 3: إنشاء مثيل Aspose.OCR

```java
AsposeOCR api = new AsposeOCR();
```

إنشاء كائن `AsposeOCR` يمنحك الوصول إلى طريقة `RecognizePage`، التي تُجري عملية OCR الفعلية.

## الخطوة 4: تجهيز المستطيلات بالنصوص

```java
ArrayList<Rectangle> rectArray = new ArrayList<Rectangle>();
rectArray.add(new Rectangle(138, 352, 2033, 537));
rectArray.add(new Rectangle(147, 890, 2033, 1157));
rectArray.add(new Rectangle(923, 2045, 465, 102));
rectArray.add(new Rectangle(104, 2147, 2076, 819));
```

كل `Rectangle(x, y, width, height)` يخبر Aspose.OCR بالضبط أين يبحث عن النص. عدّل الإحداثيات لتتناسب مع تخطيط صورتك المصدرية.

## الخطوة 5: إجراء التعرف الضوئي على الأحرف (OCR)

```java
try {
    String result = api.RecognizePage(imagePath, rectArray);
    System.out.println("Result with rect: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

استدعاء `RecognizePage` يعالج المستطيلات المحددة فقط ويعيد السلسلة المستخرجة. يتيح لك إخراج وحدة التحكم التحقق من نتيجة **تعرف النص عبر OCR** فورًا.

## المشكلات والنصائح الشائعة

| العدد | السبب | الحل |
|-------|-------|----------|
| ** لا يوجد مخرج ** | إحداثيات المستطيلة غير صحيحة أو مسار الصورة الخاطئة | تحقق من قيمة `dataDir` وتأكد من المناطق التي تغطي المستطيلات النص الأصلي. |
| **أحرف مهملة** | صورة منخفضة الدقة أو خط غير مدعوم | استخدم مصدرًا جيدًا أو طبًا دقيقًا جدًا للسيدة (مثل الثنائيات). |
| **لم يتم تطبيق الترخيص** | لم يتم الاتصال بـ `SetLicense` بواسطة OCR | تأكد من تشغيل `SetLicense.main(null);` قبل أي اتصالات API. |
| **تأخر الأداء** | عدد كبير من المستطيلات الكبيرة | تقليل عدد الاستراتات وجعلها محكمة قدر الإمكان حول النص. |

## خاتمة

لقد تعلمت الآن كيفية دمج Aspose.OCR for Java، إعداد الترخيص، تعريف مسارات الصور، والأهم من ذلك—إعداد المستطيلات لتوجيه **تعرف النص عبر OCR** إلى أجزاء محددة من الصورة. هذه التقنية مثالية لأي **java ocr tutorial** يحتاج إلى استخراج نص دقيق وعالي الأداء.

## الأسئلة الشائعة

**س: هل يتوافق Aspose.OCR مع لغات برمجة أخرى؟**

ج: نعم، يدعم Aspose.OCR أيضًا .NET وC++ وPython. راجع الوثائق الرسمية للاطلاع على أمثلة خاصة بكل لغة.


**س: هل يمكنني استخدام Aspose.OCR في مشروع تجاري؟**

ج: بالتأكيد. يمكنك شراء ترخيص تجاري من خلال متجر Aspose.


**س: هل تتوفر نسخة تجريبية مجانية؟**

ج: نعم، يمكنك تنزيل نسخة تجريبية من هنا.


**س: كيف أحصل على ترخيص مؤقت للتقييم؟**

ج: تُقدم التراخيص المؤقتة من خلال بوابة التراخيص المؤقتة لـ Aspose.

**س: أين يمكنني الحصول على دعم من المجتمع؟**

لمجتمع؟ ج: تفضل بزيارة منتدى Aspose.OCR (https://forum.aspose.com/c/ocr/16) للاطلاع على الأسئلة والنصائح ونماذج التعليمات البرمجية.

---

**آخر تحديث:** 2025-12-06
**تم الاختبار باستخدام:** Aspose.OCR لجافا 24.12
**المؤلف:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
