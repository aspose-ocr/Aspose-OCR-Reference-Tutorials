---
category: general
date: 2026-02-27
description: يتيح الكشف التلقائي عن اللغة استخراج النص من ملفات الصور مثل PNG في جافا
  — راجع مثال OCR بجافا يتيح الكشف التلقائي عن اللغة.
draft: false
keywords:
- automatic language detection
- extract text from image
- convert png to text
- java ocr example
- enable auto language detection
language: ar
og_description: الكشف التلقائي عن اللغة في OCR باستخدام جافا يجعل استخراج النص من
  ملفات الصور سهلاً. تعلّم كيفية تمكين الكشف التلقائي عن اللغة مع مثال كامل لـ OCR
  بجافا.
og_title: اكتشاف اللغة تلقائيًا في OCR بجافا – دليل شامل
tags:
- Java
- OCR
- Aspose
title: اكتشاف اللغة تلقائيًا في OCR باستخدام جافا – دليل خطوة بخطوة
url: /ar/java/advanced-ocr-techniques/automatic-language-detection-in-java-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# الكشف التلقائي عن اللغة في Java OCR – دليل شامل

هل احتجت يوماً إلى **الكشف التلقائي عن اللغة** عند استخراج النص من لقطة شاشة تحتوي على الإنجليزية والروسية معًا؟ لست وحدك. في العديد من التطبيقات الواقعية—مثل ماسحات الفواتير، النماذج متعددة اللغات، أو بوتات الصور على وسائل التواصل الاجتماعي—اختيار اللغة يدويًا يُعد نقطة ضعف.

الخبر السار هو أن Aspose OCR for Java يمكنه اكتشاف اللغة تلقائيًا، بحيث يمكنك ببساطة **استخراج النص من ملفات الصورة** دون أي إعداد يدوي. في هذا الدرس سنعرض **مثال java ocr** يُفعِّل **الكشف التلقائي عن اللغة**، يعالج صورة PNG متعددة اللغات، ويطبع النتيجة في وحدة التحكم. بنهاية الدرس ستعرف بالضبط كيف **تحويل png إلى نص** ببضع أسطر من الشيفرة فقط.

## ما الذي ستحتاجه

- Java 17 (أو أي JDK حديث) – تعمل الواجهة البرمجية مع Java 8+ لكن الإصدارات الأحدث تعطي أداءً أفضل.
- مكتبة Aspose OCR for Java (أحدث نسخة حتى 2026‑02‑27). يمكنك الحصول عليها من Maven Central:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version>
</dependency>
```

- ملف صورة يحتوي على أكثر من لغة واحدة. في مثالنا سنستخدم `mixed-eng-rus.png` (إنجليزية + روسية).  
- بيئة تطوير متكاملة جيدة (IntelliJ IDEA، Eclipse، VS Code…) – أي منها يناسبك.

> **نصيحة محترف:** إذا لم يكن لديك صورة اختبار، أنشئ PNG يحتوي على بضع كلمات إنجليزية وما يعادلها بالروسية. محرك OCR لا يهتم بالمصدر، فقط ببيانات البكسل.

فيما يلي البرنامج الكامل الجاهز للتنفيذ.

![الكشف التلقائي عن اللغة في صورة PNG متعددة اللغات](/images/mixed-eng-rus.png "مثال على الكشف التلقائي عن اللغة")

## الخطوة 1: إعداد محرك OCR

أولاً، أنشئ مثيلًا من `OcrEngine`. هذا الكائن هو قلب المكتبة؛ فهو يحمل جميع خيارات التكوين، بما في ذلك الخيار الذي يُفعِّل **الكشف التلقائي عن اللغة**.

```java
import com.aspose.ocr.*;

public class MixedLanguageDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable automatic language detection
        ocrEngine.setAutoDetectLanguage(true);
```

لماذا نفعِّله هنا؟  
لأنه بدون `setAutoDetectLanguage(true)`، سيفترض المحرك لغةً افتراضية (عادةً الإنجليزية). عندما تمزج صورتك بين أنظمة كتابة مختلفة، خطوة الكشف تحسّن الدقة بشكل كبير—فكر فيها كالمترجم الفوري متعدد اللغات الذي يستمع قبل الترجمة.

## الخطوة 2: تمرير الصورة وتشغيل عملية OCR

الآن وجه المحرك إلى ملف PNG. تُعيد طريقة `processImage` كائنًا من نوع `OcrResult` يحتوي على النص المُعترف به، درجات الثقة، وحتى رمز اللغة المكتشفة.

```java
        // Step 3: Process the image that contains both English and Russian text
        OcrResult ocrResult = ocrEngine.processImage("YOUR_DIRECTORY/mixed-eng-rus.png");
```

بعض الملاحظات:

- **معالجة المسار:** استخدم مسارًا مطلقًا أو ضع الصورة في مجلد الموارد الخاص بالمشروع وحمِّلها عبر `getResourceAsStream`.
- **نصيحة أداء:** إذا كنت تعالج العديد من الصور، أعد استخدام نفس مثيل `OcrEngine` بدلاً من إنشاء جديد في كل مرة. المحرك يخزن نماذج اللغات في الذاكرة، لذا تكون الاستدعاءات اللاحقة أسرع.

## الخطوة 3: استرجاع وعرض النص المُعترف به

أخيرًا، استخرج النص العادي من `OcrResult`. تُعيد طريقة `getText()` النص بدون أي معلومات تخطيطية، لتمنحك سلسلة نظيفة يمكنك تخزينها أو البحث فيها أو تمريرها إلى نظام آخر.

```java
        // Step 4: Print the recognized text to the console
        System.out.println(ocrResult.getText());
    }
}
```

عند تشغيل البرنامج، يجب أن ترى شيئًا مشابهًا لـ:

```
Hello world!
Привет мир!
```

هذا الإخراج يؤكد أن المحرك حدد بنجاح كلًا من القسمين الإنجليزي والروسي، بفضل **الكشف التلقائي عن اللغة**. إذا أوقفت هذه الميزة، ستحصل على أحرف سيريالية مشوشة، مما يوضح أهمية خاصية الكشف التلقائي في السيناريوهات متعددة اللغات.

## الاختلافات الشائعة والحالات الخاصة

### تحويل PNG إلى نص دون الكشف عن اللغة

إذا كنت تعلم أن الصورة تحتوي على لغة واحدة فقط، يمكنك تخطي خطوة الكشف التلقائي:

```java
ocrEngine.setLanguage(OcrLanguage.English);
```

لكن تذكر، بمجرد ظهور حرف من نظام كتابة آخر، تنخفض الدقة بشكل حاد.

### التعامل مع الصور الكبيرة

للمسحات عالية الدقة، فكر في تقليل الحجم إلى حد أقصى 300 DPI قبل تمرير الصورة. يعمل محرك OCR بأفضل أداء في نطاق 150‑300 DPI؛ ما فوق ذلك يستهلك الذاكرة دون فائدة ملحوظة.

```java
BufferedImage original = ImageIO.read(new File("large.png"));
BufferedImage resized = ImageUtil.resize(original, 1024, 0); // keep aspect ratio
ocrEngine.processImage(resized);
```

### استخراج النص من صورة في خدمة ويب

إذا كنت تعرض هذه الوظيفة عبر نقطة نهاية REST، تذكر أن:

- تتحقق من نوع الملف المرفوع (اقبل PNG/JPEG فقط).
- تشغل OCR في خيط خلفي أو مهمة غير متزامنة لتجنب حجز خيط الطلب.
- تُعيد النص كـ JSON:

```json
{ "extractedText": "Hello world!\nПривет мир!" }
```

## مثال كامل يعمل (جميع الخطوات مجمعة)

فيما يلي البرنامج الكامل الذي يمكنك نسخه ولصقه في ملف `MixedLanguageDemo.java`. يتضمن عبارات الاستيراد، معالجة الأخطاء، وتعليق يوضح كل سطر.

```java
import com.aspose.ocr.*;
import java.io.File;

/**
 * Demonstrates automatic language detection with Aspose OCR for Java.
 * This example loads a PNG that contains both English and Russian text,
 * enables auto‑detect, and prints the extracted text.
 */
public class MixedLanguageDemo {
    public static void main(String[] args) throws Exception {
        // Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Enable automatic language detection so the engine picks the right script(s)
        ocrEngine.setAutoDetectLanguage(true);

        // Path to the image – replace with your actual location
        String imagePath = "YOUR_DIRECTORY/mixed-eng-rus.png";

        // Process the image and obtain the result
        OcrResult ocrResult = ocrEngine.processImage(imagePath);

        // Output the recognized text – should contain both English and Russian lines
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

شغّله باستخدام:

```bash
mvn compile exec:java -Dexec.mainClass=MixedLanguageDemo
```

إذا تم إعداد كل شيء بشكل صحيح، ستظهر وحدة التحكم السطر الإنجليزي متبوعًا بنظيره الروسي.

## ملخص وخطوات مستقبلية

استعرضنا **مثال java ocr** يُفعِّل **الكشف التلقائي عن اللغة**، يعالج PNG متعددة اللغات، و**يستخرج النص من ملفات الصورة** دون الحاجة لتحديد اللغة يدويًا. النقاط الأساسية:

1. فعل `setAutoDetectLanguage(true)` لتترك Aspose يتعامل مع المحتوى متعدد اللغات.
2. استخدم `processImage` لتمرير أي PNG (أو JPEG) واحصل على سلسلة نظيفة عبر `getText()`.
3. نفس النمط يعمل مع PDFs، TIFFs، أو حتى تدفقات الكاميرا الحية—فقط استبدل مصدر الإدخال.

هل تريد التعمق أكثر؟ جرّب الأفكار التالية:

- **معالجة دفعات:** كرّر العملية على مجلد من PNGs وخزن كل نتيجة في قاعدة بيانات.
- **معالجة ما بعد اللغة:** بعد الكشف، وجه النص الإنجليزي إلى مدقق إملائي والنص الروسي إلى خدمة تحويل نص إلى صوت.
- **دمج مع الذكاء الاصطناعي:** أغذِ النص المستخرج إلى نموذج لغة لتلخيصه أو ترجمته.

هذا كل شيء حتى الآن. إذا واجهت أي مشاكل—مثل عدم اكتشاف المحرك للغة متوقعة—تحقق من وضوح الصورة وأنك تستخدم أحدث نسخة من Aspose OCR. نتمنى لك برمجة سعيدة، واستمتع بقوة **الكشف التلقائي عن اللغة** في مشاريع Java الخاصة بك!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}