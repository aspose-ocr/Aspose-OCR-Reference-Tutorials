---
category: general
date: 2026-02-09
description: تشغيل OCR على الصورة باستخدام Aspose OCR في Java – تعلّم كيفية استخراج
  النص من PNG وتمكين الكشف التلقائي عن لغة OCR في بضع خطوات فقط.
draft: false
keywords:
- run OCR on image
- extract text from PNG
- auto detect language OCR
- Aspose OCR Java
- Hindi OCR example
language: ar
og_description: قم بتشغيل OCR على الصورة فورًا. يوضح هذا الدليل كيفية استخراج النص
  من ملفات PNG وتمكين الكشف التلقائي عن اللغة في OCR باستخدام Aspose OCR للغة Java.
og_title: تشغيل OCR على الصورة باستخدام Java – دليل Aspose OCR الكامل
tags:
- OCR
- Java
- Aspose
title: تشغيل OCR على صورة باستخدام Java – دليل Aspose OCR الكامل
url: /ar/java/ocr-operations/run-ocr-on-image-with-java-complete-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تشغيل OCR على صورة باستخدام Java – دليل Aspose OCR الكامل

هل احتجت يومًا إلى **run OCR on image** للملفات ولكنك لم تكن متأكدًا من أين تبدأ؟ ربما لديك مجموعة من لقطات شاشة PNG تحتوي على نص هندي، وتتساءل إذا كان بإمكان Java استخراج الكلمات دون إعداد تعلم آلي ضخم. الخبر السار هو: يمكنك ذلك، وهو بسيط بشكل مدهش مع Aspose OCR.

في هذا الدرس سنستعرض مثالًا عمليًا ي **extracts text from PNG** الملفات، يوضح لك كيفية تمكين **auto detect language OCR**، ويزودك ببرنامج Java جاهز للتنفيذ. في النهاية ستحصل على مقتطف يعمل يطبع الأحرف الهندية إلى وحدة التحكم، وستفهم لماذا كل سطر مهم.

## ما ستحتاجه

- **Java Development Kit (JDK) 8** أو أحدث – يتم تجميع الكود مع أي نسخة حديثة.  
- مكتبة **Aspose.OCR for Java** – احصل على أحدث JAR من موقع Aspose أو Maven Central.  
- صورة نموذجية (`hindi_sample.png`) تحتوي على نص ديڤاناجاري – يمكنك إنشاء واحدة بأي أداة لقطة شاشة.  
- بيئة تطوير متكاملة أو محرر نص بسيط – أستخدم IntelliJ IDEA، لكن `javac` العادي يعمل جيدًا.

لا توجد خدمات خارجية، ولا مفاتيح API سحابية، فقط JAR محلي وصورة. بسيط، أليس كذلك؟

## الخطوة 1: إضافة Aspose OCR إلى مشروعك

أولاً، تأكد من أن JAR الخاص بـ Aspose OCR موجود في مسار الفئات (classpath). إذا كنت تستخدم Maven، أضف هذا الاعتماد:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check for the latest version -->
</dependency>
```

إذا كنت تفضل الطريقة اليدوية، قم بتنزيل `aspose-ocr-23.10.jar` وضعه في مجلد `libs/`، ثم قم بالترجمة باستخدام:

```bash
javac -cp "libs/*" LanguageExample.java
```

> **Pro tip:** احتفظ برقم نسخة الـ JAR في تعليق في أعلى ملف المصدر – يساعدك ذلك في المستقبل على تذكر أي واجهة API استهدفتها.

## الخطوة 2: إنشاء كائن محرك OCR

الآن نقوم بإنشاء الكائن الأساسي الذي يقوم بكل المعالجة الثقيلة. فكر في `OcrEngine` كالعقل وراء العملية.

```java
// Step 2: Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();
```

لماذا ننشئه هنا؟ يحتفظ المحرك بإعدادات التكوين (مثل اللغة) والموارد القابلة لإعادة الاستخدام، لذا فإن إنشائه مرة واحدة لكل تطبيق يقلل من الحمل الزائد.

## الخطوة 3: ضبط إعدادات اللغة (وتفعيل الاكتشاف التلقائي)

إذا كنت تعرف اللغة مسبقًا—مثل الهندية—يمكنك إخبار المحرك بالتركيز على ديڤاناجاري. هذا يعزز الدقة ويسرّع المعالجة.

```java
// Step 3a: Force Hindi (Devanagari) recognition
ocrEngine.getConfiguration().setLanguage(Language.HINDI);

// Step 3b (optional): Let the engine guess the language if you're unsure
ocrEngine.getConfiguration().setAutoDetectLanguage(true);
```

السطر `setAutoDetectLanguage(true)` هو مفتاح **auto detect language OCR**. عندما تزود المحرك بصورة متعددة اللغات، سيحاول تحديد كل نص تلقائيًا. هذا مفيد للمهام الدفعية حيث لا يمكنك وضع علامة يدوية على كل ملف.

## الخطوة 4: تشغيل OCR على صورة PNG

هنا حيث نقوم فعليًا **run OCR on image** للبيانات. طريقة `recognize` تقبل مسار ملف، تقرأ الـ bitmap، وتعيد كائن `RecognitionResult`.

```java
// Step 4: Perform OCR on the PNG file
RecognitionResult result = ocrEngine.recognize("YOUR_DIRECTORY/hindi_sample.png");
```

استبدل `YOUR_DIRECTORY` بالمسار الفعلي للمجلد. إذا لم يُعثر على الملف، ستطلق Aspose استثناءً واضحًا – لا حاجة لتخمين سبب الفشل لاحقًا.

## الخطوة 5: استرجاع وعرض النص المستخرج

أخيرًا، استخرج السلسلة المعترف بها من كائن النتيجة واطبعها. بالنسبة للهندية، سترى أحرف Unicode في وحدة التحكم، بشرط أن يدعم الطرفية UTF‑8.

```java
// Step 5: Output the recognized Hindi text
System.out.println("Hindi text:");
System.out.println(result.getText());
```

**المخرجات المتوقعة** (بافتراض أن الصورة النموذجية تقول “नमस्ते दुनिया”):

```
Hindi text:
नमस्ते दुनिया
```

إذا قمت بتمكين الاكتشاف التلقائي وكانت الصورة تحتوي على الإنجليزية أيضًا، فإن المخرجات ستشمل كلا النصين، مختلطة بشكل جميل.

## مثال كامل يعمل

فيما يلي البرنامج الكامل القابل للتنفيذ. انسخه إلى `LanguageExample.java`، عدل مسار الصورة، وستكون جاهزًا للبدء.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.enums.*;

public class LanguageExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Specify the language to be recognized (Hindi – Devanagari script)
        ocrEngine.getConfiguration().setLanguage(Language.HINDI);

        // Step 3: (Optional) Enable automatic fallback to language detection
        ocrEngine.getConfiguration().setAutoDetectLanguage(true);

        // Step 4: Run OCR on the input image
        RecognitionResult result = ocrEngine.recognize("YOUR_DIRECTORY/hindi_sample.png");

        // Step 5: Print the extracted Hindi text
        System.out.println("Hindi text:");
        System.out.println(result.getText());
    }
}
```

> **Note:** إذا كنت تستخدم بيئة تطوير متكاملة، تأكد من أن مسار بناء المشروع يتضمن JAR الخاص بـ Aspose OCR. في IntelliJ، اذهب إلى *File → Project Structure → Libraries* وأضف الـ JAR هناك.

## أسئلة شائعة وحالات خاصة

### ماذا لو كانت صورة PNG منخفضة الدقة؟

تنخفض دقة OCR بشكل حاد تحت 150 dpi. قم بتكبير الصورة باستخدام أداة مثل ImageMagick (`convert input.png -resize 200% output.png`) قبل تمريرها إلى المحرك. لا يزال علم `auto detect language OCR` يعمل، لكنك ستلاحظ أخطاءً أقل في التعرف.

### هل يمكنني معالجة صور متعددة في حلقة؟

بالطبع. ضع استدعاء `recognize` داخل حلقة `for`، وأعد استخدام نفس كائن `OcrEngine`. إعادة استخدام المحرك يتجنب إعادة تحميل نماذج اللغة في كل تكرار، مما يوفر الذاكرة ووقت المعالج.

```java
String[] files = {"img1.png", "img2.png", "img3.png"};
for (String file : files) {
    RecognitionResult r = ocrEngine.recognize(file);
    System.out.println("Text from " + file + ":");
    System.out.println(r.getText());
}
```

### كيف أتعامل مع الطرفيات غير Unicode؟

إذا كانت الطرفية تعرض رموزًا مشوشة، اضبط ترميز الملف إلى UTF‑8 عند تشغيل Java:

```bash
java -Dfile.encoding=UTF-8 -cp "libs/*" LanguageExample
```

### هل هناك طريقة للحصول على درجات الثقة؟

نعم. يحتوي `RecognitionResult` على `getConfidence()` التي تُعيد قيمة عائمة بين 0 و 1 لكل سطر مُعترف به. يمكنك التكرار على `result.getLines()` لاستخراج تلك القيم—مفيد لتصفية النتائج ذات الثقة المنخفضة.

## نصائح احترافية للاستخدام في الإنتاج

- **Cache language models**: إذا كنت تعالج آلاف الصور، حافظ على تشغيل المحرك طوال الدفعة.
- **Parallel processing**: ضع كل صورة داخل `Callable` ومررها إلى مجموعة خيوط. فقط تذكر أن المحرك غير آمن للمتعدد الخيوط؛ أنشئ نسخة لكل خيط.
- **Logging**: استخدم مسجلًا مناسبًا (SLF4J) بدلاً من `System.out.println` للمهام الكبيرة.
- **Memory management**: استدعِ `ocrEngine.dispose()` بعد الانتهاء لتحرير الموارد الأصلية.

## نظرة بصرية

![Run OCR on image example diagram](ocr_flow.png "Run OCR on image example diagram")

المخطط أعلاه يوضح التدفق: **run OCR on image → language configuration → auto detect language OCR (optional) → extract text from PNG**.

## الخاتمة

لقد عرضنا للتو كيفية **run OCR on image** للملفات باستخدام Aspose OCR للـ Java، وكيفية **extract text from PNG** باستخدام إعدادات خاصة باللغة، وكيفية تفعيل **auto detect language OCR** لسيناريوهات مرنة ومتعددة اللغات. عينة الكود الكاملة جاهزة للنسخ، التجميع، والتنفيذ—بدون خطوات مخفية، ولا خدمات خارجية.

هل أنت مستعد للتحدي التالي؟ جرّب استبدال `Language.HINDI` بـ `Language.AUTO` ومرر مستندًا متعدد النصوص، أو جرب إدخال PDF (Aspose OCR يدعم أيضًا PDF). يمكنك أيضًا دمج هذا المقتطف في نقطة نهاية REST باستخدام Spring Boot لتوفير OCR كخدمة ويب.

برمجة سعيدة، ولتكن صورك دائمًا قابلة للقراءة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}