---
category: general
date: 2026-02-17
description: 'دليل تحويل الصورة إلى نص في جافا: تعلم كيفية استخراج النص الأردي من
  صورة باستخدام Aspose OCR. مثال كامل للـ OCR في جافا متضمن.'
draft: false
keywords:
- image to text java
- how to extract text
- extract urdu text
- java ocr example
- load image ocr
language: ar
og_description: يظهر برنامج تعليمي لتحويل الصورة إلى نص بجافا كيفية استخراج النص الأردي
  من صورة باستخدام Aspose OCR. اتبع مثال جافا OCR الكامل خطوة بخطوة.
og_title: 'صورة إلى نص جافا: استخراج النص الأردي باستخدام Aspose OCR'
tags:
- OCR
- Java
- Aspose
title: 'تحويل الصورة إلى نص جافا: استخراج النص الأردي باستخدام Aspose OCR'
url: /ar/java/ocr-operations/image-to-text-java-extract-urdu-text-with-aspose-ocr/
---

.

Make sure to keep **bold** and *italic* formatting.

Lists translate.

Tables translate.

Code block placeholders remain.

Let's craft.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# image to text java: استخراج النص الأردي باستخدام Aspose OCR

إذا كنت بحاجة إلى تحويل **image to text java** للمستندات الأردية، فأنت في المكان الصحيح. هل تساءلت يوماً *كيف تستخرج النص* من صورة لملاحظة مكتوبة بخط اليد أو صفحة جريدة ممسوحة ضوئياً؟ سيوضح لك هذا الدليل **java ocr example** الذي يلتقط الأحرف الأردية مباشرةً من صورة باستخدام Aspose OCR.

سنتناول كل شيء بدءًا من ترخيص المكتبة وحتى طباعة النتيجة على وحدة التحكم. في النهاية ستتمكن من **load image ocr**، ضبط اللغة إلى الأردية، والحصول على ناتج Unicode نظيف—دون الحاجة إلى أدوات إضافية.  

## ما الذي ستحتاجه

- **Java Development Kit (JDK) 8+** – يعمل الكود على أي JDK حديث.
- **Aspose.OCR for Java** JAR (حمّله من موقع Aspose).  
- ملف ترخيص **Aspose OCR** صالح (`Aspose.OCR.lic`).  
- صورة تحتوي على نص أردي، مثل `urdu-sample.png`.  

وجود هذه الأساسيات يعني أنك تستطيع القفز مباشرة إلى الكود دون البحث عن تبعيات مفقودة.

## image to text java – إعداد Aspose OCR

أولاً، نحتاج إلى إخبار Aspose بأن لدينا ترخيصًا. بدون الترخيص تعمل المكتبة في وضع التقييم وستضيف علامات مائية إلى الناتج.

```java
import com.aspose.ocr.*;

public class UrduDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Apply the Aspose OCR license
        License license = new License();
        license.setLicense("Aspose.OCR.lic");
```

**لماذا هذا مهم:** الترخيص يزيل حد المعالجة لمدة 5 ثوانٍ ويفتح حزمة اللغة الأردية الكاملة التي أضيفت في الربع الثالث من 2025. إذا تخطيت هذه الخطوة، سيظل محرك OCR يعمل، لكنك سترى علامة “Evaluation” صغيرة في النتائج.

## كيفية استخراج النص – تهيئة محرك OCR

الآن ننشئ المحرك ونخبره صراحةً أننا نهتم بالأردية. ثابت `OcrLanguage.URDU` يُفعّل مجموعة الأحرف الصحيحة وقواعد التجزئة الخاصة بها.

```java
        // Step 2: Create the OCR engine and set the language to Urdu
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getLanguage().setLanguage(OcrLanguage.URDU); // added in 2025‑Q3
```

**نصيحة محترف:** إذا احتجت إلى معالجة لغات متعددة في تشغيل واحد، يمكنك تمرير قائمة مفصولة بفواصل، مثل `OcrLanguage.ENGLISH, OcrLanguage.URDU`. سيكتشف المحرك كل منطقة تلقائيًا.

## Load Image OCR – تحضير الإدخال

تعمل Aspose مع كائن `OcrInput` يمكنه حمل صورة واحدة أو عدة صور. هنا نقوم **load image ocr** للبيانات من ملف محلي.

```java
        // Step 3: Load the image that contains Urdu text
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/urdu-sample.png");
```

> **ملاحظة:** استبدل `YOUR_DIRECTORY` بالمسار المطلق أو المسار النسبي من جذر مشروعك. إذا لم يُعثر على الملف، ستطرح Aspose استثناء `FileNotFoundException`. فحص سريع باستخدام `new File(path).exists()` يمكن أن يوفر لك الكثير من وقت تصحيح الأخطاء.

## التعرف على النص – تشغيل عملية OCR

مع تكوين المحرك وتحميل الصورة، نستدعي أخيرًا `recognize`. تُعيد الطريقة كائن `OcrResult` يحتوي على السلسلة المستخرجة.

```java
        // Step 4: Recognize the text from the image
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);
```

**ماذا يحدث خلف الكواليس؟** يقوم محرك OCR بتقسيم الصورة إلى أسطر، ثم إلى أحرف، مطبقًا قواعد تشكيل خاصة بالأردية (مثل ربط الأشكال). لهذا السبب ضبط اللغة مبكرًا أمر حاسم؛ وإلا ستحصل على أحرف لاتينية مشوهة.

## طباعة النص الأردي المُعترف به

الخطوة الأخيرة هي ببساطة طباعة النتيجة. لأن الأردية تستخدم كتابة من اليمين إلى اليسار، تأكد من أن وحدة التحكم تدعم Unicode (معظم الطرفيات الحديثة تدعم ذلك).

```java
        // Step 5: Print the recognized Urdu text
        System.out.println("Urdu text:\n" + ocrResult.getText());
    }
}
```

**الناتج المتوقع (مثال):**

```
Urdu text:
یہ ایک مثال کا متن ہے جو تصویر سے نکالا گیا ہے۔
```

إذا رأيت علامات استفهام أو سلاسل فارغة، تحقق مرة أخرى من أن ترميز وحدة التحكم مضبوط على UTF‑8 (`chcp 65001` على Windows، أو شغّل Java مع `-Dfile.encoding=UTF-8`).

## مثال كامل يعمل – جميع الخطوات في مكان واحد

فيما يلي البرنامج الكامل جاهز للنسخ واللصق. لا مراجع خارجية، مجرد ملف Java واحد.

```java
import com.aspose.ocr.*;

public class UrduDemo {
    public static void main(String[] args) throws Exception {
        // Apply the Aspose OCR license
        License license = new License();
        license.setLicense("Aspose.OCR.lic");

        // Create the OCR engine and set the language to Urdu
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getLanguage().setLanguage(OcrLanguage.URDU); // added in 2025‑Q3

        // Load the image that contains Urdu text
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/urdu-sample.png");

        // Recognize the text from the image
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // Print the recognized Urdu text
        System.out.println("Urdu text:\n" + ocrResult.getText());
    }
}
```

شغّله باستخدام:

```bash
javac -cp "aspose-ocr-23.10.jar" UrduDemo.java
java -cp ".:aspose-ocr-23.10.jar" UrduDemo
```

استبدل نسخة الـ JAR (`23.10`) بأي نسخة قمت بتحميلها. يجب أن تعرض وحدة التحكم الجملة الأردية المستخرجة من ملف PNG الخاص بك.

## المشكلات الشائعة وحالات الحافة

| المشكلة | لماذا يحدث | كيفية الإصلاح |
|-------|----------------|------------|
| **ناتج فارغ** | الصورة داكنة جدًا أو بدقة منخفضة. | عالج الصورة مسبقًا (زيادة التباين، تحويلها إلى ثنائية) باستخدام `BufferedImage` قبل تمريرها إلى Aspose. |
| **أحرف غير مفهومة** | ضبط لغة خاطئ (اللغة الافتراضية هي الإنجليزية). | تأكد من استدعاء `ocrEngine.getLanguage().setLanguage(OcrLanguage.URDU);` قبل `recognize`. |
| **الترخيص غير موجود** | خطأ في كتابة المسار أو الملف مفقود. | استخدم مسارًا مطلقًا أو ضع ملف `.lic` في classpath واستدعِ `license.setLicense("Aspose.OCR.lic");`. |
| **نفاد الذاكرة على صور كبيرة** | ملفات PNG الكبيرة تستهلك الذاكرة. | استدعِ `ocrEngine.setMaxImageSize(2000);` لتقليل الحجم داخليًا، أو قم بتصغير الصورة بنفسك. |

## توسيع العرض التجريبي

- **معالجة دفعات:** حلق عبر مجلد، أضف كل ملف إلى نفس `OcrInput`، واجمع النتائج في ملف CSV.  
- **لغات مختلفة:** استبدل `OcrLanguage.URDU` بـ `OcrLanguage.ARABIC` أو اجمع عدة لغات.  
- **الحفظ إلى ملف:** استخدم `Files.write(Paths.get("output.txt"), ocrResult.getText().getBytes(StandardCharsets.UTF_8));`.  

جميع هذه الأفكار تُبنى على **java ocr example** الذي أنشأناه للتو، مما يتيح لك تخصيص الحل لمشاريع العالم الحقيقي.

## الخلاصة

أصبح لديك الآن سير عمل **image to text java** قوي لاستخراج الأحرف الأردية من صورة باستخدام Aspose OCR. غطى الدليل كل خطوة—من الترخيص واختيار اللغة إلى تحميل الصورة وطباعة النتيجة—حتى يمكنك لصق الكود في أي مشروع Java ومشاهدة النتيجة تعمل.

بعد ذلك، جرّب تجربة ملفات PDF أكبر، أو نصوصًا مختلفة، أو حتى دمج خطوة OCR في نقطة نهاية REST باستخدام Spring Boot. المبادئ نفسها—**how to extract text**, **load image o**  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}