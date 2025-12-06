---
date: 2025-12-06
description: تعرّف على كيفية استخدام Aspose.OCR للغة Java لإجراء التعرف الضوئي على
  النص، واستخراج النص من الصور، وإعداد المستطيلات للتعرف المستهدف.
language: ar
linktitle: Preparing Rectangles for OCR Text Recognition in Aspose.OCR
second_title: Aspose.OCR Java API
title: إعداد المستطيلات للتعرف على النص باستخدام OCR في Aspose.OCR
url: /java/advanced-ocr-techniques/prepare-rectangles-for-ocr/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إعداد المستطيلات لتعرف النصوص عبر OCR في Aspose.OCR

## Introduction

في عالم اليوم القائم على البيانات، يُعد **تعرف النص عبر OCR** حجر الزاوية لتحويل المستندات الممسوحة ضوئيًا، واللقطات، والصور إلى محتوى قابل للبحث والتحرير. تجعل مكتبة Aspose.OCR for Java هذه العملية سريعة وموثوقة، خاصة عندما تحتاج إلى التركيز على مناطق محددة من الصورة. في هذا البرنامج التعليمي سنستعرض كل خطوة مطلوبة لإعداد المستطيلات التي تحدّ OCR إلى المناطق التي تهتم بها، مما يمنحك تحكمًا دقيقًا وأداءً أفضل.

## Quick Answers
- **ما المكتبة التي تتعامل مع تعرف النص عبر OCR في Java؟** Aspose.OCR for Java.  
- **هل أحتاج إلى ترخيص للاستخدام في الإنتاج؟** نعم – ترخيص Aspose.OCR صالح يفتح جميع الوظائف.  
- **هل يمكنني حصر OCR على أجزاء معينة من الصورة؟** بالتأكيد؛ يمكنك تعريف مستطيلات تحدد المناطق المستهدفة.  
- **ما هي المتطلبات الأساسية؟** JDK 17+، Aspose.OCR for Java، وبيئة تطوير Java.  
- **هل هذه الطريقة مناسبة لاستخراج النص من الصور؟** نعم، إنها طريقة فعّالة لـ **extract text image java** في المشاريع.

## What is OCR Text Recognition?
تحويل النص عبر OCR (Optical Character Recognition) يحوّل الصور القائمة على البكسل إلى أحرف قابلة للقراءة آليًا. يتيح لك ذلك البحث، التحرير، وتحليل المحتوى الذي كان في الأصل مجرد صور.

## Why Prepare Rectangles for OCR Text Recognition?
تحديد المستطيلات يركّز المحرك على المناطق التي تحتوي فعليًا على نص، مما:
* يقلل من زمن المعالجة.
* يحسّن الدقة بتجاهل الخلفيات المزعجة.
* يسمح لك باستخراج البيانات التي تحتاجها فقط—مثالي للنماذج، الفواتير، والإيصالات.

## Prerequisites

قبل البدء، تأكد من وجود:

- **Java Development Kit (JDK)** – تعمل Aspose.OCR for Java مع JDK 17 أو أحدث. حمّله من موقع Oracle.
- **Aspose.OCR for Java library** – احصل على أحدث ملف JAR من صفحة التحميل الرسمية [هنا](https://releases.aspose.com/ocr/java/). اتبع دليل التثبيت [هنا](https://reference.aspose.com/ocr/java/).
- **Development Environment** – أي بيئة تطوير Java (IntelliJ IDEA، Eclipse، VS Code، إلخ) ستفي بالغرض.

## Import Packages

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

## Step 1: Set Up License

```java
SetLicense.main(null);
```

استدعاء `SetLicense` يُفعّل ترخيص Aspose.OCR الخاص بك، ويزيل حدود التقييم ويتيح التعرف الكامل على النص عبر OCR.

## Step 2: Define Document Directory and Image Path

```java
String dataDir = "Your Document Directory";
String imagePath = dataDir + "p.png";
```

استبدل `"Your Document Directory"` بالمسار المطلق حيث توجد الصورة (`p.png`). هذه هي الصورة التي سيتم معالجتها.

## Step 3: Create Aspose.OCR Instance

```java
AsposeOCR api = new AsposeOCR();
```

إنشاء كائن `AsposeOCR` يمنحك الوصول إلى طريقة `RecognizePage`، التي تُجري عملية OCR الفعلية.

## Step 4: Prepare Rectangles with Texts

```java
ArrayList<Rectangle> rectArray = new ArrayList<Rectangle>();
rectArray.add(new Rectangle(138, 352, 2033, 537));
rectArray.add(new Rectangle(147, 890, 2033, 1157));
rectArray.add(new Rectangle(923, 2045, 465, 102));
rectArray.add(new Rectangle(104, 2147, 2076, 819));
```

كل `Rectangle(x, y, width, height)` يخبر Aspose.OCR بالضبط أين يبحث عن النص. عدّل الإحداثيات لتتناسب مع تخطيط صورتك المصدرية.

## Step 5: Perform OCR Recognition

```java
try {
    String result = api.RecognizePage(imagePath, rectArray);
    System.out.println("Result with rect: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

استدعاء `RecognizePage` يعالج المستطيلات المحددة فقط ويعيد السلسلة المستخرجة. يتيح لك إخراج وحدة التحكم التحقق من نتيجة **تعرف النص عبر OCR** فورًا.

## Common Issues and Tips

| Issue | Cause | Solution |
|-------|-------|----------|
| **No output** | إحداثيات المستطيل غير صحيحة أو مسار الصورة خاطئ | تحقق من قيمة `dataDir` وتأكد من أن المستطيلات تغطي فعليًا مناطق النص. |
| **Garbage characters** | صورة منخفضة الدقة أو خط غير مدعوم | استخدم مصدرًا بدقة أعلى أو طبّق معالجة مسبقة للصورة (مثل الثنائيات). |
| **License not applied** | لم يتم استدعاء `SetLicense` قبل OCR | تأكد من تشغيل `SetLicense.main(null);` قبل أي استدعاءات API. |
| **Performance lag** | عدد كبير من المستطيلات الكبيرة | قلل عدد المستطيلات واجعلها محكمة قدر الإمكان حول النص. |

## Conclusion

لقد تعلمت الآن كيفية دمج Aspose.OCR for Java، إعداد الترخيص، تعريف مسارات الصور، والأهم من ذلك—إعداد المستطيلات لتوجيه **تعرف النص عبر OCR** إلى أجزاء محددة من الصورة. هذه التقنية مثالية لأي **java ocr tutorial** يحتاج إلى استخراج نص دقيق وعالي الأداء.

## Frequently Asked Questions

**Q: Is Aspose.OCR compatible with other programming languages?**  
A: Yes, Aspose.OCR also supports .NET, C++, and Python. Check the official docs for language‑specific samples.

**Q: Can I use Aspose.OCR in a commercial project?**  
A: Absolutely. Purchase a commercial license via the [Aspose store](https://purchase.aspose.com/buy).

**Q: Is there a free trial available?**  
A: Yes, you can download a trial version [here](https://releases.aspose.com/).

**Q: How do I obtain a temporary license for evaluation?**  
A: Temporary licenses are provided through the [Aspose temporary‑license portal](https://purchase.aspose.com/temporary-license/).

**Q: Where can I get community support?**  
A: Visit the Aspose.OCR [forum](https://forum.aspose.com/c/ocr/16) for questions, tips, and code samples.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Last Updated:** 2025-12-06  
**Tested With:** Aspose.OCR for Java 24.12  
**Author:** Aspose  

---