---
category: general
date: 2026-02-19
description: استخراج النص من الصورة باستخدام Aspose OCR Java – تعلم كيفية تحويل PNG
  إلى نص، تحميل الصورة للتعرف الضوئي على الأحرف، واتبع دليل OCR بلغة Java.
draft: false
keywords:
- extract text from image
- convert png to text
- load image for ocr
- java ocr tutorial
- Aspose OCR Java
- OCR language support
language: ar
og_description: استخراج النص من الصورة باستخدام Aspose OCR Java. اتبع هذا الدليل خطوة
  بخطوة لتقنية OCR في Java لتحويل PNG إلى نص وتحميل الصورة للتعرف الضوئي على الأحرف.
og_title: استخراج النص من الصورة – دليل Java OCR
tags:
- OCR
- Java
- Aspose
- Image Processing
title: استخراج النص من الصورة – تحويل PNG إلى نص في جافا
url: /ar/java/ocr-basics/extract-text-from-image-convert-png-to-text-in-java/
---

Be careful with bold formatting: keep **text**.

Also code block placeholders remain unchanged.

Proceed.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من الصورة – دليل Java OCR

هل احتجت يومًا إلى **استخراج النص من الصورة** لكنك لم تكن متأكدًا أي مكتبة ستمكنك من ذلك دون عناء؟ لست وحدك—المطورون يسألون باستمرار، “كيف يمكنني تحويل PNG إلى نص في Java؟” الخبر السار هو أن Aspose OCR يجعل العملية بأكملها سهلة كالمشي في الحديقة. في هذا الدليل سنستعرض **دليل java ocr كامل**، ونظهر لك كيفية **تحميل الصورة للـ OCR**، وسنحصل على نص نظيف وقابل للبحث.

سنغطي كل شيء من إعداد المحرك إلى التعامل مع المحتوى متعدد اللغات، بحيث تكون في النهاية قادرًا على **استخراج النص من الصورة** لأي حجم أو تنسيق أو لغة. لا خدمات خارجية، لا مفاتيح API—فقط ملف JAR واحد وقليل من الأسطر البرمجية.

## ما ستحتاجه

- JDK 8 أو أحدث مثبت (الكود يعمل على JDK 11+ أيضًا).  
- Maven أو Gradle لسحب مكتبة Aspose OCR، أو يمكنك تنزيل ملف JAR يدويًا من موقع Aspose.  
- صورة PNG تحتوي على نص قابل للقراءة (للمثال سنستخدم `khmer-sign.png`).  
- بيئة تطوير أو محرر نصوص تشعر بالراحة معه—IntelliJ IDEA، Eclipse، VS Code، أيًا كان.

هذا كل شيء. لا أطر ثقيلة، لا بيانات اعتماد سحابية. جاهز؟ لنبدأ باستخراج النص من ملفات الصورة.

## الخطوة 1: إضافة Aspose OCR إلى مشروعك

أولًا وقبل كل شيء—تحتاج إلى محرك OCR في مسار الفئة (classpath). إذا كنت تستخدم Maven، أضف هذا الاعتماد إلى `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check the latest version on Maven Central -->
</dependency>
```

أو باستخدام Gradle:

```groovy
implementation 'com.aspose:aspose-ocr:23.10'
```

إذا كنت تفضل الطريقة اليدوية، قم بتنزيل ملف JAR من صفحة تحميل Aspose وضعه في مجلد `libs` الخاص بمشروعك، ثم أضفه إلى مسار البناء.

> **نصيحة احترافية:** دائمًا اختر أحدث نسخة مستقرة؛ الإصدارات القديمة قد تفتقد حزم اللغات أو تصحيحات الأخطاء.

## الخطوة 2: إنشاء كائن OcrEngine

الآن بعد أن المكتبة متاحة، يمكننا إنشاء كائن `OcrEngine`. فكر في المحرك كالعقل الذي سيقرأ البكسلات ويحولها إلى أحرف.

```java
import com.aspose.ocr.*;

public class ExtractTextExample {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
        // ... further steps will follow
    }
}
```

لماذا ننشئ محركًا جديدًا في كل مرة؟ المحرك يحتفظ بذاكرات داخلية وبيانات اللغة؛ البدء من الصفر يضمن نتائج حتمية، خاصةً عندما تقوم بتغيير اللغات لاحقًا.

## الخطوة 3: تمكين اللغة المطلوبة (اختياري لكن مُستحسن)

Aspose OCR يأتي مع عشرات حزم اللغات. إذا كنت تعرف لغة الصورة المصدر، فعّلها صراحةً؛ هذا يسرّع التعرف ويحسّن الدقة. في مثالنا سنفعّل اللغة الخميرية (`khm`)، لكن يمكنك استبدالها بـ `ENG` للإنجليزية، `CHN` للصينية، إلخ.

```java
// Enable Khmer language support (ISO 639‑2 code "khm")
ocrEngine.getLanguages().add(OcrLanguage.KHM);
```

> **لماذا هذا مهم:** عندما **تحمّل الصورة للـ OCR**، سيبحث المحرك فقط في القواميس الخاصة باللغات المفعّلة. ترك جميع اللغات مفعّلة قد يبطئ العملية ويزيد من الإيجابيات الزائفة.

## الخطوة 4: تحميل الصورة للـ OCR – تحويل PNG إلى نص

هنا يحدث خطوة **تحميل الصورة للـ OCR**. توفر Aspose أداة مساعدة `ImageStream.fromFile` التي تُبسط التعامل مع الإدخال/الإخراج منخفض المستوى.

```java
// Load the PNG that contains the text you want to extract
ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/khmer-sign.png"));
```

إذا كانت صورتك بتنسيق آخر (JPEG، BMP، TIFF)، تعمل نفس الطريقة—Aspose يكتشف التنسيق تلقائيًا. فقط تأكد من صحة مسار الملف؛ وإلا ستواجه استثناء `FileNotFoundException`.

## الخطوة 5: تشغيل عملية OCR وتحويل PNG إلى نص

مع جاهزية المحرك وتحميل الصورة، يصبح التعرف الفعلي استدعاءً لطريقة واحدة. كائن النتيجة يمنحك السلسلة الخام بالإضافة إلى درجات الثقة.

```java
// Run OCR and fetch the recognized text
String recognizedText = ocrEngine.recognize().getText();
```

هذا كل شيء—لقد **حولت PNG إلى نص**. قد تحتوي السلسلة المعادة على فواصل أسطر ومسافات كما رآها المحرك. يمكنك معالجة ما بعد ذلك باستخدام `trim()`, `replaceAll("\\s+", " ")` أو أي تنظيف آخر تحتاجه.

## الخطوة 6: إخراج النتيجة (أو تخزينها)

لإجراء فحص سريع، اطبع النتيجة على وحدة التحكم. في تطبيق حقيقي ربما تكتبها إلى ملف، قاعدة بيانات، أو تمرّرها إلى خدمة أخرى.

```java
System.out.println("Recognized text:");
System.out.println(recognizedText);
```

**الناتج المتوقع** (للعلامة الخميرية المقدمة) قد يبدو هكذا:

```
សួស្តី
Welcome
```

إذا كان الناتج مشوشًا، تأكد من أنك فعّلت اللغة الصحيحة في الخطوة 3 وأن الصورة ليست ضبابية جدًا. زيادة دقة الصورة (مثلاً مسح بدقة 300 dpi) غالبًا ما يساعد.

## مثال كامل يعمل

بجمع كل الأجزاء معًا، إليك برنامج مستقل يمكنك نسخه ولصقه في `ExtractTextExample.java` وتشغيله:

```java
import com.aspose.ocr.*;

public class ExtractTextExample {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Enable the language you need (Khmer in this case)
        ocrEngine.getLanguages().add(OcrLanguage.KHM);

        // 3️⃣ Load the PNG image you want to extract text from
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/khmer-sign.png"));

        // 4️⃣ Run OCR – this step actually converts PNG to text
        String recognizedText = ocrEngine.recognize().getText();

        // 5️⃣ Show the result
        System.out.println("=== OCR Result ===");
        System.out.println(recognizedText);
    }
}
```

شغّل البرنامج باستخدام:

```bash
mvn compile exec:java -Dexec.mainClass=ExtractTextExample
```

أو، إذا كنت تستخدم Gradle:

```bash
./gradlew run --args='ExtractTextExample'
```

يجب أن ترى النص المستخرج يُطبع على وحدة التحكم، مؤكدًا أنك نجحت في **استخراج النص من الصورة** باستخدام Aspose OCR.

## المشكلات الشائعة وكيفية إصلاحها

| العَرَض | السبب المحتمل | الحل |
|---------|--------------|-----|
| إرجاع سلسلة فارغة | لم يتم تمكين لغة أو تم إدخال رمز لغة خاطئ | أضف `OcrLanguage` المناسب (مثال: `ENG` للإنجليزية). |
| أحرف مشوشة | دقة الصورة منخفضة أو خلفية صاخبة | استخدم مصدرًا بدقة أعلى، أو عالج الصورة بفلتر شحذ. |
| `OutOfMemoryError` | تحميل صورة كبيرة بحجمها الكامل | قلل حجم الصورة قبل تمريرها إلى المحرك (`ImageStream.fromFile(...).scale(0.5)`). |
| `FileNotFoundException` | مسار غير صحيح | تحقق من المسار المطلق أو النسبي؛ استخدم `Paths.get(...).toAbsolutePath()`. |

> **تذكر:** OCR عملية احتمالية. حتى مع الإعدادات المثالية قد تحتاج إلى تصحيح بعض الأحرف يدويًا، خاصةً للخطوط المتصلة.

## توسيع الدرس – الخطوات التالية

- **المعالجة الدفعية:** تكرار عبر مجلد يحتوي على ملفات PNG، واستدعاء نفس المنطق لكل صورة.  
- **إخراج PDF:** استخدم Aspose PDF لدمج النص المستخرج داخل PDF قابل للبحث.  
- **اكتشاف اللغة:** استدعِ `ocrEngine.detectLanguage()` قبل تعيين لغة لتسمح للمحرك بالتخمين تلقائيًا.  
- **التكامل السحابي:** إذا احتجت إلى التوسع، غلف الكود في نقطة نهاية REST ودع الخدمات المصغرة تستدعيه.

كل هذه المواضيع تبني بشكل طبيعي على **دليل java ocr** الذي أنجزناه للتو، وتظهر مدى مرونة Aspose OCR API حقًا.

## الخلاصة

لقد استعرضنا دليلًا **java ocr** كاملًا يتيح لك **استخراج النص من الصورة**، **تحويل PNG إلى نص**، و**تحميل الصورة للـ OCR** بشكل صحيح باستخدام Aspose OCR. الخطوات بسيطة: أضف المكتبة، أنشئ محركًا، فعّل اللغة المناسبة، حمّل PNG، نفّذ `recognize()`، وتعامل مع الناتج. مع هذه الأساسيات يمكنك أتمتة إدخال البيانات، بناء أرشيفات قابلة للبحث، أو تشغيل أي تطبيق يحتاج نصًا قابلًا للقراءة آليًا من الصور.

جرّبه مع صورك الخاصة—ربما لقطة شاشة لإيصال أو عقد ممسوح. عدّل إعدادات اللغة، جرب دقة مختلفة، وسترى بسرعة مدى مرونة الحل. إذا واجهت مشكلة، راجع جدول المشكلات أو راجع الوثائق الرسمية لـ Aspose؛ فهي شاملة ومحدثة باستمرار.

برمجة سعيدة، ولتكن مشروعك القادم مليئًا بنص نظيف وقابل للبحث!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}