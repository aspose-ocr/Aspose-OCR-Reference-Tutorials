---
category: general
date: 2026-03-28
description: تشغيل التعرف الضوئي على الحروف (OCR) على الصورة في جافا باستخدام Aspose
  OCR لتحويل الصورة إلى نص، واستخراج النص التايلاندي من PNG بسرعة وموثوقية.
draft: false
keywords:
- run OCR on image
- convert image to text
- extract text from PNG
- extract Thai text
- recognize Thai text
language: ar
og_description: قم بتشغيل OCR على الصورة باستخدام Java و Aspose OCR. تعلم كيفية تحويل
  الصورة إلى نص، استخراج النص التايلاندي من PNG، والتعامل مع المشكلات الشائعة.
og_title: تشغيل OCR على الصورة باستخدام Java – استخراج النص التايلاندي بسرعة
tags:
- OCR
- Java
- Aspose
- Image Processing
title: تشغيل OCR على صورة باستخدام Java – استخراج النص التايلندي من PNG
url: /ar/java/ocr-operations/run-ocr-on-image-with-java-extract-thai-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تشغيل OCR على الصورة باستخدام Java – دليل شامل

هل تساءلت يومًا كيف يمكنك **run OCR on image** للملفات مباشرةً من كود Java؟ ربما لديك مجموعة من إيصالات الـThai، أو مستندات ممسوحة ضوئيًا، أو لقطات شاشة وتحتاج إلى النص دون كتابته يدويًا. هذه مشكلة شائعة، خاصةً عندما يكون المصدر PNG واللغة غير لاتينية.  

في هذا الدليل سنوضح لك بالضبط كيفية **run OCR on image** باستخدام مكتبة Aspose OCR، تحويل الصورة إلى نص عادي، واستخراج الأحرف Thai بثقة. بنهاية القراءة ستتمكن من **convert image to text**، **extract text from PNG**، وحتى **recognize Thai text** ببضع أسطر من الكود فقط.

## ما يغطيه هذا الدرس

* إعداد تبعية Aspose OCR في مشروع Maven/Gradle.  
* تهيئة `OcrEngine` وتكوينها للغة Thai.  
* تشغيل OCR على ملف PNG ومعالجة الأخطاء المحتملة.  
* طباعة النتيجة إلى وحدة التحكم والتحقق من المخرجات.  

لا تحتاج إلى أي خبرة سابقة مع Aspose—فقط بيئة تطوير Java أساسية وملف صورة تريد معالجته.

## المتطلبات الأساسية

* Java 8 أو أحدث مثبت (المكتبة تعمل مع Java 11+ أيضًا).  
* أداة بناء – Maven أو Gradle (سنظهر مقتطف Maven).  
* رخصة Aspose OCR (الإصدار التجريبي المجاني يعمل للاختبار، لكن الرخصة تزيل حدود التقييم).  
* ملف PNG يحتوي على نص Thai، مثل `input.png` الموجود في مجلد الموارد في مشروعك.

---

## الخطوة 1: إضافة Aspose OCR إلى مشروعك

### Maven

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest version -->
</dependency>
```

### Gradle (Kotlin DSL)

```kotlin
implementation("com.aspose:aspose-ocr:23.9")
```

> **Pro tip:** حافظ على توافق إصدار المكتبة مع ملاحظات الإصدار الرسمية لـ Aspose؛ الإصدارات الأحدث تضيف حزم لغات وتحسينات في الأداء.

بمجرد حل التبعية، يجب أن يقوم IDE الخاص بك باستيراد الفئات المطلوبة تلقائيًا.

## الخطوة 2: تهيئة محرك OCR

المحرك هو قلب العملية – فكر فيه كـ “العقل” الذي يحلل أنماط البكسل. سنخبره أيضًا أننا نهتم فقط بالأحرف Thai.

```java
import com.aspose.ocr.*;

public class ThaiOcrDemo {
    public static void main(String[] args) throws Exception {
        // Step 2: Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Tell the engine to look for Thai language patterns
        ocrEngine.getRecognitionSettings().setLanguage("th");
```

لماذا نحدد اللغة صراحةً؟ لأن تحديد `"th"` يضيق مجموعة الأحرف، مما يسرّع التعرف ويقلل الأخطاء في قراءة الرموز المتشابهة.

## الخطوة 3: تشغيل OCR على ملف PNG

الآن نُمرّر للمحرك الصورة التي نريد فك تشفيرها. تُعيد طريقة `recognizeImage` كائن `OcrResult` يحتوي على السلسلة المستخرجة ودرجات الثقة.

```java
        // Step 3: Perform OCR on the target image
        String imagePath = "src/main/resources/input.png";
        OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);
```

إذا تعذر العثور على الملف، تقوم Aspose بإلقاء استثناء `FileNotFoundException`. من الجيد تغليف الاستدعاء داخل كتلة `try‑catch` في الكود الإنتاجي، لكن في هذا الدرس سنبقي الأمور بسيطة.

## الخطوة 4: إخراج النص المُعترف به

أخيرًا، نطبع النتيجة. تُعيد طريقة `getText()` سلسلة Java عادية `String` يمكنك تخزينها، إرسالها عبر الشبكة، أو كتابتها إلى ملف.

```java
        // Step 4: Display the extracted Thai text
        System.out.println("=== Recognized Thai Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

عند تشغيل البرنامج، يجب أن ترى شيئًا مشابهًا لـ:

```
=== Recognized Thai Text ===
สวัสดีครับ นี่คือข้อความจากรูปภาพ
```

إذا كان الإخراج مشوشًا، تحقق مرة أخرى من أن ملف PNG الأصلي عالي الدقة (على الأقل 300 dpi) وأن رمز اللغة `"th"` يطابق اللغة المستهدفة.

### القائمة الكاملة

فيما يلي ملف Java كامل جاهز للتنفيذ. انسخه والصقه في IDE الخاص بك، استبدل مسار الصورة إذا لزم الأمر، واضغط **Run**.

```java
import com.aspose.ocr.*;

public class ThaiOcrDemo {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Select Thai language for recognition
        ocrEngine.getRecognitionSettings().setLanguage("th");

        // Run OCR on the PNG image
        String imagePath = "src/main/resources/input.png";
        OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);

        // Output the recognized text
        System.out.println("=== Recognized Thai Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

![مثال تشغيل OCR على الصورة](image.png "مثال تشغيل OCR على الصورة – كود Java لاستخراج النص Thai من PNG")

## الخطوة 5: الاختلافات الشائعة وحالات الحافة

### تحويل الصورة إلى نص بصيغ أخرى

إذا كنت بحاجة إلى **convert image to text** لملف JPEG أو BMP، ما عليك سوى تغيير امتداد الملف في `imagePath`. تدعم Aspose OCR PNG، JPEG، BMP، TIFF، وحتى صفحات PDF.

### استخراج نص من PNG بعدة لغات

يمكنك طلب من المحرك اكتشاف عدة لغات في آنٍ واحد:

```java
ocrEngine.getRecognitionSettings().setLanguage("th,en");
```

ستحتوي النتيجة على مزيج من الأحرف Thai والإنجليزية، وهو مفيد للإيصالات الثنائية اللغة.

### معالجة الصور منخفضة الجودة

للمسحات الضبابية، فكر في تمكين المعالجة المسبقة:

```java
ocrEngine.getRecognitionSettings().setPreprocessMode(PreprocessMode.Auto);
```

هذا يُفعِّل خوارزميات إزالة الضوضاء وتعزيز التباين المدمجة، مما يحسّن خطوة **extract text from PNG**.

### تفعيل الترخيص

بدون ترخيص، تُضيف Aspose سطر علامة مائية في الإخراج بعد 100 صفحة. فعّل ترخيصك مبكرًا:

```java
License license = new License();
license.setLicense("Aspose.OCR.lic");
```

ضع ملف `.lic` بجوار ملف JAR أو أشر إليه عبر مسار مطلق.

## الأسئلة المتكررة

**س: هل يعمل هذا على Linux؟**  
ج: بالتأكيد. Aspose OCR مكتبة Java صافية، لذا أي نظام تشغيل متوافق مع JVM يعمل بشكل جيد.

**س: ماذا لو كان PNG يحتوي على كتابة يدوية Thai؟**  
ج: التعرف على الخط اليدوي محدود؛ قد تحتاج إلى نموذج شبكة عصبية مخصص. تتفوق Aspose OCR مع النص المطبوع.

**س: هل يمكنني معالجة مجموعة من الصور دفعة واحدة؟**  
ج: غلف استدعاء `recognizeImage` داخل حلقة على `Files.list(Paths.get("folder"))`. تذكر إعادة استخدام نفس كائن `OcrEngine` لتحسين الأداء.

## الخلاصة

لقد استعرضنا مثالًا كاملاً من البداية إلى النهاية حول كيفية **run OCR on image** في Java، خصوصًا لاستخراج النص Thai من PNG. من خلال تهيئة `OcrEngine`، ضبط اللغة، استدعاء `recognizeImage`، وطباعة النتيجة، لديك الآن طريقة موثوقة لـ **convert image to text** دون الاعتماد على خدمات طرف ثالث.

من هنا يمكنك:

* **extract text from PNG** ملفات بكميات كبيرة لمشاريع استخراج البيانات.  
* دمج مخرجات OCR مع واجهة برمجة تطبيقات ترجمة للحصول على ما يعادلها بالإنجليزية.  
* استكشاف لغات أخرى تدعمها Aspose، مثل الصينية أو العربية، عبر تغيير رمز اللغة.

جرّب ذلك مع صورك الخاصة—عدّل إعدادات المعالجة المسبقة، جرب صيغ ملفات مختلفة، وشاهد مدى قوة الحل في سير عملك الواقعي.

برمجة سعيدة، ولتكن خطوط OCR دقيقة دائمًا!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}