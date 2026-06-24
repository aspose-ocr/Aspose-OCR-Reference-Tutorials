---
category: general
date: 2026-06-16
description: تحميل صورة للتعرف الضوئي على الأحرف واستخراج النص بسرعة من منطقة باستخدام
  Aspose OCR في Java. دليل خطوة بخطوة مع الكود الكامل، النصائح، ومعالجة الحالات الخاصة.
draft: false
keywords:
- load image for OCR
- extract text from region
- Aspose OCR Java
- OCR region processing
- Java image recognition
language: ar
og_description: تحميل صورة للتعرف الضوئي على الأحرف في جافا واستخراج النص من منطقة
  باستخدام Aspose OCR. دليل كامل مع الشيفرة، الشروحات، وأفضل الممارسات.
og_title: تحميل الصورة للتعرف الضوئي على الأحرف – دليل استخراج المنطقة في جافا
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: load image for OCR and quickly extract text from region using Aspose
    OCR in Java. Step‑by‑step guide with full code, tips, and edge‑case handling.
  headline: load image for OCR, extract text from region – Java
  type: TechArticle
- description: load image for OCR and quickly extract text from region using Aspose
    OCR in Java. Step‑by‑step guide with full code, tips, and edge‑case handling.
  name: load image for OCR, extract text from region – Java
  steps:
  - name: Create the OCR engine and **load image for OCR**
    text: First we instantiate `OcrEngine` and point it at the file we want to process.
      The `ImageStream.fromFile` helper takes care of reading the bytes and wrapping
      them in a format the engine understands.
  - name: Define the **region** you want to **extract text from region**
    text: A `java.awt.Rectangle` describes the X/Y offset and the width/height of
      the area you care about. The numbers are pixel‑based, so you may need to experiment
      a bit with your particular document.
  - name: Apply the region to the engine
    text: The `RecognitionSettings` object holds all the knobs you can turn. Here
      we simply set the region we just created.
  - name: Run the OCR – the engine will also deskew the region automatically
    text: 'Calling `recognize()` does the heavy lifting: it deskews, binarizes, and
      runs the character recognizer on the defined rectangle.'
  - name: '**Extract text from region** and display it'
    text: Finally we pull the plain‑text representation out of the `OcrResult`. Trimming
      removes stray line breaks and spaces.
  type: HowTo
tags:
- Java
- OCR
- Aspose
- Image Processing
title: تحميل صورة للتعرف الضوئي على الأحرف، استخراج النص من منطقة – جافا
url: /ar/java/ocr-operations/load-image-for-ocr-extract-text-from-region-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحميل صورة للتعرف الضوئي على الأحرف (OCR)، استخراج النص من منطقة – Java

هل احتجت يوماً إلى **load image for OCR** لكنك لم تكن متأكدًا من كيفية حصر الفحص على الجزء الذي يهمك فقط؟ لست وحدك. في العديد من المشاريع الواقعية—مثل الفواتير، النماذج، أو بطاقات الهوية—تريد فقط **extract text from region** التي تحتوي فعليًا على البيانات، وليس الصورة بأكملها.

في هذا الدرس سنستعرض مثالًا كاملاً وقابلاً للتنفيذ يوضح بالضبط كيفية تحميل صورة للتعرف الضوئي على الأحرف باستخدام Aspose OCR، تعريف منطقة مستطيلة، ثم استخراج النص من تلك المنطقة. في النهاية ستحصل على برنامج Java مستقل يمكنك إدراجه في أي مشروع Maven أو Gradle، بالإضافة إلى مجموعة من النصائح العملية للتعامل مع المشكلات الشائعة.

## ما ستحتاجه

| المتطلب | لماذا يهم |
|--------------|----------------|
| **Java 17** (أو أي JDK حديث) | Aspose OCR يُوزع كملف JAR متوافق مع Java 17. |
| **Aspose OCR for Java** library (قم بتنزيله من Aspose أو أضفه عبر Maven) | يوفر `OcrEngine` والفئات المرتبطة. |
| **ملف صورة** (مثال: `form.jpg`) يحتوي على الحقل الذي تريد قراءته | المحرك لا يمكنه معالجة إلا ما تزوده به. |
| **IDE جيد** (IntelliJ, Eclipse, VS Code) – اختياري لكنه مفيد | يسهل عملية تصحيح الأخطاء وتشغيل الكود. |

If you’re using Maven, add this dependency to your `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check Aspose for the latest version -->
</dependency>
```

*نصيحة احترافية:* نسخة التقييم المجانية تعمل جيدًا للاختبار، لكنها تضيف علامة مائية إلى الناتج. احصل على ترخيص كامل إذا كنت تخطط لنشر الحل.

## تحميل صورة للتعرف الضوئي على الأحرف – تنفيذ خطوة بخطوة

فيما يلي نقسم العملية إلى خمس خطوات واضحة. كل خطوة تتضمن مقتطف كود، شرحًا قصيرًا **لسبب** قيامنا بذلك، ونصيحة سريعة لتجنب الفخاخ الشائعة.

### الخطوة 1: إنشاء محرك OCR و **load image for OCR**

أولاً نقوم بإنشاء كائن `OcrEngine` ونشير إليه إلى الملف الذي نريد معالجته. تساعد الدالة `ImageStream.fromFile` في قراءة البايتات وتغليفها بصيغة يفهمها المحرك.

```java
import com.aspose.ocr.*;
import java.awt.Rectangle;

public class RoiOcr {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine and load the source image
        OcrEngine engine = new OcrEngine();
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/form.jpg"));
```

> **لماذا هذا مهم:**  
> يحتاج المحرك إلى صورة bitmap للعمل عليها. توفير مسار غير صحيح يسبب استثناء `FileNotFoundException`، لذا تحقق مرة أخرى من الموقع المطلق أو النسبي. إذا كانت صورتك في مجلد الموارد، استخدم `ClassLoader.getResourceAsStream` بدلاً من ذلك.

### الخطوة 2: تعريف **المنطقة** التي تريد **extract text from region**

كائن `java.awt.Rectangle` يصف إزاحة X/Y وعرض/ارتفاع المنطقة التي تهتم بها. الأرقام تعتمد على البكسل، لذا قد تحتاج إلى تجربة القيم قليلاً مع مستندك المحدد.

```java
        // Step 2: Define the rectangular region that contains the field to read
        Rectangle region = new Rectangle(120, 340, 560, 80); // x, y, width, height
```

> **لماذا هذا مهم:**  
> بتحديد محرك OCR على منطقة معينة، تحسن الدقة والسرعة بشكل كبير. لن يضيع المحرك الوقت في محاولة قراءة الصفحة بأكملها، ويتجنب الخلفية المزعجة التي قد تفسد النتيجة.

### الخطوة 3: تطبيق المنطقة على المحرك

كائن `RecognitionSettings` يحتوي على جميع الإعدادات التي يمكنك تعديلها. هنا نقوم ببساطة بتعيين المنطقة التي أنشأناها للتو.

```java
        // Step 3: Apply the region to the engine so only this area is processed
        engine.getRecognitionSettings().setRegion(region);
```

> **نصيحة:** إذا احتجت إلى معالجة حقول متعددة، يمكنك استدعاء `setRegion` بشكل متكرر داخل حلقة، وتحديث المستطيل في كل مرة قبل استدعاء `recognize()`.

### الخطوة 4: تشغيل OCR – سيقوم المحرك أيضًا بتصحيح الميل للمنطقة تلقائيًا

استدعاء `recognize()` يقوم بالعمل الشاق: يصحح الميل، ي二ثن (binarizes) ويشغل مُعرّف الأحرف على المستطيل المحدد.

```java
        // Step 4: Perform recognition (the engine will deskew the region automatically)
        OcrResult result = engine.recognize();
```

> **لماذا هذا مهم:**  
> تصحيح الميل يحل المشكلات الشائعة عندما لا يكون النموذج الممسوح محاذيًا بشكل كامل. بدونه، قد تحصل على أحرف مشوشة حتى لو كانت المنطقة صحيحة.

### الخطوة 5: **extract text from region** وعرضه

أخيرًا نستخرج تمثيل النص العادي من `OcrResult`. عملية القطع (trim) تزيل فواصل الأسطر والمسافات الزائدة.

```java
        // Step 5: Output the extracted text
        System.out.println("Field value: " + result.getText().trim());
    }
}
```

تشغيل البرنامج يطبع شيئًا مثل:

```
Field value: 12345-AB
```

هذه هي الدورة الكاملة: **load image for OCR**، حصر الفحص، و **extract text from region**.

## مثال كامل وقابل للتنفيذ (بدون قطع مفقودة)

إذا كنت تفضل نسخ‑لصق كل شيء مرة واحدة، إليك الفئة الكاملة، بما في ذلك عبارات الاستيراد ومقتطف `pom.xml` minimal لمستخدمي Maven.

```java
// File: RoiOcr.java
import com.aspose.ocr.*;
import java.awt.Rectangle;

public class RoiOcr {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine and load the source image
        OcrEngine engine = new OcrEngine();
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/form.jpg"));

        // Step 2: Define the rectangular region that contains the field to read
        Rectangle region = new Rectangle(120, 340, 560, 80); // x, y, width, height

        // Step 3: Apply the region to the engine so only this area is processed
        engine.getRecognitionSettings().setRegion(region);

        // Step 4: Perform recognition (the engine will deskew the region automatically)
        OcrResult result = engine.recognize();

        // Step 5: Output the extracted text
        System.out.println("Field value: " + result.getText().trim());
    }
}
```

```xml
<!-- pom.xml excerpt -->
<project>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>ocr-demo</artifactId>
    <version>1.0.0</version>
    <dependencies>
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-ocr</artifactId>
            <version>23.10</version>
        </dependency>
    </dependencies>
</project>
```

احفظ ملف Java، شغّل `mvn compile exec:java -Dexec.mainClass=RoiOcr`، ويجب أن ترى القيمة المستخرجة مطبوعة في وحدة التحكم.

![مخطط يوضح كيفية تحميل صورة للتعرف الضوئي على الأحرف وتحديد منطقة](/images/ocr-region-diagram.png "مثال تحميل صورة للتعرف الضوئي على الأحرف")

*التوضيح أعلاه يُظهر المستطيل (120, 340, 560, 80) فوق نموذج عينة.*

## التعامل مع الحالات الحدية الشائعة

| الموقف | ما الذي يجب مراقبته | حل سريع |
|-----------|-------------------|-----------|
| **الصورة مائلة بأكثر من 15°** | تصحيح الميل يعمل بشكل أفضل للزوايا الخفيفة. | قم بإعادة تدوير الصورة مسبقًا باستخدام `java.awt.Image` قبل تمريرها إلى المحرك. |
| **المنطقة تتجاوز حدود الصورة** | سيتم رمي استثناء `IllegalArgumentException`. | تحقق من أن `region.x + region.width <= imageWidth` وما شابه للـ Y. |
| **نص منخفض التباين** | تنخفض دقة OCR. | زد التباين برمجيًا أو استخدم `engine.getRecognitionSettings().setPreprocessOptions(PreprocessOptions.CONTRAST_ENHANCEMENT)`. |
| **لغات متعددة** | اللغة الافتراضية هي الإنجليزية. | استدعِ `engine.getRecognitionSettings().setLanguage(Language.FRENCH)` أو قدم قائمة. |

## نصائح احترافية لـ OCR على مستوى الإنتاج

1. **Cache the engine** – إنشاء `OcrEngine` جديد لكل صورة مكلف. أعد استخدام نفس المثيل عند المعالجة.

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة وعملية مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [استخراج نص من الصور – أساسيات OCR مع Aspose.OCR للـ Java](/ocr/english/java/ocr-basics/)
- [استخراج نص من صورة Java باستخدام وضع اكتشاف المناطق في Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [كيفية OCR نص الصورة مع اللغة باستخدام Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}