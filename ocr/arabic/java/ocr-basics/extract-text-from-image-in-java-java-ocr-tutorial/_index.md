---
category: general
date: 2026-03-07
description: استخراج النص من الصورة باستخدام Java OCR. تعلم كيفية تحميل الصورة للتعرف
  الضوئي على الأحرف، وتكوين اللغة، وتشغيل دليل Java OCR كامل في دقائق.
draft: false
keywords:
- extract text from image
- load image for ocr
- use OCR in java
- java ocr tutorial
language: ar
og_description: استخراج النص من الصورة باستخدام Java OCR. يوضح هذا الدرس كيفية تحميل
  صورة للتعرف الضوئي على الأحرف، وتكوين اللغة، وتشغيل دليل Java OCR خطوة بخطوة.
og_title: استخراج النص من الصورة في جافا – دليل OCR الكامل
tags:
- OCR
- Java
- Image Processing
title: استخراج النص من الصورة في جافا – دليل OCR لجافا
url: /ar/java/ocr-basics/extract-text-from-image-in-java-java-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من الصورة في جافا – دليل OCR كامل

هل احتجت يومًا إلى **استخراج النص من صورة** لكن لم تكن متأكدًا من أين تبدأ في جافا؟ لست وحدك—المطورون يواجهون هذه المشكلة باستمرار عند تحويل العلامات الممسوحة ضوئيًا، الإيصالات، أو الملاحظات المكتوبة يدويًا إلى سلاسل قابلة للبحث.  

الخبر السار؟ في بضع دقائق فقط يمكنك الحصول على خط أنابيب OCR يعمل يقرأ الكانادا، الإنجليزية، أو أي لغة مدعومة. في هذا الدرس سنقوم **بتحميل الصورة لـ OCR**، ضبط المحرك، وسنتبع **دروس OCR في جافا** يمكنك نسخها ولصقها وتشغيلها اليوم.

## ما يغطيه هذا الدليل

سنبدأ بسرد الأدوات التي ستحتاجها، ثم ننتقل مباشرة إلى تنفيذ **خطوة بخطوة**. بحلول النهاية ستكون قادرًا على:

* تحميل ملف صورة إلى `ImageInputStream` في جافا.
* ضبط محرك OCR للتعرف على لغة محددة (الكانادا في مثالنا).
* تشغيل عملية التعرف وطباعة النص المستخرج.
* تعديل الإعدادات للحصول على دقة أفضل ومعالجة المشكلات الشائعة.

لا حاجة إلى وثائق خارجية—كل ما تحتاجه هنا.  

**المتطلبات المسبقة**: Java 17 أو أحدث، أداة بناء مثل Maven أو Gradle، ومكتبة OCR توفر فئة `OcrEngine` (على سبيل المثال، مجموعة أدوات *SimpleOCR* الافتراضية). إذا كنت تستخدم Maven، أضف الاعتماد الموضح لاحقًا.

---

## الخطوة 1 – إعداد مشروعك وإضافة مكتبة OCR

قبل كتابة أي كود، تأكد من أن مشروعك يستطيع رؤية فئات OCR. باستخدام Maven، ضع هذا المقتطف في ملف `pom.xml` الخاص بك:

```xml
<!-- Maven dependency for SimpleOCR (replace with your actual OCR SDK) -->
<dependency>
    <groupId>com.example</groupId>
    <artifactId>simple-ocr</artifactId>
    <version>1.4.2</version>
</dependency>
```

إذا كنت تفضل Gradle، المكافئ هو:

```gradle
implementation 'com.example:simple-ocr:1.4.2'
```

> **نصيحة احترافية:** حافظ على تحديث نسخة المكتبة؛ الإصدارات الأحدث غالبًا ما تتضمن تحسينات في نماذج اللغة التي تعزز الدقة.

بعد حل الاعتماد، قم بتحديث بيئة التطوير المتكاملة (IDE) وستكون جاهزًا للبرمجة.

## الخطوة 2 – استيراد الفئات المطلوبة

فيما يلي القائمة الكاملة للاستيرادات التي ستحتاجها في المثال. تم الحفاظ عليها بسيطة عمدًا لتتمكن من رؤية ما تقوم به كل فئة.

```java
import com.example.ocr.OcrEngine;      // Main OCR engine
import com.example.ocr.OcrResult;      // Holds recognition result
import com.example.io.ImageInputStream; // Wrapper for image files
import java.nio.file.Paths;             // Convenient path handling
import java.io.IOException;             // For proper exception handling
```

> **لماذا هذه الاستيرادات؟** `OcrEngine` و `OcrResult` هما قلب عملية OCR، بينما `ImageInputStream` ي抽象 عملية قراءة الملفات. استخدام `java.nio.file.Paths` يجعل الكود مستقلاً عن نظام التشغيل.

## الخطوة 3 – تحميل الصورة لـ OCR

الآن يأتي الجزء الذي يسبب مشاكل كثيرًا: تزويد المحرك بصيغة الصورة الصحيحة. يتوقع SDK الخاص بـ OCR `ImageInputStream`، ويمكنك الحصول عليه من أي ملف على القرص.

```java
// Step 3: Load the image that contains the text you want to extract
String imagePath = "YOUR_DIRECTORY/kannada_sign.jpg";
ImageInputStream imageStream = new ImageInputStream(Paths.get(imagePath));
```

> **حالة حافة:** إذا كانت الصورة تالفة أو بصيغة غير مدعومة (مثل GIF)، سيتسبب المُنشئ في رمي `IOException`. ضع الاستدعاء داخل كتلة try‑catch أو تحقق من صحة الملف مسبقًا.

## الخطوة 4 – ضبط المحرك للتعرف على لغة محددة

معظم محركات OCR تدعم تعدد اللغات. لتحسين الدقة يجب إخبار المحرك بالضبط أي لغة يبحث عنها. في مثالنا نستخدم رمز اللغة `"kn"` للكانادا.

```java
// Step 4: Create and configure the OCR engine for Kannada
OcrEngine ocrEngine = new OcrEngine();
ocrEngine.getConfig().setLanguage("kn"); // 'kn' = Kannada
```

> **لماذا ضبط اللغة؟** تحديد مجموعة الأحرف يقلل من الإيجابيات الزائفة، خاصةً عند التعامل مع خطوط تحتوي على العديد من الرموز المتشابهة.

إذا احتجت لتغيير اللغة، ما عليك سوى تعديل سلسلة الرمز—لا حاجة لتغييرات أخرى.

## الخطوة 5 – تشغيل عملية OCR واستخراج النص

مع تحميل الصورة وضبط المحرك، يصبح التعرف الفعلي استدعاءً واحدًا للطريقة. كائن النتيجة يمنحك النص العادي، واختياريًا درجات الثقة.

```java
// Step 5: Run OCR and retrieve the recognized text
OcrResult ocrResult = ocrEngine.recognize(imageStream);
String extractedText = ocrResult.getText();
```

> **سؤال شائع:** *ماذا لو أعاد OCR سلسلة فارغة؟*  
> عادةً ما يعني ذلك أن جودة الصورة منخفضة جدًا (ضبابية، تباين منخفض) أو أن اللغة لم تُضبط بشكل صحيح. جرّب معالجة الصورة مسبقًا (زيادة التباين، تحويل إلى ثنائي) أو تحقق مرة أخرى من رمز اللغة.

## الخطوة 6 – عرض النتيجة

أخيرًا، اطبع النتيجة على وحدة التحكم. في تطبيق حقيقي قد تخزنها في قاعدة بيانات أو تُدخلها في فهرس بحث.

```java
// Step 6: Output the recognized Kannada text
System.out.println("Extracted text:");
System.out.println(extractedText);
```

### النتيجة المتوقعة

إذا كانت الصورة المصدر تحتوي على العبارة الكانادية “ಕರ್ನಾಟಕ” (كارناتاكا)، يجب أن تظهر وحدة التحكم:

```
Extracted text:
ಕರ್ನಾಟಕ
```

هذا كل شيء—سير عمل كامل **لاستخدام OCR في جافا** يمكنك تكييفه مع أي لغة أو مصدر صورة.

---

## مثال كامل يعمل

فيما يلي البرنامج بالكامل، جاهز للترجمة. استبدل `YOUR_DIRECTORY` بالمسار الفعلي لملف الصورة.

```java
import com.example.ocr.OcrEngine;
import com.example.ocr.OcrResult;
import com.example.io.ImageInputStream;
import java.nio.file.Paths;
import java.io.IOException;

public class KannadaOcrExample {
    public static void main(String[] args) {
        try {
            // Create OCR engine instance
            OcrEngine ocrEngine = new OcrEngine();

            // Configure for Kannada (language code "kn")
            ocrEngine.getConfig().setLanguage("kn");

            // Load the image you want to extract text from
            String imagePath = "YOUR_DIRECTORY/kannada_sign.jpg";
            ImageInputStream imageStream = new ImageInputStream(Paths.get(imagePath));

            // Run the OCR process
            OcrResult ocrResult = ocrEngine.recognize(imageStream);

            // Print the extracted text
            System.out.println("Extracted text:");
            System.out.println(ocrResult.getText());
        } catch (IOException e) {
            System.err.println("Failed to load image or run OCR: " + e.getMessage());
        } catch (Exception e) {
            System.err.println("Unexpected error during OCR: " + e.getMessage());
        }
    }
}
```

> **نصيحة:** في الكود الإنتاجي، فكر في إعادة استخدام نسخة واحدة من `OcrEngine` عبر عدة صور؛ إنشاءها بشكل متكرر قد يكون مكلفًا.

---

## الأسئلة المتكررة وحالات الحافة

### كيف أحسن الدقة في الصور الضوضائية؟

- **معالجة مسبقة** للصورة: تحويلها إلى تدرج الرمادي، تطبيق تصفية متوسطة، أو زيادة التباين.
- **تغيير الحجم** لتكون الصورة على الأقل 300 DPI؛ معظم محركات OCR تتوقع هذه الدقة.
- **تحديد قائمة بيضاء** من الأحرف إذا كنت تعرف النتيجة المتوقعة (مثلاً أرقام فقط).

### هل يمكنني استخدام هذا النهج مع ملفات PDF؟

نعم. استخرج كل صفحة كصورة (باستخدام PDFBox أو iText)، ثم أدخل تلك الصور في نفس خط الأنابيب. يبقى الكود كما هو؛ فقط مصدر الصورة يتغير.

### ماذا لو احتجت للتعرف على عدة لغات في صورة واحدة؟

معظم مجموعات الأدوات SDK تسمح بتمرير قائمة مفصولة بفواصل، مثل `"en,kn"`. سيحاول المحرك مطابقة أي من النصوص المقدمة.

### هل هناك طريقة للحصول على درجات الثقة؟

`OcrResult` غالبًا ما يتضمن طريقة `getConfidence()` التي تُرجع قيمة عائمة بين 0 و 1 لكل سطر. استخدمها لتصفية النتائج ذات الثقة المنخفضة.

---

## الخطوات التالية

الآن بعد أن يمكنك **استخراج النص من الصورة** باستخدام جافا، قد ترغب في استكشاف:

* **معالجة دفعات** – تكرار عبر مجلد من الصور وكتابة النتائج إلى CSV.
* **التكامل مع Apache Tika** – دمج OCR مع تحليل المستندات لإنشاء فهرس بحث موحد.
* **واجهة برمجة تطبيقات على الخادم** – إتاحة منطق OCR عبر نقطة نهاية REST (Spring Boot يجعل ذلك سهلًا).
* **مكتبات بديلة** – جرّب Tesseract عبر `tess4j` إذا كنت تحتاج إلى حل مفتوح المصدر.

كل من هذه المواضيع يبني على المفاهيم الأساسية التي تم تغطيتها في **دروس OCR في جافا**، لذا لا تتردد في التجربة وتوسيع الكود.

---

## الخلاصة

لقد استعرضنا مثالًا كاملاً في جافا **يستخرج النص من الصورة**، موضحين بالضبط كيفية **تحميل الصورة لـ OCR**، ضبط إعدادات اللغة، و**استخدام OCR في جافا** للحصول على سلاسل قابلة للقراءة. المقتطف مستقل، يتعامل مع الأخطاء بسلاسة، ويمكن إدراجه في أي مشروع جافا بأقل جهد.  

جرّبه، عدّل رمز اللغة، وسرعان ما ستحول المستندات الممسوحة إلى بيانات قابلة للبحث دون عناء. برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}