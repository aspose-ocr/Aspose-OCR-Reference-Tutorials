---
category: general
date: 2026-10-30
description: استخراج النص من الصورة باستخدام Aspose OCR Java – تعلم كيفية تحويل PNG
  إلى نص، تحميل الصورة لـ OCR، واتبع دليل OCR بلغة Java.
draft: false
keywords:
- convert png to text
- ocr image to text
- extract text from png
- aspose ocr java
- extract text image java
lastmod: 2026-10-30
og_description: استخراج النص من الصورة باستخدام Aspose OCR Java. اتبع هذا الدليل خطوة
  بخطوة لـ Java OCR لتحويل PNG إلى نص، تحميل الصورة لـ OCR، ومعالجة المحتوى متعدد
  اللغات بكفاءة.
og_image_alt: Screenshot of Java OCR code converting PNG to text using Aspose OCR
og_title: تحويل PNG إلى نص باستخدام Java OCR – دليل Aspose
schemas:
- author: Aspose
  dateModified: '2026-10-30'
  description: extract text from image using Aspose OCR Java – learn how to convert
    PNG to text, load image for OCR, and follow a java ocr tutorial.
  headline: Extract text from image – convert PNG to text in Java
  type: TechArticle
- questions:
  - answer: Yes, a commercial license is required for production use; a free trial
      is available for evaluation.
    question: Can I use Aspose OCR in a commercial application without extra licensing
      fees?
  - answer: Absolutely. The library includes language packs for Arabic, Hebrew, Persian,
      and other RTL scripts.
    question: Does Aspose OCR support right‑to‑left scripts such as Arabic or Hebrew?
  - answer: Aspose OCR can process images up to 10 000 × 10 000 pixels using streaming
      mode, which keeps memory usage under 200 MB.
    question: How large of an image can the engine handle?
  - answer: Yes, `OcrResult.getWords()` returns a collection where each word has a
      `getConfidence()` method.
    question: Is there a way to get confidence scores for each recognized word?
  - answer: The library supports JDK 8, 11, 17, and later LTS releases.
    question: What Java versions are officially supported?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
- Image Processing
title: استخراج النص من الصورة – تحويل PNG إلى نص في Java
url: /ar/java/ocr-basics/extract-text-from-image-convert-png-to-text-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من الصورة – تحويل PNG إلى نص في جافا

هل احتجت يومًا إلى **استخراج النص من الصورة** لكنك لم تكن متأكدًا أي مكتبة ستمكنك من ذلك دون عناء؟ لست وحدك—المطورون يسألون باستمرار: “كيف يمكنني تحويل PNG إلى نص في جافا؟” الخبر السار هو أن Aspose OCR يجعل العملية بأكملها كأنها نزهة في الحديقة. في هذا الدليل سنستعرض **java ocr tutorial** كامل، نوضح لك كيفية **load image for OCR**، وننتهي بنص نظيف وقابل للبحث.

سنغطي كل شيء من إعداد المحرك إلى التعامل مع المحتوى متعدد اللغات، بحيث في النهاية ستتمكن من **convert PNG to text** ملفات بأي حجم أو تنسيق أو لغة. لا خدمات خارجية، لا مفاتيح API—فقط ملف JAR واحد وقليل من أسطر الكود.

## إجابات سريعة
- **What library can convert PNG to text in Java?** Aspose OCR for Java.
- **How many lines of code are needed for a basic conversion?** حوالي خمس أسطر بعد إضافة المكتبة.
- **Does Aspose OCR support languages beyond English?** نعم—أكثر من 70 حزمة لغة، بما في ذلك الخميرية، الصينية، العربية، وأكثر.
- **Can I run the OCR engine offline?** بالتأكيد؛ يعمل المحرك بالكامل محليًا دون اتصال بالإنترنت.
- **What Java version is required?** JDK 8 أو أحدث؛ JDK 11+ مدعوم بالكامل.

## ما هو تحويل PNG إلى نص؟
**Convert PNG to text** يعني استخراج الأحرف النصية التي تظهر داخل صورة PNG وتحويلها إلى سلسلة نصية عادية يمكنك تعديلها أو البحث فيها أو تخزينها. تُعرف هذه العملية عادةً بالتعرف الضوئي على الأحرف (OCR). تعمل عن طريق تحليل أنماط البكسل ومطابقتها مع القواميس الخاصة بكل لغة، مما يسمح بتحويل المستندات الممسوحة، لقطات الشاشة، أو أي صورة نقطية تحتوي على نص قابل للقراءة إلى بيانات قابلة للتحرير.

## لماذا تستخدم Aspose OCR لجافا؟
يدعم Aspose OCR **50+ input formats** (بما في ذلك PNG و JPEG و BMP و TIFF) ويمكنه معالجة **multi‑hundred‑page documents** دون تحميل الملف بالكامل إلى الذاكرة، بفضل بنية البث الخاصة به. توفر المكتبة **70+ language packs**، وتحقق حتى **95 % accuracy** على المسحات عالية الدقة، وتتلقى تحديثات شهرية تضيف خطوطًا جديدة وتحسينات في الأداء.

## ما ستحتاجه
- JDK 8 أو أحدث مثبت (الكود يعمل على JDK 11+ أيضًا).  
- Maven أو Gradle لجلب مكتبة Aspose OCR، أو يمكنك تنزيل ملف JAR يدويًا من موقع Aspose.  
- صورة PNG تحتوي على نص قابل للقراءة (في مثالنا سنستخدم `khmer-sign.png`).  
- بيئة تطوير متكاملة أو محرر نصوص تشعر بالراحة معه—IntelliJ IDEA، Eclipse، VS Code، أيًا كان.

هذا كل شيء. لا أطر عمل ثقيلة، لا بيانات اعتماد سحابية. جاهز؟ لنبدأ باستخراج النص من ملفات الصور.

## كيف تضيف Aspose OCR إلى مشروعك؟
أضف محرك OCR إلى تكوين البناء الخاص بك بحيث تكون الفئات متاحة وقت التجميع. تضمن هذه الخطوة أن يتم الإشارة إلى ملف JAR الخاص بـ Aspose OCR واعتمادياته بشكل صحيح، مما يسمح لك باستيراد الحزم اللازمة في ملفات مصدر جافا. بمجرد إعلان الاعتماد، سيقوم Maven أو Gradle بتنزيل المكتبة من المستودع المركزي ووضعها على مسار الفئة للتجميع والتنفيذ.

**Maven** – أضف هذا الاعتماد إلى `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check the latest version on Maven Central -->
</dependency>
```

**Gradle** – أضف السطر التالي إلى `build.gradle` الخاص بك:

```groovy
implementation 'com.aspose:aspose-ocr:23.10'
```

إذا كنت تفضل الطريقة اليدوية، قم بتنزيل ملف JAR من صفحة تحميل Aspose وضعه في مجلد `libs` الخاص بمشروعك، ثم أضفه إلى مسار البناء.

> **Pro tip:** احرص دائمًا على اختيار أحدث نسخة مستقرة؛ الإصدارات القديمة قد تفتقد حزم اللغات أو تصحيحات الأخطاء.

## كيف تنشئ مثيل محرك OCR؟
OcrEngine هو الفئة الأساسية التي تقوم بالتعرف الضوئي على الأحرف. إنه يضم جميع المخازن الداخلية، بيانات اللغة، وإعدادات المعالجة المطلوبة لتحويل بكسلات الصورة إلى نص. إنشاء مثيل جديد لكل عملية يضمن نتائج حتمية، خاصة عندما تقوم بتبديل اللغات أو أوضاع المعالجة بين التشغيلات.

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

لماذا ننشئ محركًا جديدًا في كل مرة؟ لأن المحرك يخزن قواميس اللغات في الذاكرة؛ إعادة تعيينه يمنع التلوث المتبادل بين عمليات المسح للغات المختلفة.

## كيف تمكّن اللغة المطلوبة (اختياري لكن موصى به)؟
OcrLanguage يمثل قاموس لغة محدد يستخدمه المحرك أثناء التعرف. اختيار اللغة المناسبة يقلل من مساحة البحث، يسرّع المعالجة، ويحسن الدقة من خلال التركيز على مجموعة الأحرف المتوقعة في الصورة.

`OcrLanguage` يمثل قاموس لغة محدد. في مثالنا سنمكّن الخميرية (`khm`)، لكن يمكنك استبداله بـ `ENG` للإنجليزية، `CHN` للصينية، إلخ.

```java
// Enable Khmer language support (ISO 639‑2 code "khm")
ocrEngine.getLanguages().add(OcrLanguage.KHM);
```

> **Why this matters:** عندما **load image for OCR**، سيبحث المحرك فقط في القواميس اللغوية الممكّنة. ترك جميع اللغات مفعلة قد يبطئ العملية ويزيد من الإيجابيات الكاذبة.

## كيف تحمل صورة لـ OCR – تحويل PNG إلى نص
ImageStream هو غلاف يقرأ ملف الصورة إلى تدفق متوافق مع محرك OCR، مع معالجة اكتشاف الصيغة تلقائيًا.

`ImageStream` هو غلاف يقرأ ملف الصورة إلى تدفق متوافق مع محرك OCR، مع معالجة اكتشاف الصيغة تلقائيًا.

```java
// Load the PNG that contains the text you want to extract
ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/khmer-sign.png"));
```

إذا كانت صورتك بصيغة أخرى (JPEG، BMP، TIFF)، تعمل نفس الطريقة—Aspose يكتشف الصيغة تلقائيًا. فقط تأكد من صحة مسار الملف؛ وإلا ستواجه `FileNotFoundException`.

## كيف تشغّل عملية OCR وتحول PNG إلى نص؟
OcrResult يحمل نتيجة عملية التعرف، بما في ذلك النص المستخرج ومقاييس الثقة لكل حرف أو كلمة. بعد استدعاء طريقة `recognize()` على المحرك، تحصل على كائن OcrResult يمكنك الاستعلام عنه للحصول على السلسلة الخام وتفاصيل إضافية.

`ocrEngine.recognize()` تُعيد `OcrResult` التي تحتوي على `getText()` للنص المستخرج و`getConfidence()` لمقياس الثقة لكل حرف.

```java
// Run OCR and fetch the recognized text
String recognizedText = ocrEngine.recognize().getText();
```

هذا كل شيء—لقد **convert PNG to text** الآن. قد يحتوي النص المُرجع على فواصل أسطر ومسافات بيضاء تمامًا كما رآها المحرك. يمكنك معالجته لاحقًا باستخدام `trim()`، `replaceAll("\\s+", " ")`، أو أي تنظيف آخر تحتاجه.

## كيف تخرج النتيجة (أو تخزنها)؟
Result هو مثيل من OcrResult يوفر النص المعترف به عبر `getText()`. طباعة النتيجة إلى وحدة التحكم طريقة سريعة للتحقق من نجاح OCR، بينما في الإنتاج قد تكتب النص إلى ملف أو قاعدة بيانات أو خدمة أخرى.

`System.out.println(result.getText());` يطبع النص المستخرج.

```java
System.out.println("Recognized text:");
System.out.println(recognizedText);
```

**Expected output** (للإشارة الخميرية المقدمة) قد يبدو هكذا:

```
សួស្តី
Welcome
```

إذا كان الإخراج مشوشًا، تحقق مرة أخرى من أنك مكنت اللغة الصحيحة في الخطوة 3 وأن الصورة ليست ضبابية جدًا. زيادة دقة الصورة (مثلاً باستخدام مسح 300 dpi) غالبًا ما يساعد.

## كيف يبدو مثال كامل يعمل؟
فيما يلي برنامج جافا مستقل يوضح كل خطوة من إضافة الاعتماد إلى طباعة نتيجة OCR. يحتوي الصف `ExtractTextExample` على طريقة `main` التي تنشئ المحرك، تضبط اللغة، تحمل الصورة، تشغّل التعرف، وتطبع النص. يمكنك نسخ هذا الكود إلى ملف باسم `ExtractTextExample.java` وتشغيله مباشرة.

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

سترى النص المستخرج يُطبع على وحدة التحكم، مؤكدًا أنك نجحت في **extract text from image** باستخدام Aspose OCR.

## المشكلات الشائعة وكيفية إصلاحها
| العَرَض | السبب المحتمل | الحل |
|---------|--------------|-----|
| إرجاع سلسلة فارغة | عدم تمكين لغة أو رمز لغة غير صحيح | أضف `OcrLanguage` المناسب (مثال: `ENG` للإنجليزية). |
| أحرف مشوشة | دقة الصورة منخفضة جدًا أو خلفية صاخبة | استخدم مصدرًا بدقة أعلى، أو عالج مسبقًا بفلتر شحذ. |
| `OutOfMemoryError` | تحميل صورة كبيرة جدًا بالحجم الكامل | قلل حجم الصورة قبل تمريرها إلى المحرك (`ImageStream.fromFile(...).scale(0.5)`). |
| `FileNotFoundException` | مسار غير صحيح | تحقق من المسار المطلق أو النسبي؛ استخدم `Paths.get(...).toAbsolutePath()`. |

> **Remember:** OCR عملية احتمالية. حتى مع الإعدادات المثالية قد تحتاج إلى تصحيح يدوي لبعض الأحرف، خاصةً للخطوط المتصلة.

## ما هي الخطوات التالية التي يمكنك اتخاذها بعد هذا الدرس؟
- **Batch processing:** تكرار عبر دليل يحتوي على ملفات PNG، واستدعاء نفس المنطق لكل صورة.  
- **PDF output:** استخدم Aspose PDF لإدراج النص المستخرج مرة أخرى في PDF قابل للبحث.  
- **Language detection:** استدعِ `ocrEngine.detectLanguage()` قبل ضبط اللغة لتمكين المحرك من التخمين تلقائيًا.  
- **Cloud integration:** غلف الكود في نقطة نهاية REST ودع الخدمات المصغرة تستدعيه لتوفير خدمات OCR قابلة للتوسع.

كل هذه المواضيع تبني بطبيعتها على **java ocr tutorial** الذي أتممناه للتو، وتظهر مدى مرونة Aspose OCR API فعلاً.

## الأسئلة المتكررة

**Q: هل يمكنني استخدام Aspose OCR في تطبيق تجاري دون رسوم ترخيص إضافية؟**  
A: نعم، يلزم الحصول على ترخيص تجاري للاستخدام في الإنتاج؛ نسخة تجريبية مجانية متاحة للتقييم.

**Q: هل يدعم Aspose OCR النصوص من اليمين إلى اليسار مثل العربية أو العبرية؟**  
A: بالتأكيد. تشمل حزم اللغة العربية، العبرية، الفارسية، وغيرها من النصوص RTL.

**Q: ما هو أقصى حجم صورة يمكن للمحرك معالجته؟**  
A: يمكن لـ Aspose OCR معالجة صور تصل إلى 10 000 × 10 000 بكسل باستخدام وضع البث، مما يبقي استهلاك الذاكرة تحت 200 ميغابايت.

**Q: هل هناك طريقة للحصول على درجات الثقة لكل كلمة تم التعرف عليها؟**  
A: نعم، `OcrResult.getWords()` تُعيد مجموعة حيث لكل كلمة طريقة `getConfidence()`.

**Q: ما إصدارات جافا المدعومة رسميًا؟**  
A: تدعم المكتبة JDK 8، 11، 17، والإصدارات LTS الأحدث.

## الخاتمة
لقد استعرضنا دليلًا كاملًا **java ocr tutorial** يتيح لك **extract text from image**، **convert PNG to text**، وتحمّل الصورة بشكل صحيح لـ OCR باستخدام Aspose OCR. الخطوات بسيطة: أضف المكتبة، أنشئ محركًا، مكن اللغة المناسبة، حمّل PNG، شغّل `recognize()`، وتعامل مع النتيجة. بهذه الأساسيات يمكنك أتمتة إدخال البيانات، بناء أرشيفات قابلة للبحث، أو تشغيل أي تطبيق يحتاج نصًا قابلًا للقراءة من الصور.

جرّبه مع صورك الخاصة—ربما لقطة شاشة لإيصال أو عقد ممسوح. عدّل إعدادات اللغة، جرب الدقة، وسترى بسرعة مرونة الحل. إذا واجهت أي مشكلة، راجع جدول المشكلات أو تحقق من وثائق Aspose الرسمية؛ فهي شاملة ومحدثة باستمرار.

Happy coding, and may your next project be full of clean, searchable text!

**آخر تحديث:** 2026-10-30  
**تم الاختبار مع:** Aspose OCR for Java 24.10  
**المؤلف:** Aspose

## دروس ذات صلة

- [استخراج النص من صورة جافا تحميل صورة لـ OCR](/ocr/java/ocr-operations/extract-text-from-image-java-load-image-for-ocr/)
- [مثال Aspose OCR جافا تحويل الصورة إلى نص بسرعة](/ocr/java/ocr-operations/aspose-ocr-java-example-convert-image-to-text-fast/)
- [معالجة دفعة صور OCR في جافا استخراج النص من ملفات PNG بسرعة](/ocr/java/ocr-operations/batch-image-ocr-in-java-extract-text-from-png-files-fast/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}