---
category: general
date: 2026-02-14
description: تعلم كيفية إجراء التعرف الضوئي على الحروف (OCR) على الصورة واستخراج النص
  من الصورة باستخدام Aspose OCR في Java. يتضمن تحميل الصورة للتعرف الضوئي على الحروف،
  القاموس المخصص وتصحيح الأخطاء الإملائية.
draft: false
keywords:
- perform OCR on image
- extract text from image
- load image for OCR
- Aspose OCR Java
- spell correction OCR
language: ar
og_description: إجراء التعرف الضوئي على الأحرف (OCR) على صورة في جافا باستخدام Aspose
  OCR. يوضح هذا الدليل كيفية تحميل الصورة للتعرف الضوئي على الأحرف، استخراج النص من
  الصورة، وتفعيل تصحيح الإملاء.
og_title: إجراء التعرف الضوئي على الأحرف في الصورة – دليل جافا الكامل
tags:
- OCR
- Java
- Aspose
title: تنفيذ OCR على صورة باستخدام Aspose OCR – دليل خطوة بخطوة بلغة Java
url: /ar/java/advanced-ocr-techniques/perform-ocr-on-image-with-aspose-ocr-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إجراء OCR على صورة – دليل Java كامل

هل احتجت يوماً إلى **perform OCR on image** لكنك لم تكن متأكدًا من أين تبدأ؟ لست وحدك؛ كثير من المطورين يواجهون نفس المشكلة عندما يحاولون استخراج النص من بيانات الصورة للمرة الأولى. الخبر السار هو أنه باستخدام Aspose OCR for Java يمكنك الحصول على نتائج موثوقة في بضع أسطر من الشيفرة — بالإضافة إلى إمكانية تحسين الدقة باستخدام قاموس مخصص وتدقيق إملائي.

في هذا الدليل سنستعرض كل ما تحتاج معرفته: من تحميل الصورة للـ OCR، إلى تمكين تصحيح الإملاء، وأخيرًا طباعة النص المنقح. بنهاية القراءة ستكون قادرًا على **perform OCR on image** في مشاريع Java الخاصة بك، وسترى أيضًا كيفية **extract text from image** بطريقة تعمل حتى مع المسحات الضوضائية.

## ما الذي ستحتاجه

قبل أن نبدأ، تأكد من أن لديك ما يلي جاهزًا:

- **Java Development Kit (JDK) 8+** – الشيفرة تستخدم واجهات برمجة تطبيقات Java القياسية.
- مكتبة **Aspose OCR for Java** (يمكنك الحصول على أحدث ملف JAR من موقع Aspose أو Maven Central).
- ملف صورة (مثال: `invoice.png`) تريد معالجته.
- (اختياري) ملف نصي عادي `custom_dict.txt` يحتوي على كلمات خاصة بالمجال، كلمةً واحدةً في كل سطر.

هذا كل شيء — لا أطر عمل ثقيلة، ولا خدمات خارجية. مجرد Java صافية وملف JAR الخاص بـ Aspose OCR.

## الخطوة 1: إعداد المشروع واستيراد الاعتمادات

أولاً، أنشئ مشروع Maven (أو Gradle) جديد وأضف اعتماد Aspose OCR. إذا كنت تستخدم Maven، يجب أن يحتوي ملف `pom.xml` على:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Check for the latest version -->
</dependency>
```

إذا كنت تفضّل تحميل ملف JAR يدويًا، ضعّه في مجلد `libs` وأضفه إلى مسار الـ classpath.

> **نصيحة محترف:** تحقق دائمًا من رقم الإصدار في وقت الكتابة؛ الإصدارات الأحدث قد تضيف ميزات إضافية مثل حزم اللغات.

## الخطوة 2: تحميل الصورة للـ OCR

الخطوة البرمجية الأولى هي توجيه محرك OCR إلى الصورة التي تريد تحليلها. يستخدم Aspose OCR غلافًا من نوع `ImageStream`، يمكنه القراءة من ملف، أو مصفوفة بايت، أو حتى URL.

```java
import com.aspose.ocr.*;
import java.nio.file.Files;
import java.nio.file.Paths;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Step 2: Load the image you wish to process
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/invoice.png"));
```

لاحظ كيف **load image for OCR** يتم باستدعاء طريقة واحدة — دون الحاجة إلى حركات معقدة على `BufferedImage`. إذا كانت الصورة موجودة في الموارد، استبدل المسار بـ `getClass().getResourceAsStream(...)`.

## الخطوة 3: تمكين تصحيح الإملاء (اختياري لكنه قوي)

يمكن لـ Aspose OCR تصحيح الأخطاء الشائعة تلقائيًا (مثل “l” مقابل “1”). تشغيل هذه الميزة بسيط كإبدال علم:

```java
        // Step 3: Turn on spell‑checking to improve result quality
        ocrEngine.getEngineOptions().setSpellCorrectionEnabled(true);
```

لماذا؟ تخيّل أنك تمسح فاتورة مطبوعة بخط صغير والماسح يضيف بقعًا عشوائية. تصحيح الإملاء سيعيد غالبًا “Inv0ice” إلى “Invoice” دون أي جهد إضافي منك.

## الخطوة 4: توفير قاموس مخصص (تخصيص المحرك)

إذا كنت تتعامل مع مصطلحات خاصة بصناعتك — مثل الرموز الطبية، المصطلحات القانونية، أو رموز المنتجات — فإن القاموس المخصص يمكنه تحسين الدقة بشكل كبير. القاموس هو مجرد ملف نصي يحتوي على كلمة واحدة في كل سطر.

```java
        // Step 4: Load a custom dictionary to boost recognition of domain terms
        ocrEngine.getEngineOptions().setCustomDictionary(
                Files.readAllLines(Paths.get("YOUR_DIRECTORY/custom_dict.txt")));
```

تأكد من أن الملف يستخدم ترميز UTF‑8؛ وإلا قد تظهر أحرف مشوشة للكلمات غير الـ ASCII.

## الخطوة 5: تشغيل عملية OCR

الآن نترك المحرك يقوم بسحره. استدعاء `process()` يُعيد كائن `OcrResult` يحتوي على النص المستخرج، درجات الثقة، وحتى تخطيط الصفحة إذا احتجت إليه لاحقًا.

```java
        // Step 5: Execute OCR and capture the result
        OcrResult ocrResult = ocrEngine.process();
```

إذا تساءلت يومًا ما إذا كان المحرك قد رمى استثناءً، غلف هذا الاستدعاء بكتلة `try‑catch` وتفقد `ocrResult.getErrorMessage()` للحصول على التفاصيل.

## الخطوة 6: إخراج النص المستخرج (والمصحح)

الخطوة الأخيرة هي عرض — أو تخزين — السلسلة المستخرجة. للعرض السريع سنطبعها على وحدة التحكم:

```java
        // Step 6: Print the corrected text to the console
        System.out.println(ocrResult.getText());
    }
}
```

تشغيل البرنامج يجب أن يطبع شيئًا مثل:

```
Invoice Number: 12345
Date: 2023‑07‑15
Total Amount: $1,250.00
```

إذا رأيت أحرفًا غريبة، تحقق مرة أخرى من القاموس المخصص وفكّر في تعديل جودة الصورة (مثلاً زيادة التباين قبل تمريرها إلى المحرك).

### مثال كامل يعمل

بجمع كل ما سبق، إليك الفئة الكاملة الجاهزة للتنفيذ:

```java
import com.aspose.ocr.*;
import java.nio.file.Files;
import java.nio.file.Paths;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image you wish to process
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/invoice.png"));

        // Step 3: Enable spell‑checking for the OCR result
        ocrEngine.getEngineOptions().setSpellCorrectionEnabled(true);

        // Step 4: Provide a custom dictionary (one word per line)
        ocrEngine.getEngineOptions().setCustomDictionary(
                Files.readAllLines(Paths.get("YOUR_DIRECTORY/custom_dict.txt")));

        // Step 5: Run the OCR process
        OcrResult ocrResult = ocrEngine.process();

        // Step 6: Output the recognized (and corrected) text
        System.out.println(ocrResult.getText());
    }
}
```

احفظ هذا الملف باسم `SpellCorrectDemo.java`، عدّل المسارات، ثم قم بالترجمة باستخدام `javac` وشغّله بـ `java SpellCorrectDemo`. الآن يمكنك **perform OCR on image** للملفات ورؤية النص المستخرج يُطبع على الشاشة.

## أسئلة شائعة وحالات خاصة

### ماذا لو كانت الصورة بصيغة مختلفة (PDF, TIFF, إلخ)؟

يمكن لـ Aspose OCR التعامل مع العديد من صيغ الـ raster مباشرة. بالنسبة للـ PDF ستحتاج أولاً لاستخراج كل صفحة كصورة — Aspose PDF for Java يقوم بذلك بسهولة. استدعاء `setImage` نفسه يعمل بمجرد حصولك على `BufferedImage` أو تدفق بايت.

### كيف أتعامل مع مستندات متعددة الصفحات؟

كرر العملية لكل صورة صفحة، نفّذ خطوات OCR، ثم صلّ النتائج. تذكّر أن تُعيد إنشاء أو إعادة ضبط كائن `OcrEngine` لكل صفحة إذا أردت سياقات تدقيق إملائي مستقلة.

### هل يمكن تحديد اللغة أو مجموعة الأحرف؟

نعم. استخدم `ocrEngine.getEngineOptions().setLanguage(Language.English);` (أو أي لغة مدعومة أخرى) لتقليل الإيجابيات الكاذبة وتسريع المعالجة.

### ماذا عن الأداء عند معالجة دفعات كبيرة؟

Aspose OCR آمن للاستخدام المتعدد الخيوط للعمليات القراءة فقط. يمكنك إنشاء مجموعة خيوط (thread pool) ومعالجة الصور بشكل متوازي — فقط تجنّب مشاركة نفس كائن `OcrEngine` بين الخيوط.

## نصائح لتحسين الدقة

- **معالجة مسبقة للصورة**: زيادة التباين، إزالة الضوضاء الخلفية، أو التحويل إلى تدرج الرمادي.
- **استخدام مسح عالي الدقة** (300 dpi أو أعلى). الدقة المنخفضة غالبًا ما تنتج أحرفًا مشوشة.
- **اجعل القاموس المخصص مختصرًا**: كثرة الكلمات غير المرتبطة قد تشوش مدقق الإملاء.
- **تحقق من المخرجات**: إذا كنت تعرف الصيغة المتوقعة (مثل التواريخ أو الأرقام)، نفّذ تعبيرًا نمطيًا (regex) بعد المعالجة لالتقاط الشذوذ.

## الخطوات التالية

الآن بعد أن أصبحت قادرًا على **perform OCR on image** و**extract text from image** باستخدام Aspose OCR، قد ترغب في استكشاف:

- **حفظ ناتج OCR إلى PDF** مع طبقة نصية قابلة للبحث.
- **دمج النتائج مع قاعدة بيانات** لتخزين بيانات الفواتير المستخرجة تلقائيًا.
- **تطبيق معالجة ما بعد التعلم الآلي** للحصول على دقة أعلى في الملاحظات المكتوبة يدويًا.
- **استخدام علم `load image for OCR`** في خدمة ويب تقبل صورًا يرفعها المستخدمون.

كل من هذه المواضيع يبني على الخطوات الأساسية التي غطيناها، لذا ستجد الانتقال سلسًا.

---

*برمجة سعيدة! إذا واجهتك أي صعوبات، لا تتردد بترك تعليق — لا شيء يفوق التعلم من أمثلة واقعية.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}