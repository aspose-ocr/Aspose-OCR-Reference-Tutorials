---
category: general
date: 2026-02-14
description: اكتشاف لغة الصورة باستخدام Aspose OCR في Java – تعلم كيفية استخراج النص
  من الصورة، تحويل الصورة إلى نص باستخدام OCR، وقراءة نص PNG مع الحصول على اللغة المكتشفة.
draft: false
keywords:
- detect language image
- extract text image
- ocr image to text
- read text png
- get detected language
language: ar
og_description: اكتشاف لغة الصورة باستخدام Aspose OCR في جافا. تعلم كيفية استخراج
  النص من الصورة، تحويل الصورة إلى نص باستخدام OCR، قراءة نص PNG، والحصول على اللغة
  المكتشفة في دقائق.
og_title: اكتشاف لغة الصورة باستخدام Aspose OCR – دليل جافا
tags:
- OCR
- Java
- Aspose
title: اكتشاف لغة الصورة باستخدام Aspose OCR – دليل جافا
url: /ar/java/advanced-ocr-techniques/detect-language-image-with-aspose-ocr-java-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# اكتشاف لغة الصورة باستخدام Aspose OCR – دليل Java

هل احتجت يومًا إلى **اكتشاف لغة الصورة** لكنك لم تكن متأكدًا أي مكتبة يمكنها القيام بذلك تلقائيًا؟ لست وحدك—العديد من المطورين يواجهون هذه المشكلة عندما تحتوي صورة واحدة على نص بعدة لغات.  

في هذا الدليل سنوضح لك، خطوة بخطوة، كيفية استخدام Aspose OCR for Java لـ **اكتشاف لغة الصورة**، **استخراج نص الصورة**، وتحويل ملف PNG إلى نص قابل للبحث. في النهاية ستتمكن من **تحويل الصورة إلى نص**، **قراءة نص PNG**، وحتى **الحصول على اللغة المكتشفة** دون الحاجة لكتابة نموذج تعلم آلي مخصص.

## ما ستتعلمه

- كيفية إنشاء وتكوين كائن `OcrEngine`.
- تمكين الكشف التلقائي عن اللغة بحيث يختار المحرك النص المناسب.
- استخراج النص من ملف PNG متعدد اللغات.
- استرجاع رمز اللغة الذي حددته Aspose.
- المشكلات الشائعة (مثل الصور الضبابية) ونصائح لتحسين الدقة.

**المتطلبات المسبقة**  
JDK 17+، Maven أو Gradle، ورخصة Aspose OCR for Java (الإصدار التجريبي المجاني يكفي للعرض). لا تحتاج إلى أي أدوات OCR طرف ثالث أخرى.

---

## الخطوة 1: إعداد المشروع واستيراد Aspose OCR

أولاً، أضف تبعية Aspose OCR إلى ملف `pom.xml` (Maven) أو `build.gradle` (Gradle). إليك مقتطف Maven:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- latest as of Feb 2026 -->
</dependency>
```

إذا كنت تفضّل Gradle:

```gradle
// build.gradle
implementation 'com.aspose:aspose-ocr:23.10'
```

> **نصيحة احترافية:** احرص على تحديث المكتبة بانتظام؛ الإصدارات الأحدث تحسّن من الكشف متعدد اللغات.

الآن أنشئ فئة Java بسيطة تسمى `AutoLangDemo`. ستحمل هذه الملف المثال القابل للتنفيذ بالكامل.

---

## الخطوة 2: تهيئة محرك OCR (اكتشاف لغة الصورة)

أول شيء تقوم به هو إنشاء كائن `OcrEngine`. هذا الكائن هو قلب عملية **اكتشاف لغة الصورة**.

```java
import com.aspose.ocr.*;

public class AutoLangDemo {
    public static void main(String[] args) throws Exception {

        // Step 2.1: Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2.2: Load the image that contains multiple languages
        String imagePath = "YOUR_DIRECTORY/multilang.png";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));

        // Step 2.3: Enable automatic language detection
        ocrEngine.getEngineOptions().setLanguage(OcrLanguage.AUTO_DETECT);

        // Step 2.4: Perform OCR processing on the image
        OcrResult ocrResult = ocrEngine.process();

        // Step 2.5: Output the detected language and extracted text
        System.out.println("Detected language: " + ocrResult.getDetectedLanguage());
        System.out.println(ocrResult.getText());
    }
}
```

لاحظ كيف أن التعليق `// Step 2.3` يذكر *الكشف التلقائي عن اللغة*—هذا هو السطر الذي يجعل المحرك **يكتشف لغة الصورة** دون أن تحدد رمز اللغة يدويًا.

---

## الخطوة 3: تشغيل المثال والتحقق من النتيجة (استخراج نص الصورة)

قم بترجمة البرنامج وتشغيله:

```bash
mvn compile exec:java -Dexec.mainClass=AutoLangDemo
```

إذا تم إعداد كل شيء بشكل صحيح، ستظهر لك نتيجة مشابهة لـ:

```
Detected language: en
Hello World!
Bonjour le monde!
Hola Mundo!
```

تطبع وحدة التحكم **اللغة المكتشفة** (`en` للإنجليزية) متبوعةً بنتيجة **استخراج نص الصورة**. عمليًا، قد يكون رمز اللغة `fr` أو `es` أو `de`، حسب النص السائد.

> **لماذا يعمل هذا:** تقوم Aspose OCR بمسح البت ماب، وتقييم مجموعات الأحرف، وتختار اللغة الأكثر احتمالًا من القاموس المدمج. بتعيين `OcrLanguage.AUTO_DETECT`، تترك للمحرك مهمة الكشف عن اللغة.

---

## الخطوة 4: التعامل مع الحالات الخاصة – عندما يفشل الكشف

حتى أفضل محركات OCR قد تواجه صعوبات مع PNG منخفض الدقة أو مشوش. إليك بعض الحيل **لتحسين الموثوقية**:

| المشكلة | الحل |
|-------|-----|
| **صورة ضبابية** | قم بالمعالجة المسبقة باستخدام `java.awt` لتكبير الصورة (`BufferedImage.getScaledInstance`) أو تطبيق مرشح تعزيز الحدة. |
| **لغات مختلطة في نفس الصفحة** | استدعِ `ocrEngine.process()` على كل **منطقة** على حدة باستخدام `ocrEngine.setRegion(Rectangle)`. |
| **نص غير مدعوم** | عيّن صراحةً `ocrEngine.getEngineOptions().setLanguage(OcrLanguage.<YOUR_LANG>)` كخطة احتياطية. |

هذه الاقتراحات تجعل خط أنابيب **تحويل الصورة إلى نص** أكثر **متانة**، خاصة عندما تحتاج إلى **قراءة نص PNG** من إيصالات ممسوحة أو لقطات شاشة.

---

## الخطوة 5: حفظ النص المستخرج (قراءة نص PNG)  

غالبًا ما ترغب في تخزين نتيجة OCR في ملف لمعالجة لاحقة. المقتطف التالي يكتب النتيجة إلى `output.txt`:

```java
import java.nio.file.*;

Path outPath = Paths.get("output.txt");
Files.writeString(outPath, ocrResult.getText(), StandardOpenOption.CREATE);
System.out.println("Text saved to " + outPath.toAbsolutePath());
```

الآن لم تقم فقط بـ **اكتشاف لغة الصورة** و**استخراج نص الصورة**، بل لديك نسخة دائمة يمكنك تمريرها إلى فهارس البحث، أو واجهات برمجة تطبيقات الترجمة، أو خطوط البيانات.

---

## مثال كامل يعمل (جميع الخطوات مجمعة)

فيما يلي الكود الكامل الجاهز للتنفيذ. انسخه إلى `src/main/java/AutoLangDemo.java` ثم شغّله.

```java
import com.aspose.ocr.*;
import java.nio.file.*;

public class AutoLangDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load multi‑language PNG (replace with your actual path)
        String imagePath = "YOUR_DIRECTORY/multilang.png";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));

        // 3️⃣ Auto‑detect language – this is the heart of detect language image
        ocrEngine.getEngineOptions().setLanguage(OcrLanguage.AUTO_DETECT);

        // 4️⃣ Run OCR
        OcrResult ocrResult = ocrEngine.process();

        // 5️⃣ Show detected language and extracted text
        System.out.println("Detected language: " + ocrResult.getDetectedLanguage());
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());

        // 6️⃣ Persist the text (optional)
        Path outPath = Paths.get("output.txt");
        Files.writeString(outPath, ocrResult.getText(), StandardOpenOption.CREATE);
        System.out.println("Saved extracted text to " + outPath.toAbsolutePath());
    }
}
```

**الناتج المتوقع في وحدة التحكم**

```
Detected language: fr
=== Extracted Text ===
Bonjour le monde!
Hello World!
¡Hola Mundo!
```

سيتغير رمز اللغة الفعلي بحسب محتوى الصورة، لكن النمط يبقى نفسه.

---

## الأسئلة المتكررة

**س: هل يعمل هذا مع ملفات JPEG أو BMP؟**  
ج: بالتأكيد. تدعم Aspose OCR صيغ PNG، JPEG، BMP، TIFF، وGIF. فقط غيّر امتداد الملف في `imagePath`.

**س: هل يمكنني اكتشاف أكثر من لغة واحدة في نفس الصورة؟**  
ج: نعم. يعيد المحرك **اللغة الأساسية**، لكن يمكنك استدعاء `ocrEngine.process()` على مناطق منفصلة لالتقاط كل نص على حدة.

**س: ماذا لو احتوت الصورة على نص مكتوب يدويًا؟**  
ج: يبرع محرك Aspose OCR الحالي مع الخطوط المطبوعة. قد يتطلب النص المكتوب يدويًا نموذجًا متخصصًا (مثل Azure Cognitive Services) – وهذا سيناريو مختلف.

---

## الخلاصة

أصبح لديك الآن وصفة شاملة من البداية إلى النهاية لـ **اكتشاف لغة الصورة**، **استخراج نص الصورة**، و**تحويل الصورة إلى نص** باستخدام Aspose OCR for Java. بتمكين `OcrLanguage.AUTO_DETECT` تسمح للمكتبة تلقائيًا بـ **الحصول على اللغة المكتشفة**، ومع بضع أسطر إضافية يمكنك **قراءة نص PNG**، حفظ النتيجة، ومعالجة الحالات الخاصة الشائعة.

هل أنت مستعد للخطوة التالية؟ جرّب تمرير النص المستخرج إلى واجهة برمجة تطبيقات Google Translate، أو فهرسته باستخدام Elasticsearch لإنشاء ملفات PDF قابلة للبحث. يمكنك أيضًا تجربة المعالجة الدفعية—التكرار على مجلد من PNGs وكتابة كل نتيجة إلى ملف `.txt` خاص بها.

برمجة سعيدة، ولتكن خطوط OCR الخاصة بك دقيقة دائمًا!  

---

![مثال على اكتشاف لغة الصورة](detect-language-image.png "مثال على اكتشاف لغة الصورة")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}