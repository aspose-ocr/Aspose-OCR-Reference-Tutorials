---
category: general
date: 2026-03-28
description: قم بتنفيذ التعرف الضوئي على الأحرف (OCR) على الصورة باستخدام Aspose OCR
  في Java. تعلّم كيفية التعرف على النص من ملفات PNG وتحسين دقة الـ OCR باستخدام تصحيح
  الأخطاء الإملائية المدمج.
draft: false
keywords:
- perform OCR on image
- recognize text from PNG
- read image text
- improve OCR accuracy
- Aspose OCR Java
- spell correction OCR
language: ar
og_description: قم بإجراء OCR على الصورة باستخدام Aspose OCR للغة Java. يوضح هذا الدليل
  كيفية التعرف على النص من PNG وتحسين دقة OCR في دقائق.
og_title: إجراء التعرف الضوئي على الأحرف في الصورة باستخدام جافا – دليل كامل
tags:
- OCR
- Java
- Aspose
- Image Processing
title: إجراء OCR على صورة باستخدام جافا – التعرف على النص من PNG
url: /ar/java/advanced-ocr-techniques/perform-ocr-on-image-with-java-recognize-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تنفيذ OCR على صورة باستخدام Java – التعرف على النص من PNG

هل احتجت يومًا إلى **perform OCR on image** ملفات ولكنك استمرّ في الحصول على نتائج مشوشة؟ لست وحدك—المسحات الضوضائية، PNG ذات التباين المنخفض، والخطوط الغريبة يمكن أن تحول مستندًا نظيفًا إلى فوضى من الأحرف.  

في هذا الدليل سنرشدك عبر مثال Java كامل وجاهز للتنفيذ يستخدم Aspose OCR لـ **recognize text from PNG**، وسنوضح لك أيضًا كيفية **improve OCR accuracy** باستخدام ميزة تصحيح الإملاء في المكتبة. في النهاية، ستكون قادرًا على **read image text** بشكل موثوق، حتى عندما لا يكون المصدر مثاليًا.

## ما ستتعلمه

- كيفية إعداد Aspose OCR لـ Java في مشروع Maven.  
- الخطوات الدقيقة لـ **perform OCR on image** البيانات، من تحميل الملف إلى استخراج نص نظيف.  
- لماذا يمكن لتفعيل تصحيح الإملاء أن يعزز جودة الناتج بشكل كبير.  
- المشكلات الشائعة (ملفات مفقودة، صيغ غير مدعومة) وكيفية التعامل معها بسلاسة.  
- عينة شفرة كاملة جاهزة للنسخ واللصق يمكنك تشغيلها اليوم.

### المتطلبات المسبقة

- Java 8 أو أحدث مثبت على جهازك.  
- Maven لإدارة التبعيات (أي بيئة تطوير تدعم Maven تكفي).  
- صورة PNG تحتوي على بعض النص القابل للقراءة—يفضل أن تكون ذات ضوضاء قليلة حتى تتمكن من رؤية فائدة تصحيح الإملاء.

> **نصيحة احترافية:** إذا لم يكن لديك PNG جاهز، احصل على أي لقطة شاشة لمستند أو صورة لعلامة. كلما كانت أكثر “ضوضاء”، كلما قدرت تحسين الدقة بشكل أفضل.

---

## الخطوة 1: إضافة تبعية Aspose OCR

أولاً وقبل كل شيء—أضف مكتبة Aspose OCR إلى ملف `pom.xml` الخاص بك. هذه السطر الواحد يجلب أحدث نسخة (اعتبارًا من مارس 2026) ويحل جميع التبعيات المتسلسلة.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version>
</dependency>
```

> **لماذا هذا مهم:** بدون المكتبة لا يمكنك إنشاء `OcrEngine`، وستتعطل عملية **perform OCR on image** بالكامل أثناء التشغيل.

---

## الخطوة 2: تهيئة محرك OCR

إنشاء المحرك سهل، لكن هناك سبب طفيف للحفاظ على التهيئة منفصلة عن استدعاء التعرف: يمنحك ذلك مكانًا لضبط الإعدادات مثل اللغة، DPI، أو، الأكثر أهمية بالنسبة لنا، تصحيح الإملاء.

```java
import com.aspose.ocr.*;

public class SpellCorrectExample {

    public static void main(String[] args) {
        try {
            // Step 2: Initialize the OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // Pro tip: you can set the language here if you need something other than English
            // ocrEngine.getRecognitionSettings().setLanguage(OcrLanguage.FRENCH);
```

لاحظ التعليق—ضبط اللغة يمكن أن يكون منقذًا عندما تحتوي PNG الخاصة بك على أحرف غير إنجليزية.

---

## الخطوة 3: تفعيل تصحيح الإملاء لـ **Improve OCR Accuracy**

تأتي Aspose OCR مع وحدة تصحيح إملائي مدمجة تعمل كقاموس خفيف. تفعيلها سطر واحد فقط، لكن تأثيره على الناتج النهائي يمكن أن يكون هائلًا، خاصةً للصور الضوضائية.

```java
            // Step 3: Enable spell correction to improve OCR accuracy on noisy text
            ocrEngine.getRecognitionSettings().setEnableSpellCorrection(true);
```

> **ماذا لو لم تحتاجها؟** يمكنك ببساطة ضبط العلامة إلى `false`. قد يكون تعطيلها مفيدًا للنصوص المتخصصة حيث قد يعتبر القاموس المصطلحات الصحيحة أخطاء.

---

## الخطوة 4: تحميل وتعرف على PNG

الآن نحن فعليًا **read image text** من الملف. طريقة `recognizeImage` تقبل سلسلة مسار، لكن يمكنك أيضًا تمرير `java.io.InputStream` إذا كنت تجلب الصورة من قاعدة بيانات أو الويب.

```java
            // Step 4: Perform OCR on the input image
            String imagePath = "YOUR_DIRECTORY/noisy-image.png"; // replace with your actual path
            OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);
```

إذا لم يُعثر على الملف، تقوم Aspose بإلقاء استثناء وصفي—ليس هناك حاجة للتحقق يدويًا من `File.exists()`. ومع ذلك، تغليف الاستدعاء داخل `try/catch` (كما نفعل) يمنحك رسالة خطأ واضحة للمستخدم النهائي.

---

## الخطوة 5: إخراج النص المصحح

أخيرًا، اطبع النتيجة إلى وحدة التحكم. في تطبيق واقعي ربما تكتب ذلك إلى قاعدة بيانات أو خدمة لاحقة، لكن وحدة التحكم مثالية لعرض سريع.

```java
            // Step 5: Output the corrected text
            System.out.println("Corrected text:\\n" + ocrResult.getText());
        } catch (Exception e) {
            System.err.println("Error during OCR processing: " + e.getMessage());
        }
    }
}
```

**الناتج المتوقع** (بافتراض أن PNG تحتوي على العبارة “Aspose OCR library” مع بعض الضوضاء):

```
Corrected text:
Aspose OCR library
```

إذا عطلت تصحيح الإملاء، قد ترى شيئًا مثل “Asp0se OCR libr@ry” بدلاً من ذلك—وهذا بالضبط سبب أهمية **improve OCR accuracy**.

---

## الخطوة 6: التحقق من النتيجة – هل فعلاً **Read Image Text**؟

من المغري الوثوق بمخرجات وحدة التحكم دون تمحيص، لكن فحص سريع يمكن أن يوفر لك ساعات لاحقًا. إليك بعض الطرق للتحقق من النص المستخرج:

1. **فحص الطول** – قارن `ocrResult.getText().length()` مع عدد الأحرف المتوقع.  
2. **بحث عن كلمة مفتاحية** – استخدم `String.contains("Aspose")` للتأكد من ظهور المصطلحات الرئيسية.  
3. **اختبار وحدة** – إذا كنت تدمج هذا في نظام أكبر، اكتب اختبار JUnit يتحقق من أن الناتج يطابق قيمة معروفة صحيحة.

```java
// Example sanity check
if (ocrResult.getText().contains("Aspose")) {
    System.out.println("✅ Text successfully read from image.");
} else {
    System.out.println("⚠️ Unexpected OCR result – consider tweaking settings.");
}
```

---

## الحالات الطرفية الشائعة وكيفية التعامل معها

| الحالة | لماذا يحدث | الحل السريع |
|-----------|----------------|-----------|
| **File not found** | مسار خاطئ أو أذونات مفقودة | تحقق من `imagePath` واستخدم `Files.isReadable(Paths.get(imagePath))` قبل استدعاء `recognizeImage`. |
| **Unsupported format** | صيغ غير مدعومة | حوّل الصورة إلى PNG أولاً (مثلاً باستخدام ImageIO) أو استخدم `ocrEngine.recognizeImage(InputStream)`. |
| **Very low DPI** | DPI منخفض جدًا | قم بزيادة حجم الصورة باستخدام `BufferedImage` و `Graphics2D` قبل تمريرها إلى المحرك. |
| **Domain‑specific jargon** | مصطلحات متخصصة قد يستبدلها تصحيح الإملاء بكلمات القاموس | عطل تصحيح الإملاء (`setEnableSpellCorrection(false)`) أو زوّد قاموسًا مخصصًا عبر `ocrEngine.getRecognitionSettings().setCustomDictionary(...)`. |

---

## مثال كامل جاهز للتنفيذ (نسخ‑لصق)

فيما يلي ملف المصدر الكامل، جاهز للترجمة والتنفيذ. استبدل `YOUR_DIRECTORY/noisy-image.png` بالمسار الفعلي لصورتك التجريبية.

```java
import com.aspose.ocr.*;

public class SpellCorrectExample {
    public static void main(String[] args) {
        try {
            // Initialize the OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // Enable spell correction to improve OCR accuracy on noisy text
            ocrEngine.getRecognitionSettings().setEnableSpellCorrection(true);

            // Path to the PNG you want to process
            String imagePath = "YOUR_DIRECTORY/noisy-image.png";

            // Perform OCR on the input image
            OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);

            // Output the corrected text
            System.out.println("Corrected text:\\n" + ocrResult.getText());

            // Simple verification that we actually read image text
            if (ocrResult.getText().toLowerCase().contains("aspose")) {
                System.out.println("✅ OCR succeeded – key term found.");
            } else {
                System.out.println("⚠️ OCR may need tweaking – key term missing.");
            }
        } catch (Exception e) {
            System.err.println("Error during OCR processing: " + e.getMessage());
        }
    }
}
```

شغّله باستخدام:

```bash
mvn compile exec:java -Dexec.mainClass=SpellCorrectExample
```

يجب أن ترى **corrected text** مطبوعًا، مما يؤكد أنك نجحت في **perform OCR on image** البيانات.

---

## ملخص بصري

![Perform OCR on image example](/images/ocr-example.png){alt="تنفيذ OCR على الصورة – قبل وبعد تصحيح الإملاء"}

توضح لقطة الشاشة PNG ضوضائية على اليسار والنص النظيف بعد تصحيح الإملاء على اليمين.

---

## الخلاصة

لقد استعرضنا للتو حلاً كاملاً من البداية إلى النهاية لكيفية **perform OCR on image** الملفات باستخدام Aspose OCR للـ Java. من خلال تفعيل علامة تصحيح الإملاء المدمجة، يمكنك **improve

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}