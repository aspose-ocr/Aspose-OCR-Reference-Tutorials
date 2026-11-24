---
category: general
date: 2026-06-19
description: إزالة الانحراف التلقائي للصورة باستخدام Aspose OCR في جافا. تعلّم كيفية
  تصحيح الانحراف، استخراج النص باستخدام OCR والحصول على زاوية الإزالة في بضع خطوات
  سهلة.
draft: false
keywords:
- auto deskew image
- extract text ocr
- how to correct skew
- how to get deskew
language: ar
og_description: تصحيح ميل الصورة تلقائيًا باستخدام Aspose OCR في جافا. اكتشف كيفية
  تصحيح الميل، استخراج النص عبر OCR، واسترجاع زاوية التصحيح—كل ذلك في دليل واحد.
og_title: إزالة الانحراف التلقائي للصورة في جافا – دليل Aspose OCR الكامل
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Auto deskew image using Aspose OCR in Java. Learn how to correct skew,
    extract text OCR and get deskew angle in a few easy steps.
  headline: Auto Deskew Image in Java – Complete Aspose OCR Guide
  type: TechArticle
tags:
- Aspose OCR
- Java
- Image Processing
title: تصحيح الميل التلقائي للصورة في جافا – دليل Aspose OCR الكامل
url: /ar/java/ocr-operations/auto-deskew-image-in-java-complete-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تصحيح الميل التلقائي للصور في Java – دليل Aspose OCR الكامل

هل تساءلت يومًا كيف تقوم بـ **auto deskew image** للملفات قبل تشغيل OCR؟ ربما التقطت إيصالًا على طاولة مائلة، أو وصل نموذجًا ممسوحًا ضوئيًا بميل طفيف، وانتهى استخراج النص إلى تشويه. هذه مشكلة شائعة، خاصة عندما تحتاج إلى نتائج **extract text OCR** موثوقة للمعالجة اللاحقة.

في هذا الدرس سنستعرض الخطوات الدقيقة لـ **auto deskew image** للملفات باستخدام Aspose OCR for Java، ونظهر لك **how to correct skew**، ونكشف **how to get deskew** بعد انتهاء المحرك. في النهاية، ستحصل على برنامج Java جاهز للتشغيل لا يقوم فقط بتصحيح الصور تلقائيًا بل يستخرج النص النظيف منها. لا إطالة، فقط كود عملي وشروحات يمكنك نسخها ولصقها اليوم.

## ما ستتعلمه

- تحميل وترخيص Aspose OCR في مشروع Java.  
- تفعيل ميزة التصحيح التلقائي للميل في المحرك.  
- ضبط عتبة الثقة لتجنب التصحيح الزائد.  
- تشغيل OCR على صورة مائلة واسترجاع زاوية التصحيح المطبقة.  
- استخراج النص المعترف به مع نتائج مدفوعة بالثقة.  

**المتطلبات المسبقة** – SDK Java 8+، Maven أو Gradle لإدارة الاعتمادات، وملف ترخيص Aspose OCR. إذا كنت جديدًا على Maven، لا تقلق؛ سنغطي الجزء الأدنى من `pom.xml` الذي تحتاجه.

---

## ## Auto Deskew Image with Aspose OCR – الخطوة 1: إعداد المشروع

أولاً، لنضيف المكتبة إلى مشروعك. أضف الاعتمادية التالية إلى `pom.xml` الخاص بك (أو ما يعادلها في Gradle):

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check for the latest version -->
</dependency>
```

> **نصيحة احترافية:** راقب رقم الإصدار؛ فـ Aspose تصدر باستمرار تحسينات أداء لخوارزميات تصحيح الميل.

بعد أن يقوم Maven بحل الاعتمادية، أنشئ فئة Java بسيطة تسمى `SkewDemo`. ستكون هذه مساحة التجربة حيث نوضح **how to correct skew** و **how to get deskew**.

---

## ## How to Correct Skew – الخطوة 2: ترخيص وتهيئة المحرك

قبل أن تتمكن من استدعاء أي طريقة OCR، يجب تحميل الترخيص الخاص بك. وإلا، ستعمل المكتبة في وضع التقييم وتحد من عدد الصفحات التي يمكنك معالجتها.

```java
import com.aspose.ocr.*;

public class SkewDemo {
    public static void main(String[] args) throws Exception {
        // Load the Aspose OCR license (replace with your actual path)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

لاحظ كيف تم عزل خطوة الترخيص في الأعلى—هذا يعكس أفضل الممارسات حيث يكون الترخيص إعدادًا مرة واحدة، لا يتكرر لكل صورة. إذا نسيت ذلك، سيطرح المحرك استثناء ترخيص، وهو عائق شائع للمبتدئين.

---

## ## How to Get Deskew – الخطوة 3: تفعيل Auto‑Deskew وضبط الثقة

الآن نقوم بإنشاء محرك OCR ونخبره بـ **auto deskew image** تلقائيًا. استدعاء `setAutoDeskew(true)` يفعّل الخوارزمية الداخلية التي تكتشف زاوية الدوران وتدوير الصورة مرة أخرى إلى خط أفقي.

```java
        // Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Enable automatic deskewing
        ocrEngine.setAutoDeskew(true);                     // auto deskew image
        // Define how confident the engine must be before applying the correction
        ocrEngine.setDeskewConfidenceThreshold(0.85);     // 85% confidence is a safe default
```

لماذا عتبة الثقة؟ تخيل صورة لوحة إعلانات مأخوذة بزاوية غريبة؛ قد يخمن المحرك دورانًا كبيرًا ويفسد النص. بتعيين `0.85`، نقول "طبق التصحيح فقط إذا كنا على الأقل 85 % متأكدين". يمكنك تعديل هذه القيمة أعلى أو أقل حسب مدى ضوضاء مجموعة الصور.

---

## ## Extract Text OCR – الخطوة 4: التعرف على الصورة

مع جاهزية المحرك، زوده بمسار الصورة المائلة. الطريقة `recognizeImage` تقوم بكل من تصحيح الميل (إذا كان مفعلاً) و OCR في تمريرة واحدة.

```java
        // Recognize text from a skewed image
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/angled-photo.jpg");
```

إذا لم يُعثر على الملف، سيطرح Java استثناء `FileNotFoundException`. تحقق سريعًا—تأكد أن المسار مطلق أو نسبي إلى دليل العمل الذي تشغل البرنامج منه.

---

## ## Auto Deskew Image – الخطوة 5: استرجاع زاوية التصحيح والنص المستخرج

بعد التعرف، يعطينا كائن `OcrResult` قطعتين من الذهب: الزاوية التي طبقها المحرك والنص العادي المستخرج.

```java
        // Print the applied deskew angle
        System.out.println("Applied angle: " + ocrResult.getAppliedDeskewAngle());

        // Print the extracted text
        System.out.println("Extracted text:");
        System.out.println(ocrResult.getText());
    }
}
```

طريقة `getAppliedDeskewAngle()` تُرجع قيمة `double` تمثل الدرجات (موجبة للدوران مع اتجاه عقارب الساعة). إذا كانت الصورة مستوية بالفعل، ستحصل على `0.0`. هذا هو جوهر **how to get deskew**، ويمكن تسجيله لسجلات التدقيق أو إرجاعه إلى واجهة المستخدم لإظهار التصحيح الذي حدث في الخلفية.

---

## ## Full Working Example – كل الخطوات في ملف واحد

فيما يلي الفئة الكاملة الجاهزة للتشغيل في Java. انسخها إلى IDE الخاص بك، استبدل مسارات الترخيص والصورة، واضغط *Run*.

```java
import com.aspose.ocr.*;

public class SkewDemo {
    public static void main(String[] args) throws Exception {
        // -------------------- Step 1: License --------------------
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic"); // <-- update path

        // -------------------- Step 2: Engine --------------------
        OcrEngine ocrEngine = new OcrEngine();

        // -------------------- Step 3: Auto‑Deskew --------------------
        ocrEngine.setAutoDeskew(true);                     // auto deskew image
        ocrEngine.setDeskewConfidenceThreshold(0.85);     // high‑confidence only

        // -------------------- Step 4: Recognize --------------------
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/angled-photo.jpg"); // <-- update path

        // -------------------- Step 5: Results --------------------
        System.out.println("Applied angle: " + ocrResult.getAppliedDeskewAngle());
        System.out.println("Extracted text:");
        System.out.println(ocrResult.getText());
    }
}
```

**الناتج المتوقع** (مثال):

```
Applied angle: -2.7
Extracted text:
Invoice #12345
Date: 2024‑04‑01
Total: $89.99
Thank you for your business!
```

لاحظ أن الزاوية رقم سالب صغير—مما يعني أن الصورة الأصلية كانت مائلة بضع درجات عكس اتجاه عقارب الساعة، وقد صحّحها Aspose قبل OCR.

---

## ## المشكلات الشائعة وحالات الحافة

| المشكلة | لماذا يحدث | الحل |
|-------|----------------|-----|
| **لم يتم تطبيق تصحيح الميل (angle = 0)** | الصورة مستوية بالفعل أو الثقة أقل من العتبة. | قلل `setDeskewConfidenceThreshold` إلى `0.6` للماسحات الضوضائية. |
| **حروف عشوائية في الناتج** | جودة الصورة منخفضة جدًا؛ الضوضاء تتداخل مع كل من تصحيح الميل و OCR. | قم بالمعالجة المسبقة بفلتر تنعيم أو زد DPI قبل إمداد Aspose. |
| **الترخيص غير موجود** | مسار غير صحيح أو ملف مفقود. | استخدم مسارًا مطلقًا أو ضع ملف `.lic` في classpath واستدعِ `license.setLicense("Aspose.OCR.lic");`. |
| **نفاد الذاكرة في دفعات كبيرة** | كل استدعاء يحمل الصورة بالكامل في الذاكرة. | أعد استخدام كائن `OcrEngine` واحد واستدعِ `ocrEngine.clear()` بعد كل صورة. |

---

## ## Going Further – الخطوات التالية

- **Batch processing:** معالجة دفعات: حلق عبر دليل يحتوي على صور، اجمع كل `appliedDeskewAngle`، وخزن النتائج في CSV للتحليلات.  
- **Language selection:** اختيار اللغة: استخدم `ocrEngine.setLanguage(OcrLanguage.English);` لتحسين الدقة للوثائق متعددة اللغات.  
- **Region‑based OCR:** OCR قائم على المنطقة: إذا كنت تهتم بمنطقة محددة فقط (مثل الباركود)، استدعِ `ocrEngine.recognizeRegion(rect);`.  

كل هذه الإضافات لا تزال تستفيد من أساس **auto deskew image** الذي بنيناه، لأن الصورة الموجهة بشكل صحيح هي العامل الأهم للحصول على OCR عالي الجودة.

---

## ## الخاتمة

لقد غطينا كل ما تحتاجه لتطبيق **auto deskew image** للملفات في Java باستخدام Aspose OCR، وأظهرنا **how to correct skew**، وبيّنّا **how to get deskew** للزوايا، وأخيرًا استخرجنا نصًا نظيفًا عبر **extract text OCR**. البرنامج القصير المستقل يعمل في ثوانٍ، لكنه يتعامل مع مشكلة معقدة كانت ستتطلب مكتبة معالجة صور منفصلة.

جرّبه مع صورك الخاصة، عدّل عتبة الثقة، وشاهد زاوية التصحيح تظهر في وحدة التحكم. بمجرد أن تشعر بالراحة، أضف منطق الدفعات أو دمج الناتج في خط أنابيب إدارة المستندات. السماء هي الحد—فقط تذكر أن الصورة المستقيمة هي المكوّن السري وراء OCR موثوق.

إذا واجهت أي مشاكل، اترك تعليقًا أدناه أو راجع وثائق Aspose الرسمية لـ Java للحصول على أحدث تعديلات API. ترميز سعيد، ولتظل مسحاتك دائمًا مستوية! 

![مخطط يوضح التصحيح التلقائي للميل لصورة مائلة قبل استخراج OCR – عملية auto deskew image](auto-deskew-diagram.png "auto deskew image workflow")

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية حساب زاوية الميل في Java باستخدام Aspose.OCR](/ocr/english/java/ocr-basics/calculate-skew-angle/)
- [التعرف على نص الصورة باستخدام Aspose OCR – دليل Java OCR كامل](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [استخراج النص من صورة Java باستخدام Aspose.OCR وضع اكتشاف المناطق](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}