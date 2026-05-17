---
category: general
date: 2026-02-14
description: استخراج النص من الصورة باستخدام Aspose OCR. تعلّم كيفية تحميل الصورة
  للتعرف الضوئي على الأحرف، قراءة النص من المستطيل، واتبع هذا الدرس التعليمي لـ Aspose
  OCR خلال دقائق.
draft: false
keywords:
- extract text from image
- load image for ocr
- read text from rectangle
- aspose ocr tutorial
language: ar
og_description: استخراج النص من الصورة فورًا. يوضح هذا الدليل كيفية تحميل الصورة للتعرف
  الضوئي على الحروف، قراءة النص من داخل مستطيل، وإكمال دليل Aspose OCR.
og_title: استخراج النص من الصورة باستخدام Aspose OCR – دليل سريع
tags:
- Aspose
- OCR
- Java
title: استخراج النص من الصورة باستخدام Aspose OCR – عرض توضيحي خطوة بخطوة
url: /ar/java/ocr-operations/extract-text-from-image-with-aspose-ocr-step-by-step-demo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من الصورة باستخدام Aspose OCR – عرض خطوة بخطوة

هل احتجت يومًا إلى **استخراج النص من الصورة** لكن لم تكن متأكدًا من أين تبدأ؟ لست وحدك—العديد من المطورين يواجهون هذه المشكلة عندما يبدؤون في مسح الفواتير أو التحقق من الهوية. الخبر السار؟ مع Aspose OCR يمكنك تحميل صورة، تحديد المنطقة الدقيقة التي يتواجد فيها النص، واستخراج الأحرف ببضع أسطر.

في هذا **aspose ocr tutorial** سنستعرض كل ما تحتاجه: تحميل الصورة للـ OCR، ضبط مستطيل يحدد للـ engine أين يبحث، وأخيرًا قراءة النص المستخرج. في النهاية ستحصل على برنامج Java قابل للتنفيذ يطبع نص الـ ROI إلى وحدة التحكم—بدون غموض، مجرد حل واضح وعامل.

## ما ستحتاجه

قبل أن نبدأ، تأكد من أن لديك الأساسيات مغطاة:

| المتطلبات المسبقة | لماذا يهم |
|------------------|-----------|
| **Java JDK 8+** | Aspose OCR تُوزَّع كمكتبة Java؛ أي JDK حديث يكفي. |
| **Aspose.OCR for Java** (قم بتنزيله من موقع Aspose أو أضفه عبر Maven) | يوفر `OcrEngine` و `ImageStream` والفئات المرتبطة. |
| **ملف صورة** (مثال: `receipt.jpg`) يحتوي على نص قابل للطباعة | سنوجه الـ engine إلى مستطيل داخل هذا الملف. |
| **IDE أو محرر** (IntelliJ, Eclipse, VS Code…) | يساعدك على تجميع وتشغيل العينة بسرعة. |

إذا كنت تستخدم Maven، أضف هذه الاعتمادية إلى ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check Aspose for the latest version -->
</dependency>
```

> **نصيحة احترافية:** رقم الإصدار أعلاه هو الحالي حتى فبراير 2026. التحديث إلى أحدث إصدار يضمن حصولك على إصلاحات الأخطاء وتحسينات الأداء.

## الخطوة 1 – تهيئة محرك OCR

أولًا وقبل كل شيء: تحتاج إلى نسخة من `OcrEngine`. فكر فيها كالعقل الذي سيحلل البكسلات.

```java
// Step 1: Create the OCR engine object
OcrEngine ocrEngine = new OcrEngine();
```

لماذا ننشئه بهذه الطريقة؟ تقوم Aspose بفصل المحرك (الذي يحمل الإعدادات) عن بيانات الصورة، مما يمنحك مرونة لإعادة استخدام نفس المحرك لعدة صور إذا رغبت.

## الخطوة 2 – تحميل الصورة للـ OCR

الآن نقوم فعليًا **بتحميل الصورة للـ OCR**. تساعد الدالة `ImageStream.fromFile` في قراءة الملف إلى تدفق يمكن لـ Aspose فهمه.

```java
// Step 2: Load the target image (replace with your own path)
String imagePath = "YOUR_DIRECTORY/receipt.jpg";
ocrEngine.setImage(ImageStream.fromFile(imagePath));
```

إذا لم يُعثر على الملف، سيطرح المحرك استثناءً، لذا قد ترغب في تغليف ذلك بكتلة try‑catch في كود الإنتاج. في هذا العرض نترك الاستثناء يخرج—يحافظ على نظافة المثال.

## الخطوة 3 – تحديد المستطيل (قراءة النص من المستطيل)

هنا يبرز جزء **قراءة النص من المستطيل**. أنت تخبر المحرك بالضبط أين يبحث، مما يسرّع المعالجة ويقلل الإيجابيات الزائفة.

```java
// Step 3: Create a rectangle that covers the area with the receipt total
// Parameters: x, y, width, height (all in pixels)
Rectangle regionOfInterest = new Rectangle(120, 350, 600, 200);
ocrEngine.getEngineOptions().setRegionOfInterest(regionOfInterest);
```

> **لماذا مستطيل؟**  
> معظم المستندات لها تخطيطات متوقعة—مثل الفاتورة حيث يظهر المبلغ دائمًا قرب الأسفل. بالتركيز على هذا الجزء، يتجاهل محرك OCR الرسومات غير ذات الصلة ويعزز الدقة.

**حالة حافة:** إذا تجاوز المستطيل حدود الصورة، تقوم Aspose بتقليصه بصمت، لكنك ستفقد البيانات. يمكن لفحص سريع أن يمنع ذلك:

```java
if (regionOfInterest.x + regionOfInterest.width > ocrEngine.getImage().getWidth() ||
    regionOfInterest.y + regionOfInterest.height > ocrEngine.getImage().getHeight()) {
    throw new IllegalArgumentException("ROI exceeds image dimensions.");
}
```

## الخطوة 4 – معالجة الصورة

بعد ضبط كل شيء، نطلب من المحرك تنفيذ سحره.

```java
// Step 4: Run OCR on the defined ROI
OcrResult ocrResult = ocrEngine.process();
```

نداء `process()` يُعيد كائن `OcrResult` يحتوي على النص المستخرج، درجات الثقة، وحتى الصناديق المحيطة بكل كلمة إذا احتجت إليها لاحقًا.

## الخطوة 5 – إخراج النص المستخرج

أخيرًا، اطبع النتيجة. في تطبيق حقيقي قد تخزنها في قاعدة بيانات أو تُرسلها إلى خدمة أخرى، لكن لهذا الدرس يكفي إخراج إلى وحدة التحكم.

```java
// Step 5: Display the recognized text
System.out.println("ROI text:");
System.out.println(ocrResult.getText());
```

**الناتج المتوقع** (بافتراض أن المستطيل التقط المبلغ الإجمالي في الفاتورة):

```
ROI text:
$12.34
```

إذا كان الـ ROI فارغًا أو الصورة غير واضحة، سترى سلسلة فارغة أو أحرف مشوشة. اضبط المستطيل، حسّن جودة الصورة، أو فعّل خيارات ما قبل المعالجة في Aspose (مثل `setAutoSkewCorrection(true)`).

## مثال كامل يعمل

فيما يلي البرنامج الكامل الجاهز للتنفيذ. انسخه إلى ملف باسم `RoiDemo.java`، عدل مسار الصورة، ثم نفّذ `javac RoiDemo.java && java RoiDemo`.

```java
import com.aspose.ocr.*;
import java.awt.Rectangle;

/**
 * Demo: Extract text from a specific rectangle (ROI) in an image using Aspose OCR.
 * Adjust the rectangle coordinates to match the area you want to read.
 */
public class RoiDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image for OCR
        // Replace YOUR_DIRECTORY with the actual folder containing receipt.jpg
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.jpg"));

        // Step 3: Define the region of interest where text is expected
        // (x, y, width, height) in pixels
        Rectangle regionOfInterest = new Rectangle(120, 350, 600, 200);
        ocrEngine.getEngineOptions().setRegionOfInterest(regionOfInterest);

        // Optional sanity check – ensures ROI fits inside the image
        if (regionOfInterest.x + regionOfInterest.width > ocrEngine.getImage().getWidth() ||
            regionOfInterest.y + regionOfInterest.height > ocrEngine.getImage().getHeight()) {
            throw new IllegalArgumentException("ROI exceeds image dimensions.");
        }

        // Step 4: Perform OCR on the defined ROI
        OcrResult ocrResult = ocrEngine.process();

        // Step 5: Output the extracted text
        System.out.println("ROI text:");
        System.out.println(ocrResult.getText());
    }
}
```

> **التحقق من النتيجة:** بعد التشغيل، قارن مخرجات وحدة التحكم بالنص الفعلي داخل المستطيل. إذا تطابقت، فقد نجحت في **استخراج النص من الصورة** باستخدام Aspose OCR.

## أسئلة شائعة ونصائح

### ماذا لو احتجت إلى معالجة عدة مناطق ROI في نفس الصورة؟

أنشئ `Rectangle` جديد لكل منطقة، استدعِ `setRegionOfInterest` مرة أخرى، وأعد تشغيل `process()`. يعيد المحرك استخدام بيانات الصورة نفسها، لذا يبقى الأداء سريعًا.

### كيف تتعامل Aspose مع اللغات أو الخطوط المختلفة؟

يمكنك تغيير نموذج اللغة عبر `ocrEngine.getEngineOptions().setLanguage(OcrLanguage.English)`. للخطوط غير اللاتينية، حمّل حزمة اللغة المناسبة (متوفرة على صفحة تحميل Aspose).

### هل تدعم المكتبة إدخال PDF؟

نعم—يمكن لـ Aspose OCR قبول تدفقات PDF مباشرة. فقط استبدل `ImageStream.fromFile` بـ `ImageStream.fromPdfFile("doc.pdf")` ويمكنك تحديد رقم الصفحة اختياريًا.

### هل يمكن تحسين الدقة في المسحات منخفضة الجودة؟

فعّل ما قبل المعالجة:

```java
ocrEngine.getEngineOptions().setAutoSkewCorrection(true);
ocrEngine.getEngineOptions().setBinarizationMethod(BinarizationMethod.Otsu);
```

## الخلاصة

لقد استعرضنا للتو **aspose ocr tutorial** كامل يوضح كيفية **استخراج النص من الصورة**، **تحميل الصورة للـ OCR**، و**قراءة النص من المستطيل** باستخدام Java. الخطوات الأساسية هي تهيئة المحرك، إمداده بصورة، تحديد منطقة الاهتمام، المعالجة، وأخيرًا طباعة النتيجة.

من هنا قد تستكشف:

* **المعالجة الدفعية** – تكرار عبر مجلد من الفواتير وتخزين كل مبلغ في قاعدة بيانات.  
* **اكتشاف ROI ديناميكي** – استخدم مكتبات معالجة الصور (OpenCV) لتحديد كتل النص تلقائيًا.  
* **ما بعد المعالجة** – تطبيق تعبيرات regex أو المطابقة الضبابية لتنظيف عيوب OCR.

جرّب هذه الأفكار، عدّل المستطيل ليناسب مستنداتك، وستحصل على خط أنابيب استخراج نص قوي في وقت قصير. برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}