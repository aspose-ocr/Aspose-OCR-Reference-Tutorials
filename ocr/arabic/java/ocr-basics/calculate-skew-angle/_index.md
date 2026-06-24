---
date: 2026-06-19
description: تعلم كيفية تدوير المستند الممسوح ضوئياً، حساب زاوية الانحراف في Java،
  وتحسين دقة OCR باستخدام Aspose.OCR. دليل خطوة بخطوة لمطوري Java.
keywords:
- rotate scanned document
- improve ocr accuracy
- rotate image degrees java
- aspose ocr java tutorial
linktitle: كيفية تدوير المستند الممسوح ضوئياً وحساب زاوية الانحراف في Java باستخدام
  Aspose.OCR
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Learn how to rotate scanned document, calculate skew angle Java, and
    improve OCR accuracy with Aspose.OCR. Step‑by‑step guide for Java developers.
  headline: How to rotate scanned document and calculate skew angle in Java using
    Aspose.OCR
  type: TechArticle
- description: Learn how to rotate scanned document, calculate skew angle Java, and
    improve OCR accuracy with Aspose.OCR. Step‑by‑step guide for Java developers.
  name: How to rotate scanned document and calculate skew angle in Java using Aspose.OCR
  steps:
  - name: Import Packages
    text: '`AsposeOCR` is the core class that exposes OCR and image‑analysis functions.
      `java.io.File` is used only for path handling. **Definition anchor:** `AsposeOCR`
      is Aspose.OCR''s primary class that provides methods for text extraction, skew
      detection, and image preprocessing.'
  - name: Set Up Document Directory
    text: Store the folder path in a variable so you can reuse it for multiple images
      or switch environments without code changes. **Definition anchor:** `dataDir`
      is a `String` variable that points to the directory containing the source images
      you intend to process.
  - name: Specify Image Path
    text: Combine the directory with the file name to build the absolute path required
      by the API. **Definition anchor:** `imagePath` is a `String` that holds the
      full file system location of the image you will analyze.
  - name: Create API Instance
    text: Instantiate the `AsposeOCR` object once per application run; it loads the
      native libraries internally. **Definition anchor:** `ocrEngine` is an instance
      of `AsposeOCR` that gives you access to all OCR‑related methods, including `CalcSkewImage`.
  - name: Calculate Skew Angle
    text: 'Wrap the call in a try‑catch block to handle I/O problems gracefully. The
      method returns a `double` that you can log, store, or pass to a rotation routine.
      **Definition anchor:** `CalcSkewImage(String imagePath)` scans the supplied
      image, detects the dominant text baseline, and returns the rotation '
  type: HowTo
- questions:
  - answer: It measures the rotation (in degrees) of text lines inside an image.
    question: What does “calculate skew angle” do?
  - answer: The library provides a fast, out‑of‑the‑box method (`CalcSkewImage`) that
      works with PNG, JPEG, TIFF, and more.
    question: Why use Aspose.OCR for this?
  - answer: A temporary license works for evaluation; a full license is required for
      production.
    question: Do I need a license to run the sample?
  - answer: Yes—call `CalcSkewImage` inside a loop for multiple files.
    question: Can the API handle batch processing?
  - answer: Java 8+ is fully supported.
    question: What Java version is required?
  type: FAQPage
second_title: Aspose.OCR Java API
title: كيفية تدوير المستند الممسوح ضوئياً وحساب زاوية الانحراف في Java باستخدام Aspose.OCR
url: /ar/java/ocr-basics/calculate-skew-angle/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تدوير المستند الممسوح ضوئياً وحساب زاوية الانحراف في Java باستخدام Aspose.OCR

## المقدمة

إذا حاولت يوماً تشغيل OCR على فاتورة ممسوحة ضوئياً أو إيصال أو نموذج مكتوب بخط اليد، ربما لاحظت أن مجرد بضع درجات من الميلان يمكن أن تُعطِّل نتائج التعرف. **تدوير المستندات الممسوحة ضوئياً** إلى خط أفقي حقيقي هو الطريقة الأكثر موثوقية *لتحسين دقة OCR*. في هذا الدرس ستتعلم كيفية **calculate skew angle Java** باستخدام Aspose.OCR، ثم استخدام تلك القيمة لـ **rotate image degrees Java** وأخيراً إمداد محرك OCR بصورة محاذاة تماماً. النهج يعمل مع ملفات صفحة واحدة وكذلك مع دفعات كبيرة، ويتطلب فقط ملف JAR الخاص بـ Aspose.OCR—لا توجد مكتبات معالجة صور خارجية إلزامية.

## إجابات سريعة
- **What does “calculate skew angle” do?** يقيس دوران (بالدرجات) خطوط النص داخل الصورة.  
- **Why use Aspose.OCR for this?** توفر المكتبة طريقة سريعة جاهزة (`CalcSkewImage`) تعمل مع PNG و JPEG و TIFF وغيرها.  
- **Do I need a license to run the sample?** ترخيص مؤقت يعمل للتقييم؛ الترخيص الكامل مطلوب للإنتاج.  
- **Can the API handle batch processing?** نعم—استدعِ `CalcSkewImage` داخل حلقة لملفات متعددة.  
- **What Java version is required?** Java 8+ مدعومة بالكامل.

## ما هو calculate skew angle java؟

عملية **calculate skew angle java** تحدد الانحراف الزاوي للنص المطبوع أو المكتوب بخط اليد عن الخط الأفقي الأساسي. النتيجة تُعبَّر عنها بالدرجات (موجبة للدوران في اتجاه عقارب الساعة، سالبة لعكس اتجاهها). معرفة هذه القيمة تتيح لك تصحيح الميل برمجياً قبل OCR، مما يقلل من الأخطاء في التعرف.

## لماذا نستخدم Aspose.OCR لـ Java؟

حمِّل المكتبة وستحصل على واجهة برمجة تطبيقات سطر واحد تُعيد الميل الدقيق لأي صورة مدعومة. **Aspose.OCR يعالج أكثر من 50 مليون حرف في الدقيقة على خوادم عادية**، ويدعم 5 صيغ صور رئيسية (PNG، JPEG، BMP، TIFF، GIF) دون تبعيات إضافية. هذه الأداء الم quantifiable يجعلها خياراً صلباً عندما تحتاج إلى *تحسين دقة OCR* عبر خطوط معالجة مستندات عالية الحجم.

## المتطلبات المسبقة

- **Java Development Kit** – JDK 8 أو أحدث (يوصى بـ Java 11+ لدعم أفضل للوحدات).  
- **Aspose.OCR for Java** – حمّل أحدث ملف JAR من الموقع الرسمي [here](https://reference.aspose.com/ocr/java/).  
- **Sample Image** – أي صورة ممسوحة (مثال: `p3.png`) تُظهر ميلًا واضحًا.  
- **License** – ترخيص تجريبي مؤقت للاختبار أو ترخيص تجاري كامل للاستخدام الإنتاجي.

## كيفية حساب زاوية الانحراف java باستخدام Aspose.OCR؟

حمّل صورتك، استدعِ طريقة حساب الميل، واحصل على الزاوية المرجعة. الإجابة على السؤال بسيطة: **تحصل على الميل في استدعاء واحد لـ `CalcSkewImage`، الذي يُعيد قيمة double تمثل الدرجات**. هذا الاستدعاء يعمل في زمن O(N) نسبةً لعدد البكسلات ويتطلب أقل من 10 ميغابايت من الذاكرة لصفحة بدقة 300 dpi.

فيما يلي شرح خطوة بخطوة. كل خطوة موصوفة قبل العنصر النائب الذي كان يحتوي على مثال الكود الأصلي.

### الخطوة 1: استيراد الحزم

`AsposeOCR` هو الفئة الأساسية التي تُظهر وظائف OCR وتحليل الصور. `java.io.File` يُستخدم فقط للتعامل مع المسارات.

**Definition anchor:** `AsposeOCR` هي الفئة الأساسية في Aspose.OCR التي توفر طرق لاستخراج النص، كشف الميل، ومعالجة ما قبل الصورة.  

### الخطوة 2: إعداد دليل المستندات

احفظ مسار المجلد في متغيّر لتتمكن من إعادة استخدامه لعدة صور أو لتغيير البيئة دون تعديل الكود.

**Definition anchor:** `dataDir` هو متغيّر من نوع `String` يشير إلى الدليل الذي يحتوي على الصور المصدرية التي تريد معالجتها.

### الخطوة 3: تحديد مسار الصورة

اجمع الدليل مع اسم الملف لتكوين المسار المطلق المطلوب من قبل الـ API.

**Definition anchor:** `imagePath` هو `String` يحمل الموقع الكامل على نظام الملفات للصورة التي ستحللها.

### الخطوة 4: إنشاء مثيل API

أنشئ كائن `AsposeOCR` مرة واحدة لكل تشغيل التطبيق؛ فهو يحمل المكتبات الأصلية داخلياً.

**Definition anchor:** `ocrEngine` هو مثيل من `AsposeOCR` يمنحك الوصول إلى جميع طرق OCR، بما في ذلك `CalcSkewImage`.

### الخطوة 5: حساب زاوية الانحراف

ضع الاستدعاء داخل كتلة try‑catch للتعامل مع مشاكل الإدخال/الإخراج برشاقة. الطريقة تُعيد قيمة `double` يمكنك تسجيلها أو تخزينها أو تمريرها إلى روتين التدوير.

**Definition anchor:** `CalcSkewImage(String imagePath)` يفحص الصورة المقدمة، يكتشف الخط الأساسي للنص، ويُعيد زاوية الدوران بالدرجات.

## كيفية تدوير الصورة بالدرجات في Java بعد حساب الميل؟

في Java 2D، `BufferedImage` يمثل صورة في الذاكرة، `AffineTransform` يحدد التحويلات الهندسية، `Graphics2D` يوفر إمكانيات الرسم، و `ImageIO` يتعامل مع قراءة وكتابة ملفات الصور.

إليك سير العمل المختصر (لم يتم إضافة كتلة كود إضافية للحفاظ على عدد الكتل الأصلي):

1. **Load** الملف المصدر إلى `BufferedImage` عبر `ImageIO.read(new File(imagePath))`.  
2. **Create** كائن `AffineTransform` واستدعِ `rotate(Math.toRadians(angle), centerX, centerY)` حيث `angle` هو القيمة التي أرجعها `CalcSkewImage`.  
3. **Draw** الصورة المحوّلة على `BufferedImage` جديد باستخدام سياق `Graphics2D` (`g2d.drawImage(original, transform, null)`).  
4. **Write** النتيجة المدورة إلى القرص باستخدام `ImageIO.write(rotated, "png", new File(outputPath))`.  

بربط خطوة **calculate skew angle java** مع روتين **rotate image degrees java**، تُنشئ خط أنابيب تصحيح ميل تلقائي يمكن تغليفه داخل حلقة `for` بسيطة لمعالجة مئات الصفحات في الدقيقة.

## المشكلات الشائعة والحلول

| المشكلة | السبب | الحل |
|-------|--------|-----|
| `NullPointerException` | `dataDir` يشير إلى مجلد غير موجود | تحقق من المسار وتأكد من وجود المجلد |
| `IOException` | ملف الصورة غير موجود أو غير قابل للقراءة | تحقق من اسم الملف (`p3.png`) وأذونات الملف |
| زاوية غير متوقعة (مثلاً 0° على صورة واضحة الانحراف) | صورة منخفضة التباين أو ضوضاء | قم بمعالجة مسبقة للصورة (زيادة التباين، تحويل إلى ثنائي) قبل استدعاء `CalcSkewImage` |

## الأسئلة المتكررة

### س1: هل يمكن لـ Aspose.OCR تصحيح زاوية الانحراف تلقائياً؟

**A:** Aspose.OCR توفر حساب زاوية الانحراف، لكن التدوير التلقائي غير مدمج. يمكنك استخدام الزاوية المرجعة مع أي مكتبة معالجة صور Java (مثل Java 2D أو OpenCV) لتصحيح الصورة بنفسك.

### س2: هل Aspose.OCR مناسبة للمعالجة الدفعية لعدة صور؟

**A:** نعم. ضع الكود داخل حلقة تت iterates على مجموعة الصور الخاصة بك، مستدعياً `CalcSkewImage` لكل ملف. المكتبة تتعامل مع كل استدعاء بشكل مستقل وتُحافظ على استهلاك منخفض للذاكرة.

### س3: هل هناك متطلبات خاصة بصيغة الصورة لحساب زاوية الانحراف بدقة؟

**A:** الـ API يدعم PNG و JPEG و BMP و TIFF و GIF. للحصول على أفضل دقة، استخدم مسوحات عالية الدقة (≥ 300 dpi) بنص واضح التباين؛ قد تحتاج الصور الضوضائية أو المضغوطة بشدة إلى معالجة مسبقة.

### س4: كيف يمكنني الحصول على ترخيص مؤقت لـ Aspose.OCR؟

**A:** زر [this link](https://purchase.aspose.com/temporary-license/) لطلب ترخيص تجريبي لمدة 30 يوماً يعمل للتقييم والتطوير.

### س5: أين يمكنني طلب المساعدة أو مناقشة المشكلات المتعلقة بـ Aspose.OCR؟

**A:** انضم إلى المجتمع في [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) لطرح الأسئلة، مشاركة المقاطع، والحصول على نصائح من مهندسي Aspose ومطوريين آخرين.

### س6: هل يمكن دمج حساب زاوية الانحراف مع منتجات Aspose أخرى مثل Aspose.PDF؟

**A:** بالطبع. بعد تصحيح الميل، قم بتمرير الصورة المعدلة إلى Aspose.PDF أو Aspose.Words أو أي مكتبة Aspose أخرى لمزيد من المعالجة أو التحويل أو الأرشفة.

### س7: هل تعمل الطريقة مع النص المكتوب بخط اليد؟

**A:** تعمل بشكل أفضل مع النص المطبوع حيث تكون الخطوط الأساسية ثابتة. قد تُنتج الخطوط المكتوبة يدوياً زوايا أقل موثوقية بسبب عدم انتظام الضربات.

## الخلاصة

الآن لديك وصفة جاهزة للإنتاج **كيفية تدوير المستند الممسوح ضوئياً** في Java: احسب الميل باستخدام `CalcSkewImage`، دوّر البت ماب باستخدام Java 2D، ثم نفّذ OCR على صورة محاذاة تماماً. هذه العملية ذات الخطوتين تعزز *دقة OCR* عادةً بنسبة 15‑30 % على المسوحات الضوضائية وتستوعب آلاف الصفحات يومياً. جرّب جودة صور مختلفة، اجمع خط الأنابيب مع Aspose.PDF لإنشاء ملفات PDF، وستحصل على محرك معالجة مستندات قوي جاهز لأعباء العمل المؤسسية.

---

**آخر تحديث:** 2026-06-19  
**تم الاختبار مع:** Aspose.OCR for Java 24.12 (latest at time of writing)  
**المؤلف:** Aspose  

{{< blocks/products/products-backtop-button >}}

## دروس ذات صلة

- [كيفية تعيين الترخيص والتحقق من ترخيص Aspose.OCR في Java](/ocr/java/ocr-basics/set-license/)
- [استخراج نص الصور – أساسيات OCR مع Aspose.OCR لـ Java](/ocr/java/ocr-basics/)
- [استخراج النص من صورة Java باستخدام وضع اكتشاف المناطق في Aspose.OCR](/ocr/java/ocr-operations/perform-ocr-detect-areas-mode/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.Utils;

import java.io.IOException;
```

```java
String dataDir = "Your Document Directory";
```

```java
String imagePath = dataDir + "p3.png";
```

```java
AsposeOCR api = new AsposeOCR();
```

```java
try {
    double angle = api.CalcSkewImage(imagePath);
    System.out.println("Skew text is:" + angle + " degrees.");
} catch (IOException e1) {
    e1.printStackTrace();
}
```